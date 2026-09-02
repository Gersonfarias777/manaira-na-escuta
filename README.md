# Manaíra na Escuta — Canal de Escuta / Ouvidoria

Portal do Canal de Escuta do Manaíra Shopping. Mesma arquitetura e mesmo
fluxo do canal irmão do Mangabeira Shopping (ver
[github.com/Gersonfarias777/canal-de-escuta](https://github.com/Gersonfarias777/canal-de-escuta)),
só muda a identidade visual, o e-mail de destino e o telefone. Backend em
Google Apps Script (sem hospedagem paga, grava direto em planilha).

- Tipos de manifestação: Elogio, Sugestão, Crítica, Denúncia.
- Envio identificado ou 100% anônimo.
- Protocolo gerado automaticamente: prefixo `MA-<ano>-`.
- Anexo opcional (PDF, JPG, PNG, até 8 MB).
- Comprovante de envio para download.
- E-mail automático para `canaldeescuta@manairashopping.com.br` a cada envio.
- Registro em planilha própria, com abas de coleta, acompanhamento e
  dashboards executivos (`01_COLETA`, `02_ACOMPANHAMENTO`, `03_DASHBOARD`,
  `04_APRESENTAÇÃO`, `99_LISTAS`).

## Estrutura

- `apps-script/Code.gs` — backend (Google Apps Script): grava na planilha,
  sobe anexo pro Drive, gera protocolo, envia e-mail, monta os dashboards.
- `apps-script/Index.html` — formulário em wizard, servido diretamente pelo
  Apps Script (usa `google.script.run`).
- `apps-script/Dashboard.html` — painel executivo (visão gerencial), servido
  pelo Apps Script para a equipe autorizada (`doGet` sem `?view=form`).
- `index.html` — versão standalone (hospedada fora do domínio Google, ex.
  GitHub Pages) que envia via `fetch` para a URL do Web App publicado.
  **Antes de publicar**, troque `COLE_AQUI_A_URL_DO_APPS_SCRIPT_IMPLANTADO`
  pela URL real do deploy (linha ~601).
- `assets/` — arte oficial do Manaíra na Escuta (logo, contato, fotos da
  equipe) usada como imagem de topo do formulário.

## Como publicar (Google Apps Script)

1. Crie uma **planilha nova** no Google Sheets (ex: "Manaíra na Escuta —
   Respostas") na conta `canaldeescuta@manairashopping.com.br`.
2. Na planilha, vá em **Extensões → Apps Script**.
3. Apague o conteúdo padrão de `Código.gs` e cole o conteúdo de
   `apps-script/Code.gs`.
4. Crie um arquivo HTML chamado exatamente `Index` e cole o conteúdo de
   `apps-script/Index.html`.
5. Crie outro arquivo HTML chamado exatamente `Dashboard` e cole o conteúdo
   de `apps-script/Dashboard.html`.
6. Rode a função `authorizeCanalEscuta` uma vez (seletor de funções no topo →
   `authorizeCanalEscuta` → ▶) e aceite as permissões solicitadas.
7. Isso cria automaticamente:
   - as abas `01_COLETA`, `02_ACOMPANHAMENTO`, `03_DASHBOARD`,
     `04_APRESENTAÇÃO` e `99_LISTAS` na planilha;
   - a pasta **Canal de Escuta - Anexos (Formulario)** no Google Drive.
8. Compartilhe a planilha e a pasta do Drive apenas com quem for tratar as
   manifestações (Ouvidoria/RH do Manaíra Shopping).
9. **Implantar → Nova implantação** → tipo **App da Web** → executar como
   **Eu** → acesso **Qualquer pessoa** (ou restrito ao domínio, se preferir).
10. Copie a URL do Web App gerada.
11. Cole essa URL em `index.html` (linha ~601, no lugar de
    `COLE_AQUI_A_URL_DO_APPS_SCRIPT_IMPLANTADO`) — é o arquivo que vai para o
    GitHub Pages.
12. Sempre que editar o código depois: **Implantar → Gerenciar implantações →
    editar → Nova versão → Implantar**, ou a URL publicada não atualiza.

> Assim como no Mangabeira, o script não usa um ID de planilha fixo — ele
> sempre grava na planilha onde está vinculado (container-bound).

## Acesso ao painel executivo

O `doGet` do Apps Script serve o `Dashboard.html` por padrão (sem
`?view=form`), restrito por e-mail a `canaldeescuta@manairashopping.com.br`
e a qualquer conta `@manairashopping.com.br` (`assertCanalDashboardAccess_`
em `Code.gs`). Ajuste esse domínio se a equipe usar outro.

## O que foi adaptado a partir do Mangabeira

- `DEST_EMAIL`: `canaldeescuta@manairashopping.com.br`.
- Prefixo de protocolo: `MA-` (era `ME-`).
- Nome da planilha: `MANAIRA NA ESCUTA`.
- Paleta de cores: azul (`#0D3B66` / `#1565C0` / `#E3EEF9`) no lugar do
  verde-petróleo do Mangabeira; dourado (`#8A5D00`) mantido como cor de
  alerta/prioridade (é semântico, não de marca).
- Imagem de topo do formulário: arte oficial do Manaíra na Escuta
  (`assets/hero-unificada-opt.jpg`), com logo, contatos (e-mail e WhatsApp
  `83 99984-4977`) e fotos da equipe.
- Domínio de acesso ao dashboard: `@manairashopping.com.br`.

## Pendências antes de publicar

- [ ] Criar a planilha do Google Sheets e colar o script (passos acima).
- [ ] Rodar `authorizeCanalEscuta` e implantar como Web App.
- [ ] Colar a URL do Web App em `index.html`.
- [ ] Publicar `index.html` num domínio próprio (GitHub Pages, por exemplo)
      e divulgar o link (QR code, cartaz, WhatsApp).
- [ ] Rodar `/security-review` antes de publicar em produção, dado que trata
      denúncias sensíveis.
