# PT-02 — Simulation Mode: ver o encapsulamento (Módulo M02)

> **Status:** revisado estaticamente; **não executado**. Versão do PT: ____

Voltar: [Módulo 02](../../modulos/modulo-02-camadas-encapsulamento.md)

**Objetivo:** observar camada a camada o que muda entre origem e destino, **em dois cenários**: mesma rede e redes diferentes.

**Topologia:** a do [PT-01](pt-01-lan-simples.md) para o cenário 1. Para o cenário 2 use a do [PT-05](pt-05-subredes-um-roteador.md) (já com roteador).

## Procedimento
1. Mude para *Simulation* (canto inferior direito). Em *Edit Filters* deixe só **ARP**, **ICMP** e, no cenário de serviços, **HTTP/DNS/TCP/UDP**.
2. Cenário 1 (PC1→PC2): envie `ping`; use *Capture/Forward* e clique em cada PDU. Abra *Inbound/Outbound PDU Details* e, em cada dispositivo, a aba **OSI Model**.
3. Cenário 2 (PC1→PC3 através de R1): repita.
4. Preencha a tabela:

| Salto | MAC origem | MAC destino | IP origem | IP destino | Protocolo |
|---|---|---|---|---|---|
| PC1 → SW1 | | | | | |
| SW1 → R1 | | | | | |
| R1 → SW2 | | | | | |
| SW2 → PC3 | | | | | |

## Critérios
- Identifiquei quais campos mudam e quais permanecem no cenário 2, e expliquei por quê.
- Expliquei por que o ARP precede o ICMP **no primeiro ping** e por que o ARP do cenário 2 pergunta pelo **gateway**.

## Perguntas
1. Que camadas o switch processa? E o roteador? (Veja a aba OSI Model de cada um.)
2. O que o campo TTL faz e como muda?

## Evidências
Capturas de tela dos detalhes de PDU e a tabela preenchida.

## Limites
O PT mostra o que o simulador modela; alguns campos (checksums, opções) são simplificados. Compare com a captura real do [D01](../docker/d01-encapsulamento/README.md).
