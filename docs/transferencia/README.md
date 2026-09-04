# Transferência institucional — índice técnico

Auditoria documental realizada em 04/09/2026, sem alterações em produção, transferências, deploy, rotação de credenciais, commit ou push. O código versionado foi inspecionado por completo; contas e dados externos sem acesso administrativo foram classificados como **não verificados**, não como inexistentes.

## 1. Visão geral

O Canal de Escuta é uma aplicação sem framework:

1. `index.html` é o formulário público hospedado na Vercel.
2. O navegador envia um formulário URL-encoded para um Web App do Google Apps Script.
3. `apps-script/Code.gs` valida os dados, gera protocolo, grava em Google Sheets, salva anexos no Google Drive e envia e-mail por `MailApp`.
4. `apps-script/Dashboard.html` é o painel interno servido pelo Apps Script.

Não há Supabase, banco SQL, API de WhatsApp, provedor SMTP nem domínio personalizado identificados no código. O "banco" atual é uma planilha Google Sheets vinculada ao script.

## 2. Arquitetura e ativos

| Camada | Implementação | Onde administrar | Estado da evidência |
| --- | --- | --- | --- |
| Frontend público | HTML/CSS/JS estático | GitHub + Vercel | Produção ativa e igual ao `index.html` local pelo SHA-256 |
| Backend/API | Google Apps Script, `doPost` | Projeto Apps Script vinculado à planilha | URL ativa; proprietário e implantação não verificados |
| Banco | Google Sheets | Arquivo Google Sheets | Estrutura em código; dados e configuração reais não verificados |
| Storage | Google Drive | Pasta criada pelo script | Nome em código; pasta e permissões não verificadas |
| E-mail | `MailApp.sendEmail` | Conta executora do Apps Script | Destinatário em código; conta executora não verificada |
| Painel | Apps Script HTML Service | Mesma implantação do backend | Código versionado; acesso real não validado com usuário autorizado |

Arquivos essenciais: `index.html`, `apps-script/Index.html`, `apps-script/Dashboard.html`, `apps-script/Code.gs` e `assets/`. Não há gerenciador de pacotes, processo de build ou suíte de testes.

## 3. GitHub

- Repositório: `Gersonfarias777/manaira-na-escuta`, público, proprietário aparente pessoal `Gersonfarias777`.
- Branch padrão: `main`; branch remota adicional: `gh-pages`. Ambas estavam sem proteção na API pública.
- `main` estava sincronizada com `origin/main` no commit `2d4466a`.
- Sem tags. O histórico possui autoria da conta `Gersonfarias777`; o commit inicial usa endereço Gmail pessoal.
- Um workflow dinâmico do GitHub Pages está ativo; não existe workflow versionado em `.github/workflows`.
- Ambientes públicos identificados: `github-pages` e `Production`.
- Colaboradores, secrets, webhooks, deploy keys, regras e permissões não são visíveis sem acesso administrativo e devem ser conferidos na entrega.

A TI deve receber administração do repositório (transferência para organização institucional é preferível), revisar colaboradores/secrets/chaves/webhooks, proteger `main`, decidir o destino de `gh-pages` e configurar ao menos dois administradores institucionais.

## 4. Formulário — onde alterar

Há duas cópias do formulário que devem permanecer sincronizadas:

- `index.html`: versão pública/Vercel; envio por `fetch` ao Apps Script.
- `apps-script/Index.html`: versão servida pelo Apps Script; envio por `google.script.run`.

Mapa de alteração:

| Item | Frontend | Backend/estrutura |
| --- | --- | --- |
| Elogio, Sugestão, Crítica, Denúncia | cards `#tipoGrid` e objeto `TIPO_COPY` nas duas cópias | `CANAL_TIPOS` em `Code.gs` |
| Categorias de denúncia | `<select id="categoriaDenuncia">` nas duas cópias | `CANAL_CATEGORIAS_DENUNCIA` |
| Identificação/anonimato | etapa 2 e validações JS | bloco `identificado` de `submitManifestacao` |
| Perguntas gerais | etapa 3, `renderSummary` e construção de `payload` | validações e array `row` de `submitManifestacao` |
| Campos condicionais da denúncia | `applyTipoCopy` | bloco `if (tipo === 'Denúncia')` |
| Anexo | etapa 4 e `FileReader` | `MAX_FILE_BYTES`, `ALLOWED_MIME_TYPES`, `decodeCanalFile_` |
| Protocolo | geração antes do envio | `PROTOCOL_PREFIX`, regex e `createCanalProtocol_` |
| Planilha operacional | não aplicável | `getCollectionHeaders_`, `getFollowupHeaders_`, `setupListsSheet_` e rotinas `setup*` |
| E-mail | não aplicável | `DEST_EMAIL` e `sendCanalEmail_` |
| Endpoint | URL literal no `fetch` de `index.html` | implantação do Web App |

