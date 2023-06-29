---
title: 配置非生产管道
description: 了解如何配置非生产管道，以在部署到生产环境之前测试代码的质量。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 59%

---


# 配置非生产管道 {#configuring-non-production-pipelines}

了解如何配置非生产管道，以在部署到生产环境之前测试代码的质量。

## 非生产管道 {#non-production-pipelines}

除了部署到阶段和生产环境的[生产管道](#configuring-production-pipelines.md)外，您还可以设置非生产管道来验证代码。

有两种类型的非生产管道：

* **代码质量管道** – 这些代码质量管道将扫描 Git 分支中的代码并执行构建和代码质量步骤。
* **部署管道** – 除了执行代码质量管道等构建和代码质量步骤之外，这些管道还将代码部署到非生产环境。

>[!NOTE]
>
>在初始设置后，您可以[编辑管道设置](managing-pipelines.md)。

## 添加新的非生产管道 {#adding-non-production-pipeline}

在设置项目并具有至少一个使用 Cloud Manager UI 的环境后，便可以执行以下步骤来添加非生产管道。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从 Cloud Manager 主屏幕访问&#x200B;**管道**&#x200B;信息卡。 单击 **+添加** 并选择 **添加非生产管道**.

   ![添加非生产管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在&#x200B;**添加非生产管道**&#x200B;对话框的&#x200B;**配置**&#x200B;选项卡上，选择要添加的非生产管道的类型。

   * **代码质量管道** – 创建一个管道来构建您的代码、运行单元测试和评估代码质量但不部署。
   * **部署管道** – 创建一个管道来构建您的代码、运行单元测试、评估代码质量和部署到环境。

   ![“添加非生产管道”对话框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 提供&#x200B;**非生产管道名称**，识别您的管道以及以下附加信息。

   * **部署触发器** – 在定义启动管道的部署触发器时，您可以使用以下选项。

      * **手动** – 使用此选项可手动启动管道。
      * **关于Git更改**  — 只要将承诺添加到配置的Git分支，此选项就会启动CI/CD管道。 利用此选项，您仍能根据需要手动启动管道。

1. 如果您选择创建 **部署管道**，您还必须定义 **重要量度失败行为**.

   * **每次询问**  — 此行为是默认设置，需要对任何重要失败进行手动干预。
   * **立即失败**  — 如果选定此选项，则只要发生重要失败，就会取消管道。 它实际上是在模拟用户手动拒绝每个失败。
   * **立即继续**  — 如果选定此选项，则每当发生重要失败时，管道都会自动执行。 它实际上是在模拟用户手动批准每个失败。

1. 单击&#x200B;**“继续”**。

1. 在&#x200B;**添加非生产管道**&#x200B;对话框的&#x200B;**源代码**&#x200B;选项卡上，您必须选择管道应处理的代码类型。

   * **[前端代码](#front-end-code)**
   * **[全栈代码](#full-stack-code)**
   * **[Web 层配置](#web-tier-config)**

根据您选择的&#x200B;**源代码**&#x200B;选项，完成非生产管道创建的步骤有所不同。 按照上面的链接跳转到本文档的下一部分，以便您完成管道的配置。

### 前端代码 {#front-end-code}

前端代码管道部署包含一个或多个客户端 UI 应用程序的前端代码版本。 有关此类型管道的详细信息，请参阅 [CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)文档。

要完成前端代码非生产管道的配置，请执行以下步骤。

1. 在&#x200B;**源代码**&#x200B;选项卡上，必须定义以下选项。

   * **符合条件的部署环境** – 如果您的管道是部署管道，则必须选择应该部署到哪些环境。
   * **存储库**  — 此选项定义管道应从中检索代码的Git存储库。

   >[!TIP]
   > 
   >参见 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 这样您就可以了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支**  — 此选项定义所选管道中应从中检索代码的分支。
      * 输入分支名称的前几个字符以及此字段的自动完成功能。 它会查找可选择的匹配分支。
   * **代码位置** – 此选项定义管道应从中检索代码的所选存储库分支中的路径。

   ![前端管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. 单击“**保存**”。

管道已保存，您现在可以在[程序概述](managing-pipelines.md)页面的&#x200B;**管道**&#x200B;信息卡上&#x200B;**管理您的管道**。

### 全栈代码 {#full-stack-code}

全栈代码管道同时部署后端和前端代码构建，其中包含一个或多个 AEM 服务器应用程序以及 HTTPD/Dispatcher 配置。 有关此类型管道的详细信息，请参阅 [CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)文档。

>[!NOTE]
>
>如果所选环境存在全栈代码管道，则禁用此选择。

要完成全栈代码非生产管道的配置，请执行以下步骤。

1. 在&#x200B;**源代码**&#x200B;选项卡上，必须定义以下选项。

   * **符合条件的部署环境** – 如果您的管道是部署管道，则必须选择应该部署到哪些环境。
   * **存储库**  — 此选项定义管道应从中检索代码的Git存储库。

   >[!TIP]
   > 
   >参见 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 这样您就可以了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支**  — 此选项定义所选管道中应从中检索代码的分支。
      * 输入分支名称的前几个字符以及此字段的自动完成功能。 它可帮助您找到可选择的匹配分支。
   * **忽略Web层配置**  — 选中后，管道不会部署您的Web层配置。

   * **管道** – 如果您的管道是部署管道，则可以选择运行测试阶段。选中要在此阶段启用的选项。 如果未选择任何选项，则在管道运行期间不会显示测试阶段。

      * **产品功能测试** – 针对开发环境执行[产品功能测试](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)。
      * **自定义功能测试** - 针对开发环境执行[自定义功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)。
      * **自定义 UI 测试** – 为自定义应用程序执行[自定义 UI 测试](/help/implementing/cloud-manager/ui-testing.md)。

   ![全栈管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 单击“**保存**”。

管道已保存，您现在可以在[程序概述](managing-pipelines.md)页面的&#x200B;**管道**&#x200B;信息卡上&#x200B;**管理您的管道**。

### Web 层配置 {#web-tier-config}

Web层配置管道部署HTTPD/Dispatcher配置。 参见 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) 以了解有关此类型管道的更多信息。

>[!NOTE]
>
>如果所选环境存在Web层代码管道，则禁用此选择。

要完成 Web 层代码非生产管道的配置，请执行以下步骤。

1. 在&#x200B;**源代码**&#x200B;选项卡上，必须定义以下选项。

   * **符合条件的部署环境** – 如果您的管道是部署管道，则必须选择应该部署到哪些环境。
   * **存储库**  — 此选项定义管道应从中检索代码的Git存储库。

   >[!TIP]
   > 
   >参见 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 这样您就可以了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支**  — 此选项定义所选管道中应从中检索代码的分支。
   * **代码位置** – 此选项定义管道应从中检索代码的所选存储库分支中的路径。
      * 对于Web层配置管道，此路径通常包含 `conf.d`， `conf.dispatcher.d`、和 `opt-in` 目录。
      * 例如，如果项目结构是从 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans)生成的，路径将是 `/dispatcher/src`。

   ![Web 层管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. 单击“**保存**”。

>[!NOTE]
>
>如果将现有的全栈管道部署到环境中，则为同一环境创建 Web 层配置管道将忽略全栈管道中的现有 Web 层配置。

管道已保存，您现在可以在[程序概述](managing-pipelines.md)页面的&#x200B;**管道**&#x200B;信息卡上&#x200B;**管理您的管道**。

## 使用前端管道开发站点 {#developing-with-front-end-pipeline}

有了前端管道，前端开发人员可以获得更多的独立性，可加快开发过程。

请参阅文档[使用前端管道开发站点](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)，了解此流程的工作方式以及一些需要注意的事项，以便充分发挥此流程的潜力。

## 跳过 Dispatcher 程序包 {#skip-dispatcher-packages}

如果您希望将Dispatcher包作为管道的一部分构建，但又不希望将它们发布到构建存储中，则可以禁用发布它们，这可能会缩短管道运行持续时间。

必须通过您的项目添加以下禁用发布Dispatcher程序包的配置 `pom.xml` 文件。 它基于环境变量，作为一个标记，您可以在Cloud Manager构建容器中设置以定义何时应忽略Dispatcher包。

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
