[Documentação](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/index.html)

[Delta Live Tables referências linguísticas](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/language-references.html)

# Referência de linguagem SQL do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#delta-live-tables-sql-language-reference)

Este artigo contém detalhes sobre a interface de programação Delta Live Tables SQL .

Para obter informações sobre a API do Python, consulte a referência da linguagem Delta Live Tables Python.

[referência da linguagem Delta Live Tables Python](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/python-ref.html)

Para obter mais informações sobre comandos SQL, consulte Referência de linguagem SQL.

[Referência de linguagem SQL](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../sql/language-manual/index.html)

Você pode usar as funções definidas pelo usuário (UDFs) do Python em sua query SQL, mas deve definir essas UDFs nos arquivos Python antes de chamá-los nos arquivos de origem SQL. Consulte Funções escalares definidas pelo usuário - Python.

[Funções escalares definidas pelo usuário - Python](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../udf/python.html)

## Limitações

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#limitations)

A cláusula PIVOT não é suportada. As pivot operações em Spark requerem o carregamento ávido de dados de entrada para compute o esquema de saída. Esse recurso não é compatível com o site Delta Live Tables.

## Crie uma visualização materializada do Delta Live Tables ou uma tabela transmitida

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#create-a-delta-live-tables-materialized-view-or-streaming-table)

Observação

A sintaxe CREATE OR REFRESH LIVE TABLE para criar um view materializado está obsoleta. Em vez disso, use CREATE OR REFRESH MATERIALIZED VIEW.

Para usar a cláusula CLUSTER BY para ativar o líquido clustering, seu pipeline deve estar configurado para usar o canal de visualização.

