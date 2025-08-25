---
title: 创建交互式通信
description: 创建个性化、数据驱动的通信。 通过指南和教程，探索关键功能、入门步骤和实际用例。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 5dd94d22a2a1a2ddbfd7dee44e93e6ea0c4b7ad9
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# 创建交互式通信

交互式通信使您能够创建、管理和提供个性化的交互式通信，包括客户服务、计费、载入文档、优惠信函、帐户更新等。 它旨在支持任何场景，其中动态、特定于用户的内容可增强各行业的通信体验。

假设您需要向数千名客户发送银行对帐单、保险单或水电费。 每个报表都具有相同的布局但个性化的数据。 交互式通信(IC)使这成为可能。

![查找IC文档](/help/forms/interactive-communication/assets/Picture1.png)

手动生成这些文档可能非常耗时，并且经常会导致不一致，特别是在需要个性化和数据集成时。 使用交互式通信编辑器，用户可以简化创建交互式通信的过程。

## 先决条件

* [确保作者是forms-users组的成员](/help/forms/setup-forms-cloud-service.md#configure-users)

## 创建交互式通信

根据所需的重用级别和数据集成，从不同的方案中选择以创建交互式通信：

+++ 创建空白交互式通信

通过创建空白的交互式通信，您可以从头开始创建，非常适合您希望完全控制布局、结构和逻辑的情况。
要遵循的步骤：

1. 打开&#x200B;**Adobe Experience Manager (AEM) Forms as a Cloud Service实例**。
1. 导航到&#x200B;**Forms > Forms和文档**。
1. 单击&#x200B;**创建>交互式通信**。

   ![查找IC文档](/help/forms/interactive-communication/assets/comm.png)

1. 在创建屏幕中，将&#x200B;**模板**&#x200B;字段留空。

   ![查找IC文档](/help/forms/interactive-communication/assets/create-ic-document.png)

1. 填写其他详细信息，如标题、姓名、作者等。
1. 单击&#x200B;**创建**&#x200B;进入交互式通信编辑器UI并开始设计。
1. 它会打开IC编辑器，您可以在其中开始设计通信。
+++

+++ 创建基于模板的交互式通信

使用模板可通过重用一致的布局元素（如页眉、页脚、徽标或标准格式）帮助加快设计。
模板可确保品牌一致性，并节省常用通信类型的时间。 执行以下步骤：

1. 打开AEM Forms as a Cloud Service实例。
1. 转到&#x200B;**Forms > Forms &amp; Documents**，单击&#x200B;**创建>交互式通信**。
1. 在创建表单中，从下拉列表中&#x200B;**选择**&#x200B;启用的模板。
1. 填写其他详细信息，如标题、姓名、作者等。
1. 单击&#x200B;**创建**&#x200B;以设计您与所选模板结构的通信。
1. 它会打开IC编辑器，您可以在其中开始设计通信。
+++

+++ 创建数据交互的交互式通信

数据交互通信使用后端数据自动将内容个性化。
非常适合于结构保持不变，但数据因收件人而异，但为语句、发票或通知的情形。 要遵循的步骤：

1. 打开AEM Forms as a Cloud Service实例。
1. 转到&#x200B;**Forms > Forms &amp; Documents**，单击&#x200B;**创建>交互式通信**。
1. 在&#x200B;**表单数据模型**&#x200B;字段中，链接预定义的&#x200B;**FDM（表单数据模型）**。
1. 填写其他详细信息，如标题、姓名、作者等。
1. 在编辑器中使用&#x200B;**数据模型**&#x200B;将字段绑定到动态数据（例如，客户名称、余额、帐号）。
1. 根据需要使用&#x200B;**内容区域、子表单**&#x200B;和&#x200B;**片段**&#x200B;来构造和重复数据。
1. 使用&#x200B;**PDF预览**&#x200B;进行预览，并完成要交付的通信。
1. 它会打开IC编辑器，您可以在其中开始设计通信。

![查找IC文档](/help/forms/interactive-communication/assets/ic-ui.png)
+++

开始构建交互式通信以简化您的工作流并提供有影响力的特定于用户的体验。

## 后续步骤

[创建交互式通信模板](/help/forms/interactive-communication/create-interactive-communication-template.md)
[创建交互式通信片段](/help/forms/interactive-communication/create-interactive-communication-fragment.md)
