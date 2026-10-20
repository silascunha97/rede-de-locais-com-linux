# PT-04 — Transporte no Packet Tracer (limitado) (Módulo M04)

> **Status:** revisado estaticamente; **não executado**. Versão do PT: ____

Voltar: [Módulo 04](../../modulos/modulo-04-transporte.md)

**Aviso de limitação:** o PT **não** modela com fidelidade o TCP (janela, retransmissão, congestionamento). Este laboratório serve para ver portas e o início/fim das conexões e para contrastar com o [D03](../docker/d03-transporte/README.md), que usa captura real.

**Topologia:** a do [PT-03](pt-03-dns-http.md) (Web + DNS + PC).

## Procedimento
1. Em *Simulation*, filtre **TCP**, **UDP**, **HTTP**, **DNS**.
2. Acesse `http://web.lab.test` e liste as PDUs de transporte: qual protocolo cada uma usa e quais portas aparecem em *PDU Details → Layer 4*? (DNS deve usar UDP/53; HTTP, TCP/80.)
3. Procure PDUs com flags TCP (SYN, ACK, FIN) na aba de detalhes e registre quais você **viu** e quais **não** viu.

## Critério
Tabela com: PDU, protocolo de transporte, porta de origem, porta de destino. Explicação de por que as portas de origem são diferentes entre acessos.

## Falha intencional
No servidor Web, desligue o serviço HTTP e acesse de novo. Descreva o que o navegador mostra e o que o Simulation Mode mostra, sem especular além do observado.

## Perguntas
1. O que o PT mostrou do handshake? O que faltou comparado ao D03?
2. Por que a limitação do simulador não invalida o estudo do conceito?

## Evidências
Telas dos detalhes de camada 4 e a tabela.
