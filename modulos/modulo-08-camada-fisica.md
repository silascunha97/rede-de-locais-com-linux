# Módulo 08 — Camada física

**Status:** Não iniciado
**Dificuldade estimada:** Baixa-média
**Pré-requisitos:** [M01](modulo-01-conceitos.md)
**Estimativa de esforço:** 4–6 h (estimativa minha)
**Item do plano RC27CP:** 6 (camada física: meios, modos de transmissão, codificação) · Voltar: [GUIA](../GUIA_DE_ESTUDOS.md)

> Módulo **sem laboratório** (Packet Tracer e Docker não reproduzem sinais, meios nem codificação). Ausência justificada, não omitida.

## 1. Problema norteador
Um prédio precisa ligar um andar a outro: 80 m entre os armários, 1 Gbps, em um corredor com motores elétricos. Escolha o **meio** (par trançado, fibra, sem fio) e justifique contra atenuação, interferência, custo e distância. Em seguida, mostre como o bit `10110` é representado por dois esquemas de codificação.

Resultado verificável: justificativa escrita e as duas formas de onda desenhadas.

## 2. Investigação inicial
- O que sabemos? ____ · Descobrir? ____ · Hipóteses de escolha de meio: ____ · Como validaria? (consulta de limites de distância no padrão/ livro): ____

## 3. Objetivos de aprendizagem
- [ ] Comparar par trançado, fibra e meios sem fio.
- [ ] Explicar atenuação, ruído e interferência.
- [ ] Codificar bits em NRZ e Manchester.
- [ ] Distinguir simplex, half e full-duplex (retoma M01).

## 4. Fundamentação teórica (mínima)
Os meios diferem em banda, alcance, custo e imunidade a EMI. Codificações definem como o bit vira sinal; Manchester garante transição por bit (útil para sincronismo), com o dobro da taxa de sinalização. **Limites de distância/categorias de cabo:** consulte o livro ou o padrão aplicável; não os afirmo aqui.

## 5. Leituras e fontes
- **Livro (Vigliazzi):** ____ (preencher).
- **Plano:** item 6 (meios de transmissão, técnicas de codificação). **Kurose & Ross / Tanenbaum:** camada física.
- **Acadêmico:** sem questão confirmada.
- **Questões:** Q8.1–Q8.3.

## 5b. Solução preliminar
Escolha de meio: ____ · Justificativa: ____ · Riscos/limitações: ____

## 6–7. Laboratórios
**Packet Tracer:** sem equivalente (o PT escolhe o tipo de cabo, mas não simula sinal). **Docker:** sem equivalente.

## 8. Análise comparativa
Não aplicável. Observação útil: o PT exige cabo "certo" (direto × cruzado) e mostra link vermelho/verde: é uma abstração da camada física, não sua simulação.

## 9. Exercícios
Q8.1–Q8.3.

## 10. Revisão individual
- Aprendi: ____ · Hipótese errada: ____ · Evidência decisiva: ____ · Não explico: ____ · Sem o roteiro: ____

## 11. Avaliação
- [ ] Expliquei o conceito sem consultar a solução.
- [ ] Implementei o laboratório (**não se aplica**).
- [ ] Validei os resultados com evidências (exercícios resolvidos e revisados).
- [ ] Investiguei pelo menos uma falha (**não se aplica**).
- [ ] Resolvi uma variação do problema.
- [ ] Registrei dificuldades e conclusões.

Obrigatórias: D1, D8, D9.
**Nível alcançado:** 0 / 1 / 2 / 3 **Próxima revisão:** ____ **Pendências:** ____
