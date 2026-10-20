# D01 — Encapsulamento em uma rede bridge (Módulo M02)

Voltar: [README dos laboratórios](../README.md) · [Módulo 02](../../../modulos/modulo-02-camadas-encapsulamento.md)

**Problema:** um cliente acessa um servidor web na mesma sub-rede. Quais endereços (MAC, IP, porta) e flags aparecem na rede, e em que ordem?

**Arquitetura:** rede `lan` 192.0.2.0/24 (`internal: true`); `web` (nginx) 192.0.2.10; `cli` (netshoot) 192.0.2.100. Sem portas publicadas. Arquivo: [compose.yaml](compose.yaml).

## 1–3. Pré-requisitos, preparação, inicialização
```powershell
cd laboratorios\docker\d01-encapsulamento
docker compose up -d
docker compose ps
```
## 4. Inspeção da topologia
```powershell
docker network ls
docker network inspect d01_lan
docker compose exec cli ip -br addr
docker compose exec cli ip route
```
Anote: qual o IP do gateway da rede (`Gateway` no inspect)? Por que `cli` não o usa para falar com `web`?

## 5. Teste e captura
```powershell
docker compose exec cli sh -c 'tcpdump -i eth0 -nn -e -c 12 port 80 & sleep 1; curl -s http://web/ -o /dev/null; wait'
docker compose exec cli getent hosts web
docker compose exec cli ip neigh
```
**Resultado observado (execução de 2026-10-20; MACs/portas variam):** 12 pacotes: `S`, `S.`, `.` (handshake); `P.` com a requisição (133 bytes) e a resposta; `F.` de ambos os lados. Cada linha mostra `MAC origem > MAC destino`, `ethertype IPv4`, IPs, porta 80 e flags. `getent hosts web` → `192.0.2.10`. `ip neigh` mostra o MAC do `web` como `REACHABLE`.

**O que observar:** (a) os MACs são os dos containers e **não mudam** durante a troca, pois não há roteador; (b) a porta de origem é efêmera; (c) o ARP não aparece com o filtro `port 80`: faça `docker compose down` e `up -d` e capture com o filtro `arp or port 80` para vê-lo.

## 6. Falha controlada
```powershell
docker compose exec cli curl -s -m 3 http://web:8080/ ; echo $LASTEXITCODE
```
Previsão (**não registrada por mim**): o cliente envia `SYN` e recebe `RST` (porta fechada) ou nada. Capture e registre o real.

## 7–10. Evidências, diagnóstico, correção, validação
Salve a captura em `evidencias/` (ver [README](../../../evidencias/README.md)). Diagnóstico: `docker compose exec web ss -tln` mostra quais portas escutam. Correção: usar a porta 80. Validação: `curl -s -o /dev/null -w '%{http_code}' http://web/` retorna `200`.

## 11. Limpeza
```powershell
docker compose down -v
```

**Limite:** o nome `web` resolve pelo DNS **embutido do Docker** (127.0.0.11), que não equivale a um servidor DNS da sua rede. Veja o [D02](../d02-dns/README.md).
