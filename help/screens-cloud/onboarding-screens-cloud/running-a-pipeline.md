---
title: 运行管道
description: 本页介绍如何在Cloud Manager中将Screens作为Cloud Service项目运行管道。
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 8%

---

# 在Cloud Manager中运行屏幕as a Cloud Service程序管道 {#run-pipeline-screens-cloud}

本节介绍如何在Cloud Manager中运行管道并为程序部署代码。

>[!NOTE]
>请参阅 [配置CD-CD管线](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) 和 [部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) 了解如何在Cloud Manager中为程序运行管道。

## 目标 {#objective}

以下部分介绍如何在Cloud Manager中配置CI/CD管道并为程序部署代码。

## 在Cloud Manager中为Screens项目运行管道的步骤 {#steps-branch-creation}

1. 环境设置成功完成后，您将在Cloud Manager的 **概述** 页面。

   ![图像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. 单击 **设置管道** 从 **概述** 页面。

1. 单击 **下一个** 选择分支后。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. 从 **设置管道** 向导。 单击 **保存**.

   >[!NOTE]
   >要了解“设置管道”向导中的选项，请参阅 [从Cloud Manager配置管道设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) 以了解更多详细信息。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 安装管道完成后，行动动员卡会更新，如下图所示。 单击部署。

   >[!NOTE]
   >要了解Cloud Manager中的部署阶段，请参阅 [部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) 以了解更多详细信息。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 单击 **生成** 以启动构建过程。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. 构建过程完成后，您将在 **环境** Cloud Manager的卡片 **概述** 页面。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 下一步 {#whats-next}

在Cloud Manager中了解如何为程序设置环境后，您现在可以继续执行载入流程中的下一步，即， [导航到Screens服务提供商](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
