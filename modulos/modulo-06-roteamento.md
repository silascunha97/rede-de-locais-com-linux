# Módulo 06 — Repasse e roteamento

**Status:** Não iniciado
**Dificuldade estimada:** Alta
**Pré-requisitos:** [M05](modulo-05-ipv4-subredes.md)
**Estimativa de esforço:** 10–12 h (estimativa minha)
**Item do plano RC27CP:** 5 (repasse e roteamento, algoritmos de roteamento) · Voltar: [GUIA](../GUIA_DE_ESTUDOS.md)

## 1. Problema norteador

Após interligar duas LANs por um roteador, o `ping` de A para B **envia** pacotes, o roteador **os encaminha** e B os **recebe**, mas A nunca recebe resposta. Descubra por que, localize o ponto da falha com evidências em cada salto, corrija, e explique **qual regra** o roteador usa para escolher entre uma rota específica e uma rota padrão.

Resultado verificável: diagnóstico em 4 passos com um comando por passo, e rota restaurada.

## 2. Investigação inicial
- O que sabemos? ____ · O que descobrir? ____
- Hipóteses: ____ (rota de volta? gateway do destino? filtragem?)
- O que você capturaria e **onde**, para saber até que ponto o pacote chega? ____

## 3. Objetivos de aprendizagem
- [ ] Diferenciar repasse (por pacote, via tabela) de roteamento (cálculo da tabela).
- [ ] Aplicar o prefixo mais longo e a rota padrão.
- [ ] Configurar rotas estáticas e perceber que são necessárias **ida e volta**.
- [ ] Diagnosticar com `traceroute`, tabela de rotas e captura no roteador.
- [ ] Descrever (conceito) vetor de distância e estado de enlace.

## 4. Fundamentação teórica (mínima)
O roteador procura o prefixo mais longo que casa com o destino; `0.0.0.0/0` é a rota padrão. Rotas podem ser conectadas, estáticas ou aprendidas por protocolo. Vetor de distância: troca de custos entre vizinhos (Bellman-Ford); estado de enlace: topologia completa + Dijkstra. RIP/OSPF: apenas conceito; extensão opcional no PT.

## 5. Leituras e fontes
- **Livro (Vigliazzi):** seção sobre roteamento/gateway em Linux: ____ (preencher; comandos antigos: `route` → `ip route`).
- **Plano:** item 5 (algoritmos de roteamento, roteamento na Internet).
- **Acadêmico:** UFPR lista 1 (roteamento direto/indireto, tabela de roteamento, traceroute/ICMP).
- **Questões:** Q6.1–Q6.4.
- **Técnica:** `man ip-route`; RFC 792 (ICMP, base do traceroute); documentação Cisco IOS de `ip route`.

## 5b. Solução preliminar
Hipótese: ____ · Justificativa: ____ · Alterações: ____ · Esperado: ____ · Riscos: ____ · Testes: ____

## 6. Laboratório Cisco Packet Tracer
[PT-06 — dois roteadores, rotas estáticas](../laboratorios/packet-tracer/pt-06-rotas-estaticas.md). *Não executado pelo autor.*

## 7. Laboratório Docker
[D04 — partes B e falhas 1–3](../laboratorios/docker/d04-roteador/README.md#parte-b--roteamento-m06). **Executado** em 2026-10-20, incluindo as três falhas.
**Atenção às armadilhas** que o autor encontrou: redes `internal` impedem o roteamento; `sysctl -w ip_forward` falha no container; o gateway `.1` do Docker aparece como "salto 1" quando falta a rota.

## 8. Análise comparativa
Comparáveis: `show ip route` × `ip route`, `tracert` × `traceroute`, "ida chega, volta não". Não equivalentes: IOS × kernel Linux; o PT permite protocolos dinâmicos (verificar versão), o laboratório Docker não os implementa; Docker tem gateway próprio que não existe no PT.

## 9. Exercícios
Q6.1–Q6.4. **Transferência:** T.3 (terceira rede no D04).

## 10. Revisão individual
- Aprendi: ____ · Hipótese errada: ____ · Evidência decisiva: ____ · Não explico: ____ · Sem o roteiro: ____

## 11. Avaliação
- [ ] Expliquei o conceito sem consultar a solução.
- [ ] Implementei o laboratório.
- [ ] Validei os resultados com evidências.
- [ ] Investiguei pelo menos uma falha.
- [ ] Resolvi uma variação do problema.
- [ ] Registrei dificuldades e conclusões.

Obrigatórias: D4, D5, D6, D7, D8.
**Nível alcançado:** 0 / 1 / 2 / 3 **Próxima revisão:** ____ **Pendências:** ____
