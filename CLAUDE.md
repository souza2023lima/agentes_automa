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

TODO: preencher host, usuário, pasta da aplicação, comando de atualização e
health check da VPS.

```bash
# ssh <VPS_USER>@<VPS_HOST>
# cd <VPS_APP_DIR> && git pull --ff-only && <restart>
# curl -f <health-check-url>
```

## Estrutura

```
docs/            documentação e decisões
.env.example     variáveis esperadas (nunca versionar .env)
```

## Regras do projeto

- Nada de segredo em arquivo versionado; valor real só no `.env` local e na VPS.
- Toda decisão técnica relevante entra em `docs/decisoes.md`.
- Antes de escolher a stack, registrar o motivo em `docs/decisoes.md`.
