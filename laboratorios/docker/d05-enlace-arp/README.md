# D05 — ARP e vizinhos na mesma bridge (Módulo M07)

Voltar: [README dos laboratórios](../README.md) · [Módulo 07](../../../modulos/modulo-07-enlace-switching.md)

**Problema:** como `h1` descobre o MAC de `h2`, e o que `h3` (também na rede) consegue ver?

**Arquivo:** [compose.yaml](compose.yaml): `h1` 192.0.2.11, `h2` .12, `h3` .13 (o `.1` é do Docker).
```powershell
cd laboratorios\docker\d05-enlace-arp
docker compose up -d
docker compose exec h1 ip neigh
```
**Observado:** tabela de vizinhos vazia no início.

## Teste
```powershell
docker compose exec h1 sh -c 'tcpdump -i eth0 -nn -e -c 4 arp or icmp & sleep 1; ping -c1 192.0.2.12 >/dev/null; wait'
docker compose exec h1 ip neigh
docker compose exec h2 ip -br link show eth0
```
**Observado:** `Request who-has 192.0.2.12 tell 192.0.2.11` com destino `ff:ff:ff:ff:ff:ff` (broadcast), que **apareceu duplicado** na captura (hipótese não verificada: investigue); `Reply … is-at <MAC de h2>` em unicast; depois o ICMP já com o MAC de `h2`. `ip neigh` passou a ter `192.0.2.12 … REACHABLE`, e o MAC coincide com o `link/ether` de `h2`.

## Quem vê o quê
Em um terminal: `docker compose exec h3 tcpdump -nn -c 3 icmp`; em outro, `h1` pinga `h2`. **Observado:** `h3` **não** viu o ICMP unicast entre h1 e h2. Se `h3` vê o ARP request (broadcast), confira: **não registrei**.

## Falha controlada
`docker compose exec h1 ip neigh flush all` e repita o ping com captura: o ARP recomeça. Variante: `ping -c1 -W1 192.0.2.99` (inexistente); previsão (**não executada**): `ip neigh` mostra `FAILED`/`INCOMPLETE` e o ping falha com "Destination Host Unreachable".

## Limpeza
`docker compose down -v`

## Limites
A bridge Linux aprende MACs (`bridge fdb`, no host/VM), mas **não** é um switch gerenciável: sem `show mac address-table`, sem portas físicas, sem VLAN. A tabela MAC de um switch é estudada no [PT-07](../../packet-tracer/pt-07-arp-switch.md).
