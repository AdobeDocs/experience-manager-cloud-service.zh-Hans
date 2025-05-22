---
title: 使用 Edge Delivery Services 发布包含 DAM 资产的页面
description: 了解需要哪些设置可确保您页面的 DAM 资产顺利发布到 Edge Delivery Services。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '433'
ht-degree: 100%

---

# 使用 Edge Delivery Services 发布包含 DAM 资产的页面 {#dam-assets}

了解需要哪些设置可确保您页面的 DAM 资产顺利发布到 Edge Delivery Services。

## 通用编辑器、DAM 资产和 Edge Delivery {#overview}

为通用编辑器编辑内容时，您当然可以从 DAM 中选择资产。当您将内容发布到 Edge Delivery Services 时，相关的 DAM 内容也会发布。

为了确保这个过程顺利无缝，AEM 和 Edge Delivery Services 必须具有对 DAM 的适当访问权限才能正确发布。这包括：

* [确保资产文件夹可访问](#accessible)。
* [确保资产文件夹被分配了正确的配置（根据需要）](#configuration)。

## 确保资产文件夹可访问 {#accessible}

将页面从 AEM 发布到 Edge Delivery Services 时，需要使用[技术帐户](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。每当您首次发布使用通用编辑器创建的页面时，Cloud Manager 都会自动在 AEM 中创建此帐户作为一个用户，其名称格式为 `<hash>@techacct.adobe.com`。

![技术帐户](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

此技术帐户必须具有对所有 DAM 文件夹的访问权限才能发布这些文件夹的内容。您可以：

* 不使用专用 DAM 文件夹。
* 授予技术帐户对 DAM 文件夹的用户访问权限。

## 确保资产文件夹被分配了正确的配置 {#configuration}

通常，确保您的技术帐户可以访问 DAM 中的资产，就可以确保将您的资产与页面一起发布到 Edge Delivery Services。

但是，在另外两种情况下还需要进行额外的配置：

* 如果您希望将包含非图像资产（例如 PDF 或视频）的页面发布到 Edge Delivery Services。
* 如果您希望将图像资产与页面分开发布到 Edge Delivery Services。

为了支持这两种用例，必须给 DAM 文件夹分配一个[配置](/help/implementing/developing/introduction/configurations.md)。

1. 登录您的 AEM 创作环境。
1. 在 **Sites** 中选择您要发布资产的 Site 或者要与资产相关联的 Site。
1. 在工具栏中点击或单击&#x200B;**属性**。
1. 在属性窗口中的&#x200B;**高级**&#x200B;选项卡中，记下&#x200B;**云配置**&#x200B;字段中的配置。
   * 当您创建 `/conf/<site-name>` 格式的 Site 时，就会自动创建该配置。
1. 在属性窗口中点击或单击&#x200B;**取消**，然后导航至&#x200B;**资产** -> **文件**，选择您的 DAM 文件夹。
1. 在工具栏中点击或单击&#x200B;**属性**。
1. 在属性窗口中的 **Cloud Services** 选项卡中，在&#x200B;**云配置**&#x200B;字段中选择与之前记下的相同的配置。
1. 点击或单击&#x200B;**保存并关闭**。
