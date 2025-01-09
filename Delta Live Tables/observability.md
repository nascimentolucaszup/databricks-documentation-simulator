[Documentação](https://docs.databricks.com/pt/delta-live-tables/observability.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/observability.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/observability.html/index.html)

# Monitorar pipelines Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#monitor-delta-live-tables-pipelines)

Este artigo descreve o uso de monitoramento integrado e recurso de observabilidade para o pipeline Delta Live Tables. Esses recursos dão suporte a tarefas como as do senhor:

Observar o progresso e o status das atualizações do pipeline. Consulte Quais detalhes do pipeline estão disponíveis na interface do usuário?

[Quais detalhes do pipeline estão disponíveis na interface do usuário?](https://docs.databricks.com/pt/delta-live-tables/observability.html/#pipeline-details)

Alertas sobre eventos do pipeline, como o sucesso ou a falha de atualizações do pipeline. Consulte Adicionar notificações email para eventos pipeline .

[Adicionar notificações email para eventos pipeline](https://docs.databricks.com/pt/delta-live-tables/observability.html/#notifications)

Visualizando métricas para fontes de transmissão como Apache Kafka e Auto Loader (Public Preview). Ver view transmissão métricas.

[view transmissão métricas](https://docs.databricks.com/pt/delta-live-tables/observability.html/#streaming-observability)

Extração de informações detalhadas sobre as atualizações do site pipeline, como linhagem de dados, métricas de qualidade de dados e uso de recursos. Consulte O que é o registro de eventos do Delta Live Tables?

[O que é o registro de eventos do Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/observability.html/#event-log)

Definir ações personalizadas a serem executadas quando ocorrerem eventos específicos. Consulte Definir monitoramento personalizado de pipelines do Delta Live Tables com ganchos de eventos.

[Definir monitoramento personalizado de pipelines do Delta Live Tables com ganchos de eventos](https://docs.databricks.com/pt/delta-live-tables/observability.html/event-hooks.html)

Para inspecionar e diagnosticar o desempenho da consulta, consulte Acessar o histórico de consultas para o pipeline Delta Live Tables . Esse recurso está em Public Preview.

[Acessar o histórico de consultas para o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/observability.html/dlt-query-history.html)

## Adicionar notificações por e-mail para eventos de pipeline

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#add-email-notifications-for-pipeline-events)

O senhor pode configurar um ou mais endereços email para receber notificações quando ocorrer o seguinte:

A atualização do pipeline foi concluída com êxito.

Uma atualização de pipeline falha, seja com um erro que pode ser tentado ou não. Selecione essa opção para receber uma notificação de todas as falhas de pipeline.

Uma atualização de pipeline falha com um erro fatal (não recuperável). Selecione essa opção para receber uma notificação somente quando ocorrer um erro que não pode ser repetido.

Um único fluxo de dados falha.

Para configurar as notificações do email quando o senhor criar ou editar um pipeline:

[criar](https://docs.databricks.com/pt/delta-live-tables/observability.html/configure-pipeline.html)

Clique em Adicionar notificação.

Digite um ou mais endereços email para receber notificações.

Clique na caixa de seleção de cada tipo de notificação a ser enviada para os endereços email configurados.

Clique em Adicionar notificação.

## Quais detalhes do pipeline estão disponíveis na IU?

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#what-pipeline-details-are-available-in-the-ui)

O gráfico pipeline é exibido assim que uma atualização do site pipeline é iniciada com sucesso. As setas representam as dependências entre os conjuntos de dados em seu site pipeline. Em default, a página de detalhes pipeline mostra a atualização mais recente da tabela, mas o senhor pode selecionar atualizações mais antigas em um menu suspenso.

Os detalhes incluem o ID do pipeline, o código-fonte, o custo do compute, a edição do produto e o canal configurado para o pipeline.

Para ver uma tabular view do dataset, clique na Lista tab. A de lista view permite que você veja todos os dataset em seu pipeline representados como uma linha em uma tabela e é útil quando o DAG do pipeline é muito grande para ser visualizado na de gráfico view. Você pode controlar o dataset exibido na tabela usando vários filtros, como nome, tipo e status do dataset . Para voltar à visualização do DAG, clique em gráficos.

A execução como usuário é o proprietário do pipeline e o pipeline atualiza a execução com as permissões desse usuário. Para alterar o usuário run as , clique em Permissões e altere o proprietário do pipeline.

### Como você pode visualizar os detalhes do conjunto de dados?

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#how-can-you-view-dataset-details)

Clicar em um dataset no pipeline gráfico ou na lista dataset mostra detalhes sobre o dataset. Os detalhes incluem o esquema dataset, as métricas de qualidade de dados e um link para o código-fonte que define o dataset.

### Ver histórico de atualização

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#view-update-history)

Para view a história e o status das atualizações do pipeline, clique no menu suspenso atualizar história na barra superior.

Selecione a atualização no menu suspenso para view o gráfico, os detalhes e os eventos de uma atualização. Para retornar à atualização mais recente, clique em Mostrar a atualização mais recente.

## view transmissão métricas

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#view-streaming-metrics)

Prévia

A observabilidade da transmissão para Delta Live Tables está em Public Preview.

[Public Preview](https://docs.databricks.com/pt/delta-live-tables/observability.html/../release-notes/release-types.html)

O senhor pode view transmissão métricas da fonte de dados suportada pela Spark transmissão estruturada, como as tabelas Apache Kafka, Amazon Kinesis, Auto Loader e Delta, para cada fluxo de transmissão em sua Delta Live Tables pipeline. As métricas são exibidas como gráficos no painel direito da interface do usuário do Delta Live Tables e incluem segundos de atraso, bytes de atraso, registros de atraso e arquivos de atraso. Os gráficos exibem o valor máximo agregado por minuto e uma dica de ferramenta mostra os valores máximos quando você passa o mouse sobre o gráfico. Os dados são limitados às últimas 48 horas a partir da hora atual.

As tabelas em seu pipeline com transmissão métricas disponíveis exibem o ícone  ao visualizar o pipeline DAG na UI gráfica view. Para view a transmissão métrica, clique em  para exibir o gráfico de transmissão métrica em Flows tab no painel direito. O senhor também pode aplicar um filtro para view apenas tabelas com transmissão métricas clicando em List e, em seguida, em Has transmissão métricas.

![Delta Live Tables Ícone do gráfico](https://docs.databricks.com/pt/delta-live-tables/observability.html/../_images/dlt-chart-icon.png)

![Delta Live Tables Ícone do gráfico](https://docs.databricks.com/pt/delta-live-tables/observability.html/../_images/dlt-chart-icon.png)

Cada fonte de transmissão suporta apenas métricas específicas. As métricas não suportadas por uma fonte de transmissão não estão disponíveis para view na UI. A tabela a seguir mostra as métricas disponíveis para as fontes de transmissão suportadas:

| Origem | bytes da lista de pendências | registros de pendências | segundos de atraso | arquivos de lista de pendências |
| --- | --- | --- | --- | --- |
| Kafka | ✓ | ✓ |  |  |
| Kinesis | ✓ |  | ✓ |  |
| Delta | ✓ |  |  | ✓ |
| Auto Loader | ✓ |  |  | ✓ |
| Google Pub/Sub | ✓ | ✓ |  |  |


Origem

bytes da lista de pendências

registros de pendências

segundos de atraso

arquivos de lista de pendências

Kafka

✓

✓

Kinesis

✓

✓

Delta

✓

✓

Auto Loader

✓

✓

Google Pub/Sub

✓

✓

## O que são os logs de eventos do Delta Live Tables?

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#what-is-the-delta-live-tables-event-log)

O log de eventos Delta Live Tables contém todas as informações relacionadas a um pipeline, incluindo logs de auditoria, verificações de qualidade de dados, progresso do pipeline e linhagem de dados. Você pode usar os logs de eventos para rastrear, entender e monitorar o estado de seu pipeline de dados.

É possível acessar as entradas do evento view log na interface de usuário Delta Live Tables, no site Delta Live Tables APIou consultando diretamente o evento log. Esta seção se concentra na consulta direta ao log de eventos.

[API](https://docs.databricks.com/pt/delta-live-tables/observability.html/https://docs.databricks.com/api/workspace/pipelines)

Você também pode definir ações customizadas para execução quando eventos forem logs, por exemplo, envio de alerta, com event hooks.

[event hooks](https://docs.databricks.com/pt/delta-live-tables/observability.html/event-hooks.html)



## Esquema logs de eventos

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#event-log-schema)

A tabela a seguir descreve o esquema logs de eventos. Alguns desses campos contêm dados JSON que requerem análise para realizar alguma query, como o campo details. Databricks oferece suporte ao operador : para analisar campos JSON. Veja : (sinal de dois pontos) operador.

[: (sinal de dois pontos) operador](https://docs.databricks.com/pt/delta-live-tables/observability.html/../sql/language-manual/functions/colonsign.html)

| Campo | Descrição |
| --- | --- |
| id | Um identificador exclusivo para o registro logs de eventos. |
| sequence | Um documento JSON contendo metadados para identificar e ordenar eventos. |
| origin | Um documento JSON contendo metadados para a origem do evento, por exemplo, o provedor clouds , a região do provedor clouds ,user_id,pipeline_idoupipeline_typepara mostrar onde o pipeline foi criado,DBSQLouWORKSPACE. |
| timestamp | A hora em que o evento foi registrado. |
| message | Uma mensagem legível por humanos descrevendo o evento. |
| level | O tipo de evento, por exemplo,INFO,WARN,ERRORouMETRICS. |
| error | Se ocorreu um erro, detalhes descrevendo o erro. |
| details | Um documento JSON contendo detalhes estruturados do evento. Este é o campo principal usado para analisar eventos. |
| event_type | O tipo de evento. |
| maturity_level | A estabilidade do esquema de eventos. Os valores possíveis são:STABLE: O esquema é estável e não será alterado.NULL: O esquema é estável e não será alterado. O valor pode serNULLse o registro foi criado antes de o campomaturity_levelser adicionado (versão 2022.37).EVOLVING: O esquema não é estável e pode mudar.DEPRECATED: o esquema está obsoleto e o Delta Live Tables Runtime pode parar de produzir este evento a qualquer momento. |


Campo

Descrição

id

Um identificador exclusivo para o registro logs de eventos.

sequence

Um documento JSON contendo metadados para identificar e ordenar eventos.

origin

Um documento JSON contendo metadados para a origem do evento, por exemplo, o provedor clouds , a região do provedor clouds , user_id, pipeline_id ou pipeline_type para mostrar onde o pipeline foi criado, DBSQL ou WORKSPACE.

timestamp

A hora em que o evento foi registrado.

message

Uma mensagem legível por humanos descrevendo o evento.

level

O tipo de evento, por exemplo, INFO, WARN, ERROR ou METRICS.

error

Se ocorreu um erro, detalhes descrevendo o erro.

details

Um documento JSON contendo detalhes estruturados do evento. Este é o campo principal usado para analisar eventos.

event_type

O tipo de evento.

maturity_level

A estabilidade do esquema de eventos. Os valores possíveis são:

STABLE: O esquema é estável e não será alterado.

NULL: O esquema é estável e não será alterado. O valor pode ser NULL se o registro foi criado antes de o campo maturity_level ser adicionado (versão 2022.37).

[versão 2022.37](https://docs.databricks.com/pt/delta-live-tables/observability.html/../release-notes/delta-live-tables/2022/37/index.html)

EVOLVING: O esquema não é estável e pode mudar.

DEPRECATED: o esquema está obsoleto e o Delta Live Tables Runtime pode parar de produzir este evento a qualquer momento.

## Consultando os logsde eventos

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#querying-the-event-log)

A localização dos logs de eventos e a interface para query os logs de eventos dependem se o seu pipeline está configurado para usar o Hive metastore ou Unity Catalogs.

### Hive metastore

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#hive-metastore)

Se o seu pipeline publica tabelas no Hive metastore, o evento log é armazenado em /system/events no local storage. Por exemplo, se o senhor tiver configurado o pipeline storage como /Users/username/data, o log de eventos será armazenado no caminho /Users/username/data/system/events no DBFS.

[publica tabelas no Hive metastore](https://docs.databricks.com/pt/delta-live-tables/observability.html/hive-metastore.html)

Se você não configurou a configuração storage, o local default logs de eventos é /pipelines/<pipeline-id>/system/events no DBFS. Por exemplo, se o ID do pipeline for 91de5e48-35ed-11ec-8d3d-0242ac130003, o local de armazenamento será /pipelines/91de5e48-35ed-11ec-8d3d-0242ac130003/system/events.

Você pode criar uma view para simplificar a consulta dos logs de eventos. O exemplo a seguir cria uma view temporária chamada event_log_raw. Esta view é usada no exemplo query logs de eventos incluído nestes artigos:

Substitua <event-log-path> pelo local logs de eventos.

Cada instância de uma execução de pipeline é chamada de atualização. Muitas vezes você deseja extrair informações para a atualização mais recente. execute a query a seguir para localizar o identificador da atualização mais recente e salve-o na view temporária latest_update_id . Esta view é usada no exemplo query logs de eventos incluído nestes artigos:

Você pode query os logs in um Databricks Notebook ou no editor SQL. Use um Notebook ou o editor SQL para executar a query logs eventos de exemplo.

[editor SQL](https://docs.databricks.com/pt/delta-live-tables/observability.html/../sql/user/sql-editor/index.html)

### Unity Catalog

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#unity-catalog)

Se seu pipeline publica tabelas para Unity Catalogs, você deve usar a função de valor de tabela event_log (TVF) para buscar os logs de eventos para o pipeline. Você recupera os logs de eventos de um pipeline passando a ID do pipeline ou um nome de tabela para o TVF. Por exemplo, para recuperar os registros logs de eventos para o pipeline com ID 04c78631-3dd7-4856-b2a6-7d84e9b2638b:

[publica tabelas paraUnity Catalogs](https://docs.databricks.com/pt/delta-live-tables/observability.html/unity-catalog.html)

Para recuperar os registros logs de eventos para o pipeline que criou ou possui a tabela my_catalog.my_schema.table1:

Para chamar o TVF, você deve usar clusters compartilhados ou um armazém SQL. Por exemplo, você pode usar um Notebook anexado a clusters compartilhados ou usar o editor SQL conectado a um SQL warehouse.

[editor SQL](https://docs.databricks.com/pt/delta-live-tables/observability.html/../sql/user/sql-editor/index.html)

Para simplificar a consulta de eventos para um pipeline, o proprietário do pipeline pode criar uma view sobre o event_log TVF. O exemplo a seguir cria uma view dos logs de eventos de um pipeline. Essa view é usada na query logs de eventos de exemplo incluída neste artigo.

Observação

O TVF event_log pode ser chamado apenas pelo proprietário do pipeline e uma view criada sobre o TVF event_log pode ser query apenas pelo proprietário do pipeline. A view não pode ser compartilhada com outros usuários.

Substitua <pipeline-ID> pelo identificador exclusivo do pipeline Delta Live Tables. Você pode encontrar o ID no painel de detalhes do pipeline na IU do Delta Live Tables.

Cada instância de uma execução de pipeline é chamada de atualização. Muitas vezes você deseja extrair informações para a atualização mais recente. execute a query a seguir para localizar o identificador da atualização mais recente e salve-o na view temporária latest_update_id . Esta view é usada no exemplo query logs de eventos incluído nestes artigos:

## Consultar informações de linhagem dos logsde eventos

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#query-lineage-information-from-the-event-log)

Eventos contendo informações sobre linhagem possuem o tipo de evento flow_definition. O objeto details:flow_definition contém o output_dataset e input_datasets que definem cada relacionamento no gráfico.

Você pode usar a seguinte query para extrair o dataset de entrada e saída para ver a informação de linhagem:

| output_dataset | input_datasets |
| --- | --- |
| customers | null |
| sales_orders_raw | null |
| sales_orders_cleaned | ["customers","sales_orders_raw"] |
| sales_order_in_la | ["sales_orders_cleaned"] |


output_dataset

input_datasets

customers

null

sales_orders_raw

null

sales_orders_cleaned

["customers", "sales_orders_raw"]

sales_order_in_la

["sales_orders_cleaned"]

## Consultar a qualidade dos dados dos logsde eventos

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#query-data-quality-from-the-event-log)

Se você definir expectativas no dataset em seu pipeline, as métricas de qualidade de dados serão armazenadas no objeto details:flow_progress.data_quality.expectations. Eventos contendo informações sobre qualidade de dados possuem o tipo de evento flow_progress. O exemplo a seguir query as métricas de qualidade de dados para a última atualização do pipeline:

| dataset | expectation | passing_records | failing_records |
| --- | --- | --- | --- |
| sales_orders_cleaned | valid_order_number | 4083 | 0 |


dataset

expectation

passing_records

failing_records

sales_orders_cleaned

valid_order_number

4083

0

## Monitorelogs de dados de volta consultando os logsde eventos

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#monitor-data-backlog-by-querying-the-event-log)

Delta Live Tables rastreia quantos dados estão presentes no backlog no objeto details:flow_progress.metrics.backlog_bytes . Os eventos que contêm métricas de backlog têm o tipo de evento flow_progress. O exemplo a seguir query métricas de backlog para a última atualização do pipeline:

Observação

As métricas de backlog podem não estar disponíveis dependendo do tipo de fonte de dados do pipeline e da versão do Databricks Runtime.

## Monitorar eventos de autoescala aprimorados do evento log para pipeline sem serverless ativado

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#monitor-enhanced-autoscaling-events-from-the-event-log-for-pipelines-without-serverless-enabled)

Para o pipeline DLT que não usa serverless compute, o evento log captura cluster redimensiona quando a autoescala aprimorada está ativada em seu pipeline. Os eventos que contêm informações sobre a escala automática aprimorada têm o tipo de evento autoscale. As informações da solicitação de redimensionamento do cluster são armazenadas no objeto details:autoscale. O exemplo a seguir consulta as solicitações de redimensionamento do enhanced autoscale cluster para a última atualização do pipeline:

## Monitore a utilização de recursos de computação

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#monitor-compute-resource-utilization)

cluster_resources os eventos fornecem métricas sobre o número de slots de tarefa nos clusters, quanto esses slots de tarefa são utilizados e quantas tarefas estão esperando para serem agendadas.

Quando a escala automática aprimorada está ativada, os eventos cluster_resources também contêm métricas para o algoritmo de escala automática, incluindo latest_requested_num_executors e optimal_num_executors. Os eventos também mostram o status do algoritmo em diferentes estados, como CLUSTER_AT_DESIRED_SIZE, SCALE_UP_IN_PROGRESS_WAITING_FOR_EXECUTORS e BLOCKED_FROM_SCALING_DOWN_BY_CONFIGURATION. Essas informações podem ser visualizadas em conjunto com os eventos de autoescala para fornecer uma visão geral da autoescala aprimorada.

O exemplo a seguir query o histórico do tamanho da fila de tarefas para a última atualização do pipeline:

O exemplo a seguir query o histórico de utilização para a última atualização do pipeline:

O exemplo a seguir consulta o histórico de contagem do executor, acompanhado de métricas disponíveis somente para o pipeline de autoescala aprimorado, incluindo o número de executores solicitados pelo algoritmo na última solicitação, o número ideal de executores recomendados pelo algoritmo com base nas métricas mais recentes e o estado do algoritmo de autoescala:

## Auditar pipelines Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#audit-delta-live-tables-pipelines)

Você pode usar os registros de log de eventos do Delta Live Tables e outros logs de auditoria do Databricks para obter uma visão completa de como os dados estão sendo atualizados no Delta Live Tables.

Delta Live Tables usa as credenciais do proprietário do pipeline para atualizações de execução. Você pode alterar as credenciais usadas atualizando o proprietário do pipeline. Delta Live Tables registra o usuário para ações no pipeline, incluindo criação de pipeline, edições na configuração e atualizações de acionamento.

Consulte Eventos do Unity Catalog para obter uma referência dos eventos de auditoria do Unity Catalog.

[Eventos do Unity Catalog](https://docs.databricks.com/pt/delta-live-tables/observability.html/../admin/account-settings/audit-logs.html#uc)

## Consultar ações do usuário nos logsde eventos

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#query-user-actions-in-the-event-log)

Você pode usar os logs de eventos para auditar eventos, por exemplo, ações do usuário. Eventos contendo informações sobre ações do usuário possuem o tipo de evento user_action.

informações sobre a ação são armazenadas no objeto user_action no campo details . Use a query a seguir para construir logs de auditoria de eventos do usuário. Para criar a view event_log_raw usada nesta consulta, consulte Consultando os logsde eventos.

[Consultando os logsde eventos](https://docs.databricks.com/pt/delta-live-tables/observability.html/#query-event-log)

| timestamp | action | user_name |
| --- | --- | --- |
| 2021-05-20T19:36:03.517+0000 | START | user@company.com |
| 2021-05-20T19:35:59.913+0000 | CREATE | user@company.com |
| 2021-05-27T00:35:51.971+0000 | START | user@company.com |


timestamp

action

user_name

2021-05-20T19:36:03.517+0000

START

user@company.com

2021-05-20T19:35:59.913+0000

CREATE

user@company.com

2021-05-27T00:35:51.971+0000

START

user@company.com

## Informação Runtime

[](https://docs.databricks.com/pt/delta-live-tables/observability.html/#runtime-information)

Você pode view informações de tempo de execução para uma atualização de pipeline, por exemplo, a versão do Databricks Runtime para a atualização:

| dbr_version |
| --- |
| 11,0 |


dbr_version

11,0

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/observability.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/observability.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/observability.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/observability.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/observability.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/observability.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/observability.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/observability.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
