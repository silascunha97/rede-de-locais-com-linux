# GUIA DE ESTUDOS — Redes de Computadores (RC27CP) com PBL

> **Versão 1.0 — 2026-10-20.** Caderno de acompanhamento para ser preenchido, revisado e expandido.
> **Honestidade sobre o estado:** os 6 laboratórios Docker foram **executados** pelo autor em 2026-10-20 (Docker Desktop 29.7.2, Windows 10); os 8 laboratórios de Packet Tracer **não foram executados** (revisão estática). Nenhum módulo está concluído: **todos "Não iniciado"** até você registrar evidência.

## Índice
1. [Apresentação e objetivos](#1-apresentação-e-objetivos)
2. [Como utilizar o caderno](#2-como-utilizar-o-caderno)
3. [Metodologia PBL](#3-metodologia-pbl)
4. [Ferramentas e pré-requisitos](#4-ferramentas-e-pré-requisitos)
5. [Inventário das fontes](#5-inventário-das-fontes)
6. [Mapeamento do livro](#6-mapeamento-do-livro)
7. [Referências acadêmicas e provas](#7-referências-acadêmicas-e-provas)
8. [Plano de estudos](#8-plano-de-estudos)
9. [Matriz de integração entre as três frentes](#9-matriz-de-integração-entre-as-três-frentes)
10. [Módulos de aprendizagem](#10-módulos-de-aprendizagem)
11. [Laboratórios de Packet Tracer](#11-laboratórios-de-packet-tracer)
12. [Laboratórios Docker](#12-laboratórios-docker)
13. [Banco de questões e exercícios](#13-banco-de-questões-e-exercícios)
14. [Registro de erros e descobertas](#14-registro-de-erros-e-descobertas)
15. [Avaliação e acompanhamento](#15-avaliação-e-acompanhamento)
16. [Revisões periódicas](#16-revisões-periódicas)
17. [Projeto integrador final](#17-projeto-integrador-final)
18. [Glossário técnico](#18-glossário-técnico)
19. [Referências bibliográficas e técnicas](#19-referências-bibliográficas-e-técnicas)
20. [Histórico de alterações do caderno](#20-histórico-de-alterações-do-caderno)

---

## 1. Apresentação e objetivos

Caderno de longo prazo para estudar **Redes de Computadores 1 (RC27CP, UTFPR Pato Branco, Engenharia de Computação)** por **Aprendizagem Baseada em Problemas**. O conteúdo-núcleo é o conteúdo programático do plano de ensino (6 itens); NAT e firewall entram como trilha complementar.

Você deve ser capaz, ao final, de **explicar** por que uma rede funciona, **observá-la** (simulada e em containers), **provocar e diagnosticar falhas** e **demonstrar** isso com evidências. Três frentes sobre os mesmos problemas:

| Frente | O que faz |
|---|---|
| **A — Teoria e problemas** | Compreensão, hipóteses, cálculo, explicação causal |
| **B — Cisco Packet Tracer** | Visualizar e configurar em topologia simulada |
| **C — Docker** | Reproduzir aspectos em uma rede executável (Linux) |

**Fora do escopo declarado:** o caderno não substitui as provas da disciplina nem afirma equivalência entre simulador, containers e rede física.

## 2. Como utilizar o caderno

**Estrutura** (todos os caminhos abaixo existem):
```
GUIA_DE_ESTUDOS.md              <- este arquivo (índice, registros, avaliação)
docs/                           <- fontes, plano, critérios, questões, projeto
modulos/                        <- 9 módulos PBL
laboratorios/packet-tracer/     <- 8 roteiros (.md)
laboratorios/docker/            <- 6 laboratórios (compose + README)
evidencias/                     <- suas evidências
```
**Ciclo por módulo** (não pule a etapa 2): 1) ler o problema; 2) **responder à investigação inicial antes de qualquer teoria**; 3) ler as fontes; 4) escrever a solução preliminar; 5) PT; 6) Docker; 7) comparar, registrar erros; 8) variação do problema; 9) avaliar-se.

**Aviso anti-spoiler:** as respostas estão **separadas** em [docs/gabarito-referencia.md](docs/gabarito-referencia.md). Só abra depois de registrar a sua.

**Convenções:** blocos de endereço `192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24` (RFC 5737); domínio `.test`; `____` = campo seu; "Observado" = vi na execução; "previsão/hipótese" = não verificado.

## 3. Metodologia PBL

Cada módulo percorre o ciclo: **(1)** problema → **(2)** investigação inicial (o que sei, o que não sei, hipóteses, evidências que as refutariam) → **(3)** objetivos → **(4)** estudo autodirigido (livro, plano, questões, documentação) → **(5)** solução preliminar (hipótese, justificativa, resultado esperado, riscos, testes) → **(6)** implementação (PT e Docker) → **(7)** verificação e diagnóstico (esperado × observado) → **(8)** reflexão causal → **(9)** transferência (variação do problema).

Perguntas de fechamento (Etapa 8): por que funcionou? qual hipótese estava errada? qual evidência foi mais útil? como diagnosticaria sem saber a solução? que diferenças vi entre simulação e containers? que limitações impedem concluir?

Quando um conceito não puder ser representado fielmente em um ambiente, o módulo diz isso explicitamente (M01 e M08 sem Docker; M08 sem PT; PT-04 limitado).

## 4. Ferramentas e pré-requisitos

| Item | Detalhe |
|---|---|
| Conhecimentos | Binário/hex, potências de 2, Linux básico, PS26CP (pré-requisito do plano). **Faça o [diagnóstico inicial](docs/banco-de-questoes.md#diagnóstico-inicial)** em vez de eu presumir seu nível. |
| Packet Tracer | Versão: ____ . Roteiros assumem roteador 1941 (`g0/0`, `g0/1`) e switch 2960; **confirme**. |
| Docker | Engine/Desktop + Compose v2. Veja [laboratorios/docker/README.md](laboratorios/docker/README.md). Testado no Docker Desktop 29.7.2/Windows 10. |
| Shell | Comandos escritos para **PowerShell/Linux**. Git Bash converte caminhos (use `MSYS_NO_PATHCONV=1`). |
| Segurança | Sem `privileged`, sem `network_mode: host`, sem `macvlan`, sem portas publicadas; `NET_ADMIN` só onde justificado no compose. |

Verificação:
```powershell
docker version
docker compose version
```

## 5. Inventário das fontes

Detalhes em [docs/fontes-e-referencias.md](docs/fontes-e-referencias.md).

| Categoria | Material | Situação |
|---|---|---|
| Critérios (Markdown) | `RC27CP.md` (plano de ensino) | Lido. Linha de "Camada Física" embaralhada na conversão: **conferir no PDF** |
| Livro | *Redes Locais com Linux* (Vigliazzi), 2ª ed., Visual Books | **Só a capa** (imagem pequena); sem sumário/paginação |
| Provas/documentos acadêmicos | Nenhuma prova fornecida; 1 lista da UFPR lida | Lacuna |
| Documentação técnica | Docker, RFCs, man pages | Parcial; ver fontes |
| Rascunho anterior | `ex-rede-computadores.md` | **Superado**; continha laboratório de roteamento que **não funcionava** |

## 6. Mapeamento do livro

O livro **não pôde ser mapeado**: não há sumário nem páginas, e a lista de tópicos da capa não é legível na imagem. **Não invento capítulos.** A tabela de mapeamento está pronta para preenchimento em [docs/fontes-e-referencias.md](docs/fontes-e-referencias.md#2-o-livro).

**Ação sua (P1):** fotografe/transcreva o sumário e envie. Nota: o livro consta como referência **complementar** no plano; para teoria de transporte e roteamento, prefira Kurose & Ross, Comer ou Tanenbaum. Comandos antigos (`ifconfig`, `route`, `ipchains`) devem ser comparados com `ip`/`iptables-nft`.

## 7. Referências acadêmicas e provas

Resumo (completo em [docs/fontes-e-referencias.md](docs/fontes-e-referencias.md#3-fontes-acadêmicas-de-instituições-federais)):

| Fonte | Situação |
|---|---|
| UFPR — Lista 1 de Fundamentos de Redes & SD (Prof. Elias P. Duarte Jr.), https://www.inf.ufpr.br/elias/fundresd/lista1fundresd.html | **Acessada em 2026-10-20**; usada para confirmar tópicos; sem cópia de questões |
| UFRGS, UFU, UFSC, UFMG | Localizadas; **não lidas**; "a verificar" |

**Rastreio de questões (a preencher conforme você obtiver provas):**

| Fonte | Questão (resumo) | Tipo (encontrada / adaptada / original) | Módulo | Variante / PT / Docker |
|---|---|---|---|---|
| | | | | |

As questões do banco são **originais**.

## 8. Plano de estudos

Detalhe e dependências: [docs/plano-de-estudos.md](docs/plano-de-estudos.md). Sem calendário fixo: avance por nível alcançado.

## 9. Matriz de integração entre as três frentes

Matriz completa (problema, conceito, livro, fonte, PT, Docker, evidência, critério) em [docs/plano-de-estudos.md](docs/plano-de-estudos.md#2-matriz-de-integração-três-frentes).

## 10. Módulos de aprendizagem

| ID | Módulo | Item RC27CP | PT | Docker | Status |
|---|---|---|---|---|---|
| M01 | [Conceitos e atrasos](modulos/modulo-01-conceitos.md) | 1 | PT-01 | — (justificado) | Não iniciado |
| M02 | [Camadas e encapsulamento](modulos/modulo-02-camadas-encapsulamento.md) | 2 | PT-02 | D01 | Não iniciado |
| M03 | [Aplicação: DNS e HTTP](modulos/modulo-03-aplicacao-dns-http.md) | 3 | PT-03 | D02 | Não iniciado |
| M04 | [Transporte: TCP e UDP](modulos/modulo-04-transporte.md) | 4 | PT-04 (limitado) | D03 | Não iniciado |
| M05 | [IPv4 e sub-redes](modulos/modulo-05-ipv4-subredes.md) | 5 | PT-05 | D04-A | Não iniciado |
| M06 | [Repasse e roteamento](modulos/modulo-06-roteamento.md) | 5 | PT-06 | D04-B | Não iniciado |
| M07 | [Enlace, ARP e switching](modulos/modulo-07-enlace-switching.md) | 6 | PT-07 | D05 (parcial) | Não iniciado |
| M08 | [Camada física](modulos/modulo-08-camada-fisica.md) | 6 | — | — | Não iniciado |
| M09 | [NAT e firewall (complementar)](modulos/modulo-09-nat-firewall.md) | — | PT-08 | D06 | Não iniciado |

**Lacunas do plano (assumidas):** FTP, SMTP e SSH (item 3) só têm leitura; protocolos de roteamento dinâmico, VLAN, DHCP e IPv6 são extensões opcionais.

## 11. Laboratórios de Packet Tracer

*Todos revisados estaticamente; **nenhum executado**.*

| Lab | Módulo | Assunto |
|---|---|---|
| [PT-01](laboratorios/packet-tracer/pt-01-lan-simples.md) | M01 | LAN simples, falha de máscara |
| [PT-02](laboratorios/packet-tracer/pt-02-simulacao-pdu.md) | M02 | Simulation Mode, PDUs |
| [PT-03](laboratorios/packet-tracer/pt-03-dns-http.md) | M03 | DNS e HTTP |
| [PT-04](laboratorios/packet-tracer/pt-04-transporte.md) | M04 | Portas e transporte (limitado) |
| [PT-05](laboratorios/packet-tracer/pt-05-subredes-um-roteador.md) | M05 | Dois segmentos, um roteador |
| [PT-06](laboratorios/packet-tracer/pt-06-rotas-estaticas.md) | M06 | Rotas estáticas |
| [PT-07](laboratorios/packet-tracer/pt-07-arp-switch.md) | M07 | ARP e tabela MAC |
| [PT-08](laboratorios/packet-tracer/pt-08-nat-acl.md) | M09 | NAT overload e ACL |

Não há arquivos `.pkt`: apenas roteiros. Ao concluir, salve seu `.pkt` em `evidencias/`.

## 12. Laboratórios Docker

Leia primeiro o [README geral](laboratorios/docker/README.md) (armadilhas: um lab por vez, redes `internal` não roteiam, `.1` é do Docker, nomes de interface instáveis).

| Lab | Módulo | Tema | Teste do autor |
|---|---|---|---|
| [D01](laboratorios/docker/d01-encapsulamento/README.md) | M02 | Captura e encapsulamento | Executado |
| [D02](laboratorios/docker/d02-dns/README.md) | M03 | DNS com dnsmasq | Executado |
| [D03](laboratorios/docker/d03-transporte/README.md) | M04 | TCP × UDP | Executado |
| [D04](laboratorios/docker/d04-roteador/README.md) | M05/M06 | Roteador Linux, 3 falhas | Executado |
| [D05](laboratorios/docker/d05-enlace-arp/README.md) | M07 | ARP/vizinhos | Executado |
| [D06](laboratorios/docker/d06-nat-firewall/README.md) | M09 | NAT e firewall | Executado |

"Executado" significa observado **no ambiente do autor**; trechos marcados "previsão" ou "não registrado" **não** foram observados.

## 13. Banco de questões e exercícios

- Caderno do estudante: [docs/banco-de-questoes.md](docs/banco-de-questoes.md) (originais, com dificuldade ★).
- ⚠️ Respostas: [docs/gabarito-referencia.md](docs/gabarito-referencia.md) — **não abra antes de tentar.**

## 14. Registro de erros e descobertas

### Diário de laboratório (copie para cada experimento)
```
Data:
Módulo / Lab:
Objetivo:
Hipótese (o que espero ver e por quê):
Ambiente e versões (PT / Docker / SO):
Topologia e endereçamento:
Comandos executados:
Resultados observados:
Evidências (link para evidencias/...):
Erros encontrados:
Diagnóstico:
Correção aplicada:
Conclusão (a hipótese se confirmou?):
Dúvidas pendentes:
```

### Erros recorrentes e dúvidas
| Data | Módulo | Erro / dúvida | Hipótese | Resolvido? | Link da evidência |
|---|---|---|---|---|---|
| | | | | | |

### Conceitos ainda não consolidados / questões para refazer / laboratórios pendentes
| Item | Tipo (conceito / questão / lab) | Módulo | Próxima tentativa |
|---|---|---|---|
| | | | |

## 15. Avaliação e acompanhamento

Escala de 4 níveis (0 Não demonstrado · 1 Inicial · 2 Funcional · 3 Consolidado), dimensões D1–D9 e regra do "menor nível": [docs/criterios-de-avaliacao.md](docs/criterios-de-avaliacao.md). Laboratório "funcionando" **não** é conclusão.

| Módulo | Status | Data | Nível (0–3) | Dificuldades | Pendências | Próxima revisão | Evidência |
|---|---|---|---|---|---|---|---|
| M01 | Não iniciado | | | | | | |
| M02 | Não iniciado | | | | | | |
| M03 | Não iniciado | | | | | | |
| M04 | Não iniciado | | | | | | |
| M05 | Não iniciado | | | | | | |
| M06 | Não iniciado | | | | | | |
| M07 | Não iniciado | | | | | | |
| M08 | Não iniciado | | | | | | |
| M09 | Não iniciado | | | | | | |
| PI | Não iniciado | | | | | | |

**Checklist geral**
- [ ] Diagnóstico inicial feito
- [ ] Sumário do livro enviado/preenchido (P1)
- [ ] Versão do Packet Tracer registrada
- [ ] `docker version` e `docker compose version` conferidos
- [ ] M01–M08 em nível ≥ 2
- [ ] M09 (opcional) em nível ≥ 2
- [ ] Projeto integrador entregue

## 16. Revisões periódicas

Não há calendário rígido: **o desempenho determina o intervalo.**
- Nível 3 → revisar em ~1 mês: refazer um cálculo e reexplicar sem notas.
- Nível 2 → em ~1 semana, refazendo **um** laboratório sem roteiro, em topologia alterada.
- Nível ≤ 1, ou erro recorrente → revisar em 1–2 dias, na dimensão que falhou.
- Antes de cada novo módulo: 1 questão dos pré-requisitos.

(Os intervalos são sugestões minhas, sem dados do seu ritmo; ajuste.) Registre cada revisão na tabela da seção 15. Tempo de execução ≠ domínio: ver "Tempo ≠ domínio" nos critérios.

## 17. Projeto integrador final

[docs/projeto-integrador.md](docs/projeto-integrador.md): rede de pequena empresa (3 setores, VLSM, roteador, DNS/HTTP, NAT e filtro), PT + Docker, relatório, 2 falhas diagnosticadas. Conceitos não preparados (DHCP, VLAN, IPv6, roteamento dinâmico) são **extensões opcionais**.

## 18. Glossário técnico

**ARP** resolve IP→MAC no enlace local · **Bridge (Docker)** ponte virtual do kernel; não é switch gerenciável · **CIDR** notação IP/prefixo · **Datagrama** PDU da camada de rede (e do UDP) · **Encapsulamento** adição de cabeçalhos por camada · **Gateway** roteador de saída de uma sub-rede · **Handshake** SYN, SYN+ACK, ACK · **ICMP** mensagens de controle/diagnóstico do IP · **MAC** endereço físico da interface · **Masquerade** NAT que usa o IP da interface de saída · **NAT** tradução de endereços · **Namespace de rede** pilha de rede isolada (cada container tem a sua) · **PDU** unidade de dados do protocolo · **Prefixo mais longo** regra de escolha de rota · **Quadro** PDU do enlace · **RTT** tempo de ida e volta · **Segmento** PDU do TCP · **Store-and-forward** recebe o pacote inteiro antes de encaminhar · **TTL** limite de saltos do datagrama · **VLSM** sub-redes de tamanhos diferentes.

## 19. Referências bibliográficas e técnicas

Lista completa em [docs/fontes-e-referencias.md](docs/fontes-e-referencias.md#6-bibliografia). Principais: Kurose & Ross (5. ed.), Comer (4. ed.), Tanenbaum (4. ed.) — básicas do plano; Vigliazzi, *Redes Locais com Linux* (Visual Books) — complementar; Docker docs; RFC 791, 792, 826, 768, 9293, 1034/1035, 5737.

## 20. Histórico de alterações do caderno

| Data | Versão | Alteração |
|---|---|---|
| 2026-10-20 | 1.0 | Criação a partir do plano RC27CP, capa do livro e rascunho v0.1. 9 módulos, 8 roteiros PT, 6 laboratórios Docker **executados**. Correção do laboratório de roteamento do rascunho (redes `internal` impediam o roteamento). |
| | | |

### Pendências conhecidas
P1 sumário do livro · P2 abrir fontes externas (UFRGS, UFU, UFSC, UFMG) e registrar questões · P3 conferir o plano no PDF · P4 executar os roteiros do Packet Tracer · P5 registrar versão do PT · P6 confirmar a observação sobre redes `internal` em outra versão do Docker.
