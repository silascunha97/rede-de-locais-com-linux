# D06 — NAT e firewall em roteador Linux (Módulo M09, complementar)

Voltar: [README dos laboratórios](../README.md) · [Módulo 09](../../../modulos/modulo-09-nat-firewall.md)

**Problema:** `pc` (rede interna 192.0.2.0/24) precisa acessar o servidor `srv` (rede externa 203.0.113.0/24). O `srv` **não conhece** a rede interna. Resolver com NAT e depois restringir com firewall.

**Arquivo:** [compose.yaml](compose.yaml). `gw` 192.0.2.254 / 203.0.113.254 com `ip_forward=1`; `pc` .10 com rota padrão via `gw`; `srv` 203.0.113.10 (nginx) com a rota padrão do Docker removida (senão a resposta escaparia pelo gateway do Docker; achado nº 5). `NET_ADMIN` em `pc`/`srv` serve só para `ip route`; em `gw`, também para `iptables`.

```powershell
cd laboratorios\docker\d06-nat-firewall
docker compose up -d
docker compose exec srv ip route
docker compose exec gw iptables -t nat -L -n -v
```
**Observado:** `srv` só tem `203.0.113.0/24 dev eth0`; a tabela NAT está vazia.

## 1. Sem NAT (falha esperada)
```powershell
docker compose exec pc curl -s -m 3 -o /dev/null -w '%{http_code}\n' http://203.0.113.10/
```
**Observado:** `000` (timeout). Diagnóstico: o pedido chega ao `srv` com origem 192.0.2.10 e o `srv` não tem rota de volta. Prove com `docker compose exec srv tcpdump -nn -c 2 -i any port 80` (em outro terminal).

## 2. Mascaramento
```powershell
docker compose exec gw iptables -t nat -A POSTROUTING -s 192.0.2.0/24 -d 203.0.113.0/24 -j MASQUERADE
docker compose exec pc curl -s -m 3 -o /dev/null -w '%{http_code}\n' http://203.0.113.10/
docker compose logs srv
docker compose exec gw conntrack -L
```
**Observado:** `200`; o log do nginx mostra origem **203.0.113.254** (o `gw`), não 192.0.2.10. O `conntrack` mostra a tradução. A regra usa origem/destino, e **não** `-o ethX`, porque o nome da interface não é estável.

## 3. Firewall
```powershell
docker compose exec gw iptables -A FORWARD -s 192.0.2.0/24 -p tcp --dport 80 -j DROP
docker compose exec pc curl -s -m 3 -o /dev/null -w '%{http_code}\n' http://203.0.113.10/
docker compose exec pc ping -c 1 203.0.113.10
docker compose exec gw iptables -L FORWARD -n -v
```
**Observado:** `curl` → `000`; o `ping` continua respondendo; o contador da regra DROP ficou > 0 (3 pacotes na execução). Remoção: `docker compose exec gw iptables -D FORWARD -s 192.0.2.0/24 -p tcp --dport 80 -j DROP`.

## 4. Sentido inverso
`docker compose exec srv curl -m 3 http://192.0.2.10/`: previsão (**não registrada**): falha imediata (rede inalcançável). Explique com a Q9.2.

## Limpeza
```powershell
docker compose down -v
```
As regras de `iptables` vivem no container `gw` e somem com ele; nada altera o host nem a VM.

## Limites
`iptables` aqui é a variante `nf_tables`. As regras **não persistem** (reinício do container). O Docker não roteia entre as duas redes: o `gw` é quem o faz.
