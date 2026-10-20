# Módulo 01 — Conceitos básicos de redes e atrasos

**Status:** Não iniciado
**Dificuldade estimada:** Baixa
**Pré-requisitos:** PS26CP (noções de sinal e taxa); binário/decimal.
**Estimativa de esforço:** 6–8 h (estimativa minha; ajuste)
**Item do plano RC27CP:** 1 · Voltar: [GUIA](../GUIA_DE_ESTUDOS.md)

## 1. Problema norteador

Um colega afirma: "meu enlace é de 10 Mbps, então 12 MB chegam em 10 segundos". Outro diz que "depende de a rede ser comutada por pacotes ou por circuitos, e de quantos roteadores existem no caminho". Você precisa **decidir quem tem razão**, estimar o tempo para enviar um arquivo de 12 MB por um caminho de 3 enlaces de 10 Mbps com 2 roteadores *store-and-forward*, e **classificar** a rede da empresa (prédio, campus, cidade) e o modo de transmissão de cada link.

Resultado verificável: um cálculo documentado com cada parcela de atraso, e uma tabela de classificação com justificativa.

## 2. Investigação inicial (responda **antes** de ler a teoria)

- O que sabemos? _______________
- O que precisamos descobrir? _______________
- Hipóteses (≥ 2) e como testá-las:
  1. _______________ → teste: ______
  2. _______________ → teste: ______
- Palpite do tempo para 12 MB em 10 Mbps, 1 enlace: ____ s. Em 3 enlaces com 2 roteadores: ____ s.

## 3. Objetivos de aprendizagem

- [ ] Diferenciar Internet, internet, intranet e extranet.
- [ ] Classificar redes por tecnologia (ponto a ponto × difusão) e escala (PAN, LAN, MAN, WAN).
- [ ] Distinguir simplex, half e full-duplex.
- [ ] Calcular atrasos de transmissão (L/R) e de propagação (d/v) e explicar fila e processamento.
- [ ] Explicar *store-and-forward* e comparar comutação de pacotes com comutação de circuitos.

*Pré-requisitos conhecidos:* unidades (bit, byte, Mbps). *Novo:* os 5 itens acima.

## 4. Fundamentação teórica (mínima)

- **Atrasos por salto:** processamento + fila + transmissão (L/R) + propagação (d/v). Transmissão depende do tamanho e da taxa; propagação, da distância e do meio.
- **Store-and-forward:** o roteador recebe o pacote inteiro antes de encaminhar; dividir uma mensagem em pacotes permite *pipeline*.
- **Comutação de pacotes × circuitos:** pacotes compartilham enlaces (multiplexação estatística), toleram rajadas e sofrem fila/perda; circuitos reservam recursos.
- **Escala:** PAN/LAN/MAN/WAN (a classificação é por abrangência, não por tecnologia).

*Hipótese vs. fato:* "a Internet é a maior rede" é uma descrição, não uma definição; use as definições do livro-texto escolhido.

## 5. Leituras e fontes

- **Livro (Vigliazzi):** capítulo/seção introdutória sobre redes: ______ (preencher pelo sumário; ver [fontes](../docs/fontes-e-referencias.md#2-o-livro)). Pergunta-guia: o livro define LAN/WAN? Com que critério?
- **Referências básicas do plano:** Kurose & Ross (introdução, atrasos e comutação), Comer, Tanenbaum. Procure "atraso de transmissão" e "store-and-forward".
- **Documento acadêmico:** UFPR, lista 1 de Fundamentos de Redes & SD (tópicos LAN×WAN) — ver [fontes §3](../docs/fontes-e-referencias.md#3-fontes-acadêmicas-de-instituições-federais).
- **Questões:** Q1.1–Q1.5 em [banco-de-questoes.md](../docs/banco-de-questoes.md#m01--conceitos).
- **Documentação técnica:** nenhuma necessária (ping como ferramenta de observação de RTT: `man ping`).

## 5b. Solução preliminar (preencha antes do laboratório)
Hipótese principal: ____ · Justificativa: ____ · Resultado esperado dos pings: ____ · Riscos/limitações: ____ · Testes: ____

## 6. Laboratório Cisco Packet Tracer
[PT-01 — LAN simples](../laboratorios/packet-tracer/pt-01-lan-simples.md): LAN de 3 PCs, pings, falha de máscara. *Não executado pelo autor.*

## 7. Laboratório Docker
**Sem equivalente.** Atrasos de propagação/transmissão não existem de forma significativa numa bridge virtual local. Reproduzi-los exigiria `tc netem` (extensão opcional, não testada). Em vez disso use `ping` do seu host para um destino real e compare o RTT medido com a sua previsão de propagação, registrando que há fila e processamento envolvidos.

## 8. Análise comparativa
Só há PT neste módulo. Registre o que o PT **não** mostra (propagação real, filas).

## 9. Exercícios e questões
Q1.1–Q1.5. Transferência: refaça o cálculo do problema com a mensagem dividida em pacotes de 1500 B; o que muda e por quê? (Veja a Q1.3 para o mecanismo; resolva sem copiá-la.)

## 10. Revisão individual
- O que aprendi? ____
- Qual hipótese estava errada? ____
- Qual evidência foi decisiva? ____
- O que ainda não consigo explicar? ____
- Como resolveria um problema semelhante sem o roteiro? ____

## 11. Avaliação
- [ ] Expliquei o conceito sem consultar a solução.
- [ ] Implementei o laboratório.
- [ ] Validei os resultados com evidências.
- [ ] Investiguei pelo menos uma falha.
- [ ] Resolvi uma variação do problema.
- [ ] Registrei dificuldades e conclusões.

Dimensões obrigatórias: D1, D2, D6, D8 ([critérios](../docs/criterios-de-avaliacao.md)).
**Nível alcançado:** 0 / 1 / 2 / 3 **Próxima revisão:** ____ **Pendências:** ____
