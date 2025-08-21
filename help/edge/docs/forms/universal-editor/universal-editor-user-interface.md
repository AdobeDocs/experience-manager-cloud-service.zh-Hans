---
title: 导航 AEM Forms 的通用编辑器界面
description: 掌握如何使用通用编辑器界面通过 Edge Delivery Services 创建 AEM Forms。通过此综合界面指南了解基本工具、快捷方式和工作流程，以高效构建表单。
keywords: 通用编辑器、AEM Forms、edge delivery services、界面指南、表单创作、所见即所得编辑器、表单构建器工具、用户界面导航
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '2355'
ht-degree: 90%

---


# 导航 AEM Forms 的通用编辑器界面

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)提供了一个可视界面，用于通过 Edge Delivery Services 创建 AEM Forms。它提供了一种&#x200B;**What You See Is What You Get (WYSIWYG)**&#x200B;体验，可向用户准确显示您的表单的显示方式。

![通用编辑器界面概述](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

本指南可帮助您了解用于高效构建表单的界面。 无论您是表单构建新手还是经验丰富的开发人员，本指南都将帮助您：

**了解基本技能：**

- 充满信心地高效导航界面
- 使用适当的工具完成常见的表单构建任务
- 使用键盘快捷键提高工作效率
- 解决常见的界面问题

**主要工作流：**

- 设置您的工作区，以达到最佳工作效率
- 从设计理念到发布的整个表格构建
- 跨设备测试和预览表单
- 与团队成员协作，完成表单项目



## 快速入门

**首次使用者：**&#x200B;从[基本工具](#essential-tools-for-form-building)开始了解您将最常用到的核心功能。

**经验丰富的用户：**&#x200B;跳至[高级功能](#advanced-features-and-integrations)，了解专门的工具和集成。

**快速参考：**&#x200B;使用[界面概述](#interface-overview)和[键盘快捷键](#keyboard-shortcuts)部分，以便快速查找。

>[!NOTE]
>
> 您是表单创作新手？请参见[开始使用 Edge Delivery Services 创建 AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)，获得表单创建分步指导。

## 界面概述

通用编辑器界面分为四个主要区域，每个区域都专门用于特定的任务：

![通用编辑器界面布局](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **区域** | **用途** | **主要用途** |
|----------|-------------|----------------|
| **[A：Experience Cloud 标题](#experience-cloud-header)** | 导航和帐户管理 | 在 Adobe 工具之间切换、访问帮助、管理通知 |
| **[B：通用编辑器工具栏](#universal-editor-toolbar)** | 编辑与发布表单 | 创建、编辑、预览和发布表单 |
| **[C：属性面板](#properties-panel)** | 组件配置 | 配置表单字段、管理内容结构、访问高级功能 |
| **[D：编辑器画布](#editor-canvas)** | 视觉表单构建 | 添加组件、安排布局、查看实时预览 |

**界面流程：**&#x200B;大多数用户主要在&#x200B;**编辑器画布**（D）和&#x200B;**属性面板**（C）中工作，使用&#x200B;**工具栏**（B）执行预览和发布等操作。

## 表单构建的基本工具

如果您是使用通用编辑器的新手，请从这里开始。这些是您在大多数表单构建任务中会用到的核心工具：

### **1. 编辑器画布 - 您的主要工作区**

**编辑器画布**&#x200B;是您以可视化方式构建表单的地方。它准确地展示了您的表单将如何显示给用户。

![编辑器画布](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**关键操作：**

- **添加组件**：点击属性面板中的&#x200B;**添加**&#x200B;按钮
- **选择元素**：在画布上直接点击需要的元素
- 配置组件时&#x200B;**查看实时变化**
- 在预览模式下&#x200B;**测试交互情况**

### **2。属性面板 - 配置您的组件**

**属性面板**（右侧）是您自定义选定组件和管理表单结构的地方。

![属性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**主要功能：**

- **属性模式**（`d`快捷键）- 配置选定的组件设置
- **内容树**（`f` 快捷键）- 导航表单结构
- **添加组件**（`a` 快捷键）- 插入新的表单字段
- **组件操作** - 复制或删除选定的元素

### **3. 工具栏概要 - 预览和发布**

**通用编辑器工具栏**&#x200B;提供了用于测试和发布表单的关键操作。

![通用编辑器工具栏](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**必须了解的工具：**

- **预览模式**（`p` 快捷键）- 按照用户将看到的情况测试您的表单
- **响应模式** - 检查您的表单在移动设备上的显示情况
- **打开页面**（`o` 快捷键）- 在新选项卡中查看表单
- **发布** - 将表单上线，让用户访问

### **4. 快速入门工作流**

**为您的第一个表单：**

1. **开始构建** - 通过&#x200B;**添加**&#x200B;按钮 (`a`) 添加组件
2. **配置字段** - 选择组件，使用&#x200B;**属性模式** (`d`)
3. **测试您的表单** - 使用&#x200B;**预览模式** (`p`) 与您的表单进行交互
4. **检查移动设备视图** - 切换到&#x200B;**响应模式**&#x200B;进行移动设备测试
5. **上线** - 准备就绪后，点击&#x200B;**发布**

**验证检查点：**

- 您可以添加和配置表单字段吗？
- 预览模式是否正常工作？
- 是否正确设置了所有必填字段？
- 表单在移动设备上是否正常显示？

## Experience Cloud 标题

**Experience Cloud 标题**&#x200B;提供导航和帐户管理工具。大多数表单构建者偶尔会使用它在 Adobe 工具之间切换或者访问帮助功能。

![Experience Cloud 标题](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**关键元素：**

| **元素** | **用途** | **何时使用** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | 导航至其他 Adobe 工具 | 在 Sites、Assets、Forms 之间切换 |
| **组织** | 在组织之间切换 | 多组织访问场景 |
| **帮助** | 访问文档和支持 | 当您需要指导或者要提交反馈时 |
| **通知** | 查看已分配的任务和警报 | 检查工作流状态 |
| **解决方法** | 快速访问其他 Adobe 解决方案 | 在不同的 Adobe 产品之间移动 |
| **用户轮廓** | 帐户设置和退出登录 | 管理帐户或切换用户 |

**最常见的用途：**

- **获取帮助** - 点击“帮助”图标获取文档和支持
- **切换组织** - 如果您拥有多组织访问权限，请使用“组织”下拉列表

## 通用编辑器工具栏

**通用编辑器工具栏**&#x200B;包含主要的表单编辑和发布工具。这些工具按照使用频率和典型工作流排列。

![通用编辑器工具栏](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **日常工作流工具**

**大多数表单构建过程中都要使用这些工具：**

#### **预览模式**（`p` 快捷键）

**用途：**&#x200B;按照用户体验准确测试表单\
**何时使用：**&#x200B;发布前和更改后，用于测试表单功能

![预览模式](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**最佳实践：**&#x200B;每次重大更改后进行预览，以便尽早发现问题。

#### **响应式模式**

**用途：**&#x200B;检查表单在移动设备上的显示情况\
**何时使用：**&#x200B;表单构建之后，发布之前

![响应式模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**最佳实践：**&#x200B;始终测试移动设备视图 - 许多用户会在手机上访问表单。

#### **打开页面**（`o` 快捷键）

**用途：**&#x200B;在新选项卡中查看表单，无需编辑器界面\
**何时使用：**&#x200B;用于全屏测试，与利益相关者共享以进行审阅

![打开页面](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **发布**

**用途：**&#x200B;将您的表单上线，让用户访问\
**何时使用：**&#x200B;在预览和响应模式下进行全面测试之后

![发布](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

**发布前的验证清单：**

- 已在预览模式下测试了表单
- 已验证移动设备上的响应能力
- 配置了所有必填字段
- 提交操作正常运行

### **导航工具**

#### **主页按钮**

**用途：**&#x200B;返回到通用编辑器开始页面\
**何时使用：**&#x200B;开始在另一个表单上工作

![主页按钮](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **位置栏**（`l` 快捷键）

**用途：**&#x200B;通过 URL 直接导航到任何表单\
**何时使用：**&#x200B;在特定表单之间快速切换

![位置栏](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **高级配置工具**

**这些工具用于一些特定场景或高级设置：**

#### **AEM表单属性**

**用途：**&#x200B;配置表单级别的设置，例如表单数据模型 (FDM) 和发布日期\
**何时使用：**&#x200B;设置数据集成、安排发布时间

![表单属性](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

![表单属性向导](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

“表单属性”面板包括以下部分：

- **提交**：定义用户提交表单后发生的情况。 从多个提交操作中进行选择，例如通过电子邮件发送数据，提交到SharePoint，使用表单数据模型，或与Adobe Experience Platform或Microsoft Power Automate等服务集成。 有关支持的提交操作的完整列表，请参阅[提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)文章。

- **预填充**：配置在用户与表单交互之前自动填充表单字段的方式。 您可以连接到表单数据模型(FDM)等数据源，或使用URL参数预填充字段，从而增强用户体验并减少手动输入。 若要了解详细信息，请参阅[预填充服务](/help/edge/docs/forms/universal-editor/prefill-form.md)文章。

- **谢谢**：自定义提交表单后用户看到的内容。 您可以显示确认消息或将它们重定向到其他网页，以确保流畅而专业的完成体验。 要了解如何为表单配置感谢消息，请参阅[配置感谢消息](/help/edge/docs/forms/universal-editor/configure-thankyou-message.md)文章。

#### **规则编辑器**（早期访问）

**用途：**&#x200B;添加动态行为、验证和条件逻辑\
**何时使用：**&#x200B;创建具有复杂业务逻辑的交互式表单

![规则编辑器](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **早期访问功能：**&#x200B;规则编辑器需要专门的访问权限。联系 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，以启用此功能。
>
> **了解详情：**&#x200B;请参阅[规则编辑器指南](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)，获取详细说明。

#### **身份验证标头设置**

**用途：**&#x200B;设置自定义身份验证标头，用于开发测试\
**何时使用：**&#x200B;本地开发需要身份验证的表单时

![身份验证标头](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **附加选项**（省略号菜单）

**用途：**&#x200B;访问不太常用的操作，例如取消发布\
**何时使用：**&#x200B;将表单离线，访问高级选项

![其他选项](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## 属性面板

**属性面板**（右侧）是您构建和配置表单的控制中心。它会根据您的选择而变化，为不同的任务提供不同的工具。

![属性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

### **核心表单构建工具**

**这些工具对于创建和组织表单至关重要：**

#### **添加组件**（`a` 快捷键）

**用途：**&#x200B;插入新的表单字段和元素\
**方式：**&#x200B;显示选定容器的可用组件

![添加组件](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**常用组件：**

- 文本输入、电子邮件、电话字段
- 下拉菜单、单选按钮、复选框
- 文件上传、日期选取器
- 用于组织内容的面板和分区

#### **属性模式**（`d` 快捷键）

**用途：**&#x200B;配置选定组件的设置\
**何时使用：**&#x200B;在添加任何组件之后，用于自定义其行为

![属性模式](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**关键设置：**

- 字段标签和占位符文本
- 验证规则（必填项、格式、长度）
- 默认值和帮助文本
- 有条件的可见性规则

#### **内容树**（`f` 快捷键）

**用途：**&#x200B;导航和组织您的表单结构\
**何时使用：**&#x200B;包含多个分区的复杂表单，用于查找特定组件

![内容树](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**优势：**

- 快速导航至任何组件
- 视觉上的表单层级结构
- 轻松地将元素重新排序

#### **组件操作**

**用途：**&#x200B;管理现有组件\
**可用的操作：**

- **复制** - 快速复制组件 ![复制](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **删除** - 删除组件（无确认提示）![删除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **高级功能和集成**

**这些工具可实现复杂的表单功能：**

+++数据集成

#### **数据源**

**用途：**&#x200B;将表单与后端数据系统连接\
**何时使用：**&#x200B;需要读取/写入数据库或外部服务的表单

![数据源](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**功能：**

- 表单数据模型（FDM）配置
- 动态数据填充
- 提交至外部系统

+++

+++AI支持的工具

#### **生成变体**

**用途：**&#x200B;使用 AI 创建不同版本的表单内容\
**何时使用：**&#x200B;试验不同的文本、布局或方法

    ![生成变体](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**了解详情：**[生成变体指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **内容草稿**

**用途：**&#x200B;创建并保存初版文本\
**何时使用：**&#x200B;迭代表单副本，保存替换文本选项

![内容草稿](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++测试和优化

#### **A/B 测试**

**用途：**&#x200B;比较不同的表单变体，以优化性能\
**何时使用：**&#x200B;优化转化率，测试不同的设计

![A/B 测试](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **试验**

**用途：**&#x200B;对不同的表单设计进行控制测试\
**何时使用：**&#x200B;以数据驱动方法优化表单，测试用户体验

    ![试验](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Collaboration Tools

#### **任务管理**

**用途：**&#x200B;为表单项目组织团队工作流\
**何时使用：**&#x200B;多人表单开发，项目跟踪

![任务管理](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **个性化**

**用途：**&#x200B;与 Adobe Experience Platform 连接，以获得定制体验\
**何时使用：**&#x200B;根据用户数据创建个性化表单

    ![个性化](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## 编辑器画布

**编辑器画布**&#x200B;是您以可视化方式构建表单的主要工作区。 它准确地展示了您的表单将如何显示给用户，并在您进行更改时提供实时反馈。

![编辑器画布](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**主要功能：**

- **所见即所得编辑方法** - 您做的更改可以立即看到
- **直接交互** - 点击任意组件即可选择并编辑该组件
- **实时预览** - 切换到预览模式以测试功能
- **自适应显示** - 切换设备视图，以检查移动设备兼容性

**最佳实践：**

- **从结构开始** - 在详细说明组件之前添加主要分区
- **经常测试** - 定期使用预览模式，及早发现问题
- **优先考虑移动设备** - 在整个设计过程中总是检查响应模式

## 键盘快捷键

掌握这些快捷键可以更快、更高效地构建表单：

| **快捷键** | **操作** | **何时使用** |
|--------------|------------|----------------|
| `a` | 打开组件列表 | 添加新的表单字段 |
| `d` | 打开组件属性 | 配置选定的元素 |
| `f` | 切换内容树 | 导航复杂的表单 |
| `p` | 切换预览模式 | 测试表单功能 |
| `o` | 在新选项卡中打开表单 | 全屏测试 |
| `l` | 聚焦位置栏 | 切换到不同的表单 |

**专业提示：**&#x200B;组合使用这些快捷键 - 例如选择一个组件，按下 `d` 进行配置，然后按下 `p` 测试更改。

## 常用工作流

### **创建您的第一个表单**

1. **添加结构** - 使用 `a` 为表单分区添加面板
2. **添加字段** - 插入文本输入、电子邮件和其他组件
3. **配置属性** - 选择每个字段，然后按下 `d` 设置标签并进行验证
4. **测试功能** - 按下 `p` 预览并测试表单
5. **检查移动设备视图** - 使用响应模式验证移动设备上的显示
6. **发布** - 上线准备就绪后，点击“发布”

### **编辑现有的表单**

1. **导航结构** - 使用内容树 (`f`) 快速查找组件
2. **选择并更改** - 直接点击组件或使用内容树
3. **测试更改** - 每次重大更改后进行预览 (`p`)
4. **验证工作流** - 在重新发布之前测试完整的表单流程

### **与团队协作**

1. **使用任务管理** - 将特定的表单分区分配给团队成员
2. **分享以供审阅** - 使用“打开页面”(`o`) 分享简洁的预览
3. **一起测试** - 为协作测试会话使用预览模式
4. **跟踪进度** - 查看任务更新通知

## 常见问题排查

### **界面问题**

+++接口元素未加载

**问题：**&#x200B;工具栏按钮、属性面板或其他界面元素未显示

**解决办法：**

- **刷新页面** - 浏览器刷新的简单方法通常可以解决加载问题
- **检查浏览器兼容性** - 使用 Chrome、Firefox 或 Safari
- **清理浏览器缓存** - 移除可能已过期的缓存文件
- **验证权限** - 确保您拥有适当的表单编辑权限

+++

+++组件没有响应

**问题：**&#x200B;无法选择组件或属性面板不更新

**解决办法：**

- **直接点击组件** - 避免点击空白区域
- **使用内容树** - 按下 `f` 并从树中选择组件
- **检查重叠元素** - 某些组件可能阻碍了其他组件
- **重新加载表单** - 使用位置栏 (`l`) 重新加载当前表单

+++

+++预览模式问题

**问题：**&#x200B;预览模式无法正常工作或显示错误

**解决办法：**

- **检查表单验证** - 确保已正确配置了所有必填字段
- **首先在编辑模式中测试** - 在预览之前验证组件是否正常工作
- **清理浏览器缓存** - 缓存的脚本可能会影响预览
- **检查组件配置** - 检查属性模式设置是否错误

+++

## 高效构建表单的最佳实践

### **组织性建议**

- **使用描述性名称** - 在属性模式中清晰地标记组件
- **将相关字段分组** - 使用面板，按逻辑组织表单分区
- **构建前先规划** - 开始前先草拟表单结构
- **保持简洁** - 避免使用过多的字段让用户感到不知所措

### **用户体验**

- **经常测试** - 每次进行重大更改后都使用预览模式
- **从用户的角度思考** - 考虑完整的表单填写体验
- **提供清晰的标签** - 使用户能够清楚了解字段的用途
- **添加帮助文本** - 为复杂字段使用帮助文本

### **性能优化**

- **最小化组件** - 仅使用必要的表单字段
- **优化图像** - 压缩表单中使用的所有图像
- **在移动设备上测试** - 确保在较慢的移动设备连接上也能获得良好的性能
- **尽早验证** - 设置适当的验证，防止提交错误

## 后续步骤

现在您已了解通用编辑器界面：

1. **通过简单表单进行练习** - 从基本字段开始逐渐熟悉
2. **探索高级功能** - 基本功能熟悉之后，尝试使用 AI 驱动的工具和集成
3. **了解表单创作** - 请参见[快速入门指南](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **主要规则编辑器** - 参考[规则编辑器指南](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)，添加动态行为

**请记住：**&#x200B;通用编辑器旨在以更直观的方式构建表单。从基本功能开始，随着您的需求增加，逐步探索高级功能。
