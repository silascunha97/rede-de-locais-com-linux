# Fontes e referências

Cobre as seções 5, 6, 7 e 19 do [GUIA_DE_ESTUDOS.md](../GUIA_DE_ESTUDOS.md). Última revisão: 2026-10-20.

Regra de honestidade deste caderno: cada item abaixo diz **o que foi realmente lido** e **o que não foi**.

## 1. Inventário (Etapa A)

| Material | Arquivo / URL | Papel | Lido? | Observação |
|---|---|---|---|---|
| Plano de ensino RC27CP (UTFPR Pato Branco) | `RC27CP.md`, `RC27CP.pdf` | **Especificação do projeto pedagógico** | `.md` lido por inteiro (sem as imagens base64). PDF não aberto; o `.md` é conversão dele | Ver §1.1 |
| Livro "Redes Locais com Linux" | foto da capa `0079c404-…webp` | Referência teórica pessoal | **Só a capa** | Ver §2 |
| Caderno anterior (rascunho v0.1) | `ex-rede-computadores.md` | Rascunho aproveitado | Lido | **Superado por este caderno** (ver §4: continha um laboratório que não funcionava) |
| Prova(s) / listas de exercícios | — | — | **Nenhuma foi fornecida** | Lacuna. Ver §3 |
| Documentação oficial | URLs em §5 | Validação técnica | Parcial | Ver §5 |

### 1.1 O que o plano RC27CP determina (critérios obrigatórios)

- Disciplina Redes de Computadores 1, código RC27CP, 6º período, Engenharia de Computação, matriz 535. Pré-requisito: PS26CP (Princípios de Sistemas de Comunicação).
- Carga: 72 aulas (AT 34, AP 34, APS 4). Aprovação: frequência ≥ 75% e nota final ≥ 6,0.
- **Conteúdo programático (6 itens)** → é a espinha dorsal dos módulos M01–M08: (1) conceitos, LAN/MAN/WAN, simplex/half/full; (2) camadas, OSI e TCP/IP, endereço físico/lógico/porta; (3) aplicação: HTTP, FTP, SMTP, DNS, SSH; (4) transporte, TCP/UDP; (5) rede: IP, repasse, roteamento; (6) enlace, switching, camada física.
- Metodologia: aulas práticas com laboratório e **atividades práticas supervisionadas** com estudos dirigidos e estudos de caso: compatível com PBL.
- O livro do Vigliazzi consta como referência **complementar** (não básica). As básicas são Comer, Kurose & Ross e Tanenbaum.
- Itens do prompt **fora do plano** (NAT, firewall, DHCP, IPv6, VLAN): ficam como trilha complementar (M09 e extensões), marcados como tal. Nenhum critério explícito do plano foi substituído.

### 1.2 Conflitos e ambiguidades

| # | Situação | Decisão |
|---|---|---|
| C1 | O prompt lista 15 eixos (IPv6, VLAN, DHCP, firewall…); o plano cobre só 6 itens. | Núcleo = plano. NAT/firewall entram como M09 (complementar). IPv6, VLAN e DHCP ficam como extensões opcionais citadas nos módulos, sem laboratório próprio. |
| C2 | O prompt pede PBL e Docker com "problemas realistas"; o plano é de uma disciplina de 6º período com cálculo (atrasos, sub-redes, CRC). | Módulos mistos: parte analítica (cálculo) + parte prática. Camada física (M08) não tem laboratório. |
| C3 | O `.md` do plano tem a linha "Camada de Enlace/Física" embaralhada na conversão. | Conteúdo reconstruído a partir do texto; **conferir no PDF** (pendência P3). |
| C4 | Prompt pede mapeamento capítulo-a-capítulo do livro; só há a capa. | Coluna "Livro" fica vazia por desenho. Não invento páginas (pendência P1). |
| C5 | O prompt pede questões de provas federais; nenhuma prova foi fornecida e as fontes externas não foram lidas por inteiro. | Questões do banco são **originais**; fontes externas só indicam tópicos (§3). |

## 2. O livro

