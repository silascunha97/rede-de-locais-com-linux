# Redes Locais com Linux — estudos de Redes de Computadores com PBL

Repositório de estudo individual de **Redes de Computadores** (disciplina RC27CP, UTFPR Pato Branco), com o livro *Redes Locais com Linux* (Douglas Vigliazzi, Visual Books) como uma das referências, organizado pela metodologia **PBL — Problem-Based Learning (Aprendizagem Baseada em Problemas)**.

O objetivo não é decorar comandos, e sim **explicar por que uma rede funciona, observar seu comportamento, provocar e diagnosticar falhas e demonstrar isso com evidências**.

> **Estado atual (2026-10-20):** material em construção. Nenhum módulo foi estudado ainda (todos "Não iniciado"). Os 6 laboratórios Docker foram executados pelo autor; os 8 roteiros de Packet Tracer **não** foram executados (apenas revisados). O mapeamento do livro está pendente (falta o sumário).

## O que é PBL aqui

Em vez de começar pela teoria, cada módulo começa por um **problema técnico plausível**, com sintomas mas sem causa nem solução. O fluxo é:

1. **Problema** — situação com objetivo verificável.
2. **Investigação inicial** — o que se sabe, o que não se sabe, hipóteses e o teste que refutaria cada uma (antes de ler a teoria).
3. **Objetivos de aprendizagem** — derivados das lacunas encontradas.
4. **Estudo autodirigido** — livro, plano de ensino, documentação oficial, questões.
5. **Solução preliminar** — tratada como hipótese até haver evidência.
6. **Experimentação** — Packet Tracer e Docker.
7. **Análise das evidências** — esperado × observado.
8. **Conclusão e reflexão** — por que funcionou, qual hipótese estava errada.
9. **Transferência** — uma variação do problema, resolvida sem copiar a configuração.

Exemplo de problema (módulo 5): dois hosts com interface ativa não se comunicam; é preciso decidir se a causa é IP, máscara, gateway ou rota, **com evidência de cada diagnóstico**.

As respostas ficam separadas, em [docs/gabarito-referencia.md](docs/gabarito-referencia.md), para não antecipar a investigação.

## As três frentes

| Frente | Ferramenta | Papel |
|---|---|---|
| A | Teoria e problemas | Compreensão, hipóteses, cálculo e explicação causal |
| B | Cisco Packet Tracer | Visualizar e configurar topologias simuladas |
| C | Docker (Linux) | Reproduzir aspectos em redes executáveis, com captura de pacotes |

As frentes **não são equivalentes**: uma bridge Docker não é um switch gerenciável nem uma LAN física, e o Packet Tracer não modela o TCP em detalhe. Cada módulo registra o que pode e o que não pode ser comparado.

## Módulos

| ID | Tema | Packet Tracer | Docker |
|---|---|---|---|
| [M01](modulos/modulo-01-conceitos.md) | Conceitos e atrasos | PT-01 | — |
| [M02](modulos/modulo-02-camadas-encapsulamento.md) | Camadas e encapsulamento | PT-02 | D01 |
| [M03](modulos/modulo-03-aplicacao-dns-http.md) | Aplicação: DNS e HTTP | PT-03 | D02 |
| [M04](modulos/modulo-04-transporte.md) | Transporte: TCP e UDP | PT-04 | D03 |
| [M05](modulos/modulo-05-ipv4-subredes.md) | IPv4 e sub-redes | PT-05 | D04 |
| [M06](modulos/modulo-06-roteamento.md) | Repasse e roteamento | PT-06 | D04 |
| [M07](modulos/modulo-07-enlace-switching.md) | Enlace, ARP e switching | PT-07 | D05 |
| [M08](modulos/modulo-08-camada-fisica.md) | Camada física | — | — |
| [M09](modulos/modulo-09-nat-firewall.md) | NAT e firewall (complementar) | PT-08 | D06 |

Fechamento: [projeto integrador](docs/projeto-integrador.md).

## Estrutura

```
GUIA_DE_ESTUDOS.md              caderno principal (índice, registros, avaliação)
docs/                           fontes, plano, critérios, questões, gabarito, projeto
modulos/                        módulos PBL
laboratorios/packet-tracer/     roteiros (.md)
laboratorios/docker/            compose.yaml + README por laboratório
evidencias/                     suas evidências (vazia)
```

## Como começar

1. Leia o [GUIA_DE_ESTUDOS.md](GUIA_DE_ESTUDOS.md).
2. Faça o [diagnóstico inicial](docs/banco-de-questoes.md#diagnóstico-inicial).
3. Abra o [módulo 01](modulos/modulo-01-conceitos.md) e responda a investigação inicial **antes** da teoria.
4. Para os laboratórios Docker (Docker com Compose v2):
   ```powershell
   cd laboratorios\docker\d01-encapsulamento
   docker compose up -d
   # ... siga o README do laboratório ...
   docker compose down -v
   ```
   Rode **um laboratório por vez** (as sub-redes se repetem). Leia antes o [README dos laboratórios](laboratorios/docker/README.md).

## Avaliação

Quatro níveis (0 Não demonstrado, 1 Inicial, 2 Funcional, 3 Consolidado) aplicados a hipóteses, endereçamento, implementação, diagnóstico, evidências, explicação e transferência. Um laboratório que "funcionou" **não** está concluído: exige explicação do mecanismo e evidência. Veja [docs/criterios-de-avaliacao.md](docs/criterios-de-avaliacao.md).

## Fontes e limitações

- **Plano de ensino:** `RC27CP.md` / `RC27CP.pdf` define o conteúdo-núcleo.
- **Livro:** só a capa foi fornecida; **sem capítulos nem páginas citados** até haver sumário.
- **Provas:** nenhuma fornecida; as questões do banco são **originais**.
- **Fundamentação da PBL:** este README descreve o fluxo adotado, **sem citar literatura**. A pesquisa metodológica com referências verificáveis (autores, DOI/URL) ainda **não foi feita**; ela é o objetivo do documento `MODELO_PBL_REDES.md`, que **não foi criado**.
- Detalhes: [docs/fontes-e-referencias.md](docs/fontes-e-referencias.md).

`ex-rede-computadores.md` é um rascunho anterior, **superado** pelo guia (continha um laboratório de roteamento que não funcionava).
