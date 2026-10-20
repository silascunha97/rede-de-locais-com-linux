# Módulo 04 — Camada de transporte: TCP e UDP

**Status:** Não iniciado
**Dificuldade estimada:** Média-alta
**Pré-requisitos:** [M02](modulo-02-camadas-encapsulamento.md), [M03](modulo-03-aplicacao-dns-http.md)
**Estimativa de esforço:** 8–10 h (estimativa minha)
**Item do plano RC27CP:** 4 · Voltar: [GUIA](../GUIA_DE_ESTUDOS.md)

## 1. Problema norteador

Um host oferece dois serviços de teste: um sobre **TCP** (porta 5000) e outro sobre **UDP** (porta 5001). O administrador desliga ambos e executa o mesmo teste de conectividade. Um dos clientes recebe um erro imediato; o outro "parece ter enviado". Explique a diferença com **evidência de captura** e diga por que isso importa para escolher o protocolo de uma aplicação.

Resultado verificável: duas capturas comentadas (TCP com handshake e término; UDP sem), e previsão da captura **antes** de rodar.

## 2. Investigação inicial
- O que sabemos? ____ · Precisamos descobrir? ____
- Hipóteses sobre por que o UDP não "reclama": ____
- Como cada hipótese seria confirmada (captura? código de saída?): ____

## 3. Objetivos de aprendizagem
- [ ] Explicar multiplexação/demultiplexação por portas e a quádrupla de uma conexão TCP.
- [ ] Descrever o handshake de 3 vias e o encerramento.
- [ ] Calcular números de sequência/ACK em exemplos simples.
- [ ] Distinguir controle de fluxo e de congestionamento (conceito).
- [ ] Justificar TCP × UDP para um caso de uso.

## 4. Fundamentação teórica (mínima)
UDP: sem conexão, sem confirmação, cabeçalho curto. TCP: orientado à conexão, fluxo confiável, ordenado, com confirmações e retransmissão; controle de fluxo protege o receptor, controle de congestionamento protege a rede. Detalhes de algoritmos (Reno/CUBIC) **não** são exigidos aqui.

## 5. Leituras e fontes
- **Livro (Vigliazzi):** ____ (preencher; pode não cobrir teoria de TCP a fundo: complemente com Kurose & Ross).
- **Plano:** item 4 (multiplexação, conexão, congestionamento, UDP, TCP).
- **Acadêmico:** UFPR lista 1 (escolha entre TCP e UDP; identificação de aplicações).
- **Questões:** Q4.1–Q4.4.
- **Técnica:** RFC 9293 (TCP), RFC 768 (UDP); `man ss`, `man tcpdump`.

## 5b. Solução preliminar
Hipótese: ____ · Justificativa: ____ · Esperado (**escreva a captura prevista**): ____ · Riscos: ____ · Testes: ____

## 6. Laboratório Cisco Packet Tracer
[PT-04 — Transporte (limitado)](../laboratorios/packet-tracer/pt-04-transporte.md). **Limitação:** o PT não modela o TCP em detalhe. *Não executado pelo autor.*

## 7. Laboratório Docker
[D03 — TCP × UDP](../laboratorios/docker/d03-transporte/README.md). **Executado** em 2026-10-20: handshake `S`, `S.`, `.`; término `F.`; UDP com 1 pacote sem resposta.

## 8. Análise comparativa
O PT ajuda a ver portas; o Docker mostra o protocolo real. Controle de congestionamento **não é observável** em nenhum dos dois neste caderno (rede sem perda).

## 9. Exercícios
Q4.1–Q4.4. **Transferência:** T.2 (trocar portas/protocolos e prever a captura).

## 10. Revisão individual
- Aprendi: ____ · Hipótese errada: ____ · Evidência decisiva: ____ · Não explico: ____ · Sem o roteiro: ____

## 11. Avaliação
- [ ] Expliquei o conceito sem consultar a solução.
- [ ] Implementei o laboratório.
- [ ] Validei os resultados com evidências.
- [ ] Investiguei pelo menos uma falha.
- [ ] Resolvi uma variação do problema.
- [ ] Registrei dificuldades e conclusões.

Obrigatórias: D1, D6, D7, D8.
**Nível alcançado:** 0 / 1 / 2 / 3 **Próxima revisão:** ____ **Pendências:** ____
