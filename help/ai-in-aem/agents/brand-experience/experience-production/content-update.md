---
title: 内容更新作业
description: 了解Brand Experience Agent的内容更新作业及其可为您执行的操作。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: baf12e49dadc7b25f5169279a52d5712380445de
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 2%

---


# 内容更新作业 {#content-update}

[Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md)的内容更新作业可自动执行内容生产，以加速Adobe Experience Manager (AEM) as a Cloud Service和Edge Delivery Services的日常任务。

## 概述 {#overview}

内容更新作业可更新现有内容，包括内容片段、页面、表单和资产。 该作业可以执行更新、删除、替换或添加内容元素等操作，以保持体验准确且最新。 输入可以是自然语言描述，在与Jira PDF一起使用时，屏幕截图也可以提供输入。

内容更新作业将您通过自然语言或可视化图表提供的详细信息转换为页面上的内容更新。 您可以提供需要更新的页面的URL，以及需要更新的内容的详细信息，座席技能将完成您的任务。 与Adobe Experience Manager (AEM) as a Cloud Service一起使用时，该作业会创建一个新的[启动项](/help/sites-cloud/authoring/launches/overview.md)，以便您可以在应用之前查看更新。 当与文档创作一起使用时，作业将创建新的[版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/sites/document-authoring/how-to/document-versions#)。

## 功能 {#capabilities}

您可以从以下位置访问内容更新技能：

* [AI助手](#ai-assistant)
* [Jira](#jira)

## AI 助手 {#ai-assistant}

您可以通过AI助手访问AEM中的作业。

从[`experience.adobe.com`，](https://experience.adobe.com)打开AI助手，然后使用`Ask AI Assistant anything`字段以自然语言指定提示开始交互：

![内容更新作业](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### 配置发布URL {#configuring-the-publish-url}

要使用发布（面向公众）URL，必须一次性配置：

* 先决条件：

   * 要进行配置，用户必须具有系统管理员或产品管理员权限。

* 配置：

   1. 通过请求URL的内容更新来调用内容更新技能。
   1. 助手将通过询问您一系列问题来引导您完成配置。
   1. 完成后，发布URL即已配置并可使用。

例如：

![内容更新技能 — 配置发布URL](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-publish-url-configuration.png)

### 提示 {#prompts}

要启动内容更新，您可以提供各种自然语言提示。 您需要指定要更新的页面的面向公众的（发布）URL或创作环境URL。 部分（但不是全部）支持的动词；替换、更新、删除、更改、修订、修改、调整、删除。

>[!NOTE]
>
>使用[Jira](#jira)进行交互时，可以使用文件上载，但AI Assistant不支持文件上载。

### 示例提示 {#sample-prompts}

示例提示包括：

* 在`<your-publish-URL>`更新中“您的完美咖啡离您还有四个问题！” “你的咖啡，你的方式！”
* 在`<your-author-env-URL>`上，将图像从“holdingcup.png”替换为“stairhead.png”
* 在`<your-publish-URL>`上，将“参加我们的咖啡测验”按钮更改为更吸引人的版本
* 在`<your-author-env-URL>`上删除“未领回的奖励是已错过的礼物！”部分

## Jira {#jira}

通过将内容更新作业与Jira结合使用，您可以根据自动编辑的操作说明创建票证。

### 创建票证 {#create-a-ticket}

创建Jira票证（任何类型）。 票证的&#x200B;**描述**&#x200B;字段中需要两个基本详细信息：

1. 您需要编辑的页面的面向公众的URL。

1. 所需的更改。

   该作业支持以下格式范围来描述更改：

   * 票证描述中的自然语言
      * 例如“将标题从X更改为Y”
   * 已附加注释的PDF
      * 例如，创建页面的PDF并添加注释，其中详述您想要更改的内容
   * 所附的PDF中的备注
      * 例如，创建页面的PDF并添加注释，其中详述需要更改的内容
   * 附加注释的屏幕截图
      * 例如，拍摄部分页面的屏幕快照并添加注释，其中详细描述您要更改的内容
   * 附加的Microsoft Word文件，包含自然语言更改

### 从您的票证调用作业 {#invoke-the-job-from-your-ticket}

要使用作业，请向票证添加注释。 在注释中提及带有`@`符号的作业以及说明。

例如：

* `@aemagent@adobe.com process this ticket`

### 工作如何交互 {#how-the-agent-interacts}

向作业发出命令后，作业会在Jira中做出响应，并带有注释。 这些注释详细说明了作业的进度和采取的操作。

在用于触发更新的`process`命令的情况下，响应可能遵循以下顺序：

* 初始注释用于确认作业已启动。

* 任务完成后，作业会使用另一个注释进行响应，其中包含所执行操作的详细信息。
   * 作业进行的内容更新是无损的 — 这意味着对预览实例进行了更新。
   * 评论包含更新的链接，以便您可以根据需要查看和发布，或将Jira分配给负责人员。

* 下图显示了一个触发内容更新作业的`process`命令的Jira示例：

  ![使用Brand Experience Agent的内容更新作业的Jira示例](assets/content-update-jira-example.png)

## 激活 {#activation}

您可以通过[游乐场](https://www.aem.live/developer/aem-playground)探索AEM代理，或与您的CSM或TAM联系，讨论通过代理SKU进行访问的问题。

## 限制 {#limitations}

请注意以下限制：

* 与[Jira](#jira)交互时可以使用文件上载，但在与[AI助手](#ai-assistant)交互时不支持文件上载。
