---
title: 如何使用通用编辑器基于Edge Delivery Services模板创建独立表单？
description: 本文介绍了如何使用通用编辑器通过在“表单创建向导”中选择基于Edge Delivery Services的模板来创建表单。 您还可以将表单发布到AEM Edge Delivery Services。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 979aad24ebbd0ef1d4d1fc92d402fca20bc27a44
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 83%

---

# 在通用编辑器中创建独立表单的分步指南

<span class="preview"> 此功能通过早期访问计划提供。要请求获得访问权限，请通过您的官方地址向 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> 发送电子邮件，并附上您的 GitHub 组织名称和存储库名称。例如，如果存储库 URL 为 https://github.com/adobe/abc，则组织名称为 adobe，存储库名称为 abc。</span>

通过从“表单创建向导”中选择基于Edge Delivery Services的模板，本文指导您完成使用通用编辑器创建和创作独立表单的过程。 您还可以使用通用编辑器将创作的表单发布到 AEM Edge Delivery Services。

AEM Forms 提供 Adaptive Forms Block，可帮助您轻松创建 Edge Delivery Services Forms，以捕获和存储数据。您可以[创建预先配置了 Adaptive Forms Block 的新 AEM 项目](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)或[将 Adaptive Forms Block 添加到现有的 AEM Site 项目](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)。

![Github 存储库工作流](/help/edge/assets/repo-workflow.png)

## 先决条件

