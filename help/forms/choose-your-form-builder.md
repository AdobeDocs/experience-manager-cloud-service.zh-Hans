---
title: 表单生成器：选择您的方法
description: 比较表单构建器并找到创建自适应表单的正确方法。 无论您是需要模板还是需要构建复杂表单的表单创建者，请根据自己的需要选择最佳的表单生成器。
keywords: 表单生成器， AEM forms，表单生成器，创建表单，表单生成器，自适应表单，核心组件，基础组件， edge delivery services，构建表单
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: choose-form-builder-guide
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 8%

---


# 表单生成器：选择您的方法 {#choose-your-form-builder}

Adobe Experience Manager (AEM) Forms提供了三种强大的表单构建方法，每种方法均针对不同的用例、技术要求和发布目标而设计。 无论您是正在查找模板的表单创建者还是构建复杂表单的开发人员，本指南都可以帮助您为您的项目选择正确的表单生成器。

## 快速决策指南

使用本快速参考可确定符合您需求的最佳表单生成器：

| **如果您需要……** | **选择** |
|-------------------|------------|
| **具有最新功能的现代、可扩展表单** | 核心组件 |
| 高流量网站的&#x200B;**快如闪电的表单** | 通用编辑器 |
| **维护现有表单或旧版集成** | Foundation 组件 |
| **可视化拖放创作** | 核心组件或通用编辑器 |
| **基于电子表格的表单创建** | 基于文档的创作 |
| **全渠道投放（Web、移动设备、网亭）** | 核心组件（使用Headless API） |
| **自定义前端应用程序(React、Angular)** | 核心组件（使用Headless API） |
| **完全控制表单渲染** | 核心组件（使用Headless API） |

## 了解表单生成器选项

AEM Forms提供了三种主要的表单构建方法，每种方法均针对不同类型的表单创建者和用例而设计。 无论您是需要简单的表单生成器来执行快速任务，还是需要高级表单生成器功能来执行复杂的项目，有一种方法可以满足您的需求：

### 基础组件表单生成器

基础组件代表着经典的AEM Forms创作体验。 虽然仍受支持，但主要建议维护现有表单而不是创建新表单。

**关键特性：**

- 传统AEM创作界面
- 现有工作流的经验证的稳定性
- 仅限于AEM发布
- 基本组件库

### 核心组件表单生成器

核心组件通过改进的性能、可访问性和灵活性提供最新的AEM Forms功能。 此表单生成器非常适合于需要具有现代化功能的专业结果的表单创建者。 它支持AEM和Edge Delivery Services发布，并自动生成Headless表单以在多个平台上交付API驱动。

**关键特性：**

- 现代的标准化组件
- 增强的性能和可访问性
- 灵活的发布选项(AEM + Edge Delivery)
- 高级自定义功能
- 面向未来的体系结构
- 用于全渠道投放的Headless表单自动生成

### 通用编辑器(Edge Delivery Services)

通用编辑器为Edge Delivery Services提供了两种强大的创作方法：WYSIWYG可视化创作和使用电子表格进行基于文档的创作。 这种表单生成器方法非常适合于希望以卓越的性能快速创建表单的用户。

**关键特性：**

- 卓越性能（Lighthouse得分较高）
- 两种创作方法：WYSIWYG和document-based
- 针对Edge Delivery Services进行优化
- 卓越的性能和SEO
- 快速开发和部署


## 详细比较

### 技术功能

| **功能** | **基础** | **核心** | **通用编辑器** | **基于文档** |
|----------------|----------------|----------|---------------------|-------------------|
| **表单复杂性** | 基本 | 高级 | 高级 | 从简单到适中 |
| **规则引擎** | 高级 | 高级 | 高级 | 有限制 |
| **自定义组件** | ✅ | ✅ | ✅ | ✅ |
| **主题** | ✅ | ✅ | 项目级 | 项目级 |
| **模板** | ✅ | ✅ | 仅初始内容 |  |
| **片段** | ✅ | ✅ | ✅ | ✅ |
| **本地化** | ✅ | ✅ | 通过AEM Sites | 手动/功能 |

### 集成和提交

