# Mapa dos dados e reconstrução da planilha

O armazenamento de produção é uma planilha Google vinculada ao Apps Script. `setupManairaNaEscuta()` cria ou atualiza sua estrutura. Essa execução altera a planilha; fazer backup antes de usá-la sobre uma base existente.

## Abas

| Aba | Finalidade | Origem da estrutura |
| --- | --- | --- |
| `01_COLETA` | Registro original das manifestações | `getCollectionHeaders_()` e `submitManifestacao()` |
| `02_ACOMPANHAMENTO` | Investigação, risco, prazos e conclusão | `getFollowupHeaders_()` e `appendFollowupRow_()` |
| `03_DASHBOARD` | Indicadores na planilha | `setupDashboard_()` |
| `04_APRESENTAÇÃO` | Painel para apresentação | `setupPresentationDashboard_()` |
| `99_LISTAS` | Listas de validação | `setupListsSheet_()` |

## `01_COLETA` — 22 colunas

Data/hora; protocolo; tipo; modo de envio; nome; setor/função; contato; categoria da denúncia; assunto; descrição; contexto; local/setor; data aproximada; recorrência; pessoas envolvidas; testemunhas; identificação das testemunhas; urgência; solicitação de retorno; URL do anexo; status; prazo para confirmação.

Os nomes exatos e a ordem são definidos por `getCollectionHeaders_()`. Ao restaurar dados, não mudar a ordem sem atualizar o array gravado por `submitManifestacao()`.

## `02_ACOMPANHAMENTO` — 33 colunas

Protocolo, recebimento, tipo, categoria, status, prioridade, responsável, início, relato, contexto, local/data, recorrência, fatores, procedimentos, evidência, análise técnica, descrição do risco, probabilidade, severidade, nível de risco, impactos, plano de ação, data prevista, indicadores, revisão do PGR, documento digitalizado, conclusão, resultado, retorno, dias em aberto, prazo, última atualização e observações de governança.

Os nomes exatos, fórmulas, formatos e validações estão em `getFollowupHeaders_()`, `appendFollowupRow_()` e `setupFollowupValidation_()`.

## Relacionamentos e classificações

- O protocolo `MA-AAAA-XXXXXXXX` relaciona coleta e acompanhamento.
- A URL do anexo fica na coluna 20 da coleta; o arquivo fica no Drive.
- Tipos: Elogio, Sugestão, Crítica e Denúncia.
- Status: Recebida, Em triagem, Em investigação, Plano de ação, Aguardando informação, Concluída e Arquivada.
- Prioridades: Baixa, Média, Alta e Crítica.
- Categorias de denúncia ficam em `CANAL_CATEGORIAS_DENUNCIA`.

## Backup e verificação

O backup mínimo inclui cópia nativa/exportação da planilha, projeto Apps Script, pasta de anexos, data, proprietário e contagens. Dados reais não devem entrar no Git.

Após restaurar, comparar contagens das duas abas principais, amostrar protocolos, validar fórmulas, abrir anexos autorizados, conferir dashboards e realizar uma manifestação de teste identificada como teste.
