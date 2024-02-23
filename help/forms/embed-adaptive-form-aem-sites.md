---
title: 如何将自适应表单添加到AEM Sites页面？
description: 将自适应Forms无缝嵌入到AEM Sites页面或AEM外部托管的网页中。
feature: Adaptive Forms
role: Admin, User, Developer
Keywords: Forms AEM Sites, Embed Form to a Sites page, Adaptive Forms AEM Sites, Embed Adaptive Forms to AEM Page, Embed Forms in an AEM Sites page
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '3145'
ht-degree: 5%

---

# 将自适应表单嵌入到AEM站点页面 {#embed-an-adaptive-form-to-aem-sites-page}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites.html) |
| AEM as a Cloud Service | 本文 |


## 概述 {#overview}

AEM Forms允许表单开发人员将自适应Forms无缝嵌入到AEM Sites页面或AEM外部托管的网页中。 嵌入式自适应表单功能齐全，用户无需离开页面即可填写和提交表单。 它有助于用户保留在网页上其他元素的上下文中，同时与表单交互。 这允许您的用户方便地填写和提交表单，而无需离开他们所在的页面。 此集成提供了一种便捷的方式，可重复使用他们已创建的自适应Forms。

您可以使用AEM页面编辑器快速将多个表单嵌入到AEM Sites页面。 通过使用AEM页面编辑器，内容创作者可以使用自适应Forms组件的强大功能（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化）在Sites页面中创建无缝的数据捕获体验。 它还允许您使用AEM Sites页面的各种功能，例如，版本控制、定位、翻译和多站点管理器。

AEM Forms提供 **[!UICONTROL 自适应表单容器]** 和 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 组件。 您可以使用 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 组件，用于添加现有的自适应表单或使用自适应Forms编辑器创建表单，而 **[!UICONTROL 自适应表单容器]** 在体验片段或AEM Sites页面中创建新表单。

![AEM Sites页面中的自适应表单示例](/help/forms/assets/adaptive-form-in-sites-page.png)

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). 

## Why embed an Adaptive Form in AEM Sites page or AEM Experience Fragment? 

Using **[!UICONTROL Adaptive Forms – Embed(v2)]** in AEM Page Editor lets you create seamless data capture experiences within a Sites page using the power of Adaptive Forms components including dynamic behavior, validations, data integration, generate document of record and business process automation. It also lets you use various features of AEM Sites pages like, versioning, targeting, translation, and multi-site manager, enhancing the overall form creation and management experience. Let's explore some of these features:

* **Versioning:** AEM Sites pages offer [robust versioning capabilities](/help/sites-cloud/authoring/sites-console/page-versions.md), allowing you to track and manage different versions of your forms. This enables you to make changes and enhancements to forms while maintaining the ability to roll back to previous versions if needed. Versioning ensures a controlled and organized approach to form development and evolution.
* **Targeting (Integration with Adobe Target):** With AEM Sites pages targeting capabilities, you can also [personalize the form experience for different audiences](/help/sites-cloud/integrating/integration-adobe-target-ims.md). By using user segments and targeting criteria, you can tailor the form's content, design, or behavior to specific groups of users. This enables you to provide a personalized and relevant form experience, increasing engagement and conversion rates.
* **Translation:** AEM Sites [seamless integration with translation services](/help/sites-cloud/administering/translation/overview.md), allowing you to translate forms into multiple languages easily. This feature simplifies the localization process, ensuring that your forms are accessible to a global audience. You can manage translations efficiently within AEM translation projects, reducing time and effort required for multilingual form support. See considerations section for more information on translation.  
* **Multi-site Management and Live Copy:** AEM Sites provide robust [Multi-site Management and Live Copy capabilities](/help/sites-cloud/administering/msm/overview.md), enabling you to create and manage multiple websites within a single environment. This feature now lets you reuse forms across different sites, ensuring consistency and reducing duplication efforts. With centralized control and management, you can efficiently maintain and update forms across multiple websites.
* **Themes:** AEM Sites pages provide a framework for designing and maintaining consistent visual styles across multiple web pages. These define colors, fonts, style sheets, and other visual elements that contribute to the overall look and feel of the website. [You can use the themes designed for an AEM Sites page for an Adaptive Form, saving time and effort](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes). 
* **Tagging:** AEM Sites pages allow you to [assign tags or labels to a page, an asset, or other content](/help/implementing/developing/introduction/tagging-framework.md). Tags are keywords or metadata labels that provide a way to categorize and organize content based on specific criteria. You can assign one or more tags to pages, assets, or any other content items within AEM to improve search and categorize the assets. 
* **Locking and Unlocking content:** AEM Sites allow users to [control access and modifications to pages](/help/sites-cloud/authoring/page-editor/edit-content.md) within the AEM Sites environment. When a page is locked, it means that it is protected from unauthorized changes or edits by other users. Only the user who has locked the content or a designated administrator can unlock it to allow modifications. 