| **功能** | **基础** | **核心** | **通用编辑器** | **基于文档** |
|-------------|----------------|----------|---------------------|-------------------|
| **数据模型** | FDM，自定义 | FDM，自定义 | FDM，自定义 | 自定义 |
| **提交操作** | 多个选项 | 多个选项 | 多个选项 | 仅限电子表格 |
| **预填充** | ✅ | ✅ | 通过向导 | ✅ |
| **验证码** | 多种类型 | reCAPTCHA、hCaptcha | reCAPTCHA Enterprise | reCAPTCHA Enterprise |
| **附件** | ✅ | ✅ | ✅ | 抢先体验 |
| **数字签名** | ✅ |  |  |  |

### 发布和性能

| **外观** | **基础** | **核心** | **通用编辑器** | **基于文档** |
|------------|----------------|----------|---------------------|-------------------|
| **正在发布** | 仅限 AEM | AEM + Edge Delivery + Headless API | Edge Delivery | Edge Delivery |
| **性能** | 标准 | 已改进 | Lighthouse得分较高 | Lighthouse得分较高 |
| **SEO优化** | 基本 | 良好 | 优秀 | 优秀 |
| **移动响应** | 良好 | 优秀 | 优秀 | 优秀 |

## 选择正确的生成器

### 选择基础组件，如果：

- 您正在维护现有的基于Foundation的表单
- 您需要数字签名集成
- 您的工作流取决于已建立的Foundation功能
- 您正在满足仅限AEM的发布要求

**适用于：**&#x200B;表单维护、旧版系统集成、已建立的工作流

### 在下列情况下选择核心组件：

- 你正在建造新的现代形式
- 您需要灵活地在AEM或Edge Delivery Services上发布
- 您需要最新的功能
- 您需要高级自定义和设置主题
- 可访问性和性能是优先事项
- 您需要面向未来的技术

**非常适合：**&#x200B;新项目、可扩展解决方案、现代Web体验

### 选择通用编辑器，如果：

- 您需要卓越的性能和SEO
- 您正在为Edge Delivery Services站点构建
- 您需要具有自定义操作的复杂表单
- 需要与外部系统集成

**适用于：**&#x200B;高性能网站、Edge Delivery Services、可视化创作工作流

### 选择基于文档的创作，如果：

- 企业用户更喜欢基于电子表格的创作
- 您需要快速原型制作和部署
- Forms相对简单（调查、注册、反馈）
- 电子表格中的数据收集符合您的需求
- 无需高级提交工作流

**适用于：**&#x200B;快速部署、业务用户创作、简单的数据收集


## 迁移注意事项

### 从基础到核心组件

- **推荐的方法：**&#x200B;使用[迁移实用工具工具](/help/forms/migration-utility-tool-for-af-core-components.md)
- **优点：**&#x200B;新功能、更好的性能、双发布功能
- **工作量：**&#x200B;中高低，具体取决于表单复杂度

### 从传统编辑器到通用编辑器

- **方法：**&#x200B;使用WYSIWYG或在通用编辑器中基于文档的创作重新生成表单
- **优点：**&#x200B;卓越的性能、现代开发经验、高SEO分数
- **工作量：**&#x200B;复杂表单工作量高，简单表单工作量低

## 快速入门

选择表单生成器后：

### 基础组件

1. [创建自适应表单（基础组件）](/help/forms/creating-adaptive-form.md)
2. [Foundation Components创作指南](/help/forms/introduction-forms-authoring.md)

### 核心组件

1. [创建自适应表单（核心组件）](/help/forms/creating-adaptive-form-core-components.md)
2. [核心组件功能概述](/help/forms/adaptive-form-core-components-json-schema-form-model.md)

### 通用编辑器(Edge Delivery Services)

1. **WYSIWYG创作：** [通用编辑器入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
2. **基于文档的创作：** [使用电子表格生成您的第一个表单](/help/edge/docs/forms/tutorial.md)


## 需要帮助进行决策？

仍不确定要选择哪个表单生成器？ 请考虑以下因素：

- **团队专业知识：**&#x200B;您团队的技术技能水平如何？
- **项目时间表：**&#x200B;您需要以多快的速度部署？
- **性能要求：**&#x200B;速度和SEO是否至关重要？
- **未来的可伸缩性：**&#x200B;是否需要经常展开或修改表单？
- **发布目标：**&#x200B;您的表单将发布到何处？

有关个性化指导，请咨询您的AEM Forms实施团队或Adobe支持人员。

## 相关文章

- [详细的表单创作比较](/help/edge/docs/forms/authoring-a-form.md)
- [AEM Forms核心组件概述](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)
- [适用于Forms的Edge Delivery Services概述](/help/edge/docs/forms/overview.md)
- [带核心组件的Headless自适应Forms](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)
