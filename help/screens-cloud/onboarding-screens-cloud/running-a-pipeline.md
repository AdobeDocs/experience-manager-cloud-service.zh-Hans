---
title: 运行管道
description: 本页介绍如何在Cloud Manager中将Screens作为Cloud Service项目运行管道。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---


# 在Cloud Manager中运行屏幕作为Cloud Service程序的管道 {#run-pipeline-screens-cloud}

本节介绍如何在Cloud Manager中运行管道并为程序部署代码。

>[!NOTE]
>请参阅[配置CD-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en)和[部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) ，以了解如何在Cloud Manager中为程序运行管道。

## 目标 {#objective}

以下部分介绍如何在Cloud Manager中配置CI/CD管道并为程序部署代码。

## 在Cloud Manager中为Screens项目运行管道的步骤 {#steps-branch-creation}

1. 环境设置成功完成后，您将在Cloud Manager的&#x200B;**概述**&#x200B;页面中看到行动动员卡更新。

   ![图像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. 单击&#x200B;**概述**&#x200B;页面中的&#x200B;**设置管道**。

1. 选择分支后，单击&#x200B;**Next**。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. 从&#x200B;**设置管道**&#x200B;向导中选择您的选项。 单击&#x200B;**Save**。

   >[!NOTE]
   >要了解“设置管道”向导中的选项，请参阅[从Cloud Manager配置管道设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en)以获取更多详细信息。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 安装管道完成后，行动动员卡会更新，如下图所示。 单击部署。

   >[!NOTE]
   >要了解Cloud Manager中部署的阶段，请参阅[部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) ，以获取更多详细信息。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 单击&#x200B;**Build**&#x200B;以开始构建过程。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. 构建过程完成后，您将从Cloud Manager的&#x200B;**Overview**&#x200B;页面的&#x200B;**Environments**&#x200B;卡中看到创作链接。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 下一步 {#whats-next}

在Cloud Manager中了解如何为程序设置环境后，您现在可以继续进入载入过程的下一步，即[导航到Screens服务提供商](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md)。