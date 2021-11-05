---
title: 配置非生产管道
description: 可查看本页以了解有关在Cloud Manager中配置非生产管道的信息
index: true
source-git-commit: 2ac65af4cf410491d1196b9e20f67647e0a1b4d1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# 配置非生产管道 {#configure-non-production-pipeline}

除了部署到暂存和生产的主管道之外，客户还能够设置其他管道，称为非生产管道。

非生产管道有两种类型：

1. 代码质量：在git分支中的代码上运行代码质量扫描。 此管道可执行生成和代码质量步骤。
1. 部署：除了执行构建和代码质量步骤之外，此管道还会将代码部署到选定的非生产环境到AEMas a Cloud Service环境。

## 添加新的非生产管道 {#adding-non-production-pipeline}

在主屏幕上，这些管道将列在新卡中：

1. 访问 **管道** Cloud Manager主屏幕中的信息卡。 单击 **+添加** 选择 **添加非生产管道**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **添加非生产管道**  对话框。 选择要创建的管道类型 **代码质量管道** 或 **部署管道**.

   >[!NOTE]
   >对于部署管道，必须选择部署环境。

   此外，您还可以设置 **部署触发器** 和 **重要量度失败行为** 从 **部署选项**. 单击 **继续**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

   您可以定义以下部署触发器以启动管道。

   * **手动**  — 使用UI手动启动管道。
   * **在Git更改时**  — 每当向配置的git分支添加提交时，都会启动CI/CD管道。 即使选择此选项，也始终可以手动启动管道。

      在管道设置或编辑期间，部署管理器可以选择在任何质量门中遇到重要故障时定义管道的行为。

      这对于希望实现更自动化流程的客户非常有用。 可用选项包括：
   您可以定义重要的失败量度行为以启动管道。

   * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
   * **立即失败**  — 如果选中，则每当发生重要故障时，将取消管道。 这实质上是在模拟用户手动拒绝每个故障。
   * **立即继续**  — 如果选中，则每当发生重要故障时，管道将自动继续。 这实质上是在模拟用户手动批准每次失败。


1. 选择 **[完整堆栈代码](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** 或 **[前端代码](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**.

   如果已选择 **前端代码**，则必须选择 **存储库**, **Git分支** 和 **代码位置**，如下图所示：

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-confignew1.png)

   如果已选择 **完整堆栈代码**，则必须选择 **存储库** 和 **Git分支**，如图所示：
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack1.png)

   >[!IMPORTANT]
   >如果所选环境已存在完整堆栈代码管道，则将禁用此选择。

   >[!NOTE]
   >在开始配置前端管线之前，请参阅 [AEM快速网站创建历程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) 通过易于使用的AEM快速站点创建工具实现端到端工作流。 此文档网站将帮助您简化AEM网站的前端开发，并在不了解AEM后端知识的情况下快速自定义您的网站。

1. 现在，新创建的非生产管道将显示在 **管道** 卡。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack2.png)


   管道显示在主屏幕的卡片上，带有四个操作，如下所示：

   * **添加**  — 允许添加新管道。
   * **显示全部**  — 允许用户查看所有管道。
   * **访问存储库信息**  — 允许用户获取访问Cloud Manager Git存储库所需的信息。
   * **了解更多**  — 导航到了解CI/CD管道文档资源。