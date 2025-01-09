[Documentação](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/index.html)

# Configurar um pipeline do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#configure-a-delta-live-tables-pipeline)

Este artigo descreve a configuração básica do pipeline Delta Live Tables usando a UI workspace.

Databricks recomenda o desenvolvimento de um novo pipeline usando o site serverless. Para obter instruções de serverless configuração para serverless Delta Live Tables pipeline o pipeline, consulte Configurar um pipeline .

[configuração para serverless Delta Live Tables pipeline](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/serverless-dlt.html)

As instruções de configuração neste artigo usam o endereço Unity Catalog. Para obter instruções sobre como configurar o pipeline com o legado Hive metastore, consulte Usar o pipeline Delta Live Tables com o legado Hive metastore.

[Usar o pipeline Delta Live Tables com o legado Hive metastore](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/hive-metastore.html)

Observação

A interface do usuário tem uma opção para exibir e editar configurações em JSON. O senhor pode definir a maioria das configurações com a interface do usuário ou com uma especificação JSON. Algumas opções avançadas só estão disponíveis usando a configuração JSON.

JSON Os arquivos de configuração também são úteis ao implantar o pipeline em novos ambientes ou ao usar o CLI ou o REST API.

[REST API](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/https://docs.databricks.com/api/workspace/pipelines)

Para obter uma referência completa sobre as definições de configuração JSON do Delta Live Tables, consulte Configurações de pipeline do Delta Live Tables.

[Configurações de pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/properties.html#config-settings)

## Configurar um novo pipeline do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#configure-a-new-delta-live-tables-pipeline)

Para configurar um novo pipeline do Delta Live Tables, faça o seguinte:

Clique em Delta Live Tables na barra lateral.

Clique em Create pipeline (Criar pipeline).

Forneça um nome exclusivo para o pipeline.

(Opcional) Use o seletor de arquivos  para configurar os arquivos do Notebook e workspace como código-fonte.

![Ícone do seletor de arquivos](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/../_images/file-picker.png)

Se o senhor não adicionar nenhum código-fonte, será criado um novo Notebook para o site pipeline. O Notebook é criado em um novo diretório no seu diretório de usuário, e um link para acessar esse Notebook é mostrado no campo Código-fonte no painel de detalhes do pipeline após a criação do pipeline.

O senhor pode acessar esse Notebook com o URL apresentado no campo Código-fonte no painel de detalhes do pipeline depois de criar seu pipeline.

Use o botão Add source code (Adicionar código-fonte ) para adicionar código-fonte ativo adicional.

Selecione Unity Catalog em Storage options (Opções de armazenamento).

Selecione um catálogo para publicar dados.

Selecione um esquema no catálogo. Todas as tabelas de transmissão e visualizações materializadas definidas no site pipeline são criadas nesse esquema.

Na seção de computação, marq ue a caixa ao lado de Use Photon Acceleration (Usar aceleração). Para considerações adicionais sobre a configuração do site compute, consulte opções de configuração de computação.

[opções de configuração de computação](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#compute)

Clique em Criar.

Essas configurações recomendadas criam um novo pipeline configurado para execução no modo Triggered e usam o canal Current. Essa configuração é recomendada para muitos casos de uso, incluindo desenvolvimento e teste, e é adequada para cargas de trabalho de produção que devem ser executadas em um programador. Para obter detalhes sobre o pipeline de programação, consulte Delta Live Tables pipeline tarefa for Job.

[Delta Live Tables pipeline tarefa for Job](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/../jobs/pipeline.html)

## Opções de configuração de computação

[](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#compute-configuration-options)

Databricks recomenda sempre usar a escala automática aprimorada. Os valores padrão para outras configurações do compute funcionam bem para muitos pipelines.

O pipeline sem servidor remove as opções de configuração do compute. Para obter instruções de serverless configuração do serverless Delta Live Tables pipeline pipeline, consulte Configurar um pipeline .

[configuração do serverless Delta Live Tables pipeline](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/serverless-dlt.html)

Use as seguintes configurações para personalizar as configurações do site compute:

Os administradores do workspace podem configurar uma política de cluster. As políticas de computação permitem que os administradores controlem quais opções compute estão disponíveis para os usuários. Consulte Selecionar uma política de cluster.

[Selecionar uma política de cluster](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/configure-compute.html#cluster-policy)

Opcionalmente, o senhor pode configurar o modo de cluster para execução com tamanho fixo ou escala automática legada. Consulte Otimizar a utilização de cluster do pipeline Delta Live Tables com autoescala aprimorada.

[Otimizar a utilização de cluster do pipeline Delta Live Tables com autoescala aprimorada](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/auto-scaling.html)

Para cargas de trabalho com a autoescala ativada, defina Trabalhador mínimo e Trabalhador máximo para definir limites para comportamentos de escalonamento. Consulte Configurar computação para um pipeline do Delta Live Tables.

[Configurar computação para um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/configure-compute.html)

Opcionalmente, o senhor pode desativar a aceleração do Photon. Veja o que é Photon?.

[o que é Photon](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/../compute/photon.html)

Selecione um perfil de instância se o seu pipeline usa um instance profile para controlar o acesso ao cloud serviço. Consulte Configuração do armazenamento em nuvem.

[Configuração do armazenamento em nuvem](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/hive-metastore.html#configure-cloud-storage)

Use o Cluster Tag para ajudar a monitorar os custos associados ao pipeline Delta Live Tables. Consulte Configurar tag de cluster.

[Configurar tag de cluster](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/configure-compute.html#tags)

Configure Instance types para especificar o tipo de máquinas virtuais usadas para executar seu pipeline. Consulte Selecionar tipos de instância para executar a pipeline.

[Selecionar tipos de instância para executar a pipeline](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/configure-compute.html#instance-types)

Selecione um tipo de trabalhador otimizado para as cargas de trabalho configuradas em seu site pipeline.

Opcionalmente, o senhor pode selecionar um tipo de driver diferente do seu tipo worker. Isso pode ser útil para reduzir os custos no pipeline com grandes tipos de worker e baixa utilização do driver compute ou para escolher um tipo de driver maior para evitar problemas de falta de memória em cargas de trabalho com muitos trabalhadores pequenos.

## Outras considerações de configuração

[](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#other-configuration-considerations)

As seguintes opções de configuração também estão disponíveis para o pipeline:

A edição Advanced produto lhe dá acesso a todos os Delta Live Tables recurso. Opcionalmente, o senhor pode executar o pipeline usando as edições Pro ou Core do produto. Consulte Escolher uma edição do produto.

[Escolher uma edição do produto](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#editions)

O senhor pode optar por usar o modo Contínuo pipeline ao executar o pipeline na produção. Consulte Modo de pipeline acionado vs. contínuo.

[Modo de pipeline acionado vs. contínuo](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/pipeline-mode.html)

Se o site workspace não estiver configurado para Unity Catalog ou se a carga de trabalho precisar usar o site legado Hive metastore, consulte Usar o pipeline Delta Live Tables com o site legado Hive metastore.

[Usar o pipeline Delta Live Tables com o site legado Hive metastore](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/hive-metastore.html)

Adicionar notificações para atualizações do site email com base em condições de sucesso ou falha. Consulte Adicionar notificações email para eventos pipeline .

[Adicionar notificações email para eventos pipeline](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/observability.html#notifications)

Use o campo Configuration para definir o valor keypara o pipeline. Essas configurações têm duas finalidades:

Defina parâmetros arbitrários que você pode referenciar em seu código-fonte. Consulte Usar parâmetros com o pipeline Delta Live Tables .

[Usar parâmetros com o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/parameters.html)

Configurar as definições do pipeline e as configurações do Spark. Consulte a referência das propriedades do Delta Live Tables.

[referência das propriedades do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/properties.html)

Use o canal Preview para testar seu pipeline em relação às alterações pendentes de tempo de execução do Delta Live Tables e testar novos recursos.

### Escolha uma edição do produto

[](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#choose-a-product-edition)

Selecione a edição do produto Delta Live Tables com o melhor recurso para suas necessidades pipeline. As seguintes edições do produto estão disponíveis:

Core para execução, transmissão e ingestão de cargas de trabalho. Selecione a edição Core se o site pipeline não exigir recursos avançados, como captura de dados de alterações (CDC) (CDC) ou Delta Live Tables expectations.

Pro para execução, transmissão, ingestão e CDC cargas de trabalho. A edição Pro produto oferece suporte a todos os recursos Core, além de suporte a cargas de trabalho que exigem a atualização de tabelas com base em alterações nos dados de origem.

Advanced para execução transmissão ingest cargas de trabalho, CDC cargas de trabalho e cargas de trabalho que exigem expectativas. A edição do produto Advanced suporta o recurso das edições Core e Pro e inclui restrições de qualidade de dados com as expectativas do site Delta Live Tables.

O senhor pode selecionar a edição do produto ao criar ou editar um pipeline. O senhor pode escolher uma edição diferente para cada pipeline. Veja a página do produto Delta Live Tables.

[página do produto Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/https://www.databricks.com/product/pricing/delta-live)

Observação: se o site pipeline incluir recursos não compatíveis com a edição do produto selecionada, como expectativas, o senhor receberá uma mensagem de erro explicando o motivo do erro. O senhor pode então editar o pipeline para selecionar a edição apropriada.

## Configurar o código-fonte

[](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#configure-source-code)

O senhor pode usar o seletor de arquivos na UI do Delta Live Tables para configurar o código-fonte que define seu pipeline. O código-fonte do pipeline é definido no Databricks Notebook ou nos scripts SQL ou Python armazenados nos arquivos workspace. Ao criar ou editar o site pipeline, o senhor pode adicionar um ou mais arquivos Notebook ou workspace ou uma combinação de arquivos Notebook e workspace.

Como o Delta Live Tables analisa automaticamente as dependências do dataset para construir o gráfico de processamento do seu pipeline, o senhor pode adicionar o código-fonte ativo em qualquer ordem.

O senhor pode modificar o arquivo JSON para incluir o código-fonte Delta Live Tables definido em SQL e os scripts Python armazenados nos arquivos workspace. O exemplo a seguir inclui os arquivos Notebook e workspace:

## gerenciar dependências externas para pipelines que usam Python

[](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#manage-external-dependencies-for-pipelines-that-use-python)

Delta Live Tables suporta o uso de dependências externas em seu pipeline, como Python pacote e biblioteca. Para saber mais sobre as opções e recomendações para o uso de dependências, consulte gerenciar Python dependencies for Delta Live Tables pipeline.

[gerenciar Python dependencies for Delta Live Tables pipeline](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/external-dependencies.html)

## Use os módulos Python armazenados em seu espaço de trabalho do Databricks

[](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/#use-python-modules-stored-in-your-databricks-workspace)

Além de implementar seu código Python no Databricks Notebook, o senhor pode usar Databricks Git Folders ou workspace files para armazenar seu código como módulos Python. Armazenar seu código como módulos do Python é especialmente útil quando o senhor tem uma funcionalidade comum que deseja usar em vários pipelines ou Notebooks no mesmo pipeline. Para saber como usar os módulos Python com o seu pipeline, consulte Importar módulos Python de pastas Git ou arquivos workspace .

[Importar módulos Python de pastas Git ou arquivos workspace](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/import-workspace-files.html)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/configure-pipeline.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
