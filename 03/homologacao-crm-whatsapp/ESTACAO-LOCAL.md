# Serviços Locais — DragonZord (Grupo Reis)

Este diretório concentra os serviços locais de interface que os painéis DragonZord
acionam via `http://localhost:<porta>`.

## Serviços ativos

| Serviço | Porta | Status | Stack |
|---|---|---|---|
| Vocero CRM 2.7.0 | 3000 | online | Docker Compose (app + Postgres + Nea) |

## Subir / reiniciar

```powershell
# 1. Garantir que o Docker Desktop está ativo
Start-Process "C:\Program Files\Docker\Docker\Docker Desktop.exe"

# 2. Aguardar o daemon
docker info

# 3. Subir a stack
cd "C:\Users\reisc\Documents\Default Project\vocero-crm"
docker compose up -d

# 4. Verificar
curl http://localhost:3000/api/health
```

## Parar

```powershell
cd "C:\Users\reisc\Documents\Default Project\vocero-crm"
docker compose down          # mantém os volumes (dados persistem)
docker compose down -v       # remove volumes (apaga dados - use com cuidado)
```

## Portas reservadas no ecossistema

| Porta | Uso |
|---|---|
| 3000 | Vocero CRM (ativo) |
| 5432 | Postgres (interno, não exposto) |
| 7860 | Notebooks Gradio (F5-TTS, LivePortrait, etc.) |
| 5678 | n8n |
| 8080 | Evolution API |

## Critérios de segurança

- O `.env` do Vocero contém segredos de desenvolvimento e **não é versionado**.
- Nenhum túnel público foi criado. A exposição externa exige Cloudflare Tunnel + Access.
- A infraestrutura de produção da AWS permanece intocada.

## Próximos serviços

Os demais CRMs do Teste 3 (Chatwoot, Typebot, Botpress, DeskcommCRM, WACRM, Evo CRM)
ainda não estão clonados. Cada um será instanciado sob demanda, seguindo o mesmo padrão:
clone → `.env` → `docker compose up -d` → validar HTTP 200.