[canal de visualização](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../release-notes/delta-live-tables/index.html#runtime-channels)

O senhor usa a mesma sintaxe básica de SQL ao declarar uma tabela de transmissão ou uma tabela materializada view.

### Declarar uma visualização materializada do Delta Live Tables com SQL

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#declare-a-delta-live-tables-materialized-view-with-sql)

A seguir, descrevemos a sintaxe para declarar um view materializado em Delta Live Tables com SQL:

### Declare a tabela de transmissão Delta Live Tables com SQL

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#declare-a-delta-live-tables-streaming-table-with-sql)

Você só pode declarar tabelas transmitidas usando query que lê contra uma fonte transmitida. Databricks recomenda o uso do Auto Loader para ingestão de transmissão de arquivos do armazenamento de objetos cloud . Consulte Sintaxe do Auto Loader SQL.

[Sintaxe do Auto Loader SQL](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#auto-loader-sql)

Ao especificar outras tabelas ou visualizações em seu site pipeline como fontes de transmissão, o senhor deve incluir a função STREAM() em torno de um nome dataset.

A seguir, descrevemos a sintaxe para declarar uma tabela de transmissão em Delta Live Tables com SQL:

## Criar uma exibição Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#create-a-delta-live-tables-view)

O seguinte descreve a sintaxe para declarar view com SQL:

## Sintaxe SQL Auto Loader

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#auto-loader-sql-syntax)

O seguinte descreve a sintaxe para trabalhar com o Auto Loader em SQL:

O senhor pode usar as opções de formato compatíveis com o Auto Loader. Usando a função map(), você pode passar opções para o método read_files(). As opções são par key-value, em que a chave e os valores são strings. Para obter detalhes sobre formatos e opções de suporte, consulte Opções de formato de arquivo.

[formato de arquivo](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../ingestion/cloud-object-storage/auto-loader/options.html#format-options)

## Exemplo: definir tabelas

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#example-define-tables)

Você pode criar um dataset lendo de uma fonte de dados externa ou de dataset definido em um pipeline. Para ler um dataset interno , anexe a palavra-chave LIVE ao nome dataset . O exemplo a seguir define dois dataset diferentes: uma tabela chamada taxi_raw que usa um arquivo JSON como fonte de entrada e uma tabela chamada filtered_data que usa a tabela taxi_raw como entrada:

## Exemplo: Ler de uma fonte transmitida

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#example-read-from-a-streaming-source)

Para ler dados de uma fonte de transmissão, por exemplo, Auto Loader ou um dataset interno, defina uma tabela STREAMING:

Para mais informações sobre dados transmitidos, consulte transformação de dados com Delta Live Tables.

[transformação de dados com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/transform.html)

## Controle como as tabelas são materializadas

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#control-how-tables-are-materialized)

As tabelas também oferecem controle adicional de sua materialização:

Especifique como as tabelas são particionadas usando PARTITIONED BY. Você pode usar o particionamento para acelerar query.

[particionadas](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#schema-partition-example)

Você pode definir as propriedades da tabela usando TBLPROPERTIES. Consulte as propriedades da tabela Delta Live Tables.

[as propriedades da tabela Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/properties.html#table-properties)

Defina um local de armazenamento usando a configuração LOCATION . Por default, os dados da tabela são armazenados no local de armazenamento do pipeline se LOCATION não estiver definido.

Você pode usar colunas geradas em sua definição de esquema. Consulte Exemplo: Especifique um esquema e colunas de partição.

[colunas geradas](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../delta/generated-columns.html)

[Exemplo: Especifique um esquema e colunas de partição](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#schema-partition-example)

Observação

Para tabelas com menos de 1 TB de tamanho, a Databricks recomenda deixar que o Delta Live Tables controle a organização dos dados. A menos que o senhor espere que sua tabela cresça além de um terabyte, a Databricks recomenda que não especifique colunas de partição.

## Exemplo: especificar um esquema e colunas de partição

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#example-specify-a-schema-and-partition-columns)

Opcionalmente, você pode especificar um esquema ao definir uma tabela. O exemplo a seguir especifica o esquema para a tabela de destino, incluindo o uso de colunas geradas pelo Delta Lake e a definição de colunas de partição para a tabela:

[de colunas geradas](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../delta/generated-columns.html)

Por default, Delta Live Tables infere o esquema da definição table se você não especificar um esquema.

## Exemplo: Definir restrições de tabela

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#example-define-table-constraints)

Observação

O suporte do Delta Live Tables para restrições de tabela está na visualização pública. Para definir restrições de tabela, seu pipeline deve ser um pipeline habilitado para o Unity Catalog e configurado para usar o canal preview.

[visualização pública](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../release-notes/release-types.html)

Ao especificar um esquema, o senhor pode definir chaves primárias e estrangeiras. As restrições são informativas e não são aplicadas. Consulte a cláusula CONSTRAINT na referência da linguagem SQL.

[cláusula CONSTRAINT](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../sql/language-manual/sql-ref-syntax-ddl-create-table-constraint.html)

O exemplo a seguir define uma tabela com uma restrição primária e estrangeira key:

## Parametrize os valores usados ao declarar tabelas ou exibições com SQL

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#parameterize-values-used-when-declaring-tables-or-views-with-sql)

Use SET para especificar um valor de configuração em uma consulta que declare uma tabela ou view, incluindo as configurações de Spark. Qualquer tabela ou view que o senhor definir em um Notebook após a instrução SET terá acesso ao valor definido. Todas as configurações de Spark especificadas com a instrução SET são usadas ao executar a consulta Spark para qualquer tabela ou view após a instrução SET. Para ler um valor de configuração em uma consulta, use a sintaxe de interpolação de cadeias ${}. O exemplo a seguir define um valor de configuração do Spark chamado startDate e usa esse valor em uma consulta:

Para especificar vários valores de configuração, use uma instrução SET separada para cada valor.

## Exemplo: Definir um filtro de linha e uma máscara de coluna

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#example-define-a-row-filter-and-column-mask)

Visualização

Os filtros de linha e as máscaras de coluna estão na Pré-visualização pública.

[Pré-visualização pública](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../release-notes/release-types.html)

Para criar uma tabela materializada view ou de transmissão com um filtro de linha e uma máscara de coluna, use a cláusula ROW FILTER e a cláusula MASK. O exemplo a seguir demonstra como definir uma tabela materializada view e uma tabela de transmissão com um filtro de linha e uma máscara de coluna:

[cláusula ROW FILTER](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../sql/language-manual/sql-ref-syntax-ddl-row-filter.html)

[cláusula MASK](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../sql/language-manual/sql-ref-syntax-ddl-column-mask.html)

Para obter mais informações sobre filtros de linha e máscaras de coluna, consulte Publicar tabelas com filtros de linha e máscaras de coluna.

[Publicar tabelas com filtros de linha e máscaras de coluna](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/unity-catalog.html#row-filters-and-column-masks)

## Propriedades SQL

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#sql-properties)

Observação

Para usar a cláusula CLUSTER BY para ativar o líquido clustering, seu pipeline deve estar configurado para usar o canal de visualização.

[canal de visualização](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../release-notes/delta-live-tables/index.html#runtime-channels)

| CREATE TABLE ou VIEW |
| --- |
| TEMPORARYCriar uma tabela, mas não publicar os metadados da tabela. A cláusulaTEMPORARYinstrui o Delta Live Tables a criar uma tabela que esteja disponível para o pipeline, mas que não deva ser acessada fora do pipeline. Para reduzir o tempo de processamento, uma tabela temporária persiste durante o tempo de vida do pipeline que a cria, e não apenas em uma única atualização. |
| STREAMINGCrie uma tabela que leia um dataset de entrada como uma transmissão. O dataset de entrada deve ser uma fonte de dados transmitida, por exemplo, Auto Loader ou uma tabelaSTREAMING. |
| CLUSTERBYHabilite o clustering líquido na tabela e defina as colunas a serem usadas como chave clustering.ConsulteUsar clusters líquidos para tabelas Delta. |
| PARTITIONEDBYUma lista opcional de uma ou mais colunas a serem usadas para particionar a tabela. |
| LOCATIONUm local de armazenamento opcional para dados da tabela. Se não for definido, o sistema assumirá default o local de armazenamento do pipeline. |
| COMMENTUma descrição opcional para a tabela. |
| column_constraintUma restrição opcional informativa primária key ou estrangeira key na coluna. |
| MASKclause(Pré-visualização pública)Adiciona uma função de máscara de coluna para tornar anônimos os dados confidenciais. As consultas futuras para essa coluna retornam o resultado da função avaliada em vez do valor original da coluna. Isso é útil para o controle de acesso refinado, pois a função pode verificar a identidade do usuário e as associações de grupo para decidir se o valor deve ser redigido.Consulte acláusula de máscara de coluna. |
| table_constraintUma restrição opcional informativa primária key ou estrangeira key na tabela. |
| TBLPROPERTIESUma lista opcional depropriedades de tabelapara a tabela. |
| WITHROWFILTERclause(Pré-visualização pública)Adiciona uma função de filtro de linha à tabela. As consultas futuras para essa tabela recebem um subconjunto das linhas para as quais a função é avaliada como TRUE. Isso é útil para o controle de acesso refinado, pois permite que a função inspecione a identidade e as associações de grupo do usuário que a invoca para decidir se deve filtrar determinadas linhas.Consulte acláusula ROW FILTER. |
| select_statementUma query Delta Live Tables que define o dataset para a tabela. |


CREATE TABLE ou VIEW

TEMPORARY

Criar uma tabela, mas não publicar os metadados da tabela. A cláusula TEMPORARY instrui o Delta Live Tables a criar uma tabela que esteja disponível para o pipeline, mas que não deva ser acessada fora do pipeline. Para reduzir o tempo de processamento, uma tabela temporária persiste durante o tempo de vida do pipeline que a cria, e não apenas em uma única atualização.

STREAMING

Crie uma tabela que leia um dataset de entrada como uma transmissão. O dataset de entrada deve ser uma fonte de dados transmitida, por exemplo, Auto Loader ou uma tabela STREAMING.

CLUSTER BY

Habilite o clustering líquido na tabela e defina as colunas a serem usadas como chave clustering.

Consulte Usar clusters líquidos para tabelas Delta.

[Usar clusters líquidos para tabelas Delta](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../delta/clustering.html)

PARTITIONED BY

Uma lista opcional de uma ou mais colunas a serem usadas para particionar a tabela.

LOCATION

Um local de armazenamento opcional para dados da tabela. Se não for definido, o sistema assumirá default o local de armazenamento do pipeline.

COMMENT

Uma descrição opcional para a tabela.

column_constraint

Uma restrição opcional informativa primária key ou estrangeira key na coluna.

MASK clause (Pré-visualização pública)

Adiciona uma função de máscara de coluna para tornar anônimos os dados confidenciais. As consultas futuras para essa coluna retornam o resultado da função avaliada em vez do valor original da coluna. Isso é útil para o controle de acesso refinado, pois a função pode verificar a identidade do usuário e as associações de grupo para decidir se o valor deve ser redigido.

Consulte a cláusula de máscara de coluna.

[cláusula de máscara de coluna](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../sql/language-manual/sql-ref-syntax-ddl-column-mask.html)

table_constraint

Uma restrição opcional informativa primária key ou estrangeira key na tabela.

TBLPROPERTIES

Uma lista opcional de propriedades de tabela para a tabela.

[propriedades de tabela](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/properties.html)

WITH ROW FILTER clause (Pré-visualização pública)

Adiciona uma função de filtro de linha à tabela. As consultas futuras para essa tabela recebem um subconjunto das linhas para as quais a função é avaliada como TRUE. Isso é útil para o controle de acesso refinado, pois permite que a função inspecione a identidade e as associações de grupo do usuário que a invoca para decidir se deve filtrar determinadas linhas.

Consulte a cláusula ROW FILTER.

[cláusula ROW FILTER](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/../sql/language-manual/sql-ref-syntax-ddl-row-filter.html)

select_statement

Uma query Delta Live Tables que define o dataset para a tabela.

| Cláusula CONSTRAINT |
| --- |
| EXPECTexpectation_nameDefina a restrição de qualidade de dadosexpectation_name. Se a restriçãoONVIOLATIONnão estiver definida, adicione as linhas que violam a restrição ao destino dataset. |
| ONVIOLATIONAção opcional a ser executada para linhas com falha:FAILUPDATE: pare imediatamente a execução do pipeline.DROPROW: Elimine o registro e continue processando. |


Cláusula CONSTRAINT

EXPECT expectation_name

Defina a restrição de qualidade de dados expectation_name. Se a restrição ON VIOLATION não estiver definida, adicione as linhas que violam a restrição ao destino dataset.

ON VIOLATION

Ação opcional a ser executada para linhas com falha:

FAIL UPDATE: pare imediatamente a execução do pipeline.

DROP ROW: Elimine o registro e continue processando.

## captura de dados de alterações (CDC) com SQL em Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/#change-data-capture-with-sql-in-delta-live-tables)

Use a instrução APPLY CHANGES INTO para usar a funcionalidade Delta Live Tables CDC, conforme descrito a seguir:

Você define restrições de qualidade de dados para um destino APPLY CHANGES usando a mesma cláusula CONSTRAINT que não éAPPLY CHANGES query. Veja como gerenciar a qualidade dos dados com Delta Live Tables.

[como gerenciar a qualidade dos dados com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/expectations.html)

Observação

O comportamento default para os eventos INSERT e UPDATE é atualizar os eventos CDC da origem: atualize todas as linhas na tabela de destino que correspondam à(s) key(s) especificada(s) ou insira uma nova linha quando um registro correspondente não existir na tabela de destino. A manipulação de eventos DELETE pode ser especificada com a condição APPLY AS DELETE WHEN .

Importante

Você deve declarar uma tabela de transmissão de destino para aplicar as alterações. Você pode opcionalmente especificar o esquema para sua tabela de destino. Ao especificar o esquema da tabela de destino APPLY CHANGES , você também deve incluir as colunas __START_AT e __END_AT com o mesmo tipo de dados do campo sequence_by .

Consulte a seção APPLY CHANGES APIs: Simplificar a captura de dados de alterações (CDC) com Delta Live Tables.

[APPLY CHANGES APIs: Simplificar a captura de dados de alterações (CDC) com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/cdc.html)

| Cláusulas |
| --- |
| KEYSA coluna ou combinação de colunas que identificam exclusivamente uma linha nos dados de origem. Isso é usado para identificar quais eventos CDC se aplicam a registros específicos na tabela de destino.Para definir uma combinação de colunas, use uma lista de colunas separadas por vírgula.Esta cláusula é necessária. |
| IGNORENULLUPDATESPermitir a ingestão de atualizações contendo um subconjunto da coluna de destino. Quando um evento CDC corresponde a uma linha existente e IGNORE NULL UPDATES é especificado, as colunas com umnullmanterão seus valores existentes no destino. Isso também se aplica a colunas aninhadas com um valor denull.Esta cláusula é opcional.O default é sobrescrever colunas existentes com valoresnull. |
| APPLYASDELETEWHENEspecifica quando um evento CDC deve ser tratado como umDELETEem vez de um upsert. Para lidar com dados fora de ordem, a linha excluída é retida temporariamente como uma marca para exclusão na tabela Delta subjacente e uma view é criada no metastore que filtra essas marcas para exclusão. O intervalo de retenção pode ser configurado com apropriedade da tabelapipelines.cdc.tombstoneGCThresholdInSeconds.Esta cláusula é opcional. |
| APPLYASTRUNCATEWHENEspecifica quando um evento CDC deve ser tratado como uma tabela completaTRUNCATE. Como essa cláusula aciona um truncamento completo da tabela de destino, ela deve ser usada apenas para casos de uso específicos que exigem essa funcionalidade.A cláusulaAPPLYASTRUNCATEWHENé compatível apenas com SCD type 1. SCD type 2 não é compatível com as operações truncate.Esta cláusula é opcional. |
| SEQUENCEBYO nome da coluna que especifica a ordem lógica dos eventos CDC nos dados de origem. Delta Live Tables usa esse sequenciamento para lidar com eventos de alteração que chegam fora de ordem.A coluna especificada deve ser um tipo de dados classificável.Esta cláusula é necessária. |
| COLUMNSEspecifica um subconjunto de colunas a serem incluídas na tabela de destino. Você também pode:Especifique a lista completa de colunas a serem incluídas:COLUMNS(userId,name,city).Especifique uma lista de colunas a serem excluídas:COLUMNS*EXCEPT(operation,sequenceNum)Esta cláusula é opcional.O default é incluir todas as colunas na tabela de destino quando a cláusulaCOLUMNSnão for especificada. |
| STOREDASSe os registros devem ser armazenados como SCD tipo 1 ou SCD tipo 2.Esta cláusula é opcional.O default é SCD tipo 1. |
| TRACKHISTORYONEspecifica um subconjunto de colunas de saída para gerar registros de história quando houver alterações nessas colunas especificadas. Você também pode:Especifique a lista completa de colunas a serem rastreadas:COLUMNS(userId,name,city).Especifique uma lista de colunas a serem excluídas do acompanhamento:COLUMNS*EXCEPT(operation,sequenceNum)Essa cláusula é opcional. O default é para rastrear a história de todas as colunas de saída quando houver alguma alteração, equivalente aTRACKHISTORYON*. |


Cláusulas

KEYS

A coluna ou combinação de colunas que identificam exclusivamente uma linha nos dados de origem. Isso é usado para identificar quais eventos CDC se aplicam a registros específicos na tabela de destino.

Para definir uma combinação de colunas, use uma lista de colunas separadas por vírgula.

Esta cláusula é necessária.

IGNORE NULL UPDATES

Permitir a ingestão de atualizações contendo um subconjunto da coluna de destino. Quando um evento CDC corresponde a uma linha existente e IGNORE NULL UPDATES é especificado, as colunas com um null manterão seus valores existentes no destino. Isso também se aplica a colunas aninhadas com um valor de null.

Esta cláusula é opcional.

O default é sobrescrever colunas existentes com valores null.

APPLY AS DELETE WHEN

Especifica quando um evento CDC deve ser tratado como um DELETE em vez de um upsert. Para lidar com dados fora de ordem, a linha excluída é retida temporariamente como uma marca para exclusão na tabela Delta subjacente e uma view é criada no metastore que filtra essas marcas para exclusão. O intervalo de retenção pode ser configurado com a propriedade da tabela pipelines.cdc.tombstoneGCThresholdInSeconds .

[propriedade da tabela](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/properties.html#table-properties)

Esta cláusula é opcional.

APPLY AS TRUNCATE WHEN

Especifica quando um evento CDC deve ser tratado como uma tabela completa TRUNCATE. Como essa cláusula aciona um truncamento completo da tabela de destino, ela deve ser usada apenas para casos de uso específicos que exigem essa funcionalidade.

A cláusula APPLY AS TRUNCATE WHEN é compatível apenas com SCD type 1. SCD type 2 não é compatível com as operações truncate.

Esta cláusula é opcional.

SEQUENCE BY

O nome da coluna que especifica a ordem lógica dos eventos CDC nos dados de origem. Delta Live Tables usa esse sequenciamento para lidar com eventos de alteração que chegam fora de ordem.

A coluna especificada deve ser um tipo de dados classificável.

Esta cláusula é necessária.

COLUMNS

Especifica um subconjunto de colunas a serem incluídas na tabela de destino. Você também pode:

Especifique a lista completa de colunas a serem incluídas: COLUMNS (userId, name, city).

Especifique uma lista de colunas a serem excluídas: COLUMNS * EXCEPT (operation, sequenceNum)

Esta cláusula é opcional.

O default é incluir todas as colunas na tabela de destino quando a cláusula COLUMNS não for especificada.

STORED AS

Se os registros devem ser armazenados como SCD tipo 1 ou SCD tipo 2.

Esta cláusula é opcional.

O default é SCD tipo 1.

TRACK HISTORY ON

Especifica um subconjunto de colunas de saída para gerar registros de história quando houver alterações nessas colunas especificadas. Você também pode:

Especifique a lista completa de colunas a serem rastreadas: COLUMNS (userId, name, city).

Especifique uma lista de colunas a serem excluídas do acompanhamento: COLUMNS * EXCEPT (operation, sequenceNum)

Essa cláusula é opcional. O default é para rastrear a história de todas as colunas de saída quando houver alguma alteração, equivalente a TRACK HISTORY ON *.

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/sql-ref.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
