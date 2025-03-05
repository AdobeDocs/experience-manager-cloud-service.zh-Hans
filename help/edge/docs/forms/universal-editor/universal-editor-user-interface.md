---
title: 了解通用编辑器
description: 本教程可帮助您启动并运行通用编辑器界面。 它可指导您了解在通用编辑器中创建自己的Edge Delivery Services表单的用户界面。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 1%

---


# 探索通用编辑器(WYSIWYG)界面

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)为Adobe Edge Delivery Services Forms提供了一个简单、直观的What You See Is What You Get (WYSIWYG)界面。 它提供了一个现代化的界面，具有拖放功能以实现高效的表单创作。

![通用编辑器用户界面](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## 您将学习的内容

在本教程结束时，您将：

- 了解通用编辑器界面的主要组件
- 放心地浏览不同的界面部分
- 了解如何访问和使用重要的表单构建工具
- 熟悉可提高生产力的键盘快捷键

## 了解通用编辑器界面

使用通用编辑器编辑表单时，控制台会打开一个交互式WYSIWYG界面，该界面允许您立即开始编辑。 此界面可在您工作时提供实时可视化反馈，向最终用户显示表单的确切方式。

>[!NOTE]
>
> 要了解如何使用通用编辑器创作表单，请参阅文章[使用通用编辑器(WYSIWYG)的Edge Delivery Services for AEM Forms快速入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)。

![通用编辑器用户界面](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

通用编辑器界面分为四个逻辑部分：

- **[A： Experience Cloud标头](#experience-cloud-header)**
- **[B：通用编辑器工具栏](#universal-editor-toolbar)**
- **[C：属性面板](#properties-panel)**
- **[D：编辑器](#editor)**

让我们详细了解一下每个部分。

### Experience Cloud标题

Experience Cloud标题显示在控制台顶部，并在更广泛的Adobe Experience Cloud生态系统中提供导航上下文。 它可显示您当前的位置，并允许快速访问其他Experience Cloud应用程序。

![通用编辑器Experience Cloud标头](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

让我们检查每个组件：

- **Adobe Experience Cloud**

  单击屏幕左侧的&#x200B;**Adobe Experience Cloud**&#x200B;链接可导航到Experience Manager解决方案的根目录。 从该位置，您可以访问Experience Manager Sites、Experience Manager Assets和Experience Manager Guides等其他工具。

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png)

- **组织名称**

  **组织名称**&#x200B;显示您当前登录的Identity Management System (IMS)组织的名称。 如果您有权访问多个组织，则可以使用此下拉菜单在它们之间切换。 例如，在屏幕截图中，当前选定的IMS组织是“AEM Forms Internal01”。

  ![组织](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png)

- **帮助**

  通过“帮助”图标，可快速访问学习和支持资源。 当您遇到挑战或需要有关特定功能的指导时，此功能尤其有用。 您还可以通过此部分提交反馈。

  ![帮助](/help/edge/docs/forms/universal-editor/assets/ue-help.png)

- **通知**

  **通知**&#x200B;部分显示IMS组织中当前分配的未完成通知、请求和当前任务的数量。 关注此部分有助于您随时掌握工作流程。

  ![通知](/help/edge/docs/forms/universal-editor/assets/ue-notification.png)

- **解决方案**

  通过&#x200B;**解决方案**&#x200B;菜单，您可以切换到其他Adobe Experience Cloud解决方案，以便轻松地在工作流中的不同工具之间移动。

  ![解决方案](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png)

- **用户配置文件**

  此图标显示您的配置文件信息，以及您当前登录的IMS组织的名称。 单击此图标可访问帐户设置和注销选项。

  ![作者](/help/edge/docs/forms/universal-editor/assets/ue-author.png)

### 通用编辑器工具栏

工具栏提供了重要的导航和编辑工具。 利用它，您可以在表单之间移动、发布或取消发布表单、编辑表单属性，以及访问用于添加动态行为的规则编辑器。

![通用编辑器工具栏](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

以下是每个组件提供的功能：

- **主页按钮**

  使用“主页”按钮可返回到通用编辑器的起始页。 当您需要开始处理其他表单时，这将很有用。 您还可以直接在位置栏中输入URL，以导航到要编辑的任何表单。

  ![通用编辑器主页](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

- **位置栏**

  **位置栏**&#x200B;显示您当前编辑的表单的地址。 要切换到其他表单，只需单击位置栏并输入其URL即可。 用于聚焦位置栏的键盘快捷键是`l`。

  ![位置栏](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

- **规则编辑器**

  **规则编辑器**&#x200B;允许您通过直观的可视界面向表单添加动态行为。 利用它，您可以创建条件、验证和操作来响应用户输入，使表单具有交互性和智能性。

  ![规则编辑器](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > - 默认情况下，通用编辑器中未启用规则编辑器扩展。 要启用这项强大的功能，请通过您的正式电子邮件地址通过[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)联系我们。
  > - 要了解如何创建和管理规则，请参阅文章[WYSIWYG创作中的规则编辑器简介](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)。

- **编辑表单属性**

  使用&#x200B;**编辑表单属性**&#x200B;选项，可配置重要的表单设置，如表单数据模型(FDM)和发布日期。 这些属性会影响表单的行为以及与后端系统的集成。

  ![编辑表单属性](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

- **身份验证标头设置**

  **身份验证标头设置**&#x200B;选项允许您为本地开发目的设置自定义身份验证标头。 在测试需要身份验证凭据的表单时，这尤其有用。

  ![身份验证标头](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

- **响应模式**

  **响应模式**&#x200B;功能允许您测试表单在不同设备上的显示方式。 默认情况下，编辑器在桌面布局中打开，但您可以切换到移动设备视图，以确保您的表单仍然可用且在较小的屏幕上具有吸引力。

  ![响应模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

- **预览模式**

  **预览模式**&#x200B;显示的表单与发布时显示的表单完全相同。 这允许您通过单击链接和按钮与表单进行交互，就像您的用户一样。 这是发布之前的重要步骤，用于验证所有内容是否均可按预期运行。 使用键盘快捷键`p`在编辑和预览模式之间切换。

  ![预览](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

- **打开页面**

  使用&#x200B;**打开页面**&#x200B;按钮可在新的浏览器选项卡中打开您的表单以进行预览。 这为您提供了表单的全屏视图，而无需编辑器界面。 此操作的键盘快捷键为`o`。

  ![打开页面](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

- **发布**

  表单可供用户使用后，**发布**&#x200B;按钮会使其上线并对受众可用。 这是表单创建工作流中的最后一步。

  ![发布](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

- **省略号菜单**

  单击省略号(...)会显示其他选项，包括&#x200B;**取消发布**&#x200B;当前在线表单的功能。 当您需要临时从公共访问中删除表单或将其替换为更新版本时，这将很有用。

  ![省略号](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

### 属性面板

**属性面板**&#x200B;将显示在界面的右侧，并根据您在表单中选择的内容显示上下文信息。 未选择任何组件时，将显示整体窗体结构。

![属性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

让我们探讨一下其主要组件：

- **属性模式**

  **属性**&#x200B;模式显示当前选定组件的设置和选项。 您可以在此处自定义表单的各个元素，以满足您的特定要求。 打开选定组件属性的键盘快捷键为`d`。

  ![属性](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

- **内容树**

  **内容树**&#x200B;显示表单的分层结构。 此可视化表示形式可帮助您了解组件如何彼此嵌套。 单击树中的任意项目会在编辑器中选中该项目并滚动到其位置。 这在复杂形式中特别有用。 使用键盘快捷键`f`切换内容树视图。

  ![内容树](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

- **生成变体**

  **生成变体**&#x200B;功能利用人工智能根据特定提示创建表单的不同版本。 这可帮助您试验不同的方法和设计，而无需手动创建每个变体。 提示可由Adobe提供或由您自定义。

  ![生成变体](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

  >[!NOTE]
  >
  > 有关使用生成表单变体的详细说明，请参阅[生成变体](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)文章。

- **正在试验**

  **试验**&#x200B;功能允许您运行比较不同表单设计和布局的控制测试。 通过分析用户与每个变体的交互方式，您可以做出数据驱动型决策，以优化转化率和用户体验。

  ![正在试验](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

- **个性化**

  **Personalization**&#x200B;设置允许您将表单与Adobe Experience Platform (AEP)或外部应用程序连接。 这种连接使您能够根据用户数据和行为创建量身定制的表单体验，从而提高相关性和参与度。

  ![个性化](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

- **A/B测试**

  **A/B测试**&#x200B;可帮助您比较表单的特定变体，以确定哪些变体效果更好。 与更广泛的试验不同，A/B测试通常侧重于比较特定元素或更改，以确定最有效的选项。

  ![A/B测试](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

- **任务管理**

  **任务管理**&#x200B;功能通过帮助您的团队组织、跟踪和完成与表单创建和优化相关的任务来简化协作。 这有助于通过明确的问责制使项目高效推进。

  ![任务管理](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

- **内容草稿**

  **内容草稿**&#x200B;功能允许您创建和保存表单中文本元素的初步版本。 您可以使用现有的表单文本创建草稿，或从头开始创建，然后根据需要编辑或删除草稿。 默认情况下，您会看到三个草稿，但单击“显示全部”****&#x200B;会显示其他草稿。

  ![内容草稿](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

- **数据Source**

  通过&#x200B;**数据Source**&#x200B;选项，您可以为表单数据模型(FDM)配置和选择数据源。 此集成使选定源中的所有数据模型对象、属性和服务都可在表单中使用，从而实现动态数据检索和提交。

  ![数据Source](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

- **添加**

  **添加**&#x200B;按钮显示了一个下拉列表，其中包含可添加到当前选定容器的组件。 例如，在选择自适应表单部分时，此列表显示可添加到该部分的所有组件。 打开此组件列表的键盘快捷键为`a`。

  ![添加图标](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

- **重复**

  **复制**&#x200B;选项创建选定组件的精确副本。 当您需要多个相似元素时，这可以节省时间，因为您可以先复制然后再修改，而不是从头开始创建。

  ![图标重复](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)

- **删除**

  **删除**&#x200B;选项会从表单中删除所选的组件。 使用此选项时请务必小心，因为它会立即删除元素，而不显示确认提示。

  ![删除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### 编辑器

编辑器是您在其中创建和修改表单的中心工作区。 它可显示位置栏中指定的表单，并提供一个WYSIWYG体验，该体验可准确地向用户显示您的表单。 在预览模式下，您可以像用户一样与表单进行交互，测试通过按钮和链接的导航。

![编辑器](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

在编辑器中，您将花费大部分时间添加组件、配置其属性并安排它们以创建直观、有效的表单体验。

## 键盘快捷键摘要

要提高工作效率，请记住以下重要的键盘快捷键：

- `l` — 聚焦位置栏
- `p` — 在编辑和预览模式之间切换
- `o` — 在新选项卡中打开表单
- `d` — 打开选定组件的属性
- `f` — 切换内容树视图
- `a` — 打开要添加组件的列表


