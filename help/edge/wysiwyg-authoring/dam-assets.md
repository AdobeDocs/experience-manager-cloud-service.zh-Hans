---
title: 使用Edge Delivery Services发布带DAM Assets的页面
description: 了解确保将页面的DAM资源无缝发布到Edge Delivery Services所需的设置。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 65a3b4d923a91702e7ea9b13356802836fa4ce0b
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 2%

---


# 使用Edge Delivery Services发布带DAM Assets的页面 {#dam-assets}

了解确保将页面的DAM资源无缝发布到Edge Delivery Services所需的设置。

## 通用编辑器、DAM Assets和Edge Delivery {#overview}

在编辑通用编辑器的内容时，您当然可以从DAM中选择资源。 在将内容发布到Edge Delivery Services时，也会发布相关的DAM内容。

要确保这种无缝行为，AEM和Edge Delivery Services必须具有对DAM的正确访问权限才能发布。 这包括：

* [确保资产文件夹可访问。](#accessible)
* [确保为assets文件夹分配了正确的配置（如果需要）。](#configuration)

## 确保Assets文件夹可访问 {#accessible}

将页面从AEM发布到Edge Delivery Services时，使用了[技术帐户](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。 当您首次发布使用通用编辑器创建的页面时，Cloud Manager会在AEM中自动创建名称为`<hash>@techacct.adobe.com`格式的用户帐户。

![技术帐户](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

此技术帐户必须具有对所有DAM文件夹的访问权限，才能发布其内容。 您可以：

* 不使用专用DAM文件夹。
* 授予技术帐户用户对DAM文件夹的访问权限。

## 确保为Assets文件夹分配了正确的配置 {#configuration}

通常，确保技术帐户有权访问DAM中的资产，这足以将资产与页面发布到Edge Delivery Services。

但是，在另外两种情况下需要额外的配置：

* 如果您希望将包含PDF或视频等非图像资源的页面发布到Edge Delivery Services。
* 如果您希望将图像资产发布到Edge Delivery Services，而不依赖于页面。

要支持这两种使用案例，必须将[配置](/help/implementing/developing/introduction/configurations.md)分配给DAM文件夹。

1. 登录您的AEM创作环境。
1. 在&#x200B;**站点**&#x200B;下，选择发布资产的站点或与资产关联的站点。
1. 点按或单击工具栏中的&#x200B;**属性**。
1. 在属性窗口的&#x200B;**高级**&#x200B;选项卡上，记下字段&#x200B;**云配置**&#x200B;中的配置。
   * 当您以`/conf/<site-name>`格式创建站点时，将自动创建此项。
1. 在属性窗口中点按或单击&#x200B;**取消**，然后导航到&#x200B;**Assets** -> **文件**，并选择您的DAM文件夹。
1. 点按或单击工具栏中的&#x200B;**属性**。
1. 在Cloud Service窗口的&#x200B;**属性**&#x200B;选项卡的&#x200B;**云配置**&#x200B;字段中，选择与之前说明的相同的配置。
1. 点按或单击&#x200B;**保存并关闭**。
