[Documentação](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/index.html)

[Desenvolver o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/develop-pipelines.html)

# Desenvolver e depurar o pipeline Delta Live Tables no Notebook

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#develop-and-debug-delta-live-tables-pipelines-in-notebooks)

Visualização

A experiência do Notebook para o desenvolvimento do Delta Live Tables está em Public Preview.

[Public Preview](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/../release-notes/release-types.html)

Este artigo descreve os recursos do Databricks Notebook que auxiliam no desenvolvimento e na depuração do código Delta Live Tables.

## Visão geral do recurso

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#overview-of-features)

Quando o senhor trabalha em um Python ou SQL Notebook que é o código-fonte de um Delta Live Tables pipeline existente, é possível conectar o Notebook diretamente ao pipeline. Quando o Notebook está conectado ao pipeline, os seguintes recursos estão disponíveis:

começar e validar o pipeline do Notebook.

view pipelineO gráfico de fluxo de dados e o evento do site log para obter a última atualização no site .Notebook

view pipeline diagnósticos no editor Notebook.

view o status do pipeline's cluster no Notebook.

Acesse a interface do usuário Delta Live Tables pelo site Notebook.

## Pré-requisitos

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#prerequisites)

O senhor deve ter um Delta Live Tables pipeline existente com um Python ou SQL Notebook como código-fonte.

O senhor deve ser o proprietário do pipeline ou ter o privilégio CAN_MANAGE.

## Limitações

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#limitations)

Os recursos abordados neste artigo estão disponíveis somente no site Databricks Notebook. workspace não são suportados.

O terminal da Web não está disponível quando conectado a um pipeline. Como resultado, ele não fica visível como tab no painel inferior.

## Conecte um Notebook a um Delta Live Tables pipeline

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#connect-a-notebook-to-a-delta-live-tables-pipeline)

Dentro do site Notebook, clique no menu suspenso usado para selecionar compute. O menu suspenso mostra todos os seus pipelines Delta Live Tables com esse Notebook como código-fonte. Para conectar o Notebook a um pipeline, selecione-o na lista.

## Visualizar o status do cluster do pipeline

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#view-the-pipelines-cluster-status)

Para entender facilmente o estado do seu pipeline's cluster, seu status é mostrado no menu suspenso compute com uma cor verde para indicar que o cluster está em execução.

## Validar o código do pipeline

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#validate-pipeline-code)

O senhor pode validar o pipeline para verificar se há erros de sintaxe no código-fonte sem processar nenhum dado.

[validar o pipeline](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/updates.html#validate-update)

Para validar um pipeline, siga um destes procedimentos:

No canto superior direito do site Notebook, clique em Validate (Validar).

Pressione Shift+Enter em qualquer célula do site Notebook.

No menu dropdown de uma célula, clique em Validate pipeline.

Observação

Se o senhor tentar validar o pipeline enquanto uma atualização existente já estiver em execução, será exibida uma caixa de diálogo perguntando se deseja encerrar a atualização existente. Se o senhor clicar em Yes, a atualização existente será interrompida e uma atualização válida começará automaticamente.

## começar a pipeline

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#start-the-pipeline)

Uma atualização do site pipeline faz o seguinte: começa a cluster, descobre e valida todas as tabelas e visualizações definidas e cria ou atualiza tabelas e visualizações com os dados mais recentes disponíveis.

Para começar uma atualização de seu site pipeline, clique no botão começar no canto superior direito do site Notebook.

## Exibir o status de uma atualização

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#view-the-status-of-an-update)

O painel superior do site Notebook mostra se há uma atualização do pipeline:

Iniciando

Validação

Parando

## Visualizar erros e diagnósticos

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#view-errors-and-diagnostics)

Depois que o site pipeline foi iniciado ou validado, todos os erros são mostrados em linha com um sublinhado vermelho. Passe o mouse sobre um erro para ver mais informações.

## Exibir eventos do pipeline

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#view-pipeline-events)

Quando anexado a um pipeline, há um evento Delta Live Tables log tab na parte inferior do Notebook.

![Registro de eventos](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/../_images/dlt-event-log-tab.png)

## Exibir o gráfico de fluxo de dados do pipeline

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#view-the-pipeline-dataflow-graph)

Para view um gráfico de fluxo de dados de pipeline, use o gráfico Delta Live Tables tab na parte inferior do site Notebook. A seleção de um nó no gráfico exibe seu esquema no painel direito.

![Fluxo de dados gráfico](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/../_images/dataflow-graph.png)

## Como acessar a interface do usuário Delta Live Tables a partir do Notebook

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#how-to-access-the-delta-live-tables-ui-from-the-notebook)

Para acessar facilmente a interface do usuário Delta Live Tables, use o menu no canto superior direito do site Notebook.

![Abrir na DLT UI a partir de Notebook](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/../_images/open-in-dlt-ui.png)

## Acesse o driver logs e o site Spark UI do Notebook

[](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/#access-driver-logs-and-the-spark-ui-from-the-notebook)

Os drivers logs e Spark UI associados ao pipeline que está sendo desenvolvido podem ser facilmente acessados no menu do Notebook view menu.

![Acesse o driver logs e Spark UI](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/../_images/driver-logs-spark-ui.png)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/dlt-notebook-devex.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
