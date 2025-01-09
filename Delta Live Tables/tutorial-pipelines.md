[Documentação](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/index.html)

# Tutorial: Executar seu primeiro pipeline Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#tutorial-run-your-first-delta-live-tables-pipeline)

Este tutorial conduz o senhor pelos passos para configurar seu primeiro Delta Live Tables pipeline, escrever o código básico ETL e executar uma atualização pipeline.

Todos os passos neste tutorial foram projetados para o espaço de trabalho com o Unity Catalog ativado. O senhor também pode configurar o pipeline Delta Live Tables para trabalhar com o legado Hive metastore. Consulte Usar o pipeline Delta Live Tables com o legado Hive metastore.

[Usar o pipeline Delta Live Tables com o legado Hive metastore](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/hive-metastore.html)

Observação

Este tutorial contém instruções para o desenvolvimento e a validação do novo código pipeline usando o Databricks Notebook. O senhor também pode configurar o pipeline usando o código-fonte nos arquivos Python ou SQL.

O senhor pode configurar um pipeline para executar seu código se já tiver um código-fonte escrito usando a sintaxe do Delta Live Tables. Consulte Configurar um pipeline do Delta Live Tables.

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/configure-pipeline.html)

O senhor pode usar a sintaxe SQL totalmente declarativa em Databricks SQL para registrar e definir refresh programar a visualização materializada e as tabelas de transmissão como objetos do Unity Catalog-gerenciar. Consulte Use materialized view em Databricks SQL e Load uso de dados transmission tables em Databricks SQL.

[Use materialized view em Databricks SQL](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/../views/materialized.html)

[Load uso de dados transmission tables em Databricks SQL](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/../tables/streaming.html)

## Exemplo: Ingerir e processar dados de nomes de bebês de Nova York

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#example-ingest-and-process-new-york-baby-names-data)

O exemplo deste artigo usa um site disponível publicamente dataset que contém registros de nomes de bebês do Estado de Nova York. Este exemplo demonstra o uso de um pipeline do Delta Live Tables para:

[nomes de bebês do Estado de Nova York](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/https://health.data.ny.gov/Health/Baby-Names-Beginning-2007/jxy9-yhdk/about_data)

Ler dados CSV brutos de um volume em uma tabela.

Leia os registros da tabela de ingestão e use as expectativas do Delta Live Tables para criar uma nova tabela que contenha dados limpos.

[as expectativas](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/expectations.html)

Use os registros limpos como entrada para as consultas Delta Live Tables que criam conjuntos de dados derivados.

Este código demonstra um exemplo simplificado da arquitetura medalhão. Consulte Qual é a arquitetura medalhão do lakehouse?.

[Qual é a arquitetura medalhão do lakehouse?](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/../lakehouse/medallion.html)

As implementações desse exemplo são fornecidas para Python e SQL. Siga as etapas para criar um novo pipeline e um Notebook e, em seguida, copie e cole o código fornecido.

Também é fornecido um notebook de exemplo com código completo.

[um notebook](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#notebooks)



## Requisitos

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#requirements)

Para iniciar um pipeline, o senhor deve ter permissão de criação de clusters ou acesso a uma política de cluster que defina clusters do Delta Live Tables. O tempo de execução do Delta Live Tables cria um cluster antes de executar o pipeline e falha se o senhor não tiver a permissão correta.

[permissão de criação de clusters](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/../compute/clusters-manage.html#cluster-level-permissions)

Todos os usuários podem acionar atualizações usando o pipeline serverless por default. O serverless deve ser ativado no nível account e pode não estar disponível em sua região workspace. Consulte Ativar serverless compute .

[Ativar serverless compute .](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/../admin/workspace-settings/serverless.html)

Os exemplos deste tutorial usam o Unity Catalog. Databricks recomenda a criação de um novo esquema para executar esse tutorial, pois vários objetos de banco de dados são criados no esquema de destino.

[o Unity Catalog](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/../data-governance/unity-catalog/index.html)

Para criar um novo esquema em um catálogo, você deve ter os privilégios ALL PRIVILEGES ou USE CATALOG e CREATE SCHEMA.

Se o senhor não puder criar um novo esquema, execute este tutorial em um esquema existente. Você deve ter os seguintes privilégios:

USE CATALOG para o catálogo principal.

ALL PRIVILEGES ou privilégios USE SCHEMA, CREATE MATERIALIZED VIEW e CREATE TABLE no esquema de destino.

Este tutorial usa um volume para armazenar dados de amostra. A Databricks recomenda a criação de um novo volume para este tutorial. Se o senhor criar um novo esquema para este tutorial, poderá criar um novo volume nesse esquema.

Para criar um novo volume em um esquema existente, você deve ter os seguintes privilégios:

USE CATALOG para o catálogo principal.

ALL PRIVILEGES ou privilégios USE SCHEMA e CREATE VOLUME no esquema de destino.

Opcionalmente, você pode usar um volume existente. Você deve ter os seguintes privilégios:

USE CATALOG para o catálogo principal.

USE SCHEMA para o esquema principal.

ALL PRIVILEGES ou READ VOLUME e WRITE VOLUME no volume alvo.

Para definir essas permissões, entre em contato com o administrador da Databricks. Para saber mais sobre os privilégios do Unity Catalog, consulte Privilégios e objetos protegíveis do Unity Catalog.

[Privilégios e objetos protegíveis do Unity Catalog](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/../data-governance/unity-catalog/manage-privileges/privileges.html)

## o passo 0: download de dados

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#step-0-download-data)

Este exemplo carrega dados de um volume do Unity Catalog. O código a seguir downloads um arquivo CSV e o armazena no volume especificado. Abra um novo Notebook e execute o seguinte código para download esses dados no volume especificado:

Substitua <catalog-name>, <schema-name> e <volume-name> pelos nomes de catálogo, esquema e volume de um volume do Unity Catalog. O código fornecido tentará criar o esquema e o volume especificados se esses objetos não existirem. O senhor deve ter os privilégios adequados para criar e gravar em objetos no Unity Catalog. Consulte os requisitos.

[os requisitos](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#requirements)

Observação

Certifique-se de que este Notebook foi executado com sucesso antes de continuar com o site tutorial. Não configure este Notebook como parte de seu pipeline.

## o passo 1: Criar um pipeline

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#step-1-create-a-pipeline)

Delta Live Tables cria o pipeline resolvendo as dependências definidas no Notebook ou em arquivos (chamados de código-fonte) usando a sintaxe Delta Live Tables. Cada arquivo de código-fonte pode conter apenas um idioma, mas o senhor pode adicionar Notebook ou arquivos específicos de vários idiomas no site pipeline.

Importante

Não configure nenhum ativo no campo Código-fonte. Deixar esse campo em branco cria e configura um Notebook para criação de código-fonte.

As instruções neste tutorial usam serverless compute e Unity Catalog. Use as configurações do site default para todas as opções de configuração não especificadas nestas instruções.

Observação

Se o serverless não estiver habilitado ou não for compatível com o seu workspace, o senhor poderá concluir o tutorial conforme escrito usando as configurações do default compute . O senhor deve selecionar manualmente o Unity Catalog em Storage options (Opções de armazenamento) na seção Destination (Destino ) da interface de usuário Create pipeline (Criar pipeline ).

Para configurar um novo pipeline, faça o seguinte:

Na barra lateral, clique em Delta Live Tables.

Clique em Create pipeline (Criar pipeline).

No nome do pipeline, digite um nome exclusivo pipeline.

Marque a caixa de seleção sem servidor.

Em Destination, para configurar um local do Unity Catalog onde as tabelas são publicadas, selecione um Catalog e um Schema.

Em Advanced (Avançado), clique em Add configuration (Adicionar configuração ) e, em seguida, defina os parâmetros pipeline para o catálogo, o esquema e o volume para os quais o senhor faz download do uso de dados com os seguintes nomes de parâmetros:

my_catalog

my_schema

my_volume

Clique em Criar.

A interface do usuário do pipeline é exibida para o novo pipeline. Um Notebook de código-fonte é criado e configurado automaticamente para o site pipeline.

O Notebook é criado em um novo diretório no seu diretório de usuário. O nome do novo diretório e arquivo corresponde ao nome do seu pipeline. Por exemplo, /Users/your.username@databricks.com/my_pipeline/my_pipeline.

Um link para acessar esse Notebook está abaixo do campo Código-fonte no painel de detalhes do pipeline. Clique no link para abrir o Notebook antes de prosseguir para o próximo passo.



## o passo 2: Declarar a visualização materializada e as tabelas de transmissão em um Notebook com Python ou SQL

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#step-2-declare-materialized-views-and-streaming-tables-in-a-notebook-with-python-or-sql)

O senhor pode usar o Datbricks Notebook para desenvolver e validar interativamente o código-fonte do pipeline Delta Live Tables. O senhor deve anexar o Notebook ao site pipeline para usar essa funcionalidade. Para anexar o Notebook recém-criado ao site pipeline que o senhor acabou de criar:

Clique em Connect (Conectar ) no canto superior direito para abrir o menu de configuração do site compute.

Passe o mouse sobre o nome do site pipeline que o senhor criou no passo 1.

Clique em Conectar.

A interface do usuário muda para incluir os botões Validate e Começar no canto superior direito. Para saber mais sobre o suporte do Notebook para o desenvolvimento do código pipeline, consulte Desenvolver e depurar o pipeline Delta Live Tables no Notebook.

[Desenvolver e depurar o pipeline Delta Live Tables no Notebook](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/dlt-notebook-devex.html)

Importante

Delta Live Tables O pipeline avalia todas as células de um Notebook durante o planejamento. Diferentemente do Notebook, que é executado no site compute ou agendado como Job, o pipeline não garante que as células sejam executadas na ordem especificada.

O Notebook só pode conter uma única linguagem de programação. Não misture os códigos Python e SQL no Notebook de código-fonte pipeline.

Para obter detalhes sobre o desenvolvimento de código com Python ou SQL, consulte Desenvolver código de pipeline com Python ou Desenvolver código de pipeline com SQL.

[Desenvolver código de pipeline com Python](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/python-dev.html)

[Desenvolver código de pipeline com SQL](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/sql-dev.html)

### Exemplo de código de pipeline

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#example-pipeline-code)

Para implementar o exemplo neste tutorial, copie e cole o código a seguir em uma célula do Notebook configurada como código-fonte para o seu pipeline.

O código fornecido faz o seguinte:

Importa os módulos necessários (somente Python).

Faz referência aos parâmetros definidos durante a configuração do pipeline.

Define uma tabela de transmissão denominada baby_names_raw que é ingerida a partir de um volume.

Define um view materializado chamado baby_names_prepared que valida os dados ingeridos.

Define um view materializado chamado top_baby_names_2021 que tem um view altamente refinado dos dados.

## o passo 3: começar a pipeline update

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#step-3-start-a-pipeline-update)

Para começar uma atualização do pipeline, clique no botão começar no canto superior direito da UI do Notebook.



## Notebooks de Exemplo

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#example-notebooks)

O Notebook a seguir contém os mesmos exemplos de código fornecidos neste artigo. Esses Notebooks têm os mesmos requisitos que os passos deste artigo. Consulte os requisitos.

[os requisitos](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#requirements)

Para importar um Notebook, conclua os seguintes passos:

Abra a interface do usuário do Notebook.

Clique em + New > Notebook.

Um Notebook vazio é aberto.

Clique em Arquivo > Importar... A caixa de diálogo Importar é exibida.

Selecione a opção URL para Importar de.

Cole o URL do Notebook.

Clique em Importar.

Este tutorial requer que o senhor execute um Notebook de configuração de dados antes de configurar e executar seu Delta Live Tables pipeline. Importe o Notebook a seguir, anexe o Notebook a um compute recurso, preencha a variável necessária para my_catalog, my_schema e my_volume e clique em executar tudo.

### Dados download para pipeline tutorial

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#data-download-for-pipelines-tutorial)

Abra o bloco de anotações em outra guia   Copiar link para importação

[Abra o bloco de anotações em outra guia](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html//_extras/notebooks/source/dlt-data-setup.html)

![Copiar para área de transferência](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html//_static/clippy.svg)

O Notebook a seguir fornece exemplos em Python ou SQL. Quando o senhor importa um Notebook, ele é salvo no diretório inicial do usuário.

Depois de importar um dos Notebooks abaixo, complete os passos para criar um pipeline, mas use o seletor de arquivo de código-fonte para selecionar o Notebook de downloads. Depois de criar o site pipeline com um Notebook configurado como código-fonte, clique em começar na UI do site pipeline para acionar uma atualização.

### Comece a usar o notebook Python Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#get-started-with-delta-live-tables-python-notebook)

Abra o bloco de anotações em outra guia   Copiar link para importação

[Abra o bloco de anotações em outra guia](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html//_extras/notebooks/source/dlt-babynames-python.html)

![Copiar para área de transferência](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html//_static/clippy.svg)

### Comece a usar o notebook SQL Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/#get-started-with-delta-live-tables-sql-notebook)

Abra o bloco de anotações em outra guia   Copiar link para importação

[Abra o bloco de anotações em outra guia](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html//_extras/notebooks/source/dlt-babynames-sql.html)

![Copiar para área de transferência](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html//_static/clippy.svg)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/tutorial-pipelines.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
