---
title: 如何基于核心组件或 Edge Delivery Services 模板创建独立表单并将其发布到 Edge Delivery Services 上
description: 本文介绍如何通过在表单创建向导中选择一个基于核心组件或基于 Edge Delivery Services 的模板来创建自适应表单。您还可以将表单发布到 AEM Edge Delivery Services。
feature: Edge Delivery Services
role: User
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: e2ea802856a2fbab90d4ddb1ecf7280ce789d59c
workflow-type: ht
source-wordcount: '1626'
ht-degree: 100%

---


# 从创作到发布：Edge Delivery Services 上的 AEM 表单

<span class="preview"> 此功能通过早期访问计划提供。要请求获得访问权限，请通过您的官方地址向 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> 发送电子邮件，并附上您的 GitHub 组织名称和存储库名称。例如，如果存储库 URL 为 https://github.com/adobe/abc，则组织名称为 adobe，存储库名称为 abc。</span>

Adobe Experience Manager (AEM) 可让您创建引人入胜的响应式动态表单。它提供多种创作方法，每种方法都适合不同的要求和用户专业知识水平。&#x200B;

本文重点介绍在 AEM 环境中创作表单并通过 Edge Delivery Services 发布的方法。使用基于核心组件的模板构建的表单可以在 AEM 和 Edge Delivery Services 上发布，从而提供部署灵活性。相比之下，使用基于 Edge Delivery Services 的模板创作的表单只能在 Edge Delivery Services 上发布。&#x200B;

![创作和发布自适应表单](/help/edge/docs/forms/universal-editor/assets/author-publish-af.png){width=50% align=center}

## 在 AEM 中创作表单并使用 Edge Delivery Services 发布的优势：

* **保留现有的 AEM 工作流**：组织可以继续使用其已建立的 AEM 工作流和治理结构，确保对内容创建的控制及其一致性。&#x200B;

* **增强性能**：通过 Edge Delivery Services 发布可以加快渲染时间，改善用户体验，减少页面加载时间。&#x200B;

* **改进 SEO**：Edge Delivery Services 旨在提供具有 Google Lighthouse 高评分的内容，从而实现更好的搜索引擎优化并提高可见性。&#x200B;

* **灵活的部署选项**：使用核心组件构建的表单可以在 AEM 和 Edge Delivery Services 上发布，从而提供部署策略方面的灵活性。

## 开始之前

在 AEM 中开始创作表单并通过 Edge Delivery Services 发布表单之前，请确保满足以下先决条件：

