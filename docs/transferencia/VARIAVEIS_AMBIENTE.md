# Variáveis de ambiente

Inventário de 04/09/2026. O código da aplicação não lê variáveis de ambiente.

| Variável | Serviço | Finalidade | Ambiente | Sensível? |
| --- | --- | --- | --- | --- |
| `VERCEL_OIDC_TOKEN` | Vercel CLI | Token temporário gerado para operações locais da CLI; não é usado pela aplicação | Local | Sim |

`VERCEL_OIDC_TOKEN` foi identificado apenas pelo nome em `.env.local`, que está corretamente ignorado. Não copiar seu valor, não o colocar no `.env.example` como requisito e renová-lo pela autenticação institucional da Vercel quando necessário.

Configurações hoje fixadas no código, e não em ambiente:

| Configuração | Local | Observação |
| --- | --- | --- |
| URL do Web App | `index.html`, chamada `fetch` | Pública, mas operacionalmente crítica |
| E-mail destinatário | `CANAL_CONFIG.DEST_EMAIL` | Alterar e reimplantar Apps Script |
| Prefixo de protocolo | `CANAL_CONFIG.PROTOCOL_PREFIX` | Manter frontend e backend coerentes |
| Limite/MIME de anexos | `CANAL_CONFIG` e formulários | Duplicado nas camadas |

Antes da entrega, um administrador Vercel deve exportar **somente os nomes, escopos e ambientes** das variáveis do projeto pelo painel/CLI institucional e comparar com esta lista. Valores devem permanecer no cofre corporativo. Se o endpoint for parametrizado futuramente, documentar o nome escolhido e deixar apenas um placeholder no `.env.example`.
