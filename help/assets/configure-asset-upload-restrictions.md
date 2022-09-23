---
title: 配置资产上传限制
description: 配置Adobe Experience Manager Assets，以根据MIME类型限制用户可上传的资产类型。 它有助于防止意外上载不需要的格式和恶意文件。
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
source-git-commit: d2d0d8b0d484d2e5cd2bf44449e7d71d3da98eea
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 4%

---

# 配置资产上传限制 {#configure-asset-upload-restrictions}

您可以配置Adobe Experience Manager Assets，以根据MIME类型限制用户可上传的资产类型。

>[!IMPORTANT]
>
>默认情况下，Experience Manager Assets允许用户上传所有MIME类型的资产。 但是，您可以配置设置，以限制用户仅上传特定MIME类型的文件。

## 前提条件 {#prerequisites-asset-upload-restrictions}

您必须拥有管理员权限才能配置资产上传限制。

## 对资产上传应用限制 {#apply-restrictions-asset-uploadsssssss}

配置 [!DNL Experience Manager] 要限制用户上传特定MIME类型的文件，请执行以下操作：

1. 导航到 **[!UICONTROL 工具>资产>资产配置]**.

1. 单击 **[!UICONTROL 上载限制]**.

1. 单击 **[!UICONTROL 添加]** 以定义允许的MIME类型。

1. 在文本框中指定MIME类型。 您可以单击 **[!UICONTROL 添加]** 再次指定更多允许的MIME类型。 您还可以单击 ![删除图标](assets/delete-icon.svg) 从列表中删除任何MIME类型。

1. 单击“**[!UICONTROL 保存]**”。

**示例1:允许将所有图像和PDF文件上传到Experience Manager Assets**

要允许将所有格式的图像和PDF文件上传到Experience Manager Assets，请执行以下设置：

![资产上传限制](assets/asset-upload-restrictions.png)

`image/*` 因为MIME类型允许上传所有格式的图像。 `application/pdf` 因为使用MIME类型，可将PDF文件上传到Experience Manager Assets。

如果您尝试上传的文件未包含在允许的MIME类型列表中，则Experience Manager Assets会显示以下错误消息：

![受限文件](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov` 是指允许的MIME类型中未包含的文件名。

**示例2:允许将特定图像格式上传到Experience Manager Assets**

要向允许的MIME类型添加特定图像格式并限制上传所有其他资产格式，请执行以下设置：

![资产限制](assets/asset-restrictions.png)

根据图像中描述的设置，您可以将。JPG、 .PNG和。GIF格式的图像上传到Experience Manager Assets。
