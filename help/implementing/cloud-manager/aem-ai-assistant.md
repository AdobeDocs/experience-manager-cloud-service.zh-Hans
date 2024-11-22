---
title: Adobe Experience Manager(Beta有限公司)人工智能助手
description: 使用Adobe Experience Manager中的AI助手帮助您查找答案、排除故障并浏览Sites、Assets、Forms和Cloud Manager。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
source-git-commit: e454581a2e6f2b8184a54d6550daec60e58bbc6c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---

# 关于Adobe Experience Manager中的AI助手 {#aem-home}

AEM (Adobe Experience Manager)中的AI助手提供了一个对话界面，旨在简化对Adobe Experience Manager相关查询的查找。 它可帮助您访问产品知识、排除问题并探索Experience League中可用的信息。 在有限的Beta计划期间，AI助手支持Adobe Experience Manager as a Cloud Service，包括Sites、Assets、Forms和Cloud Manager。

>[!IMPORTANT]
>请确保您已查看并提交了用户协议，以便Adobe能够启用AI Assistant功能，以便您试用并参与Beta计划。
>
>如有任何问题，请通过与Adobe ID关联的电子邮件地址向[Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com)发送电子邮件。

## 隐私、安全和治理

AEM中的AI助手在设计时特别强调隐私、安全和治理。

本文概述了AI Assistant提供的以信任为中心的功能：

* AI助手不使用任何个人数据，包括用于培训目的。
* AI助手无法访问消费者数据。
* 需要明确权限才能与AI助手交互。
* 不与其他客户共享用户提供的提示（问题、查询等）。


## 了解产品知识的AI助手 {#ai-prod-insights}

产品知识包含从Adobe Experience League文档派生出的概念和主题。 这些问题可划分为以下子组：

| 产品知识 | 示例 |
| --- | --- |
| 点式学习 | <ul><li>什么是通用编辑器？</li><li>如何在Cloud Manager中创建程序？</li></ul> |
| 打开发现 | <ul><li>如何使用通用编辑器？</li><li>是否有办法将内容从一个环境复制到另一个环境？</li></ul> |
| 疑难解答 | <ul><li>为何无法访问通用编辑器？</li><li>我的管道为什么会失败？</li></ul> |

AI Assistant的当前范围侧重于解决Adobe Experience Manager as a Cloud Service的产品知识问题。 此范围包括对关键领域(如Sites、Assets、Forms和Cloud Manager)的全面支持。

## 如何提出有效的问题 {#ai-craft-questions}

要从AI助手那里获得最准确的响应，请务必用清楚明了的上下文表述您的问题。 使用以下提示来确保您的查询清晰且结构合理：

* 以简洁明了的方式清楚地陈述您的任务或问题。
* 避免使用含糊不清的措辞或过于复杂的语法，以增进理解。
* 包含有关您的任务或问题的相关上下文，因为此方法有助于AI助手提供更精确且相关的答案。

### 不支持的问题的示例 {#ai-unsupported-questions}

| 区域 | 示例 |
| --- | --- |
| 运营见解 | <ul><li>我的租户中有多少个开发环境？</li><li>谁启动了最后一个生产管道？</li></ul> |
| 疑难解答 | <ul><li>为什么我的生产管道失败？</li></ul> |
| 任务和自动化 | <ul><li>从开发分支为我配置代码质量管道。</li></ul> |


## 使用AI助手 {#ai-use}


### 启动或重置对话

您可以重置AI助手，并在要更改主题时开始新对话。 在排除查询失败或提供错误信息时，此功能特别有用。

![开始对话按钮](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**要启动或重置对话：**

1. 在AI助手上，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 要通知AI助手有关新主题或主题更改的信息，请单击&#x200B;**开始新对话**。

### 使用可发现性

AI Assistant包括可发现性功能，可帮助您探索支持的主题和类别。

![创意灯泡图标](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**要使用可发现性：**

1. 在AI助理的右上角附近，单击![学习图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)。
1. 选择一个类别以查看相关提示的列表。
1. 选择一个提示以更好地了解AI助手可以回答的问题类型。

### 提供关于AI助手的反馈

您的输入有助于改进AI Assistant以获得更好的性能和准确性。

通过以下选项，分享您对AI Assistant体验的反馈：

![竖起拇指、竖下拇指和标记图标](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| 图标 | 描述 |
| --- | --- |
| ![竖起大拇指图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 单击以指示哪些方面进展顺利，并分享积极反馈。 |
| ![拇指朝下缩进图示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 单击以提供改进建议。 添加有关您的体验的特定评论，这些评论每天都会审核。 |
| ![标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | 单击可报告关注事项或提供关于您与AI助手交互的详细反馈。 |

## 关于AI助理的常见问题解答 {#ai-faq}

以下是有关AI助手的一些常见问题的答案：

* **AI助手实时提供的信息吗？**\
  不会。AI Assistant从Adobe Experience League文档获取其内容。 对内容的更新可能需要一些时间才能反映在其响应中。
* **AI助手支持哪些Adobe应用程序？**\
  目前，AI Assistant支持AEM as a Cloud Service，包括Sites、Assets、Forms和Cloud Manager，专门用于产品知识查询。
* **AI助手有哪些功能？**\
  AI Assistant用于回答与Adobe产品知识相关的查询。
* **AI助手是否使用个人信息提供培训数据？**\
  不会。AI助手不使用个人信息进行培训。 避免与AI助手共享您或其他人的个人信息，包括姓名或联系方式。



