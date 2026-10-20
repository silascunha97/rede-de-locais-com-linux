# Caderno de Estudos — Redes de Computadores 1 (RC27CP)

> **Status do documento (2026-10-20):** versão 0.1, construída por revisão estática.
> **Nenhum laboratório foi executado.** Toda saída marcada como "esperada" é prevista a partir do funcionamento conhecido dos protocolos e **não foi observada**. Ao executar, registre o resultado real no diário (seção 12).
> Todos os módulos estão como **Não iniciado** até haver evidência (seção 10).

**Objetivo geral:** compreender por que uma rede funciona, como observar seu comportamento e como diagnosticar falhas, combinando três frentes: **A** teoria e problemas, **B** Cisco Packet Tracer (PT), **C** Docker.

---

## 1. Como usar este caderno

Ciclo por módulo (siga na ordem; não olhe o gabarito antes de tentar):

1. Ler a seção do livro e resumir **com suas palavras** (seção 12, diário).
2. Resolver as questões **sem consulta** (seção 8). Só depois consultar dicas e o gabarito (seção 9).
3. Fazer o laboratório PT (Etapa 1 guiada → 2 reconstrução → 3 falha).
4. Fazer o laboratório Docker, quando existir.
5. Comparar PT × Docker e registrar diferenças.
6. Aplicar a avaliação de domínio do módulo (seção 10).

Convenções: endereços de laboratório usam blocos reservados para documentação (RFC 5737): `192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24`. Nomes DNS usam o domínio reservado `.test`.

---

## 2. Inventário das fontes

### 2.1 Arquivos do projeto

| Arquivo | Papel | Autoridade | Observação |
|---|---|---|---|
| `RC27CP.md` / `RC27CP.pdf` | Plano de ensino UTFPR Pato Branco, Redes de Computadores 1 | **Critério obrigatório** | A conversão `.md` tem trechos embaralhados na linha de "Camada Física"; conferir no PDF. |
| `ex-rede-computadores.md` | Este caderno | Produto | Estava vazio; é o arquivo de saída. |

### 2.2 Dados da disciplina (confirmados em RC27CP)

- Código RC27CP, 6º período, Engenharia de Computação, matriz 535. Pré-requisito: PS26CP (Princípios de Sistemas de Comunicação).
- 72 aulas: AT 34, AP 34, APS 04.
- Aprovação: frequência ≥ 75% e nota final ≥ 6,0.
- Aulas práticas incluem resolução tutorada de exercícios e laboratório com equipamentos.

### 2.3 Fontes acadêmicas externas (consulta em 2026-10-20)

Status honesto: **localizadas por busca; conteúdo das questões NÃO confirmado** (os PDFs não puderam ser lidos integralmente). Por isso nenhuma questão deste caderno é "original de prova": todas são **autorais**, escritas para as competências do plano.

| Instituição | Documento | URL | Tipo | Status |
|---|---|---|---|---|
| UFRGS (Inst. de Informática) | Lista de Exercícios 2 (camadas de rede, transporte e aplicação) | http://www.inf.ufrgs.br/~asc/redes/pdf/lista2.pdf | Lista de exercícios | Baixado; texto não extraível (PDF com imagem). Tópicos citados pela busca: sub-redes, roteamento, TCP. **A verificar.** |
| UFU (FACOM) | Lista 1: História da Internet e Modelo OSI (2sem2014) | https://www.facom.ufu.br/~albertini/2sem2014/redes/lista01.pdf | Lista | Não acessado (erro de certificado). **A verificar.** |
| UFSC (repositório) | Planos DEC7126 / DEC7557 / DEC7128 | https://repositorio.ufsc.br/bitstream/handle/123456789/231301/DEC7126%20-%20Redes%20de%20computadores.pdf | Plano de ensino | Não aberto. **A verificar.** |
| UFMG (DCC) | Slides cap. 5 Kurose & Ross (enlace) | https://homepages.dcc.ufmg.br/~jmarcos/cursos/redes/Telecom2008/cap05a-Camada-de-Enlace.pdf | Slides | Não aberto. |
| UFPR | Lista 1 FundReSD | https://www.inf.ufpr.br/elias/fundresd/lista1fundresd.html | Lista | Não aberto. |

