---
title: 配置生产管道
description: 配置生产管道
index: true
source-git-commit: f25e26c84a87cf793f9c8a5ac53009034e6cd2e9
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# 配置生产管道 {#configure-production-pipeline}

部署管理器负责配置生产管道。

>[!NOTE]
>在程序创建完成、Git存储库至少具有一个分支，并且创建了生产和暂存环境集之前，无法设置生产管道。

在开始部署代码之前，必须先从 [!UICONTROL Cloud Manager].

>[!NOTE]
>在初始设置后，可以更改管道设置。

## 添加新的生产管道 {#adding-production-pipeline}

设置程序并使用 [!UICONTROL Cloud Manager] UI，您就可以添加生产管道。

请按照以下步骤配置生产管道的行为和首选项：

1. 导航到 **管道** 卡 **计划概述** 页面。
单击 **+添加** 选择 **添加生产管道**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **添加生产管道** 对话框。 输入管道名称。

   此外，您还可以设置 **部署触发器** 和 **重要量度失败行为** 从 **部署选项**. 单击 **继续**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   您可以定义部署触发器以启动管道。

   * **手动**  — 使用UI手动启动管道。
   * **在Git更改时**  — 每当向配置的git分支添加提交时，都会启动CI/CD管道。 即使选择此选项，也始终可以手动启动管道。

      在管道设置或编辑期间，部署管理器可以选择在任何质量门中遇到重要故障时定义管道的行为。

      这对于希望实现更自动化流程的客户非常有用。 可用选项包括：
   您可以定义重要的失败量度行为以启动管道。

   * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
   * **立即失败**  — 如果选中，则每当发生重要故障时，将取消管道。 这实质上是在模拟用户手动拒绝每个故障。
   * **立即继续**  — 如果选中，则每当发生重要故障时，管道将自动继续。 这实质上是在模拟用户手动批准每次失败。


1. 的 **添加生产管道** 对话框包括标记为 **源代码**. 您可以选择 **[完整堆栈代码](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** 或 **[前端代码](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**. 您可以选择 **存储库** 和 **Git分支**. 选择生产部署选项，如下所述。 单击 **继续**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack1.png)

   如果已选择 **前端代码**，则必须选择 **存储库**, **Git分支** 和 **代码位置**，如下图所示：
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack1.png)

   如果已选择 **完整堆栈代码**，则必须选择 **存储库**, **Git分支** 和 **生产部署选项**，如下图所示：
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack2.png)

   **生产部署选项：**

   * **部署到生产之前暂停**:此选项允许部署在生产之前暂停。
   * **已计划**:此选项允许用户启用计划的生产部署。

   >[!IMPORTANT]
   >如果所选环境已存在完整堆栈代码管道，则将禁用此选择。
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/full-stack-disabled.png)

   >[!NOTE]
   >在开始配置前端管线之前，请参阅 [AEM快速网站创建历程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) 通过易于使用的AEM快速站点创建工具实现端到端工作流。 此文档网站将帮助您简化AEM网站的前端开发，并在不了解AEM后端知识的情况下快速自定义您的网站。





1. 的 **添加生产管道** 对话框包含第三个标签为 **体验审核**. 此选项为应始终包含在体验审核中的URL路径提供了一个表。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >您必须单击 **添加页面** 定义您自己的自定义链接。 页面路径必须以开头 `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   单击 **添加新页面** 提供要包含在体验审核中的URL路径。

   例如，如果您希望包含 `https://wknd.site/us/en/about-us.html` 在体验审核中，输入路径 `/us/en/about-us.html` 单击 **保存**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   表中显示的URL将为：

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   最多可包含25行。 如果用户在此部分中未提交页面，则默认情况下网站的主页将包含在体验审核中。

   请参阅 [了解体验审核结果](/help/implementing/cloud-manager/experience-audit-testing.md) 以了解更多详细信息。

   >[!NOTE]
   > 将配置的页面提交到服务，并根据性能、辅助功能、SEO（搜索引擎优化）、最佳实践和PWA（渐进式Web应用程序）测试进行评估。

1. 单击 **保存**. 现在，新创建的生产管道将显示在 **管道** 卡。

   管道显示在主屏幕的卡片上，带有三个操作，如下所示：

   * **添加**  — 允许添加新管道。
   * **访问存储库信息**  — 允许用户获取访问Cloud Manager Git存储库所需的信息。
   * **了解更多**  — 导航到了解CI/CD管道文档资源。


