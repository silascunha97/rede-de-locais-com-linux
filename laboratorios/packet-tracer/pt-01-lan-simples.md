# PT-01 — LAN simples (Módulo M01)

> **Status:** roteiro revisado estaticamente. **Não executado** (Packet Tracer indisponível na produção do caderno). Versão do PT usada por você: ____

Voltar: [Módulo 01](../../modulos/modulo-01-conceitos.md) · [GUIA](../../GUIA_DE_ESTUDOS.md)

**Objetivo técnico:** montar uma LAN de um segmento, verificar conectividade e entender o que a máscara determina.

**Topologia:** 1 switch 2960 (`SW1`) e 3 PCs, todos em cabo direto (Copper Straight-Through) nas portas Fa0/1–Fa0/3. Sem roteador.

| Dispositivo | IP | Máscara | Gateway |
|---|---|---|---|
| PC1 | 192.0.2.1 | 255.255.255.0 | — |
| PC2 | 192.0.2.2 | 255.255.255.0 | — |
| PC3 | 192.0.2.3 | 255.255.255.0 | — |

(Blocos de documentação, RFC 5737.)

## Procedimento
1. Adicione os dispositivos e cabos; aguarde os links ficarem verdes.
2. Em cada PC: *Desktop → IP Configuration* (Static) e preencha a tabela.
3. Teste no *Command Prompt*: `ping 192.0.2.2`, `ping 192.0.2.3` (a partir do PC1) e o inverso. O primeiro ping costuma perder 1 pacote por causa do ARP (**observe e explique**).

## Critério de conclusão
0% de perda entre todos os pares **e** você explicou por que o switch não precisa de IP para isso.

## Falha intencional
No PC3, use máscara 255.255.255.128 e IP 192.0.2.130. Teste os pings nos dois sentidos. **Antes de testar**, escreva sua previsão (quem alcança quem?). Depois explique o resultado com o cálculo da sub-rede de cada host.

## Simulation Mode (curto)
Alterne para *Simulation*, envie um ping PC1→PC2 e observe as PDUs (ARP primeiro, depois ICMP). Detalhes no [PT-02](pt-02-simulacao-pdu.md).

## Perguntas
1. Qual a diferença de função entre o link (verde) e a conectividade IP?
2. Que parte do atraso de um ping é de propagação, nesta simulação? (Pense no que o PT modela.)

## Evidências a registrar
Captura de tela da topologia final, saída dos pings, tabela de endereçamento, previsão e resultado da falha.

**Limite do simulador:** o PT não modela com fidelidade os atrasos de propagação/transmissão; o cálculo do M01 é analítico.
