# Conteúdo necessário no repositório

O repositório é tecnicamente autossuficiente quando uma pessoa autorizada da TI, com os acessos institucionais, consegue reconstruir, alterar, publicar, testar e restaurar a aplicação usando este conteúdo. Isso não significa guardar dados ou senhas no Git.

## Conteúdo versionado

| Necessidade | Arquivo/diretório | Situação |
| --- | --- | --- |
| Frontend público | `index.html` | Disponível |
| Formulário servido pelo Google | `apps-script/Index.html` | Disponível |
| Backend, validações, e-mail e planilha | `apps-script/Code.gs` | Disponível |
| Painel executivo | `apps-script/Dashboard.html` | Disponível |
| Manifesto Apps Script | `apps-script/appsscript.json` | Disponível |
| Modelo de vínculo `clasp` | `apps-script/.clasp.json.example` | Disponível sem ID real |
| Imagens utilizadas | `assets/` | Disponíveis em JPEG |
| Configuração de ambiente | `.env.example` e `VARIAVEIS_AMBIENTE.md` | Disponível |
| Arquitetura e mapa de alterações | `docs/transferencia/README.md` | Disponível |
| Estrutura dos dados | `MAPA_DADOS.md` | Disponível |
| Publicação, recuperação e diagnóstico | `MANUAL_CONTINUIDADE.md` | Disponível |
| Prova de entrega | `VALIDACAO_RECEBIMENTO_TI.md` | Disponível |
| Ativos e credenciais externas | Matriz e inventário de credenciais | Disponível sem valores |

## Itens que não devem estar no Git

| Item | Onde deve ficar |
| --- | --- |
| Senhas, tokens, PINs e sessões | Cofre corporativo |
| `.clasp.json` real e `.env.local` | Máquina/CI institucional protegida |
| Denúncias e dados de produção | Google Sheets institucional |
| Anexos de produção | Google Drive institucional |
| IDs administrativos internos | Cofre ou inventário operacional restrito |
| Zona e credenciais DNS | Provedor DNS/cofre |
| Recuperação do WhatsApp | Cofre corporativo |

## Entregas externas obrigatórias

Mesmo com o código completo, a TI deve receber administração de GitHub e Vercel; acesso/propriedade do Apps Script, planilha e pasta Drive; domínio/DNS; e-mail; WhatsApp; e um backup inicial dos dados e anexos.

Também deve ser entregue o arquivo-fonte editável da arte, se existir. O Git contém somente JPEG; sem a fonte, trocar telefone ou textos incorporados à imagem exige recriação gráfica.

## Regra de aceite

O código está completo quando a primeira tabela permanece atendida. A custódia só está completa depois que a TI conclui `VALIDACAO_RECEBIMENTO_TI.md` e comprova as entregas externas.
