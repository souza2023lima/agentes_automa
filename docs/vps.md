# VPS de agentes — colaboratech.cloud

Servidor Contabo `vmi3732296.contaboserver.net` — `5.183.35.108`.
Ubuntu 26.04 · 6 vCPU AMD EPYC · 11 GB RAM · 193 GB disco.

Acesso: `ssh vps-agentes` (usuário `itasuporte`, chave `~/.ssh/id_ed25519`).

## Isolamento

Cada aplicação roda em container próprio, com compose, volume e rede
independentes em `/opt/agentes/<app>/`. Portas publicadas **apenas em
127.0.0.1**; o nginx faz o proxy público.

| App | Subdomínio | Porta interna | Pasta | Status |
| --- | --- | --- | --- | --- |
| Hermes Agent | hermes.colaboratech.cloud | 9119 (dashboard) | `/opt/agentes/hermes` | rodando |
| Paperclip | paperclip.colaboratech.cloud | 18081 | `/opt/agentes/paperclip` | pendente |
| OpenBot | openbot.colaboratech.cloud | 18082 | `/opt/agentes/openbot` | pendente |

## Hermes Agent

Imagem `nousresearch/hermes-agent:latest` (Debian 13, Python 3.14), com
s6-overlay supervisionando gateway e dashboard. Limites: 4 GB / 2 vCPU.

```bash
cd /opt/agentes/hermes
docker compose ps
docker compose logs -f --tail 50
docker compose restart
docker exec -it hermes hermes model      # configurar provedor de modelo
docker exec -it hermes hermes doctor
```

Dados persistentes em `/opt/agentes/hermes/data` (`config.yaml`, `.env`,
sessões, memórias, skills).

- Dashboard: porta 9119, login por usuário/senha (variáveis
  `HERMES_DASHBOARD_BASIC_AUTH_*` no `.env` da pasta).
- Webapp: porta 9120, sobe após um provedor de modelo ser configurado.
- `dashboard.trusted_proxies` = `172.18.0.0/16` (rede do compose).

## Proxy e TLS

`/etc/nginx/sites-available/agentes.conf` — um server block por subdomínio.

DNS no Cloudflare: registros `A` apontando para `5.183.35.108`.
Emitir/renovar certificados (após o DNS propagar):

```bash
sudo certbot --nginx -d hermes.colaboratech.cloud \
  -d paperclip.colaboratech.cloud -d openbot.colaboratech.cloud
```

Depois da emissão, o proxy do Cloudflare pode ficar laranja (Full strict).

## Segredos

Nunca versionados. Ficam em `/opt/agentes/<app>/.env` (modo 600).
