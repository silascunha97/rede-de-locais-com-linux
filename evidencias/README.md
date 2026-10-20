# Evidências

Guarde aqui as evidências dos seus experimentos. **Nada nesta pasta foi produzido pelo autor do caderno em seu nome**: está vazia de propósito.

## Convenção sugerida
```
evidencias/
└── m05/
    ├── 2026-11-02-pt05-show-ip-route.txt
    ├── 2026-11-02-pt05-topologia.png
    └── 2026-11-03-d04-falha1-tcpdump.txt
```
Nome: `AAAA-MM-DD-<lab>-<assunto>.<ext>`.

## O que guardar
- Saída de comandos (`ip route`, `show ip route`, `dig`, `ss`…), como texto.
- Capturas de pacotes: preferir o **trecho de texto** do `tcpdump` (curto) em vez de arquivos `.pcap` volumosos.
- Telas do Packet Tracer (topologia final e detalhes de PDU).
- Diário de laboratório preenchido (modelo na seção 14 do [GUIA](../GUIA_DE_ESTUDOS.md#14-registro-de-erros-e-descobertas)).

## Cuidados
Não coloque senhas, chaves ou dados pessoais. Os laboratórios usam apenas endereços de documentação (RFC 5737).

Para salvar uma saída do PowerShell: `docker compose exec cli ip route > evidencias\m05\2026-11-02-d04-ip-route.txt`.
