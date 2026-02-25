---
title: 内容更新作业
description: 了解Brand Experience Agent的内容更新作业及其可为您执行的操作。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: 71e3770a7a26b8d3144717513f3ec1c997b3b435
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 2%

---


# 内容更新作业 {#content-update}

[Brand Experience Agent](/help/ai-in-aem/agents/brand-experience/overview.md)的内容更新作业可自动执行内容生产，以加速Adobe Experience Manager (AEM) as a Cloud Service和Edge Delivery Services的日常任务。

## 概述 {#overview}

内容更新作业可更新现有内容，包括内容片段、页面、表单和资产。 该作业可以执行更新、删除、替换或添加内容元素等操作，以保持体验准确且最新。 输入可以是自然语言描述，在与Jira PDF一起使用时，屏幕截图也可以提供输入。

内容更新作业将您通过自然语言或可视化图表提供的详细信息转换为页面上的内容更新。 您可以提供需要更新的页面的URL，以及需要更新的内容的详细信息，座席技能将完成您的任务。

## 功能 {#capabilities}

您可以从以下位置访问内容更新技能：

* [AI助手](#ai-assistant)
* [Jira](#jira)

## AI 助手 {#ai-assistant}

您可以通过AI助手访问AEM中的作业。

从[`experience.adobe.com`，](https://experience.adobe.com)打开AI助手，然后使用`Ask AI Assistant anything`字段以自然语言指定提示开始交互：

![内容更新作业](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### 示例提示 {#sample-prompts}

要启动内容更新，您可以提供各种自然语言提示。 您还需要指定要更新的页面的面向公众的URL。 例如：

* 修改以下页面`https://www.your-url.com/sale`将主页标题更新为“黑色星期五特大促销 — 高达70%折扣”，将倒计时计时器更改为“48小时后结束”，删除“注册更新”，将所有“立即购买”按钮更改为“购买优惠”

* `https://www.your-url.com/laptops/your-laptop-model`将横幅副本更新为“仅今天节省300美元”，将定价从1,299美元更新为999美元，删除融资选项横幅

* `https://www.your-url.com/your-sneaker`将库存状态从“缺货”更新为“补货 — 数量有限”，更改大小选择器以绿色突出显示可用大小，删除“即将推出”徽章

* `https://www.your-url.com/your-sneaker`更新产品图像以显示新颜色

>[!NOTE]
>
>使用[Jira](#jira)进行交互时，可以使用文件上载，但AI Assistant不支持文件上载。

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

要使用作业，请向票证添加注释。 在注释中，提及带有`@`符号的作业以及应执行的命令；例如：

* `@aemagent@adobe.com process`

目前，该作业可以理解以下命令：

* `process` — 处理请求
* `cancel` — 取消处理请求
* `retry` — 重新处理请求
* `feedback` — 将反馈应用于上一代
* `reprocess` — 重新处理原始请求

### 工作如何交互 {#how-the-agent-interacts}

向作业发出命令后，作业会在Jira中做出响应，并带有注释。 这些注释详细说明了作业的进度和采取的操作。

在用于触发更新的`process`命令的情况下，响应可能遵循以下顺序：

* 初始注释用于确认作业已启动。

* 任务完成后，作业会使用另一个注释进行响应，其中包含所执行操作的详细信息。
   * 作业进行的内容更新是无损的 — 这意味着对预览实例进行了更新。
   * 评论包含更新的链接，以便您可以根据需要查看和发布，或将Jira分配给负责人员。

* 下图显示了一个触发内容更新作业的`process`命令的Jira示例：

  ![使用Experience Production Agent的内容更新作业的Jira示例](assets/content-update-jira-example.png)

## 激活 {#activation}

要激活并访问通信创建作业，您需要联系Adobe。 要开始配置，您可以：

* 联系人`experience-production-agent@adobe.com`
* 或与您的客户团队联系

为了加快该过程，提供以下信息会很有帮助：

* 对于AEM as a Cloud Service，您需要提供：
   * 组织 ID
   * `product_id`
   * `profile_id`

   * 可以按照以下步骤找到这些值：
      1. 您的管理员需要访问[`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)
      1. 选择&#x200B;**Adobe Experience Manager as a Cloud Service**
      1. 选择适当的AEM实例
      1. 选择允许对相关内容执行读写操作的配置文件
      1. 获取浏览器URL
      1. 从URL提取`product_id`和`profile_id`。
例如，`https://adminconsole.adobe.com/products/profiles/users`

* Edge Delivery文档创作
   * 向您的Adobe团队提供以下信息：
      * 相关域
      * 相关Github信息：
         * 组织
         * 存储库
         * 分支

## 限制 {#limitations}

请注意以下限制：

* 与[Jira](#jira)交互时可以使用文件上载，但在与[AI助手](#ai-assistant)交互时不支持文件上载。
