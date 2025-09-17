---
title: Forms Experience Builder
description: Forms Experience Builder 简介
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: ce61bc434614e5d7b92de3f1290e7e15325d27b7
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 100%

---


# Forms Experience Builder 简介

>[!IMPORTANT]
>
> **文档可能会发生变化**：此文档目前正在针对产品进行测试，因此可能会进行更新和修订。随着 Forms Experience Builder 在早期采用者计划期间不断改进，其功能、命令和示例可能会发生变化。

AEM Forms Experience Builder 利用生成式 AI 的强大功能，使得数字表单体验的创建和更新更加大众化、更加快速。它能够实现基于用户意图的以自然语言交互驱动的工作流，使用户能够快速、轻松、顺畅无缝地设计、修改和优化表单。

Forms Experience Builder 在现代网络技术的基础上构建，以先进的 AI 服务作为驱动，使技术用户和非技术用户都能通过对话式界面创建复杂的专业级表单。这种革命性的方法将实现价值的时间从几天缩短到几小时，通过界面简化消除技术障碍，将现代化工作扩展到您的整个表单生态系统中。

## 核心功能

Forms Experience Builder 提供了两种用于创建强大数字表单的主要工作流：

### &#x200B;1. AI 驱动的表单创建

**使用自然语言生成表单**

使用简单的英语描述从头开始创建完整的表单。只需描述您的要求，例如“创建一个带有评分量表和评论字段的客户反馈表”，Forms Experience Builder 就会生成适当的表单结构。您可以使用可视化编辑器的体验生成器来添加更多字段、验证规则和提交逻辑。

**动态字段管理**

通过对话式命令添加、修改或移除表单字段。AI 会理解上下文，并根据您的要求智能地提出字段类型、验证规则和用户界面改进方面的建议。

**布局优化**

通过自然语言更新表单布局和配置。要求进行更改，例如“将表单布局改为向导式布局”， Forms Experience Builder 就会应用适当的样式调整布局。

**全面的提交操作配置**

配置表单提交，与您现有的业务系统集成：

- **电子邮件集成**：设置自动电子邮件通知和确认
- **REST API 端点**：与自定义应用程序和服务连接
- **云存储**：与 Azure Blob 存储、SharePoint 和 OneDrive 集成
- **工作流自动化**：与 Power Automate 和 Workfront Fusion 连接
- **营销平台**：与 Marketo 直接集成，实现潜在客户管理
- **AEM 工作流**：利用现有的 AEM 工作流功能

### &#x200B;2. 智能导入和转换

**受支持的导入格式**

将现有的表单和文档转变为交互式数字体验。Forms Experience Builder 支持：

- **Acroforms**：具有现有字段结构的交互式 PDF 表单
- **XFA PDF**：基于 XML 的复杂表单架构
- **扁平化 PDF**：将静态文档转换为交互式表单
- **图像和屏幕快照**：JPG、PNG 格式（与团队确认大小限制）
- **手绘表单**：草图和纸质照片

**智能转换过程**

对上传的内容进行分析，以便：

- 检测字段类型和关系
- 尽可能保留布局
- 增强为现代响应式设计
- 添加高级验证和条件逻辑
- 针对无障碍和移动设备体验进行优化

## 如何工作

Forms Experience Builder 采用一种简单的对话式方法：

    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │  1. 描述    │───▶│  2. AI 创建  │───▶│  3.优化 &amp;    │
    │  您的表单      │    │  初始表单   │    │  配置      │
    │  要求   │    │                 │    │                 │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
    │                       │                       │
    │                       │                       │
    ▼                       ▼                       ▼
    ┌───────────────────────────────────────────────────────────────────────────┐
    │  “创建一个贷款申请表”  →  表单中包含相关的                  │
    │  “添加电子邮件地址字段”           →  字段和基本的                          │
    │  “将电子邮件地址字段的值设置为 @firstname@gmail.com” →  验证规则   │
    └───────────────────────────────────────────────────────────────────────────┘

