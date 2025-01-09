[Documentação](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/index.html)

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/configure-pipeline.html)

# Importar módulos Python de pastas Git ou arquivos de espaço de trabalho

[](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/#import-python-modules-from-git-folders-or-workspace-files)

O senhor pode armazenar o código Python em pastasDatabricks Git  ou em arquivosworkspace  e, em seguida, importar esse código Python para o pipeline Delta Live Tables. Para obter mais informações sobre como trabalhar com módulos em pastas Git ou arquivos workspace, consulte Work with Python and R modules.

[pastasDatabricks Git](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/../repos/index.html)

[arquivosworkspace](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/../files/workspace.html)

[Work with Python and R modules](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/../files/workspace-modules.html)

Observação

O senhor não pode importar o código-fonte de um Notebook armazenado em uma pasta Databricks Git ou em um arquivo workspace. Em vez disso, adicione o Notebook diretamente quando o senhor criar ou editar um pipeline. Consulte Configurar um pipeline do Delta Live Tables.

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/configure-pipeline.html)

## Importe um módulo Python para um pipeline Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/#import-a-python-module-to-a-delta-live-tables-pipeline)

O exemplo a seguir demonstra a importação de consultas dataset como módulos Python de arquivos workspace. Embora este exemplo descreva o uso de arquivos workspace para armazenar o código-fonte pipeline, o senhor pode usá-lo com o código-fonte armazenado em uma pasta Git.

Para executar este exemplo, utilize os seguintes passos:

Clique em  workspace na barra lateral de seu Databricks workspace para abrir o navegador workspace.

![Ícone do espaço de trabalho](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/../_images/workspaces-icon-account.png)

Use o navegador workspace para selecionar um diretório para os módulos Python.

Clique em  na coluna mais à direita do diretório selec ionado e clique em Create > File (Criar arquivo).

![Menu Kebab](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/../_images/kebab-menu.png)

Digite um nome para o arquivo, por exemplo, clickstream_raw_module.py. O editor de arquivos é aberto. Para criar um módulo para ler dados de origem em uma tabela, digite o seguinte na janela do editor:

Para criar um módulo que crie uma nova tabela contendo dados preparados, crie um novo arquivo no mesmo diretório, digite um nome para o arquivo, por exemplo, clickstream_prepared_module.py, e digite o seguinte na nova janela do editor:

Em seguida, crie um pipeline Notebook. Acesse seu site Databricks páginas de aterrissagem e selecione Create a Notebook, ou clique em  New na barra lateral e selecione Notebook. O senhor também pode criar o Notebook no navegador workspace clicando em  e em Create > Notebook.

![Novo ícone](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/../_images/create-icon.png)

![Menu Kebab](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/../_images/kebab-menu.png)

Nomeie seu Notebook e confirme que o Python é o idioma default.

Clique em Criar.

Digite o código de exemplo no Notebook.

Observação

Se o seu Notebook importar módulos ou pacotes de um caminho de arquivos workspace ou de um caminho de pastas Git diferente do diretório Notebook, o senhor deverá anexar manualmente o caminho aos arquivos usando sys.path.append().

Se estiver importando um arquivo de uma pasta Git, o senhor deve acrescentar /Workspace/ ao caminho. Por exemplo, sys.path.append('/Workspace/...'). A omissão de /Workspace/ no caminho resulta em um erro.

Se os módulos ou o pacote estiverem armazenados no mesmo diretório que o Notebook, o senhor não precisará acrescentar o caminho manualmente. O senhor também não precisa anexar manualmente o caminho ao importar do diretório raiz de uma pasta Git porque o diretório raiz é automaticamente anexado ao caminho.

Substitua <module-path> pelo caminho para o diretório que contém os módulos Python a serem importados.

Crie um pipeline usando o novo Notebook.

Para executar o pipeline, na página de detalhes do Pipeline , clique em começar.

O senhor também pode importar o código Python como um pacote. O seguinte trecho de código de um Delta Live Tables Notebook importa o pacote test_utils do diretório dlt_packages dentro do mesmo diretório que o Notebook. O diretório dlt_packages contém os arquivos test_utils.py e __init__.py, e test_utils.py define a função create_test_table():

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/import-workspace-files.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