In addition, Adaptive Forms in AEM Page Editor use [Adaptive Forms Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#features). These Core Components provide a standard and easier methods to style and customize the components, identical to [AEM Sites WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=en).

-->

## 如何在AEM Sites页面或AEM Experience Fragment中创建或嵌入自适应表单？ {#various-options-to-create-or-embed-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

您可以使用以下选项来充分利用此功能：

* **[使用批准的模板创建自适应表单并将其嵌入到AEM Sites页面](#embed-form-using-adaptive-form-wizzard-aem-sites)：** 您可以使用预批准的模板快速创建和嵌入符合您组织的品牌准则和设计标准的自适应Forms。

* **[将现有表单嵌入到AEM Sites页面](#embed-an-adaptive-form-in-sites-editor)：** 您可以将已创建的表单轻松集成到网站中，从而使访客能够直接与表单进行交互。

* **[将嵌入的自适应表单转换为体验片段](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)：** 将添加到AEM Sites页面的嵌入式自适应表单转换为体验片段，以便在多个AEM Sites页面中重用表单。

* **[创建自定义自适应表单并将其添加到AEM Sites页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor-or-experience-fragment)：** 您可以使用 **[!UICONTROL 自适应表单容器]** 从头开始构建全新表单的组件，根据您的要求和设计偏好对其进行定制。

* **[创建自定义自适应表单并将其添加到体验片段](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor)：** 您可以将表单添加到AEM体验片段中来扩展表单的影响范围，从而允许在多个页面或网站上无缝重用。

* **将多个表单添加到AEM Sites页面或体验片段：**  您可以在AEM Sites页面上创建或添加多个自适应Forms，以根据用户的偏好和要求为其提供多个选择。 您可以使用AEM页面编辑器快速将多个表单嵌入到AEM Sites页面。 您可以使用 **[!UICONTROL 自适应表单容器]** 多次组件，以在AEM Sites页面中添加自适应Forms。 您可以使用 **[!UICONTROL 自适应Forms — 嵌入]** 在AEM Sites页面中多次使用组件，仅当 **[!UICONTROL 表单覆盖框架的整个宽度]** 已选中选项。 如果 **[!UICONTROL 表单覆盖框架的整个宽度]** 选项未选中，AEM Sites页面仅支持一个不带iframe的自适应表单。 要添加更多自适应Forms，请使用 **[!UICONTROL 自适应Forms — 嵌入]** 组件，选择 **[!UICONTROL 表单覆盖框架的整个宽度]** 选项。

## 将自适应表单嵌入到AEM Sites页面或AEM Experience Fragment中的注意事项 {#consideration}

* 使用或添加表单时 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 表单的翻译和本地化过程均采用AEM Forms翻译流程。 在这种情况下，Sites 页面的所有语言副本中会维护和引用一个表单。**[!UICONTROL 自适应Forms — 嵌入(v2)]** 组件不提供对AEM Sites页面的各种功能（如版本控制、定位、翻译和多站点管理器）的访问权限。

* 当您使用 **[!UICONTROL 自适应表单容器]** 要创建表单，表单将通过AEM Sites翻译流程进行翻译和本地化。 对于每种语言，系统都会生成网站页面和相应表单的单独副本（语言副本），而当内容作者修改父页面上表单中的规则时，必须在该表单的所有语言副本中进行相同的更改。**[!UICONTROL 自适应表单容器]** 还允许您使用AEM Sites页面的各种功能，如，版本控制、定位、翻译和多站点管理器。


## 在AEM Sites页面或AEM Experience Fragment中嵌入自适应表单的要求 {#before-you-start-embedding-an-adaptive-form}

在开始嵌入新的自适应表单或预先存在的自适应表单之前，使用 **[!UICONTROL 自适应Forms — 嵌入(v2)]**，启用 **自适应Forms核心组件** 并添加 **自适应Forms客户端库** 转到您的AEM Sites页面：

+++  为您的AEM Cloud Service环境启用自适应Forms核心组件

确保 AEM Forms as a Cloud Service 环境已启用[自适应表单核心组件。](enable-adaptive-forms-core-components.md)

+++

+++  将自适应Forms客户端库添加到AEM Sites页面或体验片段

当 **[!UICONTROL 当表单覆盖页面的整个宽度时]** 选项已选中以下项中的 **[!UICONTROL 表单容器]** 由于使用了“配置”对话框和使用核心组件的自适应Forms，因此需要在相应的站点页面上包含客户端库。

![选择表单涵盖页面整个宽度选项并使用带有核心组件的自适应表单时](/help/forms/assets/overlaycorecomponent.gif)


添加 **Customheaderlibs** 和 **Customfooterlibs** 使用部署管道将客户端库连接到AEM Sites页面。 要添加客户端库，请执行以下操作：

1. 访问并克隆 [AEM Cloud Service Git 存储库。](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html)
1. 在计划文本编辑器中打开 AEM Cloud Service Git 存储库文件夹。例如，Microsoft® Visual Code。
1. 打开 `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` 文件并将以下代码添加到该文件中：

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. 打开 `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` 文件并将以下代码添加到该文件中：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. 打开 `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` 文件并将以下代码添加到该文件中：

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. 打开 `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` 文件并将以下代码添加到该文件中：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. [运行部署管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html)，将客户端库部署到 AEM as a Cloud Service 环境。

+++

+++ 启用 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 用于您的AEM Sites页面或体验片段

要启用 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 组件时，请执行以下步骤：

1. 打开AEM Sites页面或体验片段进行编辑。 要打开页面进行编辑，请选择该页面，然后单击 **[!UICONTROL 编辑]**.
1. 打开站点或体验片段页面的模板。 要打开模板，请转到&#x200B;**[!UICONTROL 页面信息]**![页面信息](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 编辑模板。]** 它会在模板编辑器中打开相应的模板。
1. 在结构视图中，单击菜单栏中的&#x200B;**[!UICONTROL 策略]**![策略](/help/forms/assets/Smock_FeedManagement_18_N.svg)图标。在 **[!UICONTROL 允许的组件]** 列出并选择 **[!UICONTROL 自适应Forms — 嵌入(v2)]**  复选框 **[AEM原型项目名称]  — 自适应表单**.
1. 单击&#x200B;**[!UICONTROL 完成]**。

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

## 使用自适应Forms — 嵌入(v2)组件嵌入自适应表单 {#embed-an-adaptive-form-in-sites-editor-or-experience-fragment}

使用 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 使用“表单创建向导”直接在AEM Sites编辑器中创建自适应表单的组件。 生成的表单将另存为外部实体，以便在其他Sites页面和独立表单中重复使用。 您可以直接从头开始在AEM Sites页面或体验片段中嵌入全新表单，根据您的要求和设计偏好设置专门定制表单。 对于一次性表单，建议直接创作到AEM Sites页面，而体验片段则适用于必须在网站上的多个页面中重用的表单。

您可以使用轻松嵌入新表单 **[!UICONTROL 自适应Forms — 嵌入(v2)]**.  例如，设想将新的联系我们表单合并到AEM Sites页面或AEM体验片段中。 对AEM Sites页面或体验片段中的联系人表单所做的任何更新或修改都会自动应用于部署该表单的所有页面。 这简化了对网站表单的管理，确保在简化整体过程的同时提供无缝的用户体验。

使用 **[!UICONTROL 自适应Forms — 嵌入(v2)]**，您可以：

* [“在AEM Sites中使用‘自适应Forms’向导嵌入新表单”页](#embed-form-using-adaptive-form-wizzard-aem-sites)
* [在体验片段中使用“自适应Forms向导”嵌入新表单](#embed-form-using-adaptive-form-wizzard-experience-fragment)
* [在AEM Sites页面中嵌入现有的自适应表单](#embed-an-adaptive-form-in-sites-editor)
* [在体验片段中嵌入现有表单](#embed-an-adaptive-form-in-experience-fragment)
* [将AEM Sites页面中的自适应表单转换为体验片段](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### “在AEM Sites中使用‘自适应Forms’向导嵌入新表单”页 {#embed-form-using-adaptive-form-wizzard-aem-sites}

将新表单嵌入到AEM Sites页面的步骤如下：

1. 以编辑模式打开 AEM Sites 页面。
1. 在组件浏览器面板中，拖放 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 组件。
1. 单击 **加号** 图标后，您将被重定向到表单创建向导。

   ![自适应Forms — 嵌入组件](/help/forms/assets/aemformcontainer.png)

1. 创建新的自适应表单 **[!UICONTROL 表单创建]** 向导。
此 **[!UICONTROL 资产路径]** 已包含所创建自适应表单的路径
1. 保存设置。 现在，自适应表单已嵌入到页面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

接下来，您可以 [设置提交操作](/help/forms/configuring-submit-actions.md) 使用表单创建向导创建嵌入式自适应表单的高级属性。


### 在体验片段中使用“自适应Forms向导”嵌入新表单 {#embed-form-using-adaptive-form-wizzard-experience-fragment}

将新表单嵌入到体验片段的步骤如下：

1. 在编辑模式下打开体验片段。
1. 在组件浏览器面板中，拖放 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 组件。
1. 单击 **加号** 图标后，您将被重定向到表单创建向导。

   ![自适应Forms — 嵌入组件](/help/forms/assets/aemformcontainer.png)

1. 创建新的自适应表单 **[!UICONTROL 表单创建]** 向导。
此 **[!UICONTROL 资产路径]** 已包含所创建自适应表单的路径
1. 保存设置。 自适应表单现在嵌入到体验片段中。

接下来，您可以 [设置提交操作](/help/forms/configuring-submit-actions.md) 使用表单创建向导创建嵌入式自适应表单的高级属性。

### 在AEM Sites页面中嵌入现有的自适应表单 {#embed-an-adaptive-form-in-sites-editor}

使用 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 将预先存在的自适应表单轻松集成到AEM Sites中的页面中。 此功能显着增强了自适应Forms的适应性和可重用性，为客户提供了重用他们已创建的表单的便捷方式。 例如，设想将联系人表单合并到AEM Sites页面，而无需多次重新创建表单。

要将现有的自适应表单嵌入到站点页面中，请执行以下操作：

1. 以编辑模式打开 AEM Sites 页面。
1. 拖放 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 组件从组件浏览器转到站点页面。
1. 选择 **[!UICONTROL 自适应Forms — 嵌入]** 组件，然后选择 ![自适应表单容器属性](/help/forms/assets/configure-icon.svg) 在操作栏上。 此 **[!UICONTROL 编辑自适应Forms — 嵌入(v2)]** 对话框打开。
1. 浏览并选择要嵌入到中的自适应表单 **[!UICONTROL 资产路径]**.
1. 保存设置。 现在，自适应表单已嵌入到页面中。

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

接下来，您可以 [设置提交操作](/help/forms/configuring-submit-actions.md) 使用表单创建向导创建嵌入式自适应表单的高级属性。

### 将现有的自适应表单嵌入到体验片段中 {#embed-an-adaptive-form-in-experience-fragment}

您还可以通过将表单嵌入到AEM体验片段来扩展表单的辅助功能。 要在体验片段中嵌入自适应表单，请执行以下操作：

1. 在编辑模式下打开体验片段。
1. 拖放 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 从组件浏览器到体验片段的组件。
1. 选择 **[!UICONTROL 自适应Forms — 嵌入]** 体验片段中的组件并选择 ![自适应表单容器属性](/help/forms/assets/configure-icon.svg) 在操作栏上。 此 **[!UICONTROL 编辑自适应Forms — 嵌入(v2)]** 对话框打开。
1. 浏览并选择要嵌入到中的自适应表单 **[!UICONTROL 资产路径]**.
1. 保存设置。 自适应表单现在嵌入到体验片段中。

接下来，您可以 [设置提交操作](/help/forms/configuring-submit-actions.md) 使用表单创建向导创建嵌入式自适应表单的高级属性。

### 将AEM Sites页面中的表单转换为体验片段 {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

您可以在站点页面编辑器中将现有的自适应表单转换为体验片段，以在多个页面或站点中重用该表单。

要将AEM Sites页面中的自适应表单转换为体验片段，请执行以下操作：

1. 在编辑模式下打开包含自适应表单的AEM Sites页面(在自适应Forms容器组件中)。
1. 打开内容树，然后选择 **[!UICONTROL 自适应Forms容器]** ，用于托管您的自适应表单。 一个AEM Sites页面可以托管多个自适应Forms。 因此，请仔细选择正确的自适应Forms容器。
1. 在菜单栏上，选择 ![“转换为体验片段变量”图标](/help/forms/assets/Smock_FilingCabinet_18_N.svg) “转换为体验片段变量”图标。

   ![单击文件柜徽标可将AEM Sites中的自适应表单页面转换为体验片段](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   出现一个对话框，用于将自适应表单容器转换为新的体验片段或添加到现有的体验片段。

1. 在 **[!UICONTROL 转换为体验片段]** 变体对话框中，为以下选项设置值：

   * **操作：** 选择以创建体验片段或添加到现有体验片段。
   * **父级路径：** 指定要承载体验片段的文件夹的路径。 选项仅适用于创建新体验片段。
   * **模板：** 指定体验片段模板的路径。 如果您没有体验片段模板， [创建它](/help/implementing/developing/extending/experience-fragments.md). 选项仅可用于将自适应表单添加到现有体验片段。
   * **片段标题：** 指定体验片段的标题。 标题唯一标识体验片段。
   * **片段标记：** 指定体验片段的标记。 标记唯一标识体验片段的类别。

## 配置自适应表单嵌入(v2)属性

您可以自定义的 **[!UICONTROL 自适应表单 — 嵌入(v2)]** 组件。 在 **[!UICONTROL 编辑自适应Forms — 嵌入]** 对话框，您可以指定以下内容：

* **资产路径**：浏览并选择要嵌入的自适应表单。 如果您将其从资产浏览器中删除，则会自动填充该变量。
* **帖子提交** ：选择在表单提交时触发的操作。 您可以选择显示感谢消息或感谢页面。
   * **显示感谢信息**：使用富文本编辑器编写消息以在表单提交时显示。 仅当您选择显示感谢消息时，此选项才可用。
   * **显示感谢页面**：浏览并选择要在表单提交时显示的页面。 仅当您选择显示感谢页面时，此选项才可用。
   * **重定向到感谢页面**：启用选项，将包含嵌入的自适应表单的页面替换为感谢页面。 否则，“感谢”页面将取代 **[!UICONTROL 自适应Forms — 嵌入(v2)]** 组件，无需刷新页面的基础站点。 仅当您选择显示感谢页面时，此选项才可用。
   * **感谢消息**：成功提交表单后屏幕上显示的简短确认或确认。
   * **“感谢”页面**：浏览并选择成功提交表单后显示的页面。

* **使用页面语言**：使用AEM Sites页面的本地，而不是自适应表单的区域设置。 此选项仅适用于自适应表单(Foundation)。
* **设置专注于表单**：选择以将焦点设置为自适应表单的第一个字段。 此选项仅适用于自适应表单(Foundation)。
* **主题**：选择用于定义自适应表单组件样式的主题。 样式设置包括外观属性，如字体样式、背景颜色、尺寸和对齐方式。 此选项仅适用于自适应表单(Foundation)。

  >[!NOTE]
  >
  > 您可以使用 **使用页面语言**， **设置专注于表单** 和 **主题** 仅自适应表单(Foundation)的选项。

* **表单覆盖框架的整个宽度**：内联框架(iframe)是一个HTML元素，用于将自适应表单加载到AEM Sites页面。

   * 如果 **[!UICONTROL 表单覆盖框架的整个宽度]** 如果选中复选框，则自适应表单会占据其所在的容器的整个宽度。 在这种情况下，不使用iframe呈现表单。 自适应表单的布局和设计可适应容器的整个宽度，使其响应速度快并可根据不同的屏幕大小进行调整。 利用此选项，您可以在AEM Sites页面中嵌入多个自适应Forms。

     >[!NOTE]
     >
     > 要在AEM Sites页面中嵌入多个表单，请选择 **[!UICONTROL 表单覆盖框架的整个宽度]** 复选框。

   * 如果 **[!UICONTROL 表单覆盖框架的整个宽度]** 复选框未选中，自适应表单不会覆盖容器的整个宽度。 而是使用iframe呈现表单，该表单不能扩展到超过特定宽度。 当自适应表单具有明确的边界并且必须在容器中与其旁边的其他AEM组件共存时，此方法很有用。 如果未选中此选项，则仅允许在AEM Sites中嵌入一个不带iframe的自适应Forms。

     >[!NOTE]
     >
     > AEM Sites页面仅支持一个不带iframe的自适应表单。 要添加更多自适应Forms，请使用 **[!UICONTROL 自适应Forms — 嵌入]** 组件，选择 **[!UICONTROL 表单覆盖框架的整个宽度]** 选项。

* **高度**：指定容器的高度。 将其留空可自动调整容器大小。
* **CSS客户端库**：指定CSS客户端库的路径。

<!--
In AEM Sites page, you can add an Adaptive Form using:

* **Adaptive Forms - Embed component**
   Adaptive Forms - Embed component enables AEM Sites authors to include an existing Adaptive Form within an AEM Sites page, thereby enhancing the reusability of adaptive forms. Existing Adaptive Forms can be used standalone or embedded in the site page. This integration provides a convenient way for customers to reuse Adaptive Forms they have already created.

* **Asset browser**
  All the forms are available under Assets. You can drag-drop the form as an asset on your page.

## Prerequisites {#prerequisites}

 To embed an Adaptive Form in an AEM Sites page that uses an editable template, ensure that the AEM Form component is configured as an allowed component in the associated template. 

In case **Adaptive Forms - Embed component** is not visible in the **Component browser panel** of AEM sites page, perform the following steps as illustrated in the video.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

In case Sites page is using a static template, you need to configure it in the paragraph system of the site page. 

## Embedding an Adaptive Form {#af-component}

To embed an Adaptive Form using the **[!UICONTROL Adaptive Forms - Embed]** component:

1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the [!UICONTROL Adaptive Forms - Embed] component on the page. Alternatively, you can search for an Adaptive Form in the Assets browser and drag-drop it onto the Sites page. You can add a new Adaptive Form or embed an existing Adaptive Form. 

   >[!NOTE]
   >
   >Multiple Adaptive Forms - Embed components on a page are not supported.

1. To create and embed a new form, on the component toolbar, select the **Create Form** icon. A window to create the form opens. 

1. Select the embedded Adaptive Forms - Embed component in the sites page, and then select ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit Adaptive Forms - Embed]** dialog opens.
1. In the Edit Adaptive Forms - Embed dialog, specify the following.

    **Asset Type:** Select the type of asset to embed. 
    * **Asset Path**: Browse and select the Adaptive Form to embed. It is auto-populated if you dropped it from the Assets browser.
    * **Post Submission** : Select the action to trigger on form submission. You can choose to show a thank you message or a thank you page.
        * Show

        * **Thank You Message**: Write a message using the rich text editor to show on form submission. This option is available only when you choose to show a thank you message.
        * **Thank You Page**: Browse and select the page to display on form submission. This option is available only when you choose to show a thank you page.
           * **Redirect to thank you page**: Enable the option to replace the page containing the embedded Adaptive Form with thank you page. Otherwise, the thank you page replaces the Adaptive Form in the [!UICONTROL Adaptive Forms - Embed] component, without refreshing underlying sites the page. This option is available only when you choose to show a thank you page.
    * **Use Page Language**: Use local of the AEM Sites page instead locale of Adaptive Form.
    * **Set Focus on Form**: Select to set the focus on the first field of the Adaptive Form.
    * **Theme**: Select a theme that defines styling for components of your Adaptive Form. Styling includes appearance properties such as font style, background color, dimensions, and alignment.
    * **Form covers entire width of the frame**: If checked, iframe is not used to render the form. 
    * **Height**: Specify the height of the container. Leave it blank to automatically resize the container.
    * **CSS Client library**: Specify path to a CSS client library.

1. Save the settings. The Adaptive Form  is now embedded in the page.


AEM site also lets you create an Adaptive Form on the fly using the Adaptive Forms - Embed component. Follow the steps to create an Adaptive Form using the **Adaptive Forms - Embed component** on AEM sites page:
1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the Adaptive Forms - Embed component on the page.
1. Click the **Plus** icon and you are redirected to the form creation wizard.

    ![Adaptive Forms - Embed Component](/help/forms/assets/aemformcontainer.png)

1. You can now embed an Adaptive Form on AEM site pages using the [!UICONTROL AEM Forms Container Component].
-->

## 发布嵌入式自适应表单 {#publishing-embedded-adaptive-form}

让我们考虑以下在AEM Sites页面中发布嵌入式自适应表单的场景：

* 如果您是首次发布AEM站点页面，并且它包含嵌入的自适应表单，请发布站点页面和嵌入的资产。
* 如果您在发布的站点页面中仅修改了嵌入的自适应表单，请发布原始资产，所做的更改会反映在发布的站点页面中。 已发布的站点页面包含对资产的引用，因此无需重新发布页面。
* 如果您修改了站点页面和嵌入的自适应表单，请重新发布站点页面和嵌入的资产。

## 修改嵌入式自适应表单  {#modifying-embedded-adaptive-form}

要修改嵌入式自适应表单的任何配置或属性，请执行以下操作之一。

* 在相应的编辑器中打开自适应表单中的原始表单，并修改它们。
* 在编辑模式下从网站页面中选择自适应表单，然后选择 **[!UICONTROL 在新窗口中编辑]**. 原始表单在编辑模式下打开，您可以修改该模式。

>[!NOTE]
>
>在原始自适应表单中所做的更改将自动反映在嵌入表单中。 但是，重新发布自适应表单或站点页面，以反映已发布页面中的更改。

## 最佳实践 {#best-practices}

在AEM Sites页面中嵌入自适应Forms时，请牢记以下几点：

* 原始表单中的页眉和页脚未包含在嵌入表单中。
* 支持用户草稿和提交嵌入表单，这些草稿和提交表单会显示在Forms Portal的“草稿”和“已提交的Forms”选项卡中。
* 在原始表单上配置的提交操作将保留在嵌入表单中。
* 如果您已为原始表单配置了Adobe Analytics，则会在Adobe Analytics中捕获嵌入表单的分析数据。 但是，它在Forms Analytics报表中不可用。

## 另请参阅 {#see-also}

* [创建基于核心组件的独立自适应Forms](/help/forms/creating-adaptive-form-core-components.md)
* [直接在AEM Sites页面中创建基于核心组件的自适应表单](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
