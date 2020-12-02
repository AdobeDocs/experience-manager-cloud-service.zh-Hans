---
title: ' [!DNL Assets]中的签入和签出文件'
description: 了解如何签出资产进行编辑，并在更改完成后将其签回。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 4%

---


# 资产{#check-in-and-check-out-files-in-assets}中的签入和签出文件

Adobe Experience Manager(AEM)资产允许您签出要编辑的资产，并在完成更改后将其签回。 注销资产后，只有您才能编辑、批注、发布、移动或删除资产。 签出资产会锁定资产。 其他用户不能对资产执行任何这些操作，除非您将资产签回AEM Assets。 但是，他们仍可以更改锁定资产的元数据。

要能够签出／登录资产，您需要对资产具有写入权限。

此功能有助于防止其他用户覆盖作者所做的更改，在创作中，多个用户跨团队协作编辑工作流。

## 签出资产{#checking-out-assets}

1. 从资产UI中，选择要签出的资产。 您还可以选择多个资产进行注销。

   ![chlimage_1-468](assets/chlimage_1-468.png)

1. 在工具栏中，单击／点按&#x200B;**[!UICONTROL 结帐]**&#x200B;图标。

   ![chlimage_1-469](assets/chlimage_1-469.png)

   请注意，**[!UICONTROL Checkout]**&#x200B;图标在锁定打开时切换为&#x200B;**[!UICONTROL Checkin]**&#x200B;图标。

   ![chlimage_1-470](assets/chlimage_1-470.png)

   要验证其他用户是否可以编辑您注销的资产，请以其他用户身份登录。 您签出的资产的缩略图上会显示一个锁图标。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   选择资产。 请注意，工具栏不会显示任何允许您编辑、批注、发布或删除资产的选项。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   但是，您可以单击／点按&#x200B;**[!UICONTROL 视图属性]**&#x200B;图标，以编辑锁定资产的元数据。

1. 单击／点按编辑图标以在编辑模式下打开资产。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 编辑资产并保存更改。 例如，裁剪图像并保存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您还可以选择对资产添加注释或发布。

1. 从 Assets UI 中选择已编辑资产，然后单击/点按工具栏中的&#x200B;**[!UICONTROL 签入]**&#x200B;图标。

   ![chlimage_1-475](assets/chlimage_1-475.png)

   修改后的资产将签入AEM Assets，可供其他用户编辑。

## 强制签入{#forced-check-in}

管理员可以签入其他用户签出的资产。

1. 以管理员身份登录AEM Assets。
1. 在资产UI中，选择已由其他用户签出的一个或多个资产。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具栏中，单击／点按&#x200B;**[!UICONTROL 释放锁]**&#x200B;图标。 资产将签回，可供其他用户编辑。

   ![chlimage_1-477](assets/chlimage_1-477.png)