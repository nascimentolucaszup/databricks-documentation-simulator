[Documentação](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/index.html)

[Delta Live Tables referências linguísticas](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/language-references.html)

# Referência da linguagem Python do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#delta-live-tables-python-language-reference)

Este artigo contém detalhes sobre a interface de programação Delta Live Tables Python .

Para obter informações sobre a SQL API, consulte a referência da linguagem SQL Delta Live Tables.

[referência da linguagem SQL Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/sql-ref.html)

Para obter detalhes específicos sobre a configuração do Auto Loader, consulte O que é o Auto Loader?.

[O que é o Auto Loader?](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../ingestion/cloud-object-storage/auto-loader/index.html)

## Antes de começar

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#before-you-begin)

A seguir, há considerações importantes quando o senhor implementa o pipeline com a interface Delta Live Tables Python :

Como as funções Python table() e view() são invocadas várias vezes durante o planejamento e a execução de uma atualização pipeline, não inclua código em uma dessas funções que possa ter efeitos colaterais (por exemplo, código que modifique dados ou envie um email). Para evitar um comportamento inesperado, suas funções Python que definem o conjunto de dados devem incluir apenas o código necessário para definir a tabela ou view.

Para realizar operações como o envio de e-mail ou a integração com um serviço de monitoramento externo, especialmente em funções que definem conjuntos de dados, use ganchos de eventos. A implementação dessas operações nas funções que definem seu conjunto de dados causará um comportamento inesperado.

[ganchos de eventos](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/event-hooks.html)

O Python table e view as funções devem retornar um DataFrame. Algumas funções que operam em DataFrames não retornam DataFrames e não devem ser usadas. Essas operações incluem funções como collect()count(), toPandas(), save() e saveAsTable(). Como as transformações do DataFrame são executadas após a resolução do gráfico de fluxo de dados completo, o uso dessas operações pode ter efeitos colaterais indesejados.

## Importar o módulo Python dlt

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#import-the-dlt-python-module)

As funções do Python das Tabelas do Delta Live são definidas no módulo dlt. Seus pipelines implementados com a API do Python devem importar este módulo:

## Criar uma exibição materializada Delta Live Tables ou tabela de transmissão

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#create-a-delta-live-tables-materialized-view-or-streaming-table)

Em Python, Delta Live Tables determina se deve atualizar uma dataset como uma tabela materializada view ou de transmissão com base na consulta de definição. O decorador @table pode ser usado para definir tanto a exibição materializada quanto as tabelas de transmissão.

Para definir um view materializado em Python, aplique @table a uma consulta que executa uma leitura estática em uma fonte de dados. Para definir uma tabela de transmissão, aplique @table a uma consulta que execute uma leitura de transmissão em uma fonte de dados ou use a função create_streaming_table(). Os dois tipos de dataset têm a mesma especificação de sintaxe, como segue:

