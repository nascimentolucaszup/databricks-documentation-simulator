[Documentação](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/index.html)

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/configure-pipeline.html)

# Configurar a computação para um pipeline do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#configure-compute-for-a-delta-live-tables-pipeline)

Este artigo contém instruções e considerações sobre a configuração de definições personalizadas do compute para o pipeline Delta Live Tables.

O pipeline sem servidor não fornece as opções de configuração do compute. Consulte Configurar um pipeline Delta Live Tables sem servidor.

[Configurar um pipeline Delta Live Tables sem servidor](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/serverless-dlt.html)

## Selecionar uma política de cluster

[](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#select-a-cluster-policy)

Os usuários devem ter permissão para implantar o compute para configurar e atualizar o pipeline Delta Live Tables. Os administradores do workspace podem configurar a política de cluster para fornecer aos usuários acesso a compute recurso para Delta Live Tables. Consulte Definir limites em Delta Live Tables pipeline compute .

[Definir limites em Delta Live Tables pipeline compute .](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/../admin/clusters/policy-definition.html#dlt)

Observação

política de cluster são opcionais. Verifique com seu administrador workspace se o senhor não possui os privilégios compute necessários para Delta Live Tables.

Para garantir que os valores da política de cluster default sejam aplicados corretamente, defina apply_policy_default_values como true nas configurações decluster  em sua configuração de pipeline:

[configurações decluster](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#cluster-config)

## Configurar a tag do cluster

[](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#configure-cluster-tags)

O senhor pode usar o Cluster Tag para monitorar o uso do seu pipeline clusters. Adicione a tag de cluster na interface do usuário Delta Live Tables ao criar ou editar um pipeline ou ao editar as configurações JSON do seu pipeline clusters.

[Cluster Tag](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/../compute/configure.html#tags)

## Selecione os tipos de instância para executar a pipeline

[](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#select-instance-types-to-run-a-pipeline)

Em default, Delta Live Tables seleciona os tipos de instância para o driver de pipelinee os nós de worker. Opcionalmente, você pode configurar os tipos de instância.

Por exemplo, selecione tipos de instância para melhorar o desempenho do pipeline ou resolver problemas de memória ao executar o pipeline. O senhor pode configurar os tipos de instância ao criar ou editar um pipeline com a API REST ou na UI do Delta Live Tables.

[criar](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/https://docs.databricks.com/api/workspace/pipelines/create)

[editar](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/https://docs.databricks.com/api/workspace/pipelines/update)

Para configurar os tipos de instância quando o senhor criar ou editar um pipeline na interface do usuário do Delta Live Tables:

Clique no botão Configurações.

Na seção Advanced das configurações do site pipeline, nos menus suspensos worker type e Driver type, selecione os tipos de instância para o site pipeline.

## Configurações avançadas de computação

[](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#advanced-compute-configurations)

Observação

Como compute recurso é totalmente gerenciado para serverless pipeline DLT, compute configurações não estão disponíveis quando o senhor seleciona serverless para um pipeline.

Cada pipeline do Delta Live Tables tem dois clusters associados:

O cluster updates processa as atualizações do pipeline.

O maintenance cluster executa a tarefa de manutenção diária.

As configurações de computação especificadas usando a UI de configuração workspace pipeline se aplicam tanto à atualização quanto à manutenção clusters. O senhor deve editar a configuração JSON para modificar essas configurações de forma independente.

A configuração que esses clusters usam é determinada pelo atributo clusters especificado em suas configurações de pipeline.

Usando cluster rótulo, o senhor pode adicionar compute configurações que se aplicam somente a um tipo cluster específico. Há três rótulos que o senhor pode usar ao configurar o site pipeline clusters:

Observação

A configuração do rótulo do cluster pode ser omitida se o senhor definir apenas uma configuração de cluster. O rótulo default é aplicado às configurações de cluster se nenhuma configuração para o rótulo for fornecida. A configuração do rótulo do cluster é necessária somente se o senhor precisar personalizar as configurações para diferentes tipos de cluster.

O rótulo default define compute configurações para updates e maintenance clusters. A aplicação das mesmas configurações em ambos os sites clusters aumenta a confiabilidade da execução da manutenção, garantindo que as configurações necessárias, como as credenciais de acesso aos dados de um local de armazenamento, sejam aplicadas à manutenção cluster.

O rótulo maintenance define as configurações do compute que se aplicam somente ao maintenance cluster. O senhor também pode usar o rótulo maintenance para substituir as configurações definidas pelo rótulo default.

O rótulo updates define configurações que se aplicam somente ao cluster updates. Use-a para definir configurações que não devem ser aplicadas ao cluster maintenance.

As configurações definidas usando o rótulo default e updates são mescladas para criar a configuração final para o updates cluster. Se a mesma configuração for definida usando os rótulos default e updates, a configuração definida com o rótulo updates substituirá a configuração definida com o rótulo default.

O exemplo a seguir define um parâmetro de configuração do Spark que é adicionado somente à configuração do cluster updates:

Delta Live Tables O senhor tem opções semelhantes para as configurações do cluster como outros compute no Databricks. Como outras configurações de pipeline, o senhor pode modificar a configuração JSON dos clusters para especificar opções que não estão presentes na interface do usuário. Consulte Computação.

[Computação](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/../compute/index.html)

Observação

Como o tempo de execução do Delta Live Tables gerencia o ciclo de vida do pipeline clusters e executa uma versão personalizada do Databricks Runtime, o senhor não pode definir manualmente algumas configurações do cluster em uma configuração do pipeline, como a versão do Spark ou os nomes do cluster. Consulte Atributos de cluster que não podem ser definidos pelo usuário.

[Atributos de cluster que não podem ser definidos pelo usuário](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/properties.html#non-settable-attrs)

### Configurar tipos de instância para clusters de atualização e manutenção

[](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#configure-instance-types-for-update-and-maintenance-clusters)

Para configurar os tipos de instância nas configurações JSON do pipeline, clique no botão JSON e insira as configurações do tipo de instância na configuração do cluster:

Observação

Para evitar a atribuição de um recurso desnecessário ao maintenance cluster, este exemplo usa o rótulo updates para definir os tipos de instância apenas para o updates cluster. Para atribuir os tipos de instância aos clusters updates e maintenance, use o rótulo default ou omita a configuração do rótulo. O rótulo default é aplicado às configurações de cluster de pipeline se nenhuma configuração para o rótulo for fornecida. Consulte Configurações avançadas do site compute .

[Configurações avançadas do site compute](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#cluster-config)

### Atrasar o desligamento da computação

[](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#delay-compute-shutdown)

Para controlar o comportamento de desligamento do cluster, o senhor pode usar o modo de desenvolvimento ou produção ou usar a configuração pipelines.clusterShutdown.delay na configuração do pipeline. O exemplo a seguir define o valor pipelines.clusterShutdown.delay como 60 segundos:

Quando o modo production está ativado, o valor default para pipelines.clusterShutdown.delay é 0 seconds. Quando o modo development está ativado, o valor default é 2 hours.

Observação

Como um cluster Delta Live Tables é desligado automaticamente quando não está em uso, a referência a uma política de cluster que define autotermination_minutes em sua configuração de cluster resulta em erro.

### Criar um cluster de nó único

[](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/#create-a-single-node-cluster)

Se o senhor definir num_workers como 0 nas configurações de clustering, o clustering será criado como um clustering de nó único. A configuração de um cluster de autoescala e a definição de min_workers como 0 e max_workers como 0 criam um cluster de nó único.

[clustering de nó único](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/../compute/configure.html#single-node)

Se o senhor configurar um clustering de autoescala e definir apenas min_workers como 0, o clustering não será criado como um clustering de nó único. O clustering tem pelo menos um worker ativo em todos os momentos até ser encerrado.

Um exemplo de configuração de clustering para criar um clustering de nó único em Delta Live Tables:

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/configure-compute.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
