---
title: Forms Experience Builder
description: 使用表单片段更快地制作强大的表单
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 6134772ea9916fc17fb7fc8a30e18799a81d4994
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 3%

---


# Forms Experience Builder简介

>[!IMPORTANT]
>
> **文档可能会发生变化**：此文档目前正在针对产品进行测试，因此可能会进行更新和修订。随着Forms Experience Builder在率先采用者计划中的不断演进，功能、命令和示例可能会发生变化。

AEM Forms Experience Builder利用创新型人工智能的强大功能实现民主化并加速数字表单体验的创建和更新。 通过支持通过自然语言交互驱动的基于意图的工作流，它使用户能够快速轻松地无缝设计、修改和优化表单。

Forms Experience Builder构建于现代Web技术之上，由高级AI服务提供支持，它使技术用户和非技术用户都能够通过对话界面创建完善的专业级表单。 这种革命性的方法可将实现价值的时间从数天减少到数小时，通过界面简化消除技术障碍，并可在整个形式的生态系统中扩展现代化工作。



## 核心功能

Forms Experience Builder提供两种用于创建强大数字表单的主要工作流程：

### &#x200B;1. AI支持的表单创建

**自然语言表单生成**

使用纯英文描述从头开始创建完整的表单。 您只需描述自己的要求，例如“创建一个具有评级尺度和评论字段的客户反馈表单”，Forms Experience Builder即会生成相应的表单结构。 您可以使用可视编辑器的体验生成器来添加更多字段、验证规则和提交逻辑。

**动态字段管理**

通过对话式命令添加、修改或删除表单字段。 AI理解上下文，可以根据您的要求智能建议字段类型、验证规则和用户界面改进。

**布局优化**

通过自然语言更新表单布局和配置。 请求更改（如“将表单布局更改为向导布局”）以及Forms Experience Builder应用适当的样式和布局调整。

**完整的提交操作配置**

配置表单提交以与现有业务系统集成：

- **电子邮件集成**：设置自动电子邮件通知和确认
- **REST API端点**：连接到自定义应用程序和服务
- **云存储**：与Azure Blob Storage、SharePoint和OneDrive集成
- **工作流自动化**：连接到Power Automate和Workfront Fusion
- **营销平台**：与Marketo直接集成，用于潜在客户管理
- **AEM工作流**：利用现有AEM工作流功能


### 2.智能导入和转换

**支持的导入格式**

将现有表单和文档转换为交互式数字体验。 Forms Experience Builder支持：

- **Acroforms**：具有现有字段结构的交互式PDF forms
- **XFA PDF**：复杂的基于XML的表单架构
- **平面PDF**：转换为交互式表单的静态文档
- **图像和屏幕截图**：JPG、PNG格式（与团队核对大小限制）
- **手绘Forms**：草图和纸质照片


**智能转换进程**

分析上传的内容以便：

- 检测字段类型和关系
- 尽可能保留布局
- 通过现代响应式设计进行增强
- 添加高级验证和条件逻辑
- 优化辅助功能和移动体验

## 工作原理

Forms Experience Builder遵循一种简单的对话式方法：

    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │ 1. 描述    │───▶│ 2. AI创建│───▶│ 3。 优化和    │
    │您的表单      │    │初始表单   │    │配置      │
    │要求   │    │                 │    │                 │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
    │                       │                       │
    │                       │                       │
    ▼                       ▼                       ▼
    ┌───────────────────────────────────────────────────────────────────────────┐
    │ “创建贷款申请表”→含相关内容的表格                  │
    │ “添加电子邮件字段”           →字段和基本                          │
    │“将电子邮件字段的值设置为@firstname@gmail.com”→验证规则   │
    └───────────────────────────────────────────────────────────────────────────┘

## 示例场景

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Transform PDF Forms to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">将PDF forms转换为数字Forms</p>
                    <p class="is-size-6">将Acroform、XFA PDF或平面PDF文档转换为具有增强功能的响应式交互式数字表单。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Modernize Legacy XFA Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">实现旧版XFA Forms的现代化</p>
                    <p class="is-size-6">通过改进的用户工作流程，将复杂的XFA应用程序转换为现代的、可访问的数字体验。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Convert Screenshots to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">将屏幕截图转换为数字Forms</p>
                    <p class="is-size-6">将图像、屏幕快照或手绘表单转换为功能齐全的数字体验。</p>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- #### Import and Enhance Web Forms

Import existing HTML forms and enhance them with advanced features while preserving existing functionality.

**Key benefits:**

- Advanced validation and business logic
- Conditional field behaviors
- Multi-channel submission options
- Enhanced user experience design -->

## Forms Experience Builder与传统开发

| 方面 | 传统表单创建 | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **创建时间** | 2-3天 | 2-3小时 |
| **技术知识** | 必填 | 非必需 |
| **验证规则** | 手动编码 | 自然语言 |
| **辅助功能** | 手动实施 | 内置合规性 |


## 为组织带来的好处

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Democratized Form Creation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">民主化表单创建</p>
                    <p class="is-size-6">通过自然语言对话，使非技术性用户能够在不具备编程知识的情况下创建复杂的表单。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Reduced Time to Value (TTV)">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">缩短实现价值的时间(TTV)</p>
                    <p class="is-size-6">大幅加快表单开发，从几天缩短到几小时，使数字计划更快走向市场。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Interface Simplicity">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">界面简化</p>
                    <p class="is-size-6">通过直观的对话界面消除学习曲线，减少培训时间并提高采用率。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Scaling Modernization Efforts">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">扩展现代化工作</p>
                    <p class="is-size-6">高效地实现旧版表单产品组合现代化，保留业务逻辑并增强整个表单生态系统的用户体验。</p>
                </div>
            </div>
        </div>
    </div>
</div>

## 加入

Forms Experience Builder目前作为早期访问(EA)计划的一部分提供。 要参与并获得访问权限，您需要以下信息：

### 所需信息

- **IMS组织ID**：您的Adobe组织标识符
- **项目ID**：您在Adobe Experience Cloud中的特定项目标识符
- **项目详细信息**：时间表、范围和预期用例
- **正式工作电子邮件**：与您组织的Adobe帐户关联


### 如何获取IMS组织ID和项目ID

有关查找IMS组织ID和项目ID的详细步骤，请参阅：

- [Adobe Experience Cloud组织设置指南](/help/onboarding/cloud-manager-introduction.md)
- [项目和环境管理](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

### 请求访问

1. 使用上述指南收集您的IMS组织ID和项目ID
2. 向[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)发送一封请求访问的电子邮件
3. 在您的请求中包含：
   - 组织名称和IMS组织ID
   - 项目ID
   - 项目时间表和范围
   - 预期用例和业务目标

>[!IMPORTANT]
>
> **有限可用性计划**：访问Forms Experience Builder需要获得内部利益相关者的批准。 Adobe将根据项目容量以及与早期访问标准的符合情况审查您的请求。 批准并不保证，具体取决于当前计划的可用性。

有关提前访问程序及其功能的详细信息，请参阅[AEM Forms提前访问文档](/help/forms/early-access-ea-features.md)。


## 快速入门

要开始使用Forms Experience Builder，请访问[Forms Experience Builder文档](forms-ai-assistant-getting-started.md)。 您可以通过Forms编辑器或通用编辑器访问AEM Forms Experience Builder，具体取决于您的首选工作流程。

对于希望转变表单创建过程的组织，Forms Experience Builder提供了一个强大、直观的解决方案，它将对话式人工智能的灵活性与企业级表单管理的强大功能结合起来。
