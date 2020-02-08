---
title: 将资产、文件夹和收藏集共享为链接
description: 本文介绍如何在Experience Manager资产中以超链接的形式共享资产、文件夹和收藏集。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 共享和分发Experience Manager中管理的资产 {#share-assets-from-aem}

Adobe Experience Manager(AEM)资产允许您与组织成员和外部实体（包括合作伙伴和供应商）共享资产、文件夹和收藏集。 您可以使用以下方法将Experience Manager资产共享为云服务：

* 作为链接共享
* 下载资产
* 通过AEM桌面应用程序共享
* 通过Adobe Asset Link共享
* （即将推出的功能）使用Brand Portal进行共享

## 以链接方式共享资产 {#sharelink}

要为要与用户共享的资产生成URL，请使用“链接共享”对话框。 具有管理员权限或在位置具有读取权 `/var/dam/share` 限的用户可以查看与他们共享的链接。 通过链接共享资产是一种方便的方式，使外部方无需先登录AEM资产即可获得资源。

>[!NOTE]
>
>* 您需要对要作为链接共享的文件夹或资产具有编辑ACL权限。
>* 在与用户共享链接之前，请确保已配置Day CQ mail服务。 否则，将发生错误。


1. 在“资产”用户界面中，选择要作为链接共享的资产。
1. 在工具栏中，单击／点按共 **[!UICONTROL 享链接]**。

   资产链接会在共享链接字段中 **[!UICONTROL 自动创建]** 。 复制此链接并与用户共享。 链接的默认过期时间为一天。

   或者，也可以继续执行此操作过程的第 3-7 步，以添加电子邮件收件人、配置链接的有效时间，以及从对话框中发送电子邮件。

   >[!NOTE]
   >
   >如果共享资产被移到其他位置，其链接将停止工作。 重新创建链接并与用户重新共享。

1. 从Web控制台中，打开 **[!UICONTROL Day CQ Link Externalizer]** （日CQ链接外部器）配置，并修改“ **[!UICONTROL Domains]** ”（域）字段中的以下属性，其中各个属性的值均提及：

   * 本机
   * 作者
   * 发布
   对于本地属性和作者属性，请分别提供本地实例和作者实例的URL。 如果运行单个AEM作者实例，则本地属性和作者属性的值相同。 对于发布，请提供发布实例的URL。

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. 您也可以与多个用户共享链接。

   如果用户是您组织的成员，请从键入区域下方的列表中显示的建议电子邮件ID中选择用户的电子邮件ID。对于外部用户，键入完整的电子邮件ID，然后从列表中选择它。

   要向用户发送电子邮件，请在 [Day CQ Mail service中配置SMTP服务器详细信息](/help/assets/configure-asset-sharing.md#configmailservice)。

   >[!NOTE]
   >
   >如果您输入的电子邮件 ID 所对应的用户不是您组织的成员，则该用户的电子邮件 ID 前面会标记有“外部用户”字样。

1. 在&#x200B;**[!UICONTROL 主题]**&#x200B;框中，为您要共享的资产输入主题。
1. 在“消 **[!UICONTROL 息]** ”框中，输入可选消息。
1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. 默认情况下，过期日期设置为您共享链接后一周的时间。
1. 要允许用户下载原始图像和再现，请选择“允 **[!UICONTROL 许下载原始文件”]**。

   >[!NOTE]
   >
   >默认情况下，用户只能下载您共享为链接的资产的演绎版。

1. 单击&#x200B;**[!UICONTROL 共享]**。系统会显示一条消息，确认已通过电子邮件与用户共享该链接。
1. 要查看共享的资产，请单击／点按发送给用户的电子邮件中的链接。 共享的资产会显示在 **[!UICONTROL Adobe Marketing Cloud页面]** 。

   要切换到列表视图，请单击／点按工具栏中的布局图标。

1. 要生成资产的预览，请单击／点按共享资产。 要关闭预览并返回至 **[!UICONTROL Marketing Cloud]** ，请单击／点 **[!UICONTROL 按工具栏中的返回]** 。 如果已共享文件夹，请单击／点按父 **[!UICONTROL 文件夹]** ，以返回到父文件夹。

   >[!NOTE]
   >
   >AEM支持生成以下MIME类型的资产预览：JPG、PNG、GIF、BMP、INDD、PDF和PPT。 您只能下载其他MIME类型的资产。

1. 要下载共享的资产，请单击／点按工 **[!UICONTROL 具栏中的]** “选择”，单击／点按资产，然后单击／点按工具栏中的 **[!UICONTROL 下载]** 。
1. 要查看您作为链接共享的资产，请转到资产UI，然后单击／点按GlobalNav图标。 从列 **[!UICONTROL 表中选择]** “导航”以显示“导航”窗格。
1. 从导航窗格中，选择 **[!UICONTROL 共享链接]** ，以显示共享资产列表。
1. 要取消共享资产，请选择该资产，然后点按／单击工 **[!UICONTROL 具栏中]** 的取消共享。

系统会显示一条消息，确认您已取消共享该资产。此外，该资产对应的条目也会从列表中删除。

## 下载和共享资产 {#download-and-share-assets}

用户可以在Experience manager之外下载并共享某些资产。 有关详细信息，请 [参阅如何搜索资产](/help/assets/search-assets.md)[、如何下载资产](/help/assets/download-assets-from-aem.md)，以 [及如何下载集合](manage-collections.md#download-a-collection)

## 与创意专业人士共享资源 {#share-with-creatives}

营销人员和业务线用户可以使用、

* **AEM桌面应用程序**:该应用程序在Windows和Mac上工作。 请参阅 [桌面应用程序概述](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)。 要了解任何授权的桌面用户如何轻松访问共享资产，请参 [阅浏览、搜索和预览资产](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)。 桌面用户可以创建新资产并与AEM用户的对应人员共享，例如，通过上传新图像。 请参阅 [使用桌面应用程序上传资产](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)。

* **Adobe Asset Link**:创意专业人士可以直接在Adobe inDesign、Adobe Illustrator和Adobe Photoshop中搜索和使用资源。

### Best practices and troubleshooting {#bestpractices}

* 名称中包含空白的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享资产，请向AEM管理员检查下载限 [制](/help/assets/configure-asset-sharing.md#maxdatasize) 。
* 如果您无法发送包含共享资产链接的电子邮件，或如果其他用户无法收到您的电子邮件，请咨询您的AEM管理员(如果电子邮件服务 [已配置](/help/assets/configure-asset-sharing.md#configmailservice) ，或未配置)。
* 如果您无法使用链接共享功能共享资产，请确保您拥有相应的权限。 请参阅 [共享资产](#sharelink)。

<!--
Add content or link about how to share using BP, DA, AAL, etc.
-->