**Pendência:** abrir cada documento no navegador, anotar as questões relevantes e preencher a tabela da seção 14 antes de adaptá-las.

---

## 3. Bibliografia

**Livro físico principal (informado por você):** VIGLIAZZI, Douglas. *Redes Locais com Linux*. Florianópolis/SC: Visual Books (consta como 2004 no plano RC27CP; **edição do seu exemplar: ____**). Listado como referência **complementar** no plano.

**Referências do plano RC27CP:**
- Básicas: COMER (*Redes de Computadores e Internet*, 4. ed., Bookman, 2007); KUROSE & ROSS (*Redes de computadores e a internet: uma abordagem top-down*, 5. ed., Pearson, 2010); TANENBAUM (*Redes de computadores*, 4. ed., Campus, 2003).
- Complementares: Soares/Lemos/Colcher (1995); Matthews (2006); Torres (2001); Arnett et al. (1997); Tarouco (1986); Vigliazzi (2004).

**Limitação importante:** o sumário do livro do Vigliazzi **não foi encontrado** online (buscas retornaram só a ficha do autor, que o descreve como livro para implantar redes locais com serviços essenciais e segurança). Portanto **não há mapeamento capítulo→módulo**; a coluna "Livro" abaixo está vazia de propósito. Envie foto ou transcrição do sumário e eu preencho.

Observação pedagógica (inferência minha): o Vigliazzi é prático/administrativo (Linux, serviços); a teoria conceitual do plano (camadas, TCP, roteamento) é melhor coberta por Kurose & Ross, Tanenbaum ou Comer. Use o Vigliazzi principalmente nos módulos de serviços e laboratório.

---

## 4. Pré-requisitos

- Binário/decimal/hexadecimal, potências de 2. Noção de sinais e largura de banda (PS26CP).
- Linha de comando (Linux básico).
- Ferramentas: Cisco Packet Tracer (versão: ____); Docker (ver 5.3).

---

## 5. Ambiente e limitações

### 5.1 Packet Tracer
Simulador. Não reproduz fielmente todo o comportamento de equipamentos reais, de temporizadores e de recursos avançados. Roteadores usados: **1941** (interfaces `g0/0`, `g0/1`); switches **2960**. Registre sua versão.

### 5.2 Docker no Windows 10
Docker Desktop (backend WSL2) executa containers dentro de uma VM Linux: a rede que você vê não é a do Windows. Containers compartilham o kernel da VM; uma bridge Docker **não** é um switch gerenciável. Docker manipula iptables/NAT por conta própria. Camada física, codificação e comutação em hardware **não são reproduzíveis**.

### 5.3 Verificação do ambiente
```
docker version
docker compose version
docker run --rm nicolaka/netshoot ip -br addr
```
Imagem usada nos clientes: `nicolaka/netshoot` (traz `ip`, `ping`, `traceroute`, `tcpdump`, `dig`, `curl`, `nc`, `ss`).

### 5.4 Segurança
Nenhum laboratório usa `privileged: true` nem o socket do Docker. O roteador usa só `cap_add: NET_ADMIN` e `sysctls`. Nenhuma porta é publicada no host (tudo interno).

---

## 6. Mapa curricular

Núcleo = itens do plano RC27CP. Trilha complementar (T) = não exigida pelo plano, incluída por seu prompt; estude após o núcleo.

| Mód. | Item RC27CP | Tema | Livro (Vigliazzi) | PT | Docker |
|---|---|---|---|---|---|
| 1 | 1 | Conceitos, tipos de rede, modos de transmissão | ___ | Sim | Parcial |
| 2 | 2 | Camadas, encapsulamento, OSI×TCP/IP, endereços | ___ | Sim | Sim |
| 3 | 3 | Aplicação: HTTP, DNS, SMTP, FTP, SSH | ___ | Sim | Sim |
| 4 | 4 | Transporte: UDP, TCP, portas | ___ | Limitado | Sim |
| 5 | 5 | Rede: IP, sub-redes, repasse, roteamento | ___ | Sim | Sim |
| 6 | 6 | Enlace: erros, MAC/ARP, switches | ___ | Sim | Parcial |
| 7 | 6 | Física: meios, codificação | ___ | Não | Não |
| T1 | — | NAT, DHCP, firewall | ___ | Sim | Sim |
| T2 | — | IPv6, VLANs | ___ | Sim | Parcial |
| 8 | todos | Projeto integrador | ___ | Sim | Sim |

