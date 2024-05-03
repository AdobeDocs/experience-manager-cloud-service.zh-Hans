---
title: 如何在AEM Sites页面中添加或创建自适应表单核心组件？
description: 在AEM Sites页面中使用自适应表单核心组件填写和提交表单，而不离开AEM Sites页面。
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 4%

---

# 使用AEM Sites编辑器创建或添加自适应表单 {#add-an-adaptive-form-to-aem-sites-page}

您可以将自适应Forms无缝创作或嵌入到AEM Sites页面中，使用户无需离开站点页面即可填写和提交表单。 它有助于用户保留在网页其他元素的上下文中，同时与表单交互。

您可以选择以下方法之一来创建或将自适应表单添加到AEM Sites页面：

* **使用自适应Forms容器组件创建自适应表单**：和 [自适应表单容器](#af-container-component) 通过组件，可直接在AEM Sites编辑器中利用自适应Forms组件构建数字注册体验。 此集成为希望在AEM Sites页面中创建和管理表单的AEM Sites作者提供了无缝体验。

* **添加现有自适应表单**：和 [自适应Forms — 嵌入(v2)](#embed-existing-af) 通过组件，您可以轻松地将预先存在的自适应表单添加到AEM Sites中的页面。 此功能增强了自适应Forms的适应性和可重用性。 此集成为客户提供了一种便捷的方式，可重复使用他们已创建的自适应Forms。

* **使用“自适应Forms向导”创建表单**：使用 [自适应Forms — 嵌入(v2)](#embed-new-af) 用于在AEM Sites编辑器中使用表单创建向导创建自适应表单的组件。 表单另存为外部实体。 您也可以在其他Sites页面和独立表单中重复使用此表单。

* **在AEM Sites页面中添加多个自适应Forms**：要在AEM Sites页面中添加多个自适应Forms，请使用AEM Forms容器组件 —  [自适应Forms — 嵌入(v2)](#embed-new-af) 和 [自适应表单容器](#af-container-component). 如果需要在某个AEM Sites页面中添加多个自适应表单作为div，则可以使用自适应表单容器组件。

您可以使用规则编辑器添加或控制自适应表单组件的动态行为。 例如，隐藏或显示组件。 规则编辑器不可用于非自适应表单组件。 因此，在AEM Forms Container组件中使用非自适应表单组件时，请务必勤勉工作。

## 使用自适应Forms容器组件创建自适应表单 {#af-container-component}

此 [!UICONTROL 自适应表单容器] 组件允许在AEM Sites编辑器中使用自适应Forms组件构建数字注册体验。 您可以通过拖放表单组件来创建自适应表单。

### 先决条件 {#prerequisites-af-container}

+++ 启用 **[!UICONTROL 自适应Forms容器]** 组件。

若要启用模板策略中的[!UICONTROL 自适应表单容器]组件，请执行以下步骤：

1. 转到 [!UICONTROL 页面信息] > [!UICONTROL 编辑模板]
1. 单击 [!UICONTROL 策略] 并选择 **[!UICONTROL 自适应Forms容器]**  复选框 **[AEM原型项目名称]  — 自适应表单**.
1. 单击&#x200B;**[!UICONTROL 完成]**。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ “将自适应Forms客户端库包含到AEM Sites”页面

要在AEM Sites页面中使用自适应Forms组件，请使用AEM Archetype/Git存储库和部署管道将Customheaderlibs和Customfooterlibs客户端库包含到AEM Sites页面。

1. 打开您的 [AEM Forms原型或克隆的Git存储库](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 在文本编辑器中编辑项目。 例如，Visual Studio Code。
1. 导航到 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 复制的值 `sling:resourceSuperType`. 例如，值为 `core/wcm/components/page/v3/page`.

   ![Sling 资源](/help/forms/assets/slingresource.png)

1. 在该位置创建类似结构 `ui.apps/src/main/content/jcr_root/apps` 与 `core/wcm/components/page/v3/page`.

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


要使用创建自适应表单，请执行以下操作 [!UICONTROL 自适应Forms容器] 组件：

1. 以编辑模式打开 AEM Sites 页面。
1. 在组件浏览器面板中，拖放 **[!UICONTROL 自适应Forms容器]** 组件。
1. 使用自适应Forms组件创建自适应表单。
1. 保存设置。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

您的表单已准备就绪。 发布AEM Sites页面时，该页面会自动发布自适应表单及其关联的引用资源。

#### 配置自适应表单容器属性 {#configure-additional-settings-container}

您可以自定义的 [!UICONTROL 自适应表单容器] 组件。 例如，

* 您可以将预填充服务配置为在站点的页面上加载预填充值的自适应表单。
* 您可以配置数据模型设置以将自适应表单与数据源关联。
* 您可以配置提交操作，以便在提交表单时在Microsoft® OneDrive、Microsoft®OneDrive或其他数据源上发送数据。 您还可以为自适应Forms创建和选择自定义提交操作。

要设置属性 **[!UICONTROL 自适应Forms容器]** 组件，单击 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) 在操作栏上。 此 **[!UICONTROL 编辑自适应Forms容器]** 对话框打开。

![“编辑”对话框](/help/forms/assets/adaptiveformcontainer-editdialog.png)

在 [!UICONTROL 编辑自适应Forms容器] 对话框，您可以指定以下内容。
* **“基本”选项卡**
   * **预填充服务**：您可以使用预填充服务使用现有数据自动填充自适应表单的字段。 当用户打开表单时，这些字段的值会预先填充。 有关预填充服务的信息，请参阅 [预填自适应表单字段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **客户端库类别**：指定 [JavaScript函数](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) 在表达式中使用并且受自适应Forms支持的这些函数。
* **数据模型**：通过数据模型，您可以将来自不同数据源的实体和服务集成到自适应表单中。 选择 **[!UICONTROL 表单数据模型]** 如果您创建的自适应表单涉及从多个数据源获取数据并将数据写入多个数据源。
   * **表单数据模型**：表单数据模型(FDM)允许自适应表单与不同的数据源进行通信。 有关配置数据源的信息，请参阅 [配置数据源](/help/forms/configure-data-sources.md).
   * **架构**：架构表示组织中的后端系统生成或使用数据的结构。 您可以 [将架构关联到自适应表单](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) 并使用其元素将动态内容添加到自适应表单。

     >[!NOTE]
     >
     > 配置表单数据模型(FDM)后，无法更改关联的表单模型。 但是，可以修改与表单数据模型(FDM)关联的架构。

* **提交选项卡**

   * **重定向到URL**
      * **重定向URL/路径**：指定自适应表单在提交后重定向到的URL或路径。

      * **提交操作**：当用户单击自适应表单上的提交按钮时，会触发提交操作。 您可以 [在自适应表单上配置提交操作](/help/forms/configuring-submit-actions.md). 自适应表单提供以下开箱即用的提交操作：
         * 提交到 REST 端点
         * 发送电子邮件
         * 使用表单数据模型(FDM)提交
         * 调用 AEM 工作流
         * 提交到 SharePoint
         * 提交到 OneDrive
         * 提交到 Azure Blob 存储

  您还可以 [扩展默认提交操作](custom-submit-action-form.md) 以创建您自己的自定义提交操作。

* **显示消息**
   * **消息内容**：使用富文本编辑器编写消息以在表单提交时显示。 仅当您选择显示感谢消息时，此选项才可用。

## 嵌入自适应表单  {#aem-container-component}

使用 **[!UICONTROL 自适应Forms — 嵌入(V2)]** 组件，您可以在站点的页面中嵌入新的自适应表单或嵌入现有的自适应表单。 此 [!UICONTROL 自适应Forms — 嵌入(v2)] 组件允许您：

* [添加现有自适应表单](#embed-new-af)

* [创建和添加新的自适应表单](#embed-existing-af)

### 先决条件 {#prerequisites}

+++ 启用 **自适应Forms — 嵌入** 组件。

要启用 [!UICONTROL 自适应Forms — 嵌入(v2)] 组件时，请执行以下步骤：

1. 转到 [!UICONTROL 页面信息] > [!UICONTROL 编辑模板]

1. 单击 [!UICONTROL 策略] 并选择 **[!UICONTROL 自适应表单 — 嵌入(v2)]** 复选框 **[!UICONTROL [AEM原型项目名称] - FORMS]** 组。
1. 单击&#x200B;**[!UICONTROL 完成]**。

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ “将自适应Forms客户端库包含到AEM Sites”页面

当 **[!UICONTROL 当表单覆盖页面的整个宽度时]** 选项已选中以下项中的 **[!UICONTROL 表单容器]** “配置”对话框和 **使用核心组件的自适应Forms** 时，必须在相应的站点页面上包含clientlibs。

![叠加Gif](/help/forms/assets/overlaycorecomponent.gif)

要在AEM Sites页面中使用自适应Forms组件，请包含 `Customheaderlibs` 和 `Customfooterlibs` 使用AEM原型/Git存储库和部署管道将客户端库移至AEM Sites页面。

1. 打开您的 [AEM Forms原型或克隆的Git存储库](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 在文本编辑器中编辑项目。 例如，Visual Studio Code。
1. 导航到 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。
1. 复制的值 `sling:resourceSuperType`. 例如，值为 `core/wcm/components/page/v3/page`.

   ![Sling 资源](/help/forms/assets/slingresource.png)

1. 在该位置创建类似结构 `ui.apps/src/main/content/jcr_root/apps` 与 `core/wcm/components/page/v3/page`.

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

   此 `customfooterlibs.html` 用于JavaScript和 `customheaderlibs.html` 用于CSS。

1. [运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 以部署更改。

+++

### 将现有的自适应表单添加到AEM Sites页面 {#embed-existing-af}

1. 以编辑模式打开 AEM Sites 页面。
1. 在组件浏览器面板中，拖放 [!UICONTROL 自适应Forms — 嵌入] 组件。
1. 选择 [!UICONTROL 自适应Forms — 嵌入] 组件，然后选择 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) 在操作栏上。 此 **[!UICONTROL 编辑自适应Forms — 嵌入]** 对话框打开。
1. 浏览并选择要嵌入到中的自适应表单 [!UICONTROL 资产路径].
1. 保存设置。 现在，自适应表单已嵌入到页面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### “创建新的自适应表单并将其添加到AEM Sites”页面 {#embed-new-af}

1. 以编辑模式打开 AEM Sites 页面。
1. 在组件浏览器面板中，拖放 [!UICONTROL 自适应Forms — 嵌入(v2)] 组件。
1. 单击 **加号** 图标后，您将被重定向到表单创建向导。

   ![自适应Forms — 嵌入组件](/help/forms/assets/aemformcontainer.png)

1. 创建新的自适应表单 [!UICONTROL 表单创建] 向导。
1. 此 [!UICONTROL 资产路径] 已包含所创建自适应表单的路径
1. 保存设置。 现在，自适应表单已嵌入到页面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### 配置自适应表单 — 嵌入(v2)属性 {#configure-adaptive-form-embed}

您可以自定义的 [!UICONTROL 自适应表单 — 嵌入(v2)] 组件。 在 [!UICONTROL 编辑自适应Forms — 嵌入(v2)] 对话框，您可以指定以下内容。

* **资产路径**：浏览并选择要嵌入的自适应表单。 如果您将其从资产浏览器中删除，则会自动填充该变量。
* **帖子提交** ：选择在表单提交时触发的操作。 您可以选择显示感谢消息或感谢页面。
   * **显示感谢信息**：使用富文本编辑器编写消息以在表单提交时显示。 仅当您选择显示感谢消息时，此选项才可用。
   * **显示感谢页面**：浏览并选择要在表单提交时显示的页面。 仅当您选择显示感谢页面时，此选项才可用。
   * **重定向到感谢页面**：启用选项，将包含嵌入的自适应表单的页面替换为感谢页面。 否则，“感谢”页面将取代 [!UICONTROL 自适应Forms — 嵌入] 组件，无需刷新页面的基础站点。 仅当您选择显示感谢页面时，此选项才可用。
* **使用页面语言**：使用AEM Sites页面的本地，而不是自适应表单的区域设置。
* **设置专注于表单**：选择以将焦点设置为自适应表单的第一个字段。
* **表单覆盖框架的整个宽度**：如果选中，则不使用iframe渲染表单。
* **高度**：指定容器的高度。 将其留空可自动调整容器大小。
* **CSS客户端库**：指定CSS客户端库的路径。

### 发布添加了使用自适应表单的自适应Forms — 嵌入(v2)组件  {#publish-embedded-adaptive-form}

考虑以下场景以使用发布添加的自适应Forms **[!UICONTROL 自适应表单 — 嵌入(v2)]** 组件：

* 首次发布AEM Sites页面时，会自动发布添加到站点页面的表单。
* 在修改添加到已发布Sites页面的自适应表单时，手动发布相应的自适应Forms。
* 在修改Sites页面和相应的自适应Forms时，重新发布Sites页面以及添加到Sites页面的所有自适应Forms。

### 使用自适应表单 — 嵌入(v2)组件修改已添加的自适应Forms  {#modifying-embedded-adaptive-form}

要修改自适应表单的任何配置或属性，请执行以下操作之一：

* 在相应的编辑器中打开自适应表单中的原始表单，并修改它们。
* 在编辑模式下从网站页面中选择自适应表单，然后选择 **[!UICONTROL 在新窗口中编辑]**. 原始表单在编辑模式下打开，您可以修改该模式。

## 更改添加到AEM Sites页面中的自适应表单的布局 {#change-layout-af-aem-sites-page}

在AEM Sites页面中， [布局模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) 使您能够调整在AEM Sites页面上创建或添加的自适应表单的大小。

![AF布局支持](/help/forms/assets/afsite-layoutsupport.gif)

AEM sites页面维护对自适应表单的引用。 在翻译AEM Sites页面时，它将使用自动翻译自适应表单及其关联的引用资源 [翻译项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) 翻译成其他语言。

## 最佳实践 {#best-practices}

* 原始表单中的页眉和页脚未包含在嵌入表单中。
* 支持用户草稿和提交嵌入表单，这些草稿和提交表单会显示在Forms Portal的“草稿”和“已提交的Forms”选项卡中。

>[!MORELIKETHIS]
>
>* [将基于核心组件的自适应表单嵌入到外部网页](/help/forms/embed-adaptive-form-core-components-external-web-page.md)
>* [在外部网页中嵌入自适应表单](/help/forms/embed-adaptive-form-external-web-page.md)