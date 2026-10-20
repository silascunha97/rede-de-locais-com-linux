# Módulo 07 — Enlace, ARP e comutação

**Status:** Não iniciado
**Dificuldade estimada:** Média
**Pré-requisitos:** [M02](modulo-02-camadas-encapsulamento.md), [M05](modulo-05-ipv4-subredes.md)
**Estimativa de esforço:** 8–10 h (estimativa minha)
**Item do plano RC27CP:** 6 (enlace, endereçamento de enlace, switching) · Voltar: [GUIA](../GUIA_DE_ESTUDOS.md)

## 1. Problema norteador

Em uma LAN com um switch novo, a tabela de endereços MAC está vazia. Ao primeiro `ping` entre duas estações, o tráfego se comporta de modo diferente do ping seguinte, e uma terceira estação, que não participa, consegue ver apenas **parte** da conversa. Explique o que o switch faz em cada etapa, de onde vem o MAC de destino que a estação usa, e por que isso muda quando o destino está em **outra** rede.

Resultado verificável: tabelas MAC/ARP antes e depois, com a sequência de quadros anotada.

## 2. Investigação inicial
- O que sabemos? ____ · Descobrir? ____
- Hipóteses sobre o que o switch aprende e de qual campo: ____
- Como provar que o terceiro host não vê o unicast? ____

## 3. Objetivos de aprendizagem
- [ ] Descrever detecção de erros (paridade, checksum, CRC) em nível conceitual e calcular paridade.
- [ ] Explicar CSMA/CD (conceito) e a diferença hub/bridge/switch.
- [ ] Explicar o aprendizado e o *flooding* do switch.
- [ ] Explicar o ARP e por que o gateway é consultado para destinos remotos.
- [ ] Ler `show mac address-table`, `arp -a`, `ip neigh`.

## 4. Fundamentação teórica (mínima)
O switch aprende o MAC de **origem** de cada quadro (por porta) e encaminha por MAC de **destino**; desconhecido ou broadcast é inundado. O ARP resolve IP→MAC **no segmento**; para outra rede, o host faz ARP do gateway. VLAN, STP: **extensões** (não exigidas pelo plano).

## 5. Leituras e fontes
- **Livro (Vigliazzi):** ____ (preencher).
- **Plano:** item 6 (protocolos de acesso ao meio, endereçamento de enlace, interconexão: hubs, switches, bridges).
- **Acadêmico:** UFPR lista 1 (Ethernet, CSMA/CD, ARP, caches).
- **Questões:** Q7.1–Q7.5.
- **Técnica:** RFC 826 (ARP); `man ip-neighbour`.

## 5b. Solução preliminar
Hipótese: ____ · Justificativa: ____ · Esperado: ____ · Riscos: ____ · Testes: ____

## 6. Laboratório Cisco Packet Tracer
[PT-07 — ARP e tabela MAC](../laboratorios/packet-tracer/pt-07-arp-switch.md). *Não executado pelo autor.*

## 7. Laboratório Docker (parcial)
[D05 — ARP e vizinhos](../laboratorios/docker/d05-enlace-arp/README.md). **Executado** em 2026-10-20 (ARP request em broadcast, reply em unicast, `h3` sem ver o ICMP unicast).

## 8. Análise comparativa
Comparáveis: ARP e cache. **Não equivalente:** a bridge Linux não é um switch gerenciável (sem `show mac address-table` nem portas físicas); CSMA/CD e hubs não existem em nenhum dos ambientes.

## 9. Exercícios
Q7.1–Q7.5.

## 10. Revisão individual
- Aprendi: ____ · Hipótese errada: ____ · Evidência decisiva: ____ · Não explico: ____ · Sem o roteiro: ____

## 11. Avaliação
- [ ] Expliquei o conceito sem consultar a solução.
- [ ] Implementei o laboratório.
- [ ] Validei os resultados com evidências.
- [ ] Investiguei pelo menos uma falha.
- [ ] Resolvi uma variação do problema.
- [ ] Registrei dificuldades e conclusões.

Obrigatórias: D1, D6, D7.
**Nível alcançado:** 0 / 1 / 2 / 3 **Próxima revisão:** ____ **Pendências:** ____
