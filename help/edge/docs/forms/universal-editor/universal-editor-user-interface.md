---
title: 了解通用编辑器 — 开发人员教程
description: 本教程可帮助您启动并运行通用编辑器界面。 它可指导您了解在通用编辑器中创建自己的Edge Delivery Services表单的用户界面。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: ba42a99e6138616ab6a7564c4bf58400844bdcc4
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# 探索通用编辑器(WYSIWYG)界面

[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)为Adobe Edge Delivery Services (EDS) Forms提供了一个简单、直观的What You See Is What You Get (WYSIWYG)界面。 它提供了一个现代化的界面，具有拖放功能以实现高效的表单创作。

![通用编辑器用户界面](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## 了解通用编辑器界面

当表单作者使用通用编辑器编辑表单时，控制台会打开一个交互式WYSIWYG界面，允许用户开始编辑表单。

>[!NOTE]
>
> 要了解如何使用通用编辑器创作表单，请参阅文章[使用通用编辑器(WYSIWYG)的Edge Delivery Services for AEM Forms快速入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)。

![通用编辑器用户界面](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

通用编辑器界面分为四个部分：

* **[A： Experience Cloud标头](#experience-cloud-header)**
* **[B：通用编辑器工具栏](#universal-editor-toolbar)**
* **[C：属性面板](#properties-panel)**
* **[D：编辑器](#editor)**

### Experience Cloud标题

Experience Cloud标题位于控制台顶部。 它提供有关Experience Cloud中当前位置的信息。 它还允许您导航到其他Experience Cloud应用程序。

![通用编辑器Experience Cloud标头](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


让我们了解它的每个组件。

* **Adobe Experience Cloud**

  您可以单击屏幕左侧的&#x200B;**Adobe Experience Cloud**&#x200B;链接以导航到Experience Manager解决方案的根目录并访问Experience Manager Sites、Experience Manager Assets和Experience Manager Guides等工具。

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%，height=50%}

* **组织名称**

  **组织名称**&#x200B;显示您当前登录的IMS组织的名称。 您可以从下拉列表中选择，切换到其他IMS组织（如果它们有权访问其他组织）。 例如，当前选定的IMS组织名称为`AEM Forms Internal01`。

  ![组织](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%，height=50%}


* **帮助**

  通过帮助图标，可快速访问学习和支持资源。 表单作者还可以在&#x200B;**帮助**部分中添加反馈。
  ![帮助](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%，height=50%}


* **通知**

  **通知**&#x200B;部分显示IMS组织中当前分配的未完成通知数、请求数和当前任务。

  ![通知](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%，height=50%}


* **解决方案**

  您可以使用&#x200B;**解决方案**链接切换到其他Experience Cloud解决方案。
  ![解决方案](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%，height=50%}


* **作者**
图标表示表单作者的详细信息，以及作者当前登录的IMS组织的名称。
  ![作者](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%，height=50%}

### 通用编辑器工具栏

您可以通过工具栏导航和编辑其他表单。 它还允许他们发布或取消发布表单、编辑表单的属性并访问规则编辑器。
![通用编辑器工具栏](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

让我们了解它的每个组件。

* **主页按钮**
使用“主页”按钮可导航到通用编辑器的起始页。 您还可以使用通用编辑器直接输入要编辑的表单的URL。
  ![通用编辑器主页](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **位置栏**
**位置栏**&#x200B;显示作者正在编辑的表单的地址。 您还可以通过单击位置栏输入其他表单URL。 打开位置栏的快捷键是`l`键。
  ![位置栏](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){width=50%，height=50%}



* **规则编辑器**

  **规则编辑器**&#x200B;为创建和管理规则提供了一个直观的可视化界面。 您可以使用规则编辑器添加动态表单行为。

  ![规则编辑器](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * 在通用编辑器中，默认情况下不启用规则编辑器扩展。 要启用规则编辑器扩展，请从您的正式电子邮件ID中通过[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)向我们发送电子邮件。
  > * 要了解如何创建规则，请参阅文章[WYSIWYG创作中的规则编辑器简介](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)。

* **编辑表单属性**
您可以通过单击**编辑表单属性**选项来编辑表单属性，如表单数据模型和发布日期。
  ![编辑表单属性](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **身份验证标头设置**
**身份验证标头设置**允许作者设置自定义身份验证标头用于本地开发。
  ![身份验证标头](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%，height=50%}



* **响应模式**
  **响应模式**&#x200B;选项允许您定义通用编辑器呈现表单的方式。 默认情况下，编辑器会在桌面布局中打开，其中高度和宽度由浏览器自动确定。 或者，您可以选择模拟移动设备，并检查表单在移动设备上的显示方式。

  ![响应模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%，height=50%}


* **预览模式**
在预览模式下，表单在编辑器中会与发布时完全一致。 这允许作者通过单击链接和按钮来导航表单。 在对编辑内容感到满意后，作者可以为实时用户发布表单。 在编辑模式和预览模式之间切换的快捷键是`p`。
  ![预览](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **打开页面**
**打开页面**&#x200B;选项会在新选项卡中打开表单以进行预览。 在新选项卡中以预览模式打开表单的快捷键是`o`。
  ![打开页面](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **发布**

  您可以使用&#x200B;**发布**按钮将表单提供给实时用户。
  ![发布](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%，height=50%}

* **省略号**
当作者单击(...)省略号选项时，会显示**取消发布**&#x200B;选项。 您可以使用&#x200B;**取消发布**选项取消发布表单。
  ![省略号](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%，height=50%}

### 属性面板

**属性面板**位于编辑器的右侧。 它显示表单层次结构中所选组件的详细信息。 未选择任何组件时，它是缺省结构。
![ue-properties面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%，height=50%}


让我们了解它的每个组件。


* **属性模式**
在**属性**&#x200B;中，选项在编辑器中显示所选组件的属性。 例如，该图像显示了所选编号输入组件的属性。 可以使用此选项修改组件的属性。 用于打开组件属性的快捷键是`d`。

  ![ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%，height=50%}


* **内容树**
**内容树**&#x200B;选项显示表单的层次结构。 当作者单击内容树中的项时，编辑器会选择该项并滚动到该组件。 在内容树视图之间切换的快捷键是`f`键。

  ![内容树](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%，height=50%}


* **生成变体**
  **生成变体**&#x200B;使用人工智能根据特定提示生成不同的表单版本。 这些提示可以由Adobe提供，也可以由表单作者制作和管理。

  ![变量](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%，height=50%}


  >[!NOTE]
  >
  > 有关使用生成表单变体的说明，请参阅[生成变体](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)文章

* **正在试验**：

  **试验**指用于测试不同表单和布局变化以优化用户体验和性能的技术。
  ![正在试验](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%，height=50%}


* **Personalization**
**Personalization**选项配置设置，以便在表单与Adobe Experience Platform (AEP)(属于Adobe生态系统或外部应用程序的一部分)之间建立连接。
  ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%，height=50%}


* **A/B测试**：
  **A/B测试**指用于测试各种不同的表单和布局变化以优化用户体验和性能的技术。
  ![A/B测试](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%，height=50%}



* **任务管理**：
通过**任务管理**功能，您可以简化工作流并增强协作，方法是允许团队管理、跟踪和执行与自定义和优化表单相关的任务
  ![任务管理](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){width=50%，height=50%}

。
* **内容草稿**

  **内容草稿**&#x200B;选项允许您为富文本元素创建草稿。 可以使用现有表单文本或从头开始创建草稿。 您可以根据需要编辑或删除草稿。 默认情况下，只有三个草稿可见，但单击“显示全部”****&#x200B;将显示其余草稿。

  ![任务管理](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){width=50%，height=50%}


* **数据Source**

  **数据Source**选项允许您配置数据源，并在创建表单数据模型(FDM)时选择数据源。 它使选定数据源中的所有数据模型对象、属性和服务可用于表单数据模型。
  ![数据Source](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%，height=50%}

* **添加**

  **添加**&#x200B;选项会打开一个下拉列表，其中包含可添加到选定容器的组件。 例如，在“自适应表单”部分中，列表显示了可添加到表单的可用组件。 打开组件列表的快捷键是`a`。
  ![添加图标](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%，height=50%}

* **重复**

  **复制**选项将创建在内容树或编辑器中选定的组件副本。
  ![图标重复](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%，height=50%}


* **删除**
**删除**&#x200B;选项会删除在内容树或编辑器中选择的组件。

  ![删除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%，height=50%}

### 编辑器

编辑器允许您编辑表单，并且在位置栏中指定的表单在编辑区域中呈现。 如果编辑器处于预览模式，则可以使用可用的按钮和链接在表单中导航。
![编辑器](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%，height=50%}

## 另请参阅

{{universal-editor-see-also}}