Tempo: dedique mais a **5 (sub-redes e roteamento)** e **4 (TCP)**, que exigem cálculo e diagnóstico.

### Tabela comparativa teoria × PT × Docker

| Conceito | Teoria | Packet Tracer | Docker | Diferença a observar |
|---|---|---|---|---|
| Endereçamento IP | Máscara, CIDR | Config. de hosts | `ip -br addr` | Docker atribui via IPAM; PT é manual |
| Roteamento | Tabela, prefixo mais longo | Roteador IOS, `show ip route` | `ip route`, container-roteador | PT = IOS; Docker = kernel Linux |
| ARP | Resolução IP→MAC | Modo simulação | `ip neigh` | Docker mostra MACs virtuais |
| DNS | Resolução hierárquica | Servidor DNS do PT | dnsmasq + `dig` | Docker usa implementação real |
| TCP | Handshake, janelas | Muito limitado | `tcpdump`, `ss` | PT não modela TCP em detalhe |

---

## 7. Módulos

Estados possíveis: Não iniciado · Em estudo · Em consolidação · Dominado.

### Módulo 1 — Conceitos básicos de redes (item 1)
**Estado:** Não iniciado
**Objetivos:** diferenciar Internet/internet/intranet/extranet; classificar redes (ponto a ponto vs. difusão; PAN/LAN/MAN/WAN); distinguir simplex/half/full-duplex; calcular atrasos básicos.
**Conceitos (explique por quê):**
- *Comutação de pacotes vs. circuitos:* pacotes compartilham enlaces (multiplexação estatística) e toleram rajadas, ao custo de filas e perdas.
- *Atrasos:* processamento + fila + transmissão (L/R) + propagação (d/v). Transmissão depende do tamanho e da taxa; propagação, da distância e do meio.
**Checklist:** ver seção 10.

**Lab PT-1 (introdutório) — LAN simples:** 1 switch 2960, 3 PCs, rede `192.0.2.0/24`.
- PC1 `192.0.2.1`, PC2 `192.0.2.2`, PC3 `192.0.2.3`, máscara `255.255.255.0`.
- Testes: `ping` entre todos. Critério: 0% de perda.
- Falha (Etapa 3): configure PC3 com máscara `255.255.255.128` e `192.0.2.130`. Explique por que fica isolado ou se comporta de modo assimétrico.

### Módulo 2 — Camadas e encapsulamento (item 2)
**Estado:** Não iniciado
**Objetivos:** descrever a pilha TCP/IP e OSI; nomear PDUs (mensagem, segmento, datagrama, quadro); distinguir endereço físico (MAC), lógico (IP) e de porta.
**Conceito:** cada camada acrescenta cabeçalho; serviços são prestados à camada acima e consumidos da abaixo. O MAC muda a cada salto; o IP origem/destino se mantém (ausente NAT).

**Lab PT-2:** repita PT-1, use **modo Simulação**, filtre ICMP/ARP e inspecione as PDUs camada a camada. Registre: quais campos mudaram entre origem e destino.
**Lab Docker D1 — observar encapsulamento** (salve como `labs/d1/compose.yaml`; cada laboratório Docker fica em `labs/dN/`):
```yaml
# labs/d1/compose.yaml
services:
  web:
    image: nginx:alpine
    networks: [lan]
  cli:
    image: nicolaka/netshoot
    command: sleep infinity
    networks: [lan]
networks:
  lan:
    ipam:
      config:
        - subnet: 192.0.2.0/24
```
Comandos:
```
docker compose up -d
docker compose exec cli ip -br addr
docker compose exec -d cli sh -c "tcpdump -i eth0 -nn -e -w /tmp/c.pcap port 80"
docker compose exec cli curl -s http://web/ -o /dev/null
docker compose exec cli tcpdump -nn -e -r /tmp/c.pcap
docker compose down -v
```
Esperado (não testado): captura mostra MAC origem/destino, IP, porta 80 e flags TCP. Hipótese: o nome `web` resolve via DNS embutido do Docker (redes definidas pelo usuário). Questão: o DNS embutido é equivalente a um servidor DNS da rede real? (Não: é do Docker.)

