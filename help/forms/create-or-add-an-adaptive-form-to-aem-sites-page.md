---
title: 在AEM Sites页面中创建或添加自适应表单
description: 了解如何轻松地创建或无缝地将自适应表单添加到AEM Sites页面。 了解将动态和可自定义表单集成到网站中的分步技术和最佳实践，优化数字体验以发挥最大影响。
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---


# 在AEM Sites页面中创建或添加自适应表单 {#create-or-add-an-adaptive-form-to-aem-sites-page}

借助AEM Forms，您可以将自适应表单无缝地合并到网页中。 这样，您的访客便可以方便地填写和提交表单，而无需离开他们所在的页面。 这样，他们就可以轻松地与网站的其他元素保持接触，同时与表单进行积极互动。

您可以充分利用此功能，方法是使用以下选项：

* **添加自定义表单：** 从头开始构建全新的表单，根据您的要求和设计偏好进行定制。

* **增强体验片段：** 通过将表单添加到AEM Experience Fragments来扩展表单的覆盖范围，从而允许多个页面或站点无缝重用。

* **利用批准的模板：** 利用预批准的模板快速创建符合您组织的品牌准则和设计标准的表单。

* **添加现有表单：** 轻松地将您已创建的表单集成到网站中，使访客能够直接与表单进行交互。

* **添加多个表单：**  将多个表单添加到页面中，以根据用户的偏好和要求为其提供多个选择。 这些表单可以是全新表单和现有表单的组合。

您可以使用AEM Sites编辑器快速创建多个表单并将其添加到AEM Sites页面。 使用AEM Sites编辑器，内容创作者可以利用自适应表单组件的强大功能（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化），在Sites页面中创建无缝的数据捕获体验。 它还允许您使用AEM Sites页面的各种功能，例如，版本控制、定位、翻译和多站点管理器。

## 目标

* 了解如何使用AEM Sites编辑器和体验片段创建自适应表单
* 了解如何设置添加到AEM Sites页面的自适应表单的布局和主题，以及
* 使用AEM Sites编辑器和体验片段创建自适应表单


## 注意事项 {#consideration}

AEM Forms提供自适应表单容器和自适应Forms — 嵌入组件。 您可以使用自适应表单容器在体验片段或AEM Sites页面中创建和添加新表单，而自适应Forms — 嵌入组件允许您添加现有自适应表单或使用自适应Forms编辑器创建新表单。

使用自适应表单容器创建或添加表单时，表单会通过AEM Sites翻译流程进行翻译和本地化。 对于每种语言，都会生成站点页面和相应表单的单独副本（语言副本），当内容作者在父页面上的表单中修改规则时，必须在表单的所有语言副本中进行相同的更改。 自适应表单容器还允许您使用AEM Sites页面的各种功能，例如，版本控制、定位、翻译和多站点管理器。

使用自适应表单嵌入组件创建或添加表单时，将使用AEM Forms翻译流程翻译和本地化表单。 在这种情况下，将维护一个表单，并在站点页面的所有语言副本中引用该表单。 自适应表单嵌入组件不提供对AEM Sites页面的各种功能（如版本控制、定位、翻译和多站点管理器）的访问权限。


## 开始之前 {#before-you-start}

+++  为您的环境启用自适应Forms核心组件

确保 [已为您的AEM Formsas a Cloud Service环境启用自适应Forms核心组件](enable-adaptive-forms-core-components.md).

+++

+++ 启用**[!UICONTROL 自适应Forms容器]

启用 [!UICONTROL 自适应Forms容器] 组件时，请执行以下步骤：

