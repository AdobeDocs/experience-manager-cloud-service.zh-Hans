---
title: 资产中的登记和注销文件
description: 了解如何在更改完成后注销要编辑的资产并重新登记。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 资产中的登记和注销文件 {#check-in-and-check-out-files-in-assets}

Adobe Experience Manager(AEM)资产可让您签出资产进行编辑，并在完成更改后将其签回。 注销资产后，只有您才能编辑、批注、发布、移动或删除资产。 注销资产会锁定资产。 在您将资产签回AEM资产之前，其他用户无法对资产执行任何这些操作。 但是，他们仍然可以更改锁定资产的元数据。

要能够注销／登录资产，您需要对资产具有写入权限。

此功能有助于防止其他用户覆盖作者所做的更改，在作者中，多个用户跨团队协作处理编辑工作流程。

## 注销资产 {#checking-out-assets}

1. 从资产UI中，选择要注销的资产。 您还可以选择多个资产以注销。

   ![chlimage_1-468](assets/chlimage_1-468.png)

1. From the toolbar, click/tap the **[!UICONTROL Checkout]** icon.

   ![chlimage_1-469](assets/chlimage_1-469.png)

   观察“检 **[!UICONTROL 出]** ”(Checkout **[!UICONTROL )图标在锁定打开时切换]** 为“检入”(Checkin)图标。

   ![chlimage_1-470](assets/chlimage_1-470.png)

   要验证其他用户是否可以编辑您注销的资产，请以其他用户身份登录。 注销的资产的缩略图上会显示锁图标。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   选择资产。 请注意，工具栏不显示任何允许您编辑、注释、发布或删除资产的选项。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   但是，您可以单击／点按查看 **[!UICONTROL 属性图标]** ，以编辑锁定资产的元数据。

1. 单击／点按编辑图标以在编辑模式下打开资产。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 编辑资产并保存更改。 例如，裁剪图像并保存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您还可以选择对资产添加注释或发布资产。

1. 从资产UI中选择已编辑的资产，然后单击／点按工具栏中 **[!UICONTROL 的]** “签入”图标。

   ![chlimage_1-475](assets/chlimage_1-475.png)

   修改后的资产会登记到AEM资产，可供其他用户编辑。

## 强制登记 {#forced-check-in}

管理员可以登记其他用户注销的资产。

1. 以管理员身份登录到AEM资产。
1. 从资产UI中，选择一个或多个已由其他用户注销的资产。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具栏中，单击／点按释放 **[!UICONTROL 锁定图标]** 。 资产将重新登记，可供其他用户编辑。

   ![chlimage_1-477](assets/chlimage_1-477.png)