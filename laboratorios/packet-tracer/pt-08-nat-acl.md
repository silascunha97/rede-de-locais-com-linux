# PT-08 — NAT com sobrecarga e ACL (Módulo M09, complementar)

> **Status:** revisado estaticamente; **não executado**. Versão do PT: ____ (os comandos de NAT/ACL do IOS existem no PT 1941; **confirme** na sua versão).

Voltar: [Módulo 09](../../modulos/modulo-09-nat-firewall.md)

**Objetivo:** uma LAN privada acessa um servidor "externo" via NAT; depois restringir um serviço com ACL.

**Topologia:** `PC1 — SW1 — R1 — SW2 — Server`. Interna: 192.0.2.0/24 (R1 g0/0 = .254). Externa: 203.0.113.0/24 (R1 g0/1 = .254; Server = .10/24, gateway 203.0.113.254, **sem rota para a rede interna**).

## Configuração (R1)
```
interface g0/0
 ip address 192.0.2.254 255.255.255.0
 ip nat inside
 no shutdown
interface g0/1
 ip address 203.0.113.254 255.255.255.0
 ip nat outside
 no shutdown
access-list 1 permit 192.0.2.0 0.0.0.255
ip nat inside source list 1 interface g0/1 overload
```
(Todos em modo de configuração; `interface` entra no submodo.)

## Testes
1. **Sem as linhas de NAT** (faça primeiro): `ping` PC1→Server. Previsão: falha por falta de rota de volta no servidor. Registre.
2. Com o NAT: `ping` e HTTP funcionam. `show ip nat translations`: qual o endereço "interno global"?
3. No Simulation, compare IP de origem antes e depois de R1.

## ACL (firewall simples)
```
ip access-list extended BLOQ_WEB
 deny tcp 192.0.2.0 0.0.0.255 any eq 80
 permit ip any any
interface g0/0
 ip access-group BLOQ_WEB in
```
Teste: HTTP falha; `ping` funciona. `show access-lists` mostra contadores. **Hipótese antes de testar.**

## Critério
Explicar a tradução, por que o servidor não precisa de rota para a rede interna e por que o ping passa com o HTTP bloqueado.

## Falhas
Inverter `ip nat inside`/`outside`; esquecer o `permit ip any any` (efeito do deny implícito).

## Evidências
`show ip nat translations`, `show access-lists`, telas do Simulation.

## Comparação com o D06
O mesmo problema com `iptables` em [D06](../docker/d06-nat-firewall/README.md). O PT usa IOS (ACL em interface); o Linux usa tabelas/cadeias (NAT em `POSTROUTING`, filtro em `FORWARD`).