## 场景示例

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Transform PDF Forms to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">将 PDF 表单转换为数字表单</p>
                    <p class="is-size-6">将 Acroforms、XFA PDF 或扁平化 PDF 文档转换为具有增强功能的响应式交互式数字表单。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Modernize Legacy XFA Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">将旧版 XFA 表单现代化</p>
                    <p class="is-size-6">将复杂的 XFA 应用程序转变为改进了用户工作流、现代化、可访问的数字体验。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Convert Screenshots to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">将屏幕快照转换为数字表单</p>
                    <p class="is-size-6">将图像、屏幕快照或手绘表单转变为功能完整的数字体验。</p>
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

## Forms Experience Builder 与传统开发的比较

| 方面 | 传统表单创建 | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **创建时间** | 2-3 天 | 2-3 小时 |
| **技术知识** | 必需 | 不必需 |
| **验证规则** | 手动编码 | 自然语言 |
| **无障碍访问** | 手动实施 | 内置合规 |


## 给组织带来的好处

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Democratized Form Creation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">大众化表单创建</p>
                    <p class="is-size-6">通过自然语言对话，非技术用户无需编程知识也可以创建复杂的表单。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Reduced Time to Value (TTV)">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">减少价值实现时间 (TTV)</p>
                    <p class="is-size-6">将表单开发时间从几天大幅缩短至几小时，加快数字计划的上市速度。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Interface Simplicity">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">界面简洁</p>
                    <p class="is-size-6">通过直观的对话式界面消除学习曲线，减少培训时间，提高采用率。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Scaling Modernization Efforts">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">扩展现代化工作</p>
                    <p class="is-size-6">有效地对旧版表单收藏集进行现代化改造，保留业务逻辑，增强您的整个表单生态系统的用户体验。</p>
                </div>
            </div>
        </div>
    </div>
</div>

## 加入

Forms Experience Builder 目前是早期访问 (EA) 计划的一部分。要参与该计划并获得访问权限，您需要提供以下信息：

### 必要的信息

- **IMS 组织 ID**：您的 Adobe 组织标识符
- **项目群 ID**：您在 Adobe Experience Cloud 内的特定项目群标识符
- **项目详细信息**：时间表、范围和预期用例
- **官方工作电子邮件地址**：与您组织的 Adobe 帐户关联的地址

### 如何获取 IMS 组织 ID 和项目群 ID

有关查找 IMS 组织 ID 和项目群 ID 的详细步骤，请参阅：

- [Adobe Experience Cloud 组织设置指南](/help/onboarding/cloud-manager-introduction.md)
- [项目群和环境管理](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

### 请求访问

1. 使用上述指南收集您的 IMS 组织 ID 和项目群 ID
2. 发送电子邮件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 申请访问权限
3. 请在您的申请中提供：
   - 组织名称和 IMS 组织 ID
   - 项目群 ID
   - 项目时间线和范围
   - 预期用例和业务目标

>[!IMPORTANT]
>
> **限制提供计划**：Forms Experience Builder 的访问权限需经过内部利益相关者的审批。Adobe 将根据计划容量和是否符合早期访问标准来审核您的申请。不保证一定能通过审批，并且取决于当前计划的可用性。

有关早期访问计划及其功能的更多信息，请参阅 [AEM Forms 早期访问文档](/help/forms/early-access-ea-features.md)。

## 快速入门

要开始使用 Forms Experience Builder，请访问 [Forms Experience Builder 文档](forms-ai-assistant-getting-started.md)。您可以通过 AEM Forms 编辑器或通用编辑器访问 Forms Experience Builder，具体取决于您首选的工作流。

对于旨在转变表单创建流程的组织，Forms Experience Builder 将对话式 AI 的灵活性与企业级表单管理的稳健性相结合，是一款强大、直观的解决方案。
