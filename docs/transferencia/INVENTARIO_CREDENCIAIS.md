# Inventário de credenciais e acessos

Não contém valores. `Não verificado` significa que a auditoria do repositório não comprova proprietário, membros ou credenciais da plataforma.

| Credencial/acesso | Serviço | Responsável atual | Novo responsável | Ação |
| --- | --- | --- | --- | --- |
| Administração do repositório | GitHub | Conta `Gersonfarias777` | TI/organização institucional | Transferir; criar dois admins; revisar e depois remover acessos pessoais |
| Secrets, webhooks e deploy keys | GitHub | Não verificado | TI | Inventariar no painel; rotacionar/revogar o que não for institucional |
| Administração do projeto `manaira-na-escuta` | Vercel | Time identificado apenas por ID local; titular não verificado | Team institucional | Transferir ou recriar; validar domínio, Git e ambientes |
| Token/OAuth da integração GitHub | Vercel/GitHub | Não verificado | TI | Reconectar usando integração institucional |
| Variáveis/secrets da Vercel | Vercel | Não verificado | TI | Listar nomes/escopos no painel e recadastrar/rotacionar |
| `VERCEL_OIDC_TOKEN` local | Vercel CLI | Sessão local atual | TI | Não transferir valor; gerar token temporário em login institucional |
| Proprietário/editor do projeto Apps Script | Google Workspace | Não verificado | TI + conta de serviço/gestão institucional adequada | Transferir/compartilhar projeto e registrar ID |
| Implantação do Web App | Google Apps Script | Não verificado | TI | Dar controle da implantação; registrar ID/URL/versão; reimplantar institucionalmente se necessário |
| Conta executora e autorizações OAuth | Google Apps Script | Não verificado | Conta institucional | Reautorizar Drive, Sheets e Mail; retirar conta anterior após teste |
| Proprietário da planilha de produção | Google Sheets | Não verificado | TI/área institucional | Transferir propriedade/acesso e revisar compartilhamentos |
| Pasta de anexos | Google Drive | Não verificado | TI/área institucional | Localizar ID correto, transferir e revisar ACL/retenção |
| Caixa `canaldeescuta@manairashopping.com.br` | Google Workspace/e-mail corporativo | Institucional aparente; administração não verificada | TI | Confirmar administrador, delegados, MFA, retenção e recuperação |
| Número `83 99984-4977` | WhatsApp/telefonia | Não verificado | Empresa/TI ou área designada | Comprovar titularidade; inventariar Business/Meta se houver |
| Domínio `manairashopping.com.br` e DNS | Registrador/DNS | Não verificado; não usado como host comprovado do app | TI | Confirmar acesso apenas se houver domínio/customização relacionados |
| Backups/exportações | Sheets/Drive/Apps Script | Não identificados | TI | Definir cofre, periodicidade, retenção e teste de restauração |

## Entrega segura

Credenciais reais devem ser criadas ou rotacionadas sob identidade institucional e armazenadas em gerenciador de senhas/cofre de secrets corporativo. Transferência de propriedade deve ocorrer na própria plataforma sempre que possível. Nunca enviar secrets por README, Markdown, Git, issue, commit, chat ou e-mail aberto.

Procedimento: (1) cadastrar dois administradores institucionais; (2) entregar acessos pelo cofre; (3) testar em sessão da TI; (4) gerar credenciais novas; (5) atualizar serviços sem interrupção; (6) verificar logs e fluxo ponta a ponta; (7) revogar acessos antigos; (8) registrar data, executor e evidência em sistema institucional.