[função create_streaming_table()](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#create-target-fn)

Observação

Para usar o argumento cluster_by para habilitar o líquido clustering, seu pipeline deve estar configurado para usar o canal de visualização.

[canal de visualização](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../release-notes/delta-live-tables/index.html#runtime-channels)

## Criar uma exibição de Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#create-a-delta-live-tables-view)

Para definir uma visualização em Python, aplique o decorador do @view. Como o decorador @table, você pode usar exibições em Delta Live Tables para datasets estáticos ou de transmissão. A seguir está a sintaxe para definir visualizações com Python:

## Exemplo: definir tabelas e exibições

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#example-define-tables-and-views)

Para definir uma tabela ou visualização em Python, aplique o decorador @dlt.view ou @dlt.table a uma função. Você pode utilizar o nome da função ou o parâmetro name para atribuir a tabela ou visualizar o nome. O exemplo a seguir define dois datasets diferentes: uma visualização chamada taxi_raw que usa um arquivo JSON como fonte de entrada e uma tabela chamada filtered_data que usa a taxi_raw exibição como entrada:

## Exemplo: acessar um dataset definido no mesmo pipeline

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#example-access-a-dataset-defined-in-the-same-pipeline)

Observação

Embora as funções dlt.read() e dlt.read_stream() ainda estejam disponíveis e sejam totalmente compatíveis com a interface Python do Delta Live Tables, a Databricks recomenda sempre usar as funções spark.read.table() e spark.readStream.table() devido ao seguinte:

As funções do site spark suportam a leitura de conjuntos de dados internos e externos, inclusive conjuntos de dados em armazenamento externo ou definidos em outro pipeline. As funções do site dlt suportam apenas a leitura de conjuntos de dados internos.

As funções spark suportam a especificação de opções, como skipChangeCommits, para operações de leitura. A especificação de opções não é suportada pelas funções dlt.

Para acessar um dataset definido no mesmo pipeline, use as funções spark.read.table() ou spark.readStream.table(), acrescentando a palavra-chave LIVE ao nome dataset:

## Exemplo: Leitura de uma tabela cadastrada em um metastore

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#example-read-from-a-table-registered-in-a-metastore)

Para ler dados de uma tabela registrada no site Hive metastore, no argumento da função, omita a palavra-chave LIVE e, opcionalmente, qualifique o nome da tabela com o nome do banco de dados:

Para obter um exemplo de leitura de uma tabela Unity Catalog , consulte Ingerir dados em um pipeline Unity Catalog .

[Ingerir dados em um pipeline Unity Catalog](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/unity-catalog.html#ingest-data)

## Exemplo: acesse um dataset usando spark.sql

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#example-access-a-dataset-using-sparksql)

Você também pode retornar um dataset utilizando uma expressão do spark.sql em uma função de consulta. Para ler de um dataset interno, acrescente o nome do dataset LIVE.:

## Criar uma tabela para ser usada como destino das operações de transmissão

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#create-a-table-to-use-as-the-target-of-streaming-operations)

Use a função create_streaming_table() para criar uma tabela de destino para os registros de saída das operações de transmissão, inclusive os registros de saída apply_changes(), apply_changes_from_snapshot() e @append_flow.

[apply_changes()](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#cdc)

[apply_changes_from_snapshot()](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#cdc-snapshots)

[@append_flow](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/flows.html#append-flows)

Observação

As funções create_target_table() e create_streaming_live_table() estão obsoletas. A Databricks recomenda atualizar o código existente para usar a create_streaming_table() função.

Observação

Para usar o argumento cluster_by para habilitar o líquido clustering, seu pipeline deve estar configurado para usar o canal de visualização.

[canal de visualização](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../release-notes/delta-live-tables/index.html#runtime-channels)

| Argumentos |
| --- |
| nameTipo:strO nome da tabela.Este parâmetro é necessário. |
| commentTipo:strUma descrição opcional para a tabela. |
| spark_confTipo:dictUma lista opcional de configurações do Spark para a execução desta consulta. |
| table_propertiesTipo:dictUma lista opcional depropriedades da tabelada tabela. |
| partition_colsTipo:arrayUma lista opcional de uma ou mais colunas para usar no particionamento da tabela. |
| cluster_byTipo:arrayOpcionalmente, ative o clustering líquido na tabela e defina as colunas a serem usadas como chave clustering.ConsulteUsar clusters líquidos para tabelas Delta. |
| pathTipo:strUm local de armazenamento opcional para os dados da tabela. Se não for definido, o sistema usará como padrão o local de armazenamento pipeline. |
| schemaTipo:strouStructTypeUma definição de esquema opcional para a tabela. Os esquemas podem ser definidos como SQL DDL strings ou com PythonStructType. |
| expect_allexpect_all_or_dropexpect_all_or_failTipo:dictRestrições opcionais de qualidade de dados para a tabela. Vejamúltiplas expectativas. |
| row_filter(Pré-visualização pública)Tipo:strUma cláusula opcional de filtro de linha para a tabela. ConsultePublicar tabelas com filtros de linha e máscaras de coluna. |


Argumentos

name

Tipo: str

O nome da tabela.

Este parâmetro é necessário.

comment

Tipo: str

Uma descrição opcional para a tabela.

spark_conf

Tipo: dict

Uma lista opcional de configurações do Spark para a execução desta consulta.

table_properties

Tipo: dict

Uma lista opcional de propriedades da tabela da tabela.

[propriedades da tabela](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/properties.html)

partition_cols

Tipo: array

Uma lista opcional de uma ou mais colunas para usar no particionamento da tabela.

cluster_by

Tipo: array

Opcionalmente, ative o clustering líquido na tabela e defina as colunas a serem usadas como chave clustering.

Consulte Usar clusters líquidos para tabelas Delta.

[Usar clusters líquidos para tabelas Delta](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../delta/clustering.html)

path

Tipo: str

Um local de armazenamento opcional para os dados da tabela. Se não for definido, o sistema usará como padrão o local de armazenamento pipeline.

schema

Tipo: str ou StructType

Uma definição de esquema opcional para a tabela. Os esquemas podem ser definidos como SQL DDL strings ou com Python StructType.

expect_all expect_all_or_drop expect_all_or_fail

Tipo: dict

Restrições opcionais de qualidade de dados para a tabela. Veja múltiplas expectativas.

[múltiplas expectativas](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/expectations.html#expect-all)

row_filter (Pré-visualização pública)

Tipo: str

Uma cláusula opcional de filtro de linha para a tabela. Consulte Publicar tabelas com filtros de linha e máscaras de coluna.

[Publicar tabelas com filtros de linha e máscaras de coluna](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/unity-catalog.html#row-filters-and-column-masks)

## Controle como as tabelas são materializadas

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#control-how-tables-are-materialized)

As tabelas também oferecem controle adicional de sua materialização:

Especifique como as tabelas são particionadas usando partition_cols. Você pode usar o particionamento para acelerar query.

[particionadas](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#schema-partition-example)

Você pode definir as propriedades da tabela ao definir uma view ou tabela. Consulte as propriedades da tabela Delta Live Tables.

[as propriedades da tabela Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/properties.html#table-properties)

Defina um local de armazenamento para os dados da tabela usando a configuração path. Por padrão, os dados da tabela são armazenados no local de armazenamento do pipeline se path não estiver definido.

Você pode usar colunas geradas em sua definição de esquema. Consulte Exemplo: Especifique um esquema e colunas de partição.

[colunas geradas](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../delta/generated-columns.html)

[Exemplo: Especifique um esquema e colunas de partição](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#schema-partition-example)

Observação

Para tabelas com menos de 1 TB de tamanho, a Databricks recomenda deixar que o Delta Live Tables controle a organização dos dados. O senhor não deve especificar colunas de partição, a menos que espere que a tabela cresça além de um terabyte.

## Exemplo: especificar um esquema e colunas de partição

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#example-specify-a-schema-and-partition-columns)

Opcionalmente, você pode especificar um esquema de tabela utilizando uma string do Python StructType ou SQL DDL. Quando especificada com uma cadeia de caracteres DDL, a definição pode incluir colunas geradas.

[colunas geradas](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../delta/generated-columns.html)

O exemplo a seguir cria uma tabela chamada sales com um esquema especificado usando Python StructType:

O exemplo a seguir especifica o esquema para uma tabela usando uma string DDL, define uma coluna gerada e define uma coluna de partição:

Por padrão, Delta Live Tables infere o esquema da definição table se você não especificar um esquema.

## Configurar uma tabela de transmissão para ignorar alterações em uma tabela de transmissão de origem

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#configure-a-streaming-table-to-ignore-changes-in-a-source-streaming-table)

Observação

O sinalizador skipChangeCommits funciona apenas com spark.readStream usando a função option() . Você não pode usar este sinalizador em uma função dlt.read_stream() .

Você não pode usar o sinalizador skipChangeCommits quando a tabela de transmissão de origem estiver definida como destino de uma função apply_changes() .

[apply_changes()](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#cdc)

Por default, as tabelas de transmissão exigem fontes somente anexadas. Quando uma tabela de transmissão usa outra tabela de transmissão como origem, e a tabela de transmissão de origem requer atualizações ou exclusões, por exemplo, processamento de “direito ao esquecimento” do GDPR, o sinalizador skipChangeCommits pode ser definido ao ler a tabela de transmissão de origem para ignorar essas mudanças. Para obter mais informações sobre esse sinalizador, consulte Ignorar atualizações e exclusões.

[Ignorar atualizações e exclusões](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../structured-streaming/delta-lake.html#ignore-changes)

## Exemplo: Definir restrições de tabela

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#example-define-table-constraints)

Visualização

As restrições de tabela estão na Pré-visualização pública.

[Pré-visualização pública](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../release-notes/release-types.html)

Ao especificar um esquema, o senhor pode definir chaves primárias e estrangeiras. As restrições são informativas e não são aplicadas. Consulte a cláusula CONSTRAINT na referência da linguagem SQL.

[cláusula CONSTRAINT](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../sql/language-manual/sql-ref-syntax-ddl-create-table-constraint.html)

O exemplo a seguir define uma tabela com uma restrição primária e estrangeira key:

## Exemplo: Definir um filtro de linha e uma máscara de coluna

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#example-define-a-row-filter-and-column-mask)

Visualização

Os filtros de linha e as máscaras de coluna estão na Pré-visualização pública.

[Pré-visualização pública](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../release-notes/release-types.html)

Para criar uma tabela materializada view ou de transmissão com um filtro de linha e uma máscara de coluna, use a cláusula ROW FILTER e a cláusula MASK. O exemplo a seguir demonstra como definir uma tabela materializada view e uma tabela de transmissão com um filtro de linha e uma máscara de coluna:

[cláusula ROW FILTER](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../sql/language-manual/sql-ref-syntax-ddl-row-filter.html)

[cláusula MASK](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../sql/language-manual/sql-ref-syntax-ddl-column-mask.html)

Para obter mais informações sobre filtros de linha e máscaras de coluna, consulte Publicar tabelas com filtros de linha e máscaras de coluna.

[Publicar tabelas com filtros de linha e máscaras de coluna](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/unity-catalog.html#row-filters-and-column-masks)

## Propriedades do Python Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#python-delta-live-tables-properties)

As tabelas a seguir descrevem as opções e propriedades que você pode especificar ao definir tabelas e exibições com Delta Live Tables:

Observação

Para usar o argumento cluster_by para habilitar o líquido clustering, seu pipeline deve estar configurado para usar o canal de visualização.

[canal de visualização](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../release-notes/delta-live-tables/index.html#runtime-channels)

| @tabela ou @visualizar |
| --- |
| nameTipo:strUm nome opcional para a tabela ou visualização. Se não estiver definida, o nome da função será usado como a tabela ou o nome de visualização. |
| commentTipo:strUma descrição opcional para a tabela. |
| spark_confTipo:dictUma lista opcional de configurações do Spark para a execução desta consulta. |
| table_propertiesTipo:dictUma lista opcional depropriedades da tabelada tabela. |
| pathTipo:strUm local de armazenamento opcional para os dados da tabela. Se não for definido, o sistema usará como padrão o local de armazenamento pipeline. |
| partition_colsTipo:acollectionofstrUma coleção opcional, por exemplo, umlistde uma ou mais colunas a serem usadas para particionar a tabela. |
| cluster_byTipo:arrayOpcionalmente, ative o clustering líquido na tabela e defina as colunas a serem usadas como chave clustering.ConsulteUsar clusters líquidos para tabelas Delta. |
| schemaTipo:strouStructTypeUma definição de esquema opcional para a tabela. Os esquemas podem ser definidos como SQL DDL strings ou com PythonStructType. |
| temporaryTipo:boolCrie uma tabela, mas não publique metadados para a tabela. A palavra-chavetemporaryinstrui o Delta Live Tables a criar uma tabela que esteja disponível para o pipeline, mas que não deva ser acessada fora do pipeline. Para reduzir o tempo de processamento, uma tabela temporária persiste durante o tempo de vida do pipeline que a cria, e não apenas em uma única atualização.O padrão é 'falso'. |
| row_filter(Pré-visualização pública)Tipo:strUma cláusula opcional de filtro de linha para a tabela. ConsultePublicar tabelas com filtros de linha e máscaras de coluna. |


@tabela ou @visualizar

name

Tipo: str

Um nome opcional para a tabela ou visualização. Se não estiver definida, o nome da função será usado como a tabela ou o nome de visualização.

comment

Tipo: str

Uma descrição opcional para a tabela.

spark_conf

Tipo: dict

Uma lista opcional de configurações do Spark para a execução desta consulta.

table_properties

Tipo: dict

Uma lista opcional de propriedades da tabela da tabela.

[propriedades da tabela](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/properties.html)

path

Tipo: str

Um local de armazenamento opcional para os dados da tabela. Se não for definido, o sistema usará como padrão o local de armazenamento pipeline.

partition_cols

Tipo: a collection of str

Uma coleção opcional, por exemplo, um list de uma ou mais colunas a serem usadas para particionar a tabela.

cluster_by

Tipo: array

Opcionalmente, ative o clustering líquido na tabela e defina as colunas a serem usadas como chave clustering.

Consulte Usar clusters líquidos para tabelas Delta.

[Usar clusters líquidos para tabelas Delta](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../delta/clustering.html)

schema

Tipo: str ou StructType

Uma definição de esquema opcional para a tabela. Os esquemas podem ser definidos como SQL DDL strings ou com Python StructType.

temporary

Tipo: bool

Crie uma tabela, mas não publique metadados para a tabela. A palavra-chave temporary instrui o Delta Live Tables a criar uma tabela que esteja disponível para o pipeline, mas que não deva ser acessada fora do pipeline. Para reduzir o tempo de processamento, uma tabela temporária persiste durante o tempo de vida do pipeline que a cria, e não apenas em uma única atualização.

O padrão é 'falso'.

row_filter (Pré-visualização pública)

Tipo: str

Uma cláusula opcional de filtro de linha para a tabela. Consulte Publicar tabelas com filtros de linha e máscaras de coluna.

[Publicar tabelas com filtros de linha e máscaras de coluna](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/unity-catalog.html#row-filters-and-column-masks)

| Definição de tabela ou exibição |
| --- |
| def<function-name>()Uma função do Python que define o dataset. Se o parâmetronamenão estiver configurado, então<function-name>será utilizado como o nome do dataset de destino. |
| queryUma declaração Spark SQL que retorna um dataset Spark ou DataFrame Koalas.Usedlt.read()ouspark.read.table()para realizar uma leitura completa de um dataset definido no mesmo pipeline. Para ler um site externo dataset, use a funçãospark.read.table(). O senhor não pode usar o sitedlt.read()para ler conjuntos de dados externos. Comospark.read.table()pode ser usado para ler um conjunto de dados interno, um conjunto de dados definido fora do site pipeline atual, e permite que o usuário especifique opções de leitura de dados, o site Databricks recomenda usá-lo em vez da funçãodlt.read().Quando o senhor usar a funçãospark.read.table()para ler de um dataset definido no mesmo pipeline, acrescente a palavra-chaveLIVEao nome dataset no argumento da função. Por exemplo, para ler em um dataset chamadocustomers:spark.read.table("LIVE.customers")Você também pode utilizar a funçãospark.read.table()para ler de uma tabela registrada no metastore omitindo a palavra-chaveLIVEe, opcionalmente, qualificando o nome da tabela com o nome do banco de dados:spark.read.table("sales.customers")Usedlt.read_stream()ouspark.readStream.table()para realizar uma leitura de transmissão de um dataset definido no mesmo pipeline. Para realizar uma leitura de transmissão de um site externo dataset, use a funçãospark.readStream.table(). Comospark.readStream.table()pode ser usado para ler um conjunto de dados interno, um conjunto de dados definido fora do site pipeline atual, e permite que o usuário especifique opções de leitura de dados, o site Databricks recomenda usá-lo em vez da funçãodlt.read_stream().Para definir uma consulta em uma função Delta Live Tablestableusando a sintaxe SQL, use a funçãospark.sql. Vejao exemplo: Acessar um site dataset usando spark.sql. Para definir uma consulta em uma função Delta Live Tablestableusando Python, use a sintaxedo PySpark. |


Definição de tabela ou exibição

def <function-name>()

Uma função do Python que define o dataset. Se o parâmetro name não estiver configurado, então <function-name> será utilizado como o nome do dataset de destino.

query

Uma declaração Spark SQL que retorna um dataset Spark ou DataFrame Koalas.

Use dlt.read() ou spark.read.table() para realizar uma leitura completa de um dataset definido no mesmo pipeline. Para ler um site externo dataset, use a função spark.read.table(). O senhor não pode usar o site dlt.read() para ler conjuntos de dados externos. Como spark.read.table() pode ser usado para ler um conjunto de dados interno, um conjunto de dados definido fora do site pipeline atual, e permite que o usuário especifique opções de leitura de dados, o site Databricks recomenda usá-lo em vez da função dlt.read().

Quando o senhor usar a função spark.read.table() para ler de um dataset definido no mesmo pipeline, acrescente a palavra-chave LIVE ao nome dataset no argumento da função. Por exemplo, para ler em um dataset chamado customers:

spark.read.table("LIVE.customers")

Você também pode utilizar a função spark.read.table() para ler de uma tabela registrada no metastore omitindo a palavra-chave LIVE e, opcionalmente, qualificando o nome da tabela com o nome do banco de dados:

spark.read.table("sales.customers")

Use dlt.read_stream() ou spark.readStream.table() para realizar uma leitura de transmissão de um dataset definido no mesmo pipeline. Para realizar uma leitura de transmissão de um site externo dataset, use a função spark.readStream.table(). Como spark.readStream.table() pode ser usado para ler um conjunto de dados interno, um conjunto de dados definido fora do site pipeline atual, e permite que o usuário especifique opções de leitura de dados, o site Databricks recomenda usá-lo em vez da função dlt.read_stream().

Para definir uma consulta em uma função Delta Live Tables table usando a sintaxe SQL, use a função spark.sql. Veja o exemplo: Acessar um site dataset usando spark.sql. Para definir uma consulta em uma função Delta Live Tables table usando Python, use a sintaxe do PySpark.

[o exemplo: Acessar um site dataset usando spark.sql](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#use-spark-sql)

[do PySpark](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/https://api-docs.databricks.com/python/pyspark/latest/pyspark.sql/dataframe.html)

| Expectativas |
| --- |
| @expect("description","constraint")Declarar uma restrição de qualidade de dados identificada pordescription. Se uma linha violar a expectativa, inclua a linha no dataset de destino. |
| @expect_or_drop("description","constraint")Declarar uma restrição de qualidade de dados identificada pordescription. Se uma linha violar a expectativa, solte a linha do dataset de destino. |
| @expect_or_fail("description","constraint")Declarar uma restrição de qualidade de dados identificada pordescription. Se uma linha violar a expectativa, interrompa imediatamente a execução. |
| @expect_all(expectations)Declare uma ou mais restrições de qualidade de dados.expectationsé um dicionário Python, em que a chave é a descrição da expectativa e o valor é a restrição de expectativa. Se uma linha violar qualquer uma das expectativas, inclua a linha no dataset de destino. |
| @expect_all_or_drop(expectations)Declare uma ou mais restrições de qualidade de dados.expectationsé um dicionário Python, em que a chave é a descrição da expectativa e o valor é a restrição de expectativa. Se uma linha violar qualquer uma das expectativas, solte a linha do dataset de destino. |
| @expect_all_or_fail(expectations)Declare uma ou mais restrições de qualidade de dados.expectationsé um dicionário Python, em que a chave é a descrição da expectativa e o valor é a restrição de expectativa. Se uma linha violar qualquer uma das expectativas, interrompa imediatamente a execução. |


Expectativas

@expect("description", "constraint")

Declarar uma restrição de qualidade de dados identificada por description. Se uma linha violar a expectativa, inclua a linha no dataset de destino.

@expect_or_drop("description", "constraint")

Declarar uma restrição de qualidade de dados identificada por description. Se uma linha violar a expectativa, solte a linha do dataset de destino.

@expect_or_fail("description", "constraint")

Declarar uma restrição de qualidade de dados identificada por description. Se uma linha violar a expectativa, interrompa imediatamente a execução.

@expect_all(expectations)

Declare uma ou mais restrições de qualidade de dados. expectations é um dicionário Python, em que a chave é a descrição da expectativa e o valor é a restrição de expectativa. Se uma linha violar qualquer uma das expectativas, inclua a linha no dataset de destino.

@expect_all_or_drop(expectations)

Declare uma ou mais restrições de qualidade de dados. expectations é um dicionário Python, em que a chave é a descrição da expectativa e o valor é a restrição de expectativa. Se uma linha violar qualquer uma das expectativas, solte a linha do dataset de destino.

@expect_all_or_fail(expectations)

Declare uma ou mais restrições de qualidade de dados. expectations é um dicionário Python, em que a chave é a descrição da expectativa e o valor é a restrição de expectativa. Se uma linha violar qualquer uma das expectativas, interrompa imediatamente a execução.

## captura de dados de alterações (CDC) de um feed de alterações com Python em Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#change-data-capture-from-a-change-feed-with-python-in-delta-live-tables)

Use a função apply_changes() no site Python API para usar a funcionalidade Delta Live Tables captura de dados de alterações (CDC) (CDC) para processar dados de origem de um feed de dados de alterações (CDF).

Importante

O senhor deve declarar uma tabela de transmissão de destino para aplicar as alterações. Opcionalmente, o senhor pode especificar o esquema da tabela de destino. Ao especificar o esquema da tabela de destino apply_changes(), o senhor deve incluir as colunas __START_AT e __END_AT com o mesmo tipo de dados dos campos sequence_by.

Para criar a tabela de destino necessária, o senhor pode usar a função create_streaming_table() na interface Python do Delta Live Tables.

[create_streaming_table()](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#create-target-fn)

Observação

Para o processamento de APPLY CHANGES, o comportamento do default para eventos INSERT e UPDATE é fazer upsert de eventos CDC da origem: atualizar todas as linhas da tabela de destino que correspondam ao(s) key(s) especificado(s) ou inserir uma nova linha quando não houver um registro correspondente na tabela de destino. O tratamento de eventos DELETE pode ser especificado com a condição APPLY AS DELETE WHEN.

Para saber mais sobre o processamento do CDC com um feed de alterações, consulte APLICAR ALTERAÇÕES APIs: Simplifique a captura de dados de alterações (CDC) com Delta Live Tables. Para ver um exemplo de uso da função apply_changes(), consulte Exemplo: Processamento de SCD tipo 1 e SCD tipo 2 com dados de origem CDF.

[APLICAR ALTERAÇÕES APIs: Simplifique a captura de dados de alterações (CDC) com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/cdc.html)

[Exemplo: Processamento de SCD tipo 1 e SCD tipo 2 com dados de origem CDF](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/cdc.html#cdc-example)

Importante

O senhor deve declarar uma tabela de transmissão de destino para aplicar as alterações. Opcionalmente, o senhor pode especificar o esquema da tabela de destino. Ao especificar o esquema da tabela de destino apply_changes, o senhor deve incluir as colunas __START_AT e __END_AT com o mesmo tipo de dados que o campo sequence_by.

Consulte a seção APPLY CHANGES APIs: Simplificar a captura de dados de alterações (CDC) com Delta Live Tables.

[APPLY CHANGES APIs: Simplificar a captura de dados de alterações (CDC) com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/cdc.html)

| Argumentos |
| --- |
| targetTipo:strO nome da tabela a ser atualizada. Você pode usar a funçãocreate_streaming_table()para criar a tabela de destino antes de executar a funçãoapply_changes().Este parâmetro é necessário. |
| sourceTipo:strA fonte de dados que contém os registros do CDC.Este parâmetro é necessário. |
| keysTipo:listA coluna ou combinação de colunas que identificam exclusivamente uma linha nos dados de origem. Isso é usado para identificar quais eventos de CDC se aplicam a registros específicos na tabela de destino.Você pode especificar:Uma lista de strings:["userId","orderId"]Uma lista de funções do Spark SQLcol():[col("userId"),col("orderId"]Argumentos para funçõescol()não podem incluir qualificadores. Por exemplo, você pode usarcol(userId), mas não pode usarcol(source.userId).Este parâmetro é necessário. |
| sequence_byTipo:stroucol()O nome da coluna que especifica a ordem lógica dos eventos de CDC nos dados de origem. O Delta Live Tables usa esse sequenciamento para manipular eventos de alteração que chegam fora de ordem.Você pode especificar:Uma string:"sequenceNum"Uma função Spark SQLcol():col("sequenceNum")Argumentos para funçõescol()não podem incluir qualificadores. Por exemplo, você pode usarcol(userId), mas não pode usarcol(source.userId).A coluna especificada deve ser um tipo de dados classificável.Este parâmetro é necessário. |
| ignore_null_updatesTipo:boolPermitir a ingestão de atualizações que contenham um subconjunto da coluna de destino. Quando um evento CDC corresponde a uma linha existente eignore_null_updateséTrue, as colunas comnullmantêm seus valores existentes no destino. Isso também se aplica a colunas aninhadas com um valor denull. Quandoignore_null_updateséFalse, os valores existentes são substituídos por valoresnull.Este parâmetro é opcional.O padrão éFalse. |
| apply_as_deletesTipo:strouexpr()Especifica quando um evento CDC deve ser tratado comoDELETEem vez de upsert. Para lidar com dados fora de ordem, a linha excluída é temporariamente retida como uma lápide na tabela subjacente Delta e é criado um view no metastore que filtra essas lápides. O intervalo de retenção pode ser configurado com a propriedade de tabelapipelines.cdc.tombstoneGCThresholdInSeconds.Você pode especificar:Uma string:"Operation='DELETE'"Uma função Spark SQLexpr():expr("Operation='DELETE'")Este parâmetro é opcional. |
| apply_as_truncatesTipo:strouexpr()Especifica quando um evento de CDC deve ser tratado como uma tabela completaTRUNCATE. Como esta cláusula aciona uma operação completa de truncamento da tabela de destino, ela deve ser usada apenas para casos de uso específicos que exijam essa funcionalidade.O parâmetroapply_as_truncatesé compatível apenas com o SCD tipo 1. O SCD tipo 2 não oferece suporte a operações de truncamento.Você pode especificar:Uma string:"Operation='TRUNCATE'"Uma função Spark SQLexpr():expr("Operation='TRUNCATE'")Este parâmetro é opcional. |
| column_listexcept_column_listTipo:listUm subconjunto de colunas a incluir na tabela de destino. Usecolumn_listpara especificar a lista completa de colunas a incluir. Useexcept_column_listpara especificar as colunas a serem excluídas. Você pode declarar o valor como uma lista de strings ou como funções Spark SQLcol():column_list=["userId","name","city"].column_list=[col("userId"),col("name"),col("city")]except_column_list=["operation","sequenceNum"]except_column_list=[col("operation"),col("sequenceNum")Argumentos para funçõescol()não podem incluir qualificadores. Por exemplo, você pode usarcol(userId), mas não pode usarcol(source.userId).Este parâmetro é opcional.O padrão é incluir todas as colunas na tabela de destino quando nenhum argumentocolumn_listouexcept_column_listé passado para a função. |
| stored_as_scd_typeTipo:strouintSe os registros devem ser armazenados como SCD tipo 1 ou SCD tipo 2.Defina como1para SCD tipo 1 ou2para SCD tipo 2.Esta cláusula é opcional.O padrão é SCD tipo 1. |
| track_history_column_listtrack_history_except_column_listTipo:listUm subconjunto de colunas de saída a serem rastreadas para história na tabela de destino. Usetrack_history_column_listpara especificar a lista completa de colunas a serem rastreadas. Utilizetrack_history_except_column_listpara especificar as colunas a serem excluídas do acompanhamento. Você pode declarar qualquer valor como uma lista de strings ou como funções Spark SQLcol(): -track_history_column_list=["userId","name","city"]. -track_history_column_list=[col("userId"),col("name"),col("city")]-track_history_except_column_list=["operation","sequenceNum"]-track_history_except_column_list=[col("operation"),col("sequenceNum")Argumentos para funçõescol()não podem incluir qualificadores. Por exemplo, você pode usarcol(userId), mas não pode usarcol(source.userId).Este parâmetro é opcional.O padrão é incluir todas as colunas na tabela de destino quando nenhum argumentotrack_history_column_listoutrack_history_except_column_listé passado para a função. |


Argumentos

target

Tipo: str

O nome da tabela a ser atualizada. Você pode usar a função create_streaming_table() para criar a tabela de destino antes de executar a função apply_changes() .

[create_streaming_table()](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#create-target-fn)

Este parâmetro é necessário.

source

Tipo: str

A fonte de dados que contém os registros do CDC.

Este parâmetro é necessário.

keys

Tipo: list

A coluna ou combinação de colunas que identificam exclusivamente uma linha nos dados de origem. Isso é usado para identificar quais eventos de CDC se aplicam a registros específicos na tabela de destino.

Você pode especificar:

Uma lista de strings: ["userId", "orderId"]

Uma lista de funções do Spark SQL col(): [col("userId"), col("orderId"]

Argumentos para funções col() não podem incluir qualificadores. Por exemplo, você pode usar col(userId), mas não pode usar col(source.userId).

Este parâmetro é necessário.

sequence_by

Tipo: str ou col()

O nome da coluna que especifica a ordem lógica dos eventos de CDC nos dados de origem. O Delta Live Tables usa esse sequenciamento para manipular eventos de alteração que chegam fora de ordem.

Você pode especificar:

Uma string: "sequenceNum"

Uma função Spark SQL col(): col("sequenceNum")

Argumentos para funções col() não podem incluir qualificadores. Por exemplo, você pode usar col(userId), mas não pode usar col(source.userId).

A coluna especificada deve ser um tipo de dados classificável.

Este parâmetro é necessário.

ignore_null_updates

Tipo: bool

Permitir a ingestão de atualizações que contenham um subconjunto da coluna de destino. Quando um evento CDC corresponde a uma linha existente e ignore_null_updates é True, as colunas com null mantêm seus valores existentes no destino. Isso também se aplica a colunas aninhadas com um valor de null. Quando ignore_null_updates é False, os valores existentes são substituídos por valores null.

Este parâmetro é opcional.

O padrão é False.

apply_as_deletes

Tipo: str ou expr()

Especifica quando um evento CDC deve ser tratado como DELETE em vez de upsert. Para lidar com dados fora de ordem, a linha excluída é temporariamente retida como uma lápide na tabela subjacente Delta e é criado um view no metastore que filtra essas lápides. O intervalo de retenção pode ser configurado com a propriedade de tabela pipelines.cdc.tombstoneGCThresholdInSeconds.

Você pode especificar:

Uma string: "Operation = 'DELETE'"

Uma função Spark SQL expr(): expr("Operation = 'DELETE'")

Este parâmetro é opcional.

apply_as_truncates

Tipo: str ou expr()

Especifica quando um evento de CDC deve ser tratado como uma tabela completa TRUNCATE. Como esta cláusula aciona uma operação completa de truncamento da tabela de destino, ela deve ser usada apenas para casos de uso específicos que exijam essa funcionalidade.

O parâmetro apply_as_truncates é compatível apenas com o SCD tipo 1. O SCD tipo 2 não oferece suporte a operações de truncamento.

Você pode especificar:

Uma string: "Operation = 'TRUNCATE'"

Uma função Spark SQL expr(): expr("Operation = 'TRUNCATE'")

Este parâmetro é opcional.

column_list

except_column_list

Tipo: list

Um subconjunto de colunas a incluir na tabela de destino. Use column_list para especificar a lista completa de colunas a incluir. Use except_column_list para especificar as colunas a serem excluídas. Você pode declarar o valor como uma lista de strings ou como funções Spark SQL col():

column_list = ["userId", "name", "city"].

column_list = [col("userId"), col("name"), col("city")]

except_column_list = ["operation", "sequenceNum"]

except_column_list = [col("operation"), col("sequenceNum")

Argumentos para funções col() não podem incluir qualificadores. Por exemplo, você pode usar col(userId), mas não pode usar col(source.userId).

Este parâmetro é opcional.

O padrão é incluir todas as colunas na tabela de destino quando nenhum argumento column_list ou except_column_list é passado para a função.

stored_as_scd_type

Tipo: str ou int

Se os registros devem ser armazenados como SCD tipo 1 ou SCD tipo 2.

Defina como 1 para SCD tipo 1 ou 2 para SCD tipo 2.

Esta cláusula é opcional.

O padrão é SCD tipo 1.

track_history_column_list

track_history_except_column_list

Tipo: list

Um subconjunto de colunas de saída a serem rastreadas para história na tabela de destino. Use track_history_column_list para especificar a lista completa de colunas a serem rastreadas. Utilize track_history_except_column_list para especificar as colunas a serem excluídas do acompanhamento. Você pode declarar qualquer valor como uma lista de strings ou como funções Spark SQL col() : - track_history_column_list = ["userId", "name", "city"]. - track_history_column_list = [col("userId"), col("name"), col("city")] - track_history_except_column_list = ["operation", "sequenceNum"] - track_history_except_column_list = [col("operation"), col("sequenceNum")

Argumentos para funções col() não podem incluir qualificadores. Por exemplo, você pode usar col(userId), mas não pode usar col(source.userId).

Este parâmetro é opcional.

O padrão é incluir todas as colunas na tabela de destino quando nenhum argumento track_history_column_list ou track_history_except_column_list é passado para a função.

## captura de dados de alterações (CDC) do banco de dados Snapshot com Python em Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#change-data-capture-from-database-snapshots-with-python-in-delta-live-tables)

Visualização

A API APPLY CHANGES FROM SNAPSHOT está em pré-visualização pública.

[pré-visualização pública](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/../release-notes/release-types.html)

Use a função apply_changes_from_snapshot() no site Python API para usar a funcionalidade Delta Live Tables captura de dados de alterações (CDC) (CDC) para processar os dados de origem do banco de dados Snapshot.

Importante

Você deve declarar uma tabela de transmissão de destino para aplicar as alterações. Opcionalmente, você pode especificar o esquema para sua tabela de destino. Ao especificar o esquema da tabela de destino do apply_changes_from_snapshot(), você também deve incluir as colunas __START_AT e __END_AT com o mesmo tipo de dados que o campo sequence_by .

Para criar a tabela de destino necessária, o senhor pode usar a função create_streaming_table() na interface Python do Delta Live Tables.

[create_streaming_table()](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#create-target-fn)

Observação

Para o processamento APPLY CHANGES FROM SNAPSHOT, o comportamento do default é inserir uma nova linha quando não houver um registro correspondente com o mesmo key(s) no destino. Se houver um registro correspondente, ele será atualizado somente se algum dos valores da linha tiver sido alterado. As linhas com chave presentes no destino, mas não mais presentes na origem, são excluídas.

Para saber mais sobre o processamento do CDC com o Snapshot, consulte APLICAR ALTERAÇÕES APIs: Simplifique a captura de dados de alterações (CDC) com Delta Live Tables. Para obter exemplos de uso da função apply_changes_from_snapshot(), consulte os exemplos de ingestão periódica em Snapshot  e ingestão histórica em Snapshot .

[APLICAR ALTERAÇÕES APIs: Simplifique a captura de dados de alterações (CDC) com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/cdc.html)

[ingestão periódica em Snapshot](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/cdc.html#periodic-snapshot-example)

[ingestão histórica em Snapshot](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/cdc.html#historical-snapshot-example)

| Argumentos |
| --- |
| targetTipo:strO nome da tabela a ser atualizada. O senhor pode usar a funçãocreate_streaming_table()para criar a tabela de destino antes de executar a funçãoapply_changes().Este parâmetro é necessário. |
| sourceTipo:stroulambdafunctionO nome de uma tabela ou view para Snapshot periodicamente ou uma função lambda Python que retorna o Snapshot DataFrame a ser processado e a versão Snapshot. ConsulteImplementar o argumento de origem.Este parâmetro é necessário. |
| keysTipo:listA coluna ou combinação de colunas que identificam exclusivamente uma linha nos dados de origem. Isso é usado para identificar quais eventos de CDC se aplicam a registros específicos na tabela de destino.Você pode especificar:Uma lista de strings:["userId","orderId"]Uma lista de funções do Spark SQLcol():[col("userId"),col("orderId"]Argumentos para funçõescol()não podem incluir qualificadores. Por exemplo, você pode usarcol(userId), mas não pode usarcol(source.userId).Este parâmetro é necessário. |
| stored_as_scd_typeTipo:strouintSe os registros devem ser armazenados como SCD tipo 1 ou SCD tipo 2.Defina como1para SCD tipo 1 ou2para SCD tipo 2.Esta cláusula é opcional.O padrão é SCD tipo 1. |
| track_history_column_listtrack_history_except_column_listTipo:listUm subconjunto de colunas de saída a serem rastreadas para história na tabela de destino. Usetrack_history_column_listpara especificar a lista completa de colunas a serem rastreadas. Utilizetrack_history_except_column_listpara especificar as colunas a serem excluídas do acompanhamento. Você pode declarar qualquer valor como uma lista de strings ou como funções Spark SQLcol(): -track_history_column_list=["userId","name","city"]. -track_history_column_list=[col("userId"),col("name"),col("city")]-track_history_except_column_list=["operation","sequenceNum"]-track_history_except_column_list=[col("operation"),col("sequenceNum")Argumentos para funçõescol()não podem incluir qualificadores. Por exemplo, você pode usarcol(userId), mas não pode usarcol(source.userId).Este parâmetro é opcional.O padrão é incluir todas as colunas na tabela de destino quando nenhum argumentotrack_history_column_listoutrack_history_except_column_listé passado para a função. |


Argumentos

target

Tipo: str

O nome da tabela a ser atualizada. O senhor pode usar a função create_streaming_table() para criar a tabela de destino antes de executar a função apply_changes().

[create_streaming_table()](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#create-target-fn)

Este parâmetro é necessário.

source

Tipo: str ou lambda function

O nome de uma tabela ou view para Snapshot periodicamente ou uma função lambda Python que retorna o Snapshot DataFrame a ser processado e a versão Snapshot. Consulte Implementar o argumento de origem.

[Implementar o argumento de origem](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#snapshot-version-type)

Este parâmetro é necessário.

keys

Tipo: list

A coluna ou combinação de colunas que identificam exclusivamente uma linha nos dados de origem. Isso é usado para identificar quais eventos de CDC se aplicam a registros específicos na tabela de destino.

Você pode especificar:

Uma lista de strings: ["userId", "orderId"]

Uma lista de funções do Spark SQL col(): [col("userId"), col("orderId"]

Argumentos para funções col() não podem incluir qualificadores. Por exemplo, você pode usar col(userId), mas não pode usar col(source.userId).

Este parâmetro é necessário.

stored_as_scd_type

Tipo: str ou int

Se os registros devem ser armazenados como SCD tipo 1 ou SCD tipo 2.

Defina como 1 para SCD tipo 1 ou 2 para SCD tipo 2.

Esta cláusula é opcional.

O padrão é SCD tipo 1.

track_history_column_list

track_history_except_column_list

Tipo: list

Um subconjunto de colunas de saída a serem rastreadas para história na tabela de destino. Use track_history_column_list para especificar a lista completa de colunas a serem rastreadas. Utilize track_history_except_column_list para especificar as colunas a serem excluídas do acompanhamento. Você pode declarar qualquer valor como uma lista de strings ou como funções Spark SQL col() : - track_history_column_list = ["userId", "name", "city"]. - track_history_column_list = [col("userId"), col("name"), col("city")] - track_history_except_column_list = ["operation", "sequenceNum"] - track_history_except_column_list = [col("operation"), col("sequenceNum")

Argumentos para funções col() não podem incluir qualificadores. Por exemplo, você pode usar col(userId), mas não pode usar col(source.userId).

Este parâmetro é opcional.

O padrão é incluir todas as colunas na tabela de destino quando nenhum argumento track_history_column_list ou track_history_except_column_list é passado para a função.

### Implementar o argumento source

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#implement-the-source-argument)

A função apply_changes_from_snapshot() inclui o argumento source. Para processar o Snapshot histórico, espera-se que o argumento source seja uma função lambda Python que retorne dois valores para a função apply_changes_from_snapshot(): um Python DataFrame contendo os dados Snapshot a serem processados e uma versão Snapshot.

A seguir, a assinatura da função lambda:

O argumento para a função lambda é a versão mais recentemente processada do site Snapshot.

O valor de retorno da função lambda é None ou uma tupla de dois valores: O primeiro valor da tupla é um DataFrame que contém o Snapshot a ser processado. O segundo valor da tupla é a versão Snapshot que representa a ordem lógica do Snapshot.

Um exemplo que implementa e chama a função lambda:

O tempo de execução do Delta Live Tables executa os seguintes passos sempre que o pipeline que contém a função apply_changes_from_snapshot() é acionado:

Execute a função next_snapshot_and_version para carregar o próximo Snapshot DataFrame e a versão correspondente do Snapshot.

Se nenhum DataFrame retornar, a execução será encerrada e a atualização do pipeline será marcada como concluída.

Detecta as alterações no novo Snapshot e as aplica de forma incremental à tabela de destino.

Retorna ao passo #1 para carregar o próximo Snapshot e sua versão.

## Limitações

[](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/#limitations)

A interface Python do Delta Live Tables tem a seguinte limitação:

A função pivot() não é suportada. As pivot operações em Spark requerem o carregamento ávido de dados de entrada para compute o esquema de saída. Esse recurso não é compatível com o site Delta Live Tables.

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/python-ref.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
