---
title: 分发和共享资产、文件夹和收藏集
description: 使用共享作为链接、下载和通过之类的方法分发数字资产 [!DNL Brand Portal], [!DNL desktop app]和 [!DNL Asset Link].
contentOwner: AG
feature: Asset Management,Collaboration,Asset Distribution
role: User,Admin
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: c74846dc4d4da9fa5050ce7b8ffce7f27e77269b
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 1%

---

# 共享和分发在 [!DNL Experience Manager] {#share-assets-from-aem}

[!DNL Adobe Experience Manager Assets] 允许您与组织成员以及外部实体（包括合作伙伴和供应商）共享资产、文件夹和收藏集。 使用以下方法从共享资产 [!DNL Experience Manager Assets] as a [!DNL Cloud Service]:

* [共享为链接](#sharelink).
* [下载资产](/help/assets/download-assets-from-aem.md) 并单独共享。
* 共享方式 [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html).
* 共享方式 [[!DNL Adobe Asset Link]](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html).
* 共享方式 [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html).

## 以链接方式共享资产 {#sharelink}

通过链接共享资产是让外部各方无需登录即可获取资源的一种便捷方式 [!DNL Assets]. 利用功能，匿名用户可以访问和下载与他们共享的资产。 当用户从共享链接下载资产时， [!DNL Assets] 使用异步服务，可提供更快、不间断的下载。 要下载的资产将在后台的收件箱中排入可管理文件大小的ZIP存档。 对于大型下载，下载内容捆绑为100 GB的文件。

<!--
Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. 
-->

>[!NOTE]
>
>* 您需要对要作为链接共享的文件夹或资产具有编辑ACL权限。
>* [启用出站电子邮件](/help/implementing/developing/introduction/development-guidelines.md#sending-email) 链接。


可使用链接共享功能通过两种方式共享资产：

1. 生成共享链接， [复制并共享资产链接](#copy-and-share-assets-link) 其他用户。 链接的默认过期时间为一天。 与其他用户共享复制的链接时，无法更改过期时间。

1. 生成共享链接并 [通过电子邮件共享资产链接](#share-assets-link-through-email). 在这种情况下，您可以修改默认值（如过期日期和时间），并允许下载原始资产及其演绎版。 您可以通过添加多个用户的电子邮件地址，向其发送电子邮件。

![链接共享对话框](assets/link-sharing-dialog.png)

### 复制并共享资产链接{#copy-and-share-asset-link}

要将资产共享为公共URL，请执行以下操作：

1. 登录到 [!DNL Experience Manager Assets] 并导航到 **[!UICONTROL 文件]**.
1. 选择包含资产的资产或文件夹。 在工具栏中，单击 **[!UICONTROL 共享链接]**.
1. 的 **[!UICONTROL 链接共享]** 对话框中，其中包含一个自动生成的资产链接，位于 **[!UICONTROL 共享链接]** 字段。
1. 复制资产链接并将其与用户共享。

### 通过电子邮件通知共享资产链接 {#share-assets-link-through-email}

要通过电子邮件共享资产，请执行以下操作：

1. 选择包含资产的资产或文件夹。 在工具栏中，单击 **[!UICONTROL 共享链接]**.
1. 的 **[!UICONTROL 链接共享]** 对话框中，其中包含一个自动生成的资产链接，位于 **[!UICONTROL 共享链接]** 字段。

   * 在电子邮件地址框中，键入要与其共享链接的用户的电子邮件ID。 您可以与多个用户共享该链接。 如果用户是您组织的成员，请从下拉列表中显示的建议中选择其电子邮件ID。 如果用户是外部用户，请键入完整的电子邮件ID并按 **[!UICONTROL 输入]**;电子邮件ID会添加到用户列表。

   * 在 **[!UICONTROL 主题]** 框中，键入一个主题以指定共享资产的用途。
   * 在 **[!UICONTROL 消息]** 框中，根据需要键入消息。
   * 在 **[!UICONTROL 过期]** 字段中，使用日期选取器指定链接的过期日期和时间。
   * 启用 **[!UICONTROL 允许下载原始文件]** 复选框以允许收件人下载原始演绎版。

1. 单击&#x200B;**[!UICONTROL 共享]**。系统会显示一条消息，确认已与用户共享该链接。 用户会收到一封包含共享链接的电子邮件。

![链接共享电子邮件](assets/link-sharing-email-notification.png)

### 使用资产链接下载资产

任何有权访问共享资产链接的用户都可以下载zip文件夹中捆绑的资产。 无论用户是访问复制的资产链接，还是使用通过电子邮件共享的资产链接，下载过程都是相同的。

* 单击资产链接或将URL粘贴到浏览器中。 的 [!UICONTROL 链接共享] 接口打开，您可以在其中切换到 [!UICONTROL 卡片视图] 或 [!UICONTROL 列表视图].

* 在 [!UICONTROL 卡片视图]，您可以将鼠标悬停在共享资产或共享资产文件夹上，以选择资产或将其排入队列进行下载。

* 默认情况下，用户界面会显示 **[!UICONTROL 下载收件箱]** 选项。 它反映已排队等待下载的所有共享资产或文件夹的列表及其状态。

* 选择资产或文件夹时， **[!UICONTROL 队列下载]** 选项。 单击 **[!UICONTROL 队列下载]** 选项启动下载过程。

   ![队列下载](assets/queue-download.png)

* 准备下载文件时，单击 **[!UICONTROL 下载收件箱]** 选项来查看下载的状态。 对于大型下载，请单击 **[!UICONTROL 刷新]** 按钮以更新状态。

   ![下载收件箱](assets/link-sharing-download-inbox.png)

* 处理完成后，单击 **[!UICONTROL 下载]** 按钮下载zip文件。

<!--
You can also copy the auto-generated link and share it with the users. The default expiration time for the link is one day.
-->

>[!NOTE]
>
>如果共享资产被移动到其他位置，则其链接会停止工作。 重新创建链接并与用户重新共享。


<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to Experience Manager Assets.

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

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single Experience Manager author instance. For publish, provide the URL for the publish instance.

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
   >Experience Manager supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## 单独下载资产和共享 {#download-and-share-assets}

用户可以下载所需的资产，并在 [!DNL Experience Manager]. 有关更多信息，请参阅 [如何搜索资产](/help/assets/search-assets.md), [如何下载资产](/help/assets/download-assets-from-aem.md)和 [如何下载收藏集](manage-collections.md#download-a-collection)

## 与创意专业人士共享资产 {#share-with-creatives}

营销人员和业务线用户可以使用

* **Experience Manager桌面应用程序**:该应用程序在Windows和Mac上工作。 请参阅 [桌面应用程序概述](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html). 要了解任何授权桌面用户如何轻松访问共享资产，请参阅 [浏览、搜索和预览资产](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). 桌面用户可以创建资产并将其与作为Experience Manager用户的对应用户共享，例如，通过上传新图像。 请参阅 [使用桌面应用程序上传资产](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Adobe资产链接**:创意专业人士可以直接从内部搜索和使用资产 [!DNL Adobe InDesign], [!DNL Adobe Illustrator]和 [!DNL Adobe Photoshop].

## 配置资产共享 {#configure-sharing}

共享资产的不同选项需要进行特定配置，并且具有特定的先决条件。

### 配置资产链接共享 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

要为要与用户共享的资产生成URL，请使用链接共享对话框。 具有管理员权限或具有读取权限的用户位于 `/var/dam/share` 位置可以查看与其共享的链接。 通过链接共享资产是使外部各方无需首先登录即可获得资源的一种便捷方式 [!DNL Assets].

>[!NOTE]
>
>如果要将来自创作实例的链接共享到外部实体，请确保仅显示以下URL `GET` 请求。 阻止其他URL以确保创作实例的安全。
>
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.
### Configure maximum data size {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, Experience Manager compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. To secure the system from a potential denial of service attack due to this situation, you can configure the maximum size of the downloaded files. If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click/Tap the Experience Manager logo and then go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Save the changes.
-->

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### 允许桌面操作与桌面应用程序一起使用 {#desktop-actions}

从 [!DNL Assets] 用户界面中，您可以浏览资产位置或签出，然后打开资产以在桌面应用程序中进行编辑。 这些选项称为桌面操作，要启用它，请参阅 [启用桌面操作 [!DNL Assets] web界面](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2).

![使用桌面应用程序时，允许桌面操作用作快捷方式](assets/enable_desktop_actions.png)

### 要使用的配置 [!DNL Adobe Asset Link] {#configure-asset-link}

Adobe资产链接可简化内容创建过程中创意人员与营销人员之间的协作。 它连接 [!DNL Adobe Experience Manager Assets] with [!DNL Creative Cloud] 桌面应用程序 [!DNL Adobe InDesign], [!DNL Adobe Photoshop]和 [!DNL Adobe Illustrator]. 的 [!DNL Adobe Asset Link] 面板允许创意人员访问和修改 [!DNL Assets] 不离开他们最熟悉的创意应用程序。

请参阅 [如何配置 [!DNL Assets] 使用 [!DNL Adobe Asset Link]](https://helpx.adobe.com/cn/enterprise/using/configure-aem-assets-for-asset-link.html).

## 最佳实践和疑难解答 {#bestpractices}

* 名称中包含空格的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享的资产，请与Experience Manager管理员确认 [下载限制](#maxdatasize) 。
* 要使用户预览使用链接共享共享的视频，该视频必须在 `/jcr:content/renditions` 在存储库中视频节点的位置。 预览的可用性不取决于 [!DNL Dynamic Media] 演绎版。
* 通过链接共享下载视频资产时， [!DNL Dynamic Media] 下载的存档中不包含演绎版。

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your Experience Manager administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->
