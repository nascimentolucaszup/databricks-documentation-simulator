[Documentação](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/index.html)

[Desenvolver o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/develop-pipelines.html)

# Desenvolva o código do pipeline do Delta Live Tables em seu ambiente de desenvolvimento local

[](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/#develop-delta-live-tables-pipeline-code-in-your-local-development-environment)

Além de usar o Notebook ou o editor de arquivos em seu Databricks workspace para implementar o código pipeline que usa a interface Delta Live Tables Python , o senhor também pode desenvolver o código em seu ambiente de desenvolvimento local. Por exemplo, o senhor pode usar seu ambiente de desenvolvimento integrado (IDE) favorito, como o Visual Studio Code ou o PyCharm. Depois de escrever seu código pipeline localmente, o senhor pode movê-lo manualmente para seu Databricks workspace ou usar as ferramentas Databricks para operacionalizar seu pipeline, inclusive implantando e executando o pipeline.

[Python](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/python-ref.html)

Este artigo descreve as ferramentas e métodos disponíveis para desenvolver seu pipeline Python localmente e implantá-lo em seu workspace do Databricks. Também são fornecidos links para artigos que fornecem mais detalhes sobre o uso dessas ferramentas e métodos.

## Obtenha verificação de sintaxe, preenchimento automático e verificação de tipo em seu IDE

[](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/#get-syntax-checking-autocomplete-and-type-checking-in-your-ide)

Databricks fornece um módulo Python que você pode instalar em seu ambiente local para auxiliar no desenvolvimento de código para seu pipeline Delta Live Tables. Este módulo possui as interfaces e referências de docstring para a interface Python do Delta Live Tables, fornecendo verificação de sintaxe, preenchimento automático e verificação de tipo de dados conforme você escreve código em seu IDE.

Este módulo inclui interfaces, mas nenhuma implementação funcional. Você não pode usar esta biblioteca para criar ou executar um pipeline Delta Live Tables localmente. Em vez disso, use um dos métodos descritos abaixo para implantar seu código.

O módulo Python para desenvolvimento local está disponível no PyPI. Para obter instruções de instalação e uso, consulte stub Python para Delta Live Tables.

[stub Python para Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/https://pypi.org/project/databricks-dlt/)

## Valide, implante e execute seu código de pipeline com Databricks ativo Bundles

[](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/#validate-deploy-and-run-your-pipeline-code-with-databricks-asset-bundles)

Depois de implementar o código do pipeline Delta Live Tables, a Databricks recomenda usar Databricks ativo Bundles para operacionalizar o código. Os pacotes ativos do Databricks fornecem recursos de CI/CD para o ciclo de vida de desenvolvimento do pipeline, incluindo validação dos artefatos do pipeline, empacotamento de todos os artefatos do pipeline, como código-fonte e configuração, implantação do código em seu workspace do Databricks e início de atualizações do pipeline.

Para saber como criar um pacote para gerenciar seu código pipeline usando Databricks ativo Bundles, consulte Desenvolver o pipeline Delta Live Tables com Databricks ativo Bundles.

[Desenvolver o pipeline Delta Live Tables com Databricks ativo Bundles](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../dev-tools/bundles/pipelines-tutorial.html)

## Desenvolva e sincronize código de pipeline em seu IDE

[](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/#develop-and-sync-pipeline-code-in-your-ide)

Se você usar o IDE do Visual Studio Code para desenvolvimento, poderá usar o módulo Python para desenvolver seu código e, em seguida, usar a extensão Databricks para Visual Studio Code para sincronizar seu código diretamente do Visual Studio Code para seu workspace. Consulte O que é a extensão Databricks para Visual Studio Code?.

[módulo Python](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/#dlt-module)

[O que é a extensão Databricks para Visual Studio Code?](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../dev-tools/vscode-ext/index.html)

Para saber como criar um pipeline usando o código que o senhor sincronizou com o seu workspace usando a extensão Databricks para o Visual Studio Code, consulte Importar módulos Python de pastas Git ou arquivos workspace .

[Importar módulos Python de pastas Git ou arquivos workspace](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/import-workspace-files.html)

## Sincronize manualmente o código do pipeline com o workspace do Databricks

[](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/#manually-sync-your-pipeline-code-to-your-databricks-workspace)



Em vez de criar um pacote usando pacotes ativos do Databricks ou usando a extensão Databricks para Visual Studio Code, você pode sincronizar seu código com seu espaço de trabalho do Databricks e usar esse código para criar um pipeline dentro do espaço de trabalho. Isso pode ser particularmente útil durante os estágios de desenvolvimento e teste, quando você deseja iterar o código rapidamente. O Databricks oferece suporte a vários métodos para mover código do seu ambiente local para o seu workspace.

Para saber como criar um pipeline usando o código que o senhor sincronizou com o seu workspace usando um dos métodos abaixo, consulte Importar módulos Python de pastas Git ou arquivos workspace .

[Importar módulos Python de pastas Git ou arquivos workspace](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/import-workspace-files.html)

arquivosworkspace : você pode usar arquivos workspace do Databricks para upload o código-fonte do pipeline para o workspace do Databricks e, em seguida, importar esse código para um pipeline. Para saber como usar arquivos de espaço de trabalho, consulte O que são arquivos de espaço de trabalho?.

[O que são arquivos de espaço de trabalho?](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../files/workspace.html)

Databricks Git pastas: Para facilitar a colaboração e o controle de versões, Databricks recomenda o uso de pastas Databricks Git para sincronizar o código entre o ambiente local e o Databricks workspace. Git As pastas se integram ao seu provedor Git, permitindo que o senhor envie o código do seu ambiente local e, em seguida, importe esse código para um pipeline no seu workspace. Para saber como usar as pastas Git do Databricks, consulte Integração do Git para pastas Git do Databricks.

[Integração do Git para pastas Git do Databricks](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../repos/index.html)

Copie seu código manualmente: O senhor pode copiar o código de seu ambiente local, colá-lo em um Notebook Databricks e usar a interface do usuário Delta Live Tables para criar um novo pipeline com o Notebook. Para saber como criar um pipeline na interface do usuário, consulte Configurar um pipeline do Delta Live Tables.

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/configure-pipeline.html)

## Implementar fluxo de trabalho personalizado de CI/CD

[](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/#implement-custom-cicd-workflows)

Se você preferir escrever scripts para gerenciar seu pipeline, o Databricks tem uma API REST, a interface de linha de comando (CLI) do Databricks e kits de desenvolvimento de software (SDKs) para linguagens de programação populares. Você também pode usar o recurso databricks_pipeline no provedor Databricks Terraform.

Para saber como usar a API REST, consulte Delta Live Tables na Referência da API REST do Databricks.

[Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/https://docs.databricks.com/api/workspace/pipelines)

Para saber como usar a CLI do Databricks, consulte O que é a CLI do Databricks?.

[O que é a CLI do Databricks?](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../dev-tools/cli/index.html)

Para saber como usar o Databricks Python SDK, consulte Databricks SDK para Python e os exemplos de pipeline nos repositórios GitHub do projeto.

[Databricks SDK para Python](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../dev-tools/sdk-python.html)

[exemplos de pipeline](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/https://github.com/databricks/databricks-sdk-py/tree/main/examples/pipelines)

Para saber como usar os SDKs da Databricks para outros idiomas, consulte Usar SDKs com a Databricks.

[Usar SDKs com a Databricks](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../dev-tools/sdks.html)

Para saber como usar o provedor Databricks Terraform, consulte o provedor Databricks Terraform e a documentação do Terraform para o recurso databricks_pipeline.

[o provedor Databricks Terraform](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/../dev-tools/terraform/index.html)

[recurso databricks_pipeline](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/https://registry.terraform.io/providers/databricks/databricks/latest/docs/resources/pipeline)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/develop-locally.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