Fluxo atual: tipo → identificação/anonimato → detalhes → anexo opcional → revisão/declaração → envio. Nome é obrigatório somente no modo identificado; assunto (3–150) e descrição (10–4000) são obrigatórios; categoria é obrigatória para denúncia; contato é exigido quando identificado e solicita retorno. Anexos aceitos: PDF/JPEG/PNG, até 8 MB.

Depois de qualquer mudança, atualizar as duas cópias, revisar cabeçalhos/linha gravada/e-mail, criar nova versão do Apps Script e publicar o frontend. Hoje não há mecanismo automático que impeça divergência entre as cópias.

## 5. Supabase

Não foram encontrados SDK, URL, chaves, migrations, schemas, RLS, Auth, Storage, Edge Functions, triggers ou configuração Supabase. Portanto, não há projeto Supabase a transferir segundo as evidências disponíveis. Antes da assinatura da entrega, o responsável atual deve declarar formalmente se existe algum projeto externo não referenciado pelo repositório.

## 6. Banco e armazenamento

O banco é Google Sheets, com abas `01_COLETA`, `02_ACOMPANHAMENTO`, `03_DASHBOARD`, `04_APRESENTAÇÃO` e `99_LISTAS`. Cabeçalhos, listas, validações, fórmulas e dashboards são recriáveis por `setupManairaNaEscuta`; dados de produção, ID da planilha, histórico, compartilhamentos e proteções não estão versionados. Anexos são guardados na primeira pasta Drive encontrada com o nome `Canal de Escuta - Anexos (Formulario)`; o ID e as ACLs não estão versionados.

Para a transferência, compartilhar/transferir a planilha, projeto Apps Script e pasta com contas institucionais; registrar IDs no cofre/inventário operacional; exportar backups de Sheets e Drive; validar permissões; e definir retenção e resposta a incidentes para denúncias e dados pessoais.

## 7. Vercel e deploy

- Projeto localmente vinculado: `manaira-na-escuta`; IDs de projeto/time existem em `.vercel/project.json`, arquivo ignorado.
- URL ativa: `https://manaira-na-escuta.vercel.app` (HTTP 200 em 04/09/2026).
- O conteúdo servido tinha o mesmo SHA-256 do `index.html` local.
- Integração GitHub é fortemente indicada pelos deployments públicos de cada commit de `main`, mas membros, conta/time, variáveis, domínios, logs e permissões não puderam ser auditados sem sessão Vercel.
- Nenhum `vercel.json`, redirect, rewrite ou workflow próprio foi encontrado. O site é estático e não requer build documentado.
- A única variável local identificada foi `VERCEL_OIDC_TOKEN`, temporária da ferramenta, ignorada e não necessária à aplicação.

**Cenário A — transferir o projeto:** criar/usar Team institucional, adicionar administradores da TI, transferir o projeto, reconectar o GitHub institucional, revisar ambientes/variáveis/domínios e remover o antigo proprietário após validação.

**Cenário B — recriar:** importar o repositório na conta institucional, definir `index.html` como conteúdo estático, configurar produção/preview, validar o endpoint do Apps Script, associar domínio se houver, comparar hash/comportamento e só então desativar o projeto anterior.

Resposta atual: **PARCIALMENTE**. O deploy é reproduzível a partir do Git, mas a TI ainda não possui administração comprovada da conta/time e da integração atual.

## 8. Domínio e DNS

Não foi identificado domínio personalizado. O único endereço público comprovado é o subdomínio gerenciado pela Vercel `manaira-na-escuta.vercel.app`; o `homepage` do GitHub aponta para ele. Não há registrador, nameservers, certificados ou registros DNS próprios no repositório.

