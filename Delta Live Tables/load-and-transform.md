[Documentação](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/index.html)

# Carga e transformação de dados com Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/#load-and-transform-data-with-delta-live-tables)

Os artigos desta seção fornecem padrões comuns, recomendações e exemplos de ingestão de dados e transformações no pipeline Delta Live Tables. Ao ingerir dados de origem para criar o conjunto de dados inicial em um pipeline, esses conjuntos de dados iniciais são comumente chamados de tabelas de bronze e geralmente realizam transformações simples. Por outro lado, as tabelas finais em um pipeline, comumente chamadas de tabelas de ouro, geralmente exigem agregações complicadas ou leitura de fontes que são alvos de uma APPLY CHANGES INTO operação.

## Carregar dados

[](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/#load-data)

O senhor pode carregar dados de qualquer fonte de dados suportada por Apache Spark em Databricks usando Delta Live Tables. Para obter exemplos de padrões para carregar dados de diferentes fontes, incluindo o armazenamento de objetos cloud, barramentos de mensagens como Kafka e sistemas externos como PostgreSQL, consulte Carregar dados com Delta Live Tables. Esses exemplos recorrem a recomendações como o uso de tabelas de transmissão com Auto Loader em Delta Live Tables para uma experiência de ingestão otimizada.

[Carregar dados com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/load.html)

## Fluxos de dados

[](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/#data-flows)

Em Delta Live Tables, um fluxo é uma consulta de transmissão que processa os dados de origem de forma incremental para atualizar uma tabela de transmissão de destino. Muitas consultas de transmissão necessárias para implementar um Delta Live Tables pipeline criam um fluxo implícito como parte da definição da consulta. O Delta Live Tables também suporta a declaração explícita de fluxos quando é necessário um processamento mais especializado. Para saber mais sobre os fluxos do site Delta Live Tables e ver exemplos de uso de fluxos para implementar a tarefa de processamento de dados, consulte Carregar e processar dados de forma incremental com os fluxos do site Delta Live Tables .

[Carregar e processar dados de forma incremental com os fluxos do site Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/flows.html)

## captura de dados de alterações (CDC) (CDC)

[](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/#change-data-capture-cdc)

Delta Live Tables simplifica a captura de dados de alterações (CDC) (CDC) com o APPLY CHANGES API. Ao tratar automaticamente os registros fora de sequência, a API APPLY CHANGES API em Delta Live Tables garante o processamento correto dos registros CDC e elimina a necessidade de desenvolver uma lógica complexa para tratar registros fora de sequência. Consulte a seção APPLY CHANGES APIs: Simplificar a captura de dados de alterações (CDC) com Delta Live Tables.

[APPLY CHANGES APIs: Simplificar a captura de dados de alterações (CDC) com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/cdc.html)

## transformação de dados

[](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/#transform-data)

Com o site Delta Live Tables, é possível declarar transformações no conjunto de dados e especificar como os registros são processados por meio da lógica de consulta. Para obter exemplos de padrões de transformações comuns ao criar o pipeline Delta Live Tables, incluindo o uso de tabelas de transmissão, visualização materializada, união estática de transmissão e modelos MLflow no pipeline, consulte transformação de dados com Delta Live Tables.

[transformação de dados com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/transform.html)

## Otimizar o processamento de estado em Delta Live Tables com marcas d'água

[](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/#optimize-stateful-processing-in-delta-live-tables-with-watermarks)

Para gerenciar efetivamente os dados mantidos no estado, o senhor pode usar marcas d'água ao executar o processamento de transmissão com estado em Delta Live Tables, incluindo agregações, junções e deduplicação. No processamento de transmissão, uma marca d'água é um Apache Spark recurso que pode definir um limite baseado em tempo para o processamento de dados ao realizar operações com estado. Os dados que chegam são processados até que o limite seja atingido e, nesse momento, a janela de tempo definida pelo limite é fechada. As marcas d'água podem ser usadas para evitar problemas durante o processamento de consultas, principalmente ao processar um conjunto de dados maior ou um processamento de longa duração.

Para obter exemplos e recomendações, consulte Otimizar o processamento com estado em Delta Live Tables com marcas d'água.

[Otimizar o processamento com estado em Delta Live Tables com marcas d'água](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/stateful-processing.html)



© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/load-and-transform.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
