[Documentação](https://docs.databricks.com/pt/delta-live-tables/parameters.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/parameters.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/parameters.html/index.html)

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/parameters.html/configure-pipeline.html)

# Usar parâmetros com o pipeline Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/parameters.html/#use-parameters-with-delta-live-tables-pipelines)

Este artigo explica como o senhor pode usar as configurações do Delta Live Tables pipeline para parametrizar o código pipeline.

## Parâmetros de referência

[](https://docs.databricks.com/pt/delta-live-tables/parameters.html/#reference-parameters)

Durante as atualizações, o código-fonte do pipeline pode acessar os parâmetros do pipeline usando a sintaxe para obter valores para as configurações do Spark.

O senhor faz referência aos parâmetros do pipeline usando o key. O valor é injetado em seu código-fonte como uma cadeia de caracteres antes da avaliação da lógica do código-fonte.

A sintaxe do exemplo a seguir usa um parâmetro com key source_catalog e valor dev_catalog para especificar a fonte de dados de um site materializado view:

## Definir parâmetros

[](https://docs.databricks.com/pt/delta-live-tables/parameters.html/#set-parameters)

Passe parâmetros para o pipeline passando parâmetros arbitrários key-value como configurações para o pipeline. O senhor pode definir parâmetros ao definir ou editar uma configuração pipeline usando a UI workspace ou JSON. Consulte Configurar um pipeline do Delta Live Tables.

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/parameters.html/configure-pipeline.html)

A chave de parâmetro do pipeline só pode conter _ - . ou caracteres alfanuméricos. Os valores dos parâmetros são definidos como strings.

Os parâmetros do pipeline não são compatíveis com valores dinâmicos. O senhor deve atualizar o valor associado a um key na configuração do pipeline.

Importante

Não use palavras-chave que entrem em conflito com valores reservados de configuração do pipeline ou do Apache Spark.

## Parametrizar declarações de conjuntos de dados em Python ou SQL

[](https://docs.databricks.com/pt/delta-live-tables/parameters.html/#parameterize-dataset-declarations-in-python-or-sql)

Os códigos Python e SQL que definem seu conjunto de dados podem ser parametrizados pelas configurações do pipeline. A parametrização permite os seguintes casos de uso:

Separando caminhos longos e outras variáveis do seu código.

Reduzir a quantidade de dados processados em ambientes de desenvolvimento ou de teste para acelerar os testes.

Reutilizar a mesma lógica de transformações para processar a partir de várias fontes de dados.

O exemplo a seguir usa o valor de configuração startDate para limitar o pipeline de desenvolvimento a um subconjunto dos dados de entrada:

## Controle a fonte de dados com parâmetros

[](https://docs.databricks.com/pt/delta-live-tables/parameters.html/#control-data-sources-with-parameters)

O senhor pode usar os parâmetros do pipeline para especificar diferentes fontes de dados em diferentes configurações do mesmo pipeline.

Por exemplo, o senhor pode especificar caminhos diferentes nas configurações de desenvolvimento, teste e produção para um pipeline usando a variável data_source_path e, em seguida, fazer referência a ela usando o código a seguir:

Esse padrão é benéfico para testar como a lógica de ingestão pode lidar com esquemas ou dados malformados durante a ingestão inicial. O senhor pode usar o código idêntico em todo o site pipeline em todos os ambientes, alternando o conjunto de dados.

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/parameters.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/parameters.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/parameters.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/parameters.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/parameters.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/parameters.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/parameters.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/parameters.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
