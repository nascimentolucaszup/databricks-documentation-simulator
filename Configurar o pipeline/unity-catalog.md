[Documentação](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/index.html)

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/configure-pipeline.html)

# Use o Unity Catalog com seus pipelines Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#use-unity-catalog-with-your-delta-live-tables-pipelines)

Visualização

O suporte ao Delta Live Tables para Unity Catalog está em Visualização pública.

[Visualização pública](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../release-notes/release-types.html)

Databricks Recomenda configurar o pipeline Delta Live Tables com Unity Catalog.

O pipeline configurado com Unity Catalog publica todas as visualizações materializadas definidas e tabelas de transmissão no catálogo e no esquema especificados. Unity Catalog O pipeline pode ler de outras tabelas e volumes do site Unity Catalog.

Para gerenciar permissões nas tabelas criadas por um pipeline do Unity Catalog, use GRANT e REVOKE.

[GRANT e REVOKE](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../data-governance/unity-catalog/manage-privileges/index.html)

## Requisitos

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#requirements)

Permissões necessárias para criar tabelas no Unity Catalog a partir de um pipeline do Delta Live Tables:

USE CATALOG privilégios no catálogo de destino.

CREATE MATERIALIZED VIEW e USE SCHEMA privilégios no esquema de destino se o site pipeline criar uma visualização materializada.

