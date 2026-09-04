# Checklist de entrega institucional

Marcar somente com evidência arquivada e data/responsável registrados.

## GitHub

- [ ] propriedade transferida para organização institucional
- [ ] pelo menos dois administradores da TI definidos
- [ ] `main` e `gh-pages` revisadas; branch desnecessária encerrada de forma controlada
- [ ] proteção/regras da `main` configuradas
- [ ] Actions, environments e Pages revisados
- [ ] secrets, colaboradores, webhooks, deploy keys e tokens revisados
- [ ] histórico verificado e secret scanning executado

## Vercel

- [ ] propriedade/Team institucional
- [ ] projeto transferido ou recriado
- [ ] GitHub institucional conectado
- [ ] variáveis de Production, Preview e Development inventariadas/configuradas
- [ ] domínio/URL e certificados validados
- [ ] membros, logs, deploys e proteção de produção revisados
- [ ] deploy e rollback testados pela TI

## Google Apps Script, banco e storage

- [ ] projeto Apps Script sob conta/Workspace institucional
- [ ] TI controla a implantação e possui IDs/URL/versão registrados
- [ ] conta executora e escopos OAuth revisados
- [ ] planilha de produção acessível e com propriedade definida
- [ ] todas as cinco abas e fórmulas comparadas ao código
- [ ] pasta de anexos localizada por ID, transferida e com ACL revisada
- [ ] backup de código, planilha e anexos criado e restauração testada
- [ ] logs, quotas e alertas operacionais definidos

## Supabase

- [ ] inexistência confirmada formalmente **ou**, se descoberto, organização/projeto/administração transferidos
- [ ] se existir: schema, migrations, RLS, Auth, Storage, Functions, secrets e dados auditados

## Domínio e DNS

- [ ] ausência de domínio personalizado confirmada ou registrador identificado
- [ ] propriedade institucional e acesso ao registrador/DNS comprovados, se aplicável
- [ ] zona DNS exportada e registros documentados antes de mudança

## E-mail

- [ ] caixa `canaldeescuta@manairashopping.com.br` sob administração institucional
- [ ] conta executora/remetente do `MailApp` confirmada
- [ ] destinatários, delegados, retenção, MFA, recuperação, quotas e logs revisados
- [ ] envio real testado e evidência recebida

## WhatsApp

- [ ] número da arte identificado e titularidade definida
- [ ] inexistência de API/Meta/webhook confirmada ou ativos externos inventariados
- [ ] arte editável entregue para permitir troca do número
- [ ] tokens, se descobertos, sob controle institucional e rotacionados

## Credenciais e segurança

- [ ] inventário confrontado com os painéis administrativos
- [ ] novas credenciais geradas no cofre corporativo
- [ ] acessos antigos revogados somente após validação
- [ ] MFA e recuperação institucional configurados
- [ ] `no-cors`/falso sucesso corrigido e teste ponta a ponta automatizado ou documentado
- [ ] proteção antiabuso e controles LGPD aprovados
- [ ] dashboard testado com autorizado e não autorizado

## Local e continuidade

- [ ] nenhuma dependência crítica no computador anterior
- [ ] `.env.local` não foi transferida nem versionada
- [ ] clone limpo executado pela TI
- [ ] publicação do frontend e reimplantação do Apps Script reproduzidas pela TI
- [ ] responsáveis, SLA, backup, restauração e incidentes formalizados

## Critério final — todos devem ser “SIM”

- [ ] TI administra GitHub
- [ ] TI administra Vercel
- [ ] TI administra Apps Script, Sheets e Drive
- [ ] TI administra domínio/DNS aplicável
- [ ] TI controla e-mail e WhatsApp aplicáveis
- [ ] TI acessa dados e secrets por meio institucional
- [ ] TI gera novas e revoga antigas credenciais
- [ ] TI altera qualquer pergunta/fluxo
- [ ] TI realiza deploy e rollback
- [ ] TI substitui serviços externos
- [ ] TI opera sem o computador/desenvolvedor anterior
