# D04 — Roteador Linux entre duas sub-redes (Módulos M05 e M06)

Voltar: [README dos laboratórios](../README.md) · [M05](../../../modulos/modulo-05-ipv4-subredes.md) · [M06](../../../modulos/modulo-06-roteamento.md)

**Problema:** `host_a` (192.0.2.10/24) e `host_b` (198.51.100.10/24) estão em redes Docker diferentes. O Docker **não** as interliga. Construir a comunicação com um roteador explícito e depois quebrá-la.

**Arquivo:** [compose.yaml](compose.yaml). O `router` tem uma interface em cada rede (192.0.2.254 e 198.51.100.254) e `ip_forward=1`. Os hosts recebem a rota estática para a outra rede via `router`. As redes são bridge **comuns** (não `internal`): ver o [README geral](../README.md). Consequência: cada host também tem uma rota padrão via o `.1` do Docker; as rotas estáticas, mais específicas, têm precedência.

```powershell
cd laboratorios\docker\d04-roteador
docker compose up -d
```
## Parte A — endereçamento e gateway (M05)
```powershell
docker compose exec host_a ip -br addr
docker compose exec host_a ip route
docker compose exec router ip -br addr
```
**Observado:** em `host_a`: `default via 192.0.2.1`, `192.0.2.0/24 dev eth0`, `198.51.100.0/24 via 192.0.2.254`. Perguntas: por que o roteador precisa de **duas** interfaces em redes diferentes? Por que a ordem `eth0/eth1` no `router` não é garantida (confira nas suas execuções)?

## Parte B — roteamento (M06)
```powershell
docker compose exec host_a ping -c 2 198.51.100.10
docker compose exec host_a traceroute -n -m 4 198.51.100.10
```
**Observado:** 0% de perda; `traceroute`: salto 1 = `192.0.2.254`, salto 2 = `198.51.100.10`.

**Captura no roteador** (dois terminais): no 1º `docker compose exec router tcpdump -i any -nn -e icmp`; no 2º, o `ping`. **Observado:** `eth0 In … echo request` seguido de `eth1 Out … echo request` (o nome da interface pode inverter no seu caso).

## Falha 1 — falta a rota de volta
```powershell
docker compose exec host_b ip route del 192.0.2.0/24
docker compose exec host_a ping -c 2 -W 1 198.51.100.10
```
**Observado:** 100% de perda. Na captura do roteador, o pedido entra e sai; **nenhuma resposta** retorna por ele. Diagnóstico: `docker compose exec host_b ip route` mostra apenas `default via 198.51.100.1` (gateway do Docker) e a rede local: a resposta vai ao gateway errado. Correção:
```powershell
docker compose exec host_b ip route add 192.0.2.0/24 via 198.51.100.254
docker compose exec host_a ping -c 1 198.51.100.10
```
**Observado:** voltou a responder.

## Falha 2 — host sem a rota de ida
```powershell
docker compose exec host_a ip route del 198.51.100.0/24
docker compose exec host_a traceroute -n -w 1 -m 3 198.51.100.10
```
**Observado:** salto 1 = `192.0.2.1` (gateway do Docker), depois `* * *`. Correção: `ip route add 198.51.100.0/24 via 192.0.2.254`.

## Falha 3 — roteador sem encaminhamento
`sysctl -w` **falha** no container (`/proc/sys` somente leitura). Recrie o container com o valor alterado:
```powershell
docker compose down
# edite compose.yaml: net.ipv4.ip_forward: "0"
docker compose up -d
docker compose exec router cat /proc/sys/net/ipv4/ip_forward
docker compose exec host_a ping -c 1 -W 1 198.51.100.10
```
(Com `tcpdump -i any -nn icmp` no roteador, em outro terminal.) **Observado:** `ip_forward = 0`; o pedido **entra** no roteador (`In`) e **não sai**. Restaure `"1"` ao terminar.

## Limpeza
`docker compose down -v` e confirme que o `compose.yaml` voltou a `ip_forward: "1"`.

## Limites e comparação com o Packet Tracer
O roteador aqui é o **kernel Linux**; no PT é IOS (`show ip route`). Não há roteamento dinâmico. O gateway `.1` do Docker e o reencaminhamento pelo host tornam o isolamento diferente de uma LAN física (achado nº 5 em [fontes-e-referencias.md](../../../docs/fontes-e-referencias.md#4-achados-técnicos-que-corrigem-o-rascunho-anterior)).