[visualização materializada](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/index.html#dlt-datasets)

CREATE TABLE e USE SCHEMA privilégios no esquema de destino se o site pipeline criar tabelas de transmissão.

[tabelas de transmissão](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/index.html#dlt-datasets)

Se um esquema de destino não for especificado nas configurações do pipeline, você deverá ter privilégios CREATE MATERIALIZED VIEW ou CREATE TABLE em pelo menos um esquema no catálogo de destino.

computação necessária para executar um Unity Catalog-enabled pipeline:

Modo de acesso compartilhado clusters. Um pipeline habilitado para o Unity Catalog não pode ser executado em um único usuário ("atribuído") cluster. Consulte Limitações do modo de acesso compartilhado no Unity Catalog.

[Limitações do modo de acesso compartilhado no Unity Catalog](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../compute/access-mode-limitations.html#shared-limitations)

A computação necessária para consultar tabelas criadas por um Delta Live Tables pipeline usando Unity Catalog (incluindo tabelas de transmissão e visualização materializada) inclui qualquer um dos seguintes itens:

SQL warehouses

Modo de acesso compartilhado clusters em Databricks Runtime 13.3 LTS ou acima.

Modo de acesso de usuário único (ou "atribuído") clusters, se o controle de acesso refinado estiver ativado no usuário único cluster (ou seja, o cluster está em execução no Databricks Runtime 15.4 ou acima e o serverless compute está ativado para o workspace). Para obter mais informações, consulte Controle de acesso refinado em um único usuário compute.

[Controle de acesso refinado em um único usuário compute](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../compute/single-user-fgac.html)

Modo de acesso de usuário único (ou "atribuído") clusters em 13.3 LTS até 15.3, somente se o proprietário da tabela executar a consulta.

Aplicam-se limitações adicionais ao site compute. Consulte a seção a seguir.

## Limitações

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#limitations)

Veja a seguir as limitações ao usar o Unity Catalog com Delta Live Tables:

Por default, somente o proprietário do pipeline e os administradores do workspace podem view o driver logs do cluster que executa um Unity Catalog habilitado pipeline. Para permitir que outros usuários acessem o driver,logs consulte Permitir que usuários não administradores view acessem o driver logs de um Unity Catalog pipeline habilitado.

[que usuários não administradores view acessem o driver logs de um Unity Catalog pipeline](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/privileges.html#driver-log-permissions)

Os pipelines existentes que usam o Hive metastore não podem ser atualizados para usar o Unity Catalog. Para migrar um pipeline existente que grava no Hive metastore, você deve criar um novo pipeline e reingerir dados da fonte de dados(s).

O senhor não pode criar um Unity Catalog-enabled pipeline em um workspace anexado a um metastore que foi criado durante o Unity Catalog Public Preview. Consulte Atualizar para herança de privilégios.

[Atualizar para herança de privilégios](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../data-governance/unity-catalog/manage-privileges/upgrade-privilege-model.html)

Os JARs não são suportados. Somente a Python biblioteca de terceiros é compatível. Consulte gerenciar as dependências do Python para o pipeline do Delta Live Tables .

[gerenciar as dependências do Python para o pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/external-dependencies.html)

query de linguagem de manipulação de dados (DML) que modificam o esquema de uma tabela de transmissão não são suportadas.

Um view materializado criado em um Delta Live Tables pipeline não pode ser usado como fonte de transmissão fora desse pipeline, por exemplo, em outro pipeline ou em um Notebook downstream.

Se um pipeline for publicado em um esquema com um local de armazenamento gerenciado, o esquema poderá ser alterado em uma atualização subsequente, mas somente se o esquema atualizado usar o mesmo local de armazenamento que o esquema especificado anteriormente.

As tabelas são armazenadas no local de armazenamento do esquema de destino. Se um local de armazenamento do esquema não for especificado, as tabelas serão armazenadas no local de armazenamento do catálogo. Se os locais de armazenamento do esquema e do catálogo não forem especificados, as tabelas serão armazenadas no local de armazenamento raiz do metastore.

A história do Catalog Explorer tab não mostra a história da visualização materializada.

A propriedade LOCATION não é suportada ao definir uma tabela.

Os pipelines habilitados para Unity Catalog não podem publicar no Hive metastore.

O suporte ao Python UDF está em Public Preview.

[Public Preview](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../release-notes/release-types.html)

O senhor não pode usar Delta Sharing com uma Delta Live Tables materializada view ou uma tabela de transmissão publicada em Unity Catalog.

[Delta Sharing](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../delta-sharing/index.html)

Você não pode usar a função com valor de tabela event_log em um pipeline ou query para acessar os logs de eventos de vários pipelines.

[função com valor de tabela](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/observability.html#event-log-with-uc)

Você não pode compartilhar uma view criada na função de valor de tabela event_log com outros usuários.

[função de valor de tabela](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/observability.html#event-log-with-uc)

Observação

Os arquivos subjacentes que suportam view materializada podem incluir dados de tabelas upstream (incluindo possíveis informações de identificação pessoal) que não aparecem na definição view materializada. Esses dados são adicionados automaticamente ao armazenamento subjacente para oferecer suporte à atualização incremental da view materializada.

Como os arquivos subjacentes de uma view materializada podem expor dados de tabelas upstream que não fazem parte do esquema view materializada, o Databricks recomenda não compartilhar o armazenamento subjacente com consumidores downstream não confiáveis.

Por exemplo, suponha que uma definição materializada do site view inclua uma cláusula COUNT(DISTINCT field_a). Embora a definição do view materializado inclua apenas a cláusula aggregate COUNT DISTINCT, os arquivos subjacentes conterão uma lista dos valores reais de field_a.

## Posso usar o pipeline Hive metastore e Unity Catalog juntos?

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#can-i-use-hive-metastore-and-unity-catalog-pipelines-together)

Seu workspace pode conter um pipeline que usa o Unity Catalog e o legado Hive metastore. No entanto, um único pipeline não pode gravar nos sites Hive metastore e Unity Catalog. O pipeline existente que grava no site Hive metastore não pode ser atualizado para usar o site Unity Catalog.

Os pipelines existentes que não usam Unity Catalog não são afetados pela criação de um novo pipeline configurado com Unity Catalog. Esses pipelines continuam a manter os dados no site Hive metastore usando o local de armazenamento configurado.

A menos que especificado de outra forma neste documento, todas as funcionalidades existentes de fonte de dados e Delta Live Tables são compatíveis com pipelines que usam o Unity Catalog. As interfaces Python e SQL são compatíveis com pipelines que usam o Unity Catalog.

[Python](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/python-ref.html)

[SQL](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/sql-ref.html)

## Mudanças na funcionalidade existente

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#changes-to-existing-functionality)

Quando o Delta Live Tables é configurado para persistir dados no Unity Catalog, o ciclo de vida da tabela é gerenciado pelo pipeline do Delta Live Tables. Porque o pipeline gerencia o ciclo de vida e as permissões da tabela:

Quando uma tabela é removida da definição Delta Live Tables pipeline , a entrada correspondente da tabela materializada view ou de transmissão é removida de Unity Catalog na próxima atualização pipeline. Os dados reais são retidos por um período para que possam ser recuperados se excluídos por engano. Os dados podem ser recuperados adicionando a tabela materializada view ou de transmissão novamente à definição pipeline.

A exclusão do pipeline Delta Live Tables resulta na exclusão de todas as tabelas definidas nesse pipeline. Devido a essa alteração, a UI do Delta Live Tables foi atualizada para solicitar que o senhor confirme a exclusão de um pipeline.

As tabelas de apoio internas, incluindo aquelas usadas para suportar APPLY CHANGES INTO, não são diretamente acessíveis pelos usuários.

## Gravar tabelas no Unity Catalog a partir de um pipeline Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#write-tables-to-unity-catalog-from-a-delta-live-tables-pipeline)

Observação

Se o senhor não selecionar um catálogo e um esquema de destino para um pipeline, as tabelas não serão publicadas no Unity Catalog e só poderão ser acessadas por consultas no mesmo pipeline.

Para gravar suas tabelas em Unity Catalog, o senhor deve configurar seu pipeline para trabalhar com ele por meio de seu workspace. Quando o senhor criar um pipeline, selecione Unity Catalog em Storage options (Opções de armazenamento), selecione um catálogo no menu suspenso Catalog (Catálogo ) e selecione um esquema existente ou digite o nome de um novo esquema no menu suspenso Target schema (Esquema de destino ). Para saber mais sobre os catálogos do Unity Catalog, consulte O que são catálogos no Databricks? Para saber mais sobre esquemas no Unity Catalog, consulte O que são esquemas no Databricks?

[criar um pipeline](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/configure-pipeline.html)

[O que são catálogos no Databricks?](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../catalogs/index.html)

[O que são esquemas no Databricks?](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../schemas/index.html)

## Ingerir dados em um pipeline do Unity Catalog

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#ingest-data-into-a-unity-catalog-pipeline)

Seu pipeline configurado para usar o Unity Catalog pode ler dados de:

Unity Catalog gerenciado e tabelas externas, view, view materializada e tabelas transmitidas.

Tabelas e view Hive metastore.

Auto Loader usando a função read_files() para ler de locais externos Unity Catalog .

Apache Kafka e Amazon Kinesis.

Veja a seguir exemplos de leitura do Unity Catalog e tabelas Hive metastore .

### ingestão de lotes de uma tabela do Unity Catalog

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#batch-ingestion-from-a-unity-catalog-table)

### alterações transmitidas de uma tabela Unity Catalog

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#stream-changes-from-a-unity-catalog-table)

### Ingerir dados do Hive metastore

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#ingest-data-from-hive-metastore)

Um pipeline que usa Unity Catalog pode ler dados de tabelas Hive metastore usando o catálogo hive_metastore:

### Ingerir dados do Auto Loader

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#ingest-data-from-auto-loader)

## Compartilhar visão materializada

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#share-materialized-views)

Por default, somente o proprietário de pipeline tem permissão para consultar o conjunto de dados criado por pipeline. O senhor pode conceder a outros usuários a capacidade de consultar uma tabela usando instruções GRANT e pode revogar o acesso à consulta usando instruções REVOKE. Para obter mais informações sobre privilégios em Unity Catalog, consulte gerenciar privilégios em Unity Catalog.

[GRANT](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../sql/language-manual/security-grant.html)

[REVOKE](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../sql/language-manual/security-revoke.html)

[gerenciar privilégios em Unity Catalog](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../data-governance/unity-catalog/manage-privileges/index.html)

### Conceder select em uma tabela

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#grant-select-on-a-table)

### Revogar seleção em uma tabela

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#revoke-select-on-a-table)

## Conceder privilégios para criar tabela ou criar visualização materializada

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#grant-create-table-or-create-materialized-view--privileges)

## Exibir a linhagem de um pipeline

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#view-lineage-for-a-pipeline)

A linhagem das tabelas em um pipeline do Delta Live Tables é visível no Catalog Explorer. A interface de usuário de linhagem do Catalog Explorer mostra as tabelas upstream e downstream da exibição materializada ou das tabelas de transmissão em um Unity Catalog habilitado pipeline. Para saber mais sobre Unity Catalog a linhagem, consulte Captura e view linhagem de dados Unity Catalog usando.

[Captura e view linhagem de dados Unity Catalog](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../data-governance/unity-catalog/data-lineage.html)

Para uma view materializada ou tabela de transmissão em um pipeline Delta Live Tables habilitado para Catálogo do Unity, a UI de linhagem do Catalog Explorer também se vinculará ao pipeline que produziu a view materializada ou tabela de transmissão se o pipeline estiver acessível no workspace atual.

## Adicionar, alterar ou excluir dados em uma tabela transmitida

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#add-change-or-delete-data-in-a-streaming-table)

O senhor pode usar instruções de linguagem de manipulação de dados (DML), incluindo instruções de inserção, atualização, exclusão e merge, para modificar as tabelas de transmissão publicadas em Unity Catalog. O suporte a consultas DML em tabelas de transmissão permite casos de uso como a atualização de tabelas para compliance com o Regulamento Geral de Proteção de Dados (GDPR) (GDPR).

[de linguagem de manipulação de dados](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../sql/language-manual/index.html#dml-statements)

Observação

As instruções DML que modificam o esquema de tabela de uma tabela de transmissão não são suportadas. Certifique-se de que suas instruções DML não tentem evoluir o esquema da tabela.

As instruções DML que atualizam uma tabela de transmissão podem ser executadas somente em um Unity Catalog cluster compartilhado ou em um SQL warehouse usando Databricks Runtime 13.3 LTS e acima.

Como a transmissão requer fonte de dados somente anexada, se o seu processamento exigir transmissão de uma tabela de transmissão de origem com alterações (por exemplo, por instruções DML), defina o sinalizador skipChangeCommits ao ler a tabela de transmissão de origem. Quando skipChangeCommits é definido, as transações que excluem ou modificam registros na tabela de origem são ignoradas. Caso o seu processamento não necessite de uma tabela de transmissão, você pode utilizar uma view materializada (que não possui a restrição somente de acréscimo) como tabela de destino.

[sinalizador skipChangeCommits](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/python-ref.html#ignore-changes)

A seguir estão exemplos de instruções DML para modificar registros em uma tabela de transmissão.

### Excluir registros com um ID específico:

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#delete-records-with-a-specific-id)

### Atualizar registros com um ID específico:

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#update-records-with-a-specific-id)

## Publicar tabelas com filtros de linha e máscaras de coluna

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#publish-tables-with-row-filters-and-column-masks)

Visualização

Este recurso está em prévia pública.

[prévia pública](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../release-notes/release-types.html)

Os filtros de linha permitem que o senhor especifique uma função que se aplica como um filtro sempre que uma varredura de tabela obtém linhas. Esses filtros garantem que as consultas subsequentes retornem apenas linhas para as quais o predicado do filtro seja avaliado como verdadeiro.

[Os filtros de linha](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../sql/language-manual/sql-ref-syntax-ddl-row-filter.html)

As máscaras de coluna permitem mascarar os valores de uma coluna sempre que uma varredura de tabela busca linhas. Consultas futuras para essa coluna retornam o resultado da função avaliada em vez do valor original da coluna. Para obter mais informações sobre o uso de filtros de linha e máscaras de coluna, consulte Filtro sensível à tabela uso de dados filtros de linha e máscaras de coluna.

[As máscaras de coluna](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../sql/language-manual/sql-ref-syntax-ddl-column-mask.html)

[Filtro sensível à tabela uso de dados filtros de linha e máscaras de coluna](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/../tables/row-and-column-filters.html)

### Gerenciamento de filtros de linha e máscaras de coluna

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#managing-row-filters-and-column-masks)

Os filtros de linha e as máscaras de coluna na visualização materializada e nas tabelas de transmissão devem ser adicionados, atualizados ou eliminados por meio do comando CREATE OR REFRESH.

Para obter uma sintaxe detalhada sobre a definição de tabelas com filtros de linha e máscaras de coluna, consulte Referência de linguagem SQL do Delta Live Tables e Referência de linguagem Python do Delta Live Tables.

[Referência de linguagem SQL do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/sql-ref.html)

[Referência de linguagem Python do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/python-ref.html)

### Comportamento

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#behavior)

A seguir, detalhes importantes sobre o uso de filtros de linha ou máscaras de coluna no pipeline Delta Live Tables:

Atualizar como proprietário: quando uma atualização pipeline atualiza uma tabela materializada view ou de transmissão, as funções de filtro de linha e máscara de coluna são executadas com os direitos do proprietário pipeline. Isso significa que a tabela refresh usa o contexto de segurança do usuário que criou o pipeline. As funções que verificam o contexto do usuário (como CURRENT_USER e IS_MEMBER) são avaliadas usando o contexto do usuário do proprietário do pipeline.

Consulta: Ao consultar uma tabela materializada view ou de transmissão, as funções que verificam o contexto do usuário (como CURRENT_USER e IS_MEMBER) são avaliadas usando o contexto do usuário do invocador. Essa abordagem impõe controles de acesso e segurança de dados específicos do usuário com base no contexto do usuário atual.

Ao criar uma visualização materializada sobre tabelas de origem que contêm filtros de linha e máscaras de coluna, o site refresh da visualização materializada view é sempre um site completo refresh. Um refresh completo reprocessa todos os dados disponíveis na fonte com as definições mais recentes. Esse processo verifica se as políticas de segurança nas tabelas de origem são avaliadas e aplicadas com os dados e as definições mais atualizados.

### Observabilidade

[](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/#observability)

Use DESCRIBE EXTENDED, INFORMATION_SCHEMA ou o Catalog Explorer para examinar os filtros de linha e as máscaras de coluna existentes que se aplicam a uma determinada tabela materializada view ou de transmissão. Essa funcionalidade permite que os usuários auditem e revisem o acesso aos dados e as medidas de proteção na visualização materializada e nas tabelas de transmissão.

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/unity-catalog.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