### Módulo 3 — Camada de aplicação (item 3)
**Estado:** Não iniciado
**Objetivos:** explicar HTTP, DNS, SMTP, FTP, SSH (modelo cliente-servidor, portas, TCP/UDP); resolver nomes e interpretar respostas.
**Pontos:** DNS usa normalmente UDP/53 (TCP/53 para respostas grandes e transferência de zona); HTTP/1.x sobre TCP/80; SMTP/25; FTP/21 (+ dados); SSH/22.

**Lab PT-3:** servidor DNS + servidor HTTP no PT. Servidor Web `192.0.2.10`, DNS `192.0.2.53` com registro `web.lab.test → 192.0.2.10`; PC configurado com DNS `192.0.2.53`. Teste no navegador do PC: `http://web.lab.test`. Critério: página abre. Falha: apague o registro DNS.

**Lab Docker D2 — DNS real com dnsmasq:**
```
labs/d2/
  compose.yaml
  dns/Dockerfile
  dns/dnsmasq.conf
```
`dns/Dockerfile`:
```dockerfile
FROM alpine:3.20
RUN apk add --no-cache dnsmasq
COPY dnsmasq.conf /etc/dnsmasq.conf
CMD ["dnsmasq", "-k", "--log-queries", "--log-facility=-"]
```
`dns/dnsmasq.conf`:
```
no-resolv
address=/web.lab.test/192.0.2.10
```
`compose.yaml`:
```yaml
services:
  dns:
    build: ./dns
    networks:
      lan: { ipv4_address: 192.0.2.53 }
  web:
    image: nginx:alpine
    networks:
      lan: { ipv4_address: 192.0.2.10 }
  cli:
    image: nicolaka/netshoot
    command: sleep infinity
    dns: [192.0.2.53]
    networks:
      lan: { ipv4_address: 192.0.2.100 }
networks:
  lan:
    ipam:
      config:
        - subnet: 192.0.2.0/24
```
Execução e diagnóstico:
```
docker compose up -d --build
docker compose exec cli dig web.lab.test
docker compose exec cli curl -s http://web.lab.test | head -n 3
docker compose logs dns
docker compose down -v
```
Esperado (não testado): `dig` retorna `192.0.2.10`; log do dnsmasq mostra a consulta. Falha: remova a linha `address=`, reconstrua (`up -d --build`) e observe `NXDOMAIN`/`REFUSED`. Atenção: com `no-resolv`, nomes externos não resolvem — intencional (isolamento). Observação: dentro de redes definidas pelo usuário o Docker injeta seu DNS embutido; a opção `dns:` tenta substituí-lo, e o comportamento pode variar com a versão; confira com `docker compose exec cli cat /etc/resolv.conf`.

### Módulo 4 — Camada de transporte (item 4)
**Estado:** Não iniciado
**Objetivos:** multiplexação/demultiplexação por portas; UDP vs. TCP; handshake de 3 vias; números de sequência e ACK; ideia de controle de fluxo e de congestionamento.
**Conceitos:** UDP não garante entrega; TCP oferece fluxo confiável e ordenado via confirmações e retransmissão. Controle de fluxo protege o receptor; controle de congestionamento protege a rede.

**Lab PT-4 (limitado):** o PT não detalha TCP. Use o modo simulação para ver SYN/ACK em conexões HTTP quando disponível e registre o que viu e o que não viu.
**Lab Docker D3:**
```yaml
# labs/d3/compose.yaml
services:
  srv:
    image: nicolaka/netshoot
    command: sh -c "nc -lk -p 5000 & nc -lu -p 5001 & sleep infinity"
    networks: [lan]
  cli:
    image: nicolaka/netshoot
    command: sleep infinity
    networks: [lan]
networks:
  lan:
    ipam:
      config:
        - subnet: 192.0.2.0/24
```
(O `nc` da netshoot é o do Alpine/busybox ou nmap; se as flags divergirem, rode `nc -h` e ajuste.)
```
docker compose up -d
docker compose exec srv ss -tuln
docker compose exec -d cli tcpdump -i eth0 -nn -w /tmp/t.pcap port 5000
docker compose exec cli sh -c "echo oi | nc srv 5000"
docker compose exec cli tcpdump -nn -r /tmp/t.pcap
docker compose down -v
```
Esperado (não testado): três primeiros pacotes `S`, `S.`, `.` (handshake), depois dados e `F`. Compare com UDP em 5001: sem handshake.

