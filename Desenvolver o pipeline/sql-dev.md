[Documentação](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/index.html)

[Desenvolver o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/develop-pipelines.html)

# Desenvolver código de pipeline com SQL

[](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/#develop-pipeline-code-with-sql)

Delta Live Tables introduz várias novas palavras-chave e funções no site SQL para definir a visualização materializada e as tabelas de transmissão no pipeline. SQL O suporte ao desenvolvimento de pipeline se baseia nos conceitos básicos do site Spark SQL e adiciona suporte à funcionalidade de transmissão estruturada.

Os usuários familiarizados com o PySpark DataFrames podem preferir desenvolver o código do pipeline com Python. O Python oferece suporte a testes e operações mais abrangentes que são difíceis de implementar com o SQL, como operações de metaprogramação. Consulte Desenvolver código de pipeline com Python.

[Desenvolver código de pipeline com Python](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/python-dev.html)

Para obter uma referência completa da sintaxe SQL do Delta Live Tables, consulte Referência da linguagem SQL do Delta Live Tables.

[Referência da linguagem SQL do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/sql-ref.html)

## Noções básicas de SQL para desenvolvimento de pipeline

[](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/#basics-of-sql-for-pipeline-development)

SQL O código que cria o conjunto de dados Delta Live Tables usa a sintaxe CREATE OR REFRESH para definir a visualização materializada e as tabelas de transmissão em relação aos resultados da consulta.

A palavra-chave STREAM indica se a fonte de dados referenciada em uma cláusula SELECT deve ser lida com a semântica de transmissão.

Delta Live Tables O código-fonte difere criticamente dos scripts do SQL: o Delta Live Tables avalia todas as definições do dataset em todos os arquivos de código-fonte configurados em um pipeline e cria um gráfico de fluxo de dados antes da execução de qualquer consulta. A ordem das consultas que aparecem em um Notebook ou script não define a ordem de execução.

## Criar uma visualização materializada com SQL

[](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/#create-a-materialized-view-with-sql)

O exemplo de código a seguir demonstra a sintaxe básica para criar um view materializado com SQL:

## Criar uma tabela de transmissão com SQL

[](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/#create-a-streaming-table-with-sql)

O exemplo de código a seguir demonstra a sintaxe básica para criar uma tabela de transmissão com SQL:

Observação

Nem todas as fontes de dados suportam leituras de transmissão, e algumas fontes de dados devem sempre ser processadas com a semântica de transmissão.

## Carregar dados do armazenamento de objetos

[](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/#load-data-from-object-storage)

O Delta Live Tables suporta o carregamento de dados de todos os formatos suportados pela Databricks. Consulte Opções de formato de dados.

[Opções de formato de dados](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/../query/formats/index.html)

Observação

Esses exemplos usam dados disponíveis no /databricks-datasets montado automaticamente em seu site workspace. Databricks recomenda o uso de caminhos de volume ou URIs cloud para fazer referência aos dados armazenados no armazenamento de objetos cloud. Consulte O que são volumes do Unity Catalog?

[O que são volumes do Unity Catalog?](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/../volumes/index.html)

Databricks recomenda o uso das tabelas Auto Loader e transmissão ao configurar cargas de trabalho de ingestão incremental em relação aos dados armazenados no armazenamento de objetos cloud. Consulte O que é o Auto Loader?

[O que é o Auto Loader?](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/../ingestion/cloud-object-storage/auto-loader/index.html)

O SQL usa a função read_files para invocar a funcionalidade do Auto Loader. O senhor também deve usar a palavra-chave STREAM para configurar uma transmissão lida com read_files.

O exemplo a seguir cria uma tabela de transmissão a partir dos arquivos JSON usando Auto Loader:

A função read_files também é compatível com a semântica de lotes para criar uma visualização materializada. O exemplo a seguir usa a semântica de lotes para ler um diretório JSON e criar um view materializado:

## Valide os dados de acordo com as expectativas

[](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/#validate-data-with-expectations)

Você pode usar as expectativas para definir e aplicar restrições de qualidade de dados. Veja como gerenciar a qualidade dos dados com Delta Live Tables.

[como gerenciar a qualidade dos dados com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/expectations.html)

O código a seguir define uma expectativa chamada valid_data que descarta registros nulos durante a ingestão de dados:

## Consultar a visualização materializada e as tabelas de transmissão definidas em seu pipeline

[](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/#query-materialized-views-and-streaming-tables-defined-in-your-pipeline)

Use o esquema LIVE para consultar outras visualizações materializadas e tabelas de transmissão definidas em seu site pipeline.

O exemplo a seguir define quatro conjuntos de dados:

Uma tabela de transmissão denominada orders que carrega dados do site JSON.

Um view materializado chamado customers que carrega os dados do CSV.

Um view materializado chamado customer_orders que une registros dos conjuntos de dados orders e customers, converte o carimbo de data/hora da ordem em uma data e seleciona os campos customer_id, order_number, state e order_date.

Um view materializado chamado daily_orders_by_state que agrega a contagem diária de pedidos para cada estado.

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/sql-dev.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
