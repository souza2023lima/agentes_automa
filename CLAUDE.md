# CLAUDE.md — agentes_automa

Regras gerais de `~/Work` continuam valendo. Este arquivo cobre o específico
do projeto.

## Stack

Ainda não definida. Projeto iniciado como estrutura + documentação.
Quando a stack for escolhida, atualizar esta seção e a seção **Comandos**.

## Comandos

```bash
# instalar dependências   -> (a definir)
# rodar                   -> (a definir)
# testar                  -> (a definir)
# lint                    -> (a definir)
# build                   -> (a definir)
```

## Deploy

VPS Contabo `vmi3732296.contaboserver.net` — Ubuntu 26.04, 193 GB de disco,
11 GB de RAM. Acesso por chave (`~/.ssh/id_ed25519`), alias `vps-agentes`:

```bash
ssh vps-agentes              # itasuporte@5.183.35.108
```

Pasta da aplicação e health check: TODO (definir quando a stack existir).

```bash
# cd <VPS_APP_DIR> && git pull --ff-only && <restart>
# curl -f <health-check-url>
```

Observações: `docker` e `node` não instalados; `git` 2.53 e `python3` 3.14
disponíveis; `sudo` pede senha.

## Estrutura

```
docs/            documentação e decisões
.env.example     variáveis esperadas (nunca versionar .env)
```

## Regras do projeto

- Nada de segredo em arquivo versionado; valor real só no `.env` local e na VPS.
- Toda decisão técnica relevante entra em `docs/decisoes.md`.
- Antes de escolher a stack, registrar o motivo em `docs/decisoes.md`.
