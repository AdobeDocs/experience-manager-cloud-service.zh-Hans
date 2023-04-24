---
title: 在AEM Sites页面中添加自适应表单（核心组件）
seo-title: How to add an Adaptive Form (Core Components) to an AEM Sites page?
description: 您可以在AEM Sites页面中使用自适应表单（核心组件）来填写和提交表单，而无需离开AEM Sites页面。
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2a487654c3af2d2ec3aa43481caed5e1d4fc77a2
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 2%

---

# 将自适应Forms添加到AEM Sites页面 {#add-an-adaptive-form-to-aem-sites-page}

## 概述 {#overview}

您可以在AEM Sites页面中无缝地创作或嵌入自适应Forms，以便用户无需离开站点页面即可填写和提交表单。 它有助于用户保持在网页其他元素的上下文中，并同时与表单进行交互。

您可以选择以下方法之一，在AEM Sites页面中创作或嵌入自适应表单：

* **通过将表单组件拖放到自适应Forms容器组件来创建自适应表单**:使用 [自适应Forms容器](#af-container-component) 组件，以在网页内创建一个托管自适应表单的空间。 您可以在此空间中拖放自适应表单组件以创建表单。 例如，请观看以下视频，了解如何使用 [!UICONTROL 自适应Forms容器] 组件：

>[!VIDEO](/help/forms/assets/formcreationbyadaptiveformcontainer.mp4)

的 [自适应表单容器](#af-container-component) 组件允许您直接在AEM Sites编辑器中利用自适应Forms组件来构建数字注册体验。 此集成可为希望在AEM Sites页面中创建和管理表单的AEM Sites作者提供无缝体验。

* **嵌入现有自适应表单**:的 [自适应Forms — 嵌入](#embed-existing-af) 组件允许您轻松地将预先存在的自适应表单合并到AEM Sites内的页面中。 例如，使用 [!UICONTROL 自适应Forms — 嵌入] 组件，如以下视频所示：

>[!VIDEO](/help/forms/assets/embednewform_embed.mp4)

该功能增强了自适应Forms的适应性和可重用性。 此集成为客户提供了一种便捷的方式，可重复使用客户已创建的自适应Forms。

* **使用自适应Forms向导创建表单**:

   使用 [自适应Forms — 嵌入](#embed-new-af) 组件来使用表单创建向导，在AEM Sites编辑器中创建自适应表单。 表单将另存为外部实体。 您还可以在其他站点页面和独立表单中重复使用此表单。
例如，请观看以下视频，了解如何使用 [!UICONTROL 自适应Forms — 嵌入] 组件。

>[!VIDEO](/help/forms/assets/createnewform_embed.mp4)

### 注意事项 {#considerations}

您可以使用规则编辑器添加或控制自适应表单组件的动态行为。 例如，隐藏或显示组件。 规则编辑器不适用于非自适应表单组件。 因此，在AEM Forms容器组件中使用非自适应表单组件时，请务必谨慎。

## 使用自适应Forms容器组件创建自适应表单 {#af-container-component}

的 [!UICONTROL 自适应表单容器] 组件允许在AEM Sites编辑器中使用自适应Forms组件构建数字注册体验。 您可以通过拖放表单组件来创建自适应表单。

### 前提条件 {#prerequisites-af-container}

+++ 启用 **[!UICONTROL 自适应Forms容器]** 组件。

启用 [!UICONTROL 自适应Forms容器] 组件，请执行以下步骤：
1. 转到 [!UICONTROL 页面信息] > [!UICONTROL 编辑模板]
1. 单击 [!UICONTROL 策略] ，然后选择 **核心组件示例 — 自适应表单** 复选框。
1. 单击 [!UICONTROL 完成].

>[!VIDEO](/help/forms/assets/adaptiveformcontainer.mp4)

+++

+++ 在网站页面上包含clientlib

要在AEM Sites页面中使用自适应Forms组件，请使用AEM Archetype/Git存储库和部署管道将Customheaderlibs和Customfooterlibs客户端库包括到AEM Sites页面。

1. 打开 [AEM Forms原型或克隆的Git存储库](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 项目。 例如，Visual Studio代码。
1. 导航到 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 复制 `sling:resourceSuperType`. 例如，值为 `core/wcm/components/page/v3/page`.

   ![sling资源](/help/forms/assets/slingresource.png)

1. 在位置创建类似结构 `ui.apps/src/main/content/jcr_root/apps` 与 `core/wcm/components/page/v3/page`.

   ![覆盖结构](/help/forms/assets/overlaystructure.png)

1. 添加 `customheaderlibs.html` 和 `customfooterlibs.html` 文件。

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly> 
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly> 
   ```

   customfooterlibs.html用于JavaScript，customheaderlibs.html用于css。

1. [运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 以部署更改。

+++

### 使用自适应Forms容器组件创建自适应表单 {#create-af-using-af-container}


使用创建自适应表单 [!UICONTROL 自适应Forms容器] 组件：

1. 在编辑模式下打开AEM Sites页面。
1. 从组件浏览器面板中，拖放 **[!UICONTROL 自适应Forms容器]** 组件。
1. 使用自适应Forms组件创建自适应表单。
1. 保存设置。

>[!VIDEO](/help/forms/assets/af-container.mp4)

您的表单已准备就绪。 在您发布AEM Sites页面时，它会自动发布自适应表单及其关联的引用资产。

#### 配置自适应表单容器属性 {#configure-additional-settings-container}

您可以自定义 [!UICONTROL 自适应表单容器] 组件。 例如，您可以配置预填充服务以在网站页面上加载具有预填充值的自适应表单。 您可以配置“数据模型”设置，以将自适应表单与数据模型关联。 如果要在提交自适应表单时在OneDrive或SharePoint上保存数据，请配置“提交”操作的设置。 您还可以为自适应Forms添加自定义提交操作。

为 **[!UICONTROL 自适应Forms容器]** 组件中，单击 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) 中。 的 **[!UICONTROL 编辑自适应Forms容器]** 对话框。

![“编辑”对话框](/help/forms/assets/adaptiveformcontainer-editdialog.png)

在 [!UICONTROL 编辑自适应Forms容器] 对话框中，您可以指定以下内容。
* **“基本”选项卡**
   * **预填充服务**:您可以使用预填充服务使用现有数据自动填充自适应表单的字段。 用户打开表单时，将预填这些字段的值。 有关预填充服务的信息，请参阅 [预填自适应表单字段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **客户端库类别**:指定 [JavaScript函数](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) 表达式中使用且受自适应Forms支持的变量。
* **数据模型**:数据模型允许您将不同数据源中的实体和服务集成到自适应表单。 选择 **[!UICONTROL 表单数据模型]** 如果您创建的自适应表单涉及从多个数据源获取数据和将数据写入多个数据源。
   * **表单数据模型**:表单数据模型允许自适应表单与不同的数据源进行通信。 有关配置数据源的信息，请参阅 [配置数据源。](/help/forms/configure-data-sources.md)
   * **架构**:架构表示组织内的后端系统生成或使用数据的结构。 您可以 [将架构与自适应表单关联](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) 并使用其元素将动态内容添加到自适应表单。

      >[!NOTE]
      >
      > 配置表单数据模型后，无法更改关联的表单模型。 但是，可以修改与表单数据模型关联的架构。

* **“提交”选项卡**

   * **重定向到 URL**

      **重定向URL/路径**:指定在提交操作后自适应表单被重定向到的URL或路径。

      **提交操作**:当用户单击自适应表单上的“提交”按钮时，会触发提交操作。 您可以 [在自适应表单上配置提交操作](/help/forms/configuring-submit-actions.md). 自适应表单提供了一些现成的提交操作：
      * 提交到REST端点
      * 发送电子邮件
      * 使用表单数据模型提交
      * 调用AEM工作流
      * 提交到 SharePoint
      * 提交到 OneDrive
      * 提交到 Azure Blob Storage

   您还可以 [扩展默认的提交操作](custom-submit-action-form.md) 创建您自己的自定义提交操作。

* **显示消息**
   * **消息内容**:使用富文本编辑器编写消息以在表单提交时显示。 仅当您选择显示感谢信时，此选项才可用。

## 嵌入现有自适应表单  {#aem-container-component}

使用 **[!UICONTROL 自适应Forms — 嵌入]** 组件中，您可以嵌入新的自适应表单，也可以在网站的页面中嵌入现有的自适应表单。 的 [!UICONTROL 自适应Forms — 嵌入] 组件允许您：

* [删除现有的自适应表单](#embed-new-af)

* [创建和嵌入新的自适应表单](#embed-existing-af)

### 前提条件 {#prerequisites}

+++ 启用 **自适应Forms — 嵌入** 组件。

启用 [!UICONTROL 自适应Forms — 嵌入] 组件，请执行以下步骤：
1. 转到 [!UICONTROL 页面信息] > [!UICONTROL 编辑模板]
1. 单击 [!UICONTROL 策略] ，然后选择 **核心内容** 复选框。
1. 单击 [!UICONTROL 完成].

>[!VIDEO](/help/forms/assets/enableadaptiveform-embedtemplate.mp4)

+++

+++ 在网站页面上包含clientlib

当 **[!UICONTROL 当表单覆盖页面的整个宽度时]** 选项 **[!UICONTROL 表单容器]** 配置对话框和 **使用核心组件的自适应Forms** ，则必须在相应网站页面上包含clientlib。

![叠加Gif](/help/forms/assets/overlaycorecomponent.gif)

要在AEM Sites页面中使用自适应Forms组件，请使用AEM Archetype/Git存储库和部署管道将Customheaderlibs和Customfooterlibs客户端库包括到AEM Sites页面。

1. 打开 [AEM Forms原型或克隆的Git存储库](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 项目。 例如，Visual Studio代码。
1. 导航到 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 复制 `sling:resourceSuperType`. 例如，值为 `core/wcm/components/page/v3/page`.

   ![sling资源](/help/forms/assets/slingresource.png)

1. 在位置创建类似结构 `ui.apps/src/main/content/jcr_root/apps` 与 `core/wcm/components/page/v3/page`.

   ![覆盖结构](/help/forms/assets/overlaystructure.png)

1. 添加 `customheaderlibs.html` 和 `customfooterlibs.html` 文件。

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
       data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
       <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly>
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
     data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
     <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly>
   ```

   customfooterlibs.html用于JavaScript，customheaderlibs.html用于CSS。

1. [运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 以部署更改。

+++

### 嵌入新的自适应表单 {#embed-new-af}

1. 在编辑模式下打开AEM Sites页面。
1. 从组件浏览器面板中，拖放 [!UICONTROL 自适应Forms — 嵌入] 组件。
1. 单击 **加号** 图标时，系统会将您重定向到表单创建向导。

   ![自适应Forms — 嵌入组件](/help/forms/assets/aemformcontainer.png)

1. 从 [!UICONTROL 表单创建] 向导。
1. 的 [!UICONTROL 资产路径] 已经包含创建的自适应表单的路径
1. 保存设置。 自适应表单现在嵌入到页面中。

### 嵌入现有自适应表单 {#embed-existing-af}

1. 在编辑模式下打开AEM Sites页面。
1. 从组件浏览器面板中，拖放 [!UICONTROL 自适应Forms — 嵌入] 组件。
1. 点按 [!UICONTROL 自适应Forms — 嵌入] 组件，然后点按 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) 中。 的 **[!UICONTROL 编辑自适应Forms — 嵌入]** 对话框。
1. 浏览并选择要嵌入到 [!UICONTROL 资产路径].
1. 保存设置。 自适应表单现在嵌入到页面中。

#### 配置自适应表单_嵌入属性

您可以自定义 [!UICONTROL 自适应表单 — 嵌入] 组件。 在 [!UICONTROL 编辑自适应Forms — 嵌入] 对话框中，您可以指定以下内容。
* **资产路径**:浏览并选择要嵌入的自适应表单。 如果您从资产浏览器中将其删除，则会自动填充该内容。
* **帖子提交** :选择要在表单提交时触发的操作。 您可以选择显示感谢信或感谢页。
   * **显示感谢消息**:使用富文本编辑器编写消息以在表单提交时显示。 仅当您选择显示感谢信时，此选项才可用。
   * **显示感谢页面**:浏览并选择要在表单提交时显示的页面。 仅当您选择显示感谢页面时，此选项才可用。
   * **重定向到“谢谢”页面**:启用选项，将包含嵌入式自适应表单的页面替换为感谢页面。 否则，感谢页面将替换 [!UICONTROL 自适应Forms — 嵌入] 组件，而不刷新页面的基础站点。 仅当您选择显示感谢页面时，此选项才可用。
* **使用页面语言**:使用AEM Sites页面的本地区域设置，而不是自适应表单。
* **聚焦表单**:选择以设置对自适应表单第一个字段的焦点。
* **表单覆盖框架的整个宽度**:如果选中此选项，则不会使用iframe来呈现表单。
* **高度**:指定容器的高度。 将其留空以自动调整容器大小。
* **CSS客户端库**:指定CSS客户端库的路径。

### 发布嵌入式自适应表单 {#publishing-embedded-adaptive-form}

让我们考虑以下方案，以在AEM站点页面中发布嵌入的自适应表单：

* 如果您是首次发布AEM站点页面，并且该页面包含嵌入的自适应表单，则发布站点页面和嵌入的资产。
* 如果您只修改了已发布站点页面中嵌入的自适应表单，则应发布原始资产，并且所做的更改会反映在已发布的站点页面中。 发布的网站页面包含对资产的引用，无需重新发布页面。
* 如果您修改了站点页面和嵌入的自适应表单，请重新发布站点页面和嵌入的资产。

### 修改嵌入的自适应表单  {#modifying-embedded-adaptive-form}

要修改嵌入的自适应表单的任何配置或属性，请执行以下操作之一。

* 在相应的编辑器中在自适应表单中打开原始表单并对其进行修改。
* 在编辑模式下，从网站页面中点按自适应表单，然后点按 **[!UICONTROL 在新窗口中编辑]**. 原始表单会在编辑模式下打开，您可以对其进行修改。

>[!NOTE]
>
>在原始自适应表单中所做的更改会自动反映在嵌入的表单中。 但是，请重新发布自适应表单或网站页面，以反映已发布页面中的更改。

### 最佳实践 {#best-practices}

* 原始表单中的页眉和页脚未包含在嵌入的表单中。
* 支持用户草稿和提交嵌入的表单，并在Forms门户的“草稿和提交的Forms”选项卡中显示这些用户草稿和提交表单。

[在AEM Sites页面中，布局模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) 允许您调整已在AEM网站的页面中创建或嵌入的自适应表单的大小。

![AF-layout-support](/help/forms/assets/afsite-layoutsupport.gif)

AEM站点页面维护对自适应表单的引用。 当您翻译AEM Sites页面时，它会使用 [翻译项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) 翻译成其他语言。

