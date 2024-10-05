---
title: 添加生产管道
description: 了解如何添加生产管道以生成代码并将其部署到生产环境。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 66%

---


# 添加生产管道 {#configure-production-pipeline}

了解如何配置生产管道以生成代码并将其部署到生产环境。 生产管道首先将代码部署到暂存环境，并在获得批准后将相同的代码部署到生产环境。

用户必须具有&#x200B;**[部署管理员](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能配置生产管道。

>[!NOTE]
>
>在程序创建完成、Git存储库至少有一个分支以及创建生产和暂存环境集之前，无法设置生产管道。

在开始部署代码之前，必须从 [!UICONTROL Cloud Manager] 配置管道设置。

>[!NOTE]
>
>在初始设置后，您可以[编辑管道设置](managing-pipelines.md)。

## 添加新的生产管道 {#adding-production-pipeline}

在设置项目并具有至少一个使用 [!UICONTROL Cloud Manager] UI 的环境后，便可以执行以下步骤来添加非生产管道。

>[!TIP]
>
>在配置前端管道之前，请参阅 [AEM 快速网站创建历程](/help/journey-sites/quick-site/overview.md)，获取易于使用的“AEM 快速站点创建”工具的端到端指南。这段历程将帮助您简化 AEM 站点的前端开发，使您能够在不了解 AEM 后端的情况下快速定制站点。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;卡并单击&#x200B;**添加**&#x200B;以选择&#x200B;**添加生产管道**。

   ![在“程序管理员”概述中的“管道”信息卡](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. 此时会显示&#x200B;**添加生产管道**&#x200B;对话框。提供&#x200B;**管道名称**，识别您的管道以及以下选项。单击&#x200B;**“继续”**。

   **部署触发器** – 在定义启动管道的部署触发器时，您可以使用以下选项。

   * **手动** – 使用此选项可手动启动管道。
   * **在 Git 发生更改时** – 只要将承诺添加到配置的 Git 分支，此选项就会启动 CI/CD 管道。利用此选项，您仍能根据需要手动启动管道。

   **重要量度失败行为r** – 在管道设置或编辑期间，**部署管理员**&#x200B;可以选择定义在任何质量审核出现重要失败时的管道行为。可用的选项为：

   * **每次询问** – 这是默认设置，需要对任何重要失败进行手动干预。
   * **立即失败** – 如果选定此选项，则只要发生重要失败，就会取消管道。这实际上是在模拟用户手动拒绝每个失败。
   * **立即继续** – 如果选定此选项，则每当发生重要失败时，管道就会自动继续。这实际上是在模拟用户手动批准每个失败。

   ![生产管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 在&#x200B;**Source代码**&#x200B;选项卡上，您必须选择管道应处理的代码类型。

   * **[全栈代码](#full-stack-code)**
   * **[目标部署](#targeted-deployment)**

有关管道类型的更多信息，请参阅[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

根据您选择的源代码类型，完成生产管道创建的步骤有所不同。 按照上面的链接跳到本文档的下一节，完成管道的配置。

### 全栈代码 {#full-stack-code}

全栈代码管道同时部署后端和前端代码构建，其中包含一个或多个AEM服务器应用程序以及HTTPD/Dispatcher配置。

>[!NOTE]
>
>如果所选环境已存在全栈代码管道，则会禁用此选择。

要完成全栈代码生产管道的配置，请执行以下步骤。

1. 在&#x200B;**源代码**&#x200B;选项卡上，必须定义以下选项。

   * **存储库** – 此选项定义管道应从中检索代码的 Git 存储库。

   >[!TIP]
   > 
   >请参阅[添加和管理存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)文档，了解如何在 Cloud Manager 中添加和管理存储库。

   * **Git 分支** – 此选项定义管道应从中检索代码的所选存储库的分支。
      * 输入分支名称的前几个字符，此字段的自动完成功能将查找匹配的分支帮助您做选择。
   * **忽略 Web 层配置** – 勾选后，该管道不会部署您的 Web 层配置。
   * **部署到生产之前暂停** – 此选项在部署到生产之前暂停管道。
   * **已计划** – 此选项允许用户启用计划的生产部署。

   ![全栈代码](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 点按或单击&#x200B;**继续**&#x200B;前进到&#x200B;**体验审核**&#x200B;选项卡，您可以在其中定义应始终包含在体验审核中的路径。

   ![添加体验审核](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. 提供要包含在体验审核中的路径。

   * 有关详细信息，请参阅文档[体验审核测试](/help/implementing/cloud-manager/experience-audit-dashboard.md#configuration)。

1. 单击&#x200B;**保存**&#x200B;以保存管道。

为体验审核配置的路径会提交给服务，并在管道运行时根据性能、可访问性、SEO（搜索引擎优化）、最佳实践和 PWA（Progressive Web 应用程序）测试进行评估。有关更多详细信息，请参阅[了解体验审核结果。](/help/implementing/cloud-manager/experience-audit-dashboard.md)

管道已保存，您现在可以在[程序概述](managing-pipelines.md)页面的&#x200B;**管道**&#x200B;信息卡上&#x200B;**管理您的管道**。

### 有针对性的部署 {#targeted-deployment}

目标部署仅会为AEM应用程序的选定部分部署代码。 在此类部署中，您可以选择&#x200B;**包含**&#x200B;以下代码类型之一：

* **配置** — 配置AEM环境中各种功能的设置。
   * 请参阅[使用配置管道](/help/operations/config-pipeline.md)以获取支持的配置列表，包括日志转发、清除相关的维护任务和各种CDN配置，并在存储库中管理这些配置以便正确部署它们。
   * 运行目标部署管道时，将部署配置，前提是这些配置已保存到您在管道中定义的环境、存储库和分支中。
   * 在任何时候，每个环境只能有一个配置管道。
* **前端代码** — 为AEM应用程序的前端配置JavaScript和CSS。
   * 有了前端管道，前端开发人员可以获得更多的独立性，可加快开发过程。
   * 请参阅文档[使用前端管道开发站点](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)，了解此流程的工作方式以及一些需要注意的事项，以便充分发挥此流程的潜力。
* **Web层配置** — 配置Dispatcher属性，以存储、处理网页并将网页交付给客户端。
   * 有关更多详细信息，请参阅文档[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)。
   * 如果所选环境存在 Web 层代码管道，则会禁用此选择。
   * 如果将现有的全栈管道部署到环境中，则为同一环境创建 Web 层配置管道将忽略全栈管道中的现有 Web 层配置。

>[!NOTE]
>
>专用存储库不支持 Web 层和配置管道。有关详细信息和完整的限制列表，请参阅文档[在Cloud Manager中添加专用存储库](/help/implementing/cloud-manager/managing-code/private-repositories.md)。

选择部署类型后，完成创建生产目标部署管道的步骤相同。

1. 选择所需的部署类型。

![目标部署选项](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. 定义&#x200B;**符合条件的部署环境**。

   * 如果您的管道是部署管道，则必须选择它应该部署到哪些环境。

1. 在&#x200B;**Source代码**&#x200B;下，定义以下选项：

   * **存储库** – 此选项定义管道应从中检索代码的 Git 存储库。

   >[!TIP]
   > 
   >请参阅[添加和管理存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，了解如何在 Cloud Manager 中添加和管理存储库。

   * **Git 分支** – 此选项定义管道应从中检索代码的所选存储库的分支。
      * 输入分支名称的前几个字符，以及此字段的自动完成功能。它会找到您可以选择的匹配分支。
   * **代码位置** – 此选项定义管道应从中检索代码的所选存储库分支中的路径。
   * **部署到生产之前暂停** – 此选项在部署到生产之前暂停管道。
   * **已计划** — 此选项允许用户启用计划的生产部署。 仅适用于Web层目标部署。

   ![配置管道](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. 单击“**保存**”。

管道已保存，您现在可以在[程序概述](managing-pipelines.md)页面的&#x200B;**管道**&#x200B;信息卡上&#x200B;**管理您的管道**。

## 跳过 Dispatcher 程序包 {#skip-dispatcher-packages}

如果希望将 Dispatcher 程序包作为管道的一部分构建，但不希望将其发布来构建存储，则可以禁用发布它们，这可能会缩短管道运行持续时间。

必须通过项目 `pom.xml` 文件，添加以下禁用发布 Dispatcher 程序包的配置。该配置基于一个环境变量，作为一个标志，您可以在 Cloud Manager 构建容器中设置，定义何时应忽略 Dispatcher 程序包。

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
