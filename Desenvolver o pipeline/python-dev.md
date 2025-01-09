[Documentação](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/index.html)

[Desenvolver o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/develop-pipelines.html)

# Desenvolver código de pipeline com Python

[](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/#develop-pipeline-code-with-python)

Delta Live Tables introduz várias novas construções de código Python para definir a visualização materializada e as tabelas de transmissão no pipeline. Python o suporte para o desenvolvimento de pipeline baseia-se nos fundamentos de PySpark DataFrame e transmissão estruturada APIs.

Para usuários não familiarizados com Python e DataFrames, a Databricks recomenda o uso da interface SQL. Consulte Desenvolver código de pipeline com SQL.

[Desenvolver código de pipeline com SQL](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/sql-dev.html)

Para obter uma referência completa da sintaxe Python do Delta Live Tables, consulte Referência da linguagem Python do Delta Live Tables.

[Referência da linguagem Python do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/python-ref.html)

## Noções básicas de Python para desenvolvimento de pipeline

[](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/#basics-of-python-for-pipeline-development)

Python O código que cria o conjunto de dados Delta Live Tables deve retornar DataFrames.

Todas as APIs Python do Delta Live Tables são implementadas no módulo dlt. Seu código Delta Live Tables pipeline implementado com Python deve importar explicitamente o módulo dlt na parte superior do Python Notebook e dos arquivos.

Delta Live TablesO código Python específico difere de outros tipos de código Python de uma maneira crítica: o código Python pipeline não chama diretamente as funções que realizam a ingestão de dados e transformações para criar o conjunto de dados Delta Live Tables. Em vez disso, o Delta Live Tables interpreta as funções de decoração do módulo dlt em todos os arquivos de código-fonte configurados em um pipeline e cria um gráfico de fluxo de dados.

Importante

Para evitar um comportamento inesperado na execução do pipeline, não inclua código que possa ter efeitos colaterais nas funções que definem o conjunto de dados. Para saber mais, consulte a referência do Python.

[referência do Python](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/python-ref.html#considerations)

## Crie uma tabela materializada view ou de transmissão com Python

[](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/#create-a-materialized-view-or-streaming-table-with-python)

O decorador @dlt.table informa ao site Delta Live Tables para criar uma tabela materializada view ou de transmissão com base nos resultados retornados por uma função. Os resultados de uma leitura de lotes criam uma tabela materializada view, enquanto os resultados de uma leitura de transmissão criam uma tabela de transmissão.

Em default, os nomes das tabelas materializadas view e de transmissão são inferidos a partir dos nomes das funções. O exemplo de código a seguir mostra a sintaxe básica para a criação de uma tabela materializada view e de transmissão:

Observação

Ambas as funções fazem referência à mesma tabela no catálogo samples e usam a mesma função decoradora. Esses exemplos destacam que a única diferença na sintaxe básica da visualização materializada e das tabelas de transmissão é usar spark.read em vez de spark.readStream.

Nem todas as fontes de dados suportam leituras de transmissão. Algumas fontes de dados devem sempre ser processadas com a semântica de transmissão.



Opcionalmente, você pode especificar o nome da tabela usando o argumento name no decorador @dlt.table. O exemplo a seguir demonstra esse padrão para uma tabela materializada view e transmissão:

## Carregar dados do armazenamento de objetos

[](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/#load-data-from-object-storage)

O Delta Live Tables suporta o carregamento de dados de todos os formatos suportados pela Databricks. Consulte Opções de formato de dados.

[Opções de formato de dados](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/../query/formats/index.html)

Observação

Esses exemplos usam dados disponíveis no /databricks-datasets montado automaticamente em seu site workspace. Databricks recomenda o uso de caminhos de volume ou URIs cloud para fazer referência aos dados armazenados no armazenamento de objetos cloud. Consulte O que são volumes do Unity Catalog?

[O que são volumes do Unity Catalog?](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/../volumes/index.html)

Databricks recomenda o uso das tabelas Auto Loader e transmissão ao configurar cargas de trabalho de ingestão incremental em relação aos dados armazenados no armazenamento de objetos cloud. Consulte O que é o Auto Loader?

[O que é o Auto Loader?](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/../ingestion/cloud-object-storage/auto-loader/index.html)

O exemplo a seguir cria uma tabela de transmissão a partir dos arquivos JSON usando Auto Loader:

O exemplo a seguir usa a semântica de lotes para ler um diretório JSON e criar um view materializado:

## Valide os dados de acordo com as expectativas

[](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/#validate-data-with-expectations)

Você pode usar as expectativas para definir e aplicar restrições de qualidade de dados. Veja como gerenciar a qualidade dos dados com Delta Live Tables.

[como gerenciar a qualidade dos dados com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/expectations.html)

O código a seguir usa @dlt.expect_or_drop para definir uma expectativa chamada valid_data que descarta registros nulos durante a ingestão de dados:

## Consultar a visualização materializada e as tabelas de transmissão definidas em seu pipeline

[](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/#query-materialized-views-and-streaming-tables-defined-in-your-pipeline)

Use o esquema LIVE para consultar outras visualizações materializadas e tabelas de transmissão definidas em seu site pipeline.

O exemplo a seguir define quatro conjuntos de dados:

Uma tabela de transmissão denominada orders que carrega dados do site JSON.

Um view materializado chamado customers que carrega os dados do CSV.

Um view materializado chamado customer_orders que une registros dos conjuntos de dados orders e customers, converte o carimbo de data/hora do pedido em uma data e seleciona os campos customer_id, order_number, state e order_date.

Um view materializado chamado daily_orders_by_state que agrega a contagem diária de pedidos para cada estado.

## Crie tabelas em um loop for

[](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/#create-tables-in-a-for-loop)

O senhor pode usar o Python for loops para criar várias tabelas de forma programática. Isso pode ser útil quando o senhor tem muitas fontes de dados ou conjuntos de dados de destino que variam em apenas alguns parâmetros, resultando em menos código total para manter e menos redundância de código.

O loop for avalia a lógica em ordem serial, mas, uma vez concluído o planejamento do conjunto de dados, o pipeline executa a lógica em paralelo.

Importante

Ao usar esse padrão para definir o conjunto de dados, certifique-se de que a lista de valores passada para o loop for seja sempre aditiva. Se um dataset previamente definido em um pipeline for omitido de uma futura execução do pipeline, esse dataset será descartado automaticamente do esquema de destino.

O exemplo a seguir cria cinco tabelas que filtram os pedidos dos clientes por região. Aqui, o nome da região é usado para definir o nome da visualização materializada de destino e para filtrar os dados de origem. A visualização temporária é usada para definir a união das tabelas de origem usadas na construção da visualização materializada final.

A seguir, um exemplo do gráfico de fluxo de dados para esse pipeline:

![Um gráfico de fluxo de dados de duas visualizações que levam a cinco tabelas regionais.](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/../_images/dlt-for-each-table.png)

### Solução de problemas: o loop for cria muitas tabelas com os mesmos valores

[](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/#troubleshooting-for-loop-creates-many-tables-with-same-values)

O modelo de execução preguiçosa que o pipeline usa para avaliar o código Python exige que sua lógica faça referência direta a valores individuais quando a função decorada por @dlt.table() é chamada.

O exemplo a seguir demonstra duas abordagens corretas para definir tabelas com um loop for. Nos dois exemplos, cada nome de tabela da lista tables é explicitamente referenciado na função decorada por @dlt.table().

O exemplo a seguir não faz referência aos valores corretamente. Esse exemplo cria tabelas com nomes distintos, mas todas as tabelas carregam dados do último valor no loop for:

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/python-dev.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
