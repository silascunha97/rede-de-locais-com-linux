# Plano de estudos e matriz de integração

Seções 8 e 9 do [GUIA_DE_ESTUDOS.md](../GUIA_DE_ESTUDOS.md).

## 1. Ordem e pré-requisitos

```
M01 ─► M02 ─► M03 ─► M04
          │
          └► M05 ─► M06 ─► M09
          │
          └► M07        M08 (independente; faça junto de M07)
                         └──────────► Projeto integrador (após M01–M07, M09)
```

| ID | Título | Item RC27CP | Pré-requisitos | Esforço* | Dificuldade |
|---|---|---|---|---|---|
| [M01](../modulos/modulo-01-conceitos.md) | Conceitos, tipos de rede, atrasos | 1 | PS26CP; binário | 6–8 h | Baixa |
| [M02](../modulos/modulo-02-camadas-encapsulamento.md) | Camadas, encapsulamento, endereços | 2 | M01 | 8–10 h | Média |
| [M03](../modulos/modulo-03-aplicacao-dns-http.md) | Aplicação: DNS e HTTP | 3 | M02 | 8–10 h | Média |
| [M04](../modulos/modulo-04-transporte.md) | Transporte: TCP e UDP | 4 | M02, M03 | 8–10 h | Média-alta |
| [M05](../modulos/modulo-05-ipv4-subredes.md) | IPv4, máscaras, sub-redes | 5 | M02 | 10–12 h | Média-alta (cálculo) |
| [M06](../modulos/modulo-06-roteamento.md) | Repasse e roteamento | 5 | M05 | 10–12 h | Alta |
| [M07](../modulos/modulo-07-enlace-switching.md) | Enlace, ARP, switching | 6 | M02, M05 | 8–10 h | Média |
| [M08](../modulos/modulo-08-camada-fisica.md) | Camada física | 6 | M01 | 4–6 h | Baixa-média |
| [M09](../modulos/modulo-09-nat-firewall.md) | NAT e firewall (complementar) | — | M06, M04 | 8–10 h | Alta |
| [PI](projeto-integrador.md) | Projeto integrador | todos | M01–M07, M09 | 12–16 h | Alta |

\*Estimativas **minhas, sem dados de seu ritmo**: ajuste após o primeiro módulo. Não há calendário fixo; a velocidade é ditada pelo nível alcançado, não pela data.

**Avaliação inicial (substitui supor seu nível):** antes do M01 faça o diagnóstico em [banco-de-questoes.md](banco-de-questoes.md#diagnóstico-inicial). Se errar a conversão binária ou potências de 2, revise isso antes do M05.

## 2. Matriz de integração (três frentes)

| Módulo | Problema | Conceito central | Livro | Fonte acadêmica | Packet Tracer | Docker | Evidência | Critério |
|---|---|---|---|---|---|---|---|---|
| M01 | Um arquivo de 12 MB demora mais do que a conta ingênua indica | Atrasos, comutação de pacotes | ___ | UFPR lista 1 (tópicos LAN/WAN) | [PT-01](../laboratorios/packet-tracer/pt-01-lan-simples.md) | **Sem equivalente** (ver módulo) | Cálculo + ping com tempos | D1, D6 |
| M02 | Quais campos mudam entre origem e destino? | Encapsulamento, MAC×IP×porta | ___ | UFPR lista 1 (PDU, OSI) | [PT-02](../laboratorios/packet-tracer/pt-02-simulacao-pdu.md) | [D01](../laboratorios/docker/d01-encapsulamento/README.md) | Captura com MAC/IP/porta | D1, D7 |
| M03 | O site abre por IP mas não pelo nome | DNS, cliente-servidor | ___ | — | [PT-03](../laboratorios/packet-tracer/pt-03-dns-http.md) | [D02](../laboratorios/docker/d02-dns/README.md) | `dig` + log do servidor | D4, D5 |
| M04 | Dois serviços, mesmo host: um responde, outro "perde" dados | TCP×UDP, portas, handshake | ___ | UFPR lista 1 (TCP×UDP) | [PT-04](../laboratorios/packet-tracer/pt-04-transporte.md) (limitado) | [D03](../laboratorios/docker/d03-transporte/README.md) | pcap com `S`,`S.`,`.` | D7 |
| M05 | Hosts "ativos" que não se falam | IP, máscara, gateway | ___ | UFPR lista 1 (IP/CIDR) | [PT-05](../laboratorios/packet-tracer/pt-05-subredes-um-roteador.md) | [D04](../laboratorios/docker/d04-roteador/README.md) parte A | Tabela de endereçamento + `ip route` | D3, D5 |
| M06 | Ida chega, volta não | Repasse, rotas ida e volta | ___ | UFPR lista 1 (roteamento) | [PT-06](../laboratorios/packet-tracer/pt-06-rotas-estaticas.md) | [D04](../laboratorios/docker/d04-roteador/README.md) parte B | `traceroute` + tcpdump no roteador | D5, D7 |
| M07 | Como o switch "sabe" a porta? | ARP, tabela MAC | ___ | UFPR lista 1 (ARP, Ethernet) | [PT-07](../laboratorios/packet-tracer/pt-07-arp-switch.md) | [D05](../laboratorios/docker/d05-enlace-arp/README.md) (parcial) | `show mac address-table`; `ip neigh` + ARP | D7 |
| M08 | Qual meio para 80 m a 1 Gbps? | Meios, codificação | ___ | — | **Sem equivalente** | **Sem equivalente** | Exercícios | D1 |
| M09 | Rede interna acessa o servidor externo; o contrário não | NAT, filtragem | ___ | — | [PT-08](../laboratorios/packet-tracer/pt-08-nat-acl.md) | [D06](../laboratorios/docker/d06-nat-firewall/README.md) | `iptables -v`, log do servidor | D4, D5, D7 |

## 3. Lacunas

| Assunto | Falta |
|---|---|
| Livro | Sumário (P1) |
| Questões reais de prova | Provas ou leitura das fontes da §3 de [fontes-e-referencias.md](fontes-e-referencias.md) |
| DHCP, VLAN, IPv6, roteamento dinâmico (RIP/OSPF) | Sem módulo próprio: aparecem como **extensões opcionais** nos módulos M06/M07/M09. Se o docente cobrar, criar módulo depois. |
| Packet Tracer | Versão do programa e arquivos `.pkt` (só há roteiros) |
