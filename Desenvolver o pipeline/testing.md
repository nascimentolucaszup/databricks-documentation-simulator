[Documentação](https://docs.databricks.com/pt/delta-live-tables/testing.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/testing.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/testing.html/index.html)

[Desenvolver o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/testing.html/develop-pipelines.html)

# Dicas, recomendações e recursos para desenvolver e testar o pipeline Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/testing.html/#tips-recommendations-and-features-for-developing-and-testing-delta-live-tables-pipelines)

Este artigo descreve os padrões que o senhor pode usar para desenvolver e testar o pipeline Delta Live Tables. Por meio das configurações do pipeline, o Delta Live Tables permite que o senhor especifique configurações para isolar o pipeline em ambientes de desenvolvimento, teste e produção. As recomendações deste artigo se aplicam ao desenvolvimento dos códigos SQL e Python.

A Databricks recomenda o uso de parâmetros para escrever código extensível do Delta Live Tables. Isso é especialmente útil para escrever código portátil entre ambientes de desenvolvimento, teste e produção. Por exemplo, o senhor pode apontar o pipeline para dados de teste com problemas conhecidos para testar a resiliência do código. Consulte Controlar fonte de dados com parâmetros.

[Controlar fonte de dados com parâmetros](https://docs.databricks.com/pt/delta-live-tables/testing.html/parameters.html#test)

## Use o modo de desenvolvimento para executar atualizações de pipeline

[](https://docs.databricks.com/pt/delta-live-tables/testing.html/#use-development-mode-to-run-pipeline-updates)

Delta Live Tables tem um botão de alternância na interface do usuário para controlar se a execução das atualizações do pipeline está no modo de desenvolvimento ou de produção. Esse modo controla como as atualizações do pipeline são processadas, inclusive:

O modo de desenvolvimento não encerra imediatamente o compute recurso depois que uma atualização é bem-sucedida ou falha. O senhor pode reutilizar o mesmo recurso compute para executar várias atualizações pipeline sem esperar que uma cluster comece.

O modo de desenvolvimento não tenta novamente de forma automática em caso de falha na tarefa, o que permite detectar e corrigir imediatamente erros lógicos ou sintáticos no pipeline.

A Databricks recomenda o uso do modo de desenvolvimento durante o desenvolvimento e os testes. No entanto, quando for implantado em um ambiente de produção, sempre mude para o modo de produção.

Consulte Modos de desenvolvimento e produção.

[Modos de desenvolvimento e produção](https://docs.databricks.com/pt/delta-live-tables/testing.html/updates.html#optimize-execution)

## Teste o código-fonte do pipeline sem esperar a atualização das tabelas

[](https://docs.databricks.com/pt/delta-live-tables/testing.html/#test-pipeline-source-code-without-waiting-for-tables-to-update)

Para verificar problemas com o código-fonte do pipeline, como erros de sintaxe e análise, durante o desenvolvimento e teste, você pode executar um Validate update. Como uma atualização Validate verifica apenas a exatidão do código-fonte do pipeline sem executar uma atualização real em nenhuma tabela, você pode identificar e corrigir problemas mais rapidamente antes de executar uma atualização real do pipeline.

[Validate update](https://docs.databricks.com/pt/delta-live-tables/testing.html/updates.html#validate-update)

## Especifique um esquema de destino durante todas as fases do ciclo de vida do desenvolvimento

[](https://docs.databricks.com/pt/delta-live-tables/testing.html/#specify-a-target-schema-during-all-development-lifecycle-phases)

Todos os conjuntos de dados em um Delta Live Tables pipeline fazem referência ao esquema virtual LIVE, que é inacessível fora do pipeline. Se um esquema de destino for especificado, o esquema virtual LIVE apontará para o esquema de destino. Você deve especificar um esquema de destino para revisar os resultados gravados em cada tabela durante uma atualização.

Você deve especificar um esquema de destino exclusivo para seu ambiente. Cada tabela em um determinado esquema só pode ser atualizada por um único pipeline.

O senhor pode isolar esses ambientes criando um pipeline separado para desenvolvimento, teste e produção com alvos diferentes. O uso do parâmetro target schema permite que o senhor remova a lógica que usa interpolação de strings ou outros widgets ou parâmetros para controlar fontes de dados e alvos.

Consulte Usar Unity Catalog com seu pipeline Delta Live Tables  e Usar o pipeline Delta Live Tables com o legado Hive metastore.

[Usar Unity Catalog com seu pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/testing.html/unity-catalog.html)

[Usar o pipeline Delta Live Tables com o legado Hive metastore](https://docs.databricks.com/pt/delta-live-tables/testing.html/hive-metastore.html)

## Use as pastas Git do Databricks para gerenciar o pipeline do Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/testing.html/#use-databricks-git-folders-to-manage-delta-live-tables-pipelines)

A Databricks recomenda o uso de pastas Git durante o desenvolvimento, o teste e a implantação do pipeline do Delta Live Tables na produção. As pastas do Git permitem o seguinte:

Acompanhar como o código está mudando ao longo do tempo.

Mesclando as mudanças que vários desenvolvedores estão fazendo.

Práticas de desenvolvimento de software, como revisões de código.

Databricks recomenda configurar um único repositório Git para todo o código relacionado a um pipeline.

Cada desenvolvedor deve ter sua própria pasta Git da Databricks configurada para desenvolvimento. Durante o desenvolvimento, o usuário configura seu próprio pipeline na pasta Databricks Git e testa a nova lógica usando o conjunto de dados de desenvolvimento, o esquema isolado e os locais. Depois de concluir o trabalho de desenvolvimento, o usuário faz o commit e envia as alterações de volta para sua ramificação no repositório central do Git e abre uma solicitação pull na ramificação de teste ou QA.

O branch resultante deve ser verificado em uma pasta Databricks Git e um pipeline deve ser configurado usando um conjunto de dados de teste e um esquema de desenvolvimento. Supondo que a lógica seja executada conforme o esperado, um pull request ou branch de liberação deve ser preparado para enviar as alterações para a produção.

Embora as pastas do Git possam ser usadas para sincronizar o código entre os ambientes, as configurações do pipeline devem ser mantidas atualizadas manualmente ou usando ferramentas como o Terraform.

Esse fluxo de trabalho é semelhante ao uso de pastas Git para CI/CD em todos os trabalhos do Databricks. Consulte as técnicas de CI/CD com pastas Git e Databricks Git (Repos).

[as técnicas de CI/CD com pastas Git e Databricks Git (Repos)](https://docs.databricks.com/pt/delta-live-tables/testing.html/../repos/ci-cd-techniques-with-repos.html)

## Código-fonte do segmento para ingestão e transformações dos passos

[](https://docs.databricks.com/pt/delta-live-tables/testing.html/#segment-source-code-for-ingestion-and-transformation-steps)

Databricks recomenda isolar as consultas que ingerem dados da lógica de transformações que enriquece e valida os dados. Se o senhor organizar o código-fonte para ingestão de dados de desenvolvimento ou teste de fonte de dados em um diretório separado da lógica de ingestão de dados de produção, poderá configurar o pipeline para vários ambientes com um conjunto de dados específico para esses ambientes. Por exemplo, o senhor pode acelerar o desenvolvimento usando um conjunto de dados menor para testes. Consulte Criar conjunto de dados de amostra para desenvolvimento e teste.

[Criar conjunto de dados de amostra para desenvolvimento e teste](https://docs.databricks.com/pt/delta-live-tables/testing.html/#sample-data)

O senhor também pode usar parâmetros para controlar a fonte de dados para desenvolvimento, teste e produção. Consulte Usar parâmetros com o pipeline Delta Live Tables .

[Usar parâmetros com o pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/testing.html/parameters.html)

Como o pipeline Delta Live Tables usa o esquema virtual LIVE para gerenciar todos os relacionamentos dataset, ao configurar o pipeline de desenvolvimento e teste com o código-fonte de ingestão que carrega dados de amostra, o senhor pode substituir o conjunto de dados de amostra usando nomes de tabelas de produção para testar o código. A mesma lógica de transformações pode ser usada em todos os ambientes.

## Crie conjuntos de dados de amostra para desenvolvimento e teste

[](https://docs.databricks.com/pt/delta-live-tables/testing.html/#create-sample-datasets-for-development-and-testing)

Databricks recomenda a criação de conjuntos de dados de desenvolvimento e teste para testar a lógica do pipeline com dados esperados e registros potencialmente malformados ou corrompidos. Há várias maneiras de criar conjuntos de dados que podem ser úteis para desenvolvimento e teste, incluindo as seguintes:

Selecione um subconjunto de dados de um dataset de produção.

Use dados anônimos ou gerados artificialmente para fontes que contenham PII.

Crie dados de teste com resultados bem definidos com base na lógica downstream das transformações.

Antecipe a possível corrupção de dados, registros malformados e alterações de dados upstream criando registros que quebram as expectativas do esquema de dados.

Por exemplo, se você tiver um Notebook que defina um dataset usando o seguinte código:

Você pode criar um dataset de amostra contendo registros específicos usando uma query como a seguinte:

O exemplo a seguir demonstra a filtragem de dados publicados para criar um subconjunto dos dados de produção para desenvolvimento ou teste:

Para usar esses diferentes dataset, crie vários pipelines com o Notebook implementando a lógica das transformações. Cada pipeline pode ler dados do dataset LIVE.input_data, mas é configurado para incluir o Notebook que cria o dataset específico para o ambiente.



© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/testing.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/testing.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/testing.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/testing.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/testing.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/testing.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/testing.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/testing.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