1. 打开AEM Sites页面进行编辑。 要打开页面进行编辑，请选择该页面，然后单击编辑。
1. 打开站点页面的模板。 要打开模板，请转到 [!UICONTROL 页面信息] ![页面信息](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL 编辑模板]. 它会在模板编辑器中打开相应的模板。
1. 在“结构”视图中，单击 **[!UICONTROL 策略]** ![策略](/help/forms/assets/Smock_FeedManagement_18_N.svg) 图标。 在 **[!UICONTROL 允许的组件]** 列出并选择 **[!UICONTROL 自适应Forms容器]**  复选框。 **[AEM原型项目名称]  — 自适应表单**.
1. 单击 **[!UICONTROL 完成]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++


+++  将自适应Forms客户端库添加到AEM Sites页面

要启用自适应Forms容器组件的完整功能，请使用部署管道将Customheaderlibs和Customfooterlibs客户端库添加到AEM Sites页面。 要添加库，请执行以下操作：

1. 访问并克隆 [AEM Cloud Service Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. 在计划文本编辑器中打开AEM Cloud Service Git存储库文件夹。 例如，Microsoft Visual Code。
1. 打开 `ui.apps/src/main/content/jcr_root/apps/[your-project]/components/page/.content.xml` 文件以进行编辑并记下值 `sling:resourceSuperType`. 例如，记下值 `core/wcm/components/page/v3/page`.


   ![sling资源](/help/forms/assets/slingresource.png)

1. 导航到 `  ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\` `ui.apps/src/main/content/jcr_root/apps` 和创建一个与上一步中所述值相同的文件夹结构。 例如，如果值与上一步中的示例类似，则最终节点结构为 `ui.apps/src/main/content/jcr_root/apps/core/wcm/components/page/v3/page`

   ![叠加结构](/help/forms/assets/overlaystructure.png)

1. 创建 `customheaderlibs.html` 和 `customfooterlibs.html` 在节点结构中创建的文件，并将以下内容添加到文件中：

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

1. [运行部署管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 以将客户端库部署到您的AEMas a Cloud Service环境。

+++

## 创建自适应表单 {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

您可以从头开始创建全新的表单，直接在AEM站点页面或体验片段中根据您的要求和设计偏好设置对其进行专门定制。 对于一次性表单，建议直接创作到AEM站点页面，而体验片段适用于需要在网站上的多个页面中重用的表单。

* [在AEM Sites页面中创建表单](#create-an-adaptive-form-in-sites-editor)
* [在体验片段中创建表单](#create-an-adaptive-form-in-experience-fragment)

### 在AEM Sites页面中创建表单 {#create-an-adaptive-form-in-sites-editor}

您可以使用AEM Sites编辑器中的自适应表单容器组件来创建自定义表单。 利用组件，可通过拖放表单组件来创建表单。 表单组件基于核心组件。 您可以根据贵组织的要求轻松自定义这些内容。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

要在站点页面中创建自适应表单，请执行以下操作：

1. 在编辑模式下打开AEM Sites页面。
1. 拖放 **[!UICONTROL 自适应Forms容器]** 组件浏览器中的组件移至“站点”页面。 它会在页面上为表单创建一个空间。 您可以使用布局模式更改容器空间的大小。
1. 将自适应表单核心组件拖放到容器空间以创建表单。
1. 添加“提交”按钮。

接下来，设置“提交”操作和高级属性。

### 在体验片段中创建表单 {#create-an-adaptive-form-in-experience-fragment}

您可以将表单添加到AEM体验片段来扩展表单的覆盖范围，从而允许跨多个页面或站点无缝重用。 例如，您可以在体验片段中包含新闻稿注册表单。 这使您能够方便地在网站的多个页面中重用片段，而无需重复重新创建表单。 在体验片段中对新闻稿注册表单所做的任何更新或修改都会自动传播到所有使用它的页面。 这简化了流程，并确保了无缝的用户体验，同时简化了网站表单的管理。

要在体验片段中创建自适应表单，请执行以下操作：

## 更改自适应表单的布局 {#change-layout-of-an-adaptive-form}

在AEM Sites页面中，使用 [布局模式](/help/sites-cloud/authoring/features/responsive-layout.md) 调整添加到AEM Sites页面中的自适应表单容器组件的大小。
