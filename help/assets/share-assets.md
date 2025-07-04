---
title: 分发和共享资源、文件夹和收藏集
description: 使用共享作为链接、下载和通过 [!DNL Brand Portal]、 [!DNL desktop app]和 [!DNL Asset Link]等方法分发您的数字资源。
feature: Asset Management, Collaboration, Asset Distribution
role: Admin, User
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 3%

---

# 共享和分发在[!DNL Experience Manager]中管理的资源 {#share-assets-from-aem}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/link-sharing.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Experience Manager Assets]允许您与组织成员和外部实体（包括合作伙伴和供应商）共享资产、文件夹和收藏集。 使用以下方法以[!DNL Cloud Service]的形式共享[!DNL Experience Manager Assets]中的资源：

* [共享为链接](#sharelink)。
* [下载资源](/help/assets/download-assets-from-aem.md)并单独共享。
* 使用[[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=zh-Hans)共享。
* 使用[[!DNL Adobe Asset Link]](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html)共享。
* 使用[[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=zh-Hans)共享。

## 先决条件 {#prerequisites}

您需要管理员权限才能[配置以链接](#config-link-share-settings)形式共享资产的设置。

## 配置链接共享设置 {#config-link-share-settings}

[!DNL Experience Manager Assets]允许您配置默认链接共享设置。

1. 单击[!DNL Experience Manager]徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL Assets配置]** > **[!UICONTROL 链接共享]**。
1. 初始设置：

   * **包含原始内容：**

      * 选择`Select Include Originals`以在链接共享对话框中选择默认的`Include Originals`选项。
      * 选择`Include Originals`选项在链接共享对话框上的呈现方式。 [!UICONTROL 可编辑]允许用户更改此处在“初始设置”中定义的设置。 对于`Read-only`，将显示设置，但无法修改设置。 `Hidden`将隐藏设置，并使用在初始设置中在此配置的值。
   * **包括格式副本：**
      * 选择`Select Include Renditions`选项以在链接共享对话框中选择默认的`Include Renditions`选项。
      * 选择`Include Renditions`选项在链接共享对话框上的呈现方式。 [!UICONTROL 可编辑]允许用户更改此处在“初始设置”中定义的设置。 对于`Read-only`，将显示设置，但无法修改设置。 `Hidden`将隐藏设置，并使用在初始设置中在此配置的值。

1. 在`Expiration date`部分的`Validity Period`字段中指定链接的默认有效期。

1. 操作栏中的&#x200B;**[!UICONTROL 链接共享]**&#x200B;按钮：
   * 所有具有`jcr:modifyAccessControl`权限的用户都可以查看[!UICONTROL 链接共享]选项。 默认情况下，它对所有管理员都可见。 默认情况下，[!UICONTROL 链接共享]按钮对所有人可见。 可以配置为仅对定义的组显示此选项，也可以从特定组拒绝此选项。 如果要允许特定组查看`Share Link`选项，请选择`Allow only for groups`。 选择`Deny from groups`以拒绝来自特定组的`Share Link`选项。 选择任意这些选项后，使用`Select Groups`字段指定组名以添加需要允许或拒绝的组名。

有关电子邮件配置的相关设置，请访问[电子邮件服务文档](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/email-service.html?lang=zh-Hans)

![配置电子邮件服务](/help/assets/assets/config-email-service.png)

## 以链接方式共享资产 {#sharelink}

通过链接共享资产是一种向外部参与方、营销人员和其他[!DNL Experience Manager]用户提供资源的便捷方式。 该功能允许匿名用户访问和下载与其共享的资产。 从共享链接下载资源时，[!DNL Experience Manager Assets]使用异步服务，该服务可提供更快且无中断的下载。 要下载的资产将在后台排入可管理文件大小的ZIP存档中。 对于大型下载，下载将捆绑到每个文件大小100 GB的多个文件中。

<!--
Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. 
-->

>[!NOTE]
>
>* 您需要对要作为链接共享的文件夹或资产具有“编辑ACL”权限。
>* [在与用户共享链接之前，启用出站电子邮件](/help/implementing/developing/introduction/development-guidelines.md#sending-email)。

可使用链接共享功能以两种方式共享资源：

1. 生成共享链接[复制，并与其他用户共享资产链接](#copy-and-share-assets-link)。
1. 生成共享链接并[通过电子邮件共享资产链接](#share-assets-link-through-email)。 您可以修改默认值（如过期日期和时间），并允许下载原始资源及其演绎版。 您可以通过添加多个用户的电子邮件地址来向其发送电子邮件。

   ![链接共享对话框](assets/share-link.png)

在这两种情况下，都可以修改默认值（如过期日期和时间），并允许下载原始资源及其演绎版。

### 复制并共享资产链接{#copy-and-share-asset-link}

要将资产共享为公共URL，请执行以下操作：

1. 登录到[!DNL Experience Manager Assets]并导航到&#x200B;**[!UICONTROL 文件]**。
1. 选择资源或包含资源的文件夹。 在工具栏中，单击&#x200B;**[!UICONTROL 共享链接]**。
1. 出现&#x200B;**[!UICONTROL 链接共享]**&#x200B;对话框，其中在&#x200B;**[!UICONTROL 共享链接]**&#x200B;字段中包含自动生成的资源链接。
1. 根据需要设置共享链接的过期日期。
1. 在&#x200B;**[!UICONTROL 链接设置]**&#x200B;下，选中或取消选中`Include Originals`或`Include Renditions`以包含或排除其中任一项。 必须选择至少一个选项。
1. 选定Assets的名称显示在[!DNL Share Link]对话框的右列。
1. 复制资产链接并与用户共享。

### 通过电子邮件通知共享资产链接 {#share-assets-link-through-email}

要通过电子邮件共享资源，请执行以下操作：

1. 选择资源或包含资源的文件夹。 在工具栏中，单击&#x200B;**[!UICONTROL 共享链接]**。
1. 出现&#x200B;**[!UICONTROL 链接共享]**&#x200B;对话框，其中在&#x200B;**[!UICONTROL 共享链接]**&#x200B;字段中包含自动生成的资源链接。

   * 在电子邮件地址框中，键入要与其共享链接的用户的电子邮件地址。 您可以与多个用户共享该链接。 如果用户是您组织的成员，请从下拉列表中显示的建议中选择其电子邮件地址。 在电子邮件地址文本字段中，键入要与其共享链接的用户电子邮件地址，然后单击[!UICONTROL 输入]。 您可以与多个用户共享该链接。

   * 在&#x200B;**[!UICONTROL 主题]**&#x200B;框中，键入主题以指定共享资源的用途。
   * 在&#x200B;**[!UICONTROL 消息]**&#x200B;框中，根据需要键入消息。
   * 在&#x200B;**[!UICONTROL 过期]**&#x200B;字段中，使用日期选取器指定链接的过期日期和时间。
   * 启用&#x200B;**[!UICONTROL 允许下载原始文件]**&#x200B;复选框，以允许收件人下载原始演绎版。

1. 单击&#x200B;**[!UICONTROL 共享]**。 将显示一条消息，确认该链接已与用户共享。 用户将收到一封包含共享链接的电子邮件。

   ![链接共享电子邮件](assets/link-sharing-email-notification.png)

### 自定义电子邮件模板 {#customize-email-template}

设计良好的模板可传达专业精神和能力，提高您的信息和组织的信誉。 [!DNL Adobe Experience Manager]允许您自定义电子邮件模板，该模板将发送给接收包含共享链接的电子邮件的收件人。 此外，自定义电子邮件模板允许通过为收件人指定名称并引用与他们相关的特定详细信息来对电子邮件内容进行个性化设置。 这种个人接触可能会让收件人感受到价值，并增加参与度。 不仅如此，自定义模板还可确保您的电子邮件与品牌标识一致，包括徽标、颜色和字体。 一致性加强了品牌认知和收件人之间的信任。

#### 自定义电子邮件模板的格式 {#format-of-custom-email-template}

可使用纯文本或HTML自定义电子邮件模板。 可在`/libs/settings/dam/adhocassetshare/en.txt`找到默认的可编辑模板链接。 您可以通过创建文件`/apps/settings/dam/adhocassetshare/en.txt`来覆盖模板。 您可以根据需要多次修改电子邮件模板。

| 占位符 | 描述 |
|---|-----|
| `${emailSubject}` | 电子邮件的主题 |
| `${emailInitiator}` | 创建电子邮件的用户的电子邮件ID |
| `${emailMessage}` | 电子邮件正文 |
| `${pagePath}` | 共享链接的URL |
| `${linkExpiry}` | 共享链接到期日期 |

<!--| `${host.prefix}` | Origin of the [!DNL Experience Manager] instance, for example `http://www.adobe.com"` |-->

#### 自定义电子邮件模板示例 {#custom-email-template-example}

```
subject: ${emailSubject}

<!DOCTYPE html>
<html><body>
<p><strong>${emailInitiator}</strong> invited you to review assets.</p>
<p>${emailMessage}</p>
<p>The shared link will be available until ${linkExpiry}.
<p>
    <a href="${pagePath}" target="_blank"><strong>Open</strong></a>
</p>

</body></html>
```

<!--Sent from instance: ${host.prefix}-->

### 使用资源链接下载资源 {#download-assets-using-asset-link}

任何有权访问共享资源链接的用户都可以下载捆绑在zip文件夹中的资源。 无论用户是访问复制的资产链接，还是使用通过电子邮件共享的资产链接，下载过程都是相同的。

* 单击资产链接或在浏览器中粘贴该URL。 [!UICONTROL 链接共享]界面打开，您可以在其中切换到[!UICONTROL 卡片视图]或[!UICONTROL 列表视图]。

* 在[!UICONTROL 卡片视图]中，您可以将鼠标悬停在共享资源或共享资源文件夹上以选择资源或将它们排入下载队列。

* 默认情况下，用户界面显示&#x200B;**[!UICONTROL 下载收件箱]**&#x200B;选项。 它反映已排队等待下载的所有共享资源或文件夹的列表及其状态。

* 选择资源或文件夹时，屏幕上会显示&#x200B;**[!UICONTROL 队列下载]**&#x200B;选项。 单击&#x200B;**[!UICONTROL 队列下载]**&#x200B;选项以启动下载过程。

  ![将下载排入队列](assets/queue-download.png)

* 准备下载文件时，单击&#x200B;**[!UICONTROL 下载收件箱]**&#x200B;选项可查看下载状态。 对于大型下载，单击&#x200B;**[!UICONTROL 刷新]**&#x200B;按钮以更新状态。

  ![下载收件箱](assets/link-sharing-download-inbox.png)

* 处理完成后，单击&#x200B;**[!UICONTROL 下载]**&#x200B;按钮下载zip文件。

<!--
You can also copy the auto-generated link and share it with the users. The default expiration time for the link is one day.
-->

>[!NOTE]
>
>如果将共享资源移动到其他位置，则其链接将停止工作。 重新创建链接并与用户重新共享。


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

用户可以下载所需的资产，并在[!DNL Experience Manager]之外共享这些资产。 有关详细信息，请参阅[如何搜索资产](/help/assets/search-assets.md)、[如何下载资产](/help/assets/download-assets-from-aem.md)和[如何下载收藏集](manage-collections.md#download-a-collection)

## 与创意专业人士共享资源 {#share-with-creatives}

营销人员和业务线用户可以轻松地与其创意专业人士共享经过批准的资产，

* **Experience Manager桌面应用程序**：该应用程序可在Windows和Mac上运行。 请参阅[桌面应用概述](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=zh-Hans)。 要了解任何授权桌面用户如何轻松访问共享资源，请参阅[浏览、搜索和预览资源](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hans#browse-search-preview-assets)。 桌面用户可以创建资源，并通过上传新图像等方式，与作为Experience Manager用户的交易方共享该资源。 请参阅[使用桌面应用程序上传资源](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hans#upload-and-add-new-assets-to-aem)。

* **Adobe Asset Link**：创意专业人士可以直接从[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]和[!DNL Adobe Photoshop]中搜索和使用资源。

## 配置资源共享 {#configure-sharing}

共享资产的不同选项需要特定配置并具有特定先决条件。

### 配置资产链接共享 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

要为要与用户共享的资源生成URL，请使用链接共享对话框。 具有管理员权限或在`/var/dam/share`位置具有读取权限的用户可以查看与其共享的链接。 通过链接共享资产是一种便利的方法，使外部参与方无需先登录[!DNL Assets]即可使用资源。

>[!NOTE]
>
>如果要将来自创作实例的链接共享到外部实体，请确保仅公开`GET`请求的以下URL。 阻止其他URL以确保您的创作实例安全。
>
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`

<!--
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password
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

### 启用桌面操作以与桌面应用程序一起使用 {#desktop-actions}

从浏览器的[!DNL Assets]用户界面中，您可以浏览资产位置或签出并打开资产以在桌面应用程序中编辑。 这些选项称为桌面操作，要启用它，请参阅[在 [!DNL Assets] Web界面](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hans#desktopactions-v2)中启用桌面操作。

![启用桌面操作以用作桌面应用程序时的快捷方式](assets/enable_desktop_actions.png)

### 要使用[!DNL Adobe Asset Link]的配置 {#configure-asset-link}

Adobe Asset Link可简化内容创建过程中创意专业人士与营销人员之间的协作。 它将[!DNL Adobe Experience Manager Assets]与[!DNL Creative Cloud]桌面应用程序、[!DNL Adobe InDesign]、[!DNL Adobe Photoshop]和[!DNL Adobe Illustrator]连接。 [!DNL Adobe Asset Link]面板允许创意人员访问和修改存储在[!DNL Assets]中的内容，而无需离开他们最熟悉的创意应用。

请参阅[如何配置 [!DNL Assets] 以将其与 [!DNL Adobe Asset Link]](https://helpx.adobe.com/cn/enterprise/using/configure-aem-assets-for-asset-link.html)一起使用。

## 最佳实践和疑难解答 {#bestpractices}

* 名称中包含空格的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享资源，请与Experience Manager管理员确认下载限制是什么。 默认值为100 MB。
* 对于要预览使用链接共享共享的视频的用户，该视频必须在存储库中视频节点的`/jcr:content/renditions`位置具有可用的静态视频演绎版。 预览不依赖于[!DNL Dynamic Media]演绎版的可用性。
* 通过链接共享下载视频资源时，[!DNL Dynamic Media]演绎版未包含在下载的存档中。

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your Experience Manager administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

