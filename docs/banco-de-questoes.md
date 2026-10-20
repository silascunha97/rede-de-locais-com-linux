# Banco de questões (caderno do estudante)

Seção 13 do [GUIA_DE_ESTUDOS.md](../GUIA_DE_ESTUDOS.md).

> **Todas as questões são originais** (autoria deste caderno, inspiradas nos tópicos do plano RC27CP e da lista da UFPR citada em [fontes-e-referencias.md](fontes-e-referencias.md)). Nenhuma é cópia ou adaptação de prova. As respostas ficam em [gabarito-referencia.md](gabarito-referencia.md): **tente antes de abrir**.

Nível: ★ básico · ★★ intermediário · ★★★ exige raciocínio em várias etapas. Escreva suas respostas no diário ou abaixo de cada questão.

## Diagnóstico inicial

- **D.1** ★ Converta 203 para binário e 10110101 para decimal.
- **D.2** ★ Quantos valores distintos cabem em 7 bits? E qual o maior valor sem sinal em 9 bits?
- **D.3** ★ Em Linux, qual comando lista os endereços IP das interfaces? E o que mostra `ping`?
- **D.4** ★ Explique com suas palavras a diferença entre largura de banda e latência.

## M01 — Conceitos

- **Q1.1** ★ Um pacote de 1500 bytes é transmitido por um enlace de 10 Mbps. Qual o atraso de transmissão?
- **Q1.2** ★ Um enlace de 2000 km com velocidade de propagação 2×10⁸ m/s: atraso de propagação?
- **Q1.3** ★★ Uma mensagem de 8000 bits passa por dois enlaces de 1 Mbps em série com um roteador *store-and-forward*. Ignorando propagação e filas, qual o atraso total? E se a mensagem for dividida em 4 pacotes de 2000 bits?
- **Q1.4** ★ Classifique em simplex, half ou full-duplex: teclado→PC; rádio walkie-talkie; telefone.
- **Q1.5** ★★ Diferencie Internet, internet, intranet e extranet com um exemplo de cada.

## M02 — Camadas

- **Q2.1** ★ Ordene, de fora para dentro, os cabeçalhos de um quadro Ethernet que carrega uma requisição HTTP.
- **Q2.2** ★★ Dois hosts em redes diferentes se comunicam via um roteador. Quais endereços (MAC, IP, porta) mudam ao longo do caminho? Justifique.
- **Q2.3** ★ Dê o nome da PDU em cada camada do modelo TCP/IP.
- **Q2.4** ★★ Em que ponto do modelo OSI você colocaria TLS? Por que a resposta não é única?

## M03 — Aplicação

- **Q3.1** ★ Qual transporte e porta padrão o DNS usa? Em que caso muda?
- **Q3.2** ★★ Diferencie consulta recursiva e iterativa.
- **Q3.3** ★★ Um site abre por `http://203.0.113.10` mas não por `http://web.lab.test`. Liste três hipóteses e, para cada uma, o comando que a confirma ou descarta.

## M04 — Transporte

- **Q4.1** ★ Descreva o handshake de 3 vias (flags e sentido).
- **Q4.2** ★★ Remetente envia 3 segmentos de 500 bytes; o primeiro byte tem sequência 1000. Quais as sequências e o ACK final esperado?
- **Q4.3** ★★ Por que DNS usa UDP para consultas curtas? Que responsabilidade passa para a aplicação?
- **Q4.4** ★★★ Duas abas do navegador acessam o mesmo servidor, porta 443, do mesmo cliente. Como o servidor distingue as conexões?

## M05 — IPv4 e sub-redes

- **Q5.1** ★★ Divida `192.0.2.0/24` em 4 sub-redes iguais: rede, broadcast e faixa de cada.
- **Q5.2** ★★ Para `198.51.100.77/27`: rede, broadcast, faixa de hosts.
- **Q5.3** ★★★ Projete VLSM para `203.0.113.0/24`: A com 100 hosts, B com 50, C com 20, e dois enlaces ponto a ponto. Indique prefixo, rede e faixa de cada.
- **Q5.4** ★★ Host `192.0.2.130/25` com gateway `192.0.2.1`. O que está errado?
- **Q5.5** ★ Por que `/31` e `/32` são exceção na fórmula 2ⁿ−2?

## M06 — Roteamento

- **Q6.1** ★★ Tabela: `192.0.2.0/24→A`, `192.0.2.128/25→B`, `0.0.0.0/0→C`. Para onde vão `192.0.2.50`, `192.0.2.200`, `203.0.113.9`?
- **Q6.2** ★★ Vetor de distância: x tem vizinhos y (custo 2) e z (custo 5). y anuncia custo 3 até D; z anuncia 1. Melhor custo e próximo salto?
- **Q6.3** ★ Diferencie repasse e roteamento.
- **Q6.4** ★★★ A→B funciona (ida), mas o ping não retorna. Descreva o plano de diagnóstico em 4 passos, com o comando de cada passo.

## M07 — Enlace e switching

- **Q7.1** ★ Calcule o bit de paridade par para `1011001`.
- **Q7.2** ★★ O que o switch faz com quadro cujo MAC de destino é desconhecido? E com broadcast?
- **Q7.3** ★★ Por que o ARP não atravessa roteadores?
- **Q7.4** ★★ Diferencie hub, bridge e switch quanto a domínios de colisão.
- **Q7.5** ★★★ O host A (rede X) fala com o host B (rede Y) pelo roteador R. Que consultas ARP ocorrem, e por quem?

## M08 — Física

- **Q8.1** ★ Uma vantagem e uma desvantagem da fibra frente ao par trançado.
- **Q8.2** ★★ Codifique `10110` em NRZ e em Manchester (convenção a sua escolha, declarada).
- **Q8.3** ★★ Por que o par trançado é trançado?

## M09 — NAT e firewall

- **Q9.1** ★★ O que um servidor externo vê como origem quando um host interno acessa-o através de NAT (masquerade)?
- **Q9.2** ★★ Por que não se consegue iniciar conexão de fora para um host por trás de NAT sem regra adicional?
- **Q9.3** ★★★ Regra de firewall "bloqueia TCP/80 de dentro para fora". O `ping` continua funcionando. Explique, e escreva o teste que prova que o bloqueio é por porta e não por host.
- **Q9.4** ★★ Qual a diferença entre publicar uma porta no Docker (`ports:`) e fazer DNAT em um roteador?

## Questões de transferência (após os laboratórios)

- **T.1** Refaça o PT-05 com 3 segmentos e VLSM, sem consultar o roteiro.
- **T.2** Repita o D03 trocando TCP/UDP e as portas, e **escreva a captura prevista antes de rodar**.
- **T.3** No D04, adicione uma terceira rede e um terceiro host; ajuste rotas e prove a conectividade com `traceroute`.
- **T.4** No D06, bloqueie apenas um host específico e mostre, por contadores do `iptables -v`, que a regra foi atingida.