- **Identificado pela capa:** DOUGLAS VIGLIAZZI, *Redes Locais com Linux*, **2ª edição**, Visual Books. O plano RC27CP cita "Santa Catarina: Visual Books, 2004" (a edição do plano pode não ser a sua; **ano da sua edição: ____**).
- A imagem enviada é muito pequena (miniatura); a lista de tópicos impressa na capa **não é legível**. Não a transcrevo.
- **Sem sumário, sem paginação.** Portanto: nenhuma página ou capítulo é citado neste caderno. Cada módulo traz uma instrução do tipo "procure no sumário o capítulo sobre X e anote aqui o número" e um campo `Livro:` para você preencher.
- Natureza do livro (informação da ficha do autor, não conferida no exemplar): obra prática sobre implantar redes locais com serviços em Linux. Inferência minha: boa para serviços/laboratório (M03, M09), menos para a teoria de transporte e roteamento, que Kurose & Ross / Comer / Tanenbaum cobrem melhor.
- **Divergências possíveis:** o livro é de 2004-época. Ferramentas como `ifconfig`, `route`, `netstat`, `iptables` legado e `ipchains` foram substituídas por `ip`, `ss`, `nftables`/`iptables-nft`. Quando o livro usar o comando antigo, use o equivalente moderno deste caderno e anote a diferença no [diário](../GUIA_DE_ESTUDOS.md#14-registro-de-erros-e-descobertas).

### Tabela de mapeamento (preencher)

| Módulo | Assunto | Capítulo/seção do livro | Páginas | Observação |
|---|---|---|---|---|
| M01 | Conceitos de redes | ___ | ___ | |
| M02 | Camadas, TCP/IP, endereços | ___ | ___ | |
| M03 | Serviços de aplicação (DNS, HTTP…) | ___ | ___ | |
| M04 | TCP/UDP | ___ | ___ | |
| M05 | IP e sub-redes | ___ | ___ | |
| M06 | Roteamento | ___ | ___ | |
| M07 | Enlace e switching | ___ | ___ | |
| M08 | Camada física | ___ | ___ | |
| M09 | NAT/firewall | ___ | ___ | |

## 3. Fontes acadêmicas de instituições federais

Verificação feita em 2026-10-20.

| Instituição | Documento | URL | Tipo | Situação real |
|---|---|---|---|---|
| UFPR, Dep. de Informática | "Lista 1 de Fundamentos de Redes & SD", Prof. Elias P. Duarte Jr. (ano não informado na página) | https://www.inf.ufpr.br/elias/fundresd/lista1fundresd.html | Lista de exercícios | **Acessada em 2026-10-20.** Resumo dos tópicos: OSI×TCP/IP, PDUs e encapsulamento, LAN×WAN, Ethernet/CSMA-CD, endereçamento IP/CIDR/máscara, roteamento direto e indireto, ARP, cabeçalho IP/fragmentação/TTL, traceroute/ICMP, TCP×UDP. Usada **só para confirmar tópicos** (M02, M05, M06, M07); nenhuma questão foi copiada. |
| UFRGS, Inst. de Informática | Lista de Exercícios 2 | http://www.inf.ufrgs.br/~asc/redes/pdf/lista2.pdf | Lista | Localizada por busca em sessão anterior; o PDF não foi lido (imagem). **A verificar.** |
| UFU, FACOM | Lista 1: História da Internet e OSI (2sem2014) | https://www.facom.ufu.br/~albertini/2sem2014/redes/lista01.pdf | Lista | Não acessada (erro de certificado). **A verificar.** |
| UFSC | Planos DEC7126/DEC7557/DEC7128 | https://repositorio.ufsc.br/bitstream/handle/123456789/231301/DEC7126%20-%20Redes%20de%20computadores.pdf | Planos de ensino | Não aberto. **A verificar.** |
| UFMG, DCC | Slides cap. 5 Kurose & Ross | https://homepages.dcc.ufmg.br/~jmarcos/cursos/redes/Telecom2008/cap05a-Camada-de-Enlace.pdf | Slides | Não aberto. |

**Consequência:** o banco de questões ([banco-de-questoes.md](banco-de-questoes.md)) é composto por **problemas originais** (categoria 3 do prompt). Não há questão "adaptada de prova federal" porque nenhuma questão foi efetivamente lida. A tabela de rastreio (GUIA §7) está pronta para você registrar questões reais quando abrir as fontes ou fornecer provas.

## 4. Achados técnicos que corrigem o rascunho anterior

Todos **observados na execução** (2026-10-20, Docker Desktop 29.7.2, Windows 10, backend containerizado):

1. **Redes `internal: true` não permitem roteamento entre si.** No rascunho, o laboratório de roteador usava `internal: true` nas duas sub-redes: o ping falhava e o `tcpdump` no roteador não via nem o pacote chegando. Os laboratórios D04 e D06 usam redes bridge comuns. *A documentação consultada (packet-filtering-firewalls) não descreve esse comportamento*; trate-o como observação empírica, a confirmar em outras versões. Hipótese não verificada: regras de filtragem que o Docker instala para redes internas.
2. **O nome da interface (`eth0`/`eth1`) dentro do roteador não é estável**: variou entre execuções. Por isso os laboratórios usam `-i any` no `tcpdump` e regras de NAT por origem/destino, não por `-o ethX`.
3. **`sysctl -w net.ipv4.ip_forward=0` falha** (`Read-only file system`) em container sem privilégios. A falha "roteador sem encaminhamento" é produzida recriando o container com `sysctls: net.ipv4.ip_forward: "0"`.
4. **O endereço `.1` da sub-rede é do gateway do Docker** (tentar usá-lo causa `Address already in use`).
5. **Roteamento assimétrico pelo host**: sem NAT, a resposta de um servidor com rota padrão do Docker ainda chegava ao cliente (o host/VM reencaminhou). Por isso `srv` no D06 tem a rota padrão removida; sem isso, "sem NAT" parece funcionar.
6. **Só um laboratório por vez**: todos usam sub-redes de documentação (RFC 5737) iguais; subir dois gera `Pool overlaps`. Faça `docker compose down -v` antes de iniciar outro.
7. **Git Bash no Windows** converte caminhos (`/tmp/x` vira `C:/…`). Prefira PowerShell, ou use `MSYS_NO_PATHCONV=1`.
8. `dns:` no Compose com rede definida pelo usuário **não faz o container falar direto com o dnsmasq**: o `resolv.conf` aponta para o DNS embutido (127.0.0.11), que encaminha ao servidor indicado. A falha do registro produziu `SERVFAIL`, não `NXDOMAIN`.

## 5. Documentação técnica oficial (para conferência)

| Assunto | Fonte |
|---|---|
| Docker Engine / redes bridge | https://docs.docker.com/engine/network/ |
| Docker: filtragem de pacotes e firewall | https://docs.docker.com/engine/network/packet-filtering-firewalls/ (acessada em 2026-10-20) |
| Compose: referência de arquivo | https://docs.docker.com/reference/compose-file/ |
| `ip`, `tcpdump`, `ss`, `iptables`, `dig` | páginas `man` das ferramentas (`man ip`, etc.) |
| ARP | RFC 826 |
| IPv4 / ICMP | RFC 791 / RFC 792 |
| UDP / TCP | RFC 768 / RFC 9293 |
| DNS | RFC 1034 / RFC 1035 |
| Endereços de documentação (192.0.2.0/24, 198.51.100.0/24, 203.0.113.0/24) | RFC 5737 |
| Cisco Packet Tracer | Ajuda interna do programa e cursos Cisco Networking Academy (conferir sua versão) |

Os laboratórios Docker foram **executados** em 2026-10-20 (ver cada README). Os de Packet Tracer **não foram executados** (sem o programa disponível): revisados estaticamente.

## 6. Bibliografia

**Plano RC27CP (básicas):** COMER, D. E. *Redes de Computadores e Internet*, 4. ed., Bookman, 2007. KUROSE, J. F.; ROSS, K. W. *Redes de computadores e a internet: uma abordagem top-down*, 5. ed., Pearson, 2010. TANENBAUM, A. S. *Redes de computadores*, 4. ed., Campus, 2003.

**Complementares:** SOARES; LEMOS; COLCHER (Campus, 1995); MATTHEWS (LTC, 2006); TORRES (Axcel, 2001); ARNETT et al. (Campus, 1997); TAROUCO (McGraw-Hill, 1986); **VIGLIAZZI, D. *Redes Locais com Linux*, Visual Books** (2ª ed. conforme capa).

**Pendências desta página:** P1 sumário do livro · P2 abrir fontes da §3 · P3 conferir plano no PDF.
