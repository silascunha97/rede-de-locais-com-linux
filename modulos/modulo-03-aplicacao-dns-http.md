# Módulo 03 — Camada de aplicação: DNS e HTTP

**Status:** Não iniciado
**Dificuldade estimada:** Média
**Pré-requisitos:** [M02](modulo-02-camadas-encapsulamento.md)
**Estimativa de esforço:** 8–10 h (estimativa minha)
**Item do plano RC27CP:** 3 (HTTP, FTP, SMTP, DNS, SSH). Este módulo aprofunda DNS e HTTP; **FTP, SMTP e SSH ficam só como leitura** (sem laboratório) — lacuna assumida, ver [plano](../docs/plano-de-estudos.md#3-lacunas).

## 1. Problema norteador

Uma pequena empresa publica um site interno. Os usuários digitam `http://web.lab.test`, mas "a página não abre". O técnico garante que o servidor está no ar porque "pelo IP funciona". Você deve **descobrir onde está a falha** e **construir a resolução de nomes do zero**, de modo que cada afirmação sua tenha uma evidência (comando ou captura).

Resultado verificável: o site abre por nome; você demonstra o que mudou ao quebrar e consertar a resolução.

## 2. Investigação inicial
- O que sabemos? ____ · O que descobrir? ____
- Hipóteses (≥ 3, ver Q3.3): ____
- Evidência que confirmaria/descartaria cada uma: ____
- Quando o acesso por IP funciona, o que isso prova e o que **não** prova?

## 3. Objetivos de aprendizagem
- [ ] Explicar o modelo cliente-servidor e portas de DNS/HTTP/SMTP/FTP/SSH.
- [ ] Descrever a resolução de nomes (recursiva × iterativa; registros A/AAAA).
- [ ] Usar `dig`/`nslookup` e interpretar `status`, `ANSWER` e o servidor consultado.
- [ ] Explicar a sequência DNS→TCP→HTTP.
- [ ] Diagnosticar falha de nome versus falha de serviço.

## 4. Fundamentação teórica (mínima)
DNS mapeia nomes a endereços; normalmente UDP/53 (TCP/53 para respostas grandes). HTTP/1.x usa TCP/80 (TLS/443 está fora do escopo do plano). O cliente consulta o resolvedor configurado; o resolvedor pode encaminhar. SMTP/25, FTP/21 (+dados), SSH/22: **apenas conceito** aqui.

## 5. Leituras e fontes
- **Livro (Vigliazzi):** seções sobre serviços de rede (DNS/Web): ____ (preencher; é onde o livro tende a ser mais útil).
- **Plano:** item 3. **Kurose & Ross / Comer / Tanenbaum:** capítulo de camada de aplicação.
- **Acadêmico:** nenhuma questão de DNS foi confirmada nas fontes lidas (lacuna).
- **Questões:** Q3.1–Q3.3.
- **Técnica:** RFC 1034/1035; `man dig`; documentação do dnsmasq; docs do Docker sobre DNS embutido.

## 5b. Solução preliminar
Hipótese: ____ · Justificativa: ____ · Alterações: ____ · Esperado: ____ · Riscos: ____ · Testes: ____

## 6. Laboratório Cisco Packet Tracer
[PT-03 — DNS e HTTP](../laboratorios/packet-tracer/pt-03-dns-http.md). *Não executado pelo autor.*

## 7. Laboratório Docker
[D02 — dnsmasq](../laboratorios/docker/d02-dns/README.md). **Executado** em 2026-10-20: resolução OK, log do servidor, e `SERVFAIL` na falha. Importante: o cliente consulta o DNS embutido do Docker, que encaminha ao dnsmasq.

## 8. Análise comparativa
Comparáveis: registro A, ordem DNS→HTTP. Não equivalentes: o DNS do PT é simplificado; no Docker há um intermediário (127.0.0.11) que a rede real não tem; nenhum dos dois tem a hierarquia raiz/TLD.

## 9. Exercícios
Q3.1–Q3.3. **Transferência:** acrescente um segundo nome (`api.lab.test`) apontando para outro container sem copiar o procedimento; explique o que precisou mudar.

## 10. Revisão individual
- Aprendi: ____ · Hipótese errada: ____ · Evidência decisiva: ____ · Não explico: ____ · Sem o roteiro: ____

## 11. Avaliação
- [ ] Expliquei o conceito sem consultar a solução.
- [ ] Implementei o laboratório.
- [ ] Validei os resultados com evidências.
- [ ] Investiguei pelo menos uma falha.
- [ ] Resolvi uma variação do problema.
- [ ] Registrei dificuldades e conclusões.

Obrigatórias: D2, D4, D5, D6.
**Nível alcançado:** 0 / 1 / 2 / 3 **Próxima revisão:** ____ **Pendências:** ____
