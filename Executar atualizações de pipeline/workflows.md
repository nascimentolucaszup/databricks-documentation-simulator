[Documentação](https://docs.databricks.com/pt/delta-live-tables/workflows.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/workflows.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/workflows.html/index.html)

[execução de uma atualização em um pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/workflows.html/updates.html)

# execução de um pipeline Delta Live Tables em um fluxo de trabalho

[](https://docs.databricks.com/pt/delta-live-tables/workflows.html/#run-a-delta-live-tables-pipeline-in-a-workflow)

Você pode executar um pipeline Delta Live Tables como parte de um fluxo de trabalho de processamento de dados com Databricks Job, Apache Airflow ou Azure Data Factory.

## Empregos

[](https://docs.databricks.com/pt/delta-live-tables/workflows.html/#jobs)

O senhor pode orquestrar várias tarefas em um Databricks Job para implementar um fluxo de trabalho de processamento de dados. Para incluir um Delta Live Tables pipeline em um trabalho, use a tarefa de pipeline quando o senhor criar um trabalho. Consulte Delta Live Tables pipeline tarefa for Job.

[Delta Live Tables pipeline tarefa for Job](https://docs.databricks.com/pt/delta-live-tables/workflows.html/../jobs/pipeline.html)

## Apache Airflow

[](https://docs.databricks.com/pt/delta-live-tables/workflows.html/#apache-airflow)

Apache Airflow é uma solução de código aberto para gerenciar e programar o fluxo de trabalho de dados. Airflow representa o fluxo de trabalho como um gráfico acíclico direcionado (DAGs) de operações. O senhor define um fluxo de trabalho em um arquivo Python e Airflow gerencia a programação e a execução. Para obter informações sobre como instalar e usar o Airflow com o Databricks, consulte Orquestrar o trabalho Databricks com o Apache Airflow .

[Apache Airflow](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://airflow.apache.org/)

[Orquestrar o trabalho Databricks com o Apache Airflow .](https://docs.databricks.com/pt/delta-live-tables/workflows.html/../jobs/how-to/use-airflow-with-jobs.html)

Para executar um pipeline Delta Live Tables como parte de um fluxo de trabalho do Airflow, use o DatabricksSubmitRunOperator.

[DatabricksSubmitRunOperator](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://airflow.apache.org/docs/apache-airflow-providers-databricks/stable/_api/airflow/providers/databricks/operators/databricks/index.html#airflow.providers.databricks.operators.databricks.DatabricksSubmitRunOperator)

### Requisitos

[](https://docs.databricks.com/pt/delta-live-tables/workflows.html/#requirements)

Os itens a seguir são necessários para usar o suporte Airflow para Delta Live Tables:

Airflow versão 2.1.0 ou mais tarde.

O pacote do provedor Databricks versão 2.1.0 ou mais tarde.

[do provedor Databricks](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://pypi.org/project/apache-airflow-providers-databricks/)

### Exemplo

[](https://docs.databricks.com/pt/delta-live-tables/workflows.html/#example)

O exemplo a seguir cria um Airflow DAG que aciona uma atualização para o pipeline Delta Live Tables com o identificador 8279d543-063c-4d63-9926-dae38e35ce8b:

Substitua CONNECTION_ID pelo identificador de uma conexãoAirflow  com o site workspace.

[conexãoAirflow](https://docs.databricks.com/pt/delta-live-tables/workflows.html/../jobs/how-to/use-airflow-with-jobs.html)

Salve este exemplo no diretório airflow/dags e use a interface do usuário Airflow para view e acionar o DAG. Use a interface do usuário Delta Live Tables para view os detalhes da atualização pipeline.

[view e acionar](https://docs.databricks.com/pt/delta-live-tables/workflows.html/../jobs/how-to/use-airflow-with-jobs.html)

## Fábrica de dados do Azure

[](https://docs.databricks.com/pt/delta-live-tables/workflows.html/#azure-data-factory)

Observação

O Delta Live Tables e o Azure Data Factory incluem opções para configurar o número de novas tentativas quando ocorre uma falha. Se os valores de nova tentativa forem configurados em seu pipeline do Delta Live Tables e na atividade do Azure Data Factory que chama o pipeline, o número de novas tentativas será o valor de nova tentativa do Azure Data Factory multiplicado pelo valor de nova tentativa do Delta Live Tables.

Por exemplo, se uma atualização do pipeline falhar, o Delta Live Tables tentará novamente a atualização até cinco vezes pelo default. Se a nova tentativa do Azure Data Factory estiver definida como três e o seu Delta Live Tables pipeline usar o default de cinco tentativas, a falha do Delta Live Tables pipeline poderá ser repetida até quinze vezes. Para evitar tentativas excessivas de nova tentativa quando as atualizações do pipeline falharem, a Databricks recomenda limitar o número de novas tentativas ao configurar o pipeline do Delta Live Tables ou a atividade do Azure Data Factory que chama o pipeline.

Para alterar a configuração de repetição do pipeline do Delta Live Tables, use a configuração pipelines.numUpdateRetryAttempts ao configurar o pipeline.

Azure O Data Factory é cloudum ETL serviço baseado no site que permite que o senhor orquestre a integração de dados e as transformações do fluxo de trabalho. Azure O Data Factory suporta diretamente a execução da tarefa Databricks em um fluxo de trabalho, incluindo o Notebook, a tarefa JAR e os scripts Python. O senhor também pode incluir um pipeline em um fluxo de trabalho chamando a API Delta Live Tables de uma atividade da Web do Azure Data Factory. Por exemplo, para acionar uma atualização de pipeline do Azure Data Factory:

[Notebook](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://learn.microsoft.com/azure/data-factory/transform-data-using-databricks-notebook)

[API](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://docs.databricks.com/api/workspace/pipelines)

[atividade da Web](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://learn.microsoft.com/azure/data-factory/control-flow-web-activity)

Crie um data factory ou abra um data factory existente.

[Crie um data factory](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://learn.microsoft.com/azure/data-factory/quickstart-create-data-factory-portal#create-a-data-factory)

Quando a criação for concluída, abra a página do seu data factory e clique no bloco Open Azure Data Factory Studio . A interface de usuário do Azure Data Factory é exibida.

Crie um novo pipeline do Azure Data Factory selecionando Pipeline no menu suspenso Novo na interface do usuário do Azure Data Factory Studio.

Na caixa de ferramentas Atividades , expanda Geral e arraste a atividade da Web para a tela do pipeline. Clique na tab Configurações e insira os seguintes valores:

Observação

Como prática recomendada de segurança ao se autenticar com ferramentas, sistemas, scripts e aplicativos automatizados, a Databricks recomenda que você use tokens OAuth.

[tokens OAuth](https://docs.databricks.com/pt/delta-live-tables/workflows.html/../dev-tools/auth/oauth-m2m.html)

Se o senhor usar a autenticação pessoal access token, a Databricks recomenda o uso de pessoal access tokens pertencente à entidade de serviço em vez de usuários workspace. Para criar o site tokens para uma entidade de serviço, consulte gerenciar tokens para uma entidade de serviço.

[entidade de serviço](https://docs.databricks.com/pt/delta-live-tables/workflows.html/../admin/users-groups/service-principals.html)

[uma entidade de serviço, consulte gerenciar tokens para uma entidade de serviço](https://docs.databricks.com/pt/delta-live-tables/workflows.html/../admin/users-groups/service-principals.html#personal-access-tokens)

URL: https://<databricks-instance>/api/2.0/pipelines/<pipeline-id>/updates.

Substitua <get-workspace-instance>.

Substitua <pipeline-id> pelo identificador do pipeline.

Método: Selecione POST no menu suspenso.

Cabeçalhos: Clique em + Novo. Na caixa de texto Nome , digite Authorization. Na caixa de texto Valor , digite Bearer <personal-access-token>.

Substitua <personal-access-token> por um  access tokenpessoal do Databricks.

[access tokenpessoal](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://docs.databricks.com/api/workspace/tokenmanagement)

Corpo: para passar parâmetros de solicitação adicionais, insira um documento JSON contendo os parâmetros. Por exemplo, para iniciar uma atualização e reprocessar todos os dados para o pipeline: {"full_refresh": "true"}. Se não houver parâmetros de solicitação adicionais, insira chaves vazias ({}).

Para testar a atividade da Web, clique em Depurar na barra de ferramentas do pipeline na interface do usuário do Data Factory. A saída e o status da execução, incluindo erros, são exibidos na  tab Saída do pipeline do Azure Data Factory. Use a IU do Delta Live Tables para view os detalhes da atualização do pipeline.

Dica

Um requisito de fluxo de trabalho comum é iniciar uma tarefa após a conclusão de uma tarefa anterior. Como a solicitação Delta Live Tables updates é assíncrona — a solicitação retorna depois de iniciar a atualização, mas antes da conclusão da atualização — as tarefas em seu pipeline do Azure Data Factory com dependência da atualização Delta Live Tables devem aguardar a conclusão da atualização. Uma opção para aguardar a conclusão da atualização é adicionar uma atividade Until após a atividade da Web que aciona a atualização Delta Live Tables. Na atividade Até:

[atividade Until](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://learn.microsoft.com/azure/data-factory/control-flow-until-activity)

Adicione uma atividade Aguardar para aguardar um número configurado de segundos para a conclusão da atualização.

[atividade Aguardar](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://learn.microsoft.com/azure/data-factory/control-flow-wait-activity)

Adicione uma atividade da Web após a atividade Wait que usa a solicitação de detalhes de atualização do Delta Live Tables para obter o status da atualização. O campo state na resposta retorna o estado atual da atualização, inclusive se ela foi concluída.

Use o valor do campo state para definir a condição de encerramento da atividade Até. Você também pode usar uma atividade Definir variável para adicionar uma variável de pipeline com base no valor state e usar essa variável para a condição de encerramento.

[atividade Definir variável](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://learn.microsoft.com/azure/data-factory/control-flow-set-variable-activity)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/workflows.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/workflows.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/workflows.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/workflows.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
