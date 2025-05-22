---
title: AEM Forms 与 Edge Delivery Services 常见问题解答
description: 获取有关带有 Edge Delivery Services 和通用编辑器的 AEM Forms 的常见问题的答案。了解多语言表单、全局模板、表单片段、分析和数据集成功能。
feature: Edge Delivery Services
role: User, Developer
hide: true
hidefromtoc: true
exl-id: b39601a1-7f37-4a7d-a4c8-7e79dca074e5
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 98%

---

# 常见问题解答（FAQ）


## 多语言支持和全球使用

### 问：EDS 和通用编辑器如何处理多语言表单？

**答：**&#x200B;多语言表单遵循与 AEM Sites 相同的翻译工作流程。通过使用标准 AEM 翻译功能，可以用多种语言创建表单，以服务于不同的市场。

### 问：我可以创建和使用全局模板和表单片段吗？

**答：**&#x200B;可以，EDS 和通用编辑器均支持全局模板和表单片段。因此您可以创建可在多种表单之间共享的可重复使用的组件。

### 问：是否可以创建一个表单并在多个网页上使用它？

**答：**&#x200B;可以，您可以在一个位置创建一个表单并在多个网页中引用它，类似于自适应表单中的表单嵌入组件功能。

## 数据集成与映射

### 问：表单数据模型（FDM）集成如何与通用编辑器协同工作？

**答：**&#x200B;目前，可以通过规则编辑器为各个字段配置 FDM 集成。自动字段映射功能（类似于自适应表单中的表单数据模型向导）正在开发中，并且即将推出。

## 分析与跟踪

### 问：对于表单分析和跟踪，有哪些推荐的选项？

**答：**&#x200B;有多种分析和跟踪选项：

- Adobe Experience Platform Web SDK（主要推荐）
- 采样度量的操作遥测
- 根据需要与其他分析系统集成

## 文档和资源

### 问：在哪里可以找到有关这些功能的文档？

**答：**&#x200B;您可以在以下位置找到详细文档：

- Forms Crosswalk 文档
- 翻译工作流程的标准 AEM Sites 文档
- 用于表单创作的通用编辑器文档
