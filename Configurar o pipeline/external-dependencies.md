[Documentação](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/index.html)

[Configurar um pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/configure-pipeline.html)

# Gerenciar as dependências do Python para o pipeline Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/#manage-python-dependencies-for-delta-live-tables-pipelines)

Delta Live Tables oferece suporte a dependências externas em seus pipelines. Databricks recomenda usar um dos dois padrões para instalar pacotes Python:

Use o comando %pip install para instalar pacotes para todos os arquivos de origem em um pipeline.

Importar módulos ou biblioteca do código-fonte armazenado em arquivos workspace. Consulte Importar módulos Python de pastas Git ou arquivos de espaço de trabalho.

[Importar módulos Python de pastas Git ou arquivos de espaço de trabalho](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/import-workspace-files.html)

Delta Live Tables também oferece suporte ao  uso init script com escopo globale clusters . No entanto, essas dependências externas, particularmente init script, aumentam o risco de problemas com atualizações de Runtime . Para atenuar esses riscos, minimize o uso init script em seus pipelines. Se o processamento exigir init script, automatize o teste do pipeline para detectar problemas antecipadamente. Se você usar init script, o Databricks recomenda aumentar sua frequência de teste.

[uso init script](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/../init-scripts/index.html)

Importante

Como a biblioteca JVM não é suportada no pipeline Delta Live Tables, não use um init script para instalar a biblioteca JVM. No entanto, você pode instalar outros tipos de bibliotecas, como bibliotecas Python, com um init script.

[a biblioteca JVM não é suportada](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/#jvm-library-support)

## bibliotecas Python

[](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/#python-libraries)

Para especificar bibliotecas Python externas, use o comando mágico %pip install . Quando uma atualização começar, o Delta Live Tables executa todas as células contendo um comando %pip install antes de executar qualquer definição de tabela. Cada Notebook Python incluído no pipeline compartilha um ambiente de biblioteca e tem acesso a todas as bibliotecas instaladas.

Importante

%pip install comando deve estar em uma célula separada na parte superior do pipeline do Delta Live Tables Notebook. Não inclua nenhum outro código nas células que contêm o comando %pip install.

Como cada Notebook em um pipeline compartilha um ambiente de biblioteca, você não pode definir diferentes versões de biblioteca em um único pipeline. Se seu processamento exigir diferentes versões de biblioteca, você deverá defini-las em diferentes pipelines.

O exemplo a seguir instala a biblioteca numpy e a disponibiliza globalmente para qualquer Notebook Python no pipeline:

Para instalar um pacote Python wheel, adicione o caminho do Python wheel ao comando %pip install. O pacote Python wheel instalado está disponível para todas as tabelas no pipeline. O exemplo a seguir instala um arquivo Python wheel chamado dltfns-1.0-py3-none-any.whl a partir de um volume Unity Catalog:

Consulte Instalar um pacote Python wheel com %pip.

[Instalar um pacote Python wheel com %pip](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/../libraries/notebooks-python-libraries.html#pip-install-wheel)

## Posso usar bibliotecas Scala ou Java em um pipeline Delta Live Tables?

[](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/#can-i-use-scala-or-java-libraries-in-a-delta-live-tables-pipeline)

Não, Delta Live Tables oferece suporte apenas a SQL e Python. Você não pode usar a biblioteca JVM em um pipeline. A instalação da biblioteca JVM causará um comportamento imprevisível e poderá interromper versões futuras do Delta Live Tables. Se o seu pipeline usar um init script, você também deverá garantir que a biblioteca JVM não seja instalada pelo script.



© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/external-dependencies.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
