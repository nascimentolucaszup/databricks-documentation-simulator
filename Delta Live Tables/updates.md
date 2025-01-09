[Documentação](https://docs.databricks.com/pt/delta-live-tables/updates.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/updates.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/updates.html/index.html)

# execução de uma atualização em um pipeline Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#run-an-update-on-a-delta-live-tables-pipeline)

Este artigo explica as atualizações do site pipeline e fornece detalhes sobre como acionar uma atualização.

## O que é uma atualização de pipeline?

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#what-is-a-pipeline-update)

Depois de criar um pipeline e estar pronto para executá-lo, você começa uma atualização. Uma atualização de pipeline faz o seguinte:

começar a clusters com a configuração correta.

Descobre todas as tabelas e visualizações definidas e verifica se há erros de análise, como nomes de colunas não válidos, dependências ausentes e erros de sintaxe.

Cria ou atualiza tabelas e view com os dados mais recentes disponíveis.

Usando uma atualização de validação, o senhor pode verificar se há problemas no código-fonte de um pipeline sem esperar que as tabelas sejam criadas ou atualizadas. Esse recurso é útil ao desenvolver ou testar o pipeline, pois permite que o senhor encontre e corrija rapidamente os erros no site pipeline, como nomes incorretos de tabelas ou colunas.

[atualização de validação](https://docs.databricks.com/pt/delta-live-tables/updates.html/#validate-update)

## Como as atualizações do pipeline são acionadas?

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#how-are-pipeline-updates-triggered)

Use uma das opções a seguir para começar pipeline atualizações:

| Atualizar gatilho | Detalhes |
| --- | --- |
| Manual | O senhor pode acionar manualmente as atualizações do pipeline na interface do usuário do pipeline, na lista de pipeline ou em um Notebook anexado ao pipeline. ConsulteAcionar manualmente uma atualização do pipelineeDesenvolver e depurar o pipeline do Delta Live Tables no Notebook. |
| Agendado | O senhor pode programar atualizações para o pipeline usando o Job. ConsulteDelta Live Tables pipeline tarefa for Job. |
| Programático | O senhor pode acionar atualizações de forma programática usando ferramentas de terceiros, APIs e CLIs. Vejaexecução a Delta Live Tables pipeline em um fluxo de trabalhoepipeline API. |


Atualizar gatilho

Detalhes

Manual

O senhor pode acionar manualmente as atualizações do pipeline na interface do usuário do pipeline, na lista de pipeline ou em um Notebook anexado ao pipeline. Consulte Acionar manualmente uma atualização do pipeline  e Desenvolver e depurar o pipeline do Delta Live Tables no Notebook.

[Acionar manualmente uma atualização do pipeline](https://docs.databricks.com/pt/delta-live-tables/updates.html/#trigger-manual)

[Desenvolver e depurar o pipeline do Delta Live Tables no Notebook](https://docs.databricks.com/pt/delta-live-tables/updates.html/dlt-notebook-devex.html)

Agendado

O senhor pode programar atualizações para o pipeline usando o Job. Consulte Delta Live Tables pipeline tarefa for Job.

[Delta Live Tables pipeline tarefa for Job](https://docs.databricks.com/pt/delta-live-tables/updates.html/../jobs/pipeline.html)

Programático

O senhor pode acionar atualizações de forma programática usando ferramentas de terceiros, APIs e CLIs. Veja execução a Delta Live Tables pipeline em um fluxo de trabalho e pipeline API.

[execução a Delta Live Tables pipeline em um fluxo de trabalho](https://docs.databricks.com/pt/delta-live-tables/updates.html/workflows.html)

[pipeline API](https://docs.databricks.com/pt/delta-live-tables/updates.html/https://docs.databricks.com/api/workspace/pipelines)

## Acionar manualmente uma atualização do pipeline

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#manually-trigger-a-pipeline-update)

Use uma das seguintes opções para acionar manualmente uma atualização do pipeline:

Clique no  botão na página de detalhes do pipeline.

![Delta Live Tables começar Icon](https://docs.databricks.com/pt/delta-live-tables/updates.html/../_images/dlt-start-button.png)

Na lista de pipelines, clique em  na coluna Ações .

![Ícone de seta para a direita](https://docs.databricks.com/pt/delta-live-tables/updates.html/../_images/right-arrow.png)

Observação

O comportamento default para atualizações pipeline acionadas manualmente é refresh todos os conjuntos de dados definidos no pipeline.

## Semântica de atualização do pipeline

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#pipeline-refresh-semantics)

A tabela a seguir descreve os comportamentos da visualização materializada e das tabelas de transmissão para default refresh e refresh completo:

| Tipo de atualização | Materializado view semântica | semântica da tabela de transmissão |
| --- | --- | --- |
| refresh (default) | Atualiza os resultados para refletir os resultados atuais da consulta definidora. | Processa novos registros por meio da lógica definida em tabelas e fluxos de transmissão. |
| refresh completo | Atualiza os resultados para refletir os resultados atuais da consulta definidora. | Limpa os dados das tabelas de transmissão, limpa as informações de estado (pontos de verificação) dos fluxos e reprocessa todos os registros da fonte de dados. |


Tipo de atualização

Materializado view semântica

semântica da tabela de transmissão

refresh (default)

Atualiza os resultados para refletir os resultados atuais da consulta definidora.

Processa novos registros por meio da lógica definida em tabelas e fluxos de transmissão.

refresh completo

Atualiza os resultados para refletir os resultados atuais da consulta definidora.

Limpa os dados das tabelas de transmissão, limpa as informações de estado (pontos de verificação) dos fluxos e reprocessa todos os registros da fonte de dados.

Por default, todas as tabelas de visualização e transmissão materializadas em um pipeline refresh a cada atualização. Opcionalmente, o senhor pode omitir tabelas das atualizações usando o seguinte recurso:

Selecionar tabelas para refresh: Use esta interface do usuário para adicionar ou remover a visualização materializada e as tabelas de transmissão antes de executar uma atualização. Consulte começar a pipeline update para tabelas selecionadas.

[começar a pipeline update para tabelas selecionadas](https://docs.databricks.com/pt/delta-live-tables/updates.html/#refresh-selection)

Atualizar tabelas com falha: começar uma atualização para a visualização materializada com falha e tabelas de transmissão, incluindo dependências downstream. Consulte  pipeline update for failed tables.

[pipeline update for failed tables](https://docs.databricks.com/pt/delta-live-tables/updates.html/#refresh-failed)

Ambos os recursos suportam a semântica default refresh ou a refresh completa. Opcionalmente, o senhor pode usar a caixa de diálogo Select tables for refresh para excluir tabelas adicionais ao executar um refresh para tabelas com falha.

### Devo usar uma atualização completa?

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#should-i-use-a-full-refresh)

Databricks recomenda executar a atualização completa somente quando necessário. Um refresh completo sempre reprocessa todos os registros da fonte de dados especificada por meio da lógica que define o dataset. O tempo e o recurso para concluir um refresh completo estão correlacionados ao tamanho dos dados de origem.

A visualização materializada retorna os mesmos resultados, quer seja usada a default ou a refresh completa. Usar um refresh completo com tabelas de transmissão redefine todas as informações de processamento de estado e de ponto de verificação e pode resultar em registros descartados se os dados de entrada não estiverem mais disponíveis.

Databricks recomenda apenas o refresh completo quando a fonte de dados de entrada contém os dados necessários para recriar o estado desejado da tabela ou view. Considere os seguintes cenários em que os dados da fonte de entrada não estão mais disponíveis e o resultado da execução de um refresh completo:

| Origem de dados | Motivo pelo qual os dados de entrada estão ausentes | Resultado da refresh |
| --- | --- | --- |
| Kafka | Limite de retenção curto | Os registros que não estão mais presentes na fonte do Kafka são descartados da tabela de destino. |
| Arquivos no armazenamento de objetos | Política de Ciclo de Vida | Os arquivos de dados que não estão mais presentes no diretório de origem são eliminados da tabela de destino. |
| Registros em uma tabela | Eliminado para compliance | Somente os registros presentes na tabela de origem são processados. |


Origem de dados

Motivo pelo qual os dados de entrada estão ausentes

Resultado da refresh

Kafka

Limite de retenção curto

Os registros que não estão mais presentes na fonte do Kafka são descartados da tabela de destino.

Arquivos no armazenamento de objetos

Política de Ciclo de Vida

Os arquivos de dados que não estão mais presentes no diretório de origem são eliminados da tabela de destino.

Registros em uma tabela

Eliminado para compliance

Somente os registros presentes na tabela de origem são processados.

Para evitar que a atualização completa seja executada em uma tabela ou view, defina a propriedade pipelines.reset.allowed da tabela como false. Consulte as propriedades da tabela Delta Live Tables. O senhor também pode usar um fluxo de acréscimo para acrescentar dados a uma tabela de transmissão existente sem precisar de um refresh completo.

[as propriedades da tabela Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/updates.html/properties.html#table-properties)

[fluxo de acréscimo](https://docs.databricks.com/pt/delta-live-tables/updates.html/flows.html#append-flows)

## começar uma atualização de pipeline para tabelas selecionadas

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#start-a-pipeline-update-for-selected-tables)

Opcionalmente, o senhor pode reprocessar dados apenas para tabelas selecionadas em seu pipeline. Por exemplo, durante o desenvolvimento, o senhor altera apenas uma única tabela e deseja reduzir o tempo de teste, ou uma atualização de pipeline falha e o senhor deseja atualizar apenas as tabelas que falharam.

[tabelas que falharam](https://docs.databricks.com/pt/delta-live-tables/updates.html/#refresh-failed)

Observação

Você pode usar refresh seletiva apenas com pipelines acionados.

Para iniciar uma atualização que refresh apenas tabelas selecionadas, na página de detalhespipeline  :

Clique em Selecionar tabelas para refresh. A caixa de diálogo Selecionar tabelas para refresh é exibida.

Se o senhor não vir o botão Select tables for refresh (Selecionar tabelas para atualização ), confirme se a página de detalhes do pipeline exibe a atualização mais recente e se a atualização foi concluída. Se um DAG não for mostrado para a última atualização, por exemplo, porque a atualização falhou, o botão Select tables for refresh (Selecionar tabelas para atualização) não será exibido.

Para selecionar as tabelas para refresh, clique em cada tabela. As tabelas selecionadas são destacadas e o rótulo é exibido. Para remover uma tabela da atualização, clique na tabela novamente.

Clique em refresh seleção.

Observação

O botão de seleçãorefresh  exibe o número de tabelas selecionadas entre parênteses.

Para reprocessar os dados já ingeridos para as tabelas selecionadas, clique em  ao lado do botão de seleção de atualização e clique em Full refresh selection (Seleção de atualização completa).

![Acento circunflexo azul para baixo](https://docs.databricks.com/pt/delta-live-tables/updates.html/../_images/down-caret-blue.png)

## começar uma atualização de pipeline para tabelas com falha

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#start-a-pipeline-update-for-failed-tables)

Se uma atualização de pipeline falhar devido a erros em uma ou mais tabelas no grafo de pipeline, você poderá iniciar uma atualização apenas de tabelas com falha e quaisquer dependências downstream.

Observação

As tabelas excluídas não são atualizadas, mesmo que dependam de uma tabela com falha.

Para atualizar tabelas com falha, na página de detalhes do Pipeline , clique em refresh tabelas com falha.

Para atualizar apenas as tabelas com falha selecionadas:

Clique  ao lado do botão refresh tabelas com falha e clique em Selecionar tabelas para refresh. A caixa de diálogo Selecionar tabelas para refresh é exibida.

![Botão para baixo](https://docs.databricks.com/pt/delta-live-tables/updates.html/../_images/button-down.png)

Para selecionar as tabelas para refresh, clique em cada tabela. As tabelas selecionadas são destacadas e o rótulo é exibido. Para remover uma tabela da atualização, clique na tabela novamente.

Clique em refresh seleção.

Observação

O botão de seleçãorefresh  exibe o número de tabelas selecionadas entre parênteses.

Para reprocessar os dados já ingeridos para as tabelas selecionadas, clique em  ao lado do botão de seleção de atualização e clique em Full refresh selection (Seleção de atualização completa).

![Acento circunflexo azul para baixo](https://docs.databricks.com/pt/delta-live-tables/updates.html/../_images/down-caret-blue.png)

## Verifique se há erros em um pipeline sem esperar a atualização das tabelas

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#check-a-pipeline-for-errors-without-waiting-for-tables-to-update)

Visualização

O recurso de atualização Delta Live Tables Validate está em visualização pública.

[visualização pública](https://docs.databricks.com/pt/delta-live-tables/updates.html/../release-notes/release-types.html)

Para verificar se o código-fonte de um pipeline é válido sem executar uma atualização completa, use Validate. Uma atualização Validate resolve as definições de dataset e fluxos definidos no pipeline, mas não materializa nem publica nenhum dataset. Erros encontrados durante a validação, como nomes incorretos de tabelas ou colunas, são relatados na UI.

Para executar uma atualização Validate, clique em  na página de detalhes pipeline ao lado de começar e clique em Validate (Validar).

![Acento circunflexo azul para baixo](https://docs.databricks.com/pt/delta-live-tables/updates.html/../_images/down-caret-blue.png)

Após a conclusão da atualização Validate, o evento log mostra eventos relacionados apenas à atualização Validate e nenhuma métrica é exibida no DAG. Se forem encontrados erros, os detalhes estarão disponíveis no evento log.

Você pode ver os resultados apenas da atualização Validate mais recente. Se a atualização Validate foi a atualização de execução mais recente, você poderá ver os resultados selecionando-a na atualização história. Se outra atualização for executada após a atualização Validate , os resultados não estarão mais disponíveis na IU.

[atualização história](https://docs.databricks.com/pt/delta-live-tables/updates.html/observability.html#update-history)

## Modos de desenvolvimento e produção

[](https://docs.databricks.com/pt/delta-live-tables/updates.html/#development-and-production-modes)

Você pode otimizar a execução do pipeline alternando entre os modos de desenvolvimento e produção. Use o  botões na IU do pipeline para alternar entre esses dois modos. Por default, os pipelines são executados no modo de desenvolvimento.

![Ícone de alternância do ambiente Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/updates.html/../_images/dlt-env-toggle.png)

Quando você executa seu pipeline no modo de desenvolvimento, o sistema Delta Live Tables faz o seguinte:

Reutiliza um cluster para evitar a sobrecarga de reinicializações. Em default, clusters execução por duas horas quando o modo de desenvolvimento estiver ativado. O senhor pode alterar isso com a configuração pipelines.clusterShutdown.delay no pipeline Configure compute for a Delta Live Tables.

[pipeline Configure compute for a Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/updates.html/configure-compute.html)

Desabilita novas tentativas de pipeline para que você possa detectar e corrigir erros imediatamente.

No modo de produção, o sistema Delta Live Tables faz o seguinte:

Reinicia os clusters para erros recuperáveis específicos, incluindo vazamentos de memória e credenciais obsoletas.

Tenta novamente a execução no caso de erros específicos, como uma falha ao começar a cluster.

Observação

A alternância entre os modos de desenvolvimento e produção controla apenas clusters e o comportamento de execução do pipeline. Os locais de armazenamento e os esquemas de destino no catálogo para publicação de tabelas devem ser configurados como parte das configurações do pipeline e não são afetados ao alternar entre os modos.



© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/updates.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/updates.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/updates.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/updates.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/updates.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/updates.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/updates.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/updates.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
