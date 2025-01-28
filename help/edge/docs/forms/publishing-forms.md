---
title: 发布 Edge Delivery Services 表单
description: 了解表单发布如何与 Edge Delivery Services 配合使用，以及如何使用 Edge Delivery Services 发布 AEM Forms。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: b90c27e3-22ea-4b18-b16e-a5c5a0ed58b8
source-git-commit: 67384a9141ced3bf5be63c8489dd5c329a288056
workflow-type: ht
source-wordcount: '993'
ht-degree: 100%

---

# 发布 Edge Delivery Services 表单

本文将指导您完成将表单发布到 AEM Edge Delivery Services 的过程。
要将表单发布到 Edge Delivery Services，您必须首先在 AEM 环境和 GitHub 存储库之间建立连接。连接后，您可以使用通用编辑器创作表单，该编辑器遵循所见即所得（WYSIWYG）方法，以实现无缝且一致的 Sites 用户体验。

## 先决条件

* 自适应表单有哪些新功能？按照提所提供的[教程](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)设置您的 GitHub 存储库。
* 如果您已经在使用 Edge Delivery Services，请将最新版本的[自适应表单区块](/help/edge/docs/forms/tutorial.md#)添加到您的 GitHub 存储库。
* AEM Forms 作者实例包含一个基于 Edge Delivery Services 的模板。确保您的环境中安装了[最新版本的核心组件](https://github.com/adobe/aem-core-forms-components)。
* 保存 AEM Forms as a Cloud Service 作者实例的 URL 和您方便的 GitHub 存储库。

## 发布适用于 Edge Delivery Services 的表单

要发布适用于 Edge Delivery Services 的表单，请执行以下步骤：

[1. 将 GitHub 存储库链接到 AEM 实例](#link-github-repository-to-aem-instance)

[2. 将 AEM 实例链接到 GitHub 存储库](#link-aem-instance-to-github-repository)

### 将 GitHub 存储库链接到 AEM 实例

要将 [GitHub 存储库上的项目](/help/edge/docs/forms/tutorial.md)链接到 AEM Forms 作者实例，请执行以下步骤：

1. 前往您为 Edge Delivery Services 创建或配置的 GitHub 存储库。
1. 打开 `fstab.yaml` 文件以供编辑。
1. 使用 AEM Forms as a Cloud Service 实例的 URL 更新 GitHub 存储库中的 `fstab.yaml` 文件。

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   例如，如果您的 GitHub 存储库名为 “aemcrosswalk” 且位于帐户 “wkndform” 下，并且您使用的是 “main” 分支，则作者实例 URL 如下所示：

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. 将更改提交至 `fstab.yaml` 文件。

### 将 AEM 实例链接到 GitHub 存储库

要将 [AEM Forms 作者实例](/help/edge/docs/forms/tutorial.md)链接到 GitHub 存储库上的项目，请执行以下步骤：

[1. 根据 Edge Delivery Services 模板创建自适应表单](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2. 在 AEM 作者实例中找到表单的配置容器](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3. 在通用编辑器中创作表单](#3-author-the-form-in-the-universal-editor)

[4. 发布和预览表单](#4-publish-and-preview-the-form)

#### 1. 根据 Edge Delivery Services 模板创建自适应表单

1. 访问您的 AEM Forms as a Cloud Service 作者实例。
1. 选择 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。1. 选择&#x200B;**[!UICONTROL 创建]**  > **[!UICONTROL 自适应表单]**。向导随即打开。在“源”选项卡中，选择基于 Edge Delivery Services 的 FormTemplate：

   ![创建 EDS Forms](/help/edge/assets/create-eds-forms.png) {width=50%, align-center}

1. 单击&#x200B;**[!UICONTROL 创建]**，将出现&#x200B;**创建表单**&#x200B;向导。
1. 指定 **GitHub URL**。例如，如果您的 GitHub 存储库名为 “aemcrosswalk” 且位于帐户 “wkndform” 下，则 URL 为：
   `https://github.com/wkndform/aemcrosswalk`
1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![创建表单向导](/help/edge/assets/create-form-wizard.png){width=50%, align-center}

   单击&#x200B;**[!UICONTROL 创建]**&#x200B;后，表单就会在通用编辑器中打开以供创作。

   ![创作表单](/help/edge/assets/author-form.png){width=50%, align-center}

   >[!NOTE]
   >
   > 基于 Edge Delivery Services 模板的表单 Edge Delivery Services 配置会在表单的配置容器中自动创建。

#### 2. 在 AEM 作者实例中找到表单的配置容器

1. 导航至 AEM Forms as a Cloud Service 作者实例上的&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Edge Delivery Services 配置]**。
1. 选择与表单名称匹配的文件夹。例如，如果您的表单名为 “contact-us”，请选择文件夹 `forms/contact-us`，然后选择配置并发布配置：

   ![Edge Delivery Services 配置](/help/forms/assets/aem-instance-eds-configuration.png){width=50%, align-center}

1. 单击&#x200B;**[!UICONTROL 属性]**&#x200B;查看配置。\
   ![自动创建的配置](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%, align-center}

   您可以原样保留 Edge Host 选项。该表单将发布到预览（.page）和实时（.live）环境。

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**。配置已保存。

#### 3. 在通用编辑器中创作表单

单击&#x200B;**[!UICONTROL 创建]**&#x200B;后，表单就会在通用编辑器中打开以供创作。

1. 打开内容浏览器，然后导航到&#x200B;**内容树**&#x200B;中的&#x200B;**[!UICONTROL 自适应表单]**&#x200B;组件。

   ![内容树](/help/edge/assets/content-tree.png){width=50%, align-center}

1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标，然后从&#x200B;**自适应表单组件**&#x200B;列表中添加所需的组件。

   ![添加组件](/help/edge/assets/add-component.png){width=50%, align-center}

1. 选择添加的自适应表单组件，并使用&#x200B;**[!UICONTROL 属性]**&#x200B;更新其属性。

   ![打开属性](/help/edge/assets/component-properties.png){width=50%, align-center}

   下面的屏幕快照显示了在通用编辑器中简单的创作 “Contact Us” 表单：

   ![”Contact Us“ 表单](/help/edge/assets/contact-us.png){width=50%, align-center}

#### 4. 发布和预览表单

现在，单击通用编辑器右上角的&#x200B;**[!UICONTROL 发布]**&#x200B;按钮将表单发布到 Edge Delivery Services。

![发布表单](/help/edge/assets/publish-form.png){width=50%, align-center}


以下是如何在 Edge Delivery Services 上访问表单的方法：

* **暂存版本（用于测试）**：暂存版本显示的是表单的未发布工作版本，用于测试目的。在表单上线前，请使用以下 URL 格式预览表单：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例如，如果您的项目存储库名为 “aemcrosswalk” 且位于帐户 “wkndform” 下，并且您使用的是 “main” 分支和 “contact us” 表单，则暂存版本 URL 如下所示：https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **实时版本（已发布的表单）**：实时版本显示表单的最新发布版本，可供最终用户访问。使用以下 URL 格式访问已发布的表单实时版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例如，如果您的项目存储库名为 “aemcrosswalk” 且位于帐户 “wkndform” 下，并且您使用的是 “main” 分支和 “contact us” 表单，则暂存版本 URL 如下所示：https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

暂存版本和实时版本的 URL 结构相同。不过，根据上下文的不同，您看到的内容也有所不同：

![查看已发布的表单](/help/edge/assets/eds-view-publish-form.png){width=50%, align-center}

## 疑难解答

是否在加载表单时遇到了问题？以下是一些常见问题及其解决方法：

* **表单 URL**：仔细检查表单的 URL 末尾是否包含 “.html” 扩展名。Edge Deliver Service 不需要此扩展名。

* **AEM 作者 URL**：确保 `fstab.yaml` 文件中列出的 AEM 作者 URL 格式正确。它应包括以下详细信息：

   * 正确的 GitHub 所有者
   * 正确的存储库名称
   * 用于 Edge Delivery Services 的特定分支

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## 另请参阅

{{see-more-forms-eds}}
