# PT-07 — ARP e tabela MAC do switch (Módulo M07)

> **Status:** revisado estaticamente; **não executado**. Versão do PT: ____

Voltar: [Módulo 07](../../modulos/modulo-07-enlace-switching.md)

**Objetivo:** observar como o switch aprende endereços MAC e como o ARP resolve IP→MAC.

**Topologia:** SW1 (2960) e PC1, PC2, PC3 (192.0.2.1–.3 /24).

## Procedimento
1. **Antes de qualquer tráfego**, no CLI do switch: `show mac address-table`. Registre.
2. PC1 `arp -d` (limpa cache) e `arp -a`. Registre.
3. Em *Simulation*, filtros ARP e ICMP: PC1 envia `ping 192.0.2.2`. Acompanhe: quem recebe o ARP request (broadcast)? Quem responde?
4. Após o ping: `show mac address-table` e `arp -a` no PC1. Compare com os valores iniciais.
5. Repita o ping e observe o que muda no Simulation (ARP reaparece?).

## Critério
Explicar: (a) por que o broadcast chega a todos, e o unicast só ao destino; (b) o que o switch aprendeu e de qual campo (MAC de **origem**); (c) como a tabela cresce.

## Falha intencional
Pingue um IP inexistente (192.0.2.99). O que o PC1 mostra, e o que aparece na tabela ARP? **Hipótese antes.**

## Extensão (fora do plano)
Duas VLANs (`vlan 10`, `switchport mode access`, `switchport access vlan 10`) e o efeito sobre o broadcast. Verifique os comandos na sua versão.

## Evidências
Saídas de `show mac address-table` antes/depois; `arp -a`; telas do Simulation.

## Comparação com o D05
O D05 mostra ARP e vizinhos, mas a bridge Docker não oferece `show mac address-table` ([D05](../docker/d05-enlace-arp/README.md)).