### Módulo 5 — Camada de rede (item 5) — **módulo central**
**Estado:** Não iniciado
**Objetivos:** diferenciar repasse (tabela, por pacote) de roteamento (cálculo da tabela); sub-redes e CIDR; prefixo mais longo; rotas estáticas; noções de vetor de distância e estado de enlace.
**Conceitos:**
- Um roteador decide pelo **prefixo mais longo** que combina com o destino; a rota padrão é `0.0.0.0/0`.
- Para n bits de host: 2ⁿ − 2 hosts utilizáveis (exceto /31, /32).
- Para a comunicação funcionar são necessárias rotas **de ida e de volta**.

**Lab PT-5 — dois segmentos, um roteador:**
Dispositivos: 1 roteador 1941, 2 switches 2960, 4 PCs.

| Dispositivo | Interface | IP | Máscara | Gateway |
|---|---|---|---|---|
| R1 | g0/0 | 192.0.2.254 | 255.255.255.0 | — |
| R1 | g0/1 | 198.51.100.254 | 255.255.255.0 | — |
| PC1/PC2 | NIC | 192.0.2.1 / .2 | 255.255.255.0 | 192.0.2.254 |
| PC3/PC4 | NIC | 198.51.100.1 / .2 | 255.255.255.0 | 198.51.100.254 |

Ligações: PC1, PC2 ↔ SW1 ↔ R1 g0/0; PC3, PC4 ↔ SW2 ↔ R1 g0/1 (cabo direto).
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
Esperado: duas rotas `C` (conectadas) e duas `L` (locais); `ping` PC1→PC3 responde. Critério de conclusão: 100% de sucesso nos pings entre os segmentos.
**Etapa 2:** refaça sem olhar, trocando para `203.0.113.0/25` e `203.0.113.128/25`.
**Etapa 3 (falha):** o instrutor (ou você) altera o gateway do PC3. Descreva o sintoma e qual comando comprova a causa.

**Lab PT-6 — dois roteadores, rotas estáticas:** R1 `g0/1 = 198.51.100.1/30`, R2 `g0/0 = 198.51.100.2/30`, LAN1 `192.0.2.0/24` em R1, LAN2 `203.0.113.0/24` em R2.
```
! R1
ip route 203.0.113.0 255.255.255.0 198.51.100.2
! R2
ip route 192.0.2.0 255.255.255.0 198.51.100.1
```
Falha: apague uma das rotas e investigue com `show ip route` e `traceroute`. Variante: substitua por `router rip` / `router ospf 1` e compare (limitações de OSPF/RIP no PT: verifique a versão).

