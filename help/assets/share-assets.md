---
title: 将资产、文件夹和收藏集共享为链接
description: 本文将介绍如何在Experience Manager资产中以超链接的形式共享资产、文件夹和收藏集。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 5%

---


# 共享和分发在Experience Manager中管理的资产 {#share-assets-from-aem}

通过Adobe Experience Manager(AEM)资产，您可以与组织成员和外部实体（包括合作伙伴和供应商）共享资产、文件夹和收藏集。 使用以下方法将Experience Manager资产作为云服务进行共享：

* 以链接形式共享。
* 下载资产并单独共享。
* 通过AEM桌面应用程序共享。
* 通过Adobe Asset Link进行共享。
* （即将推出的功能）使用Brand Portal进行共享。

## 以链接方式共享资产 {#sharelink}

要为要与用户共享的资产生成URL，请使用“链接共享”对话框。 具有管理员权限或在位置具有读取权 `/var/dam/share` 限的用户能够视图与他们共享的链接。 通过链接共享资产是一种方便的方式，使外部方无需先登录AEM资产即可获得资源。

>[!NOTE]
>
>* 您需要对要作为链接共享的文件夹或资产具有编辑ACL权限。
>* 在与用户共享链接之前，请确保已配置Day CQ邮件服务。 否则，将发生错误。


1. 在“资产”用户界面中，选择要作为链接共享的资产。
1. 在工具栏中，单击／点按共 **[!UICONTROL 享链接]**。 资产链接会在共享链接字段中 **[!UICONTROL 自动创建]** 。 复制此链接并与用户共享。 链接的默认过期时间为一天。

   >[!NOTE]
   >
   >如果共享资产被移动到其他位置，其链接将停止工作。 重新创建链接并与用户重新共享。

<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to AEM Assets.

>[!NOTE]
>
>* You need Edit ACL permission on the folder or the asset that you want to share as a link.
>* Before you share a link with users, ensure that Day CQ Mail Service is configured. Otherwise, an error occurs.

1. In the Assets user interface, select the asset to share as a link.
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**.

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. Copy this link and share it with the users. The default expiration time for the link is one day.

   Alternatively, proceed to perform steps 3-7 of this procedure to add email recipients, configure the expiration time for the link, and send it from the dialog.

   >[!NOTE]
   >
   >If a shared asset is moved to a different location, its link stops working. Re-create the link and re-share with the users.

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

    * local
    * author
    * publish

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single AEM author instance. For publish, provide the URL for the publish instance.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. You can also share the link with multiple users.

   If the user is a member of your organization, select the user's email ID from the suggested email IDs that appear in the list below the typing area. For an external user, type the complete email ID and then select it from the list.

   To enable emails to be sent out to users, configure the SMTP server details in [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words "External User" are prefixed with the email ID of the user.

1. In the **[!UICONTROL Subject]** box, enter a subject for the asset you want to share.
1. In the **[!UICONTROL Message]** box, enter an optional message.
1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. By default, the expiration date is set for a week from the date you share the link.
1. To let users download the original image along with the renditions, select **[!UICONTROL Allow download of original file]**.

   >[!NOTE]
   >
   >By default, users can only download the renditions of the asset that you share as a link.

1. Click **[!UICONTROL Share]**. A message confirms that the link is shared with the users through an email.
1. To view the shared asset, click/tap the link in the email that is sent to the user. The shared asset is displayed in the **[!UICONTROL Adobe Marketing Cloud]** page.

   To toggle to the list view, click/tap the layout icon in the toolbar.

1. To generate a preview of the asset, click/tap the shared asset. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   >[!NOTE]
   >
   >AEM supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## 下载和共享资产 {#download-and-share-assets}

用户可以在Experience manager之外下载并共享某些资产。 有关详细信息，请 [参阅如何搜索资产](/help/assets/search-assets.md)[、如何下载资产](/help/assets/download-assets-from-aem.md)以及如 [何下载集合](manage-collections.md#download-a-collection)

## 与创意专业人士共享资源 {#share-with-creatives}

营销人员和业务线用户可以使用、

* **AEM桌面应用程序**: 该应用程序在Windows和Mac上工作。 请参阅 [桌面应用程序概述](https://docs.adobe.com/content/help/zh-Hans/experience-manager-desktop-app/using/introduction.html)。 要了解任何授权桌面用户如何轻松访问共享资产，请参 [阅浏览、搜索和预览资产](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)。 桌面用户可以创建资产并将其与AEM用户的对应人员共享，例如，通过上传新图像。 请参阅 [使用桌面应用程序上传资产](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)。

* **Adobe资产链接**: 创意专业人士可以直接在Adobe InDesign、Adobe Illustrator和Adobe Photoshop中搜索和使用资源。

## 配置资产共享 {#configure-sharing}

共享资产的不同选项需要特定配置，并且具有特定的先决条件。

### 配置资产链接共享 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

要为要与用户共享的资产生成URL，请使用“链接共享”对话框。 具有管理员权限或在位置具有读取权 `/var/dam/share` 限的用户能够视图与他们共享的链接。 通过链接共享资产是一种方便的方式，使外部方无需先登录AEM资产即可获得资源。

>[!NOTE]
>
>如果要将AEM作者实例中的链接共享给外部实体，请确保仅提供以下请求 `GET` URL。 阻止其他URL以确保您的AEM作者实例安全。
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

### 配置最大数据大小 {#maxdatasize}

当您使用链接共享功能从共享的链接下载资产时，AEM会从存储库中压缩资产层次结构，然后以ZIP文件形式返回资产。 但是，在ZIP文件中压缩的数据量没有限制的情况下，大量数据会受到压缩，这会导致JVM中内存不足错误。 要保护系统免受由于这种情况而可能发生的拒绝服务攻击，您可以配置下载文件的最大大小。 如果资产的未压缩大小超出配置值，则会拒绝资产下载请求。 默认值为100 MB。

1. 单击/点按 AEM 徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web Console]**。
1. 在Web控制台中，找到 **[!UICONTROL Day CQ DAM临时资产共享代理Servlet配置]** 。
1. 在编辑模式下打开配置，并修改“最大内容大小(未 **[!UICONTROL 压缩)”参数的]** 值。
1. 保存更改。

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### 启用桌面操作以与桌面应用程序一起使用 {#desktop-actions}

从浏览器的“资产”用户界面中，您可以浏览资产位置或签出并打开资产，以便在桌面应用程序中进行编辑。 这些选项称为桌面操作，要启用它，请参阅 [在AEM Web界面中启用桌面操作](https://docs.adobe.com/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)。

![使用桌面应用程序时启用桌面操作以用作快捷方式](assets/enable_desktop_actions.png)

### 使用Adobe Asset Link的配置 {#configure-asset-link}

Adobe Asset Link简化了创意人员和营销人员在内容创建过程中的协作。 它将Adobe Experience Manager(AEM)资产与Creative Cloud桌面应用程序Adobe InDesign、Adobe Photoshop和Adobe Illustrator连接在一起。 通过Adobe Asset Link面板，创意人员可以访问和修改AEM资产中存储的内容，而无需离开他们最熟悉的创意应用程序。

了 [解如何配置AEM以与Adobe Asset Link一起使用](https://helpx.adobe.com/cn/enterprise/using/configure-aem-assets-for-asset-link.html)。

## Best practices and troubleshooting {#bestpractices}

* 名称中包含空白的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享资产，请向AEM管理员咨询下载限 [制](#maxdatasize) 。

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your AEM administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!--
Add content or link about how to share using Brand Portal when it is available on Cloud Service.
-->
