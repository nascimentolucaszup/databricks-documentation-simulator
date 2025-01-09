[Documentação](https://docs.databricks.com/pt/delta-live-tables/index.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/index.html/../data-engineering.html)

# O que é o Delta Live Tables?

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#what-is-delta-live-tables)

O Delta Live Tables é uma estrutura declarativa para a criação de pipelines de processamento de dados confiáveis, passíveis de manutenção e teste. Você especifica as transformações a serem aplicadas aos seus dados, e o Delta Live Tables cuida da orquestração de tarefas, do gerenciamento de clusters, do monitoramento, da qualidade dos dados e do tratamento de erros.

Em vez de definir seu pipeline de dados usando uma série de tarefas Apache Spark separadas, você define tabelas de transmissão e exibição materializada que o sistema deve criar e manter atualizado. Delta Live Tables gerencia como seus dados são transformados com base na consulta que você define para cada passo de processamento. Você também pode impor qualidade de dados com as expectativas do Delta Live Tables, que permitem definir a qualidade de dados esperada e especificar como lidar com registros que falham nessas expectativas.

Para saber mais sobre os benefícios de criar e executar seus pipelines de ETL com o Delta Live Tables, consulte a página do produto Delta Live Tables.

[a página do produto Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/https://www.databricks.com/product/delta-live-tables)

## O que são conjuntos de dados do Delta Live Tables?

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#what-are-delta-live-tables-datasets)

Os conjuntos de dados Delta Live Tables são tabelas de transmissão, exibições materializadas e exibições mantidas como resultados de consultas declarativas. A tabela a seguir descreve como cada conjunto de dados é processado:

| Tipo de dataset | Como os registros são processados por meio de consultas definidas? |
| --- | --- |
| Tabela de transmissão | Cada registro é processado exatamente uma vez. Isso pressupõe uma origem somente de acréscimo. |
| Visualização materializada | Os registros são processados conforme necessário para retornar resultados precisos para o estado atual dos dados. A visualização materializada deve ser usada para tarefas de processamento de dados, como transformações, agregações ou pré-computação de consultas lentas e cálculos usados com frequência. |
| View | Os registros são processados sempre que a exibição é consultada. Use modos de exibição para transformações intermediárias e verificações de qualidade de dados que não devem ser publicadas em conjuntos de dados públicos. |


Tipo de dataset

Como os registros são processados por meio de consultas definidas?

Tabela de transmissão

Cada registro é processado exatamente uma vez. Isso pressupõe uma origem somente de acréscimo.

Visualização materializada

Os registros são processados conforme necessário para retornar resultados precisos para o estado atual dos dados. A visualização materializada deve ser usada para tarefas de processamento de dados, como transformações, agregações ou pré-computação de consultas lentas e cálculos usados com frequência.

View

Os registros são processados sempre que a exibição é consultada. Use modos de exibição para transformações intermediárias e verificações de qualidade de dados que não devem ser publicadas em conjuntos de dados públicos.

As seções a seguir fornecem descrições mais detalhadas de cada tipo dataset . Para saber mais sobre como selecionar tipos dataset para implementar seus requisitos de processamento de dados, consulte Quando usar exibições, exibições materializadas e tabelas transmitidas.

[Quando usar exibições, exibições materializadas e tabelas transmitidas](https://docs.databricks.com/pt/delta-live-tables/index.html/transform.html#tables-vs-views)

### Tabela de transmissão

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#streaming-table)

Uma tabela de transmissão é uma tabela Delta com suporte extra para transmissão ou processamento incremental de dados. As tabelas de transmissão permitem que você processe um dataset crescente, manipulando cada linha apenas uma vez. Como a maioria dos conjuntos de dados cresce continuamente ao longo do tempo, as tabelas de transmissão são boas para a maioria das cargas de trabalho de ingestão. As tabelas de transmissão são ideais para pipelines que exigem atualização de dados e baixa latência. As tabelas de transmissão também podem ser úteis para transformações em grande escala, pois os resultados podem ser calculados incrementalmente à medida que novos dados chegam, mantendo os resultados atualizados sem a necessidade de recalcular completamente todos os dados de origem a cada atualização.As tabelas de transmissão foram projetadas para fontes de dados que são somente anexadas.

Observação

Embora, por default, as tabelas de transmissão requeiram fonte de dados apenas anexada, quando uma fonte de transmissão é outra tabela de transmissão que requer atualizações ou exclusões, você pode substituir esse comportamento com o sinalizador skipChangeCommits.

[sinalizador skipChangeCommits](https://docs.databricks.com/pt/delta-live-tables/index.html/python-ref.html#ignore-changes)

### Visualização materializada

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#materialized-view)

Um  viewmaterializado é um view em que os resultados foram pré-computados. As visualizações materializadas são atualizadas de acordo com o programa de atualização do site pipeline no qual estão contidas. As visualizações materializadas são poderosas porque podem lidar com qualquer alteração na entrada. Cada vez que o site pipeline é atualizado, os resultados da consulta são recalculados para refletir as alterações no conjunto de dados upstream que podem ter ocorrido devido a compliance, correções, agregações ou CDC geral. Delta Live Tables implementa a visualização materializada como tabelas Delta, mas abstrai as complexidades associadas à aplicação eficiente de atualizações, permitindo que os usuários se concentrem em escrever consultas.

### Visualizações

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#views)

Todas as exibições no Databricks calculam os resultados dos datasets de origem à medida que são consultados, aproveitando as otimizações de cache quando disponíveis. O Delta Live Tables não publica visualizações no catálogo, portanto, as visualizações podem ser referenciadas somente no pipeline em que foram definidas. As visualizações são úteis como consultas intermediárias que não devem ser expostas a usuários finais ou sistemas. A Databricks recomenda o uso de exibições para impor restrições de qualidade de dados ou transformar e enriquecer conjuntos de dados que geram várias consultas downstream.

## Declarar seus primeiros conjuntos de dados no Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#declare-your-first-datasets-in-delta-live-tables)

O Delta Live Tables apresenta uma nova sintaxe para Python e SQL. Para saber os conceitos básicos da sintaxe do pipeline, consulte Desenvolver código de pipeline com Python e Desenvolver código de pipeline com SQL.

[Desenvolver código de pipeline com Python](https://docs.databricks.com/pt/delta-live-tables/index.html/python-dev.html)

[Desenvolver código de pipeline com SQL.](https://docs.databricks.com/pt/delta-live-tables/index.html/sql-dev.html)

Observação

O Delta Live Tables separa as definições dataset do processamento de atualização, e o Delta Live Tables Notebook não se destina à execução interativa. Consulte O que é um pipeline Delta Live Tables?.

[O que é um pipeline Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/index.html/#pipeline)

## O que é um pipeline Delta Live Tables?

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#what-is-a-delta-live-tables-pipeline)

Um pipeline é a unidade principal usada para configurar e executar fluxos de trabalho de processamento de dados com o Delta Live Tables.

Um pipeline contém visualizações materializadas e tabelas de fluxo declaradas em arquivos fonte Python ou SQL. O Delta Live Tables inferem as dependências entre essas tabelas, garantindo que as atualizações ocorram na ordem correta. Para cada dataset, o Delta Live Tables compara o estado atual com o estado desejado e avança para criar ou atualizar conjuntos de dados usando métodos de processamento eficazes.

As configurações de pipelines do Delta Live Tables se enquadram em duas grandes categorias:

Configurações que definem uma coleção de Notebook ou arquivos (conhecidos como código-fonte) que usam a sintaxe Delta Live Tables para declarar o conjunto de dados.

Configurações que controlam a infraestrutura do pipeline, o gerenciamento de dependências, como as atualizações são processadas e como as tabelas são salvas no workspace.

A maioria das configurações é opcional, mas algumas exigem atenção cuidadosa, especialmente ao configurar pipelines de produção. Isso inclui o seguinte:

Para disponibilizar dados fora do pipeline, você deve declarar um esquema de destino para publicar no Hive metastore ou um catálogo de destino e um esquema de destino para publicar no Unity Catalog.

As permissões de acesso aos dados são configuradas por meio do cluster usado para execução. Certifique-se de que seu cluster tenha as permissões apropriadas configuradas para as fontes de dados e o local de armazenamento de destino, se especificado.

Para obter detalhes sobre como usar Python e SQL para escrever código-fonte para pipelines, consulte Referência de linguagem SQL Delta Live Tables e Referência de linguagem Python Delta Live Tables.

[Referência de linguagem SQL Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/sql-ref.html)

[Referência de linguagem Python Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/python-ref.html)

Para obter mais informações sobre definições e configurações de pipeline, consulte Configurar um pipeline do Delta Live Tables.

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/configure-pipeline.html)

## Implemente seu primeiro pipeline e acione atualizações

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#deploy-your-first-pipeline-and-trigger-updates)

Antes de processar dados com Delta Live Tables, você deve configurar um pipeline. Depois que um pipeline é configurado, você pode acionar uma atualização para calcular os resultados de cada conjunto de dados em seu pipeline. Para começar a usar pipelines do Delta Live Tables, consulte Tutorial: Execute seu primeiro pipeline do Delta Live Tables.

[Tutorial: Execute seu primeiro pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/tutorial-pipelines.html)

## O que é uma atualização de pipeline?

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#what-is-a-pipeline-update)

Os pipelines implementam a infraestrutura e recalculam o estado dos dados quando você inicia uma atualização. Uma atualização executa as seguintes ações:

Inicia um cluster com a configuração correta.

Descobre todas as tabelas e visualizações definidas e verifica a existência de erros de análise, como nomes de colunas inválidos, dependências ausentes e erros de sintaxe.

Cria ou atualiza tabelas e visualizações com os dados mais recentes disponíveis.

Os pipelines podem ser executados continuamente ou em um cronograma, dependendo dos requisitos de custo e latência do seu caso de uso. Consulte Executar uma atualização em um pipeline do Delta Live Tables.

[Executar uma atualização em um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/updates.html)

## Ingerir dados com o Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#ingest-data-with-delta-live-tables)

O Delta Live Tables é compatível com todas as fontes de dados disponíveis no Databricks.

O Databricks recomenda o uso de tabelas de transmissão para a maioria dos casos de uso de ingestão. Para arquivos que chegam ao armazenamento de objetos na nuvem, a Databricks recomenda o Auto Loader. Você pode ingerir dados diretamente com o Delta Live Tables da maioria dos barramentos de mensagens.

Para obter mais informações sobre como configurar o acesso ao armazenamento cloud, consulte Configuração do armazenamento em nuvem.

[Configuração do armazenamento em nuvem](https://docs.databricks.com/pt/delta-live-tables/index.html/hive-metastore.html#configure-cloud-storage)

Para formatos não compatíveis pelo Auto Loader, você pode usar Python ou SQL para consultar qualquer formato suportado pelo Apache Spark. Consulte Carregar dados com o Delta Live Tables.

[Carregar dados com o Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/load.html)

## Monitora e reforça a qualidade dos dados

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#monitor-and-enforce-data-quality)

Você pode utilizar expectativas para especificar controles de qualidade de dados no conteúdo de um conjunto de dados. Diferentemente de uma restrição CHECK em um banco de dados tradicional, que impede a adição de registros que não atendam à restrição, as expectativas oferecem flexibilidade ao processar dados que não atendem aos requisitos de qualidade de dados. Essa flexibilidade permite processar e armazenar dados que você espera que sejam confusos e dados que precisam atender a requisitos rigorosos de qualidade. Consulte Gerenciar a qualidade dos dados com o Delta Live Tables.

[Gerenciar a qualidade dos dados com o Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/expectations.html)

## Como é o Delta Live Tables e Delta Lake estão relacionadas?

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#how-are-delta-live-tables-and-delta-lake-related)

Delta Live Tables estende a funcionalidade do Delta Lake. Como as tabelas criadas e gerenciadas pelas Delta Live Tables são tabelas Delta, elas têm as mesmas garantias e recursos fornecidos pela Delta Lake. Veja O que é Delta Lake?.

[O que é Delta Lake?](https://docs.databricks.com/pt/delta-live-tables/index.html/../delta/index.html)

O Delta Live Tables adiciona várias propriedades de tabela, além das muitas propriedades de tabela que podem ser definidas no Delta Lake. Consulte Referência de propriedades do Delta Live Tables  e referência de propriedades da tabela Delta.

[Referência de propriedades do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/properties.html)

[referência de propriedades da tabela Delta](https://docs.databricks.com/pt/delta-live-tables/index.html/../delta/table-properties.html)

## Como as tabelas são criadas e gerenciadas pelo Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#how-tables-are-created-and-managed-by-delta-live-tables)

O Databricks gerencia automaticamente as tabelas criadas com o Delta Live Tables, determinando como as atualizações precisam ser processadas para calcular corretamente o estado atual de uma tabela e realizando uma série de tarefas de manutenção e otimização.

Para a maioria das operações, você deve permitir que Delta Live Tables processe todas as atualizações, inserções e exclusões em uma tabela de destino. Para obter detalhes e limitações, consulte Manter exclusões ou atualizações manuais.

[Manter exclusões ou atualizações manuais](https://docs.databricks.com/pt/delta-live-tables/index.html/transform.html#manual-ddl)

## Tarefas de manutenção executadas pelo Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#maintenance-tasks-performed-by-delta-live-tables)

Delta Live Tables executa tarefas de manutenção dentro de 24 horas após a atualização de uma tabela. A manutenção pode melhorar o desempenho query e reduzir custos removendo versões antigas de tabelas. Por default, o sistema executa uma operação OPTIMIZE completa seguida de VACUUM. Você pode desabilitar OPTIMIZE para uma tabela definindo pipelines.autoOptimize.managed = false nas propriedades da tabela para a tabela. As tarefas de manutenção são executadas somente se uma atualização de pipeline tiver execução nas 24 horas antes das tarefas de manutenção serem agendadas.

[OPTIMIZE](https://docs.databricks.com/pt/delta-live-tables/index.html/../sql/language-manual/delta-optimize.html)

[VACUUM](https://docs.databricks.com/pt/delta-live-tables/index.html/../sql/language-manual/delta-vacuum.html)

[propriedades da tabela](https://docs.databricks.com/pt/delta-live-tables/index.html/properties.html#table-properties)

## Limitações

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#limitations)

Aplicam-se as seguintes limitações:

Todas as tabelas criadas e atualizadas por Delta Live Tables são tabelas Delta.

Delta Lake As consultas de viagem do tempo são compatíveis apenas com tabelas de transmissão e não são compatíveis com visualizações materializadas. Consulte Work with Delta Lake table história.

[Work with Delta Lake table história](https://docs.databricks.com/pt/delta-live-tables/index.html/../delta/history.html)

As tabelas do Delta Live Tables só podem ser definidas uma vez, o que significa que elas só podem ser o alvo de uma única operação em todos os pipelines do Delta Live Tables.

As colunas de identidade não são compatíveis com tabelas que são o alvo do APPLY CHANGES INTO e podem ser recalculadas durante as atualizações da visualização materializada. Por esse motivo, o site Databricks recomenda o uso de colunas de identidade em Delta Live Tables somente com tabelas de transmissão. Veja as colunas de identidade de uso em Delta Lake.

[as colunas de identidade de uso em Delta Lake](https://docs.databricks.com/pt/delta-live-tables/index.html/../delta/generated-columns.html#identity)

Um workspace do Databricks é limitado a 100 atualizações de pipeline simultâneas.

Para obter uma lista dos requisitos e limitações específicos do uso do Delta Live Tables com o Unity Catalog, consulte Use Unity Catalog with your Delta Live Tables pipeline

[Use Unity Catalog with your Delta Live Tables pipeline](https://docs.databricks.com/pt/delta-live-tables/index.html/unity-catalog.html)

## Recursos adicionais

[](https://docs.databricks.com/pt/delta-live-tables/index.html/#additional-resources)

O Delta Live Tables tem suporte total na API REST da Databricks. Consulte API DLT.

[API DLT](https://docs.databricks.com/pt/delta-live-tables/index.html/https://docs.databricks.com/api/workspace/pipelines)

Para configurações de pipeline e tabela, consulte Referência de propriedades do Delta Live Tables.

[Referência de propriedades do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/properties.html)

Referência da linguagem SQL do Delta Live Tables.

[Referência da linguagem SQL do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/sql-ref.html)

Referência da linguagem Python do Delta Live Tables.

[Referência da linguagem Python do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/index.html/python-ref.html)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/index.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/index.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/index.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/index.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/index.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/index.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/index.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/index.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
