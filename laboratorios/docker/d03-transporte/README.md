# D03 — TCP × UDP (Módulo M04)

Voltar: [README dos laboratórios](../README.md) · [Módulo 04](../../../modulos/modulo-04-transporte.md)

**Problema:** dois serviços no mesmo host, porta TCP 5000 e UDP 5001. Mostrar, por captura, o que o TCP faz e o UDP não faz.

**Arquivo:** [compose.yaml](compose.yaml). `srv` 192.0.2.10 executa `nc -lk 5000` (TCP) e `nc -lku 5001` (UDP); `cli` 192.0.2.100. O `nc` é o **OpenBSD netcat** da netshoot (`nc -h` para as flags).

```powershell
cd laboratorios\docker\d03-transporte
docker compose up -d
docker compose exec srv ss -tuln
```
**Observado:** `tcp LISTEN 0.0.0.0:5000` e `udp UNCONN 0.0.0.0:5001` (mais o DNS embutido em 127.0.0.11: ignore).

## TCP
```powershell
docker compose exec cli sh -c 'tcpdump -i eth0 -nn -c 7 "port 5000" & sleep 1; echo oi | nc -N srv 5000; wait'
```
**Observado (7 pacotes):** `[S]` → `[S.]` → `[.]` (handshake), `[P.]` de 3 bytes (`oi` + newline) seq 1:4, `ack 4` do servidor, depois `[F.]` de ambos. Verifique que o ACK do SYN+ACK é `seq inicial + 1`.

## UDP
```powershell
docker compose exec cli sh -c 'tcpdump -i eth0 -nn -c 1 "port 5001" & sleep 1; echo oi | nc -u -w1 srv 5001; wait'
```
**Observado:** **um** pacote `UDP, length 3`; sem handshake nem confirmação. Use `-c 1`: com `-c 2` o comando trava, pois só existe 1 pacote.

## Falha controlada
```powershell
docker compose stop srv
docker compose exec cli sh -c 'echo oi | nc -N -w2 srv 5000; echo "exit=$?"'
docker compose exec cli sh -c 'echo oi | nc -u -w1 srv 5001; echo "exit=$?"'
```
Previsão (**não executada por mim**): o TCP falha de imediato (recusa/`RST`; confirme por captura); o UDP "parece funcionar", sem erro visível. Registre o real e explique por que o UDP não informa a falha. Depois: `docker compose start srv`. Obs.: com o container parado o nome `srv` pode nem resolver; registre o que ocorrer.

## Limpeza
`docker compose down -v`

**Limite:** não há perda nem congestionamento nesta rede virtual; retransmissão e janelas só podem ser **provocadas** com `tc netem` (extensão opcional, exige `NET_ADMIN`, **não testada aqui**).
