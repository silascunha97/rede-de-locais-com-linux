# Módulo 02 — Camadas, encapsulamento e endereços

**Status:** Não iniciado
**Dificuldade estimada:** Média
**Pré-requisitos:** [M01](modulo-01-conceitos.md)
**Estimativa de esforço:** 8–10 h (estimativa minha)
**Item do plano RC27CP:** 2 · Voltar: [GUIA](../GUIA_DE_ESTUDOS.md)

## 1. Problema norteador

Uma estação envia uma página web para um servidor. Em um cenário os dois estão na **mesma rede**; em outro, estão em **redes diferentes** com um roteador no meio. Um analista capturou pacotes nos dois pontos e diz: "alguns endereços mudaram entre os dois pontos, outros não". Sua tarefa: **prever**, antes de capturar, quais campos (MAC, IP, porta) mudam ou permanecem em cada cenário, e **comprovar** com captura real (Docker) e com PDUs (Packet Tracer).

Resultado verificável: tabela prevista × observada, com divergências explicadas.

## 2. Investigação inicial

- O que sabemos? ____
- O que precisamos descobrir? ____
- Hipóteses: (1) ____ (2) ____
- Teste para cada hipótese: ____
- **Previsão por escrito** (quem muda: MAC origem? MAC destino? IP origem? porta origem?): ____

## 3. Objetivos de aprendizagem

- [ ] Descrever as camadas TCP/IP e OSI e relacioná-las.
- [ ] Nomear a PDU de cada camada (mensagem, segmento, datagrama, quadro).
- [ ] Distinguir endereço físico (MAC), lógico (IP) e de porta, e dizer onde cada um é usado.
- [ ] Ler uma captura Ethernet/IP/TCP (campos e flags).
- [ ] Explicar o encapsulamento com um exemplo concreto.

*Conhecido:* conceito de protocolo. *Novo:* tudo acima.

## 4. Fundamentação teórica (mínima)
Cada camada acrescenta cabeçalho aos dados da camada superior e consome o da inferior (serviço). O MAC identifica a interface **no enlace local**; o IP identifica o host **na rede**; a porta identifica o processo **no host**. Roteadores reescrevem o enlace a cada salto e preservam o IP (salvo NAT). O restante da teoria — ARP, roteamento — fica para M05–M07.

## 5. Leituras e fontes
- **Livro (Vigliazzi):** seção sobre modelo de camadas/TCP-IP: ____ (preencher).
- **Plano RC27CP, item 2:** "endereço físico, lógico e de porta; OSI e TCP/IP".
- **Acadêmico:** UFPR lista 1 (OSI × TCP/IP, PDUs, encapsulamento) — tópicos confirmados, questões não copiadas.
- **Questões:** Q2.1–Q2.4.
- **Técnica:** `man tcpdump` (`-e`, `-nn`), RFC 791 e 9293 (cabeçalhos).

## 5b. Solução preliminar (antes do laboratório)
Hipótese: ____ · Justificativa: ____ · Alterações: ____ · Resultado esperado: ____ · Riscos/limitações: ____ · Testes: ____

## 6. Laboratório Cisco Packet Tracer
[PT-02 — Simulation Mode](../laboratorios/packet-tracer/pt-02-simulacao-pdu.md) (usa a topologia do [PT-01](../laboratorios/packet-tracer/pt-01-lan-simples.md) e a do [PT-05](../laboratorios/packet-tracer/pt-05-subredes-um-roteador.md)). *Não executado pelo autor.*

## 7. Laboratório Docker
[D01 — encapsulamento](../laboratorios/docker/d01-encapsulamento/README.md): captura de HTTP entre `cli` e `web` na mesma bridge. **Executado** pelo autor em 2026-10-20 para o cenário da mesma rede. O cenário com roteador é o [D04](../laboratorios/docker/d04-roteador/README.md) (use `tcpdump -e` no roteador e compare os MACs nas duas interfaces).

## 8. Análise comparativa
Comparáveis: campos Ethernet/IP/TCP; ordem ARP→ICMP→TCP. Não equivalentes: o PT simplifica campos; no Docker os MACs são virtuais e atribuídos pelo Docker; o DNS embutido do Docker (nome `web`) não existe no PT.

## 9. Exercícios e questões
Q2.1–Q2.4. **Transferência:** monte no D04 uma captura que mostre o **mesmo IP origem** com **MAC origem diferente** antes e depois do roteador, e anote os quatro MACs envolvidos.

## 10. Revisão individual
- O que aprendi? ____ · Hipótese errada: ____ · Evidência decisiva: ____ · Não consigo explicar: ____ · Sem o roteiro: ____

## 11. Avaliação
- [ ] Expliquei o conceito sem consultar a solução.
- [ ] Implementei o laboratório.
- [ ] Validei os resultados com evidências.
- [ ] Investiguei pelo menos uma falha.
- [ ] Resolvi uma variação do problema.
- [ ] Registrei dificuldades e conclusões.

Obrigatórias: D1, D4, D6, D7 ([critérios](../docs/criterios-de-avaliacao.md)).
**Nível alcançado:** 0 / 1 / 2 / 3 **Próxima revisão:** ____ **Pendências:** ____