* 确保您已为 Edge Delivery Services 配置了 Github 存储库。
   * 如果您没有存储库，[预先配置了自适应表单块的新 AEM 项目](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。
   * 如果您有存储库，请将自适应表单块添加到您现有的存储库。详细说明请参阅[适用于 AEM 表单 的 Edge Delivery Services 入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)。
* 在您的 AEM 环境和 GitHub 存储库之间建立连接。[怎么做？](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)

指导进行自适应表单设置和发布的决策流程图：

![Github 存储库工作流](/help/forms/assets/repo-workflow.png){width=auto}

## 在 AEM 中创作表单并将其发布到 Edge Delivery Services

请按照以下步骤在 AEM 中创作表单并将其发布到 Edge Delivery Services：

[1. 选择一个模板，创建表单](#choose-a-template-and-create-the-form)

[2. 创作表单](#author-the-form)

[3. 发布表单](#publish-a-form)

### 选择一个模板，创建表单

您可以在 AEM 实例上创建表单，然后使用以下方式发布到 Edge Delivery Services：

>[!BEGINTABS]

>[!TAB 基于 Edge Delivery Services 的模板]

执行以下步骤来选择模板并创建表单：

1. 登录您的 AEM Forms as a Cloud Service 作者实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应表单]**。向导随即打开。
1. 在&#x200B;**源**&#x200B;选项卡中，选择一个&#x200B;**基于 Edge Delivery Services 的模板**：

   ![创建 EDS 表单](/help/edge/assets/create-eds-forms.png)

   选择&#x200B;**基于 Edge Delivery Services 的模板**&#x200B;后，**[!UICONTROL 创建]**&#x200B;按钮就被启用。
1. （可选）在&#x200B;**[!UICONTROL 数据源]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡中，您可以选择数据源或提交操作。
1. （可选）在&#x200B;**[!UICONTROL 投放]**&#x200B;选项卡中，您可以为表单指定发布或取消发布日期。
1. 点击&#x200B;**[!UICONTROL 创建]**，会出现&#x200B;**创建表单**&#x200B;向导：

   1. 指定&#x200B;**名称**&#x200B;和&#x200B;**标题**。
   1. 指定 **GitHub URL**。例如，如果您的 GitHub 存储库名为 `edsforms`，则它位于帐户 `wkndforms` 下，其 URL 为：
      `https://github.com/wkndforms/edsforms`

   ![创建表单向导](/help/edge/assets/create-form-wizard.png)

   单击&#x200B;**[!UICONTROL 创建]**&#x200B;后，表单就会在通用编辑器中打开以供创作。

   ![创作表单](/help/edge/assets/author-form.png)
1. 点击&#x200B;**[!UICONTROL 创建]**，创建表单。现在，您可以[使用通用编辑器创作表单](#author-the-form)。

>[!TAB 基于核心组件的模板]

执行以下步骤来选择模板并创建表单：

1. 登录您的 AEM Forms as a Cloud Service 作者实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应表单]**。向导随即打开。
1. 在&#x200B;**源**&#x200B;选项卡中选择一个&#x200B;**基于核心组件的模板**&#x200B;和一个&#x200B;**主题**，**[!UICONTROL 创建]**&#x200B;按钮就会启用。

   ![基于核心组件的模板](/help/forms/assets/core-component-based-template.png)

1. （可选）在&#x200B;**[!UICONTROL 数据源]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡中，您可以选择数据源或提交操作。
1. （可选）在&#x200B;**[!UICONTROL 投放]**&#x200B;选项卡中，您可以为表单指定发布或取消发布日期。
1. 点击&#x200B;**[!UICONTROL 创建]**，会出现&#x200B;**创建表单**&#x200B;向导：
   1. 指定&#x200B;**名称**&#x200B;和&#x200B;**标题**。
   1. 在&#x200B;**路径**&#x200B;字段中指定自适应表单的保存位置。

   ![创建表单向导](/help/forms/assets/create-cc-form.png)

   点击&#x200B;**[!UICONTROL 创建]**，表单就会在自适应表单编辑器中打开以供创作。

   ![自适应表单编辑器](/help/forms/assets/af-editor-form.png)

1. 点击&#x200B;**[!UICONTROL 创建]**，创建表单。现在，您可以[使用自适应表单编辑器创作表单](#author-the-form)。

>[!ENDTABS]

### 创作表单

使用基于 Edge Delivery Services 的模板创建的表单可以在[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)中打开进行创作。但是，使用基于核心组件的模板创建的表单会在自适应表单编辑器中打开以供创作。

执行以下步骤，为基于 Edge Delivery Services 的模板使用通用编辑器或为基于核心组件的模板使用自适应表单编辑器来创作表单：

>[!BEGINTABS]

>[!TAB 基于 Edge Delivery Services 的模板]


1. 打开内容浏览器，然后导航到&#x200B;**内容树**&#x200B;中的&#x200B;**[!UICONTROL 自适应表单]**&#x200B;组件。

   ![内容树](/help/edge/assets/content-tree.png)

1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标，然后从&#x200B;**自适应表单组件**列表中添加所需的组件。
   ![添加组件](/help/edge/assets/add-component.png)

   下面的屏幕快照显示了在通用编辑器中创作的 `Registration Form` 表单：

   ![联系我们表单](/help/edge/assets/contact-us.png)

>[!NOTE]
>
> 有关使用通用编辑器创作自适应表单的详细说明，[请点击此处](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

您现在可以[配置和自定义表单的提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)。

>[!TAB 基于核心组件的模板]

1. 点击&#x200B;**将组件拖放至此**&#x200B;部分中的&#x200B;**[!UICONTROL 插入组件]**。

   ![将组件拖放至此](/help/forms/assets/drag-components-af-editor.png)

1. 从&#x200B;**自适应表单组件**&#x200B;列表中添加所需的组件。

   ![添加组件](/help/forms/assets/add-component-af.png)

下面的屏幕快照显示了在自适应表单编辑器中创作的 `Enrollment Form` 表单：

![自适应表单编辑器](/help/forms/assets/af-editor-form.png)

>[!NOTE]
>
> 有关基于核心组件的模板创建自适应表单的详细说明，[请点击此处](/help/forms/creating-adaptive-form-core-components.md)。

您现在可以[配置表单提交操作](/help/forms/configure-submit-actions-core-components.md)。

>[!ENDTABS]

### 发布该表单

要在 Edge Delivery Services 上发布自适应表单，您需要[在 AEM 实例上创建 Edge Delivery Services 配置](#create-an-edge-delivery-services-configuration)。

#### 创建 Edge Delivery Services 配置

执行以下步骤来创建 Edge Delivery Services 配置：

>[!BEGINTABS]
>[!TAB 基于 Edge Delivery Services 的模板]


基于 Edge Delivery Services 模板的表单的 Edge Delivery Services 配置会在表单的配置容器中自动创建。

![Edge Delivery Services 配置](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB 基于核心组件的模板]

1. 导航至 AEM Forms as a Cloud Service 作者实例上的&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Edge Delivery Services 配置]**。

   ![选择 Edge Delivery Services 配置](/help/edge/assets/select-eds-conf.png)

2. 选择与表单名称匹配的文件夹。例如，如果您的表单名为 `enrollment-form`，请选择文件夹 `forms/enrollment-form`，然后点击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 配置]**：

   ![Edge Delivery Services 配置](/help/forms/assets/create-eds-conf.png)

3. 点击 **[!UICONTROL Edge Delivery Services 配置]**，然后点击&#x200B;**[!UICONTROL 属性]**，打开属性：

   ![自动创建的配置](/help/forms/assets/eds-conf.png)

   Edge Delivery Services 配置出现。

4. 在 Edge Delivery Services 配置中指定以下各项：

   * **组织**：指定您的 GitHub 组织名称。

   * **站点名称**：指定您的 GitHub 存储库名称。
   * **分支**：指定分支名称。如果使用主分支，请将该文本框留空。
   * **（可选）Edge Host**：将 Edge Host 选项保留原样。表单被发布到预览（.page）和实时（.live）两个环境。
   * **（可选）站点身份验证令牌**：使用站点身份验证令牌安全地验证 AEM 实例和 Edge Delivery Services 之间的请求。

5. 选择&#x200B;**[!UICONTROL 保存并关闭]**。现在创建配置。

>[!ENDTABS]

#### 在 Edge Delivery Services 上访问表单

要访问 Edge Delivery Services 上的表单，必须发布该表单。执行以下步骤来发布表单：

>[!BEGINTABS]
>[!TAB 在通用编辑器上]

1. 点击通用编辑器右上角的&#x200B;**[!UICONTROL 发布]**&#x200B;按钮发布表单。

![发布表单](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> 请参阅[发布和部署](/help/edge/docs/forms/universal-editor/publish-forms.md)一文，了解如何将表单发布到 Edge Delivery Services。

>[!TAB 在自适应表单编辑器上]

1. 从 Experience Manager Forms 控制台导航到父级文件夹，然后选择要发布的表单。

1. 点击工具栏中的&#x200B;**[!UICONTROL 发布]** 选项，查看将随表单发布的所有引用资产。

![在自适应表单编辑器上发布表单](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> 请参阅[在 Experience Manager Forms 中管理发布](/help/forms/manage-publication.md)文章，了解如何在自适应表单编辑器上发布表单。

>[!ENDTABS]

* **暂存版本（用于测试）**：暂存版本显示的是表单的未发布工作版本，用于测试目的。在表单上线前，请使用以下 URL 格式预览表单：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`



* **实时版本（已发布的表单）**：实时版本显示表单的最新发布版本，可供最终用户访问。使用以下 URL 格式访问已发布的表单实时版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  暂存版本和实时版本的 URL 结构相同。不过，根据上下文的不同，您看到的内容也有所不同。

以下屏幕快照比较了使用基于 Edge Delivery Services 和基于核心组件的模板创建的表单的暂存及实时表单 URL 以及视觉预览：

>[!BEGINTABS]
>[!TAB 基于 Edge Delivery Services 的模板]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
    <tr>
      <th style="width: 20%;"><strong>版本</strong></th>
      <th style="width: 80%;"><strong>图像</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>暂存版本</td>
      <td><img src="/help/forms/assets/registration-form-staged-version.png" alt="注册表单暂存版本" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>实时版本</td>
      <td><img src="/help/forms/assets/registration-form-live-version.png" alt="注册表单实时版本" style="width: 100%; height: auto;" /></td>
    </tr>
    </tbody>
  </table>

>[!TAB 基于核心组件的模板]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="width: 20%;"><strong>版本</strong></th>
      <th style="width: 80%;"><strong>图像</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>暂存版本</td>
      <td><img src="/help/forms/assets/enrollment-form-staged-version.png" alt="登记表单暂存版本" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>实时版本</td>
      <td><img src="/help/forms/assets/enrollment-form-live-version.png" alt="登记表单实时版本" style="width: 100%; height: auto;" /></td>
    </tr>
  </tbody>
  </table>

>[!ENDTABS]

## 疑难解答

是否在加载表单时遇到了问题？以下是一些常见问题及其解决方法：

* **表单 URL**：仔细检查表单的 URL 末尾是否包含 “.html” 扩展名。Edge Deliver Service 不需要此扩展名。

* **AEM 作者 URL**：确保 `fstab.yaml` 文件中列出的 AEM 作者 URL 格式正确。它应包括以下详细信息：

   * 正确的 GitHub 所有者
   * 正确的存储库名称
   * 用于 Edge Delivery Services 的特定分支

## 开始创建表单

{{universal-editor-see-also}}

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.

### Managing a form

You can perform several operations on form using the AEM Forms user interface.

1. Login into your AEM Forms as a Cloud Service author instance.
1. Select **[!UICONTROL Adobe Experience Manager]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Forms & Documents]**.

1. Select a form and the toolbar displays the following operations you can perform on the selected form.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operation</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>Edit</p> </td>
   <td><p>Opens the form in edit mode.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Properties</p> </td>
   <td><p>Provides options to modify the properties of the form.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copy</p> </td>
   <td><p> Provides options to copy the form  and paste it at the desired location. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Preview</p> </td>
   <td><p>Provides options to preview the form as HTML or perform a custom preview by merging data from an XML file with the form. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Downloads the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Start Review/Manage Review</p> </td>
   <td><p>Allows initiating and managing a review of the selected form.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publish / Unpublish</p> </td>
   <td><p>Publishes / unpublishes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Delete</p> </td>
   <td><p>Deletes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Compare</p> </td>
   <td><p>Compares two different form for previewing purposes.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table> 


## How Edge Delivery Services Forms Work?

Users can author Edge Delivery Services Forms using document-based authoring tools such as Google Drive, SharePoint, or the Universal Editor (WYSIWYG authoring), while leveraging the basic styling, behaviour and components available in the GitHub repository. Once authored, Edge Delivery Services Forms can send data to any platform using the Forms Submission Service.

![How Edge Delivery Services Forms works](/help/edge/docs/forms/assets/eds-forms-working.png)

### Key components of Edge Delivery Services Forms

The key components of Edge Delivery Servies Forms are:

* **GitHub Repository**: The GitHub repository serves as a boilerplate for creating Edge Delivery Services Forms. The forms leverage basic styling and functionality from the repository and allow users to add customizations and custom components to the Edge Delivery Services Forms.

* **Form Authoring**: Edge Delivery Services Forms support two types of authoring: WYSIWYG and document-based authoring. Document-based authoring enables users to create forms using familiar tools like Google Docs and Microsoft Office. WYSIWYG authoring allows users to design forms visually using the Universal Editor, making it easy for non-technical users to create and manage forms. Universal Editor offers an intuitive form creation experience and provides access to numerous form capabilities.

* **Forms Submission Service**: The Forms Submission Service allows you to store data from forms submissions on any platform, such as OneDrive, SharePoint, or Google Sheets, making it easy to access and manage form data within your preferred system.-->
