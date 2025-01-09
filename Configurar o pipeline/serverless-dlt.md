[Documentação](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/index.html)

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/configure-pipeline.html)

# Configurar um pipeline Delta Live Tables sem servidor

[](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#configure-a-serverless-delta-live-tables-pipeline)

Este artigo descreve as configurações do pipeline serverless Delta Live Tables .

Databricks recomenda o desenvolvimento de um novo pipeline usando o site serverless. Algumas cargas de trabalho podem exigir a configuração do compute clássico ou o trabalho com o Hive metastore legado. Consulte Configurar compute para um Delta Live Tables pipelinee Usar o pipeline Delta Live Tables com o legado Hive metastore.

[Configurar compute para um Delta Live Tables pipelinee](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/configure-compute.html)

[Usar o pipeline Delta Live Tables com o legado Hive metastore](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/hive-metastore.html)

Observação

O pipeline sem servidor sempre usa Unity Catalog. O Unity Catalog para Delta Live Tables está em visualização pública e tem algumas limitações. Consulte Usar Unity Catalog com seu pipeline Delta Live Tables .

[Usar Unity Catalog com seu pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/unity-catalog.html)

O senhor não pode adicionar manualmente as configurações de compute em um objeto clusters na configuração de JSON para um serverless pipeline. Tentar fazer isso resulta em um erro.

Para obter informações sobre elegibilidade e habilitação para o pipeline serverless DLT, consulte Enable serverless compute .

[Enable serverless compute .](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../admin/workspace-settings/serverless.html)

Se o senhor precisar usar uma conexão AWS PrivateLink com o pipeline serverless DLT, entre em contato com o representante Databricks.

## Requisitos

[](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#requirements)

Seu workspace deve ter o Unity Catalog ativado para usar o pipeline serverless.

O senhor deve ter aceitado os termos de uso do serverless.

[termos de uso](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../admin/sql/serverless.html#accept-terms)

Seu site workspace deve estar em uma região habilitada paraserverless.

[região habilitada paraserverless.](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../resources/feature-region-support.html#serverless-aws)

## Configuração recomendada para o pipeline serverless

[](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#recommended-configuration-for-serverless-pipelines)

Importante

A permissão de criação de cluster não é necessária para configurar o pipeline serverless. Por meio do default, todos os usuários do workspace podem usar o pipeline serverless.

O pipeline sem servidor remove a maioria das opções de configuração, pois Databricks gerencia toda a infraestrutura. Para configurar um serverless pipeline, faça o seguinte:

Clique em Delta Live Tables na barra lateral.

Clique em Create pipeline (Criar pipeline).

Forneça um nome exclusivo para o pipeline.

Marque a caixa ao lado de sem servidor.

(Opcional) Use o seletor de arquivos  para configurar os arquivos do Notebook e workspace como código-fonte.

![Ícone do seletor de arquivos](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../_images/file-picker.png)

Se o senhor não adicionar nenhum código-fonte, será criado um novo Notebook para o site pipeline. O Notebook é criado em um novo diretório no seu diretório de usuário, e um link para acessar esse Notebook é mostrado no campo Código-fonte no painel de detalhes do pipeline após a criação do pipeline.

Um link para acessar esse Notebook está presente no campo Código-fonte, no painel de detalhes do pipeline, depois que o senhor criar seu pipeline.

Use o botão Add source code (Adicionar código-fonte ) para adicionar código-fonte ativo adicional.

Selecione um catálogo para publicar dados.

Selecione um esquema no catálogo. Todas as tabelas de transmissão e visualizações materializadas definidas no site pipeline são criadas nesse esquema.

Clique em Criar.

Essas configurações recomendadas criam um novo pipeline configurado para execução no modo Triggered e o canal Current. Essa configuração é recomendada para muitos casos de uso, incluindo desenvolvimento e teste, e é adequada para cargas de trabalho de produção que devem ser executadas em um programador. Para obter detalhes sobre o pipeline de programação, consulte Delta Live Tables pipeline tarefa for Job.

[Delta Live Tables pipeline tarefa for Job](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../jobs/pipeline.html)

O senhor também pode converter o pipeline existente configurado com Unity Catalog para usar serverless. Consulte Converter um pipeline existente para usar o serverless.

[Converter um pipeline existente para usar o serverless](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#convert)

## Outras considerações de configuração

[](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#other-configuration-considerations)

As seguintes opções de configuração também estão disponíveis para o pipeline serverless:

O senhor pode optar por usar o modo Contínuo pipeline ao executar o pipeline na produção. Consulte Modo de pipeline acionado vs. contínuo.

[Modo de pipeline acionado vs. contínuo](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/pipeline-mode.html)

Adicionar notificações para atualizações do site email com base em condições de sucesso ou falha. Consulte Adicionar notificações email para eventos pipeline .

[Adicionar notificações email para eventos pipeline](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/observability.html#notifications)

Use o campo Configuration para definir o valor keypara o pipeline. Essas configurações têm duas finalidades:

Defina parâmetros arbitrários que você pode referenciar em seu código-fonte. Consulte Usar parâmetros com o pipeline Delta Live Tables .

[Usar parâmetros com o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/parameters.html)

Configurar as definições do pipeline e as configurações do Spark. Consulte a referência das propriedades do Delta Live Tables.

[referência das propriedades do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/properties.html)

Use o canal Preview para testar seu pipeline em relação às alterações pendentes de tempo de execução do Delta Live Tables e testar novos recursos.

### Política orçamentária

[](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#budget-policy)

Visualização

Esse recurso está em Prévia Pública.

[Prévia Pública](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../release-notes/release-types.html)

As políticas de orçamento permitem que sua organização aplique tags personalizadas no uso do serverless para atribuição de faturamento granular. Depois de marcar a caixa de seleção sem servidor, a configuração da política de orçamento é exibida, onde o senhor pode selecionar a política que deseja aplicar ao pipeline. O tags é herdado da política orçamentária e só pode ser editado pelos administradores do workspace.

Observação

Após a atribuição de uma política de orçamento ao senhor, seus pipelines existentes não são automaticamente marcados com a política. O senhor deve atualizar manualmente os pipelines existentes se quiser anexar uma política a eles.

Para obter mais informações sobre políticas orçamentárias, consulte Atributo serverless uso com políticas orçamentárias.

[Atributo serverless uso com políticas orçamentárias](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../admin/usage/budget-policies.html)

## sem servidor pipeline recurso

[](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#serverless-pipeline-features)

Além de simplificar a configuração, o pipeline serverless tem o seguinte recurso:

Incremental refresh para visualização materializada: As atualizações da visualização materializada são atualizadas de forma incremental sempre que possível. O Incremental refresh tem os mesmos resultados que a recomputação completa. A atualização usa um refresh completo se os resultados não puderem ser computados de forma incremental. Consulte Incremental refresh para visualização materializada.

[Incremental refresh para visualização materializada](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../optimizations/incremental-refresh.html)

pipeline de transmissão: Para melhorar a utilização, a taxa de transferência e a latência das cargas de trabalho de transmissão de dados, como a ingestão de dados, os microbatches são um pipeline. Em outras palavras, em vez de executar microbatches sequencialmente como o padrão Spark transmissão estructurada, o pipeline serverless DLT executa microbatches simultaneamente, melhorando a utilização do recurso compute. O pipeline de transmissão é ativado por default em serverless pipeline DLT.

Escala automática vertical: serverless O pipeline DLT acrescenta à autoescala horizontal fornecida pela autoescala aprimorada Databricks alocando automaticamente os tipos de instância mais econômicos que podem executar seu Delta Live Tables pipeline sem falhar devido a erros de falta de memória. Consulte O que é a escala automática vertical?

[O que é a escala automática vertical?](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#vertical-autoscaling)

## O que é a escala automática vertical?

[](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#what-is-vertical-autoscaling)

serverless A autoescala vertical do pipeline DLT aloca automaticamente os tipos de instância disponíveis mais econômicos para executar suas atualizações Delta Live Tables pipeline sem falhar devido a erros de falta de memória. A escala automática vertical aumenta quando são necessários tipos de instância maiores para executar uma atualização do pipeline e também diminui quando determina que a atualização pode ser executada com tipos de instância menores. A escala automática vertical determina se os nós do driver, os nós do worker ou os nós do driver e do worker devem ser dimensionados para cima ou para baixo.

A autoescala vertical é usada em todo o pipeline DLT do site serverless, incluindo o pipeline usado pela visualização materializada e pelas tabelas de transmissão do site Databricks SQL.

A autoescala vertical funciona detectando atualizações do pipeline que falharam devido a erros de falta de memória. A autoescala vertical aloca tipos de instância maiores quando essas falhas são detectadas com base nos dados fora da memória coletados da atualização com falha. No modo de produção, uma nova atualização que usa o novo compute recurso é iniciada automaticamente. No modo de desenvolvimento, o novo recurso compute é usado quando o senhor começa manualmente uma nova atualização.

Se a autoescala vertical detectar que a memória das instâncias alocadas está sendo subutilizada de forma consistente, ela reduzirá os tipos de instância a serem usados na próxima atualização do site pipeline.

## Converta um pipeline existente para usar o serverless

[](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#convert-an-existing-pipeline-to-use-serverless)

O senhor pode converter o pipeline existente configurado com Unity Catalog para o pipeline serverless. Complete os seguintes passos:

Clique em Delta Live Tables na barra lateral.

Clique no nome do pipeline desejado na lista.

Clique em Configurações.

Marque a caixa ao lado de sem servidor.

Clique em Save and Começar.

Importante

Quando o senhor habilita o serverless, todas as configurações do compute que tiver configurado para um pipeline são removidas. Se o senhor mudar um pipeline de volta para atualizações que não sejam doserverless, deverá reconfigurar as configurações desejadas do compute para a configuração do pipeline.

## Como posso encontrar o uso de DBU de um pipeline sem servidor?

[](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/#how-can-i-find-the-dbu-usage-of-a-serverless-pipeline)

O senhor pode encontrar o uso DBU do pipeline serverless DLT consultando a tabela de uso faturável, parte das tabelas do sistema Databricks. Consulte Qual é o consumo de DBU de um pipeline DLT sem servidor?

[Qual é o consumo de DBU de um pipeline DLT sem servidor?](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/../admin/system-tables/billing.html#serverless-dlt-cost)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/serverless-dlt.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
