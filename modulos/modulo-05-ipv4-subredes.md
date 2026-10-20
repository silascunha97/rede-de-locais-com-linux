# Módulo 05 — IPv4, máscaras e sub-redes

**Status:** Não iniciado
**Dificuldade estimada:** Média-alta (cálculo)
**Pré-requisitos:** [M02](modulo-02-camadas-encapsulamento.md); binário/decimal (faça o diagnóstico D.1–D.2).
**Estimativa de esforço:** 10–12 h (estimativa minha)
**Item do plano RC27CP:** 5 (protocolo IP, endereçamento) · Voltar: [GUIA](../GUIA_DE_ESTUDOS.md)

## 1. Problema norteador

Duas estações, PC1 (`192.0.2.10/24`) e PC3 (`198.51.100.10/24`), têm interfaces ativas e links verdes, mas **não se comunicam**. Em outra ocorrência, um host com IP `192.0.2.130/25` e gateway `192.0.2.1` não sai da própria rede. Você deve (a) explicar, usando só endereço, máscara e gateway, por que a comunicação falha; (b) projetar o endereçamento de uma empresa com três segmentos usando um único bloco `203.0.113.0/24`; (c) validar na prática.

Resultado verificável: tabela de endereçamento sem sobreposição, e prova por comando de cada diagnóstico.

## 2. Investigação inicial
- O que sabemos? ____ · O que descobrir? ____
- Hipóteses (máscara, gateway, rota, cabo…): ____
- Evidência de cada uma (`ipconfig`/`ip addr`, `ip route`, `ping` ao gateway): ____
- Como um host decide se o destino é "local" ou precisa de gateway? Palpite: ____

## 3. Objetivos de aprendizagem
- [ ] Converter entre decimal e binário e aplicar máscaras (rede, broadcast, faixa).
- [ ] Dividir um bloco em sub-redes iguais e com VLSM, sem sobreposição.
- [ ] Explicar a decisão local × via gateway.
- [ ] Explicar o papel do gateway e por que ele deve estar **na** sub-rede do host.
- [ ] Configurar um roteador com duas interfaces e provar a conectividade.

## 4. Fundamentação teórica (mínima)
O prefixo (/n) separa rede e host. Rede = IP AND máscara. Hosts utilizáveis = 2ⁿ−2 (exceções /31, /32). Um host compara o destino com sua própria rede: se igual, ARP direto; senão, envia ao gateway. IPv6 e classes históricas: fora deste módulo (extensão: classes aparecem na lista da UFPR).

## 5. Leituras e fontes
- **Livro (Vigliazzi):** seção de endereçamento IP/configuração de interface: ____ (preencher). *Atenção:* o livro pode usar `ifconfig`/`route`; use `ip addr` e `ip route`.
- **Plano:** item 5. **Kurose & Ross/Comer:** capítulo de camada de rede (endereçamento, CIDR).
- **Acadêmico:** UFPR lista 1 (endereçamento IP, sub-redes, máscara, CIDR).
- **Questões:** Q5.1–Q5.5.
- **Técnica:** RFC 791, RFC 4632 (CIDR), RFC 3021 (/31), RFC 5737; `man ip`.

## 5b. Solução preliminar
Hipótese: ____ · Justificativa: ____ · Tabela de endereçamento proposta: ____ · Riscos: ____ · Testes: ____

## 6. Laboratório Cisco Packet Tracer
[PT-05 — dois segmentos, um roteador](../laboratorios/packet-tracer/pt-05-subredes-um-roteador.md). *Não executado pelo autor.*

## 7. Laboratório Docker
[D04 — parte A](../laboratorios/docker/d04-roteador/README.md#parte-a--endereçamento-e-gateway-m05). **Executado** em 2026-10-20. Docker usa IPAM (atribuição automática); aqui o endereçamento é fixado no `compose.yaml` e o `.1` pertence ao Docker.

## 8. Análise comparativa
O cálculo de sub-redes é **independente** de ferramenta. No PT você configura manualmente; no Docker, o IPAM declara a sub-rede. Em ambos, a falha de gateway tem o mesmo sintoma.

## 9. Exercícios
Q5.1–Q5.5, D.1–D.2. **Transferência:** T.1 (3 segmentos com VLSM no PT, sem consultar).

## 10. Revisão individual
- Aprendi: ____ · Hipótese errada: ____ · Evidência decisiva: ____ · Não explico: ____ · Sem o roteiro: ____

## 11. Avaliação
- [ ] Expliquei o conceito sem consultar a solução.
- [ ] Implementei o laboratório.
- [ ] Validei os resultados com evidências.
- [ ] Investiguei pelo menos uma falha.
- [ ] Resolvi uma variação do problema.
- [ ] Registrei dificuldades e conclusões.

Obrigatórias: D3, D4, D5, D8.
**Nível alcançado:** 0 / 1 / 2 / 3 **Próxima revisão:** ____ **Pendências:** ____
