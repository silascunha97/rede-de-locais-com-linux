# Laboratórios Docker — leia antes de começar

Seção 12 do [GUIA_DE_ESTUDOS.md](../../GUIA_DE_ESTUDOS.md).

## Laboratórios

| Lab | Módulo | Tema | Status de teste |
|---|---|---|---|
| [d01-encapsulamento](d01-encapsulamento/README.md) | M02 | Bridge, captura, MAC/IP/porta | Executado 2026-10-20 |
| [d02-dns](d02-dns/README.md) | M03 | DNS com dnsmasq | Executado 2026-10-20 |
| [d03-transporte](d03-transporte/README.md) | M04 | TCP × UDP | Executado 2026-10-20 |
| [d04-roteador](d04-roteador/README.md) | M05, M06 | Roteador Linux, rotas, falhas | Executado 2026-10-20 |
| [d05-enlace-arp](d05-enlace-arp/README.md) | M07 | ARP e vizinhos | Executado 2026-10-20 |
| [d06-nat-firewall](d06-nat-firewall/README.md) | M09 | NAT e iptables | Executado 2026-10-20 |

"Executado" = rodado por mim no ambiente abaixo, com as saídas relevantes conferidas. **Não** significa que funcionará idêntico no seu (versões do Docker/kernel podem diferir). Nos `README` as seções "Resultado esperado" refletem o que foi observado, com identificadores (MACs, portas efêmeras, IDs) que mudam a cada execução.

Ambiente de teste: Windows 10, Docker Desktop (Engine 29.7.2), shell Git Bash. Os comandos dos READMEs são escritos para **PowerShell ou Linux**.

## Pré-requisitos

```powershell
docker version
docker compose version
```
- Docker Engine/Desktop com Compose v2. Imagens fixadas por digest: `nicolaka/netshoot` (ferramentas: `ip`, `ping`, `traceroute`, `tcpdump`, `dig`, `curl`, `nc`, `ss`, `iptables`, `conntrack`) e `nginx:alpine` (1.31.7 quando testado); `alpine:3.20` por digest no D02.
- Se um digest deixar de existir, troque pela tag equivalente e anote no diário.

## O que é e o que não é Docker aqui

- Cada container tem seu **namespace de rede** próprio. Uma rede *bridge* é uma ponte virtual no kernel do host (no Docker Desktop, dentro de uma VM Linux, não no Windows). **Não** é um switch gerenciável nem uma LAN física: não há VLAN, spanning tree, portas físicas nem comutação em hardware.
- Docker **não roteia entre redes bridge distintas**: o laboratório D04 cria um roteador explícito.
- `network_mode: host`, `macvlan` e `privileged: true` **não** são usados. Só `cap_add: NET_ADMIN` onde se alteram rotas/firewall dentro do container, com justificativa no próprio compose.
- Nenhuma porta é publicada no host (`ports:` ausente). D01–D03 e D05 usam rede `internal: true`; D04 e D06 não podem (ver a seguir).

## Armadilhas já observadas (detalhes em [fontes-e-referencias.md](../../docs/fontes-e-referencias.md#4-achados-técnicos-que-corrigem-o-rascunho-anterior))

1. **Um laboratório por vez**: as sub-redes se repetem. Antes de outro: `docker compose down -v`.
2. Redes `internal: true` **quebram o roteamento entre redes** (D04/D06 usam redes comuns, que têm o gateway `.1` do Docker).
3. `.1` de cada sub-rede pertence ao Docker. Não o atribua.
4. Nomes de interface (`eth0`/`eth1`) podem mudar de ordem entre execuções: confirme com `ip -br addr`.
5. Git Bash converte caminhos Unix; use PowerShell.

## Padrão de captura (usado nos READMEs)

Captura limitada e sem arquivos: o `tcpdump` roda em segundo plano, o teste é executado, e o `wait` espera o fim.

```powershell
docker compose exec cli sh -c 'tcpdump -i eth0 -nn -e -c 12 port 80 & sleep 1; curl -s http://web/ -o /dev/null; wait'
```
`-c N` encerra após N pacotes; se o teste gerar menos que N, o comando fica aguardando (Ctrl+C).

## Sequência padrão de cada laboratório

1. Pré-requisitos · 2. Preparação · 3. Inicialização · 4. Inspeção da topologia · 5. Testes · 6. Falha controlada · 7. Evidências · 8. Diagnóstico · 9. Correção · 10. Validação · 11. Limpeza.

## Limpeza geral

```powershell
docker compose down -v          # dentro da pasta do laboratório
docker ps -a                     # nada com prefixo dNN deve restar
docker network ls
```
