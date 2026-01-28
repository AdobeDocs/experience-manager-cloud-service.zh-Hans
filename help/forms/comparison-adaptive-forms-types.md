---
title: 自适应Forms核心组件与Edge Delivery Services Forms与基础组件
description: 对AEM Forms创作方法(核心组件、Edge Delivery Services Forms和基础组件)进行技术比较。 架构、渲染、功能和用例。
keywords: 自适应表单比较，核心组件， foundation组件， edge delivery services forms， AEM forms比较，表单生成器比较
role: Architect, Developer, Admin
level: Intermediate
feature: Adaptive Forms, Core Components, Edge Delivery Services
exl-id: adaptive-forms-comparison
source-git-commit: 37799555babb15809409ec5cda8a1c46ceff24f2
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 9%

---


# 自适应Forms：核心组件与Edge Delivery Services Forms与基础组件

Adobe Experience Manager (AEM) Forms提供了三种截然不同的方法来构建数据捕获体验：基于核心组件的自适应Forms、Edge Delivery Services Forms和基于基础组件的自适应Forms。 每种方法都有不同的体系结构、渲染模型和目标用例。 本文提供了技术比较，以帮助解决方案架构师、开发人员和AEM客户为其需求选择适当的方法。

## 概述

所有这三种表单类型都用于捕获用户数据并与后端系统集成。 但是，它们在底层架构中有所不同，这些架构呈现表单的位置、提供表单的方式以及支持的功能都是不同的。

| 方法 | 状态 | 主要用例 |
|----------|--------|------------------|
| **核心组件** | 为新表单推荐 | 现代、可扩展的表单，需要具有灵活发布选项的AEM创作 |
| **Edge Delivery Services Forms** | 建议用于性能关键型站点 | 通过快速部署从边缘交付高性能表单 |
| **基础组件** | 维护模式 | 需要旧版功能支持的现有表单 |

## 基于核心组件的自适应Forms

### 定义

自适应Forms核心组件是基于Adobe Experience Manager WCM核心组件构建的30个开源、符合BEM标准的组件。 它们代表了Adobe创建新的自适应Forms的建议方法，可提供现代架构、改进的性能和自动Headless表单生成。

### 架构

核心组件使用标准化的模块化组件架构：

