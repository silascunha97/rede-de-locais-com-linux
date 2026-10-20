# PT-06 — Dois roteadores e rotas estáticas (Módulo M06)

> **Status:** revisado estaticamente; **não executado**. Versão do PT: ____ (roteadores 1941; confirme interfaces).

Voltar: [Módulo 06](../../modulos/modulo-06-roteamento.md)

**Objetivo:** interligar duas LANs por um enlace ponto a ponto com rotas estáticas; diagnosticar rota de ida/volta.

**Topologia:** `PC1 — SW1 — R1 — R2 — SW2 — PC2`. Enlace R1 g0/1 ↔ R2 g0/0 com cabo **cruzado** (ou direto, se o PT aplicar auto-MDIX; verifique o link verde).

| Rede | Prefixo | Dispositivos |
|---|---|---|
| LAN1 | 192.0.2.0/24 | R1 g0/0 = .254; PC1 = .1 (gw .254) |
| Enlace | 198.51.100.0/30 | R1 g0/1 = .1; R2 g0/0 = .2 |
| LAN2 | 203.0.113.0/24 | R2 g0/1 = .254; PC2 = .1 (gw .254) |

## Configuração
```
! R1
interface g0/0
 ip address 192.0.2.254 255.255.255.0
 no shutdown
interface g0/1
 ip address 198.51.100.1 255.255.255.252
 no shutdown
ip route 203.0.113.0 255.255.255.0 198.51.100.2
! R2
interface g0/0
 ip address 198.51.100.2 255.255.255.252
 no shutdown
interface g0/1
 ip address 203.0.113.254 255.255.255.0
 no shutdown
ip route 192.0.2.0 255.255.255.0 198.51.100.1
```
(Os comandos `ip route` são dados em modo de configuração global.)

## Testes
`ping`/`tracert` PC1→PC2; `show ip route` nos dois roteadores (rotas `S`). **Esperado:** 3 saltos no tracert.

## Falhas (hipótese antes)
1. Apague a rota de R2 (`no ip route 192.0.2.0 255.255.255.0 198.51.100.1`): quem responde e quem não responde? Use `tracert` e `show ip route`.
2. Digite o next-hop errado em R1.
3. Em R1, rota padrão no lugar da específica: `ip route 0.0.0.0 0.0.0.0 198.51.100.2`. Funciona? Em que se diferencia?

## Critério
Conectividade total; falha 1 diagnosticada identificando **qual direção** falha e por quê.

## Extensão opcional (não obrigatória no plano)
Substitua rotas estáticas por RIPv2 (`router rip`, `version 2`, `network …`) ou OSPF. **Verifique** o suporte na sua versão do PT e anote.

## Evidências
`show ip route`, `tracert`, antes/depois de cada falha.

## Comparação com o D04
Mesma falha ("ida chega, volta não") reproduzida em [D04, falha 1](../docker/d04-roteador/README.md#falha-1--falta-a-rota-de-volta).
