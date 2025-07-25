---
title: Adobe Experience ManagerAI助手（私人测试版）
description: 使用Adobe Experience Manager中的AI助手帮助您查找答案、排除故障并浏览Sites、Assets、Dynamic Media、Cloud Manager和Forms。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 0afd74120380c9ae3d02db9fb684189c2f19648f
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---

# 关于Adobe Experience Manager中的AEM AI助手 {#aem-home}

AEM (Adobe Experience Manager)中的AI助手提供了一个对话界面，旨在简化对Adobe Experience Manager相关查询的查找。 它可帮助您访问Experience League中的产品知识、排查问题并探索可用信息。 在私人测试版计划期间，AEM AI Assistant支持Adobe Experience Manager as a Cloud Service，包括Sites、Assets、Dynamic Media、Cloud Manager和Forms。

>[!IMPORTANT]
>请确保您已查看并提交了用户协议，以便Adobe能够启用AI Assistant功能，以便您试用并参与私人测试版计划。
>
>如有任何问题，请通过与Adobe ID关联的电子邮件地址向[Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com)发送电子邮件。

## 隐私、安全和治理

AEM AI Assistant的设计高度强调隐私、安全和治理。

本文概述了AEM AI Assistant可提供的以信任为中心的功能：

* AEM AI Assistant不使用任何个人数据，包括用于培训目的。
* AEM AI助手无法访问消费者数据。
* 需要明确权限才能与AEM AI助手交互。
* 不与其他客户共享用户提供的提示（问题、查询等）。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->


## 了解产品知识的AEM AI Assistant {#ai-prod-insights}

产品知识包含从Adobe Experience League文档衍生的概念和主题。 这些问题可划分为以下子组：

| 产品知识 | 示例 |
| --- | --- |
| 点式学习 | <ul><li>什么是通用编辑器？</li><li>如何在Cloud Manager中创建程序？</li></ul> |
| 打开发现 | <ul><li>如何使用通用编辑器？</li><li>是否有办法将内容从一个环境复制到另一个环境？</li></ul> |
| 疑难解答 | <ul><li>为何无法访问通用编辑器？</li><li>我的管道为什么会失败？</li></ul> |

AEM AI Assistant的当前范围侧重于解决Adobe Experience Manager as a Cloud Service的产品知识问题。 此范围包括对关键领域(如Sites、Assets、Forms和Cloud Manager)的全面支持。

## 如何提出有效的问题 {#ai-craft-questions}

要从AEM AI Assistant获得最准确的响应，请务必用清楚明了的上下文表述您的问题。 使用以下提示来确保您的查询清晰且结构合理：

* 以简洁明了的方式清楚地陈述您的任务或问题。
* 避免使用含糊不清的措辞或过于复杂的语法，以增进理解。
* 包含有关您的任务或问题的相关上下文，因为此方法有助于AEM AI助手提供更精确且相关的答案。
例如，在提示符下，为您正在使用的AEM解决方案命名(Sites、Assets、Dynamic Media、Cloud Manager和Forms)会很有帮助。

### 不支持的问题的示例 {#ai-unsupported-questions}

| 区域 | 示例 |
| --- | --- |
| 运营见解 | <ul><li>我的租户中有多少个开发环境？</li><li>谁启动了最后一个生产管道？</li></ul> |
| 疑难解答 | <ul><li>为什么我的生产管道失败？</li></ul> |
| 任务和自动化 | <ul><li>从开发分支为我配置代码质量管道。</li></ul> |


## 使用AEM AI助手 {#ai-use}

### 通过Admin Console启用AEM AI助手访问

要使用AEM AI助手，您的组织必须选择Admin Console级别的加入。 产品管理员创建（或选择）用户组并授予其新的“AI助手”权限。 任何添加到该组的人都会立即获得AEM中的“助手”访问权限。 如果目标是实现公司范围的可用性，管理员只需将所有用户分配给该组即可。

