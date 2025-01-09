[Documentação](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/index.html)

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/configure-pipeline.html)

# Modo de pipeline acionado vs. contínuo

[](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/#triggered-vs-continuous-pipeline-mode)

Este artigo descreve a semântica operacional dos modos pipeline acionado e contínuo para Delta Live Tables.

O modo de pipeline é independente do tipo de tabela que está sendo computada. Tanto a visualização materializada quanto as tabelas de transmissão podem ser atualizadas no modo pipeline.

Para alternar entre acionado e contínuo, use a opção de modo de pipeline nas configurações do pipeline ao criar ou editar um pipeline. Consulte Configurar um pipeline do Delta Live Tables.

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/configure-pipeline.html)

Observação

As operações de atualização para visualização materializada e tabelas de transmissão definidas em Databricks SQL sempre são executadas usando o modo pipeline acionado.

## O que é o modo de pipeline acionado?

[](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/#what-is-triggered-pipeline-mode)

Se o site pipeline usar o modo acionado, o sistema interromperá o processamento após atualizar com êxito todas as tabelas ou tabelas selecionadas, garantindo que cada tabela na atualização seja atualizada com base nos dados disponíveis quando a atualização começar.

## O que é o modo de pipeline contínuo?

[](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/#what-is-continuous-pipeline-mode)

Se o pipeline usa execução contínua, o Delta Live Tables processa novos dados à medida que eles chegam na fonte de dados para manter as tabelas em todo o pipeline atualizadas.

Para evitar o processamento desnecessário no modo de execução contínua, o pipeline monitora automaticamente as tabelas dependentes do Delta e executa uma atualização somente quando o conteúdo dessas tabelas dependentes é alterado.

## Escolha um modo de pipeline de dados

[](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/#choose-a-data-pipeline-modes)

A tabela a seguir destaca as diferenças entre os modos de pipeline acionado e contínuo:

| questões-chave | Acionado | Contínuo |
| --- | --- | --- |
| Quando a atualização é interrompida? | Automaticamente, uma vez concluído. | execução contínua até a interrupção manual. |
| Quais dados são processados? | Dados disponíveis quando a atualização começar. | Todos os dados à medida que chegam às fontes configuradas. |
| Para quais requisitos de atualização de dados isso é melhor? | Os dados são atualizados a cada 10 minutos, de hora em hora ou diariamente. | As atualizações de dados são desejadas entre cada 10 segundos e alguns minutos. |


questões-chave

Acionado

Contínuo

Quando a atualização é interrompida?

Automaticamente, uma vez concluído.

execução contínua até a interrupção manual.

Quais dados são processados?

Dados disponíveis quando a atualização começar.

Todos os dados à medida que chegam às fontes configuradas.

Para quais requisitos de atualização de dados isso é melhor?

Os dados são atualizados a cada 10 minutos, de hora em hora ou diariamente.

As atualizações de dados são desejadas entre cada 10 segundos e alguns minutos.

O pipeline acionado pode reduzir o consumo de recursos e as despesas porque a execução do cluster dura apenas o tempo suficiente para atualizar o pipeline. No entanto, os novos dados não serão processados até que o pipeline seja acionado. clusterO pipeline contínuo exige um sistema sempre em execução, que é mais caro, mas reduz a latência do processamento.

## Definir intervalo de disparo para pipeline contínuo

[](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/#set-trigger-interval-for-continuous-pipelines)

Ao configurar o pipeline para o modo contínuo, o senhor pode definir intervalos de acionamento para controlar a frequência com que o pipeline começa uma atualização para cada fluxo.

O senhor pode usar pipelines.trigger.interval para controlar o intervalo de acionamento de um fluxo que atualiza uma tabela ou um pipeline inteiro. Como o site pipeline acionado processa cada tabela uma vez, o pipelines.trigger.interval é usado somente com o pipeline contínuo.

Databricks recomenda a definição de pipelines.trigger.interval em tabelas individuais porque as consultas de transmissão e lotes têm padrões diferentes. Defina o valor em um pipeline somente quando o processamento exigir o controle de atualizações para todo o gráfico do pipeline.

O senhor define pipelines.trigger.interval em uma tabela usando spark_conf em Python ou SET em SQL:

Para definir pipelines.trigger.interval em um pipeline, adicione-o ao objeto configuration nas configurações do pipeline:

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/pipeline-mode.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