**Lab Docker D4 — container como roteador:**
```yaml
# labs/d4/compose.yaml
services:
  router:
    image: nicolaka/netshoot
    command: sleep infinity
    cap_add: [NET_ADMIN]
    sysctls:
      net.ipv4.ip_forward: "1"
    networks:
      net_a: { ipv4_address: 192.0.2.254 }
      net_b: { ipv4_address: 198.51.100.254 }
  host_a:
    image: nicolaka/netshoot
    cap_add: [NET_ADMIN]
    command: sh -c "ip route add 198.51.100.0/24 via 192.0.2.254 && sleep infinity"
    networks:
      net_a: { ipv4_address: 192.0.2.10 }
  host_b:
    image: nicolaka/netshoot
    cap_add: [NET_ADMIN]
    command: sh -c "ip route add 192.0.2.0/24 via 198.51.100.254 && sleep infinity"
    networks:
      net_b: { ipv4_address: 198.51.100.10 }
networks:
  net_a:
    internal: true
    ipam: { config: [ { subnet: 192.0.2.0/24 } ] }
  net_b:
    internal: true
    ipam: { config: [ { subnet: 198.51.100.0/24 } ] }
```
Execução:
```
docker compose up -d
docker compose exec host_a ip route
docker compose exec host_a ping -c 3 198.51.100.10
docker compose exec host_a traceroute -n 198.51.100.10
docker compose exec router ip -br addr
docker compose down -v
```
Esperado (não testado): `ping` responde; `traceroute` mostra `192.0.2.254` como primeiro salto. `internal: true` impede acesso externo (sem NAT).
**Falha 1:** `docker compose exec host_b ip route del 192.0.2.0/24` → ida chega, volta não. Diagnóstico: `docker compose exec router tcpdump -i any -nn icmp` mostra echo-request em ambas as interfaces e nenhum reply de volta ao A. Correção: recriar a rota.
**Falha 2:** `docker compose exec router sysctl -w net.ipv4.ip_forward=0`. Sintoma: ping sem resposta; o tcpdump vê pacotes entrando e não saindo. Compare com PT.
Diferença-chave: no PT o roteador é IOS; aqui é o kernel Linux (`ip route`, tabela de encaminhamento).

### Módulo 6 — Camada de enlace e comutação (item 6)
**Estado:** Não iniciado
**Objetivos:** detecção de erros (paridade, checksum, CRC); acesso ao meio (conceito de CSMA/CD); MAC, ARP; diferença hub/bridge/switch.
**Conceitos:** o switch aprende MACs de origem e encaminha por MAC de destino; quadro desconhecido é inundado (flooding). ARP resolve IP→MAC **dentro** do segmento; para outro segmento o host faz ARP do **gateway**.

**Lab PT-7:** 1 switch, 3 PCs. Antes dos pings: `show mac address-table` (vazia ou quase). Faça `ping`; repita o comando e anote o que foi aprendido. No PC: `arp -a`.
**Lab Docker D5 (observacional):** use D1; rode `docker compose exec cli ip neigh` antes e depois de um `curl`. Registre. Limite: a bridge Linux do Docker não é um switch gerenciável (sem `show mac address-table` como no IOS; é possível usar `bridge fdb` no host Linux, que no Windows fica dentro da VM do WSL).

### Módulo 7 — Camada física (item 6)
**Estado:** Não iniciado
**Objetivos:** comparar par trançado, fibra, sem-fio; entender codificação (NRZ, Manchester) e modos de transmissão. Sem PT/Docker: faça só exercícios (seção 8) e consulte o livro.

### Trilha complementar (fora do RC27CP)
- **T1 NAT/DHCP/firewall:** PT (NAT overload e DHCP no roteador) e Docker (`iptables`/`nftables` em container roteador com `cap_add: NET_ADMIN`). Estudar após o módulo 5.
- **T2 IPv6 e VLANs:** PT para VLAN (`vlan 10`, `switchport access vlan 10`, trunk). VLAN real não é reproduzível na bridge padrão do Docker; use apenas PT.

### Módulo 8 — Projeto integrador
**Estado:** Não iniciado
**Escopo:** rede de uma pequena empresa com 2 sub-redes (usuários `192.0.2.0/25`, servidores `192.0.2.128/25`) e uma rede de acesso `198.51.100.0/30`, um roteador, servidor DNS+HTTP.
**Entregas:** (1) diagrama e plano de endereçamento; (2) implementação PT; (3) equivalente Docker (roteador, DNS, web); (4) testes de conectividade; (5) duas falhas documentadas com diagnóstico; (6) comparação PT × Docker; (7) decisões técnicas e reflexão.
**Critérios:** endereçamento correto (30%); conectividade (25%); diagnóstico com evidências (25%); documentação (20%).

---

## 8. Questões (resolver sem consulta)

Todas **autorais**. Dicas e gabarito na seção 9.

**M1**
- **Q1.1** Um pacote de 1500 bytes é transmitido por um enlace de 10 Mbps. Qual o atraso de transmissão? 
- **Q1.2** Um enlace de 2000 km tem velocidade de propagação 2×10⁸ m/s. Qual o atraso de propagação?
- **Q1.3** Uma mensagem de 8000 bits passa por dois enlaces de 1 Mbps com um roteador *store-and-forward*. Ignorando propagação e fila, qual o atraso total?
- **Q1.4** Classifique: teclado→PC por cabo (simplex/half/full)? Walkie-talkie? Telefone?