| Tipo | Host | Destino | Serviço |
| --- | --- | --- | --- |
| Gerenciado pelo provedor | `manaira-na-escuta.vercel.app` | Projeto Vercel `manaira-na-escuta` | Vercel |

Esta linha não é um registro DNS administrável no registrador da empresa. Não se deve inventar A/CNAME. Se existir domínio divulgado fora do repositório, a TI deve obter acesso ao registrador, exportar a zona e documentar os registros antes de qualquer mudança.

## 9. E-mail

O envio usa `MailApp`, sem SMTP/API key no código. Destinatário: `canaldeescuta@manairashopping.com.br`, definido em `CANAL_CONFIG.DEST_EMAIL`; assunto e corpo ficam em `sendCanalEmail_`. O remetente efetivo, quotas, logs e propriedade dependem da conta que executa a implantação Apps Script e não foram verificados. A TI precisa controlar essa conta/projeto e a caixa destinatária, revisar delegação e retenção e fazer um teste institucional. Trocar fornecedor exigirá substituir `MailApp` no backend e cadastrar a nova credencial fora do Git.

## 10. WhatsApp

Foi identificado somente o número `83 99984-4977` incorporado na arte e citado no README. Não há `wa.me`, API, Meta, Twilio, Evolution, token ou webhook no código. Para alterar o número atual é necessário substituir as artes-fonte/arquivos JPEG e atualizar a documentação; a origem editável da arte não está versionada. A TI deve confirmar formalmente a titularidade do número e se existe uma conta WhatsApp Business externa não refletida no projeto.

## 11. Variáveis e secrets

Consulte [VARIAVEIS_AMBIENTE.md](VARIAVEIS_AMBIENTE.md) e [INVENTARIO_CREDENCIAIS.md](INVENTARIO_CREDENCIAIS.md). Nenhum valor secreto foi incluído. A URL pública do Apps Script não é segredo, mas concede acesso ao endpoint e deve ser inventariada como configuração.

## 12. Segurança e riscos prioritários

1. O `fetch` público usa `mode: 'no-cors'`; a Promise pode resolver sem que seja possível ler a resposta. A interface mostra sucesso e protocolo local mesmo se o backend retornar erro. Exigir teste ponta a ponta e corrigir antes de confiar no comprovante.
2. O endpoint público não apresenta autenticação, rate limit, CAPTCHA ou proteção antiabuso no código. Pode haver spam, consumo de quotas e criação de anexos maliciosos dentro dos MIME permitidos.
3. O repositório é público e contém o endpoint do Apps Script. Não foram encontrados padrões comuns de chaves privadas/tokens no histórico auditado, mas GitHub secret scanning e revisão administrativa ainda são necessários.
4. Denúncias, contatos e anexos são dados pessoais/sensíveis. Acesso, retenção, backups, logs, base legal, aviso de privacidade e plano de incidente precisam de validação institucional/LGPD.
5. A autorização do dashboard depende de `Session.getActiveUser().getEmail()` e do domínio; deve ser testada com a configuração real da implantação. Código e configuração da implantação são controles distintos.
6. Backend implantado não possui pipeline/clasp nem identificação de versão no Git; o conteúdo ativo pode divergir do repositório.

## 13. Documentos de entrega

- [Relatório final](RELATORIO_TRANSFERENCIA_INSTITUCIONAL.md)
- [Manual de continuidade](MANUAL_CONTINUIDADE.md)
- [Conteúdo necessário no repositório](CONTEUDO_REPOSITORIO.md)
- [Mapa dos dados](MAPA_DADOS.md)
- [Validação de recebimento pela TI](VALIDACAO_RECEBIMENTO_TI.md)
- [Checklist institucional](CHECKLIST_ENTREGA_INSTITUCIONAL.md)
- [Matriz de propriedade](MATRIZ_PROPRIEDADE.md)
- [Variáveis de ambiente](VARIAVEIS_AMBIENTE.md)
- [Inventário de credenciais](INVENTARIO_CREDENCIAIS.md)

## 14. Checklist de transferência

A transferência só termina após todos os itens do checklist estarem marcados e as evidências (capturas/exportações, responsáveis, datas e teste de restauração) estarem arquivadas em local institucional, fora do Git quando contiverem informação sensível.
