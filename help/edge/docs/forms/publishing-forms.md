---
title: 发布Forms以进行Edge Delivery Services
description: 了解表单发布如何与Edge Delivery Services配合使用以及如何使用Edge Delivery Services发布AEM表单。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---


# 发布Forms以进行Edge Delivery Services

本文会指导您完成将表单发布到AEMEdge Delivery Services的过程。
要将表单发布到Edge Delivery Services，必须首先在AEM环境和GitHub存储库之间建立连接。 连接后，您可以使用通用编辑器创作表单，该编辑器遵循WYSIWYG (What You See Is What You Get)方法，以实现与Sites的无缝且一致的用户体验。

## 先决条件

* 刚开始使用自适应Forms？ 按照提供的[教程](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)设置GitHub存储库。
* 如果您已在使用Edge Delivery Services，请将最新版本的[自适应Forms块](/help/edge/docs/forms/tutorial.md#)添加到您的GitHub存储库中。
* AEM Forms创作实例包括一个基于Edge Delivery Services的模板。 确保在您的环境中安装了[最新版本的核心组件](https://github.com/adobe/aem-core-forms-components)。
* 方便您使用AEM Formsas a Cloud Service创作实例和GitHub存储库的URL。

## 适用于Edge Delivery Services的Publish Forms

要为Edge Delivery Services发布表单，请执行以下步骤：

[1.将GitHub存储库链接到AEM实例](#link-github-repository-to-aem-instance)

[2.将AEM实例链接到GitHub存储库](#link-aem-instance-to-github-repository)

### 将GitHub存储库链接到AEM实例

要将GitHub存储库](/help/edge/docs/forms/tutorial.md)上的[项目链接到AEM Forms创作实例，请执行以下步骤：

1. 转到已为Edge Delivery Services创建或配置的GitHub存储库。
1. 打开 `fstab.yaml` 文件以供编辑。
1. 使用AEM Formsas a Cloud Service实例的URL更新GitHub存储库中的`fstab.yaml`文件。

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   例如，如果您的GitHub存储库名为“aemcrossswalk”，它位于帐户“wkndform”下，并且您使用的是“main”分支，则创作实例URL如下所示：

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. 提交对`fstab.yaml`文件的更改。

### 将AEM实例链接到GitHub存储库

要将AEM Forms创作实例链接到[您在GitHub存储库中的项目](/help/edge/docs/forms/tutorial.md)，请执行以下步骤：

[1.基于Edge Delivery Services模板创建自适应表单](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2.在AEM创作实例中找到表单的配置容器](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3.在通用编辑器中编写表单](#3-author-the-form-in-the-universal-editor)

[4. Publish并预览表单](#4-publish-and-preview-the-form)

#### 1.基于Edge Delivery Services模板创建自适应表单

1. 访问您的AEM Formsas a Cloud Service创作实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。1.选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应Forms]**。 向导随即打开。在Source选项卡中，选择一个基于Edge Delivery Services的表单模板：

   ![创建EDS Forms](/help/edge/assets/create-eds-forms.png){width=50%， align-center}

1. 单击&#x200B;**[!UICONTROL 创建]**，将显示&#x200B;**创建表单**&#x200B;向导。
1. 指定&#x200B;**GitHub URL**。 例如，如果您的GitHub存储库名为“aemcrossswalk”，则它位于帐户“wkndform”下，其URL为：
   `https://github.com/wkndform/aemcrosswalk`
1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![创建表单向导](/help/edge/assets/create-form-wizard.png){width=50%， align-center}

   单击&#x200B;**[!UICONTROL 创建]**&#x200B;后，表单即会在通用编辑器中打开以进行创作。

   ![创作表单](/help/edge/assets/author-form.png){width=50%， align-center}

   >[!NOTE]
   >
   > 在表单的配置容器中，会自动创建基于Edge Delivery Services模板的表单的Edge Delivery Services配置。

#### 2.在AEM创作实例中找到表单的配置容器

1. 在您的AEM Formsas a Cloud Service创作实例上导航到&#x200B;**[!UICONTROL Edge Delivery Services]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 工具]**。
1. 选择与表单名称匹配的文件夹。 例如，如果您的表单名为“contact-us”，请选择文件夹`forms/contact-us`并选择配置并发布配置：

   ![Edge Delivery Services配置](/help/forms/assets/aem-instance-eds-configuration.png){width=50%， align-center}

1. 单击&#x200B;**[!UICONTROL 属性]**&#x200B;查看配置。\
   ![自动创建的配置](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%， align-center}

   您可以保留“Edge主机”选项。 表单将发布到预览(.page)和实时(.live)环境。

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**。配置已保存。

#### 3.在通用编辑器中编写表单

单击&#x200B;**[!UICONTROL 创建]**&#x200B;后，将在通用编辑器中打开窗体以进行创作。

1. 打开内容浏览器，然后导航到&#x200B;**内容树**&#x200B;中的&#x200B;**[!UICONTROL 自适应表单]**&#x200B;组件。

   ![内容树](/help/edge/assets/content-tree.png){width=50%， align-center}

1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标并从&#x200B;**自适应表单组件**&#x200B;列表中添加所需的组件。

   ![添加组件](/help/edge/assets/add-component.png){width=50%， align-center}

1. 选择添加的自适应表单组件并使用&#x200B;**[!UICONTROL 属性]**&#x200B;更新其属性。

   ![打开属性](/help/edge/assets/component-properties.png){width=50%， align-center}

   以下屏幕截图显示了在Universal Editor中创作的简单“Contact Us”表单：

   ![联系我们表单](/help/edge/assets/contact-us.png){width=50%， align-center}

#### 4. Publish并预览表单

现在，通过单击通用编辑器右上角的&#x200B;**[!UICONTROL Publish]**&#x200B;按钮，将表单发布到Edge Delivery Services。

![发布表单](/help/edge/assets/publish-form.png){width=50%， align-center}


以下是如何在Edge Delivery Services上访问表单：

* **暂存版本（用于测试）**：暂存版本显示表单的未发布工作版本以进行测试。 在表单上线之前，请使用以下URL格式预览表单：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例如，如果项目的存储库名为“aemcrossswalk”，位于帐户“wkndform”下，并且您使用“main”分支和表单作为“联系我们”，则暂存版本URL如下所示：
https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **实时版本（已发布的表单）**：   实时版本显示表单的最新发布版本，最终用户可访问。 使用以下URL格式访问表单的已发布实时版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例如，如果项目的存储库名为“aemcrossswalk”，位于帐户“wkndform”下，并且您使用“main”分支和表单作为“联系我们”，则暂存版本URL如下所示：
https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

暂存版本和实时版本的URL结构均相同。 但是，您看到的内容因上下文而异：

![查看发布的表单](/help/edge/assets/eds-view-publish-form.png){width=50%， align-center}

## 疑难解答

加载表单时遇到问题？ 以下是一些常见问题以及如何修复它们：

* **表单URL**：仔细检查您的表单URL的末尾是否不包含“.html”扩展名。 Edge交付服务不需要此扩展。

* **AEM作者URL** L：确保您的`fstab.yaml`文件中列出的AEM作者URL的格式正确。 它应包括以下详细信息：

   * 正确的GitHub所有者
   * 正确的存储库名称
   * 您用于Edge Delivery Services的特定分支

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## 另请参阅

{{see-more-forms-eds}}