[Documentação](https://docs.databricks.com/pt/delta-live-tables/properties.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/properties.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/properties.html/index.html)

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/properties.html/configure-pipeline.html)

# Referência de propriedades do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/properties.html/#delta-live-tables-properties-reference)

Este artigo fornece uma referência para a especificação de configuração JSON do Delta Live Tables e propriedades da tabela no Databricks. Para obter mais detalhes sobre como usar essas várias propriedades e configurações, consulte os seguintes artigos:

Configurar um pipeline do Delta Live Tables

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/properties.html/configure-pipeline.html)

pipeline REST API

[pipeline REST API](https://docs.databricks.com/pt/delta-live-tables/properties.html/https://docs.databricks.com/api/workspace/pipelines)

## Configurações de pipeline do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/properties.html/#delta-live-tables-pipeline-configurations)

| Campos |
| --- |
| idTipo:stringUm identificador globalmente exclusivo para este pipeline. O identificador é atribuído pelo sistema e não pode ser alterado. |
| nameTipo:stringUm nome amigável para este pipeline. O nome pode ser usado para identificar Job do pipeline na interface do usuário. |
| storageTipo:stringUm local no DBFS ou armazenamento cloud onde os dados de saída e os metadados necessários para a execução do pipeline são armazenados. Tabelas e metadados são armazenados em subdiretórios deste local.Quando a configuraçãostoragenão for especificada, o sistema assumirá default um local emdbfs:/pipelines/.A configuraçãostoragenão pode ser alterada após a criação de um pipeline. |
| configurationTipo:objectUma lista opcional de configurações para adicionar à configuração do Spark dos clusters que executarão o pipeline. Essas configurações são lidas pelo Delta Live Tables Runtime e disponíveis para query de pipeline por meio da configuração do Spark.Os elementos devem ser formatados como pareskey:value. |
| librariesTipo:arrayofobjectsUma matriz de Notebook contendo o código do pipeline e os artefatos necessários. |
| clustersTipo:arrayofobjectsUma matriz de especificações para os clusters para execução do pipeline.Se isso não for especificado, os pipelines selecionarão automaticamente uma configuração clusters default para o pipeline. |
| developmentTipo:booleanUm sinalizador que indica se o pipeline deve ser executado no mododevelopmentouproduction.O valor default étrue |
| notificationsTipo:arrayofobjectsUma matriz opcional de especificações para notificações por email quando uma atualização de pipeline é concluída, falha com um erro que pode ser repetido, falha com um erro que não pode ser repetido ou um fluxo falha. |
| continuousTipo:booleanUm sinalizador que indica se o pipeline deve ser executado continuamente.O valor default éfalse. |
| targetTipo:stringO nome de um banco de dados para dados de saída de pipeline persistentes. Definir a configuraçãotargetpermite view e query os dados de saída do pipeline da interface do usuário do Databricks. |
| channelTipo:stringA versão do Delta Live Tables Runtime a ser usada. Os valores suportados são:previewpara testar seu pipeline com as próximas alterações na versão Runtime .currentpara usar a versão atual Runtime .O campochannelé opcional. O valor default écurrent. Databricks recomenda usar a versão atual Runtime para cargas de trabalho de produção. |
| editionTipostringA edição do produto Delta Live Tables para execução do pipeline. Essa configuração permite escolher a melhor edição do produto com base nos requisitos do seu pipeline:COREpara execução de transmissão de ingestão de cargas de trabalho.PROpara execução transmissão ingestão e captura de dados de alterações (CDC) (CDC) workloads.ADVANCEDcargas de trabalho de ingestão de transmissão de execução, cargas de trabalho de CDC e cargas de trabalho que exigem expectativas Delta Live Tables para impor restrições de qualidade de dados.O campoeditioné opcional. O valor default éADVANCED. |
| photonTipo:booleanUm sinalizador indicando se deve ser usadoWhat is Photon?para executar o pipeline. Photon é o mecanismo Spark de alto desempenho do Databricks. pipeline habilitados para Photon são cobrados a uma taxa diferente dos pipeline não-Photon.O campophotoné opcional. O valor default éfalse. |
| pipelines.maxFlowRetryAttemptsTipo:intSe ocorrer uma falha tentável durante uma atualização do pipeline, esse é o número máximo de vezes para tentar novamente um fluxo antes de falhar na atualização do pipelinepadrão: Duas tentativas de repetição. Quando ocorre uma falha de repetição, o tempo de execução do Delta Live Tables tenta executar o fluxo três vezes, incluindo a tentativa original. |
| pipelines.numUpdateRetryAttemptsTipo:intSe ocorrer uma falha que pode ser repetida durante uma atualização, esse é o número máximo de vezes para tentar novamente a atualização antes de falhar permanentemente na atualização. A nova tentativa é executada como uma atualização completa.Esse parâmetro se aplica somente ao pipeline em execução no modo de produção. Não há tentativas de novas tentativas se o site pipeline for executado no modo de desenvolvimento ou quando o senhor executar uma atualizaçãoValidate.default:Cinco para o pipeline acionado.Ilimitado para pipeline contínuo. |


Campos

id

Tipo: string

Um identificador globalmente exclusivo para este pipeline. O identificador é atribuído pelo sistema e não pode ser alterado.

name

Tipo: string

Um nome amigável para este pipeline. O nome pode ser usado para identificar Job do pipeline na interface do usuário.

storage

Tipo: string

Um local no DBFS ou armazenamento cloud onde os dados de saída e os metadados necessários para a execução do pipeline são armazenados. Tabelas e metadados são armazenados em subdiretórios deste local.

Quando a configuração storage não for especificada, o sistema assumirá default um local em dbfs:/pipelines/.

A configuração storage não pode ser alterada após a criação de um pipeline.

configuration

Tipo: object

Uma lista opcional de configurações para adicionar à configuração do Spark dos clusters que executarão o pipeline. Essas configurações são lidas pelo Delta Live Tables Runtime e disponíveis para query de pipeline por meio da configuração do Spark.

Os elementos devem ser formatados como pares key:value .

libraries

Tipo: array of objects

Uma matriz de Notebook contendo o código do pipeline e os artefatos necessários.

clusters

Tipo: array of objects

Uma matriz de especificações para os clusters para execução do pipeline.

Se isso não for especificado, os pipelines selecionarão automaticamente uma configuração clusters default para o pipeline.

development

Tipo: boolean

Um sinalizador que indica se o pipeline deve ser executado no modo development ou production .

O valor default é true

notifications

Tipo: array of objects

Uma matriz opcional de especificações para notificações por email quando uma atualização de pipeline é concluída, falha com um erro que pode ser repetido, falha com um erro que não pode ser repetido ou um fluxo falha.

continuous

Tipo: boolean

Um sinalizador que indica se o pipeline deve ser executado continuamente.

O valor default é false.

target

Tipo: string

O nome de um banco de dados para dados de saída de pipeline persistentes. Definir a configuração target permite view e query os dados de saída do pipeline da interface do usuário do Databricks.

channel

Tipo: string

A versão do Delta Live Tables Runtime a ser usada. Os valores suportados são:

preview para testar seu pipeline com as próximas alterações na versão Runtime .

current para usar a versão atual Runtime .

O campo channel é opcional. O valor default é current. Databricks recomenda usar a versão atual Runtime para cargas de trabalho de produção.

edition

Tipo string

A edição do produto Delta Live Tables para execução do pipeline. Essa configuração permite escolher a melhor edição do produto com base nos requisitos do seu pipeline:

CORE para execução de transmissão de ingestão de cargas de trabalho.

PRO para execução transmissão ingestão e captura de dados de alterações (CDC) (CDC) workloads.

ADVANCED cargas de trabalho de ingestão de transmissão de execução, cargas de trabalho de CDC e cargas de trabalho que exigem expectativas Delta Live Tables para impor restrições de qualidade de dados.

O campo edition é opcional. O valor default é ADVANCED.

photon

Tipo: boolean

Um sinalizador indicando se deve ser usado What is Photon? para executar o pipeline. Photon é o mecanismo Spark de alto desempenho do Databricks. pipeline habilitados para Photon são cobrados a uma taxa diferente dos pipeline não-Photon.

[What is Photon?](https://docs.databricks.com/pt/delta-live-tables/properties.html/../compute/photon.html)

O campo photon é opcional. O valor default é false.

pipelines.maxFlowRetryAttempts

Tipo: int

Se ocorrer uma falha tentável durante uma atualização do pipeline, esse é o número máximo de vezes para tentar novamente um fluxo antes de falhar na atualização do pipeline

padrão: Duas tentativas de repetição. Quando ocorre uma falha de repetição, o tempo de execução do Delta Live Tables tenta executar o fluxo três vezes, incluindo a tentativa original.

pipelines.numUpdateRetryAttempts

Tipo: int

Se ocorrer uma falha que pode ser repetida durante uma atualização, esse é o número máximo de vezes para tentar novamente a atualização antes de falhar permanentemente na atualização. A nova tentativa é executada como uma atualização completa.

Esse parâmetro se aplica somente ao pipeline em execução no modo de produção. Não há tentativas de novas tentativas se o site pipeline for executado no modo de desenvolvimento ou quando o senhor executar uma atualização Validate.

default:

Cinco para o pipeline acionado.

Ilimitado para pipeline contínuo.

## Propriedades da tabela Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/properties.html/#delta-live-tables-table-properties)

Além das propriedades da tabela suportadas pelo Delta Lake, você pode definir as seguintes propriedades da tabela.

[Delta Lake](https://docs.databricks.com/pt/delta-live-tables/properties.html/../delta/table-properties.html)

| Propriedades da tabela |
| --- |
| pipelines.autoOptimize.manageddefault:trueAtiva ou desativa a otimização agendada automaticamente desta tabela. |
| pipelines.autoOptimize.zOrderColsdefault: nenhumUma strings opcional contendo uma lista separada por vírgulas de nomes de coluna para esta tabela em Z-order. Por exemplo,pipelines.autoOptimize.zOrderCols="year,month" |
| pipelines.reset.alloweddefault:trueControla se uma refresh completa é permitida para esta tabela. |


Propriedades da tabela

pipelines.autoOptimize.managed

default: true

Ativa ou desativa a otimização agendada automaticamente desta tabela.

pipelines.autoOptimize.zOrderCols

default: nenhum

Uma strings opcional contendo uma lista separada por vírgulas de nomes de coluna para esta tabela em Z-order. Por exemplo, pipelines.autoOptimize.zOrderCols = "year,month"

pipelines.reset.allowed

default: true

Controla se uma refresh completa é permitida para esta tabela.

## Intervalo de acionamento de pipelines

[](https://docs.databricks.com/pt/delta-live-tables/properties.html/#pipelines-trigger-interval)

O senhor pode especificar um intervalo de acionamento pipeline para todo o Delta Live Tables pipeline ou como parte de uma declaração dataset. Consulte Definir intervalo de acionamento para pipelines contínuos.

[Definir intervalo de acionamento para pipelines contínuos](https://docs.databricks.com/pt/delta-live-tables/properties.html/pipeline-mode.html#trigger-interval)

| pipelines.trigger.interval |
| --- |
| O default é baseado no tipo de fluxo:Cinco segundos para query de transmissão.Um minuto para query completa quando todos os dados de entrada são de fontes Delta.Dez minutos para query completa quando alguma fonte de dados pode não ser Delta.O valor é um número mais a unidade de tempo. A seguir estão as unidades de tempo válidas:second,secondsminute,minuteshour,hoursday,daysVocê pode usar a unidade singular ou plural ao definir o valor, por exemplo:{"pipelines.trigger.interval":"1hour"}{"pipelines.trigger.interval":"10seconds"}{"pipelines.trigger.interval":"30second"}{"pipelines.trigger.interval":"1minute"}{"pipelines.trigger.interval":"10minutes"}{"pipelines.trigger.interval":"10minute"} |


pipelines.trigger.interval

O default é baseado no tipo de fluxo:

Cinco segundos para query de transmissão.

Um minuto para query completa quando todos os dados de entrada são de fontes Delta.

Dez minutos para query completa quando alguma fonte de dados pode não ser Delta.

O valor é um número mais a unidade de tempo. A seguir estão as unidades de tempo válidas:

second, seconds

minute, minutes

hour, hours

day, days

Você pode usar a unidade singular ou plural ao definir o valor, por exemplo:

{"pipelines.trigger.interval" : "1 hour"}

{"pipelines.trigger.interval" : "10 seconds"}

{"pipelines.trigger.interval" : "30 second"}

{"pipelines.trigger.interval" : "1 minute"}

{"pipelines.trigger.interval" : "10 minutes"}

{"pipelines.trigger.interval" : "10 minute"}

## atributos clusters que não são configuráveis pelo usuário

[](https://docs.databricks.com/pt/delta-live-tables/properties.html/#cluster-attributes-that-are-not-user-settable)

Como o Delta Live Tables gerencia os ciclos de vida dos clusters, muitas configurações de clusters são definidas pelo Delta Live Tables e não podem ser configuradas manualmente pelos usuários, seja em uma configuração de pipeline ou em uma política de cluster usada por um pipeline. A tabela a seguir lista essas configurações e por que elas não podem ser definidas manualmente.

| Campos |
| --- |
| cluster_nameDelta Live Tables define os nomes dos clusters usados para atualizações de pipeline de execução. Esses nomes não podem ser substituídos. |
| data_security_modeaccess_modeEsses valores são definidos automaticamente pelo sistema. |
| spark_versionExecução de clusters Delta Live Tables em uma versão personalizada do Databricks Runtime que é continuamente atualizada para incluir os recursos mais recentes. A versão do Spark é fornecida com a versão do Databricks Runtime e não pode ser substituída. |
| autotermination_minutesComo o Delta Live Tables gerencia a lógica de reutilização e encerramento automático clusters , o tempo de encerramento automático clusters não pode ser substituído. |
| runtime_engineEmbora você possa controlar esse campo habilitando Photon para seu pipeline, não é possível definir esse valor diretamente. |
| effective_spark_versionEste valor é definido automaticamente pelo sistema. |
| cluster_sourceEste campo é definido pelo sistema e é somente leitura. |
| docker_imageComo o Delta Live Tables gerencia o ciclo de vida do cluster, você não pode usar um contêiner personalizado com clusters de pipeline. |
| workload_typeEste valor é definido pelo sistema e não pode ser substituído. |


Campos

cluster_name

Delta Live Tables define os nomes dos clusters usados para atualizações de pipeline de execução. Esses nomes não podem ser substituídos.

data_security_mode access_mode

Esses valores são definidos automaticamente pelo sistema.

spark_version

Execução de clusters Delta Live Tables em uma versão personalizada do Databricks Runtime que é continuamente atualizada para incluir os recursos mais recentes. A versão do Spark é fornecida com a versão do Databricks Runtime e não pode ser substituída.

autotermination_minutes

Como o Delta Live Tables gerencia a lógica de reutilização e encerramento automático clusters , o tempo de encerramento automático clusters não pode ser substituído.

runtime_engine

Embora você possa controlar esse campo habilitando Photon para seu pipeline, não é possível definir esse valor diretamente.

effective_spark_version

Este valor é definido automaticamente pelo sistema.

cluster_source

Este campo é definido pelo sistema e é somente leitura.

docker_image

Como o Delta Live Tables gerencia o ciclo de vida do cluster, você não pode usar um contêiner personalizado com clusters de pipeline.

workload_type

Este valor é definido pelo sistema e não pode ser substituído.

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/properties.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/properties.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/properties.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/properties.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/properties.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/properties.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/properties.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/properties.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
