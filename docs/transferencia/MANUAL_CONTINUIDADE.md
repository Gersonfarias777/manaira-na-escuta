# Manual de continuidade

## Se o desenvolvedor anterior não estiver disponível amanhã

No estado atual, a TI consegue recuperar o frontend pelo GitHub, mas **não há evidência suficiente de que consiga administrar o backend e os dados de produção**. Este manual torna o código reproduzível; a continuidade real depende da conclusão do checklist de acessos.

## 1. Clonar e conferir

1. Autenticar no GitHub institucional e clonar o repositório.
2. Conferir `git status`, `git branch -a -vv` e o commit aprovado.
3. Não copiar `.env.local` do computador anterior. A aplicação atual não requer variáveis.
4. Abrir `index.html` em servidor HTTP local; não é necessário instalar dependências nem executar build.

## 2. Acessar os serviços

- GitHub: organização institucional → repositório → Settings.
- Vercel: Team institucional → projeto `manaira-na-escuta`.
- Google: Drive/Sheets → planilha de produção; Extensões → Apps Script; Deploy → Manage deployments.
- E-mail: console institucional e caixa `canaldeescuta@manairashopping.com.br`.
- Domínio/WhatsApp: usar apenas os registros e acessos formalmente entregues; não foram comprovados no repositório.

Guardar URLs/IDs administrativos no inventário interno ou cofre, não em Git se revelarem informação sensível.

## 3. Alterar formulário

Editar em paralelo `index.html` e `apps-script/Index.html`. Para tipos e textos, revisar `#tipoGrid`, `TIPO_COPY`, campos, `renderSummary` e `payload`. No backend revisar `CANAL_TIPOS`, `CANAL_CATEGORIAS_DENUNCIA`, `submitManifestacao`, cabeçalhos/linha gravada e `sendCanalEmail_`. Validar anonimato, obrigatoriedade, denúncia, anexos, protocolo e comprovante.

## 4. Alterar e-mail

Editar `CANAL_CONFIG.DEST_EMAIL` em `apps-script/Code.gs`, publicar uma nova versão do Web App e testar recebimento. O remetente é a conta executora da implantação, portanto a TI deve controlar e autorizar essa conta. Para trocar fornecedor, substituir `MailApp.sendEmail`, guardar a nova chave na configuração segura do Apps Script/cofre e documentar logs/rotação.

## 5. Alterar WhatsApp

Não existe integração funcional: o número está na imagem `assets/hero-unificada*.jpg`. Obter a arte-fonte institucional, gerar as duas imagens revisadas e atualizar README/materiais. Se houver Business/Meta fora do código, transferir separadamente conforme o inventário.

## 6. Publicar frontend

Fluxo preferencial: push revisado em `main` → integração GitHub/Vercel institucional cria preview/produção conforme as regras do Team. Confirmar HTTP 200, conteúdo e envio real. Para reconstrução, importar o repositório como site estático na Vercel. Não é necessário `VERCEL_TOKEN` no repositório; autenticação deve ocorrer pela conta/integração institucional.

## 7. Publicar backend Apps Script

O fluxo atual é manual:

1. Abrir a planilha correta e o projeto vinculado.
2. Atualizar `Code.gs`, `Index.html` e `Dashboard.html` a partir do commit aprovado.
3. Executar `authorizeCanalEscuta`/`setupManairaNaEscuta` apenas com backup e revisão, pois essas funções alteram planilha/Drive.
4. Criar nova versão em Manage deployments e manter a URL esperada ou atualizar o endpoint no frontend.
5. Testar envio identificado, anônimo, denúncia e anexo; confirmar linha, acompanhamento, Drive e e-mail.

Futuramente, versionar o projeto com `clasp` e um procedimento CI controlado, sem incluir tokens.

## 8. Backup e restauração

Backup mínimo institucional: repositório Git completo; exportação do projeto Apps Script; cópia/exportação da planilha preservando fórmulas; cópia da pasta de anexos e manifesto de IDs/permissões. Definir frequência e retenção.

Restauração em ambiente novo: criar planilha institucional → vincular Apps Script → importar três arquivos → autorizar → executar setup → restaurar dados com mapeamento de 22/33 colunas → restaurar anexos e referências → implantar Web App → atualizar endpoint → publicar frontend → testar ponta a ponta. Não apontar produção antes da reconciliação de contagens e permissões.

## 9. Diagnóstico e rollback

- Frontend indisponível: verificar deployment/logs Vercel e promover o último deployment aprovado.
- Formulário mostra sucesso sem registro: conferir planilha, execução Apps Script e e-mail; o `no-cors` atual não comprova sucesso.
- Apps Script falha: consultar Executions, quotas e autorização da conta executora; voltar à versão anterior da implantação.
- Anexo falha: conferir tamanho/MIME, quota e permissão da pasta correta.
- Dashboard nega acesso: conferir usuário, domínio Workspace e configuração "execute/access" da implantação.

Registrar incidente, horário, protocolo afetado e ações sem copiar relatos sensíveis para sistemas não autorizados.
