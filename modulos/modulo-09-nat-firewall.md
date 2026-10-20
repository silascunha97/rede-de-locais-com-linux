# Módulo 09 — NAT e firewall (trilha complementar)

**Status:** Não iniciado
**Dificuldade estimada:** Alta
**Pré-requisitos:** [M04](modulo-04-transporte.md), [M06](modulo-06-roteamento.md)
**Estimativa de esforço:** 8–10 h (estimativa minha)
**Origem:** **fora do plano RC27CP** (pedido do projeto pedagógico). Estudar após o núcleo. Voltar: [GUIA](../GUIA_DE_ESTUDOS.md)

## 1. Problema norteador
Uma rede interna (`192.0.2.0/24`) precisa acessar um servidor de outra rede (`203.0.113.0/24`) que **não conhece** a rede interna e não pode ser alterado. Além disso, o administrador quer **bloquear HTTP** dos clientes internos mantendo o ping. Faça funcionar, explique o que o servidor enxerga como origem, prove com evidência que o bloqueio é **por porta** e não por host, e diga por que o caminho inverso (servidor → rede interna) continua impossível.

## 2. Investigação inicial
- O que sabemos? ____ · Descobrir? ____
- Hipóteses de por que o acesso falha sem NAT (rota de volta?): ____
- Evidência no servidor (captura de origem do pacote, log): ____

## 3. Objetivos de aprendizagem
- [ ] Explicar NAT (masquerade/overload): o que é reescrito, onde, e o papel da tabela de tradução.
- [ ] Distinguir NAT de filtragem; filtragem sem estado × com estado (conceito).
- [ ] Escrever regra de bloqueio por protocolo/porta e comprovar por contadores.
- [ ] Explicar publicação de porta (DNAT) e comparar `ports:` do Docker.

## 4. Fundamentação teórica (mínima)
NAT reescreve endereços (e portas) e guarda o mapeamento para devolver as respostas. Firewall decide aceitar/descartar por critérios (origem, destino, protocolo, porta). Em Linux: `nat/POSTROUTING` para masquerade; `filter/FORWARD` para tráfego roteado; ACLs em IOS. Efeitos colaterais do NAT (end-to-end) e IPv6: discussão opcional.

## 5. Leituras e fontes
- **Livro (Vigliazzi):** seção de compartilhamento de acesso/firewall: ____ (preencher; **o livro pode usar `ipchains`/`iptables` legado**: confira o equivalente atual).
- **Plano RC27CP:** não lista NAT/firewall.
- **Acadêmico:** sem fonte confirmada (lacuna).
- **Questões:** Q9.1–Q9.4.
- **Técnica:** `man iptables`, documentação do Docker sobre filtragem de pacotes e publicação de portas; documentação Cisco de NAT/ACL (IOS).

## 5b. Solução preliminar
Hipótese: ____ · Justificativa: ____ · Regras: ____ · Esperado: ____ · Riscos: ____ · Testes: ____

## 6. Laboratório Cisco Packet Tracer
[PT-08 — NAT com sobrecarga e ACL](../laboratorios/packet-tracer/pt-08-nat-acl.md). *Não executado pelo autor.*

## 7. Laboratório Docker
[D06 — NAT e firewall](../laboratorios/docker/d06-nat-firewall/README.md). **Executado** em 2026-10-20: sem NAT (`000`), com NAT (`200`, origem `203.0.113.254` no log), bloqueio TCP/80 com ping preservado.

## 8. Análise comparativa
Comparáveis: tradução e filtragem. Não equivalentes: IOS (ACL por interface) × `iptables` (cadeias/tabelas); o Docker também faz NAT próprio para saída e publicação de portas, **independente** do NAT criado no `gw` — não os confunda.

## 9. Exercícios
Q9.1–Q9.4. **Transferência:** T.4.

## 10. Revisão individual
- Aprendi: ____ · Hipótese errada: ____ · Evidência decisiva: ____ · Não explico: ____ · Sem o roteiro: ____

## 11. Avaliação
- [ ] Expliquei o conceito sem consultar a solução.
- [ ] Implementei o laboratório.
- [ ] Validei os resultados com evidências.
- [ ] Investiguei pelo menos uma falha.
- [ ] Resolvi uma variação do problema.
- [ ] Registrei dificuldades e conclusões.

Obrigatórias: D4, D5, D6, D7.
**Nível alcançado:** 0 / 1 / 2 / 3 **Próxima revisão:** ____ **Pendências:** ____
