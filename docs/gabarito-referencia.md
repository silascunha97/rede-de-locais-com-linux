# ⚠️ Referência de correção — NÃO ABRA ANTES DE TENTAR

Este arquivo contém respostas e raciocínio esperado de [banco-de-questoes.md](banco-de-questoes.md) e algumas soluções-guia dos módulos. Abrir antes da investigação elimina o valor do PBL. Registre sua resposta **primeiro**.

*Cálculos revisados à mão por mim; não foram conferidos por terceiros. Se discordar, registre no diário: pode ser um erro meu.*

## Diagnóstico
- **D.1** 203 = 11001011; 10110101 = 181.
- **D.2** 2⁷ = 128 valores; 2⁹ − 1 = 511.

## M01
- **Q1.1** 12 000 bits / 10⁷ bps = **1,2 ms**.
- **Q1.2** 2×10⁶ m / 2×10⁸ m/s = **10 ms**.
- **Q1.3** Uma só mensagem: 8 ms por enlace × 2 = **16 ms** (store-and-forward: recebe tudo antes de reenviar). Com 4 pacotes de 2000 bits (2 ms cada): 1º pacote chega em 2 + 2 = 4 ms; os seguintes saem 2 ms depois cada, totalizando **10 ms** (pipeline).
- **Q1.4** Simplex; half-duplex; full-duplex.
- **Q1.5** Internet = rede mundial; internet = interconexão de redes quaisquer; intranet = rede privada de uma organização que usa tecnologias da Internet; extranet = intranet aberta a parceiros externos.

## M02
- **Q2.1** Ethernet → IP → TCP → HTTP (FCS Ethernet no fim do quadro).
- **Q2.2** MAC origem/destino mudam a cada salto; IP origem/destino permanecem (sem NAT); portas permanecem. Com NAT, IP/porta de origem podem ser reescritos.
- **Q2.3** Mensagem (aplicação), segmento (transporte; datagrama no UDP), datagrama/pacote (rede), quadro (enlace).
- **Q2.4** TLS não se encaixa de forma única: roda sobre o transporte e sob a aplicação; no OSI costuma ser associado a apresentação/sessão, mas o TCP/IP não tem essas camadas.

## M03
- **Q3.1** UDP/53 normalmente; TCP/53 para respostas grandes (truncadas) e transferência de zona.
- **Q3.2** Recursiva: o servidor resolve em nome do cliente e devolve a resposta final. Iterativa: devolve um referral e o cliente consulta o próximo.
- **Q3.3** Hipóteses: (a) cliente sem/ com DNS errado → `cat /etc/resolv.conf`; (b) registro inexistente no servidor → `dig @servidor nome`; (c) servidor DNS inacessível/serviço parado → `dig @IP`, `ss -uln` no servidor. Cache/ndots também são possibilidades.

## M04
- **Q4.1** Cliente→servidor SYN; servidor→cliente SYN+ACK; cliente→servidor ACK.
- **Q4.2** Sequências 1000, 1500, 2000; ACK final 2500 (próximo byte esperado).
- **Q4.3** Evita custo do handshake para troca de 1 pergunta/1 resposta; a aplicação trata timeout/retransmissão.
- **Q4.4** Pela quádrupla (IP origem, porta origem, IP destino, porta destino); a porta de origem efêmera difere.

## M05
- **Q5.1** /26: `.0` (bc `.63`), `.64` (bc `.127`), `.128` (bc `.191`), `.192` (bc `.255`); 62 hosts cada (`.1–.62`, etc.).
- **Q5.2** Bloco 32; 77 está em 64–95. Rede `198.51.100.64`, broadcast `.95`, hosts `.65–.94`.
- **Q5.3** A: /25 (126 hosts) `203.0.113.0/25`; B: /26 `203.0.113.128/26` (62); C: /27 `203.0.113.192/27` (30); enlaces /30: `203.0.113.224/30` e `203.0.113.228/30`. Sobra de `.232` em diante. (Outras alocações válidas existem, desde que não se sobreponham.)
- **Q5.4** O host está em `192.0.2.128/25` (hosts `.129–.254`); o gateway `192.0.2.1` está em `192.0.2.0/25`: fora da sub-rede do host, logo inalcançável no enlace.
- **Q5.5** /31 (RFC 3021) usa os 2 endereços em enlaces ponto a ponto; /32 identifica um único host (não há "rede" nem "broadcast" separados).

## M06
- **Q6.1** `192.0.2.50→A` (/24); `192.0.2.200→B` (/25, prefixo mais longo); `203.0.113.9→C` (padrão).
- **Q6.2** Via y: 2+3 = 5; via z: 5+1 = 6. Melhor 5, próximo salto y.
- **Q6.3** Repasse: por pacote, consulta a tabela e envia pela saída. Roteamento: processo/algoritmo que constrói a tabela.
- **Q6.4** (1) Rota de volta existe? `ip route` / `show ip route` no destino; (2) o gateway do destino é o roteador certo? idem; (3) o roteador recebe e encaminha? `tcpdump -i any icmp` nele; (4) filtragem? `iptables -L -n -v`/ACL. Referência prática: D04, falha 1.

## M07
- **Q7.1** Quatro bits 1 → paridade par = **0**.
- **Q7.2** Desconhecido: inunda por todas as portas exceto a de entrada; broadcast: também inunda.
- **Q7.3** ARP usa broadcast de enlace; roteadores não encaminham broadcast de camada 2.
- **Q7.4** Hub: 1 domínio de colisão para todas as portas. Bridge/switch: um domínio de colisão por porta (switch faz em hardware, com mais portas).
- **Q7.5** A faz ARP do **gateway** (IP de R na rede X). R faz ARP do IP de B na rede Y. A nunca faz ARP de B.

## M08
- **Q8.1** Vantagem: grande banda, baixa atenuação, imune a EMI. Desvantagem: custo e dificuldade de emendas/instalação.
- **Q8.2** Depende da convenção: NRZ: nível alto = 1, baixo = 0 → `H L H H L`. Manchester (IEEE 802.3: 0 = alto→baixo, 1 = baixo→alto) : cada bit tem transição no meio.
- **Q8.3** O trançado reduz a interferência eletromagnética (EMI) e a diafonia, pois a perturbação afeta ambos os fios de forma semelhante.

## M09
- **Q9.1** O IP do roteador/NAT (externo), com porta possivelmente traduzida.
- **Q9.2** A tabela de tradução só tem entrada criada por conexão iniciada de dentro; tráfego não solicitado não corresponde a entrada alguma. Exige DNAT/redirecionamento de porta.
- **Q9.3** O filtro casa `tcp dport 80`; ICMP não casa. Prova: `curl` à porta 80 falha e `curl` a outra porta do mesmo host (ex.: 8080) funciona, contadores da regra incrementam.
- **Q9.4** `ports:` cria DNAT no host Docker para um container; DNAT em roteador faz o mesmo para um host da LAN. Ambos reescrevem o destino; o primeiro é gerenciado pelo Docker.
