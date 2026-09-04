# Relatório de transferência institucional

**Data da auditoria:** 04/09/2026

**Escopo:** repositório local, metadados públicos do GitHub, arquivos locais ignorados apenas por nome/configuração, disponibilidade pública da Vercel e do endpoint Apps Script.
**Fora do alcance:** painéis autenticados de GitHub/Vercel/Google, conteúdo da planilha/Drive, caixa de e-mail, registrador/DNS e WhatsApp/Meta.

## 1. Resumo executivo

O código é pequeno, legível e o frontend pode ser reproduzido sem ferramentas especiais. A produção Vercel estava ativa e idêntica ao `index.html` local. Porém, a custódia institucional completa não está demonstrada: GitHub está em conta pessoal; Vercel não foi auditada administrativamente; Apps Script, planilha, anexos e conta executora não têm proprietário/IDs/permissões registrados; não existem backups/restauração comprovados; e há risco funcional de falso sucesso no envio.

**Nota de transferibilidade atual: 42%.** A nota mede evidência de custódia, não qualidade visual: código/documentação e frontend são recuperáveis, mas os ativos que recebem e guardam denúncias continuam dependentes de acessos externos não comprovados.

## 2. Situação atual por área

| Área | Situação | Evidência/pendência principal |
| --- | --- | --- |
| GitHub | Parcial | Público em `Gersonfarias777`; branches sem proteção; settings privados não auditados |
| Código/histórico | Bom | `main` sincronizada, histórico presente, sem padrões comuns de secrets encontrados; sem tags/testes |
| Vercel | Parcial | Site 200 e hash igual ao local; Team, membros, vars e integração não auditados |
| Apps Script | Crítico | Código versionado e endpoint ativo; projeto, versão implantada e proprietário não comprovados |
| Banco/Sheets | Crítico | Schema lógico em código; dados, ACL, ID e backup não auditados |
| Drive/storage | Crítico | Nome da pasta em código; ID, proprietário, ACL e backup desconhecidos |
| Supabase | Não aplicável aparente | Nenhuma referência/configuração; exigir declaração de inexistência externa |
| E-mail | Parcial/crítico | Destino institucional em código; remetente/conta executora, quotas e logs desconhecidos |
| WhatsApp | Baixo impacto técnico | Apenas número em imagem; titularidade e arte editável ausentes |
| Domínio/DNS | Não identificado | Somente `vercel.app`; nenhum domínio personalizado comprovado |
| Secrets | Parcial | Nenhum secret requerido pelo app no Git; painéis não auditados; token local ignorado |
| Continuidade local | Parcial | Sem caminhos absolutos/symlinks; `.vercel` e `.env.local` são locais, mas não essenciais ao app |

## 3. GitHub

Branch padrão `main`, remota `gh-pages`, sem proteção pública observada, sem tags, um workflow dinâmico Pages e ambientes `github-pages`/`Production`. Deployments públicos associam commits de `main` à produção. O proprietário atual é uma conta nominativa; há endereço Gmail pessoal no commit inicial. A transferência deve ser para organização institucional, preservando histórico, seguida de regras de branch, revisão de acessos e reconexão Vercel.

## 4. Vercel

Projeto local `manaira-na-escuta`, URL `https://manaira-na-escuta.vercel.app`, sem `vercel.json`, redirects/rewrites ou build customizado. Em 04/09/2026, HTTP 200 e SHA-256 do HTML remoto igual ao arquivo local. A CLI não estava disponível para auditar conta/variáveis; os IDs locais provam vínculo, não titularidade. Transferir para Team institucional ou recriar conforme os dois cenários do índice.

**Após a transferência, a TI administrará deploy sem a conta anterior? PARCIALMENTE hoje.** Será “SIM” apenas após acesso institucional, reconexão Git, teste de deploy e rollback.

## 5. Supabase e banco

