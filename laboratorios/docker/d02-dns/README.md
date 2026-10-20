# D02 — DNS com dnsmasq (Módulo M03)

Voltar: [README dos laboratórios](../README.md) · [Módulo 03](../../../modulos/modulo-03-aplicacao-dns-http.md)

**Problema:** o servidor web responde por IP, mas os clientes precisam usar `web.lab.test`. Montar a resolução e depois quebrá-la de forma diagnosticável.

**Arquivos:** [compose.yaml](compose.yaml), [dns/Dockerfile](dns/Dockerfile), [dns/dnsmasq.conf](dns/dnsmasq.conf). Rede `lan` 192.0.2.0/24 (`internal`): `dns` .53, `web` .10, `cli` .100. O domínio `.test` é reservado (RFC 6761).

## Passos
```powershell
cd laboratorios\docker\d02-dns
docker compose up -d --build
docker compose exec cli cat /etc/resolv.conf
docker compose exec cli dig web.lab.test
docker compose exec cli curl -s http://web.lab.test
docker compose logs dns
```
**Observado (2026-10-20):** `dig +short` → `192.0.2.10`; `curl` devolve o HTML do nginx; o log do dnsmasq mostra `query[A] web.lab.test from 192.0.2.100` (e `query[AAAA]`). **Atenção:** o `resolv.conf` do cliente aponta para `127.0.0.11` (DNS embutido do Docker), com o comentário `ExtServers: [192.0.2.53]`: o embutido **encaminha** ao dnsmasq. Não é uma consulta direta cliente→dnsmasq. Para consultar direto: `docker compose exec cli dig @192.0.2.53 web.lab.test`.

## Falha controlada
Comente a linha `address=` em `dns/dnsmasq.conf` e reconstrua:
```powershell
docker compose up -d --build
docker compose exec cli dig web.lab.test
docker compose exec cli dig @192.0.2.53 web.lab.test
```
**Observado:** o `dig` pelo resolvedor padrão retornou `status: SERVFAIL`, `ANSWER: 0`. O resultado do `dig @192.0.2.53` **não foi registrado por mim**: registre o seu. Pergunta: por que `SERVFAIL` e não `NXDOMAIN`? (Hipótese não verificada: o resolvedor embutido não obteve resposta útil do upstream.)

## Correção, validação, limpeza
Descomente `address=`, `docker compose up -d --build`, repita o `dig`. Depois `docker compose down -v`.

## Limites
Um único servidor; sem hierarquia (raiz/TLD), sem TCP/53, sem DNSSEC. O `dnsmasq.conf` usa `no-resolv`: nomes externos não resolvem (intencional; a rede é interna).