**M2**
- **Q2.1** Ordene os cabeçalhos de fora para dentro em um quadro Ethernet carregando HTTP.
- **Q2.2** Dois hosts em redes diferentes se comunicam via um roteador. Quais endereços (MAC/IP) mudam ao longo do caminho?

**M3**
- **Q3.1** Qual protocolo de transporte e porta padrão o DNS usa? Em que caso muda?
- **Q3.2** Diferencie resolução recursiva e iterativa.

**M4**
- **Q4.1** Descreva o handshake de 3 vias.
- **Q4.2** Um remetente envia 3 segmentos de 500 bytes cada; o primeiro byte tem número de sequência 1000. Quais os números de sequência e o ACK final esperado?
- **Q4.3** Por que usar UDP para consultas DNS em vez de TCP?

**M5**
- **Q5.1** Divida `192.0.2.0/24` em 4 sub-redes iguais. Liste rede e broadcast de cada.
- **Q5.2** Para o host `198.51.100.77/27`: endereço de rede, broadcast e faixa de hosts.
- **Q5.3** Tabela: `192.0.2.0/24→A`, `192.0.2.128/25→B`, `0.0.0.0/0→C`. Para onde vão os destinos `192.0.2.50`, `192.0.2.200`, `203.0.113.9`?
- **Q5.4** Vetor de distância: o nó x tem vizinhos y (custo 2) e z (custo 5). y anuncia custo 3 até D; z anuncia 1. Qual o melhor custo e o próximo salto de x até D?
- **Q5.5** Qual é a diferença entre repasse e roteamento?

**M6**
- **Q6.1** Dado o dado `1011001` (7 bits), calcule o bit de paridade par.
- **Q6.2** Um switch recebe um quadro com MAC destino desconhecido. O que faz?
- **Q6.3** Por que o ARP não atravessa roteadores?

**M7**
- **Q7.1** Cite uma vantagem e uma desvantagem da fibra óptica frente ao par trançado.

---

## 9. Dicas e gabarito comentado

*(Consulte só após tentar. Evite olhar antes.)*

**Q1.1** Dica: L/R. 1500 B = 12 000 bits; 12 000 / 10⁷ = **1,2 ms**.
**Q1.2** d/v = 2×10⁶ m / 2×10⁸ m/s = **10 ms**.
**Q1.3** Cada enlace: 8000/10⁶ = 8 ms; dois enlaces em série (store-and-forward) = **16 ms**.
**Q1.4** Simplex; half-duplex; full-duplex.
**Q2.1** Ethernet → IP → TCP → HTTP (dados) (e FCS no final do quadro).
**Q2.2** MACs mudam a cada salto; IPs origem/destino permanecem (sem NAT).
**Q3.1** UDP/53 normalmente; TCP/53 para respostas grandes e transferências de zona.
**Q3.2** Recursiva: o servidor resolve por conta do cliente e devolve a resposta final. Iterativa: o servidor devolve uma indicação (referral) e o cliente consulta o próximo.
**Q4.1** SYN → SYN+ACK → ACK.
**Q4.2** Sequências 1000, 1500, 2000; ACK final **2500** (próximo byte esperado).
**Q4.3** Menos custo de conexão para troca curta (uma pergunta/uma resposta); retransmissão pode ser feita pela aplicação.
**Q5.1** /26: `192.0.2.0` (bc `.63`), `.64` (bc `.127`), `.128` (bc `.191`), `.192` (bc `.255`); 62 hosts cada.
**Q5.2** /27 → bloco de 32. 77 está em 64–95: rede `198.51.100.64`, broadcast `.95`, hosts `.65`–`.94`.
**Q5.3** `192.0.2.50→A` (/24); `192.0.2.200→B` (/25 mais específico); `203.0.113.9→C` (padrão).
**Q5.4** via y: 2+3=5; via z: 5+1=6. Melhor: **5, próximo salto y**.
**Q5.5** Repasse: mover o pacote de uma entrada para a saída consultando a tabela. Roteamento: algoritmos que constroem a tabela.
**Q6.1** Bits com valor 1: 4 (par) → paridade par = **0**.
**Q6.2** Inunda (flooding) por todas as portas exceto a de entrada.
**Q6.3** ARP usa difusão no enlace local; roteadores não encaminham difusão de camada 2.
**Q7.1** Vantagem: grande largura de banda/baixa atenuação/imune a EMI. Desvantagem: custo e instalação/emendas mais delicadas.