Supabase não integra a solução auditada. Não há migrations SQL porque a persistência é Sheets. A estrutura de cinco abas, cabeçalhos, validações, fórmulas e dashboards está em `Code.gs`, mas isso não substitui dados, compartilhamentos, proteções nem configurações da planilha real. Produção deve ser transferida no Google Workspace ou migrada formalmente.

## 6. Formulário

Tipos, perguntas, obrigatoriedade, condicionais, anexos, anonimato e protocolo foram mapeados no índice. A alteração exige sincronizar duas versões HTML e o backend. Falta teste automatizado e existe falso positivo potencial de envio devido a `no-cors`. O protocolo exibido é criado no navegador e aceito pelo backend se válido; a tela não confirma que a gravação ocorreu.

## 7. E-mail

`MailApp` envia para `canaldeescuta@manairashopping.com.br`, com template texto em código e anexo opcional. Não há API key. Controle efetivo pertence à identidade executora do Apps Script e ao administrador da caixa; ambos precisam ser formalmente entregues e testados.

## 8. WhatsApp

Somente o número `83 99984-4977` aparece na arte/README. Não foi localizada integração, link, token ou webhook. Faltam titularidade documentada e arquivo-fonte editável da arte.

## 9. Domínio e DNS

Nenhum domínio personalizado foi comprovado. Não há registros DNS a transferir com base nas evidências. Se houver URL institucional divulgada fora do repositório, a zona deve ser exportada pelo administrador antes da transferência.

## 10. Variáveis, secrets e dependências locais

A aplicação não usa env vars. `.env.local` contém somente o nome `VERCEL_OIDC_TOKEN`, está ignorada e não deve ser entregue. `.vercel/project.json`, também ignorado, guarda vínculo local recriável. Não existem caminhos absolutos, certificados, symlinks, banco ou scripts essenciais exclusivos do computador identificados. A origem editável das imagens e credenciais/sessões administrativas externas continuam como dependências humanas, não técnicas versionadas.

## 11. Segurança

Pendências de maior prioridade: corrigir confirmação `no-cors`; proteção antiabuso/quota; validar autorização do dashboard na implantação real; testar divergência entre código implantado e Git; formalizar LGPD, retenção, menor privilégio, backups e incidentes; executar secret scanning administrativo. Nenhuma mudança de segurança em produção foi feita nesta tarefa.

## 12. Pendências bloqueadoras

1. Transferir GitHub para organização e comprovar administradores/regras.
2. Transferir ou recriar Vercel em Team institucional e testar deploy/rollback.
3. Entregar projeto e implantação Apps Script, conta executora e autorizações OAuth.
4. Transferir planilha e pasta de anexos com IDs, ACLs, dados e backups.
5. Confirmar controle da caixa de e-mail e testar o fluxo real.
6. Corrigir/testar o falso sucesso do frontend e controles antiabuso.
7. Confirmar situação de domínio/DNS, WhatsApp/Meta e Supabase por declaração do responsável.
8. Rotacionar/revogar credenciais antigas somente após o teste institucional completo.

## 13. Critério de sucesso

Hoje, não é possível responder “SIM” a administração de GitHub, Vercel, Google Apps Script/Sheets/Drive, secrets, geração/revogação de credenciais, domínio/DNS e operação sem a conta anterior. A possibilidade de alterar perguntas e republicar o frontend está documentada, mas o backend produtivo ainda depende de custódia externa não comprovada.

## 14. Resultado final

> Se a transferência fosse realizada hoje, o órgão de Tecnologia teria controle técnico, administrativo e operacional integral do Canal de Escuta?

### NÃO

Faltam comprovação e transferência dos acessos administrativos de GitHub, Vercel e Google; custódia da planilha/dados/anexos; controle da conta executora e e-mail; inventário autenticado de integrações/secrets; confirmação de domínio e WhatsApp; backup/restauração testados; e validação segura do envio. A documentação agora permite conduzir e comprovar essas etapas sem colocar credenciais no Git.