- **组件基础**：基于AEM WCM核心组件构建
- **样式设置方法**： BEM （块元素修饰符） CSS约定
- **内容存储**：具有结构化内容节点的JCR存储库
- **呈现**： AEM中的服务器端呈现，带有可选的客户端Headless呈现
- **Source**：开放源代码（在[GitHub](https://github.com/adobe/aem-core-forms-components)上提供）

### 渲染模型

核心组件支持多种渲染模型：

1. **服务器端渲染(SSR)**： Forms在AEM服务器上渲染，并将完整的HTML交付给浏览器
2. **Headless呈现**： Forms通过API公开JSON呈现，以便在React、Angular或其他框架中进行客户端呈现
3. **混合渲染**：服务器和客户端渲染的组合以实现最佳性能

### 发布选项

- AEM发布实例
- Edge Delivery Services（配置时）
- 用于自定义前端应用程序的Headless API

### 主要功能

| 类别 | 功能 |
|----------|-------------|
| **组件** | 30个标准化组件，包括文本框、数字框、日期选取器、下拉列表、复选框组、单选按钮、文件附件、向导、折叠面板、水平/垂直选项卡 |
| **表单模型** | JSON Schema （v4和2020-12）、表单数据模型(FDM)、XDP/XFA模板（有限） |
| **规则引擎** | 具有条件逻辑、验证、服务调用和自定义函数的可视化规则编辑器 |
| **提交操作** | REST端点、电子邮件、AEM Workflow、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion、表单数据模型 |
| **预填充** | 表单数据模型预填充服务，自定义预填充服务 |
| **验证码** | reCAPTCHA， hCaptcha， Turnstile |
| **记录文档** | 使用自定义或OOTB模板生成PDF |
| **辅助功能** | 符合WCAG，ARIA标签，键盘导航，屏幕阅读器支持 |
| **本地化** | 通过AEM翻译工作流提供多语言支持 |
| **版本控制** | 从AEM Sites继承的内容版本控制 |

### 先决条件

- **AEM Forms as a Cloud Service**：默认启用核心组件
- **AEM 6.5 Forms**：需要通过AEM原型启用
- **用户权限**：用户必须位于`forms-users`组中
- **模板**：需要自适应表单（核心组件）模板
- **主题**：画布主题(OOTB)或自定义主题

### 限制

- **JSON架构约束**：不支持Null类型、联合类型（任意）、OneOf/AnyOf/AllOf/NOT构造
- **组件间隙**： Adobe Sign块、涂写签名、图表、图像选择不可用（在Foundation组件中可用）
- **自定义函数**：生成器函数、异步/等待、不支持类方法
- **数字签名**：本地不可用（与基础组件不同）

### 使用时间

**推荐用于：**

- 新表单开发项目
- 需要现代、可维护的架构的组织
- 需要灵活发布的项目(AEM + Edge Delivery + Headless)
- 通过Headless API自定义前端应用程序(React、Angular)
- 优先考虑性能和辅助功能的项目
- 全渠道交付要求（Web、移动设备、网亭）

**不推荐用于：**

- 需要Adobe Sign集成的Forms（使用基础组件）
- Edge Delivery Services性能至关重要的简单表单
- 基于现有基础组件的表单（除非迁移，否则在Foundation中维护）

## Edge Delivery Services Forms

### 定义

Edge Delivery Services (EDS) Forms是一套可组合的服务，通过Adobe Experience Manager Edge Delivery Services创建和提交表单。 它们通过基于边缘的交付、客户端渲染和多种创作方法，实现了具有卓越性能的快速表单开发。

### 架构

EDS Forms使用分离的、边缘优先的体系结构：

- **内容源**： Microsoft SharePoint、Google Drive (Document-Based)或通用编辑器(WYSIWYG)
- **代码存储库**： GitHub
- **内容投放**： Edge Delivery Services CDN
- **呈现**：使用vanilla JavaScript的客户端呈现
- **表单块**：自适应Forms块处理表单定义并生成HTML

### 渲染模型

EDS Forms专门使用客户端渲染：

1. 表单定义存储为JSON（从电子表格转换或在通用编辑器中创作）
2. 从边缘获取的JSON： `https://<branch>--<repo>--<owner>.aem.live/<form>.json`
3. 自适应Forms阻止JavaScript流程JSON
4. 在浏览器中动态生成的HTML结构
5. 应用于样式的CSS

**HTML结构模式：**

```html
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required="{Required}">
   <label for="{FieldId}" class="field-label">Label</label>
   <input type="{Type}" id="{FieldId}" name="{Name}">
   <div class="field-description" id="{FieldId}-description">Help text</div>
</div>
```

### 创作方法

EDS Forms支持两种创作方法：

####  Universal Editor （所见即所得）

- 可视化拖放界面
- 使用设备模拟的实时预览
- 条件逻辑的高级规则编辑器
- 表单数据模型(FDM)集成
- AEM工作流集成
- 自定义组件支持
- 基于模板的创建

#### 基于文档的创作

- Microsoft Excel或Google工作表创作
- 基于电子表格的表单定义
- 即时发布（更改会立即反映）
- 适用于简单到中等复杂形式

### 提交选项

**Forms提交服务(FSS)：**

- 提交到Google工作表
- 提交到Microsoft Excel (OneDrive/SharePoint)
- 电子邮件通知

**AEM发布提交操作：**

- REST端点
- AEM邮件服务
- 表单数据模型
- AEM 工作流程
- SharePoint/OneDrive
- Azure Blob存储
- Microsoft Power Automate
- Adobe Workfront Fusion
- Adobe Marketo Engage

### 主要功能

| 类别 | 功能 |
|----------|-------------|
| **组件** | 所有HTML5输入类型、复选框组、单选按钮组、下拉列表、面板、可重复部分、文件附件、折叠面板、向导、模态 |
| **验证** | 字段级验证（必需、最小/最大、模式）、自定义验证消息 |
| **规则** | 条件可见性、值表达式、事件驱动规则 |
| **集成** | Adobe Sign、Salesforce、Microsoft Dynamics、A/B测试 |
| **安全性** | reCAPTCHA Enterprise、hCaptcha、CORS配置 |
| **分析** | Adobe Experience Platform Web SDK、表单视图和提交跟踪 |

### 先决条件

基于文档的创作的&#x200B;**：**

- GitHub帐户
- Google Drive或Microsoft SharePoint帐户
- 用于本地开发的Node/npm
- 配置了自适应Forms块的AEM项目
- 与`forms@adobe.com`共享文件夹（编辑权限）

通用编辑器的&#x200B;**：**

- AEM Forms as a Cloud Service 实例
- 已配置的 Edge Delivery Services 项目
- 目标目标所需的权限

用于AEM发布提交的&#x200B;**：**

- 已配置AEM云服务实例URL
- OSGi引用过滤器配置
- Edge Delivery站点域的CORS配置

### 限制

**基于文档的创作：**

- 工作表命名限制为`helix-default`和`shared-aem`
- 最适合低复杂性表单
- 有限的规则功能
- 无AEM工作流(不提交AEM Publish)
- 无表单数据模型集成

**通用编辑器：**

- 自定义函数不支持静态/动态导入
- 表单片段只能独立编辑
- 开发中的表单嵌入功能

**常规：**

- `shared-aem`工作表不应包含PII（可公开访问）
- 跨源提交需要CORS配置
- AEM发布提交需要OSGi反向链接过滤器

### 使用时间

**推荐用于：**

- 需要高Lighthouse分数的性能关键型网站
- 已在使用Edge Delivery Services的站点
- 快速表单开发和部署
- 简单到中等复杂度的数据捕获
- 团队更喜欢基于电子表格的创作（基于文档）
- 需要快速上市的项目

**不推荐用于：**

- Forms需要广泛的服务器端处理
- 与缺少REST API的旧版系统深度集成
- 离线表单要求
- 需要具有完全控制的特定JavaScript框架(React、Angular)的组织

## 基于基础组件的自适应Forms

### 定义

基础组件代表着经典的AEM Forms创作方法。 它们是AEM Forms中已经存在多年的原始自适应Forms组件。 虽然仍受支持，但Adobe建议使用基础组件主要维护现有表单，而不是创建新表单。

### 架构

基础组件使用传统的AEM架构：

- **内容模型**：具有JCR内容结构的WCM `cq:Page`组件
- **根结构**： `guideContainer` （根） → `rootPanel` → `items` （表单字段）
- **呈现**：使用客户端JavaScript进行服务器端呈现
- **SOM表达式**：正在编写用于引用表单对象的对象模型的脚本

### 渲染模型

基础组件使用服务器端渲染：

1. 表单内容存储在JCR存储库中
2. AEM服务器进程窗体结构
3. 完整呈现并发送到浏览器的HTML
4. 客户端JavaScript处理交互和验证

### 主要功能

| 类别 | 功能 |
|----------|-------------|
| **组件** | 40多个组件（包括所有核心组件等效组件）以及：Adobe Sign Block、图表、涂写签名、图像选择、摘要步骤、文件附件列表 |
| **表单模型** | 表单数据模型(FDM)、XDP/XFA模板、XML架构(XSD)、JSON架构 |
| **规则引擎** | 可视编辑器+代码编辑器（用于表单超级用户组） |
| **数字签名** | Adobe Sign集成，涂写签名 |
| **提交操作** | 多个OOTB操作与核心组件类似 |

### Foundation专有的组件

以下组件在Foundation组件中仅&#x200B;**可用**：

- Adobe Sign Block
- 图表
- 文件附件列表
- 脚注占位符
- 图像选择
- 潦草签名
- 摘要步骤
- Turnstile 验证码

### 先决条件

- AEM Forms as a Cloud Service或AEM 6.5 Forms
- 自适应表单模板(Foundation)
- `forms-users`组中的用户

### 限制

- **发布**：仅限AEM(无Edge Delivery Services或Headless API)
- **性能**：标准性能（未针对Lighthouse分数进行优化）
- **架构**：不符合BEM的旧版架构
- **打开Source**：不是开源
- **未来开发**：维护模式；新功能主要添加到核心组件

### 使用时间

**推荐用于：**

- 维护现有的基于Foundation的表单
- 需要Adobe Sign或涂写签名集成的Forms
- 依赖于已建立的基础功能的工作流
- 具有仅AEM发布要求的项目
- Forms需要Foundation专用组件（图表、图像选择）

**不推荐用于：**

- 新表单开发（使用核心组件）
- 需要Edge Delivery Services发布的项目
- Headless表单API
- 关键性能实施
- 优先考虑面向未来架构的项目

## 比较表

| 参数 | 核心组件 | Edge Delivery Services Forms | Foundation 组件 |
|-----------|-----------------|-----------------------------|-----------------------|
| **状态** | 为新表单推荐 | 推荐用于高性能站点 | 维护模式 |
| **架构** | 模块化、符合BEM | Edge优先，分离 | 传统WCM |
| **正在呈现** | 服务器端+ Headless | 仅客户端 | 服务器端 |
| **正在发布** | AEM + Edge Delivery + Headless API | 仅 Edge Delivery Services | 仅限 AEM |
| **创作** | AEM Forms 编辑器 | 通用编辑器或电子表格 | AEM Forms 编辑器 |
| **性能** | 良好（比Foundation改进） | 优秀（Lighthouse得分较高） | 标准 |
| **组件计数** | 30 | 20+(所有HTML5输入类型) | 40+ |
| **打开Source** | 是(GitHub) | 是 | 否 |
| **表单数据模型** | ✅ | ✅ （仅限通用编辑器） | ✅ |
| **JSON架构** | ✅ | 有限制 | ✅ |
| **XDP/XFA支持** | 有限制 | ❌ | ✅ |
| **XML架构** | ❌ | ❌ | ✅ |
| **规则引擎** | 高级可视编辑器 | 高级（通用编辑器）/有限（基于文档） | 高级可视化+代码编辑器 |
| **数字签名** | ❌ | ❌ | ✅ |
| **Adobe Sign** | ❌ | 通过集成 | ✅ （本机块） |
| **记录文档** | ✅ | ✅ | ✅ |
| **验证码选项** | reCAPTCHA、hCaptcha | reCAPTCHA Enterprise、hCaptcha | reCAPTCHA， hCaptcha， Turnstile |
| **AEM工作流** | ✅ | ✅ (通过AEM发布) | ✅ |
| **Headless API** | ✅ （自动） | ❌ | ❌ |
| **辅助功能** | 符合WCAG | 符合WCAG | 基本 |
| **部署速度** | 基于管道 | 即时（提交到实时） | 基于管道 |
| **样式** | BEM CSS，主题 | CSS，项目级主题 | CSS，主题 |
| **版本控制** | ✅ （继承自站点） | 基于Git | ✅ |
| **本地化** | AEM翻译工作流 | 手动/AEM Sites工作流程 | AEM翻译工作流 |

## 决策矩阵

| 要求 | 推荐的方法 |
|-------------|---------------------|
| 新表单开发 | 核心组件 |
| 维护现有表单 | 基础组件（迁移之前） |
| 性能关键（Lighthouse得分较高） | Edge Delivery Services Forms |
| Headless/全渠道投放 | 核心组件 |
| Adobe Sign集成 | Foundation 组件 |
| 基于电子表格的创作 | Edge Delivery Services（基于文档） |
| 通过Edge交付进行可视化WYSIWYG创作 | Edge Delivery Services（通用编辑器） |
| 复杂的企业集成 | 核心组件或基础组件 |
| 快速原型 | Edge Delivery Services（基于文档） |
| XFA/XDP模板支持 | Foundation 组件 |
| 自定义React/Angular前端 | 核心组件(Headless API) |

## 迁移注意事项

### 基础组件到核心组件

- **工具**： AEM现代化工具(Forms转化实用程序)
- **工作量**：中高取决于表单复杂性
- **注意事项**：
   - 规则需要手动重新创建
   - 基础独有的组件（Adobe Sign块、涂写签名、图表）在迁移期间被删除
   - 翻译设置未延续
   - 自定义函数需要重写

### 传统到Edge Delivery Services

- **方法**：使用通用编辑器或基于文档的创作重新生成表单
- **工作量**：对于复杂表单为高，对于简单表单为低
- **优点**：显着提高了性能，具有现代开发经验

## 文档缺口和含糊不清

以下区域的文档不完整或不明确：

1. **核心组件XDP/XFA支持**：文档指示支持“有限”，但未指定确切限制
2. **Edge Delivery Services表单嵌入**：在文档中标记为“即将推出”；当前状态不清楚
3. **基础组件将来**：没有明确的弃用时间表；描述为“维护模式”
4. **Headless API覆盖范围**：未记录服务器渲染表单和Headless表单之间的精确功能对等性
5. **性能基准**：未提供方法之间的特定Lighthouse得分比较

## 相关资源

- [创建自适应表单（核心组件）](/help/forms/creating-adaptive-form-core-components.md)
- [创建自适应表单（基础组件）](/help/forms/creating-adaptive-form.md)
- [Edge Delivery Services Forms概述](/help/edge/docs/forms/overview.md)
- [通用编辑器快速入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
- [基于文档的创作教程](/help/edge/docs/forms/tutorial.md)
- [迁移实用程序工具](/help/forms/migration-utility-tool-for-af-core-components.md)
- GitHub上的[AEM Forms核心组件](https://github.com/adobe/aem-core-forms-components)
