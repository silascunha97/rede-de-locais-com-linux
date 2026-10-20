# PT-05 — Dois segmentos, um roteador (Módulo M05)

> **Status:** revisado estaticamente; **não executado**. Versão do PT: ____ (assume-se roteador **1941**, interfaces `g0/0` e `g0/1`; **confirme** o modelo e os nomes das interfaces na sua versão).

Voltar: [Módulo 05](../../modulos/modulo-05-ipv4-subredes.md)

**Objetivo:** conectar duas sub-redes IPv4 com um roteador e explicar o papel do gateway.

**Topologia:** R1 (1941); SW1 e SW2 (2960); PC1, PC2 em SW1; PC3, PC4 em SW2. Ligações diretas: R1 g0/0 ↔ SW1; R1 g0/1 ↔ SW2.

| Dispositivo | Interface | IP | Máscara | Gateway |
|---|---|---|---|---|
| R1 | g0/0 | 192.0.2.254 | 255.255.255.0 | — |
| R1 | g0/1 | 198.51.100.254 | 255.255.255.0 | — |
| PC1 / PC2 | NIC | 192.0.2.1 / .2 | 255.255.255.0 | 192.0.2.254 |
| PC3 / PC4 | NIC | 198.51.100.1 / .2 | 255.255.255.0 | 198.51.100.254 |

## Configuração do roteador
```
enable
configure terminal
hostname R1
interface g0/0
 ip address 192.0.2.254 255.255.255.0
 no shutdown
interface g0/1
 ip address 198.51.100.254 255.255.255.0
 no shutdown
end
show ip interface brief
show ip route
```
## Testes
`ping` PC1→PC2 (mesma rede), PC1→PC3 (via roteador) e traceroute (`tracert 198.51.100.1` no PC). **Resultado esperado:** `show ip route` lista duas rotas `C` (conectadas) e duas `L` (locais); pings 100%; `tracert` mostra 192.0.2.254 como primeiro salto.

## Etapa 2 — refazer sem consultar
Troque para `203.0.113.0/25` e `203.0.113.128/25` (gateways `.126` e `.254`). Valide.

## Etapa 3 — falhas intencionais (uma por vez; **escreva a hipótese antes**)
a. Gateway errado no PC3. b. Máscara errada no PC3. c. `shutdown` em g0/1. Para cada: sintoma, **o comando que prova a causa** (`ipconfig`, `show ip interface brief`, `show ip route`), correção.

## Critério
100% de conectividade, explicação do porquê do gateway, falhas diagnosticadas com 1 comando-prova cada.

## Perguntas
1. Por que PC1 não precisa de rota para PC3, só de gateway?
2. Que ocorre se a máscara do PC1 for /25 e o gateway for 192.0.2.254? (veja a Q5.4)

## Evidências
Tela da topologia, saídas de `show ip route`/`show ip interface brief`, pings, tabela de endereçamento.

## Comparação com o D04
No PT o roteador é IOS e o switch é dispositivo separado; no Docker, o roteador é um container Linux e a bridge é implícita ([D04](../docker/d04-roteador/README.md)).
