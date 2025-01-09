[Documentação](https://docs.databricks.com/pt/delta-live-tables/cdc.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/cdc.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/cdc.html/index.html)

[Carga e transformação de dados com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/cdc.html/load-and-transform.html)

# A página APPLY CHANGES APIs: Simplificar a captura de dados de alterações (CDC) com Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#the-apply-changes-apis-simplify-change-data-capture-with-delta-live-tables)

Delta Live Tables simplifica a captura de dados de alterações (CDC) (CDC) com APPLY CHANGES e APPLY CHANGES FROM SNAPSHOT APIs. A interface que o senhor utiliza depende da origem dos dados de modificação:

Use APPLY CHANGES para processar alterações de um feed de dados de alteração (CDF).

Use APPLY CHANGES FROM SNAPSHOT (Public Preview) para processar alterações no Snapshot do banco de dados.

Anteriormente, a instrução MERGE INTO era comumente usada para processar registros CDC em Databricks. No entanto, MERGE INTO pode produzir resultados incorretos devido a registros fora de sequência ou exigir uma lógica complexa para reordenar os registros.

A API APPLY CHANGES é compatível com as interfaces SQL e Python do Delta Live Tables. A API APPLY CHANGES FROM SNAPSHOT A API é compatível com a interface Python do Delta Live Tables.

Tanto APPLY CHANGES quanto APPLY CHANGES FROM SNAPSHOT suportam a atualização de tabelas usando SCD tipo 1 e tipo 2:

Use o SCD tipo 1 para atualizar os registros diretamente. O histórico não é mantido para registros atualizados.

Use o SCD tipo 2 para manter um histórico de registros, em todas as atualizações ou em atualizações de um conjunto específico de colunas.

Para obter sintaxe e outras referências, consulte:

captura de dados de alterações (CDC) de um feed de alterações com Python em Delta Live Tables

[captura de dados de alterações (CDC) de um feed de alterações com Python em Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/cdc.html/python-ref.html#cdc)

captura de dados de alterações (CDC) com SQL em Delta Live Tables

[captura de dados de alterações (CDC) com SQL em Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/cdc.html/sql-ref.html#cdc)

Observação

Este artigo descreve como atualizar tabelas em seu pipeline Delta Live Tables com base nas alterações nos dados de origem. Para saber como registrar e consultar informações de alteração em nível de linha para tabelas Delta, consulte Usar o feed de dados de alteração do Delta Lake no Databricks.

[Usar o feed de dados de alteração do Delta Lake no Databricks](https://docs.databricks.com/pt/delta-live-tables/cdc.html/../delta/delta-change-data-feed.html)

## Requisitos

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#requirements)

Para usar o CDC APIs, seu pipeline deve estar configurado para usar serverless o pipeline DLT ou Delta Live Tables Pro as Advanced edições ou.

[serverless o pipeline DLT](https://docs.databricks.com/pt/delta-live-tables/cdc.html/serverless-dlt.html)

[edições](https://docs.databricks.com/pt/delta-live-tables/cdc.html/configure-pipeline.html#editions)

## Como o CDC é implementado com a API APPLY CHANGES?

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#how-is-cdc-implemented-with-the-apply-changes-api)

Ao tratar automaticamente os registros fora de sequência, a API APPLY CHANGES do Delta Live Tables garante o processamento correto dos registros CDC e elimina a necessidade de desenvolver uma lógica complexa para tratar os registros fora de sequência. É necessário especificar uma coluna nos dados de origem para sequenciar os registros, que o Delta Live Tables interpreta como uma representação monotonicamente crescente da ordenação adequada dos dados de origem. O Delta Live Tables trata automaticamente os dados que chegam fora de ordem. Para alterações SCD tipo 2, o Delta Live Tables propaga os valores de sequenciamento apropriados para as colunas __START_AT e __END_AT da tabela de destino. Deve haver uma atualização distinta por key em cada valor de sequenciamento, e não há suporte para valores de sequenciamento NULL.

Para executar o processamento em CDC com APPLY CHANGES, o senhor primeiro cria uma tabela de transmissão e, em seguida, usa a instrução APPLY CHANGES INTO em SQL ou a função apply_changes() em Python para especificar a fonte, a chave e o sequenciamento do feed de modificação. Para criar a tabela de transmissão de destino, use a instrução CREATE OR REFRESH STREAMING TABLE em SQL ou a função create_streaming_table() em Python. Veja os exemplos de processamento de SCD tipo 1 e tipo 2.

[processamento de SCD tipo 1 e tipo 2](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#cdc-example)

Para obter detalhes sobre a sintaxe, consulte a referência SQL do Delta Live Tables ou a referência Python.

[referência SQL](https://docs.databricks.com/pt/delta-live-tables/cdc.html/sql-ref.html#cdc)

[referência Python](https://docs.databricks.com/pt/delta-live-tables/cdc.html/python-ref.html#cdc)

## Como o CDC é implementado com a API APPLY CHANGES FROM SNAPSHOT?

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#how-is-cdc-implemented-with-the-apply-changes-from-snapshot-api)

Visualização

A API APPLY CHANGES FROM SNAPSHOT está em pré-visualização pública.

[pré-visualização pública](https://docs.databricks.com/pt/delta-live-tables/cdc.html/../release-notes/release-types.html)

APPLY CHANGES FROM SNAPSHOT é um API declarativo que determina com eficiência as alterações nos dados de origem comparando uma série de Snapshot em ordem e, em seguida, executa o processamento necessário para CDC o processamento dos registros no Snapshot. APPLY CHANGES FROM SNAPSHOT é compatível apenas com a interface Python do Delta Live Tables.

APPLY CHANGES FROM SNAPSHOT suporta a ingestão de Snapshot de vários tipos de fontes:

Use a ingestão periódica de Snapshot para ingerir Snapshot de uma tabela existente ou view. APPLY CHANGES FROM SNAPSHOT tem uma interface simples e otimizada para suportar a ingestão periódica de Snapshot a partir de um objeto de banco de dados existente. Um novo Snapshot é ingerido a cada atualização do site pipeline, e o tempo de ingestão é usado como a versão do Snapshot. Quando um pipeline é executado no modo contínuo, vários instantâneos são ingeridos com cada atualização do pipeline em um período determinado pela configuração do intervalo de acionamento do fluxo que contém o processamento de APLICAR ALTERAÇÕES DO instantâneo.

[intervalo de acionamento](https://docs.databricks.com/pt/delta-live-tables/cdc.html/pipeline-mode.html#trigger-interval)

Use a ingestão histórica do Snapshot para processar arquivos que contenham o Snapshot do banco de dados, como o Snapshot gerado a partir de um banco de dados Oracle ou MySQL ou um data warehouse.

Para executar o processamento de CDC a partir de qualquer tipo de fonte com APPLY CHANGES FROM SNAPSHOT, o senhor primeiro cria uma tabela de transmissão e, em seguida, usa a função apply_changes_from_snapshot() em Python para especificar a Snapshot, a chave e outros argumentos necessários para implementar o processamento. Veja os exemplos de ingestão periódica em Snapshot  e ingestão histórica em Snapshot .

[ingestão periódica em Snapshot](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#periodic-snapshot-example)

[histórica em Snapshot](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#historical-snapshot-example)

O Snapshot passado para API deve estar em ordem crescente por versão. Se o site Delta Live Tables detectar um Snapshot fora de ordem, será lançado um erro.

Para obter detalhes sobre a sintaxe, consulte a referência do Delta Live Tables Python.

[referência](https://docs.databricks.com/pt/delta-live-tables/cdc.html/python-ref.html#cdc-snapshots)

## Limitações

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#limitations)

A coluna usada para sequenciamento deve ser um tipo de dados classificável.

## Exemplo: Processamento de SCD tipo 1 e SCD tipo 2 com dados de origem CDF

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#example-scd-type-1-and-scd-type-2-processing-with-cdf-source-data)

As seções a seguir fornecem exemplos de consultas Delta Live Tables SCD tipo 1 e tipo 2 que atualizam tabelas de destino com base em eventos de origem de um feed de dados de alteração:

Cria novos registros de usuário.

Exclui um registro de usuário.

Atualiza os registros de usuários. No exemplo do SCD tipo 1, as últimas UPDATE operações chegam atrasadas e são descartadas da tabela de destino, demonstrando o tratamento de eventos fora de ordem.

Os exemplos a seguir pressupõem familiaridade com a configuração e atualização de pipelines do Delta Live Tables. Consulte Tutorial: Execute seu primeiro pipeline das Delta Live Tables.

[Tutorial: Execute seu primeiro pipeline das Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/cdc.html/tutorial-pipelines.html)

Para executar esses exemplos, você deve começar criando um dataset de amostra. Consulte Gerar dados de teste.

[Gerar dados de teste](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#generate-data)

A seguir encontram-se registros de entrada para esses exemplos:

| userId | name | city | operation | sequenceNum |
| --- | --- | --- | --- | --- |
| 124 | Raul | Oaxaca | INSERT | 1 |
| 123 | Isabel | Monterrey | INSERT | 1 |
| 125 | Mercedes | Tijuana | INSERT | 2 |
| 126 | Lily | Cancun | INSERT | 2 |
| 123 | null | null | DELETE | 6 |
| 125 | Mercedes | Guadalajara | UPDATE | 6 |
| 125 | Mercedes | Mexicali | UPDATE | 5 |
| 123 | Isabel | Chihuahua | UPDATE | 5 |


userId

name

city

operation

sequenceNum

124

Raul

Oaxaca

INSERT

1

123

Isabel

Monterrey

INSERT

1

125

Mercedes

Tijuana

INSERT

2

126

Lily

Cancun

INSERT

2

123

null

null

DELETE

6

125

Mercedes

Guadalajara

UPDATE

6

125

Mercedes

Mexicali

UPDATE

5

123

Isabel

Chihuahua

UPDATE

5

Se você cancelar o comentário da linha final nos dados de exemplo, ele inserirá o seguinte registro que especifica onde os registros devem ser truncados:

| userId | name | city | operation | sequenceNum |
| --- | --- | --- | --- | --- |
| null | null | null | TRUNCATE | 3 |


userId

name

city

operation

sequenceNum

null

null

null

TRUNCATE

3

Observação

Todos os exemplos a seguir incluem opções para especificar operações DELETE e TRUNCATE, mas cada uma delas é opcional.

## Processar atualizações do SCD tipo 1

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#process-scd-type-1-updates)

O exemplo a seguir demonstra o processamento de atualizações SCD tipo 1:

Após executar o exemplo do SCD tipo 1, a tabela de destino contém os seguintes registros:

| userId | name | city |
| --- | --- | --- |
| 124 | Raul | Oaxaca |
| 125 | Mercedes | Guadalajara |
| 126 | Lily | Cancun |


userId

name

city

124

Raul

Oaxaca

125

Mercedes

Guadalajara

126

Lily

Cancun

Depois de executar o exemplo do SCD tipo 1 com o registro TRUNCATE adicional, os registros 124 e 126 são truncados devido à operação TRUNCATE em sequenceNum=3, e a tabela de destino contém o seguinte registro:

| userId | name | city |
| --- | --- | --- |
| 125 | Mercedes | Guadalajara |


userId

name

city

125

Mercedes

Guadalajara

## Processar atualizações do SCD tipo 2

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#process-scd-type-2-updates)

O exemplo a seguir demonstra o processamento de atualizações SCD tipo 2:

Após executar o exemplo do SCD tipo 2, a tabela de destino contém os seguintes registros:

| userId | name | city | __START_AT | __END_AT |
| --- | --- | --- | --- | --- |
| 123 | Isabel | Monterrey | 1 | 5 |
| 123 | Isabel | Chihuahua | 5 | 6 |
| 124 | Raul | Oaxaca | 1 | null |
| 125 | Mercedes | Tijuana | 2 | 5 |
| 125 | Mercedes | Mexicali | 5 | 6 |
| 125 | Mercedes | Guadalajara | 6 | null |
| 126 | Lily | Cancun | 2 | null |


userId

name

city

__START_AT

__END_AT

123

Isabel

Monterrey

1

5

123

Isabel

Chihuahua

5

6

124

Raul

Oaxaca

1

null

125

Mercedes

Tijuana

2

5

125

Mercedes

Mexicali

5

6

125

Mercedes

Guadalajara

6

null

126

Lily

Cancun

2

null

Uma query SCD tipo 2 também pode especificar um subconjunto de colunas de saída a serem rastreadas para história na tabela de destino. As alterações em outras colunas são atualizadas no local, em vez de gerar novos registros de história. O exemplo a seguir demonstra a exclusão da coluna city do acompanhamento:

O exemplo a seguir demonstra o uso do histórico de rastreamento com o SCD tipo 2:

Depois de executar este exemplo sem o registro TRUNCATE adicional, a tabela de destino conterá os seguintes registros:

| userId | name | city | __START_AT | __END_AT |
| --- | --- | --- | --- | --- |
| 123 | Isabel | Chihuahua | 1 | 6 |
| 124 | Raul | Oaxaca | 1 | null |
| 125 | Mercedes | Guadalajara | 2 | null |
| 126 | Lily | Cancun | 2 | null |


userId

name

city

__START_AT

__END_AT

123

Isabel

Chihuahua

1

6

124

Raul

Oaxaca

1

null

125

Mercedes

Guadalajara

2

null

126

Lily

Cancun

2

null

## Gerar dados de teste

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#generate-test-data)

O código abaixo é fornecido para gerar um exemplo dataset para uso nas consultas de exemplo presentes neste tutorial. Supondo que o senhor tenha as credenciais adequadas para criar um novo esquema e uma nova tabela, é possível executar essas instruções com Notebook ou Databricks SQL. O código a seguir não se destina a ser executado como parte de um Delta Live Tables pipeline:

## Exemplo: Periódico Snapshot processing

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#example-periodic-snapshot-processing)

O exemplo a seguir demonstra o processamento SCD tipo 2 que ingere o Snapshot de uma tabela armazenada em mycatalog.myschema.mytable. Os resultados do processamento são gravados em uma tabela chamada target.

mycatalog.myschema.mytable registros no registro de data e hora 2024-01-01 00:00:00

| Chave | Valor |
| --- | --- |
| 1 | a1 |
| 2 | a2 |


Chave

Valor

1

a1

2

a2

mycatalog.myschema.mytable registros no registro de data e hora 2024-01-01 12:00:00

| Chave | Valor |
| --- | --- |
| 2 | b2 |
| 3 | a3 |


Chave

Valor

2

b2

3

a3

Após o processamento do Snapshot, a tabela de destino contém os seguintes registros:

| Chave | Valor | __START_AT | __END_AT |
| --- | --- | --- | --- |
| 1 | a1 | 2024-01-01 00:00:00 | 2024-01-01 12:00:00 |
| 2 | a2 | 2024-01-01 00:00:00 | 2024-01-01 12:00:00 |
| 2 | b2 | 2024-01-01 12:00:00 | null |
| 3 | a3 | 2024-01-01 12:00:00 | null |


Chave

Valor

__START_AT

__END_AT

1

a1

2024-01-01 00:00:00

2024-01-01 12:00:00

2

a2

2024-01-01 00:00:00

2024-01-01 12:00:00

2

b2

2024-01-01 12:00:00

null

3

a3

2024-01-01 12:00:00

null

## Exemplo: Histórico Snapshot processamento

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#example-historical-snapshot-processing)



O exemplo a seguir demonstra o processamento SCD tipo 2 que atualiza uma tabela de destino com base em eventos de origem de dois Snapshot armazenados em um sistema de armazenamento cloud:

Snapshot em timestamp, armazenado em /<PATH>/filename1.csv

| Chave | TrackingColumn | NonTrackingColumn |
| --- | --- | --- |
| 1 | a1 | b1 |
| 2 | a2 | b2 |
| 4 | a4 | b4 |


Chave

TrackingColumn

NonTrackingColumn

1

a1

b1

2

a2

b2

4

a4

b4

Snapshot em timestamp + 5, armazenado em /<PATH>/filename2.csv

| Chave | TrackingColumn | NonTrackingColumn |
| --- | --- | --- |
| 2 | a2_novo | b2 |
| 3 | a3 | b3 |
| 4 | a4 | b4_new |


Chave

TrackingColumn

NonTrackingColumn

2

a2_novo

b2

3

a3

b3

4

a4

b4_new

O exemplo de código a seguir demonstra o processamento de atualizações do tipo 2 do SCD com esse Snapshot:

Após o processamento do Snapshot, a tabela de destino contém os seguintes registros:

| Chave | TrackingColumn | NonTrackingColumn | __START_AT | __END_AT |
| --- | --- | --- | --- | --- |
| 1 | a1 | b1 | 1 | 2 |
| 2 | a2 | b2 | 1 | 2 |
| 2 | a2_novo | b2 | 2 | null |
| 3 | a3 | b3 | 2 | null |
| 4 | a4 | b4_new | 1 | null |


Chave

TrackingColumn

NonTrackingColumn

__START_AT

__END_AT

1

a1

b1

1

2

2

a2

b2

1

2

2

a2_novo

b2

2

null

3

a3

b3

2

null

4

a4

b4_new

1

null

## Adicionar, alterar ou excluir dados em uma tabela de streaming de destino

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#add-change-or-delete-data-in-a-target-streaming-table)

Se o pipeline publicar tabelas no Unity Catalog, você poderá usar instruções de linguagem de manipulação de dados (DML), incluindo instruções de inserção, atualização, exclusão e merge , para modificar as tabelas de transmissão de destino criadas por instruções APPLY CHANGES INTO.

[linguagem de manipulação de dados](https://docs.databricks.com/pt/delta-live-tables/cdc.html/../sql/language-manual/index.html#dml-statements)

Observação

As declarações DML que modificam o esquema de tabela de uma tabela de streaming não são suportadas. Certifique-se de que suas instruções DML não tentem evoluir o esquema da tabela.

As instruções DML que atualizam uma tabela de transmissão podem ser executadas somente em um Unity Catalog cluster compartilhado ou em um SQL warehouse usando Databricks Runtime 13.3 LTS e acima.

Como a transmissão requer fonte de dados somente anexada, se o seu processamento exigir transmissão de uma tabela de transmissão de origem com alterações (por exemplo, por instruções DML), defina o sinalizador skipChangeCommits ao ler a tabela de transmissão de origem. Quando skipChangeCommits é definido, as transações que excluem ou modificam registros na tabela de origem são ignoradas. Caso o seu processamento não necessite de uma tabela de transmissão, você pode utilizar uma view materializada (que não possui a restrição somente de acréscimo) como tabela de destino.

[sinalizador skipChangeCommits](https://docs.databricks.com/pt/delta-live-tables/cdc.html/python-ref.html#ignore-changes)

Como o Delta Live Tables usa uma coluna SEQUENCE BY especificada e propaga os valores de sequenciamento apropriados para as colunas __START_AT e __END_AT da tabela de destino (para SCD tipo 2), é necessário garantir que as instruções DML usem valores válidos para essas colunas a fim de manter a ordenação adequada dos registros. Consulte Como o CDC é implementado com a API APPLY CHANGES?

[Como o CDC é implementado com a API APPLY CHANGES?](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#how-is-cdc-implemented)

Para obter mais informações sobre o uso de instruções DML com tabelas de transmissão, consulte Adicionar, alterar ou excluir dados em uma tabela de transmissão.

[Adicionar, alterar ou excluir dados em uma tabela de transmissão](https://docs.databricks.com/pt/delta-live-tables/cdc.html/unity-catalog.html#streaming-tables-dml-statements)

O exemplo seguinte insere um registro ativo com uma sequência inicial de 5:

## Leia um feed de dados de alterações de uma tabela de destino APPLY CHANGES

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#read-a-change-data-feed-from-an-apply-changes-target-table)

Em Databricks Runtime 15.2 e acima, o senhor pode ler um feed de dados de alteração de uma tabela de transmissão que seja o alvo de consultas APPLY CHANGES ou APPLY CHANGES FROM SNAPSHOT da mesma forma que lê um feed de dados de alteração de outras tabelas Delta. Os seguintes itens são necessários para ler o feed de dados de alteração de uma tabela de transmissão de destino:

A tabela de transmissão de destino deve ser publicada em Unity Catalog. Consulte Usar Unity Catalog com seu pipeline Delta Live Tables .

[Usar Unity Catalog com seu pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/cdc.html/unity-catalog.html)

Para ler o feed de dados de alteração da tabela de transmissão de destino, o senhor deve usar o site Databricks Runtime 15.2 ou o acima. Para ler o feed de dados de alteração em outro Delta Live Tables pipeline, o pipeline deve ser configurado para usar Databricks Runtime 15.2 ou acima.

O senhor lê o feed de dados de alteração de uma tabela de transmissão de destino criada em um Delta Live Tables pipeline da mesma forma que lê um feed de dados de alteração de outras tabelas Delta. Para saber mais sobre como usar a funcionalidade de feed de dados de alterações do Delta, incluindo exemplos em Python e SQL, consulte Usar o feed de dados de alterações do Delta Lake na Databricks.

[Usar o feed de dados de alterações do Delta Lake na Databricks](https://docs.databricks.com/pt/delta-live-tables/cdc.html/../delta/delta-change-data-feed.html)

Observação

O registro do feed de dados de alteração inclui metadados que identificam o tipo de evento de alteração. Quando um registro é atualizado em uma tabela, os metadados dos registros de alteração associados normalmente incluem valores _change_type definidos como eventos update_preimage e update_postimage.

[metadados](https://docs.databricks.com/pt/delta-live-tables/cdc.html/../delta/delta-change-data-feed.html#cdf-metadata)

No entanto, os valores _change_type serão diferentes se forem feitas atualizações na tabela de transmissão de destino que incluam a alteração dos valores primários key. Quando as alterações incluem atualizações na chave primária, os campos de metadados _change_type são definidos como eventos insert e delete. As alterações na chave primária podem ocorrer quando são feitas atualizações manuais em um dos campos key com uma instrução UPDATE ou MERGE ou, no caso de tabelas SCD tipo 2, quando o campo __start_at é alterado para refletir um valor de sequência anterior.

A consulta APPLY CHANGES determina os valores primários de key, que diferem para o processamento de SCD tipo 1 e SCD tipo 2:

Para o processamento SCD tipo 1 e a interface Delta Live Tables Python , o principal key é o valor do parâmetro keys na função apply_changes(). Para a interface Delta Live Tables SQL , a key primária são as colunas definidas pela cláusula KEYS na instrução APPLY CHANGES INTO.

Para SCD tipo 2, o key primário é o parâmetro keys ou a cláusula KEYS mais o valor de retorno das coalesce(__START_AT, __END_AT) operações, em que __START_AT e __END_AT são as colunas correspondentes da tabela de transmissão de destino.

## Obtenha dados sobre registros processados por uma consulta Delta Live Tables CDC

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#get-data-about-records-processed-by-a-delta-live-tables-cdc-query)

Observação

As métricas a seguir são capturadas apenas por consultas APPLY CHANGES e não por consultas APPLY CHANGES FROM SNAPSHOT.

As seguintes métricas são capturadas pela query APPLY CHANGES:

num_upserted_rows: o número de linhas de saída inseridas no dataset durante uma atualização.

num_deleted_rows: o número de linhas de saída existentes excluídas do dataset durante uma atualização.

A métrica num_output_rows, saída para fluxos não-CDC, não é capturada para consultas apply changes.

## Quais objetos de dados são usados para o processamento do Delta Live Tables CDC?

[](https://docs.databricks.com/pt/delta-live-tables/cdc.html/#what-data-objects-are-used-for-delta-live-tables-cdc-processing)

Observação

Essas estruturas de dados se aplicam somente ao processamento APPLY CHANGES, não ao processamento APPLY CHANGES FROM SNAPSHOT.

Essas estruturas de dados se aplicam somente quando a tabela de destino é publicada no site Hive metastore. Se um pipeline for publicado no Unity Catalog, as tabelas de apoio internas ficarão inacessíveis aos usuários.

Quando você declara a tabela de destino no Hive metastore, são criadas duas estruturas de dados:

Uma visualização usando o nome atribuído à tabela de destino.

Uma tabela de apoio interna utilizada pelas Delta Live Tables para gerenciar o processamento de CDC. Essa tabela é nomeada aplicando-se o prefixo __apply_changes_storage_ no nome da tabela de destino.

Por exemplo, se você declarar uma tabela de destino chamada dlt_cdc_target, verá uma visualização chamada dlt_cdc_target e uma tabela chamada __apply_changes_storage_dlt_cdc_target no metastore. A criação de uma view possibilita que as Delta Live Tables filtrem as informações extras (por exemplo, tombstones e versões) necessárias para lidar com dados fora de ordem. Para ver os dados processados, consulte a view de destino. Como o esquema da tabela do __apply_changes_storage_ pode mudar para suportar futuros recursos ou melhorias, você não deve consultar a tabela para uso de produção. Se você adicionar dados manualmente à tabela, os registros serão assumidos antes de outras alterações, pois as colunas da versão estão faltando.

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/cdc.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/cdc.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/cdc.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/cdc.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/cdc.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/cdc.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/cdc.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/cdc.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
