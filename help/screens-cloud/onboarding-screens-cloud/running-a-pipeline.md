---
title: 运行管道
description: 本页介绍如何在Cloud Manager中将Screens的管道作为Cloud Service项目运行。
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# 在Cloud Manager中运行Screensas a Cloud Service项目的管道 {#run-pipeline-screens-cloud}

本节介绍如何在Cloud Manager中运行管道并为项目部署代码。

>[!NOTE]
>请参阅[配置CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html)和[部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)，了解如何在Cloud Manager中为程序运行该管道。

## 目标 {#objective}

以下部分介绍了如何在Cloud Manager中配置CI/CD管道并为项目部署代码。

## 在Cloud Manager中为Screens项目运行管道的步骤 {#steps-branch-creation}

1. 环境设置成功完成后，您将在Cloud Manager的&#x200B;**概述**&#x200B;页面中看到行动号召信息卡更新。

   ![图像](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. 从&#x200B;**概述**&#x200B;页面单击&#x200B;**设置管道**。

1. 选择分支后，单击&#x200B;**下一步**。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. 从&#x200B;**设置管道**&#x200B;向导中选择选项。 单击&#x200B;**保存**。

   >[!NOTE]
   >要了解“设置管道”向导中的选项，请参阅[从Cloud Manager配置管道设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html)以了解更多详细信息。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. 设置管道完成后，会更新行动号召信息卡。

   >[!NOTE]
   >要了解Cloud Manager中的部署阶段，请参阅[部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)以了解更多详细信息。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. 单击&#x200B;**部署**。

1. 单击&#x200B;**生成**&#x200B;开始生成过程。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. 生成过程完成后，您可以在Cloud Manager的&#x200B;**概述**&#x200B;页面的&#x200B;**环境**&#x200B;信息卡中看到创作链接。

   ![图像](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## 后续内容 {#whats-next}

了解如何在Cloud Manager中为项目设置环境后，您便可以开始新用户引导过程中的下一步：[导航到Screens Services Provider](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md)。
