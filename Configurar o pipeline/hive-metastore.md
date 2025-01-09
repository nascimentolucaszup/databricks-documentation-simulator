[Documentação](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/index.html)

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/configure-pipeline.html)

# Use o pipeline Delta Live Tables com o legado Hive metastore

[](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/#use-delta-live-tables-pipelines-with-legacy-hive-metastore)

Este artigo detalha as configurações e advertências específicas do pipeline Delta Live Tables configurado para publicar dados no legado Hive metastore. Databricks recomenda o uso do site Unity Catalog para todos os novos pipelines. Consulte Usar Unity Catalog com seu pipeline Delta Live Tables .

[Usar Unity Catalog com seu pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/unity-catalog.html)

## Publicar o conjunto de dados pipeline no legado Hive metastore

[](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/#publish-pipeline-datasets-to-the-legacy-hive-metastore)

Embora seja opcional, o senhor deve especificar um destino para publicar tabelas criadas pelo seu pipeline sempre que for além do desenvolvimento e do teste de um novo pipeline. A publicação de um pipeline em um destino torna o conjunto de dados disponível para consulta em qualquer lugar do seu ambiente Databricks.

O senhor pode tornar os dados de saída do seu pipeline detectáveis e disponíveis para consulta publicando o conjunto de dados no Hive metastore. Para publicar o conjunto de dados no metastore, insira um nome de esquema no campo Target (Destino ) quando o senhor criar um pipeline. O senhor também pode adicionar um banco de dados de destino a um pipeline existente.

[Hive metastore](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/../archive/external-metastores/external-hive-metastore.html)

Todas as tabelas e visualizações criadas em Delta Live Tables são locais para o pipeline por default. O senhor deve publicar tabelas em um esquema de destino para consultar ou usar o conjunto de dados Delta Live Tables fora do pipeline no qual elas são declaradas.

Para publicar tabelas do seu pipeline em Unity Catalog, consulte Use Unity Catalog with your Delta Live Tables pipeline.

[Use Unity Catalog with your Delta Live Tables pipeline](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/unity-catalog.html)

## Como publicar o conjunto de dados Delta Live Tables no legado Hive metastore

[](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/#how-to-publish-delta-live-tables-datasets-to-the-legacy-hive-metastore)

O senhor pode declarar um esquema de destino para todas as tabelas em seu Delta Live Tables pipeline usando o campo Target schema (Esquema de destino ) nas configurações do pipeline e em Create pipeline UIs.

O senhor também pode especificar um esquema em uma configuração JSON definindo o valor target.

O senhor deve executar uma atualização para que o site pipeline publique os resultados no esquema de destino.

O senhor pode usar esse recurso com várias configurações de ambiente para publicar em diferentes esquemas com base no ambiente. Por exemplo, você pode publicar em um esquema dev para desenvolvimento e um esquema prod para dados de produção.

## Como consultar tabelas de transmissão e visualizações materializadas no legado Hive metastore

[](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/#how-to-query-streaming-tables-and-materialized-views-in-the-legacy-hive-metastore)

Após a conclusão da atualização, o senhor pode acessar view o esquema e as tabelas, consultar os dados ou usar os dados em aplicativos downstream.

Depois de publicadas, as tabelas do Delta Live Tables podem ser consultadas em qualquer ambiente com acesso ao esquema de destino. Isso inclui o Databricks SQL, o Notebook e outros pipelines do Delta Live Tables.

Importante

Quando você cria uma configuração target, somente tabelas e metadados associados são publicados. não são publicadas no metastore.

## Especifique um local de armazenamento

[](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/#specify-a-storage-location)

O senhor pode especificar um local de armazenamento para um pipeline que é publicado no site Hive metastore. A principal motivação para especificar um local é controlar o local de armazenamento de objetos para os dados gravados pelo pipeline.

Como todas as tabelas, dados, pontos de verificação e metadados do pipeline Delta Live Tables são totalmente gerenciados por Delta Live Tables, a maior parte da interação com o conjunto de dados Delta Live Tables ocorre por meio de tabelas registradas em Hive metastore ou Unity Catalog.

## Configuração do armazenamento em nuvem

[](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/#cloud-storage-configuration)

O senhor usa o perfil da instância AWS para configurar o acesso ao armazenamentoS3 em AWS. Para adicionar um instance profile na interface do usuário Delta Live Tables quando o senhor criar ou editar um pipeline:

[armazenamentoS3 em AWS](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/../connect/storage/tutorial-s3-instance-profile.html)

Na página de detalhes do pipeline do seu pipeline, clique no botão Settings (Configurações ).

No menu suspenso do perfil da instância Na seção de computação das configurações do pipeline, selecione um instance profile.

Para configurar um AWS instance profile editando as configurações do JSON para o seu pipeline clusters, clique no botão JSON e insira a configuração instance profile no campo aws_attributes.instance_profile_arn da configuração cluster:

O senhor também pode configurar o perfil da instância ao criar a política de cluster para o pipeline Delta Live Tables. Para ver um exemplo, consulte a base de conhecimento.

[base de conhecimento](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/https://kb.databricks.com/clusters/set-instance-profile-arn-optional-policy)

## Exemplo pipeline código-fonte Notebook para o espaço de trabalho sem Unity Catalog

[](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/#example-pipeline-source-code-notebooks-for-workspaces-without-unity-catalog)

O senhor pode importar o seguinte Notebook para um Databricks workspace sem o Unity Catalog habilitado e usá-lo para implantar um Delta Live Tables pipeline. Importe o Notebook do idioma escolhido e especifique o caminho no campo Código-fonte ao configurar um pipeline com a opção de armazenamento Hive metastore opção de armazenamento. Consulte Configurar um pipeline do Delta Live Tables.

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/configure-pipeline.html)

### Comece a usar o notebook Python Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/#get-started-with-delta-live-tables-python-notebook)

Abra o bloco de anotações em outra guia   Copiar link para importação

[Abra o bloco de anotações em outra guia](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html//_extras/notebooks/source/dlt-wikipedia-python.html)

![Copiar para a área de transferência](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html//_static/clippy.svg)

### Comece a usar o notebook SQL Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/#get-started-with-delta-live-tables-sql-notebook)

Abra o bloco de anotações em outra guia   Copiar link para importação

[Abra o bloco de anotações em outra guia](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html//_extras/notebooks/source/dlt-wikipedia-sql.html)

![Copiar para a área de transferência](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html//_static/clippy.svg)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/hive-metastore.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
