---
title: 如何使用通用编辑器创建独立的自适应表单？
description: 本文介绍如何使用 AEM 作者实例中的表单创建向导创建自适应表单，并将表单发布到 AEM Edge Delivery Services。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 3db311812f6c4521baf1364523a0e0b1134fee65
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 83%

---

# 使用通用编辑器（所见即所得）创作独立表单

<span class="preview"> 此功能通过早期访问计划提供。要请求获得访问权限，请通过您的官方地址向 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> 发送电子邮件，并附上您的 GitHub 组织名称和存储库名称。例如，如果存储库 URL 为 https://github.com/adobe/abc，则组织名称为 adobe，存储库名称为 abc。</span>

本文将指导您通过从表单创建向导中选择基于 Edge Delivery Services 的模板，使用通用编辑器创作独立表单的过程。您还可以使用通用编辑器将创作的表单发布到 AEM Edge Delivery Services。

<!--To publish forms to Edge Delivery Services, you must first establish a connection between your AEM environment and your GitHub repository. Once connected, you can author the forms using the Universal Editor, which follows a WYSIWYG (What You See Is What You Get) approach for a seamless and consistent user experience with Sites.-->

在开始之前，了解可使用的表单组件类型：

* [Edge Delivery Services for AEM Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) 是一组可组合的服务，可用于实现快速开发环境，作者可以使用通用编辑器在其中快速更新、发布和启动新表单。通用编辑器通过用户友好的可视化所见即所得界面简化了 Adobe Edge Delivery Services 的表单创建。

* [自适应表单核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)：这些是标准化的数据捕获组件。对于您的数字注册体验，这些组件可以提供定制功能，缩短开发时间和降低维护成本。开发人员可以轻松地自定义这些组件并设置其样式。您可以访问 [https://aemcomponents.dev/](https://aemcomponents.dev/) 以查看可用核心组件的实际操作&#x200B;**Adobe 建议使用这些现代的、可扩展组件来开发自适应表单**。

* [自适应表单基础组件](/help/forms/creating-adaptive-form.md)：这些是经典（旧版）数据捕获组件。您可以继续使用这些组件来编辑您现有的基于基础组件的自适应表单。如果您正在创建新表单，Adobe 建议使用[用于创建自适应表单的自适应表单核心组件](#create-an-adaptive-form-core-components)。

AEM Forms 提供 Adaptive Forms Block，可帮助您轻松创建 Edge Delivery Services Forms，以捕获和存储数据。您可以[创建预先配置了 Adaptive Forms Block 的新 AEM 项目](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)或[将 Adaptive Forms Block 添加到现有的 AEM Site 项目](#add-adaptive-forms-block-to-your-existing-aem-project)。

![Github 存储库工作流程](/help/edge/assets/repo-workflow.png)

## 先决条件

* [设置您的 GitHub 存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，以在您的 AEM 环境和 GitHub 存储库之间建立连接。
* 如果您已经在使用 Edge Delivery Services，请将最新版本的 [Adaptive Forms Block](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) 添加到您的 GitHub 存储库。
* AEM Forms 作者实例包含一个基于 Edge Delivery Services 的模板。确保您的环境中安装了[最新版本的核心组件](https://github.com/adobe/aem-core-forms-components)。
* 保存 AEM Forms as a Cloud Service 作者实例的 URL 和您方便的 GitHub 存储库。

## 使用通用编辑器创作自适应表单

使用通用编辑器，您可以使用现成的组件（如文本字段、复选框和单选按钮）轻松创建响应式交互表单。它提供了强大的功能，如动态规则、流畅的数据集成和自定义选项，使您能够根据您的确切要求构建表单。

>[!NOTE]
>
> 您还可以[使用通用编辑器中的 Edge Delivery Services Site 模板在 AEM Site 中创作表单，并将其发布到 Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project)。

要使用通用编辑器创作独立的自适应表单，请执行以下步骤：

1. **在 AEM Forms 作者实例上创建自适应表单**

   1. 登录AEM Forms as a Cloud Service创作实例。
   1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
   1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应Forms]**。 向导随即打开。
   1. 在&#x200B;**源**&#x200B;选项卡中，选择基于 Edge Delivery Services 的表单模板：

      ![创建 EDS 表单](/help/edge/assets/create-eds-forms.png)


      当您选择基于Edge Delivery Services的模板时，将启用&#x200B;**[!UICONTROL 创建]**&#x200B;按钮。
   1. （可选）在&#x200B;**[!UICONTROL 数据Source]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡中，您可以选择数据源或提交操作。
   1. （可选）在&#x200B;**[!UICONTROL 交付]**&#x200B;选项卡中，您可以为自适应表单指定发布或取消发布日期。

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

1. **在通用编辑器中创作表单**

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

## 发布该表单

现在，单击通用编辑器右上角的&#x200B;**[!UICONTROL 发布]**&#x200B;按钮将独立表单发布到 Edge Delivery Services。

![发布表单](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> 请参阅[发布和部署](/help/edge/docs/forms/universal-editor/publish-forms.md)一文，了解如何将表单发布到 Edge Delivery Services。

以下是如何在 Edge Delivery Services 上访问表单的方法：

* **暂存版本（用于测试）**：暂存版本显示的是表单的未发布工作版本，用于测试目的。在表单上线前，请使用以下 URL 格式预览表单：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例如，如果您的项目存储库名为 “edsforms” 且位于帐户 “wkndforms” 下，并且您使用的是 “main” 分支和“注册表格”表单，则暂存版本 URL 如下所示：
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **实时版本（已发布的表单）**：实时版本显示表单的最新发布版本，可供最终用户访问。使用以下 URL 格式访问已发布的表单实时版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例如，如果您的项目存储库名为 “edsforms” 且位于帐户 “wkndforms” 下，并且您使用的是 “main” 分支和“注册表格”表单，则暂存版本 URL 如下所示：
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

暂存版本和实时版本的 URL 结构相同。不过，根据上下文的不同，您看到的内容也有所不同：

![查看已发布的表单](/help/edge/assets/eds-view-publish-form.png)

## 管理表单

您可以使用AEM Forms用户界面对表单执行多项操作。

1. 登录AEM Forms as a Cloud Service创作实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

1. 选择一个表单，工具栏会显示您可以对所选表单执行的以下操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>编辑</p> </td>
   <td><p>在编辑模式下打开表单。<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>属性</p> </td>
   <td><p>提供用于修改表单属性的选项。<br /> <br /> </p> </td>
  </tr>
  <td><p>复制</p> </td>
   <td><p> 提供相应的选项，用于复制表单并将其粘贴到所需位置。<br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>预览</p> </td>
   <td><p>提供如下选项：以HTML预览表单，或通过将XML文件中的数据与表单合并来执行自定义预览。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>下载</p> </td>
   <td><p>下载所选表单。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>开始审核/管理审核</p> </td>
   <td><p>允许启动和管理选定表单的审核。<br /> <br /> </p> </td>
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
   <td><p>删除所选的表单。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>比较</p> </td>
   <td><p>比较两个不同的表单以进行预览。<br /> <br /> </p> </td>
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
