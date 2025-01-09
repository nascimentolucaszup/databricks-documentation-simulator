[Documentação](https://docs.databricks.com/pt/delta-live-tables/privileges.html/../index.html)

[Engenharia de dados com Databricks](https://docs.databricks.com/pt/delta-live-tables/privileges.html/../data-engineering.html)

[O que é o Delta Live Tables?](https://docs.databricks.com/pt/delta-live-tables/privileges.html/index.html)

# Gerenciar identidades, permissões e privilégios para o pipeline Delta Live Tables

[](https://docs.databricks.com/pt/delta-live-tables/privileges.html/#manage-identities-permissions-and-privileges-for-delta-live-tables-pipelines)

Este artigo fornece uma visão geral das identidades, permissões e privilégios do pipeline Delta Live Tables.

Databricks recomenda usar Unity Catalog para todos os novos pipelines Delta Live Tables. Por default, a visualização materializada e as tabelas de transmissão criadas pelo pipeline configurado com Unity Catalog só podem ser consultadas pelo proprietário pipeline. Consulte Usar Unity Catalog com seu pipeline Delta Live Tables .

[Usar Unity Catalog com seu pipeline Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/privileges.html/unity-catalog.html)

Se o seu pipeline publicar um conjunto de dados no legado Hive metastore, consulte Usar o pipeline Delta Live Tables com o legado Hive metastore.

[Usar o pipeline Delta Live Tables com o legado Hive metastore](https://docs.databricks.com/pt/delta-live-tables/privileges.html/hive-metastore.html)

Para ver as melhores práticas gerais sobre configurações de identidade, consulte Práticas recomendadas de identidade.

[Práticas recomendadas de identidade](https://docs.databricks.com/pt/delta-live-tables/privileges.html/../admin/users-groups/best-practices.html)

## Qual identidade é usada para atualizações de pipeline?

[](https://docs.databricks.com/pt/delta-live-tables/privileges.html/#what-identity-is-used-for-pipeline-updates)

Delta Live Tables O processo de pipeline atualiza usando a identidade do proprietário do pipeline. Atribua um novo proprietário ao pipeline para alterar a identidade usada para executar o pipeline.

Databricks recomenda definir uma entidade de serviço como o proprietário do site pipeline. Consulte gerenciar entidade de serviço.

[gerenciar entidade de serviço](https://docs.databricks.com/pt/delta-live-tables/privileges.html/../admin/users-groups/service-principals.html)

## Quem pode executar a atualização do site pipeline?

[](https://docs.databricks.com/pt/delta-live-tables/privileges.html/#who-can-run-a-pipeline-update)

As atualizações do pipeline podem ser executadas por qualquer usuário ou entidade de serviço com as permissões CAN RUN, CAN MANAGE ou IS OWNER.

## Configurar permissões de pipeline

[](https://docs.databricks.com/pt/delta-live-tables/privileges.html/#configure-pipeline-permissions)

O senhor deve ter a permissão CAN MANAGE ou IS OWNER no pipeline para gerenciar as permissões. O pipeline usa listas de controle de acesso (ACLs) para controlar as permissões. Para obter uma lista completa de permissões e suas habilidades, consulte ACLs de pipeline do Delta Live Tables.

[ACLs de pipeline do Delta Live Tables](https://docs.databricks.com/pt/delta-live-tables/privileges.html/../security/auth/access-control/index.html#dlt)

Na barra lateral, clique em Delta Live Tables.

Selecione o nome de um pipeline.

Clique em  e selecione Permissões.

![Menu kebab](https://docs.databricks.com/pt/delta-live-tables/privileges.html/../_images/kebab-menu.png)

Em Permissions Settings (Configurações de permissões), selecione o menu suspenso Select User, Group or entidade de serviço e, em seguida, selecione um usuário, grupo ou entidade de serviço.

Selecione uma permissão no dropdown de permissões.

Clique em Adicionar.

Clique em Salvar.

## Permitir que usuários não administradores visualizem os logs de driver de um pipeline habilitado para o Unity Catalog

[](https://docs.databricks.com/pt/delta-live-tables/privileges.html/#allow-non-admin-users-to-view-the-driver-logs-from-a-unity-catalog-enabled-pipeline)

Por default, somente o proprietário do pipeline e os administradores do workspace podem view o driver logs do cluster que executa um Unity Catalog habilitado pipeline. O senhor pode habilitar o acesso aos logs de driver para qualquer usuário com permissões CAN MANAGE, CAN VIEW ou CAN RUN adicionando o seguinte parâmetro de configuração do Spark ao objeto configuration nas configurações do pipeline:

[permissões CAN MANAGE, CAN VIEW ou CAN RUN](https://docs.databricks.com/pt/delta-live-tables/privileges.html/../security/auth/access-control/index.html#dlt)

© Databricks 2025. Todos os direitos reservados. Apache, Apache Spark, Spark e o logotipo do Spark são marcas registradas da Apache Software Foundation.

[Apache Software Foundation](https://docs.databricks.com/pt/delta-live-tables/privileges.html/http://www.apache.org/)

Envie-nos seus comentários | Aviso de privacidade | Termos de uso | Declaração sobre escravidão moderna | Privacidade na Califórnia | Suas opções de privacidade

[Envie-nos seus comentários](https://docs.databricks.com/pt/delta-live-tables/privileges.html/mailto:doc-feedback@databricks.com?subject=Documentation%20Feedback)

[Aviso de privacidade](https://docs.databricks.com/pt/delta-live-tables/privileges.html/https://www.databricks.com/legal/privacynotice)

[Termos de uso](https://docs.databricks.com/pt/delta-live-tables/privileges.html/https://www.databricks.com/terms-of-use)

[Declaração sobre escravidão moderna](https://docs.databricks.com/pt/delta-live-tables/privileges.html/https://www.databricks.com/legal/modern-slavery-policy-statement)

[Privacidade na Califórnia](https://docs.databricks.com/pt/delta-live-tables/privileges.html/https://www.databricks.com/legal/supplemental-privacy-notice-california-residents)

[Suas opções de privacidade](https://docs.databricks.com/pt/delta-live-tables/privileges.html/javascript:%20OneTrust.ToggleInfoDisplay())

![](https://docs.databricks.com/pt/delta-live-tables/privileges.html/https://www.databricks.com/sites/default/files/2022-12/gpcicon_small.png)
