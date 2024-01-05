---
title: 运行管道
description: 本页介绍如何在Cloud Manager中将Screens管道作为Cloud Service项目运行。
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# 在Cloud Manager中运行Screensas a Cloud Service程序管道 {#run-pipeline-screens-cloud}

本节介绍如何在Cloud Manager中运行管道并为程序部署代码。

>[!NOTE]
>请参阅 [配置CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html) 和 [部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html) 以了解如何在Cloud Manager中为您的项目运行管道。

## 目标 {#objective}

以下部分介绍了如何在Cloud Manager中配置CI/CD管道并为项目部署代码。

## 在Cloud Manager中为屏幕项目运行管道的步骤 {#steps-branch-creation}

1. 环境设置成功完成后，您将在Cloud Manager的 **概述** 页面。

   ![图像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. 单击 **设置管道** 从 **概述** 页面。

1. 单击 **下一个** 选择分支后。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. 从中选择您的选项 **设置管道** 向导。 单击&#x200B;**保存**。

   >[!NOTE]
   >要了解设置管道向导中的选项，请参阅 [从Cloud Manager配置管道设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html) 以了解更多详细信息。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 设置管道完成后，会更新行动号召信息卡。

   >[!NOTE]
   >要了解Cloud Manager中的部署阶段，请参阅 [部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html) 以了解更多详细信息。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 单击 **部署**.

1. 单击 **生成** 以开始构建过程。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. 构建过程完成后，您可以从 **环境** 来自Cloud Manager的信息卡 **概述** 页面。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 后续内容 {#whats-next}

了解如何在Cloud Manager中为项目设置环境后，便可以继续载入流程的下一步了： [导航到Screens Services Provider](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
