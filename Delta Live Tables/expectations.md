[Documentação](https://docs.databricks.com/pt/delta-live-tables/expectations.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/expectations.html/../data-engineering.html)

[O que é Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/expectations.html/index.html)

# Gerenciar a qualidade dos dados com o Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#manage-data-quality-with-delta-live-tables)

Você utiliza expectativas para estabelecer restrições de qualidade de dados para o conteúdo de um conjunto de dados. As expectativas permitem que você garanta que os dados que chegam às tabelas atendam aos requisitos de qualidade de dados e forneçam insights sobre a qualidade de dados para cada atualização do pipeline.Você aplica expectativas para consultas usando decoradores Python ou cláusulas de restrição SQL.

## Quais são as expectativas do Delta Live Tables?

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#what-are-delta-live-tables-expectations)

As expectativas são cláusulas opcionais que você adiciona às declarações de conjuntos de dados no Delta Live Tables, que aplicam verificações de qualidade de dados em cada registro que passa por uma consulta.

Uma expectativa consiste em três coisas:

Uma descrição, que atua como um identificador exclusivo e permite que você rastreie métricas para a restrição.

Uma instrução Boolean que sempre retorna verdadeiro ou falso com base em alguma condição declarada.

Uma ação a tomar quando um registro falha na expectativa, o que significa que o Boolean retorna falso.

A matriz a seguir mostra as três ações que você pode aplicar a registros inválidos:

| Ação | Resultado |
| --- | --- |
| avisar(default) | Registros inválidos são gravados no alvo; a falha é relatada como uma métrica para o dataset. |
| derrubar | Registros inválidos são eliminados antes que os dados sejam gravados no destino; a falha é relatada como uma métrica para o dataset. |
| falhar | Registros inválidos impedem que a atualização seja bem-sucedida. É necessária uma intervenção manual antes do reprocessamento. |


Ação

Resultado

avisar (default)

[avisar](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#retain)

Registros inválidos são gravados no alvo; a falha é relatada como uma métrica para o dataset.

derrubar

[derrubar](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#drop)

Registros inválidos são eliminados antes que os dados sejam gravados no destino; a falha é relatada como uma métrica para o dataset.

falhar

[falhar](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#fail)

Registros inválidos impedem que a atualização seja bem-sucedida. É necessária uma intervenção manual antes do reprocessamento.

você pode visualizar métricas de qualidade de dados, como o número de registros que violam uma expectativa, consultando o log de eventos do Delta Live Tables. Consulte Monitorar pipelines do Delta Live Tables.

[Monitorar pipelines do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/expectations.html/observability.html)

Para obter uma referência completa da sintaxe de declaração do dataset do Delta Live Tables, consulte Referência da linguagem Python do Delta Live Tables ou Referência da linguagem SQL do Delta Live Tables.

[Referência da linguagem Python](https://docs.databricks.com/pt/delta-live-tables/expectations.html/python-ref.html)

[Delta Live](https://docs.databricks.com/pt/delta-live-tables/expectations.html/sql-ref.html)

Observação

Embora você possa incluir várias cláusulas em qualquer expectativa, apenas o Python oferece suporte à definição de ações com base em várias expectativas. Consulte Múltiplas expectativas.

[Múltiplas expectativas](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#expect-all)

As expectativas devem ser definidas usando expressões SQL. O senhor não pode usar sintaxe não-SQL (por exemplo, funções Python) ao definir uma expectativa.

## Reter registros inválidos

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#retain-invalid-records)

Use o operador expect quando quiser manter registros que violem a expectativa. Registros que violam a expectativa são adicionados ao dataset de destino junto com registros válidos:

## Solte registros inválidos

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#drop-invalid-records)

Use o operador expect or drop para evitar o processamento adicional de registros inválidos. Os registros que violam as expectativas são descartados do dataset de destino:

## Falha em registros inválidos

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#fail-on-invalid-records)

Quando registros inválidos forem inaceitáveis, use o operador expect or fail para interromper a execução imediatamente quando um registro falhar na validação. Se a operação for uma atualização de tabela, o sistema reverte atomicamente a transação:

Importante

Se o senhor tiver vários fluxos paralelos definidos em um pipeline, a falha de um único fluxo não causará a falha de outros fluxos.

Quando um pipeline falha devido a uma violação de expectativa, é necessário corrigir o código do pipeline para lidar corretamente com os dados inválidos antes de executar o pipeline novamente.

As expectativas de falha modificam o plano de consulta Spark de suas transformações para rastrear as informações necessárias para detectar e relatar violações.Para muitas consultas, é possível usar essas informações para identificar qual registro de entrada resultou na violação. A seguir, um exemplo de exceção:

## Múltiplas expectativas

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#multiple-expectations)

Você pode definir expectativas com um ou mais critérios de qualidade de dados em pipelines Python.Esses decoradores aceitam um dicionário Python como argumento, onde a chave é o nome da expectativa e o valor é a restrição da expectativa.

Use expect_all para especificar várias restrições de qualidade de dados quando os registros que falham na validação devem ser incluídos no dataset de destino:

Utilize o expect_all_or_drop para especificar múltiplas restrições de qualidade de dados quando registros que falham na validação devem ser descartados do dataset de destino:

Use expect_all_or_fail para especificar várias restrições de qualidade de dados quando os registros que falham na validação devem interromper a execução do pipeline:

Você também pode definir uma coleção de expectativas como uma variável e passá-la para uma ou mais consultas em seu pipeline:



## Colocar dados inválidos em quarentena

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#quarantine-invalid-data)

O exemplo a seguir utiliza expectativas em combinação com tabelas e visualizações temporárias. Esse padrão oferece métricas para registros que passam pelas verificações de expectativa durante as atualizações do pipeline e proporciona uma maneira de processar registros válidos e inválidos por caminhos downstream distintos.

Observação

Este exemplo lê dados de amostra incluídos no conjunto de dadosDatabricks . Como o conjunto de dados Databricks não é compatível com um pipeline que publica em Unity Catalog, este exemplo funciona somente com um pipeline configurado para publicar em Hive metastore. No entanto, esse padrão também funciona com o pipeline habilitado para Unity Catalog, mas o senhor deve ler os dados de locais externos. Para saber mais sobre o uso do Unity Catalog com o Delta Live Tables, consulte Use o Unity Catalog com o pipeline Delta Live Tables .

[conjunto de dadosDatabricks](https://docs.databricks.com/pt/delta-live-tables/expectations.html/../discover/databricks-datasets.html#dbfs-datasets)

[locais externos](https://docs.databricks.com/pt/delta-live-tables/expectations.html/../connect/unity-catalog/cloud-storage/external-locations.html)

[Use o Unity Catalog com o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/expectations.html/unity-catalog.html)

## Validar a contagem de linhas nas tabelas

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#validate-row-counts-across-tables)

O senhor pode adicionar uma tabela adicional ao site pipeline que defina uma expectativa para comparar as contagens de linhas entre duas visualizações materializadas ou tabelas de transmissão. Os resultados dessa expectativa aparecem no evento log e na UI Delta Live Tables. O exemplo a seguir valida contagens de linhas iguais entre as tabelas tbla e tblb:

## Realize validação avançada com as expectativas do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#perform-advanced-validation-with-delta-live-tables-expectations)

O senhor pode definir a visualização materializada usando consultas agregadas e join e usar os resultados dessas consultas como parte da verificação de expectativas. Isso é útil se você quiser realizar verificações complexas de qualidade de dados, por exemplo, garantindo que uma tabela derivada contenha todos os registros da tabela de origem ou garantindo a igualdade de uma coluna numérica nas tabelas.

O seguinte exemplo valida que todos os registros esperados estão presentes na tabela report:

O exemplo a seguir usa um agregado para garantir a exclusividade de uma chave primária:

## Torne as expectativas portáteis e reutilizáveis

[](https://docs.databricks.com/pt/delta-live-tables/expectations.html/#make-expectations-portable-and-reusable)

Você pode manter as regras de qualidade de dados separadamente das implementações de pipeline.

A Databricks recomenda armazenar as regras em uma tabela Delta com cada regra categorizada por uma tag. Use essa marca nas definições de dataset para determinar quais regras devem ser aplicadas.

O exemplo seguinte cria uma tabela denominada rules para manter as regras:

O exemplo de Python a seguir define as expectativas de qualidade dos dados com base nas regras armazenadas na rules tabela. A get_rules() função lê as regras da rules tabela e retorna um dicionário Python contendo regras que correspondem ao tag argumento passado para a função. O dicionário é aplicado nos @dlt.expect_all_*() decoradores para impor restrições de qualidade de dados. Por exemplo, todos os registros que falharem nas regras marcadas com validity serão retirados da raw_farmers_market tabela:

Observação

Este exemplo lê dados de amostra incluídos no conjunto de dadosDatabricks . Como o conjunto de dados Databricks não é compatível com um pipeline que publica em Unity Catalog, este exemplo funciona somente com um pipeline configurado para publicar em Hive metastore. No entanto, esse padrão também funciona com o pipeline habilitado para Unity Catalog, mas o senhor deve ler os dados de locais externos. Para saber mais sobre o uso do Unity Catalog com o Delta Live Tables, consulte Use o Unity Catalog com o pipeline Delta Live Tables .

[conjunto de dadosDatabricks](https://docs.databricks.com/pt/delta-live-tables/expectations.html/../discover/databricks-datasets.html#dbfs-datasets)

[locais externos](https://docs.databricks.com/pt/delta-live-tables/expectations.html/../connect/unity-catalog/cloud-storage/external-locations.html)

[Use o Unity Catalog com o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/expectations.html/unity-catalog.html)

Em vez de criar uma tabela chamada rules para manter as regras, o senhor poderia criar um módulo Python para as regras principais, por exemplo, em um arquivo chamado rules_module.py na mesma pasta do site Notebook:

Em seguida, modifique o site Notebook anterior importando o módulo e alterando a função get_rules() para ler do módulo em vez de ler da tabela rules:

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/expectations.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/expectations.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/expectations.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/expectations.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/expectations.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/expectations.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/expectations.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/expectations.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
