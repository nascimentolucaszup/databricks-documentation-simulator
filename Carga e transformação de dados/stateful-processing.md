[Documentação](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/index.html)

[Carga e transformação de dados com Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/load-and-transform.html)

# Otimizar o processamento de estado em Delta Live Tables com marcas d'água

[](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/#optimize-stateful-processing-in-delta-live-tables-with-watermarks)

Para gerenciar efetivamente os dados mantidos no estado, use marcas d'água ao executar o processamento de transmissão com estado em Delta Live Tables, incluindo agregações, junções e desduplicação. Este artigo descreve como usar marcas d'água em suas consultas do Delta Live Tables e inclui exemplos das operações recomendadas.

Observação

Para garantir que as consultas que realizam agregações sejam processadas de forma incremental e não totalmente recalculadas a cada atualização, o senhor deve usar marcas d'água.

## O que é uma marca d'água?

[](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/#what-is-a-watermark)

No processamento de transmissão, uma marca d'água é um recurso do Apache Spark que pode definir um limite baseado em tempo para o processamento de dados ao realizar operações com estado, como agregações. Os dados que chegam são processados até que o limite seja atingido e, nesse momento, a janela de tempo definida pelo limite é fechada. As marcas d'água podem ser usadas para evitar problemas durante o processamento de consultas, principalmente ao processar um conjunto de dados maior ou um processamento de longa duração. Esses problemas podem incluir alta latência na produção de resultados e até mesmo erros fora da memória (OOM) devido à quantidade de dados mantidos em estado durante o processamento. Como os dados de transmissão são inerentemente não ordenados, as marcas d'água também suportam operações de cálculo corretas, como agregações de janelas de tempo.

Para saber mais sobre o uso de marcas d'água no processamento de transmissão, consulte Marca d' água na transmissão estruturada do Apache Spark e Aplicar marcas d'água para controlar o limite de processamento de dados.

[água na transmissão estruturada do Apache Spark](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/https://www.databricks.com/blog/2022/08/22/feature-deep-dive-watermarking-apache-spark-structured-streaming.html)

[Aplicar marcas d'água para controlar o limite de processamento de dados](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/../structured-streaming/watermarks.html)

## Como o senhor define uma marca d'água?

[](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/#how-do-you-define-a-watermark)

O senhor define uma marca d'água especificando um campo de registro de data e hora e um valor que representa o limite de tempo para a chegada de dados atrasados. Os dados são considerados atrasados se chegarem após o limite de tempo definido. Por exemplo, se o limite for definido como 10 minutos, os registros que chegarem após o limite de 10 minutos poderão ser descartados.

Como os registros que chegam após o limite definido podem ser descartados, é importante selecionar um limite que atenda aos seus requisitos de latência versus correção. A escolha de um limite menor faz com que os registros sejam emitidos mais cedo, mas também significa que os registros atrasados têm maior probabilidade de serem descartados. Um limite maior significa uma espera mais longa, mas possivelmente uma maior integridade dos dados. Devido ao tamanho maior do estado, um limite maior também pode exigir um recurso de computação adicional. Como o valor do limite depende de seus dados e dos requisitos de processamento, é importante testar e monitorar seu processamento para determinar o limite ideal.

O senhor usa a função withWatermark() em Python para definir uma marca d'água. No SQL, use a cláusula WATERMARK para definir uma marca d'água:

## Usar marcas d'água com junção de transmissão-transmissão

[](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/#use-watermarks-with-stream-stream-joins)

Para a união transmissão-transmissão, o senhor deve definir uma marca d'água em ambos os lados do site join e uma cláusula de intervalo de tempo. Como cada fonte join tem um view incompleto dos dados, a cláusula de intervalo de tempo é necessária para informar ao mecanismo de transmissão quando não é possível fazer mais correspondências. A cláusula de intervalo de tempo deve usar os mesmos campos usados para definir as marcas d'água.

Como pode haver ocasiões em que cada transmissão exija um limite diferente para marcas d'água, as transmissões não precisam ter o mesmo limite. Para evitar a falta de dados, o mecanismo de transmissão mantém uma marca d'água global com base na transmissão mais lenta.

O exemplo a seguir reúne uma transmissão de impressões de anúncios e uma transmissão de cliques de usuários em anúncios. Neste exemplo, um clique deve ocorrer dentro de 3 minutos após a impressão. Depois que o intervalo de tempo de 3 minutos passa, as linhas do estado que não podem mais ser correspondidas são descartadas.

## Realizar agregações em janelas com marcas d'água

[](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/#perform-windowed-aggregations-with-watermarks)

Uma operação com estado comum na transmissão de dados é a agregação em janelas. As agregações em janela são semelhantes às agregações agrupadas, exceto pelo fato de que os valores agregados são retornados para o conjunto de linhas que fazem parte da janela definida.

Uma janela pode ser definida como um determinado comprimento, e uma operação de agregação pode ser realizada em todas as linhas que fazem parte dessa janela. Spark streaming suporta três tipos de janelas:

Janelas de alternância (fixas): Uma série de intervalos de tempo de tamanho fixo, não sobrepostos e contíguos. Um registro de entrada pertence apenas a uma única janela.

Janelas deslizantes: Semelhante às janelas basculantes, as janelas deslizantes são de tamanho fixo, mas as janelas podem se sobrepor e um registro pode cair em várias janelas.

Quando os dados chegam após o final da janela mais o comprimento da marca d'água, nenhum dado novo é aceito para a janela, o resultado da agregação é emitido e o estado da janela é descartado.

O exemplo a seguir calcula uma soma de impressões a cada 5 minutos usando uma janela fixa. Neste exemplo, a cláusula select usa o alias impressions_window e, em seguida, a própria janela é definida como parte da cláusula GROUP BY. A janela deve ser baseada na mesma coluna de registro de data e hora da marca d'água, a coluna clickTimestamp neste exemplo.

Um exemplo semelhante em Python para calcular o lucro em janelas fixas por hora:

## Deduplicar registros de transmissão

[](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/#deduplicate-streaming-records)

A transmissão estruturada tem garantias de processamento exatamente único, mas não elimina automaticamente a duplicação de registros da fonte de dados. Por exemplo, como muitas filas de mensagens têm garantias de pelo menos uma vez, deve-se esperar registros duplicados ao ler de uma dessas filas de mensagens. É possível usar a função dropDuplicatesWithinWatermark() para eliminar a duplicação de registros em qualquer campo especificado, removendo duplicatas de uma transmissão mesmo que alguns campos sejam diferentes (como hora do evento ou hora de chegada). O senhor deve especificar uma marca d'água para usar a função dropDuplicatesWithinWatermark(). Todos os dados duplicados que chegam dentro do intervalo de tempo especificado pela marca d'água são descartados.

Os dados ordenados são importantes porque dados fora de ordem fazem com que o valor da marca d'água avance incorretamente. Então, quando os dados mais antigos chegam, eles são considerados atrasados e descartados. Use a opção withEventTimeOrder para processar o Snapshot inicial em ordem com base no registro de data e hora especificado na marca d'água. A opção withEventTimeOrder pode ser declarada no código que define o dataset ou nas configurações dopipeline  usando spark.databricks.delta.withEventTimeOrder.enabled. Por exemplo:

[configurações dopipeline](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/configure-pipeline.html)

Observação

A opção withEventTimeOrder é compatível apenas com o Python.

No exemplo a seguir, os dados são processados ordenados por clickTimestamp, e os registros que chegam dentro de 5 segundos um do outro e que contêm colunas userId e clickAdId duplicadas são descartados.

## Otimizar a configuração do pipeline para processamento com estado

[](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/#optimize-pipeline-configuration-for-stateful-processing)

Para ajudar a evitar problemas de produção e latência excessiva, o site Databricks recomenda ativar o gerenciamento de estado baseado em RocksDBpara o processamento de transmissão com estado, principalmente se o processamento exigir o salvamento de uma grande quantidade de estado intermediário.

As configurações do Severless Pipeline gerenciam automaticamente o armazenamento do estado.

O senhor pode ativar o gerenciamento de estado baseado em RocksDBdefinindo a seguinte configuração antes de implantar um pipeline:

Para saber mais sobre o RocksDB armazenamento do estado, incluindo recomendações de configuração para RocksDB, consulte Configure RocksDB armazenamento do estado em Databricks.

[Configure RocksDB armazenamento do estado em Databricks](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/../structured-streaming/rocksdb-state-store.html)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/stateful-processing.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
