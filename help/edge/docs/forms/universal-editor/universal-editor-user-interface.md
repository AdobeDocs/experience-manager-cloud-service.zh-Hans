---
title: 在AEM Forms的通用编辑器界面中导航
description: 掌握用于使用Edge Delivery Services创建AEM Forms的通用编辑器界面。 通过这份全面的界面指南了解有效构建表单所需的基本工具、快捷方式和工作流。
keywords: 通用编辑器， AEM forms， edge delivery services，界面指南，表单创作， WYSIWYG编辑器，表单生成器工具，用户界面导航
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 4%

---


# 在AEM Forms的通用编辑器界面中导航

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)提供了一个用于使用Edge Delivery Services创建AEM Forms的可视化界面。 本指南可帮助您了解用于高效构建表单的界面。

![通用编辑器界面概述](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## 概述

通用编辑器提供了一个&#x200B;**What You See Is What You Get (WYSIWYG)**&#x200B;体验，该体验向用户准确显示您的表单的显示方式。 无论您是刚开始构建团队还是经验丰富的开发人员，本指南都将帮助您：

**学习基本技能：**

- 自信而高效地浏览界面
- 使用相应的工具执行常见的表单构建任务
- 利用键盘快捷键提高工作效率
- 常见界面问题疑难解答

**主密钥工作流：**

- 设置您的工作区以获得最佳工作效率
- 从概念到发布的构建表单
- 跨设备测试和预览表单
- 与团队成员协作处理表单项目

## 快速入门

**首次用户：**&#x200B;从[基本工具](#essential-tools-for-form-building)开始，了解您最常使用的核心功能。

**经验丰富的用户：**&#x200B;跳转到[高级功能](#advanced-features-and-integrations)，以获取专门的工具和集成。

**快速参考：**&#x200B;使用[界面概述](#interface-overview)和[键盘快捷键](#keyboard-shortcuts)部分进行快速查找。

>[!NOTE]
>
> 初次进行表单创作？ 有关表单创建分步指南，请参阅[AEM FormsEdge Delivery Services快速入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)。

## 界面概述

通用编辑器界面分为四个主要区域，每个区域都针对特定任务而设计：

![通用编辑器界面布局](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **区域** | **用途** | **主要用户** |
|----------|-------------|----------------|
| **[A：Experience Cloud 标题](#experience-cloud-header)** | 导航和帐户管理 | 在Adobe工具之间切换，访问帮助，管理通知 |
| **[B：通用编辑器工具栏](#universal-editor-toolbar)** | 表单编辑和发布 | 创建、编辑、预览和发布表单 |
| **[C：属性面板](#properties-panel)** | 组件配置 | 配置表单字段、管理内容结构、访问高级功能 |
| **[D：编辑器画布](#editor-canvas)** | 可视化表单构建 | 添加组件、排列布局、查看实时预览 |

**界面流：**&#x200B;大多数用户主要在&#x200B;**编辑器画布** (D)和&#x200B;**属性面板** (C)中工作，使用&#x200B;**工具栏** (B)执行预览和发布等操作。

## 表单构建的基本工具

如果您是通用编辑器的新手，请从此处开始。 这些是您将用于大多数表单构建任务的核心工具：

### **1. 编辑器画布 — 您的主Workspace**

**编辑器画布**&#x200B;是您以可视方式构建表单的地方。 它准确地显示了您的表单在用户眼中的外观。

![编辑器画布](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**关键操作：**

- 通过单击“属性”面板中的&#x200B;**添加**&#x200B;按钮&#x200B;**添加组件**
- **通过直接在画布中单击元素来选择元素**
- 在配置组件时&#x200B;**查看实时更改**
- 在预览模式下测试&#x200B;**交互**

### **2。属性面板 — 配置组件**

**属性面板**（右侧）是您自定义选定组件和管理表单结构的位置。

![属性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**基本功能：**

- **属性模式** （`d`快捷方式） — 配置所选的组件设置
- **内容树** （`f`快捷方式） — 导航表单结构
- **添加组件** （`a`快捷方式） — 插入新表单字段
- **组件操作** — 复制或删除选定的元素

### **3。 Toolbar Essentials — 预览和发布**

**通用编辑器工具栏**&#x200B;提供了用于测试和发布表单的关键操作。

![通用编辑器工具栏](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**必须知道的工具：**

- **预览模式** （`p`快捷方式） — 测试您的表单，因为用户将看到它
- **响应模式** — 检查您的表单在移动设备上的外观
- **打开页面** （`o`快捷方式） — 在新选项卡中查看表单
- **发布** — 为用户启用表单

### **4。 快速入门工作流**

**对于您的第一个表单：**

1. **开始生成** — 使用&#x200B;**添加**&#x200B;按钮(`a`)添加组件
2. **配置字段** — 选择组件并使用&#x200B;**属性模式** (`d`)
3. **测试您的表单** — 使用&#x200B;**预览模式** (`p`)与您的表单交互
4. **检查移动视图** — 切换到&#x200B;**响应模式**&#x200B;以进行移动测试
5. **上线** — 准备就绪后单击&#x200B;**发布**

**验证检查点：**

- 能否添加和配置表单字段？
- 预览模式是否正确工作？
- 是否正确设置了所有必填字段？
- 该表单在移动设备上是否显示良好？

## Experience Cloud 标题

**Experience Cloud标头**&#x200B;提供导航和帐户管理工具。 大多数表单生成器偶尔会使用它在Adobe工具之间切换或访问帮助。

![Experience Cloud标头](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**关键元素：**

| **元素** | **用途** | **何时使用** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | 导航到其他Adobe工具 | 在站点、Assets、Forms之间切换 |
| **组织** | 在组织之间切换 | 多组织访问方案 |
| **帮助** | 访问文档和支持 | 需要指导或希望提交反馈时 |
| **通知** | 查看已分配的任务和警报 | 检查工作流状态 |
| **解决方案** | 快速访问其他Adobe解决方案 | 在不同的Adobe产品之间移动 |
| **用户轮廓** | 帐户设置和注销 | 管理帐户或切换用户 |

**最常见的用法：**

- **获取帮助** — 单击“帮助”图标获取文档和支持
- **切换组织** — 如果您有多组织访问权限，请使用组织下拉列表

## 通用编辑器工具栏

**通用编辑器工具栏**&#x200B;包含您的主要表单编辑和发布工具。 这些工作流按使用频率和典型工作流进行整理。

![通用编辑器工具栏](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **每日工作流工具**

**这些工具用于大多数表单生成会话：**

#### **预览模式** （`p`快捷方式）

**用途：**&#x200B;完全按照用户体验的方式测试您的表单\
**何时使用：**&#x200B;发布之前，在进行更改后，测试表单功能

![预览模式](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**最佳实践：**&#x200B;在每次重大更改后进行预览，以提前捕获问题。

#### **响应式模式**

**用途：**&#x200B;检查您的表单在移动设备上的显示方式\
**何时使用：**&#x200B;生成表单后，发布之前

![响应式模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**最佳实践：**&#x200B;始终测试移动设备视图 — 许多用户将访问手机上的表单。

#### **打开页面** （`o`快捷方式）

**用途：**&#x200B;在没有编辑器界面的新选项卡中查看您的表单\
**何时使用：**&#x200B;对于全屏测试，请与利益相关者共享以进行审核

    ！[打开页面](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **发布**

**用途：**&#x200B;让您的表单上线并可供用户访问\
**何时使用：**&#x200B;在预览和响应模式下进行全面测试后

    ！[发布](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

发布前&#x200B;**验证核对清单：**

- 在预览模式下测试的表单
- 已验证移动响应性
- 已配置所有必填字段
- 提交操作正确运行

### **导航工具**

#### **主页按钮**

**用途：**&#x200B;返回通用编辑器起始页\
**何时使用：**&#x200B;开始处理其他表单

![主页按钮](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **位置栏** （`l`快捷方式）

**用途：**&#x200B;通过URL直接导航到任何表单\
**何时使用：**&#x200B;在特定表单之间快速切换

![位置栏](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **高级配置工具**

**这些工具用于特定方案或高级设置：**

#### **编辑表单属性**

**用途：**&#x200B;配置表单级设置，如表单数据模型(FDM)和发布日期\
**何时使用：**&#x200B;设置数据集成，计划发布

![表单属性](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

#### **规则编辑器** （早期访问）

**用途：**&#x200B;添加动态行为、验证和条件逻辑\
**何时使用：**&#x200B;创建具有复杂业务逻辑的交互式表单

![规则编辑器](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **早期访问功能：**&#x200B;规则编辑器需要特殊访问权限。 联系[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)以启用此功能。
>
> **了解更多：**&#x200B;有关详细说明，请参阅[规则编辑器指南](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)。

#### **身份验证标头设置**

**用途：**&#x200B;设置用于开发测试的自定义身份验证标头\
**何时使用：**&#x200B;需要身份验证的表单的本地开发

![身份验证标头](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **其他选项**（省略号菜单）

**目的：**&#x200B;访问不常见的操作，如取消发布\
**何时使用：**&#x200B;脱机使用表单，访问高级选项

![其他选项](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## 属性面板

**属性面板**（右侧）是您用于构建和配置表单的控制中心。 它会根据您选择的内容进行更改，并为不同的任务提供不同的工具。

![属性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

### **核心表单生成工具**

**这些工具对于创建和组织表单至关重要：**

#### **添加组件** （`a`快捷方式）

**用途：**&#x200B;插入新表单域和元素\
**工作方式：**&#x200B;显示所选容器的可用组件

![添加组件](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**常用组件：**

- 文本输入、电子邮件、电话字段
- 下拉列表、单选按钮、复选框
- 文件上传，日期选取器
- 组织的面板和节

#### **属性模式** （`d`快捷方式）

**用途：**&#x200B;配置选定组件的设置\
**何时使用：**&#x200B;添加任何组件以自定义其行为后

![属性模式](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**键设置：**

- 字段标签和占位符文本
- 验证规则（必需、格式、长度）
- 默认值和帮助文本
- 条件可见性规则

#### **内容树** （`f`快捷方式）

**用途：**&#x200B;导航并组织您的表单结构\
**何时使用：**&#x200B;包含多个分区的复杂表单，查找特定组件

![内容树](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**福利：**

- 快速导航到任何组件
- 可视化表单层次结构
- 轻松对元素重新排序

#### **组件操作**

**用途：**&#x200B;管理现有组件\
**可用操作：**

- **复制** — 快速复制组件![复制](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **删除** — 删除组件（无确认提示）![删除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **高级功能和集成**

**这些工具支持复杂的表单功能：**

+++数据集成

#### **数据源**

**用途：**&#x200B;将表单连接到后端数据系统\
**何时使用：**&#x200B;需要读/写数据库或外部服务的Forms

![数据源](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**功能：**

- 表单数据模型(FDM)配置
- 动态数据群体
- 提交到外部系统

+++

+++AI支持的工具

#### **生成变体**

**用途：**&#x200B;使用AI创建不同版本的表单内容\
**何时使用：**&#x200B;试验不同的文本、布局或方法

    ！[生成变体](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**了解更多：** [生成变体指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **内容草稿**

**用途：**&#x200B;创建和保存初步文本版本\
**何时使用：**&#x200B;对表单副本进行迭代，保存替换文本选项

![内容草稿](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++测试和优化

#### **A/B 测试**

**用途：**&#x200B;比较表单变体以优化性能\
**何时使用：**&#x200B;优化转化率，测试不同的设计

![A/B 测试](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **试验**

**用途：**&#x200B;对窗体设计运行受控测试\
**何时使用：**&#x200B;数据驱动表单优化、用户体验测试

    ！[试验](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Collaboration工具

#### **任务管理**

**目的：**&#x200B;组织表单项目的团队工作流\
**何时使用：**&#x200B;多人表单开发、项目跟踪

![任务管理](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **个性化**

**用途：**&#x200B;与Adobe Experience Platform连接以提供量身定制的体验\
**何时使用：**&#x200B;根据用户数据创建个性化表单

    ！[Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## 编辑器画布

**编辑器画布**&#x200B;是您在其中可视化构建表单的主工作区。 它准确地向用户显示您的表单的显示方式，并在您进行更改时提供实时反馈。

![编辑器画布](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**主要功能：**

- **WYSIWYG编辑** — 在进行更改时立即查看更改
- **直接交互** — 单击任何组件以将其选中并进行编辑
- **实时预览** — 切换到预览模式以测试功能
- **响应式显示** — 切换设备视图以检查移动设备兼容性

**最佳实践：**

- **从结构开始** — 在详细组件之前添加主要部分
- **经常测试** — 定期使用预览模式提前发现问题
- **考虑移动优先** — 在整个设计过程中检查响应模式

## 键盘快捷键

掌握这些快捷方式可更快、更高效地构建表单：

| **快捷方式** | **操作** | **何时使用** |
|--------------|------------|----------------|
| `a` | 打开组件列表 | 添加新表单字段 |
| `d` | 打开组件属性 | 配置所选元素 |
| `f` | 切换内容树 | 导航复杂表单 |
| `p` | 切换预览模式 | 测试表单功能 |
| `o` | 在新选项卡中打开表单 | 全屏测试 |
| `l` | 焦点位置栏 | 切换到不同的表单 |

**专业提示：**&#x200B;组合使用这些快捷方式 — 例如，选择组件，按`d`进行配置，然后按`p`测试更改。

## 常见工作流

### **创建您的第一个表单**

1. **添加结构** — 使用`a`为表单部分添加面板
2. **添加字段** — 插入文本输入、电子邮件和其他组件
3. **配置属性** — 选择每个字段并按`d`设置标签和验证
4. **测试功能** — 按`p`预览和测试表单
5. **检查移动视图** — 使用响应模式验证移动显示
6. **发布** — 准备上线时单击“发布”

### **编辑现有的Forms**

1. **导航结构** — 使用内容树(`f`)快速查找组件
2. **选择并修改** — 直接单击组件或使用内容树
3. **测试更改** — 每次重大更改后预览(`p`)
4. **验证工作流** — 在重新发布之前测试完整的表单流程

### **与团队协作**

1. **使用任务管理** — 将特定表单分区分配给团队成员
2. **共享以供审阅** — 使用打开页面(`o`)共享干净预览
3. **一起测试** — 使用预览模式进行协作测试会话
4. **跟踪进度** — 检查任务更新的通知

## 常见问题疑难解答

### **接口问题**

+++接口元素未加载

**问题：**&#x200B;工具栏按钮、属性面板或其他界面元素未显示

**解决方案：**

- **刷新页面** — 简单的浏览器刷新通常可以解决加载问题
- **检查浏览器兼容性** — 使用Chrome、Firefox或Safari
- **清除浏览器缓存** — 移除可能已过期的缓存文件
- **验证权限** — 确保您具有编辑表单的正确访问权限

+++

+++组件没有响应

**问题：**&#x200B;无法选择组件或属性面板未更新

**解决方案：**

- **直接单击组件** — 避免单击空区域
- **使用内容树** — 按`f`并从树中选择组件
- **检查重叠的元素** — 某些组件可能阻止了其他组件
- **重新加载表单** — 使用位置栏(`l`)重新加载当前表单

+++

+++预览模式问题

**问题：**&#x200B;预览模式无法正常工作或显示错误

**解决方案：**

- **检查表单验证** — 确保所有必填字段均已正确配置
- **首先在编辑模式下测试** — 在预览之前验证组件是否正常工作
- **清除浏览器缓存** — 缓存的脚本可能会干扰预览
- **检查组件配置** — 查看属性模式设置以查找错误

+++

## 高效表单构建的最佳实践

### **组织提示**

- **使用描述性名称** — 在属性模式下清楚地标记组件
- **分组相关字段** — 使用面板以逻辑方式组织表单节
- **在生成之前进行规划** — 在开始之前草图您的窗体结构
- **保持简单** — 避免用户过多填写字段

### **性能优化**

- **最小化组件** — 仅使用必要的表单字段
- **优化图像** — 压缩表单中使用的任何图像
- **在移动设备上测试** — 确保在速度较慢的移动设备连接上获得良好的性能
- **提前验证** — 设置正确的验证以防止提交错误

### **用户体验**

- **经常测试** — 在每次主要更改后使用预览模式
- **像用户一样思考** — 考虑完整的表单填写体验
- **提供清晰的标签** — 让用户能够清楚地了解字段目的
- **添加有用的文本** — 为复杂字段使用帮助文本

## 后续步骤

现在您已了解通用编辑器界面：

1. **使用简单表单进行练习** — 从基本字段开始练习，以舒服起见
2. **探索高级功能** — 准备就绪后尝试人工智能支持的工具和集成
3. **学习表单创作** — 请参阅[入门指南](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **主规则编辑器** — 使用[规则编辑器指南](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)添加动态行为

**请记住：**&#x200B;通用编辑器旨在使窗体生成变得直观。 从基本功能开始，随着需求的增长，逐步探索高级功能。

