---
title: 添加生产管道
description: 了解如何添加生产管道以生成代码并将其部署到生产环境。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: aa8aba7f798e251c8a25ee247402e23517707e88
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 27%

---


# 添加生产管道 {#configure-production-pipeline}

了解如何配置生产管道以生成代码并将其部署到生产环境。 生产管道首先将代码部署到暂存环境。 在获得批准后，它会将相同的代码部署到生产环境。

用户必须具有&#x200B;**[部署管理员](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能配置生产管道。

>[!NOTE]
>
>在发生以下情况之前，无法设置生产管道：
>
>* 项目随即会创建。
>* Git存储库至少有一个分支。
>* 将创建生产和暂存环境。

在开始部署代码之前，请从[!UICONTROL Cloud Manager]配置管道设置。

>[!NOTE]
>
>在初始设置后，您可以[编辑管道设置](managing-pipelines.md)。

## 添加新的生产管道 {#adding-production-pipeline}

在设置项目并具有至少一个使用[!UICONTROL Cloud Manager] UI的环境后，便可以执行以下步骤来添加生产管道。

>[!TIP]
>
>在配置前端管道之前，请参阅[AEM快速站点创建历程](/help/journey-sites/quick-site/overview.md)，获取易于使用的AEM快速站点创建工具的端到端指南。 此历程可帮助您简化AEM站点的前端开发，让您无需了解AEM后端即可快速自定义站点。

