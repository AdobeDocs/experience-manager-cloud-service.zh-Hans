---
title: 内容更新技能
description: 了解Experience Production Agent的内容更新技能及其可以对您执行的操作。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: d5b7a8343551c5880b40c692266f33a1864f9d2b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 2%

---


# 内容更新技能 {#content-update}

Experience Production Agent的内容更新技能可自动执行内容生产，以加快Adobe Experience Manager (AEM) as a Cloud Service和Edge Delivery Services的日常任务。

内容更新技能可更新CMS中的现有内容，包括内容片段、页面、表单和资源。 代理可以执行更新、删除、替换或添加内容元素等操作，以保持体验准确且最新。 输入可以是自然语言描述，在与Jira PDF一起使用时，屏幕截图也可以提供输入。

## 概述 {#overview}

内容更新技能可将您通过自然语言或可视化图表提供的详细信息转换为页面上的内容更新。 您可以提供需要更新的页面的URL，以及需要更新的内容的详细信息，座席技能将完成您的任务。

## 功能 {#capabilities}

您可以从以下位置访问内容更新技能：

* [AI 助手](#ai-assistant)

* [Jira](#jira)

## AI 助手 {#ai-assistant}

您可以通过AI助手访问AEM业务代理。

从experience.adobe.com打开AI助手，然后使用`Ask AI Assistant anything`字段以自然语言指定提示以开始交互：

![访问发现代理](/help/ai-in-aem/agents/production/assets/content-update-ai-assistant-example.png)

<!--
### Sample Prompts {#sample-prompts}

To initiate content updates you can give a wide range of natural language prompts. You also need to specify the public facing URL of the page you want to update:

* Change your headlines

  * On your-URL change the headline from X to Y
-->

>[!NOTE]
>
>使用[Jira](#jira)进行交互时，可以使用文件上载，但AI Assistant不支持文件上载。

## Jira {#jira}

通过将内容更新技能与Jira结合使用，您可以创建包含自动编辑说明的票证。

### 创建票证 {#create-a-ticket}

创建Jira票证（任何类型）。

票证的&#x200B;**描述**&#x200B;字段中需要两个基本详细信息：

1. 您需要编辑的页面的面向公众的URL。

1. 所需的更改。

   目前，该技能支持以下格式范围来描述您所做的更改：

   * 票证描述中的自然语言
      * 例如“将标题从X更改为Y”
   * 已附加注释的PDF
      * 例如，创建页面的PDF并添加注释，其中详述您想要更改的内容
   * 所附的PDF中的备注
      * 例如，创建页面的PDF并添加注释，其中详述需要更改的内容
   * 附加注释的屏幕截图
      * 例如，拍摄部分页面的屏幕快照并添加注释，其中详细描述您要更改的内容
   * 附加的Microsoft Word文件，包含自然语言更改

### 从您的票证中调用代理 {#invoke-the-agent-from-your-ticket}

要使用代理，请向票证添加注释。 在注释中提及带有`@`符号的代理，以及它应执行的命令；例如：

* `@aemagent@adobe.com process`

目前，代理程序了解以下命令：

* `process` — 处理请求
* `cancel` — 取消处理请求
* `retry` — 重新处理请求
* `feedback` — 将反馈应用于上一代
* `reprocess` — 重新处理原始请求

### 座席如何进行交互 {#how-the-agent-interacts}

向代理发出命令后，代理会在Jira中回复注释。 这些注释详细说明了座席的进度和采取的操作。

在用于触发更新的`process`命令的情况下，响应可能遵循以下顺序：

* 初始注释用于确认座席已启动。

* 任务完成后。 代理使用另一个备注进行响应，其中包含已执行操作的详细信息。
   * 代理进行的内容更新是无损的 — 这意味着对预览实例进行了更新。
   * 评论包含更新的链接，以便您可以根据需要查看和发布，或将Jira分配给负责人员。

* 下图显示了一个触发内容更新技能的`process`命令的Jira示例：

  ![使用Experience Production Agent的内容更新技能的示例Jira](assets/content-update-jira-example.png)

### 激活 {#activation}

要使用Jira激活并访问生产代理，您需要向Adobe发送电子邮件。 要开始配置，您可以联系：

* `experience-production-agent@adobe.com`
* 或与您的客户团队联系

为了加快该过程，提供以下信息会很有帮助：

* 适用于AEM as a Cloud Service的
   * 您需要提供以下信息：
      * 组织 ID
      * `product_id`
      * `profile_id`

   * 可以通过以下步骤找到这些值：
      * 您的管理员需要访问<https://adminconsole.adobe.com/>
      * 选择&#x200B;**Adobe Experience Manager as a Cloud Service**
      * 选择适当的AEM实例
      * 选择允许对相关内容执行读写操作的配置文件
      * 获取浏览器URL
      * 从URL提取`product_id`和`profile_id`。
例如，<https://adminconsole.adobe.com/products/profiles/users>

* Edge Delivery文档创作
   * 向您的Adobe团队提供以下信息：
      * 相关域
      * 相关Github信息：
         * 组织
         * 存储库
         * 分支

## 限制 {#limitations}

目前，内容更新器的限制包括：

* 与[Jira](#jira)交互时可以使用文件上载，但在与[AI助手](#ai-assistant)交互时不支持文件上载。
