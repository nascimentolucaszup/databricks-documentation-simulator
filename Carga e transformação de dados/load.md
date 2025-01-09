[Documentação](https://docs.databricks.com/pt/delta-live-tables/load.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/load.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/load.html/index.html)

[Carga e transformação de dados com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/load.html/load-and-transform.html)

# Carregar dados com Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/load.html/#load-data-with-delta-live-tables)

Você pode carregar dados de qualquer fonte de dados suportada pelo Apache Spark em Databricks usando Delta Live Tables. Você pode definir dataset (tabelas e view) em Delta Live Tables em qualquer query que retorne um Spark DataFrame, incluindo DataFrames e Pandas transmitidos para Spark DataFrames. Para tarefas de ingestão de dados, Databricks recomenda o uso de tabelas de transmissão para a maioria dos casos de uso. tabelas de transmissão são boas para ingerir dados do armazenamento de objetos cloud usando o Auto Loader ou de barramentos de mensagens como Kafka. Os exemplos abaixo demonstram alguns padrões comuns.

Importante

Nem todas as fontes de dados têm suporte a SQL. Você pode misturar SQL e Python Notebook em um pipeline Delta Live Tables para usar SQL para todas as operações além da ingestão.

Para obter detalhes sobre como trabalhar com biblioteca não pacote em Delta Live Tables por default, consulte gerenciar dependências de Python para o pipeline Delta Live Tables .

[gerenciar dependências de Python para o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/load.html/external-dependencies.html)

## Carregar arquivos do armazenamento de objetos na nuvem

[](https://docs.databricks.com/pt/delta-live-tables/load.html/#load-files-from-cloud-object-storage)

Databricks recomenda usar o Auto Loader com Delta Live Tables para a maioria das tarefas de ingestão de dados do armazenamento de objetos cloud . O Auto Loader e o Delta Live Tables são projetados para carregar de forma incremental e idempotente dados cada vez maiores à medida que chegam ao armazenamento em cloud . Os exemplos a seguir usam Auto Loader para criar dataset de arquivos CSV e JSON:

Observação

Para carregar arquivos com o Auto Loader em um pipeline habilitado para o Unity Catalog, o senhor deve usar locais externos. Para saber mais sobre o uso do Unity Catalog com o Delta Live Tables, consulte Use o Unity Catalog com o pipeline Delta Live Tables .

[locais externos](https://docs.databricks.com/pt/delta-live-tables/load.html/../connect/unity-catalog/cloud-storage/external-locations.html)

[Use o Unity Catalog com o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/load.html/unity-catalog.html)

Consulte O que é o Auto Loader? e Sintaxe SQL do Auto Loader.

[O que é o Auto Loader?](https://docs.databricks.com/pt/delta-live-tables/load.html/../ingestion/cloud-object-storage/auto-loader/index.html)

[Sintaxe SQL do Auto Loader](https://docs.databricks.com/pt/delta-live-tables/load.html/sql-ref.html#auto-loader-sql)

Aviso

Se o senhor usar Auto Loader com notificações de arquivo e executar um refresh completo para sua tabela pipeline ou de transmissão, deverá limpar manualmente o recurso. O senhor pode usar o CloudFilesResourceManager em um Notebook para realizar a limpeza.

[CloudFilesResourceManager](https://docs.databricks.com/pt/delta-live-tables/load.html/../ingestion/cloud-object-storage/auto-loader/file-notification-mode.html#cloud-resource-management)

## Carregar dados de um barramento de mensagem

[](https://docs.databricks.com/pt/delta-live-tables/load.html/#load-data-from-a-message-bus)

O senhor pode configurar o pipeline Delta Live Tables para ingerir dados de barramentos de mensagens com tabelas de transmissão. Databricks recomenda a combinação de tabelas de transmissão com execução contínua e autoescala aprimorada para fornecer a ingestão mais eficiente para o carregamento de baixa latência de barramentos de mensagens. Consulte Otimizar a utilização de cluster do pipeline Delta Live Tables com autoescala aprimorada.

[Otimizar a utilização de cluster do pipeline Delta Live Tables com autoescala aprimorada](https://docs.databricks.com/pt/delta-live-tables/load.html/auto-scaling.html)

Por exemplo, o código a seguir configura uma tabela transmitida para ingerir dados do Kafka:

Você pode escrever operações downstream em SQL puro para realizar transformações transmitidas nesses dados, como no exemplo a seguir:

Para obter um exemplo de como trabalhar com os Hubs de Eventos, consulte Usar os Hubs de Eventos do Azure como uma fonte de dados Delta Live Tables.

[Usar os Hubs de Eventos do Azure como uma fonte de dados Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/load.html/event-hubs.html)

Consulte Configurar transmissão de fonte de dados.

[Configurar transmissão de fonte de dados](https://docs.databricks.com/pt/delta-live-tables/load.html/../connect/streaming/index.html)

## Carregar dados de sistemas externos

[](https://docs.databricks.com/pt/delta-live-tables/load.html/#load-data-from-external-systems)

Delta Live Tables suporta o carregamento de dados de qualquer fonte de dados suportada pelo site Databricks. Consulte Conectar-se à fonte de dados. O senhor também pode carregar o uso externo de dados lakehouse Federation para fontes de dados compatíveis. Como o lakehouse Federation requer o Databricks Runtime 13.3 LTS ou acima, para usar o lakehouse Federation, o pipeline deve estar configurado para usar o canal de visualização.

[Conectar-se à fonte de dados](https://docs.databricks.com/pt/delta-live-tables/load.html/../connect/index.html)

[fontes de dados compatíveis](https://docs.databricks.com/pt/delta-live-tables/load.html/../query-federation/index.html#connection-types)

[canal de visualização](https://docs.databricks.com/pt/delta-live-tables/load.html/properties.html#config-settings)

Algumas fontes de dados não têm suporte equivalente em SQL. Se o senhor não puder usar a Lakehouse Federation com uma dessas fontes de dados, poderá usar um notebook Python para ingerir dados da fonte. O senhor pode adicionar código-fonte Python e SQL ao mesmo pipeline do Delta Live Tables. O exemplo a seguir declara um view materializado para acessar o estado atual dos dados em uma tabela PostgreSQL remota:

## Carregue conjuntos de dados pequenos ou estáticos do armazenamento de objetos na nuvem

[](https://docs.databricks.com/pt/delta-live-tables/load.html/#load-small-or-static-datasets-from-cloud-object-storage)

Você pode carregar dataset pequeno ou estático usando a sintaxe de carregamento do Apache Spark. Delta Live Tables suporta todos os formatos de arquivo suportados pelo Apache Spark no Databricks. Para obter uma lista completa, consulte Opções de formato de dados.

[Opções de formato de dados](https://docs.databricks.com/pt/delta-live-tables/load.html/../query/formats/index.html)

Os exemplos a seguir demonstram o carregamento de JSON para criar tabelas Delta Live Tables:

Observação

A construção SQL SELECT * FROM format.`path`; é comum a todos os ambientes SQL no Databricks. É o padrão recomendado para acesso direto a arquivos usando SQL com Delta Live Tables.

## Acesse com segurança credenciais de armazenamento com segredos em um pipeline

[](https://docs.databricks.com/pt/delta-live-tables/load.html/#securely-access-storage-credentials-with-secrets-in-a-pipeline)

O Databricks senhor pode usar os segredos do para armazenar credenciais, como chaves de acesso ou senhas. Para configurar o segredo em seu pipeline, use uma propriedade do Spark na configuração do cluster de configurações do pipeline. Consulte Configurar computação para um pipeline do Delta Live Tables.

[senhor](https://docs.databricks.com/pt/delta-live-tables/load.html/../security/secrets/index.html)

[Configurar computação para um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/load.html/configure-compute.html)

O exemplo a seguir usa um segredo para armazenar um acesso key necessário para ler dados de entrada de um armazenamento Azure Data Lake Storage Gen2 (ADLS Gen2) account usando Auto Loader. O senhor pode usar esse mesmo método para configurar qualquer segredo exigido pelo seu pipeline, por exemplo, a chave AWS para acessar S3, ou a senha para um Apache Hive metastore.

[Auto Loader](https://docs.databricks.com/pt/delta-live-tables/load.html/../ingestion/cloud-object-storage/auto-loader/index.html)

Para saber mais sobre como trabalhar com o Azure Data Lake Storage Gen2, consulte Conectar-se ao Azure Data Lake Storage Gen2 e ao Blob Storage.

[Conectar-se ao Azure Data Lake Storage Gen2 e ao Blob Storage](https://docs.databricks.com/pt/delta-live-tables/load.html/../connect/storage/azure-storage.html)

Observação

Você deve adicionar o prefixo spark.hadoop. à key de configuração spark_conf que define o valor do segredo.

Substituir

<storage-account-name> com o nome account de armazenamento ADLS Gen2.

<scope-name> com o nome do Databricks Secret Scope .

<secret-name> com o nome da key que contém a key acesso da account de armazenamento do Azure.

Substituir

<container-name> com o nome do contêiner account de armazenamento do Azure que armazena os dados de entrada.

<storage-account-name> com o nome account de armazenamento ADLS Gen2.

<path-to-input-dataset> com o caminho para o dataset de entrada.

## Carregar dados dos Hubs de Eventos do Azure

[](https://docs.databricks.com/pt/delta-live-tables/load.html/#load-data-from-azure-event-hubs)

Azure O Event Hubs é um serviço de transmissão de dados que oferece uma interface compatível com Apache Kafka . O senhor pode usar o conector de transmissão estruturada Kafka, incluído no tempo de execução Delta Live Tables, para carregar mensagens de Azure Event Hubs. Para saber mais sobre como carregar e processar mensagens de Azure Event Hubs, consulte Use Azure Event Hubs as a Delta Live Tables  fonte de dados.

[Use Azure Event Hubs as a Delta Live Tables  fonte de dados](https://docs.databricks.com/pt/delta-live-tables/load.html/event-hubs.html)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/load.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/load.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/load.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/load.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/load.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/load.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/load.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/load.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