Admin Console中的![AEM AI助手](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

从员工的角度来看，此过程非常简单：确定贵组织中Adobe Experience Manager的产品管理员，并请求将其添加到支持AI的用户组。 一旦您出现在该组中，“助理”图标将在您下次登录时自动显示。

管理员应牢记常规的Cloud Manager管理。 您必须在Admin Console中拥有产品管理员权限才能创建配置文件、管理用户组或编辑权限。 如果用户还需要该助理的内置&#x200B;**创建支持票证**&#x200B;功能，请将标准&#x200B;**支持管理员**&#x200B;角色(标准Admin Console角色)添加到相同的个人或组。

![在Admin Console的AEM AI助手中创建技术支持票证](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

有关在AEM as a Cloud Service中设置用户和组的引导式演练，请参阅[配置对AEM as a Cloud Service的访问权限](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/accessing/overview)。

另请参阅[自定义权限](/help/implementing/cloud-manager/custom-permissions.md)。


### 启动或重置对话

您可以重置AEM AI助手，并在要更改主题时开始新对话。 在排除查询失败或提供错误信息时，此功能特别有用。

![开始对话按钮](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**要启动或重置对话：**

1. 在AEM AI助手上，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 要通知AEM AI助手有关新主题或主题更改的信息，请单击&#x200B;**开始新对话**。

### 使用可发现性

AEM AI Assistant包括可发现性功能，可帮助您探索支持的主题和类别。

![创意灯泡图标](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**要使用可发现性：**

1. 在AEM AI Assistant的右上角附近，单击![学习图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)。
1. 选择一个类别以查看相关提示的列表。
1. 选择一个提示以更好地了解AEM AI助手可以回答的问题类型。

### 提供有关AEM AI助手的反馈

您的输入有助于改进AEM AI Assistant以提高性能和准确性。

通过以下选项，分享您对AEM AI Assistant体验的反馈：

![竖起拇指、竖下拇指和标记图标](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| 图标 | 描述 |
| --- | --- |
| ![竖起大拇指图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 单击以指示哪些方面进展顺利，并分享积极反馈。 |
| ![拇指朝下缩进图示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 单击以提供改进建议。 添加有关您的体验的特定评论，这些评论每天都会审核。 |
| ![标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | 单击可报告关注事项或提供关于您与AEM AI助手交互的详细反馈。 |

## 关于AEM AI助理的常见问题解答 {#ai-faq}

以下是有关AI助手的一些常见问题的答案：

* **AEM AI助手实时提供的信息吗？**\
  不行。AI Assistant从Adobe Experience League文档获取其内容。 对内容的更新可能需要一些时间才能反映在其响应中。
* **AEM AI Assistant支持哪些Adobe应用程序？**\
  目前，AI Assistant支持AEM as a Cloud Service中的产品知识查询，包括Sites、Assets、Dynamic Media、Cloud Manager和Forms。
* **AEM AI Assistant有哪些功能？**\
  AEM AI Assistant旨在回答与Adobe产品知识相关的查询。
* **AEM AI助手是否使用个人信息提供培训数据？**\
  不行。AEM AI助手不使用个人信息提供培训。 避免与AEM AI助手共享您或其他人的个人信息，包括姓名或联系方式。


## AEM Forms AI助手(Forms Experience Builder) {#ai-forms-builder}

除了用于产品知识的一般AEM AI助手外，AEM还提供专门的&#x200B;**[AEM Forms AI助手(Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**。 此增强型助理可以通过自然语言提示和回答表单特定问题来主动帮助您创建和配置表单。

### 主要功能

AEM Forms AI助手提供：

* **表单创建**：使用自然语言描述从头开始创建新表单。
* **设计导入**：将现有设计(PDF、Figma、图像)转换为功能性AEM Forms。
* **表单配置**：添加字段、面板、验证规则和条件逻辑。
* **布局管理**：组织表单结构并优化不同设备。
* **集成设置**：配置表单提交和数据处理。
* **产品知识**：回答有关AEM Forms功能和最佳实践的问题。

### 访问位置

AEM Forms AI助手包括以下内容：

* **通用编辑器**：适用于具有可视化编辑功能的Edge Delivery Services表单。
* **自适应Forms编辑器**：有关详细的表单配置和高级功能。
* **Forms管理UI**：用于高级表单创建和管理任务。

### 快速入门

>[!NOTE]
>
> AEM Forms AI助手(Forms Experience Builder)可通过私人测试版计划获取。 将工作地址中的电子邮件发送至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)以请求访问权限。

要了解有关使用AEM Forms AI助手的详细信息，请参阅[AEM Forms AI助手](/help/edge/docs/forms/forms-ai-assistant.md)文档。

### 示例用例

* **“创建包含姓名、电子邮件、评分和评论字段的客户反馈表单”**
* **“将此上载的PDF应用程序表单转换为数字自适应表单”**
* **“添加条件逻辑以仅在婚姻状态为“已婚”时显示配偶信息”**
* **“配置此表单以将数据提交到Customer Relationship Management系统”**

这个专业化的AEM Forms AI Assistant代表了表单构建的下一个发展方向，它将AI的强大功能与AEM的强大表单功能相结合，可简化表单创建工作流。