* [设置您的 GitHub 存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，以在您的 AEM 环境和 GitHub 存储库之间建立连接。
* 如果您已经在使用 Edge Delivery Services，请将最新版本的 [Adaptive Forms Block](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) 添加到您的 GitHub 存储库。
* AEM Forms 作者实例包含一个基于 Edge Delivery Services 的模板。确保您的环境中安装了[最新版本的核心组件](https://github.com/adobe/aem-core-forms-components)。
* 保存 AEM Forms as a Cloud Service 作者实例的 URL 和您方便的 GitHub 存储库。

## 在通用编辑器中处理表单

使用通用编辑器，您可以使用现成的组件（如文本字段、复选框和单选按钮）轻松创建响应式交互表单。它提供了诸如动态规则、流畅的数据集成和自定义选项等强大功能，允许您根据确切要求构建表单。 您还可以将表单发布到AEM Edge Delivery Services。 您可以在通用编辑器中对表单执行以下操作：
* [创建表单](#create-a-form)
* [创作表单](#author-a-form)
* [发布表单](#publish-a-form)
* [管理表单](#manage-a-form)

>[!NOTE]
>
> 您还可以[使用通用编辑器中的 Edge Delivery Services Site 模板在 AEM Site 中创作表单，并将其发布到 Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project)。


### 创建表单

1. 登录您的 AEM Forms as a Cloud Service 作者实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应表单]**。向导随即打开。
1. 在&#x200B;**源**&#x200B;选项卡中，选择基于 Edge Delivery Services 的表单模板：

   ![创建 EDS 表单](/help/edge/assets/create-eds-forms.png)


   选择基于 Edge Delivery Services 的模板后，**[!UICONTROL 创建]**&#x200B;按钮就被启用。
1. （可选）在&#x200B;**[!UICONTROL 数据源]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡中，您可以选择数据源或提交操作。
1. （可选）在&#x200B;**[!UICONTROL 交付]**&#x200B;选项卡中，您可以为表单指定发布或取消发布日期。

1. 单击&#x200B;**[!UICONTROL 创建]**，将出现&#x200B;**创建表单**&#x200B;向导。
1. 指定&#x200B;**名称**&#x200B;和&#x200B;**标题**。
1. 指定 **GitHub URL**。例如，如果您的 GitHub 存储库名为 `edsforms`，则它位于帐户 `wkndforms` 下，其 URL 为：
   `https://github.com/wkndforms/edsforms`
1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![创建表单向导](/help/edge/assets/create-form-wizard.png)

   单击&#x200B;**[!UICONTROL 创建]**&#x200B;后，表单就会在通用编辑器中打开以供创作。

   ![创作表单](/help/edge/assets/author-form.png)

   <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

   单击&#x200B;**[!UICONTROL 创建]**&#x200B;后，表单就会在通用编辑器中打开以供创作。

### 创作表单

1. 打开内容浏览器，然后导航到&#x200B;**内容树**&#x200B;中的&#x200B;**[!UICONTROL 自适应表单]**&#x200B;组件。

   ![内容树](/help/edge/assets/content-tree.png)

1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标，然后从&#x200B;**自适应表单组件**&#x200B;列表中添加所需的组件。

   ![添加组件](/help/edge/assets/add-component.png)

1. 选择添加的自适应表单组件，并使用&#x200B;**[!UICONTROL 属性]**&#x200B;更新其属性。

   ![打开属性](/help/edge/assets/component-properties.png)

   下面的屏幕快照显示了在通用编辑器中简单的创作 `Registration Form` 表单：

   ![联系我们表单](/help/edge/assets/contact-us.png)

   现在您可以[配置和自定义表单提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)。


<!--
## **Edge Delivery Services configuration of form**



   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Edge Delivery Services Configuration]** on your AEM Forms as a Cloud Service author instance.

        ![Select Edge Delivery Services Configuration](/help/edge/assets/select-eds-conf.png)
   1. Select the folder that matches the form's name. For example, if your form is called 'registration-form' choose the folder `forms/registration-form` and selct the configuration and publish the configuration:

        ![Edge Delivery Services Configuration](/help/edge/assets/aem-instance-eds-configuration.png)

   1. Click **[!UICONTROL Properties]** to see the configuration.   
        ![Automatically created configuration](/help/edge/assets/aem-forms-create-configuration-github.png)

        You can leave the Edge Host option as it is. The form would be published to both preview (.page) and live (.live) environments. 

   1. Click **[!UICONTROL Save and Close]**. The configuration is saved. -->

### 发布表单

现在，单击通用编辑器右上角的&#x200B;**[!UICONTROL 发布]**&#x200B;按钮将独立表单发布到 Edge Delivery Services。

![发布表单](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> 请参阅[发布和部署](/help/edge/docs/forms/universal-editor/publish-forms.md)一文，了解如何将表单发布到 Edge Delivery Services。

以下是如何在 Edge Delivery Services 上访问表单的方法：

* **暂存版本（用于测试）**：暂存版本显示的是表单的未发布工作版本，用于测试目的。在表单上线前，请使用以下 URL 格式预览表单：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例如，如果您的项目存储库名为 “edsforms” 且位于帐户 “wkndforms” 下，并且您使用的是 “main” 分支和“注册表单”表单，则暂存版本 URL 如下所示：
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **实时版本（已发布的表单）**：实时版本显示表单的最新发布版本，可供最终用户访问。使用以下 URL 格式访问已发布的表单实时版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例如，如果您的项目存储库名为 “edsforms” 且位于帐户 “wkndforms” 下，并且您使用的是 “main” 分支和“注册表单”表单，则暂存版本 URL 如下所示：
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

暂存版本和实时版本的 URL 结构相同。不过，根据上下文的不同，您看到的内容也有所不同：

![查看已发布的表单](/help/edge/assets/eds-view-publish-form.png)

### 管理表单

您可以使用 AEM Forms 用户界面对表单执行多项操作。

1. 登录您的 AEM Forms as a Cloud Service 作者实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。

1. 选择一个表单，工具栏就会显示您可以在所选表单上执行以下操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>编辑</p> </td>
   <td><p>在编辑模式中打开表单。<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>属性</p> </td>
   <td><p>提供更改表单属性的选项。<br /> <br /> </p> </td>
  </tr>
  <td><p>复制</p> </td>
   <td><p> 提供复制表单并将其粘贴到所需位置的选项。<br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>预览</p> </td>
   <td><p>提供以 HTML 格式预览表单或通过将某个 XML 文件中的数据与表单合并来执行自定义预览的选项。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>下载</p> </td>
   <td><p>下载选定的表单。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>开始审阅/管理审阅</p> </td>
   <td><p>允许启动和管理对所选表单的审阅。<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>-->
  <tr>
   <td><p>发布/取消发布</p> </td>
   <td><p>发布/取消发布选定的表单。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>删除</p> </td>
   <td><p>删除选定的表单。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>比较</p> </td>
   <td><p>比较两个不同的表单用于预览。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 疑难解答

是否在加载表单时遇到了问题？以下是一些常见问题及其解决方法：

* **表单 URL**：仔细检查表单的 URL 末尾是否包含 “.html” 扩展名。Edge Deliver Service 不需要此扩展名。

* **AEM 作者 URL**：确保 `fstab.yaml` 文件中列出的 AEM 作者 URL 格式正确。它应包括以下详细信息：

   * 正确的 GitHub 所有者
   * 正确的存储库名称
   * 用于 Edge Delivery Services 的特定分支

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## 开始创建表单

{{universal-editor-see-also}}