---

## 10. Progresso e avaliação de domínio

Escala: **Não iniciado · Em estudo · Em consolidação · Dominado**. Só marque "Dominado" com evidência (laboratório e diário preenchidos + avaliação aprovada).

| Módulo | Estado | Evidência (link p/ diário) |
|---|---|---|
| 1 | Não iniciado | |
| 2 | Não iniciado | |
| 3 | Não iniciado | |
| 4 | Não iniciado | |
| 5 | Não iniciado | |
| 6 | Não iniciado | |
| 7 | Não iniciado | |
| T1 | Não iniciado | |
| T2 | Não iniciado | |
| 8 | Não iniciado | |

**Checklist por módulo (copie para cada um):**
- [ ] Li a seção do livro
- [ ] Resumo com minhas palavras
- [ ] Resolvi os exercícios sem consulta
- [ ] Concluí o laboratório PT
- [ ] Executei o laboratório Docker (se houver)
- [ ] Investiguei uma falha intencional
- [ ] Registrei resultados e evidências
- [ ] Expliquei o conceito sem notas
- [ ] Passei na avaliação de domínio

**Avaliação de domínio (modelo):** 3 questões conceituais + 1 cálculo + 1 prática com topologia diferente da estudada + 1 falha para diagnosticar. Aprovado com ≥ 70% **e** diagnóstico correto feito sem consultar o tutorial.

**Desafios de transferência (exemplos):** M5 — refazer PT-5 com 3 segmentos e VLSM; M4 — repetir D3 com porta e protocolo trocados e prever a captura antes de rodar.

---

## 11. Registro de dificuldades

| Data | Módulo | Dificuldade | Hipótese | Resolvido? |
|---|---|---|---|---|
| | | | | |

---

## 12. Modelo de diário de laboratório (copie para cada experimento)

```
Data:
Módulo:
Objetivo:
Hipótese (o que espero ver e por quê):
Ambiente e versões (PT / Docker / SO):
Topologia (diagrama ou descrição):
Configurações:
Comandos executados:
Resultados observados:
Evidências (prints, trechos de saída, pcap):
Erros encontrados:
Diagnóstico:
Correção aplicada:
Conclusão (a hipótese se confirmou?):
Dúvidas pendentes:
```

---

## 13. Revisões periódicas

Revisar cada módulo concluído após 1 dia, 1 semana e 1 mês: refaça um problema de cálculo e reexplique o conceito sem notas. Registre a data na seção 10.

---

## 14. Fontes acadêmicas — rastreio de questões (a preencher)

| Fonte | Questão (resumo) | Tipo (original / adaptada) | Módulo | Adaptada para |
|---|---|---|---|---|
| | | | | |

Questões das seções 8–9 são **autorais**.

---

## 15. Glossário

**ARP** protocolo que resolve IP→MAC no enlace local · **CIDR** notação IP/prefixo · **Datagrama** PDU da camada de rede · **Encapsulamento** adição de cabeçalhos por camada · **Gateway** roteador de saída da sub-rede · **MAC** endereço físico da interface · **PDU** unidade de dados do protocolo · **Prefixo mais longo** regra de escolha de rota · **Quadro** PDU do enlace · **Segmento** PDU do TCP · **Store-and-forward** roteador recebe o pacote inteiro antes de encaminhar · **TTL** limite de saltos do datagrama.

---

## 16. Pendências para a versão 0.2

1. Sumário e edição do livro do Vigliazzi → preencher coluna "Livro" e a seção 3.
2. Abrir as fontes da seção 2.3 e adaptar questões (seção 14).
3. Conferir o plano no PDF (trecho de "Camada Física").
4. Executar os laboratórios, registrar saídas reais e só então marcar como testados.
5. Versões do PT e do Docker.
