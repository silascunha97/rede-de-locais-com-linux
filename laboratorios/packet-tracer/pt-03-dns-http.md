# PT-03 — DNS e HTTP (Módulo M03)

> **Status:** revisado estaticamente; **não executado**. Versão do PT: ____

Voltar: [Módulo 03](../../modulos/modulo-03-aplicacao-dns-http.md)

**Objetivo:** servidor DNS e servidor Web em uma LAN; acessar o site **por nome**.

**Topologia:** SW1 (2960) com: Web (Server-PT) 192.0.2.10, DNS (Server-PT) 192.0.2.53, PC1 192.0.2.100. Máscara 255.255.255.0. Sem gateway (rede única).

## Procedimento
1. Configure os IPs estáticos (aba *Config → FastEthernet0*).
2. Web: *Config → Services → HTTP* ligado.
3. DNS: *Services → DNS* ligado; adicione o registro **A** `web.lab.test` → `192.0.2.10`.
4. PC1: em *IP Configuration* defina **DNS Server = 192.0.2.53**.
5. PC1 → *Web Browser*: `http://192.0.2.10` (deve abrir) e depois `http://web.lab.test`.
6. Command Prompt do PC1: `nslookup web.lab.test`.

## Critério
Ambas as URLs abrem e você explicou, com o Simulation Mode (filtro DNS, HTTP), a **ordem** das PDUs (DNS antes de HTTP).

## Falha intencional
Apague o registro DNS (ou desative o serviço DNS). Teste a URL por IP e por nome; use `nslookup` e o Simulation Mode para localizar a falha, **sem** olhar o servidor primeiro. Escreva as hipóteses.

## Perguntas
1. Por que o acesso por IP continua funcionando?
2. O que o PC faz com a resposta DNS antes de abrir o HTTP?

## Evidências
Telas do navegador, `nslookup`, PDUs de DNS e HTTP no Simulation Mode.

## Limites
O DNS do PT é simplificado (sem hierarquia/recursão real); nomes externos não existem. Compare com [D02](../docker/d02-dns/README.md), que usa um servidor real.
