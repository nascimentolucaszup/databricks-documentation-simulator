[Documentação](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/index.html)

[Monitorar o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/observability.html)

# Definir o monitoramento personalizado do pipeline Delta Live Tables com ganchos de eventos

[](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/#define-custom-monitoring-of-delta-live-tables-pipelines-with-event-hooks)

Visualização

O suporte para ganchos de eventos está em Public Preview.

[Public Preview](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/../release-notes/release-types.html)

Você pode usar ganchos de eventos para adicionar funções de retorno de chamada Python personalizadas que são executadas quando os eventos são persistidos nos  logsde eventos de um pipeline do Delta Live Tables. Você pode usar ganchos de eventos para implementar soluções personalizadas de monitoramento e alertas. Por exemplo, você pode usar ganchos de eventos para enviar email ou gravar em logs quando ocorrem eventos específicos ou para integrar soluções de terceiros para monitorar eventos de pipeline.

[logsde eventos](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/observability.html#event-log)

Você define um gancho de evento com uma função Python que aceita um único argumento, onde o argumento é um dicionário que representa um evento. Em seguida, você inclui os ganchos de eventos como parte do código-fonte de um pipeline. Quaisquer ganchos de eventos definidos em um pipeline tentarão processar todos os eventos gerados durante cada atualização do pipeline. Se o seu pipeline for composto por vários artefatos de código-fonte, por exemplo, vários Notebook, quaisquer ganchos de eventos definidos serão aplicados a todo o pipeline. Embora os ganchos de eventos estejam incluídos no código-fonte do seu pipeline, eles não estão incluídos no gráfico do pipeline.

Você pode usar ganchos de eventos com pipeline que publicam no Hive metastore ou Unity Catalog.

Observação

Python é a única linguagem compatível com a definição de ganchos de eventos. Para definir funções personalizadas do Python que processam eventos em um pipeline implementado usando a interface SQL, adicione as funções personalizadas em um Python Notebook separado que é executado como parte do pipeline. As funções do Python são aplicadas a todo o pipeline quando o pipeline é executado.

Os ganchos de eventos são acionados apenas para eventos em que o nível de maturidade é STABLE.

[nível de maturidade](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/observability.html#schema)

Os ganchos de eventos são executados de forma assíncrona a partir de atualizações de pipeline, mas de forma síncrona com outros ganchos de eventos. Isso significa que apenas um único gancho de evento é executado por vez, e outros ganchos de eventos aguardam para serem executados até que o gancho de evento em execução no momento seja concluído. Se um gancho de evento for executado indefinidamente, ele bloqueará todos os outros ganchos de evento.

Delta Live Tables tenta executar cada gancho de evento em cada evento emitido durante uma atualização de pipeline. Para ajudar a garantir que os ganchos de eventos atrasados tenham tempo para processar todos os eventos enfileirados, o Delta Live Tables aguarda um período fixo não configurável antes de encerrar a compute que executa o pipeline. No entanto, não é garantido que todos os ganchos sejam acionados em todos os eventos antes do término da compute .

## Monitore o processamento do gancho de eventos

[](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/#monitor-event-hook-processing)

Use o tipo de evento hook_progress nos logs de eventos Delta Live Tables para monitorar o estado dos ganchos de eventos de uma atualização. Para evitar dependências circulares, os ganchos de eventos não são acionados para eventos hook_progress .

## Defina um gancho de evento

[](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/#define-an-event-hook)

Para definir um gancho de evento, use o decorador on_event_hook :

O max_allowable_consecutive_failures descreve o número máximo de vezes consecutivas que um gancho de evento pode falhar antes de ser desativado. Uma falha no gancho de evento é definida sempre que o gancho de evento lança uma exceção. Se um gancho de evento estiver desabilitado, ele não processará novos eventos até que o pipeline seja reiniciado.

max_allowable_consecutive_failures deve ser um número inteiro maior ou igual a 0 ou None. Um valor None (atribuído por default) significa que não há limite para o número de falhas consecutivas permitidas para o gancho de evento e que o gancho de evento nunca é desabilitado.

Falhas de ganchos de eventos e desativação de ganchos de eventos podem ser monitoradas nos logs de eventos como eventos hook_progress.

A função de gancho de evento deve ser uma função Python que aceita exatamente um parâmetro, uma representação de dicionário do evento que acionou esse gancho de evento. Qualquer valor de retorno da função de gancho de evento é ignorado.

## Exemplo: Selecione eventos específicos para processamento

[](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/#example-select-specific-events-for-processing)

O exemplo a seguir demonstra um gancho de evento que seleciona eventos específicos para processamento. Especificamente, este exemplo espera até que os eventos do pipeline STOPPING sejam recebidos e, em seguida, envia uma mensagem para os logs do driver stdout.

## Exemplo: Envie todos os eventos para um canal do Slack

[](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/#example-send-all-events-to-a-slack-channel)

O exemplo a seguir implementa um gancho de evento que envia todos os eventos recebidos para um canal do Slack usando a API do Slack.

Este exemplo usa um segredo do Databricks para armazenar com segurança os tokens necessários para autenticação na API do Slack.

[segredo](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/../security/secrets/index.html)

## Exemplo: Configurar um gancho de evento para desabilitar após quatro falhas consecutivas

[](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/#example-configure-an-event-hook-to-disable-after-four-consecutive-failures)

O exemplo a seguir demonstra como configurar um gancho de evento que será desabilitado se falhar consecutivamente quatro vezes.



## Exemplo: um pipeline Delta Live Tables com um gancho de evento

[](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/#example-a-delta-live-tables-pipeline-with-an-event-hook)

O exemplo a seguir demonstra a adição de um gancho de evento ao código-fonte de um pipeline. Este é um exemplo simples, mas completo, de uso de ganchos de eventos com um pipeline.

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/event-hooks.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
