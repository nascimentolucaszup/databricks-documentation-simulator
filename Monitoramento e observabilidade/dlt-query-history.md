[Documentação](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/index.html)

[Monitorar o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/observability.html)

# Acesse o histórico de consultas para o pipeline Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/#access-query-history-for-delta-live-tables-pipelines)

Este artigo explica como acessar o histórico de consultas e os perfis de consultas associados ao site Delta Live Tables pipeline execução. O senhor pode usar essas informações para depurar consultas, identificar gargalos de desempenho e otimizar a execução do pipeline.

Prévia

Este recurso está em Visualização pública. Os administradores do espaço de trabalho podem ativar esse recurso na página Pré-visualizações. Consulte Manage Databricks Previews.

[Visualização pública](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../release-notes/release-types.html)

[Manage Databricks Previews](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../admin/workspace-settings/manage-previews.html)

## Requisitos

[](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/#requirements)

O site pipeline deve estar configurado para execução no canal de visualização. Consulte Delta Live Tables runtime canal.

[Delta Live Tables runtime canal](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../release-notes/delta-live-tables/index.html#runtime-channels)

O site pipeline deve estar configurado para execução no modo acionado.

## Revise o histórico de consultas para obter atualizações em pipeline

[](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/#review-query-history-for-pipeline-updates)

Para todos os pipelines que atendem aos requisitos, uma instrução de consulta aparece no histórico de consultas quando a visualização materializada e as tabelas de transmissão são atualizadas. Há uma instrução REFRESH para cada execução de fluxo que atualiza uma tabela de destino. O senhor pode usar o filtro de computação na página de histórico de consultas para mostrar apenas as consultas processadas usando Delta Live Tables compute. Consulte História da consulta para saber mais sobre a interface do usuário da história da consulta.

[histórico de consultas](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../sql/user/queries/query-history.html)

[História da](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../sql/user/queries/query-history.html)

Para acessar os detalhes da consulta, siga estes passos:

Clique em  Query History (Histórico de consultas ) na barra lateral.

![Ícone de história](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../_images/history-icon.png)

Marque a caixa de seleção DLT no filtro suspenso de computação.

Clique em uma instrução de consulta para acessar view detalhes resumidos, como a duração da consulta e as métricas agregadas.

Clique em Ver perfil de consulta para abrir o perfil de consulta. Consulte Perfil de consulta para obter detalhes sobre o perfil de consulta.

[Perfil de consulta](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../sql/user/queries/query-profile.html)

Opcionalmente, use os links na seção Fonte de consulta para abrir o pipeline relacionado.

## Acessar o histórico de consultas a partir de um Notebook

[](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/#access-query-history-from-a-notebook)

Para view consultar a história de dentro de um Notebook anexado a um Delta Live Tables pipeline, use os seguintes passos:

Abra o Notebook. Se o Notebook estiver conectado a um Delta Live Tables pipeline, uma interface para inspecionar o pipeline aparecerá na parte inferior do Notebook. Consulte Desenvolver e depurar o pipeline Delta Live Tables no Notebook.

[Desenvolver e depurar o pipeline Delta Live Tables no Notebook](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/dlt-notebook-devex.html)

Clique na história da consulta DLT tab.

Clique no nome de uma consulta para acessar view os detalhes da consulta, como duração, origem da consulta e outras métricas agregadas. Para saber mais sobre os detalhes disponíveis nesse site view, consulte view query details.

[view query details](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../sql/user/queries/query-history.html#query-details)

## Acesse o histórico de consultas na interface do usuário Delta Live Tables pipeline

[](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/#access-query-history-from-the-delta-live-tables-pipeline-ui)

Na página Detalhes do pipeline na interface do usuário Delta Live Tables, clique em Consultar histórico tab próximo à parte inferior da tela para acessar o histórico do seu pipeline. O senhor pode acessar view o painel de detalhes da consulta e o perfil clicando em um extrato.

![A interface do usuário do pipeline DLT que mostra o histórico de consultas associado ao site pipeline.](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/../_images/query-history.png)

## Limitações

[](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/#limitations)

O tempo de provisionamento e de fila não está disponível.

As métricas mostradas no painel de detalhes da consulta são atualizadas em tempo real durante a execução do fluxo, mas o perfil da consulta é atualizado somente após o término da execução do fluxo.

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/dlt-query-history.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