1. 在[experience.adobe.com](https://experience.adobe.com)登录Cloud Manager。
1. 在&#x200B;**快速访问**&#x200B;部分，单击 **Experience Manager**。
1. 在左侧面板中点击 **Cloud Manager**。
1. 选择所需的组织。
1. 在&#x200B;**我的程序**&#x200B;控制台上，单击一个程序。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;卡并单击&#x200B;**添加**&#x200B;以选择&#x200B;**添加生产管道**。

   ![在“程序管理员”概述中的“管道”信息卡](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. 此时会显示&#x200B;**添加生产管道**&#x200B;对话框。提供&#x200B;**管道名称**，识别您的管道以及以下选项。单击&#x200B;**“继续”**。

   **部署触发器** – 在定义启动管道的部署触发器时，您可以使用以下选项。

   * **手动** — 手动启动管道。
   * **在Git发生更改时** — 只要将承诺添加到配置的Git分支，就会启动CI/CD管道。 利用此选项，您仍能根据需要手动启动管道。

   **重要量度失败行为r** – 在管道设置或编辑期间，**部署管理员**&#x200B;可以选择定义在任何质量审核出现重要失败时的管道行为。可用的选项为：

   * **每次询问** — 默认设置。 它要求对任何重要失败进行手动干预。
   * **立即失败** – 如果选定此选项，则只要发生重要失败，就会取消管道。此过程实际上是在模拟用户手动拒绝每个失败的情况。
   * **立即继续** — 如果选定此选项，则每当发生重要失败时，管道就会自动继续。 此过程实际上是在模拟用户手动批准每个失败的情况。

   ![生产管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 在&#x200B;**Source代码**&#x200B;选项卡上，选择管道应处理的代码类型。

   * **[我正在使用全栈代码](#full-stack-code)**
   * **[配置目标部署管道](#targeted-deployment)**

有关管道类型的更多信息，请参阅[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

根据您选择的源代码类型，完成生产管道创建的步骤有所不同。 按照上面的链接跳到本文档的下一节，完成管道的配置。

### 我使用的是全栈代码 {#full-stack-code}

全栈代码管道同时部署后端和前端代码构建，其中包含一个或多个AEM服务器应用程序以及HTTPD/Dispatcher配置。

>[!NOTE]
>
>如果所选环境已存在全栈代码管道，则会禁用此选择。

**要配置全栈栈代码管道：**

1. 在&#x200B;**Source代码**&#x200B;选项卡上，定义以下选项。

   * **存储库** — 定义管道应从中检索代码的Git存储库。

   >[!TIP]
   > 
   >请参阅[添加和管理存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支** — 从下拉列表中，选择管道应从中构建到的所选存储库中的哪个分支。 默认为 `main`。 管道使用所选分支作为构建和部署的源。 如有必要，请单击&#x200B;**刷新**&#x200B;以更新所选存储库的可用分支列表。 如果最近创建的分支未出现在列表中，请使用此选项。
   * **生成策略**
      * **完整生成** — 每次生成存储库中的所有模块
      * Beta **智能生成** — 仅生成自上次提交以来更改的模块。<br>了解有关[在非生产管道中使用Smart Build](#about-smart-build-non-production-pipeline)的更多信息。

        >[!IMPORTANT]
        >
        >智能生成仅适用于代码质量管道和开发全栈代码部署管道。
   * **忽略 Web 层配置** – 勾选后，该管道不会部署您的 Web 层配置。
   * **在部署到生产之前暂停** — 在部署到生产之前暂停管道。
   * **已计划** — 允许用户启用计划的生产部署。

   ![全栈代码](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 单击&#x200B;**继续**&#x200B;前进到&#x200B;**体验审核**&#x200B;选项卡，您可以在其中定义应始终包含在体验审核中的路径。

   ![添加体验审核](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. 提供要包含在体验审核中的路径。

   * 有关详细信息，请参阅[体验审核测试](/help/implementing/cloud-manager/reports/report-experience-audit.md#configuration)。

1. 单击&#x200B;**保存**&#x200B;以保存管道。

在管道运行时，会提交为体验审核配置的路径，并根据性能、可访问性、SEO、最佳实践和PWA测试进行评估。 有关详细信息，请参阅[了解体验审核结果](/help/implementing/cloud-manager/reports/report-experience-audit.md)。

管道已保存，您现在可以在[程序概述](managing-pipelines.md)页面的&#x200B;**管道**&#x200B;信息卡上&#x200B;**管理您的管道**。

### 我正在使用目标部署 {#targeted-deployment}

目标部署仅会为AEM应用程序的选定部分部署代码。 在此类部署中，您可以选择&#x200B;**包含**&#x200B;以下代码类型之一：

* **配置** — 为AEM环境中的各种功能配置设置。
   * 有关支持的配置（包括日志转发、清除相关的维护任务和各种CDN配置）的列表，请参阅[使用配置管道](/help/operations/config-pipeline.md)，并在存储库中管理这些配置以便正确部署它们。
   * 运行目标部署管道时，将部署配置，前提是这些配置已保存到管道中定义的环境、存储库和分支。
   * 在任何时候，每个环境只能有一个配置管道。
* **配置Edge Delivery Services配置管道** - Edge Delivery配置管道没有单独的开发、暂存和生产环境。 在AEM as a Cloud Service中，更改在开发、暂存和生产层之间移动。 相反，Edge Delivery配置管道会将其配置直接应用于在Cloud Manager中注册的所有Edge Delivery Sites域。 要了解更多信息，请参阅[添加Edge Delivery管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)。
* **前端代码** — 为AEM应用程序的前端配置JavaScript和CSS。
   * 有了前端管道，前端开发人员可以获得更多的独立性，可加快开发过程。
   * 请参阅文档[使用前端管道开发站点](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)，了解此流程的工作方式以及一些需要注意的事项，以便充分发挥此流程的潜力。
* **Web层配置** — 配置Dispatcher属性，以存储、处理网页并将网页交付给客户端。
   * 有关更多详细信息，请参阅文档[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)。
   * 如果所选环境存在 Web 层代码管道，则会禁用此选择。
   * 如果您为具有现有全栈管道的环境创建Web层配置管道，则忽略全栈管道中的Web层配置。 此更改仅影响该环境中的Web层配置。

>[!NOTE]
>
>专用存储库不支持 Web 层和配置管道。有关详细信息和完整的限制列表，请参阅[在Cloud Manager中添加专用存储库](/help/implementing/cloud-manager/managing-code/private-repositories.md)。

**要配置目标部署管道：**

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
   * **已计划** — 允许用户启用计划的生产部署。 仅适用于Web层目标部署。

   ![配置管道](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. 单击“**保存**”。

管道已保存，您现在可以在[程序概述](managing-pipelines.md)页面的&#x200B;**管道**&#x200B;信息卡上&#x200B;**管理您的管道**。

## Beta：关于在生产管道中使用Smart Build{#about-smart-build-production-pipeline}

Cloud Manager中的&#x200B;**智能生成**&#x200B;是生产管道的优化生成策略。 Smart Build通过缓存模块并仅重新生成自上次成功运行以来发生更改的模块来缩短构建时间。 未更改的模块从缓存中重用，而只重新构建已修改的模块及其依赖关系，从而提高迭代开发工作流的效率。

>[!NOTE]
>
>对这个测试版感兴趣吗？ 向 [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) 发送电子邮件，其中包含您的 Adobe OrgID 和项目群 ID。

>[!IMPORTANT]
>
>启用Smart Build后首次运行的行为类似于Full Build，因为缓存为空。

在出现以下情况时，建议使用Smart Build：

* 您正在积极开发和提交频繁的增量更改。
* 您的项目包含多个Maven模块。
* 完整内部版本需要大量时间。

当出现以下情况时，Smart Build并不总是理想的：

* 您的内部版本严重依赖在Maven的依赖关系图之外执行操作的插件。
* 每次执行都需要完全重新生成验证。

### 了解构建性能{#smart-build-performance}

使用Smart Build的性能提升取决于以下几个因素：

* 项目中的模块数。
* 代码更改的频率和范围。
* 依赖项在各个模块之间的分布。

通常，具有多个独立模块的项目可以看到最大的改进。

### 每模块缓存选择退出{#smart-build-cache-optout}

Smart Build提供细粒度控制，允许您禁用特定模块的缓存。 此功能在以下情况下很有用：

* 使用插件，如`exec-maven-plugin`或`maven-antrun-plugin`。
* 执行Maven依赖项未跟踪的文件操作。
* 缓存的内容产生不一致的结果。

### 禁用模块的缓存{#smart-build-disable-caching}

您可以将以下属性添加到受影响模块的`pom.xml`：

```xml
<properties>
  <maven.build.cache.enabled>false</maven.build.cache.enabled>
</properties>
```

此语法强制模块在每次管道执行时重新生成，而其他模块继续受益于缓存。

### 使用智能构建时的限制和注意事项{#smart-build-limitations}

使用Smart Build时，请牢记以下几点：

* Smart Build依赖于Maven依赖关系分析。
* 在依赖关系图之外进行的更改可能不会触发重新生成。
* 某些插件可能与缓存不完全兼容。
* 您可以通过编辑生产管道随时切换回&#x200B;**完整内部版本**。

如果遇到意外的生成行为，请考虑禁用特定模块的缓存或暂时将生成策略切换到&#x200B;**完整生成**。

### 智能生成问题疑难解答{#smart-build-troubleshoot}

| 问题 | 建议的解决方案 |
| --- | --- |
| 生成结果不一致 | ·禁用受影响模块的缓存。<br>·验证插件的行为（尤其是`exec`/`antrun`插件）。 |
| 无性能改进 | ·确保已多次运行（缓存预热）。<br>·检查大多数模块是否频繁更改。 |
| 意外的项目或缺少更改 | ·查看更改是否在Maven依赖项跟踪之外。<br>·使用&#x200B;**Full Build**&#x200B;进行验证。 |

请参阅[添加生产管道](#adding-production-pipeline)以启用智能生成。

## 跳过Dispatcher包 {#skip-dispatcher-packages}

要在管道中构建Dispatcher包，而不发布它们以构建存储，您可以禁用发布选项。 这样做有助于缩短管道的运行时间。

必须通过项目 `pom.xml` 文件，添加以下禁用发布 Dispatcher 程序包的配置。 环境变量用作您在Cloud Manager构建容器中设置的标记，以确定何时忽略Dispatcher包。

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>[!NOTE]rue</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
