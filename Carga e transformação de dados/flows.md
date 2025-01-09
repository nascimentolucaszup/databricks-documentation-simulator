[Documentação](https://docs.databricks.com/pt/delta-live-tables/flows.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/flows.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/flows.html/index.html)

[Carregue e transforme dados com o Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/flows.html/load-and-transform.html)

# Carregue e processe dados gradualmente com os fluxos do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/flows.html/#load-and-process-data-incrementally-with-delta-live-tables-flows)

Este artigo explica o que são fluxos e como utilizar fluxos em pipelines do Delta Live Tables para processar dados gradualmente de uma tabela de transmissão de origem para uma tabela de transmissão de destino. No Delta Live Tables, os fluxos são definidos de duas maneiras:

Um fluxo é definido automaticamente quando você cria uma consulta que atualiza uma tabela de transmissão.

O Delta Live Tables também oferece funcionalidade para definir explicitamente fluxos para processamento mais complexo, como anexar a uma tabela de transmissão a partir de várias fontes de transmissão.

Este artigo discute os fluxos implícitos criados quando você define uma consulta para atualizar uma tabela de transmissão e, em seguida, apresenta detalhes sobre a sintaxe para definir fluxos mais complexos.

## O que é um fluxo?

[](https://docs.databricks.com/pt/delta-live-tables/flows.html/#what-is-a-flow)

No Delta Live Tables, um fluxo é uma consulta de transmissão que processa dados de origem gradualmente para atualizar uma tabela de transmissão de destino. A maioria dos datasets do Delta Live Tables que você cria em um pipeline define o fluxo como parte da consulta e não exige a definição explícita do fluxo. Por exemplo, você cria uma tabela de transmissão no Delta Live Tables em um único comando DDL em vez de utilizar instruções de tabela e fluxo separadas para criar a tabela de transmissão:

Observação

Este exemplo CREATE FLOW é apresentado somente para fins ilustrativos e contém palavras-chave que não são válidas na sintaxe do Delta Live Tables.



Além do fluxo padrão definido por uma consulta, as interfaces em Python e SQL do Delta Live Tables oferecem a funcionalidade de fluxo de acréscimo. O fluxo de acréscimo é compatível com processamentos que exigem a leitura de dados de várias fontes de transmissão para atualizar uma única tabela de transmissão. Por exemplo, utilize a funcionalidade fluxo de acréscimo quando tiver uma tabela e um fluxo de transmissão existentes e quiser adicionar uma nova fonte de transmissão que grave nessa tabela de transmissão existente.

## Utilize o fluxo de acréscimo para gravar em uma tabela de transmissão a partir de vários transmissões de origem

[](https://docs.databricks.com/pt/delta-live-tables/flows.html/#use-append-flow-to-write-to-a-streaming-table-from-multiple-source-streams)

Utilize o decorador @append_flow na interface em Python ou a cláusula CREATE FLOW na interface em SQL para gravar em uma tabela de transmissão a partir de várias fontes de transmissão. Utilize o fluxo de acréscimo para tarefas de processamento como as seguintes:

Adicione fontes de transmissão que acrescentam dados a uma tabela de transmissão existente sem exigir uma atualização completa. Por exemplo, você pode ter uma tabela combinando dados regionais de cada região em que opera. À medida que novas regiões forem distribuídas, você poderá adicionar os dados da nova região à tabela sem executar uma atualização completa. Consulte Exemplo: Gravar em uma tabela de transmissão a partir de vários tópicos do Kafka.

[Exemplo: Gravar em uma tabela de transmissão a partir de vários tópicos do Kafka](https://docs.databricks.com/pt/delta-live-tables/flows.html/#multiple-sources)

Atualize uma tabela de transmissão anexando dados históricos ausentes (preenchimento). Por exemplo, você tem uma tabela de transmissão existente gravada por um tópico do Apache Kafka. Você tem também dados históricos armazenados em uma tabela que precisa ser inserida exatamente uma vez na tabela de transmissão e não pode transmitir os dados porque seu processamento inclui a execução de uma agregação complexa antes de inserir os dados. Consulte Exemplo: Executar um preenchimento de dados único.

[Exemplo: Executar um preenchimento de dados único](https://docs.databricks.com/pt/delta-live-tables/flows.html/#backfill)

Combine dados de diversas fontes e grave em uma única tabela de transmissão em vez de utilizar a cláusula UNION em uma consulta. O uso do processamento de fluxo de acréscimo em vez de UNION possibilita que você atualize a tabela de destino gradualmente sem executar uma atualização de atualização completa. Veja o exemplo: Usar processamento de fluxo de acréscimo em vez de UNION.

[atualização de atualização completa](https://docs.databricks.com/pt/delta-live-tables/flows.html/updates.html#refresh-semantics)

[exemplo: Usar processamento de fluxo de acréscimo em vez de UNION](https://docs.databricks.com/pt/delta-live-tables/flows.html/#replace-union)

O destino da saída de registros pelo processamento do fluxo de acréscimo pode ser uma tabela existente ou uma nova tabela. Para consultas em Python, utilize a função create_transmissão_table() para criar uma tabela de destino.

[create_transmissão_table()](https://docs.databricks.com/pt/delta-live-tables/flows.html/python-ref.html#create-target-fn)

Importante

Se você tiver que definir restrições de qualidade de dados com expectativas, defina as expectativas na tabela de destino como parte da função create_streaming_table() ou em uma definição de tabela existente. Você não pode definir expectativas na definição @append_flow .

[expectativas](https://docs.databricks.com/pt/delta-live-tables/flows.html/expectations.html)

Os fluxos são identificados por um nome de fluxo e esse nome é usado para identificar pontos de verificação de transmissão. O uso do nome do fluxo para identificar o ponto de verificação significa o seguinte:

Se um fluxo existente em um pipeline for renomeado, o ponto de verificação não será transferido e o fluxo renomeado será efetivamente um fluxo totalmente novo.

você não pode reutilizar um nome de fluxo em um pipeline porque o ponto de verificação existente não corresponderá à nova definição de fluxo.

Veja a seguir a sintaxe de @append_flow

## Exemplo: escrever em uma tabela de transmissão a partir de vários tópicos do Kafka

[](https://docs.databricks.com/pt/delta-live-tables/flows.html/#example-write-to-a-streaming-table-from-multiple-kafka-topics)

Os exemplos a seguir criam uma tabela de transmissão chamada kafka_target e grava nessa tabela de transmissão a partir de dois tópicos de Kafka:

Para saber mais sobre a função de valor de tabela read_kafka() usada nas consultas SQL, consulte read_kafka na referência da linguagem SQL.

[read_kafka](https://docs.databricks.com/pt/delta-live-tables/flows.html/../sql/language-manual/functions/read_kafka.html)

## Exemplo: executar um preenchimento único de dados

[](https://docs.databricks.com/pt/delta-live-tables/flows.html/#example-run-a-one-time-data-backfill)

Os exemplos a seguir executam uma consulta para acrescentar dados históricos a uma tabela de transmissão:

Observação

Para garantir um verdadeiro preenchimento único quando a consulta de backfill fizer parte de um pipeline executado de forma agendada ou contínua, remova a consulta depois de executar o pipeline uma vez. Para acrescentar novos dados se eles chegarem no diretório de backfill, deixe a consulta no lugar.

## Exemplo: utilize o processamento de fluxo de acréscimo em vez de UNION

[](https://docs.databricks.com/pt/delta-live-tables/flows.html/#example-use-append-flow-processing-instead-of-union)

Em vez de utilizar uma consulta com uma cláusula UNION, você pode utilizar consultas de fluxo de acréscimo para combinar várias fontes e gravar em uma única tabela de transmissão. O uso de consultas de fluxo de acréscimo em vez de UNION possibilita que você anexe a uma tabela de transmissão de várias fontes sem executar uma atualização completa.

[atualização completa](https://docs.databricks.com/pt/delta-live-tables/flows.html/updates.html#refresh-semantics)

O exemplo de Python a seguir inclui uma consulta que combina várias fontes de dados com uma cláusula UNION:

Os exemplos a seguir substituem a consulta UNION por consultas de fluxo de acréscimo:

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/flows.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/flows.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/flows.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/flows.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/flows.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/flows.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/flows.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/flows.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
