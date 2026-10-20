# Projeto integrador — rede de uma pequena empresa

Seção 17 do [GUIA_DE_ESTUDOS.md](../GUIA_DE_ESTUDOS.md). **Pré-requisito:** M01–M07 e M09 com nível ≥ 2.

## Cenário
Uma empresa de 3 setores precisa de uma rede interna e acesso a um servidor de serviços:

| Setor | Hosts necessários (com folga de 20%) |
|---|---|
| Atendimento | 50 |
| Desenvolvimento | 25 |
| Servidores internos | 10 |

Use **um bloco 203.0.113.0/24** para as redes internas (VLSM; decisão e justificativa suas) e **198.51.100.0/30** para o enlace com a "operadora" (servidor externo simulado). Nomes sob `.test`. (Blocos de documentação, RFC 5737.)

## Requisitos obrigatórios
1. **Diagrama lógico** e **plano de endereçamento** sem sobreposição, com a conta da dimensão de cada sub-rede.
2. **Roteamento:** um roteador interno, rota padrão para a operadora (estática).
3. **Serviços:** DNS interno (`web.empresa.test`) e HTTP.
4. **Segurança básica:** NAT para saída; bloqueio de HTTP do setor Atendimento para o setor Servidores **exceto** ao servidor web; ping liberado só entre administradores (decida e justifique qual host).
5. **Packet Tracer:** topologia completa e configuração exportável (`show running-config`).
6. **Docker:** equivalente dos itens 2–4 (roteador Linux, `dnsmasq`, `nginx`, `iptables`), reaproveitando D02, D04 e D06; **sem** `privileged`, `host` ou `macvlan`; sem portas publicadas.
7. **Testes documentados:** matriz origem×destino×serviço (esperado × observado).
8. **Duas falhas** provocadas por você, diagnosticadas com evidência e corrigidas.
9. **Relatório técnico** (modelo abaixo).

## Decisões que você precisa justificar (sem resposta única)
- Quantas sub-redes, que prefixos e por quê (reserva para crescimento).
- Onde aplicar o filtro (entrada, saída, FORWARD) e por que ali.
- O que **não** é equivalente entre PT e Docker no seu projeto.

## Extensões opcionais (não preparadas pelos módulos)
DHCP, VLAN por setor, roteamento dinâmico, IPv6, `tc netem` para atraso/perda.

## Cenários de falha (escolha 2 e, se quiser, peça a alguém para aplicar uma terceira sem avisar)
Rota de volta ausente · registro DNS removido · regra de firewall com ordem errada · máscara errada em um host · NAT ausente.

## Relatório técnico — estrutura
1. Resumo e requisitos · 2. Diagrama e endereçamento · 3. Decisões e justificativas · 4. Implementação PT · 5. Implementação Docker · 6. Matriz de testes · 7. Falhas e diagnósticos (com evidência) · 8. Comparação PT × Docker e limitações · 9. Reflexão: o que eu faria diferente.

## Critérios (pesos sugeridos)
| Critério | Peso |
|---|---|
| Endereçamento correto e justificado | 25% |
| Conectividade e serviços (PT) | 20% |
| Equivalente Docker funcional e reprodutível | 20% |
| Diagnóstico com evidências | 20% |
| Relatório e registro | 15% |

Nível 3 do projeto exige que **outra pessoa** consiga reproduzir o ambiente Docker só com o seu repositório e o relatório, e que você diagnostique uma falha aplicada sem aviso.

**Status:** Não iniciado · **Nível:** __ · **Data:** __
