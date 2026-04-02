---
title: 添加非生产管道
description: 了解如何添加非生产管道，以在部署到生产环境之前测试代码的质量。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 7663af90b17e4b9d9567041c3bed8e20465c87d9
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 21%

---


# 添加非生产管道 {#configuring-non-production-pipelines}

在Cloud Manager UI中设置项目并创建至少一个环境后，您可以添加非生产管道。 这些管道允许您在部署到生产环境之前测试代码质量。

用户必须具有&#x200B;**[部署管理员](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能配置非生产管道。

>[!NOTE]
>
>在初始设置后，您可以[编辑管道设置](managing-pipelines.md)。

## 添加新的非生产管道 {#adding-non-production-pipeline}

设置项目并在Cloud Manager UI中创建至少一个环境后，可添加非生产管道。 在部署到生产环境之前，使用这些管道测试代码质量。

**要添加新的非生产管道：**

1. 在 [experiece.adobe.com](https://experience.adobe.com) 登录 Cloud Manager。
1. 在&#x200B;**快速访问**&#x200B;部分，单击 **Experience Manager**。
1. 在左侧面板中点击 **Cloud Manager**。
1. 选择所需的组织。
1. 在&#x200B;**我的程序**&#x200B;控制台上，单击一个程序。
1. 在左侧面板中，单击&#x200B;**管道**。
1. 在&#x200B;**管道**&#x200B;页面的右上角附近，单击&#x200B;**添加管道** > **添加非生产管道**。

   ![添加非生产管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在&#x200B;**添加非生产管道**&#x200B;对话框的&#x200B;**配置**&#x200B;选项卡上，选择要创建的以下非生产管道之一：

   * **代码质量管道** — 创建管道，以便在GIT分支上生成代码、运行单元测试和评估代码质量，而无需部署到环境。
   * **部署管道** — 创建一个管道，用于生成代码、运行单元测试、评估代码质量并部署到非生产环境。

   ![“添加非生产管道”对话框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 在&#x200B;**管道配置**&#x200B;部分的&#x200B;**非生产管道名称**&#x200B;字段中，键入非生产管道的描述。
1. 在&#x200B;**部署选项**&#x200B;部分下，选择要使用的以下部署触发器之一：

   * **手动** - 您可以手动启动管道。
   * **在 Git 发生更改时** – 只要将承诺添加到配置的 Git 分支就会启动管道。 利用此选项，您仍能根据需要手动启动管道。

1. 选择要使用的&#x200B;**重要量度失败行为**。

   * **每次询问** – 此行为是默认设置，需要对任何重要失败进行手动干预。
   * **立即失败** – 如果选定此选项，则只要发生重要失败，就会取消管道。它实际上模拟用户手动拒绝每个失败。
   * **立即继续** – 如果选定此选项，则每当发生重要失败时，管道就会自动继续。它实际上模拟用户手动批准每个失败。

1. 单击&#x200B;**继续**。

1. 用于完成非生产管道配置的剩余步骤取决于您选择使用的源代码类型。
在**添加非生产管道**&#x200B;对话框的&#x200B;**Source代码**&#x200B;选项卡上，选择非生产管道应处理的代码类型。

   * **[我正在使用全栈代码](#full-stack-code)**
   * **[我正在使用目标部署](#targeted-deployment)**

   有关管道类型的更多信息，请参阅[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。


### 我正在使用全栈代码 {#full-stack-code}

全栈代码管道同时部署后端和前端代码构建，其中包含一个或多个AEM服务器应用程序以及HTTPD/Dispatcher配置。

>[!NOTE]
>
>如果所选环境存在全栈代码管道，则会禁用此选择。

要完成全栈代码非生产管道的配置，请执行以下操作：

1. 在&#x200B;**Source代码**&#x200B;部分中，定义以下选项。

   * **符合条件的部署环境** — 仅在编辑非生产管道时可用。 如果您的管道是部署管道，则必须选择它应该部署到哪些环境。
   * **存储库** — 从下拉列表中选择管道用作其源的Git存储库。 Cloud Manager从您在此处选择的存储库中生成代码。

     >[!TIP]
     > 
     >请参阅[添加和管理存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，了解如何在 Cloud Manager 中添加和管理存储库。

   * **Git分支** — 从下拉列表中，选择管道应从中构建到的所选存储库中的哪个分支。 默认为 `main`。 管道使用所选分支作为构建和部署的源。 如有必要，请单击&#x200B;**刷新**&#x200B;以更新所选存储库的可用分支列表。 如果最近创建的分支未出现在列表中，请使用此选项。
   * **生成策略**
      * **完整生成** — 每次生成存储库中的所有模块
      * Beta **智能生成** — 仅生成自上次提交以来更改的模块。<br>了解有关[在非生产管道中使用Smart Build](#about-smart-build-non-production-pipeline)的更多信息。

        >[!IMPORTANT]
        >
        >智能生成仅适用于代码质量管道和开发全栈代码部署管道。

   * **忽略Web层配置**&#x200B;复选框 — 选中后，管道不会部署您的Web层配置。

1. 在&#x200B;**管道**&#x200B;部分中，如果您的管道是部署管道，则可以选择运行测试阶段。 检查要在此阶段启用的选项。如果没有选择任何选项，则管道运行期间将不会显示测试阶段。

   * **产品功能测试** — 针对开发环境运行[产品功能测试](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)。
   * **自定义功能测试** — 针对开发环境运行[自定义功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)。
   * **自定义UI测试** — 为自定义应用程序运行[自定义UI测试](/help/implementing/cloud-manager/ui-testing.md)。
   * **体验审核** — 运行[体验审核](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![全栈管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 单击“**保存**”。

管道已保存，您现在可以[管理您的管道]&#x200B;(managing-pipe
lines.md)，它位于**项目概述**&#x200B;页面的&#x200B;**管道**&#x200B;卡上。

### 我正在使用目标部署 {#targeted-deployment}

目标部署仅会为AEM应用程序的选定部分部署代码。 在此类部署中，您可以选择&#x200B;**包含**&#x200B;以下代码类型之一：

![目标部署选项](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment1.png)

<!--
* **Config** - Configure settings for various features in your AEM environment.
  * See [Using Config Pipelines](/help/operations/config-pipeline.md) for a list of supported configurations, which include log forwarding, purge-related maintenance tasks, and various CDN configurations, and to manage them in your repository so they are deployed properly.
  * When running a targeted deployment pipeline, configurations are deployed, provided they are saved to the environment, repository, and branch you defined in the pipeline.
  * At any time, there can only be one config pipeline per environment.
* **Configure Edge Delivery Services config pipeline** - Edge Delivery Configuration Pipelines do not have separate development, staging, and production environments. In AEM as a Cloud Service, changes move through development, stage, and production tiers. In contrast, an Edge Delivery Configuration Pipeline applies its configuration directly to all Edge Delivery Sites domains registered in Cloud Manager. To learn more, see [Add an Edge Delivery Pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
-->


* **前端代码** — 为AEM应用程序的前端配置JavaScript和CSS。
   * 有了前端管道，前端开发人员可以获得更多的独立性，可加快开发过程。
   * 请参阅文档[使用前端管道开发站点](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)，了解此流程的工作方式以及一些需要注意的事项，以便充分发挥此流程的潜力。
* **Web层配置** — 配置Dispatcher属性，以存储、处理网页并将网页交付给客户端。
   * 有关更多详细信息，请参阅文档[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)。
   * 如果所选环境存在 Web 层代码管道，则会禁用此选择。
   * 如果全栈管道已部署到环境，您仍然可以为该同一环境创建Web层配置管道。 执行此操作时，Cloud Manager会忽略全栈管道中的Web层配置。

     >[!NOTE]
     >
     >专用存储库不支持 Web 层和配置管道。有关详细信息和完整的限制列表，请参阅[在Cloud Manager中添加专用存储库](/help/implementing/cloud-manager/managing-code/private-repositories.md)。

<!--
The steps to complete the creation of your non-production, targeted deployment pipeline are the same once you choose a deployment type.

1. Choose which deployment type you require.

![Targeted deployment options](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. Define the **Eligible Deployment Environments**.

   * If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
-->

1. 在&#x200B;**Source代码**&#x200B;部分下，定义以下选项：

   * **存储库** — 此选项定义非生产管道应从中检索代码的GIT存储库。

     >[!TIP]
     > 
     >请参阅[添加和管理存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)，了解如何在 Cloud Manager 中添加和管理存储库。

   * **Git分支** — 此选项定义所选管道中应从中检索代码的分支。 输入分支名称的前几个字符，以及此字段的自动完成功能。它会找到您可以选择的匹配分支。
   * **代码位置** – 此选项定义管道应从中检索代码的所选存储库分支中的路径。

<!--
   * **Pipeline** - For front-end non-production pipelines, you have the option to enable **[Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)**.
   
   ![Config pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)
-->

1. 如果启用了体验审核，请单击&#x200B;**继续**&#x200B;前进到&#x200B;**体验审核**&#x200B;选项卡，您可以在其中定义应始终包含在体验审核中的路径。

   * 如果您启用了&#x200B;**体验审核**，请参阅[体验审核](/help/implementing/cloud-manager/reports/report-experience-audit.md)文档，以了解有关如何配置的详细信息。
   * 如果未配置，请跳过此步骤。

1. 单击&#x200B;**保存**，以保存管道。

管道已保存，您现在可以在[程序概述](managing-pipelines.md)页面的&#x200B;**管道**&#x200B;信息卡上&#x200B;**管理您的管道**。


## 关于在非生产管道中使用Smart Build{#about-smart-build-non-production-pipeline}

Cloud Manager中的&#x200B;**智能生成**&#x200B;是适用于非生产管道的优化生成策略。 Smart Build通过缓存模块并仅重新生成自上次成功运行以来发生更改的模块来缩短构建时间。 未更改的模块从缓存中重用，而只重新构建已修改的模块及其依赖关系，从而提高迭代开发工作流的效率。

Smart Build当前仅适用于以下项目：

* 代码质量管道。
* 开发全栈部署管道。

>[!NOTE]
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
* 您可以通过编辑非生产管道随时切换回&#x200B;**完整内部版本**。

如果遇到意外的生成行为，请考虑禁用特定模块的缓存或暂时将生成策略切换到&#x200B;**完整生成**。

### 智能生成问题疑难解答{#smart-build-troubleshoot}

| 问题 | 建议的解决方案 |
| --- | --- |
| 生成结果不一致 | ·禁用受影响模块的缓存。<br>·验证插件的行为（尤其是`exec`/`antrun`插件）。 |
| 无性能改进 | ·确保已多次运行（缓存预热）。<br>·检查大多数模块是否频繁更改。 |
| 意外的项目或缺少更改 | ·查看更改是否在Maven依赖项跟踪之外。<br>·使用&#x200B;**Full Build**&#x200B;进行验证。 |

请参阅[添加非生产管道](#adding-non-production-pipeline)以启用智能生成。











<!--
## Add a non-production pipeline {#adding-non-production-pipeline}

Once you have set up your program and have at least one environment using the Cloud Manager UI, you are ready to add a non-production pipeline by following these steps.

1. Sign into Cloud Manager at [experiece.adobe.com](https://experience.adobe.com).
1. In the **Quick access** section, click **Experience Manager**.
1. In the left side panel, click **Cloud Manager**.
1. Select an organization that you want.
1. On the **My Programs** console, click a program. 

1. Access the **Pipelines** card from the Cloud Manager home screen. Click **+Add** and select **Add Non-Production Pipeline**. 

   ![Add non-production pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. On the **Configuration** tab of the **Add Non-Production Pipeline** dialog, select the type of non-production pipeline you with to add.

   * **Code Quality Pipeline** - Create a pipeline that builds your code, runs unit tests, and evaluates code quality but does NOT deploy.
   * **Deployment Pipeline** - Create a pipeline that builds your code, runs unit tests, evaluates code quality, and deploys to an environment.

   ![Add Non-Production pipeline dialog](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Provide a **Non-Production Pipeline Name** to identify your pipeline along with the following additional information.

   * **Deployment Trigger** - You have the following options when defining the deployment triggers to start the pipeline.
   
     * **Manual** - Use this option to start the pipeline manually.
     * **On Git Changes** - This option starts the CI/CD pipeline whenever commits are added to the configured Git branch. With this option, you can still start the pipeline manually as required.

1. If you choose to create a **Deployment Pipeline**, you must also define the **Important Metric Failures Behavior**.

   * **Ask every time** - This behavior is the default setting and requires manual intervention on any important failure.
   * **Fail Immediately** - If selected, the pipeline is canceled whenever an important failure occurs. It is essentially emulating a user manually rejecting each failure.
   * **Continue Immediately** - If selected, the pipeline procedes automatically whenever an important failure occurs. It is essentially emulating a user manually approving each failure.

1. Click **Continue**.

1. On the **Source Code** tab of the **Add Non-Production Pipeline** dialog, you must select which type of code the pipeline should process.

   * **[Full Stack Code](#full-stack-code)**
   * **[Targeted deployment](#targeted-deployment)**

See [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) for more information about the types of pipelines.

The steps to complete the creation of your non-production pipeline vary depending on the type of source code you selected. Follow the links above to jump to the next section of this document so you can complete the configuration of your pipeline.

### Full Stack Code {#full-stack-code}

A full-stack code pipeline simultaneously deploys back-end and front-end code builds containing one or more AEM server applications along with HTTPD/Dispatcher configuration.

>[!NOTE]
>
>If a full-stack code pipeline exists for the selected environment, this selection is disabled.

To finish the configuration of the full-stack code non-production pipeline, follow these steps.

1. On the **Source Code** tab, you must define the following options.

   * **Eligible Deployment Environments** - If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
   * **Repository** - This option defines from which git repo that the pipeline should retrieve the code.

   >[!TIP]
   > 
   >See [Adding and Managing Repositories](/help/implementing/cloud-manager/managing-code/managing-repositories.md) so you can learn how to add and manage repositories in Cloud Manager.

   * **Git Branch** - This option defines from which branch in the selected pipeline should retrieve the code.
     * Enter the first few characters of the branch name and the auto-complete feature of this field. It helps you find the matching branches that you can select.
   * **Ignore Web Tier Configuration** - When checked, the pipeline does not deploy your web tier configuration.
   * **Pipeline** - If your pipeline is a deployment pipeline, you can choose to run a testing phase. Check the options that you want to enable in this phase. If none of the options are selected, the testing phase is not displayed during the pipeline's run.

     * **Product Functional Testing** - Execute [product functional tests](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) against the development environment.
     * **Custom Functional Testing** - Execute [custom functional tests](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) against the development environment.
     * **Custom UI Testing** - Execute [custom UI tests](/help/implementing/cloud-manager/ui-testing.md) for custom applications.
     * **Experience Audit** - Execute [Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Full-stack pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Click **Save**.

The pipeline is saved and you can now [manage your pipelines](managing-pipelines.md) on the **Pipelines** card on the **Program Overview** page.

-->



## 排除Dispatcher包 {#exclude-dispatcher-packages}

如果您希望在管道中构建Dispatcher包，但未将其上传以构建存储，请禁用发布。 这样做可以缩短管道的运行时间。

将以下配置添加到项目`pom.xml`文件以禁用发布Dispatcher包。 在Cloud Manager构建容器中设置一个环境变量，以标记何时忽略Dispatcher包。 管道读取此标记并相应地忽略它们。

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
