---
title: 管理视频资源
description: 在 [!DNL Adobe Experience Manager]中上传、预览、注释和发布视频资源。
contentOwner: AG
feature: Asset Management, Publishing, Collaboration, Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '5001'
ht-degree: 6%

---

# 管理视频资源 {#manage-video-assets}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=en) |
| AEM as a Cloud Service | 本文 |

视频格式是组织数字资产的重要组成部分。 [!DNL Adobe Experience Manager]提供了成熟的产品和功能，可在创建视频资产后管理其整个生命周期。

了解如何在[!DNL Adobe Experience Manager Assets]中管理和编辑视频资产。 可以使用“处理配置文件”和[!DNL Dynamic Media]集成进行视频编码和转码，例如FFmpeg转码。 如果没有[!DNL Dynamic Media]许可证，[!DNL Experience Manager]将为视频提供基本支持，例如使用FFmpeg进行转码，提取支持文件格式的预览缩略图，以及在用户界面中预览支持直接在浏览器中播放的格式。

## 上传和预览视频资产 {#upload-and-preview-video-assets}

您可以将支持格式的视频资产上传并预览到[!DNL Experience Manager Assets]。
<!-- It generates previews for video assets with the extension MP4. -->

### 上传视频资产

要上传视频资产，请执行以下步骤：

1. 在数字资源文件夹或子文件夹中，导航到需要添加资源的位置。
1. 从工具栏中单击&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 文件]**。 <br>或者，在用户界面上拖动文件。
了解有关[在[!DNL Experience Manager Assets]中上传资产](manage-digital-assets.md#uploading-assets)的更多信息。

<!-- 1. To preview a video in the card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. You can pause or play video in the card view only. The [!UICONTROL Play] and [!UICONTROL Pause] options are not available in the list view.
1. To preview the video in the asset details page, select **[!UICONTROL Edit]** on the card. The video plays in the native video player of the browser. You can play, pause, control the volume, and zoom the video to full screen. -->

### 预览视频资产

您可以在[!DNL Assets]用户界面中预览受支持的呈现形式的视频。 要预览视频资源，请执行以下步骤：

1. 将支持格式的视频资产上传到[!DNL Experience Manager Assets]。 了解有关[支持的视频格式](file-format-support.md#video-formats)的详细信息。 <br>上传后，将处理视频资源并生成预览演绎版。
1. 单击资产，然后从顶部工具栏中选择![详细信息选项](assets/do-not-localize/details_icon.svg) **[!UICONTROL 详细信息]**。 视频资产将在视频查看器中打开。
1. 单击视频缩略图上的![播放选项](assets/do-not-localize/play.png)图标。 <br>您可以播放、暂停、控制音量以及将视频缩放到全屏。

对于[!DNL Experience Manager Assets]中的现有视频资源，您需要&#x200B;**[!UICONTROL 重新处理[!DNL Experience Manager]中的资源]**&#x200B;以启用视频预览功能。 了解如何在[!DNL Experience Manager]中[重新处理数字资产](reprocessing.md)。

### 视频预览的限制

* 即使生成了演绎版，MXF文件也不会显示视频预览。
* WebM文件不会生成预览呈现版本，因为它们可以由Web浏览器本机播放。

## Publish视频资源 {#publish-video-assets}

发布后，您可以将视频资产作为URL包含在网页中，或直接嵌入这些资产。 有关详细信息，请参阅[发布 [!DNL Dynamic Media] 资源](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## Publish到YouTube的视频 {#publishing-videos-to-youtube}

您可以将在Experience Manager Assets中管理的视频资产直接发布到之前创建的YouTube渠道。

要将视频资源发布到YouTube，您需要在Experience Manager Assets中使用标记来标记视频资源。 将这些标记与YouTube渠道关联。 如果视频资产的标记与YouTube渠道的标记匹配，则视频将发布到YouTube。 只要使用关联的标记，Publish到YouTube的操作就会与视频的正常发布同时进行。

YouTube自行编码。 因此，上传到Experience Manager的原始视频文件会发布到YouTube，而不是Dynamic Media的编码创建的任何视频演绎版。 虽然无需使用Dynamic Media处理视频，但预计可在播放时需要查看器预设时这样做。

当您绕过视频处理配置文件并直接发布到YouTube时，这仅仅意味着您在Experience Manager资源中的视频资源没有获取可查看的缩略图。 它还意味着未编码的视频不适用于任何Dynamic Media资源类型。

将视频资产发布到YouTube服务器需要完成以下任务，以确保通过YouTube进行安全可靠的服务器到服务器验证：

1. [配置Google云设置](#configuring-google-cloud-settings)
1. [创建YouTube渠道](#creating-a-youtube-channel)
1. [添加标记以进行发布](#adding-tags-for-publishing)
1. [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem)
1. [（可选）自动为您上传的视频设置默认YouTube属性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publish视频到您的YouTube渠道](#publishing-videos-to-your-youtube-channel)
1. [（可选）验证YouTube上发布的视频](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [将YouTube URL关联到您的Web应用程序](#linking-youtube-urls-to-your-web-application)

您还可以[取消发布视频以将其从YouTube](#unpublishing-videos-to-remove-them-from-youtube)中删除。

### 配置Google云设置 {#configuring-google-cloud-settings}

要发布到YouTube，您需要Google帐户。 如果您拥有GMAIL帐户，则表明您已经拥有Google帐户；如果您没有Google帐户，则可以轻松创建一个帐户。 您需要帐户，因为您需要凭据才能将视频资产发布到YouTube。<!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

用于Google Cloud的帐户和用于YouTube的Google帐户不需要相同。

Google会定期更改其用户界面。 因此，将视频发布到YouTube的步骤可能与以下文档记录的内容略有不同。 当您尝试检查视频是否已上传到YouTube时，此警告也适用。

>[!NOTE]
>
>在编写本报告时，以下步骤是准确的。 但是，Google会定期更新其云网页，恕不另行通知。 因此，某些配置选项在Google用户界面中的名称可能与步骤中使用的名称略有不同。

**配置Google Cloud设置：**

1. 创建一个Google帐户。

   如果您已经拥有Google帐户，则可以跳至下一步。

1. 转到[https://cloud.google.com/](https://cloud.google.com/)。
1. 在&#x200B;**[!UICONTROL Google Cloud]**&#x200B;页面的右上角附近，选择&#x200B;**[!UICONTROL 控制台]**。

   如有必要，请使用您的Google帐户凭据&#x200B;**[!UICONTROL 登录]**&#x200B;以查看&#x200B;**[!UICONTROL 控制台]**&#x200B;选项。

1. 在&#x200B;**[!UICONTROL 功能板]**&#x200B;页面的&#x200B;**[!UICONTROL Google Cloud Platform]**&#x200B;右侧，选择&#x200B;**[!UICONTROL 项目]**&#x200B;下拉列表以打开&#x200B;**[!UICONTROL 选择项目]**&#x200B;对话框。
1. 在&#x200B;**[!UICONTROL 选择项目]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL 新建项目]**。
1. 在&#x200B;**[!UICONTROL 新建项目]**&#x200B;对话框的&#x200B;**[!UICONTROL 项目名称]**&#x200B;字段中，键入新项目的名称。

   您的项目ID基于您的项目名称。 因此，请仔细选择项目名称；在创建项目后无法对其进行更改。 此外，稍后在Experience Manager中设置YouTube时，必须再次输入相同的项目ID。 所以，写下来。

1. 选择&#x200B;**[!UICONTROL 创建]**。

1. 执行以下任一操作：

   * 在项目的仪表板的&#x200B;**[!UICONTROL 快速入门]**&#x200B;信息卡中，选择&#x200B;**[!UICONTROL 浏览并启用API]**。
   * 在项目的仪表板的&#x200B;**[!UICONTROL API]**&#x200B;信息卡中，选择&#x200B;**[!UICONTROL 转到API概述]**。

1. 在&#x200B;**[!UICONTROL API和服务]**&#x200B;页面的顶部中间附近，选择&#x200B;**[!UICONTROL 启用API和服务]**。<!-- NEXT STEP BELOW IS STEP 10 -->
1. 在&#x200B;**[!UICONTROL API库]**&#x200B;页面的左侧&#x200B;**[!UICONTROL 类别]**&#x200B;下，选择&#x200B;**[!UICONTROL YouTube]**。 选择页面右侧的&#x200B;**[!UICONTROL YouTube]**。
1. 在&#x200B;**[!UICONTROL YouTube]**&#x200B;页面上，选择&#x200B;**[!UICONTROL YouTube Data API v3]**。
1. 在&#x200B;**[!UICONTROL YouTube Data API v3]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 管理]**。

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. 要使用API，您需要凭据。 如有必要，请在&#x200B;**[!UICONTROL API和服务]**&#x200B;页面的左侧选择&#x200B;**[!UICONTROL 凭据]**。
1. 在&#x200B;**[!UICONTROL 凭据]**&#x200B;页面顶部附近，选择&#x200B;**[!UICONTROL 创建凭据]**，然后选择&#x200B;**[!UICONTROL OAuth客户端ID]**。
1. 在&#x200B;**[!UICONTROL 创建OAuth客户端ID]**&#x200B;页面的&#x200B;**[!UICONTROL 应用程序类型]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL Web应用程序]**。

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. 执行下列操作之一：

   * 在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，输入OAuth 2.0客户端的唯一名称。
   * 使用Google已在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中提供的默认名称。

1. 在&#x200B;**[!UICONTROL 授权的JavaScript源]**&#x200B;标题下，选择&#x200B;**[!UICONTROL 添加URI]**。

   ![6_5_googleaccount-apis-nameauthorizations](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. 在&#x200B;**[!UICONTROL URI]**&#x200B;文本字段中，输入以下路径，在路径中替换您自己的域和端口号，然后按&#x200B;**[!UICONTROL Enter]**&#x200B;将路径添加到列表中：

   `https://<servername.domain>:<port_number>`

   例如，`https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >上述URI路径示例是假设性的，仅用于解释。

1. 在&#x200B;**[!UICONTROL 授权重定向URI]**&#x200B;标题下，选择“添加URI”。
1. 在&#x200B;**[!UICONTROL URI]**&#x200B;文本字段中，输入以下路径，在路径中替换您自己的域和端口号，然后按&#x200B;**[!UICONTROL Enter]**&#x200B;将路径添加到列表中：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如，`https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >上述URI路径示例是假设性的，仅用于解释。

1. 在&#x200B;**[!UICONTROL 创建OAuth客户端ID]**&#x200B;页面的底部附近，选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL OAuth客户端已创建]**&#x200B;对话框中，执行以下操作：

   * （可选）复制&#x200B;**[!UICONTROL 您的客户端ID]**&#x200B;和&#x200B;**[!UICONTROL 您的客户端密钥]**&#x200B;字段中的值并保存。
   * 选择&#x200B;**[!UICONTROL 下载JSON]**，然后保存JSON文件。

   稍后在Adobe Experience Manager中设置YouTube时，您需要此下载的JSON文件。

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. 在&#x200B;**[!UICONTROL OAuth客户端已创建]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL 确定]**。
1. 注销Google帐户。 现在创建一个YouTube渠道。

### 创建YouTube渠道 {#creating-a-youtube-channel}

将视频发布到YouTube要求您拥有一个或多个渠道。 如果您已创建YouTube渠道，则可以跳过此任务并转到[添加标记以进行发布](/help/assets/dynamic-media/video.md#adding-tags-for-publishing)。

>[!CAUTION]
>
>请确保在&#x200B;*之前已在YouTube*&#x200B;中设置了一个或多个渠道，然后在Experience Manager的YouTube设置下添加渠道(请参阅下面的[在Experience Manager中设置YouTube](#setting-up-youtube-in-aem))。 如果无法设置渠道，则不会警告您不存在任何现有渠道。 但是，在添加频道时，Google验证仍会进行，但无法选择发送视频的频道。

**要创建YouTube频道：**

1. 转到[https://www.youtube.com](https://www.youtube.com/)并使用您的Google帐户凭据登录。
1. 在YouTube页面的右上角，选择您的个人资料图片（它也可以显示为实色圆圈中的字母），然后选择&#x200B;**[!UICONTROL YouTube设置]**（圆形齿轮图标）。
1. 在“概述”页面的“其他功能”标题下，选择&#x200B;**[!UICONTROL 查看我的所有渠道或创建渠道]**。
1. 在“渠道”页面上，选择&#x200B;**[!UICONTROL 创建新渠道]**。
1. 在“品牌帐户”页面的“品牌帐户名称”字段中，输入要发布视频资产的位置的公司名称或任何其他渠道名称，然后选择&#x200B;**[!UICONTROL 创建]**。

   请记住您在此处输入的名称；在必须在Experience Manager中设置YouTube时，必须再次输入该名称。

1. （可选）如有必要，请添加更多渠道。

   现在，您可以添加标记以进行发布。

### 添加标记以进行发布 {#adding-tags-for-publishing}

要将视频发布到YouTube，Experience Manager会将标记与一个或多个YouTube渠道关联。 要添加标记以进行发布，请参阅[管理标记](/help/sites-cloud/authoring/sites-console/tags.md)。

或者，如果您打算在Experience Manager中使用默认标记，则可以跳过此任务并转到[在Experience Manager中设置YouTube](#setting-up-youtube-in-aem)。

>[!NOTE]
>
>配置Cloud Service后，无需进行其他配置即可在此时启用YouTube Publish复制代理。 原因是保存Cloud Service配置时启用了它。

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### 在Experience Manager中设置YouTube {#setting-up-youtube-in-aem}

从Experience Manager6.4开始，引入了一种新的触屏用户界面方法，用于在Experience Manager中设置YouTube发布。 根据您所使用的Experience Manager的安装实例，执行以下操作之一：

* 要在6.4之前的Experience Manager中配置YouTube，请参阅[在6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before)之前的Experience Manager中设置YouTube 。
* 要在Experience Manager6.4或更高版本中配置YouTube，请参阅[在Experience Manager6.4和更高版本中设置YouTube](#setting-up-youtube-in-aem-and-later)。

#### 在Experience Manager6.4及更高版本中设置YouTube {#setting-up-youtube-in-aem-and-later}

1. 确保以管理员身份登录到Dynamic Media实例。
1. 选择Experience Manager左上角的Experience Manager徽标，然后在左边栏中，导航到&#x200B;**[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL Cloud Service]** > **[!UICONTROL YouTube Publishing Configuration]**。
1. 选择&#x200B;**[!UICONTROL global]**（不要选择它）。

1. 在全局页面的右上角附近，选择&#x200B;**[!UICONTROL 创建]**。
1. 在“创建 YouTube 配置”页面的“Google Cloud Platform 设置”下的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   在之前配置Google Cloud设置时指定了项目ID。
保持创建YouTube配置页面处于打开状态；稍后您将返回到此页面。

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用纯文本编辑器，打开您之前在[配置Google云设置](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings)任务中下载并保存的JSON文件。
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 在页面的右上角附近，选择&#x200B;**[!UICONTROL 保存]**。

   现在在Experience Manager中设置YouTube渠道。

1. 选择&#x200B;**[!UICONTROL 添加频道]**。
1. 在“渠道名称”字段中，输入您在任务&#x200B;**[!UICONTROL 之前向YouTube添加一个或多个渠道]**&#x200B;中创建的渠道的名称。

   如果需要，您可以选择添加描述。

1. 选择&#x200B;**[!UICONTROL 添加]**。
1. 将显示YouTube/Google验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID关联的Google用户名和密码，以及上面的JSON文本。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择渠道。 不要选择电子邮件地址；它不是渠道。
   * 在下一页上，选择&#x200B;**[!UICONTROL 接受]**&#x200B;以允许对此渠道的访问。

1. 选择&#x200B;**[!UICONTROL 允许]**。

   现在设置标记以进行发布。

1. **[!UICONTROL 设置标记以进行发布]** — 在“Cloud Service”>“YouTube”页面上，选择铅笔图标以编辑要使用的标记列表。
1. 要在Experience Manager中显示可用标签列表，请选择下拉列表图标（上下倒置插入号）。
1. 要添加这些标记，请选择一个或多个标记。

   要删除已添加的标记，请选择该标记，然后选择&#x200B;**[!UICONTROL X]**。

1. 添加完所需的标记后，选择&#x200B;**[!UICONTROL 保存]**。

   现在，您可以将视频发布到YouTube渠道。

#### 在6.4之前的Experience Manager中设置YouTube {#setting-up-youtube-in-aem-before}

1. 确保以管理员身份登录到Dynamic Media实例。

1. 选择Experience Manager左上角的Experience Manager徽标，然后在左边栏中，导航到&#x200B;**[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 部署]** > **[!UICONTROL Cloud Service]**。
1. 在“第三方服务”标题的YouTube下，选择&#x200B;**[!UICONTROL 立即配置]**。
1. 在创建配置对话框中，在相应字段中输入标题（必填）和名称（可选）。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在“YouTube 帐户设置”对话框的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您在最初[配置Google Cloud设置](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings)时指定了项目ID。
保持YouTube帐户设置对话框处于打开状态；稍后您将返回到此对话框。

1. 使用纯文本编辑器，打开您之前在配置Google云设置任务中下载并保存的JSON文件。
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 选择&#x200B;**[!UICONTROL 确定]**。

   现在在Experience Manager中设置YouTube渠道。

1. 在&#x200B;**[!UICONTROL 可用频道]**&#x200B;的右侧，选择&#x200B;**+** （加号图标）。
1. 在“YouTube频道设置”对话框的“标题”字段中，输入您在之前向YouTube添加一个或多个频道任务中创建的频道 **[!UICONTROL 名称]** 。

   如果需要，您可以选择添加描述。

1. 选择&#x200B;**[!UICONTROL 确定]**。
1. 将显示YouTube/Google验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID关联的Google用户名和密码，以及上面的JSON文本。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择渠道。 不要选择电子邮件地址；它不是渠道。
   * 在下一页上，选择&#x200B;**[!UICONTROL 接受]**&#x200B;以允许对此渠道的访问。

1. 选择&#x200B;**[!UICONTROL 允许]**。

   现在设置标记以进行发布。

1. **[!UICONTROL 设置标记以进行发布]** — 在“Cloud Service”>“YouTube”页面上，选择铅笔图标以编辑要使用的标记列表。
1. 要在Experience Manager中显示可用标签列表，请选择下拉列表图标（上下倒置插入号）。
1. 要添加这些标记，请选择一个或多个标记。

   要删除已添加的标记，请选择该标记，然后选择&#x200B;**X**。

1. 完成添加所需标记后，选择&#x200B;**[!UICONTROL 确定]**。

   现在，您可以将视频发布到YouTube渠道。

### （可选）自动为您上传的视频设置默认YouTube属性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以选择在上传视频时自动设置YouTube属性。 在Experience Manager中创建元数据处理配置文件。

要创建元数据处理配置文件，您首先需要从&#x200B;**[!UICONTROL 字段标签]**、**[!UICONTROL 映射到属性]**&#x200B;和&#x200B;**[!UICONTROL 选择]**&#x200B;字段中复制值，所有这些字段均位于视频的元数据架构中。然后，您可以通过向处理配置文件添加这些值来构建您的YouTube视频元数据处理配置文件。

**要自动为上传的视频设置默认YouTube属性：**

1. 选择Experience Manager左上角的Experience Manager徽标，然后在左边栏中，导航到&#x200B;**[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。
1. 选择&#x200B;**[!UICONTROL 默认值]**。 （请勿在“default”左侧的选择框中添加复选标记。）
1. 在&#x200B;**[!UICONTROL 默认]**&#x200B;页面上，选中&#x200B;**[!UICONTROL 视频]**&#x200B;左侧的框，然后选择&#x200B;**[!UICONTROL 编辑]**。
1. 在“元数据架构编辑器”页面上，选择&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。
1. 在YouTube发布标题下，选择&#x200B;**[!UICONTROL YouTube类别]**。
1. 在页面右侧的&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡下，执行以下操作：

   * 在&#x200B;**[!UICONTROL 映射到属性]**文本字段中，选择并复制该值。
将复制的值粘贴到打开的文本编辑器中。 稍后在创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

   * 在&#x200B;**[!UICONTROL 选择]**下，选择并复制您要使用的默认值（如“人员”和“博客”或“科学和技术”）。
将复制的值粘贴到打开的文本编辑器中。 稍后在创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

1. 在YouTube发布标题下，选择&#x200B;**[!UICONTROL YouTube隐私]**。
1. 在页面右侧的&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡下，执行以下操作：

   * 在&#x200B;**[!UICONTROL 映射到属性]**文本字段中，选择并复制该值。
将复制的值粘贴到打开的文本编辑器中。 稍后在创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

   * 在&#x200B;**[!UICONTROL 选择]**下，选择并复制您要使用的默认值。 请注意，“选择”成对分组为两个组。 该对中的底部字段是您要复制的默认值，例如public、unlisted或private。
将复制的值粘贴到打开的文本编辑器中。 稍后在创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

1. 在元数据架构编辑器页面的右上角附近，选择&#x200B;**[!UICONTROL 取消]**。
1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中选择&#x200B;**[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL Assets]** > **[!UICONTROL 元数据配置文件]**。

1. 在“元数据配置文件”页面的右上角附近，选择&#x200B;**[!UICONTROL 创建]**。
1. 在“添加元数据配置文件”对话框的&#x200B;**[!UICONTROL 配置文件标题]**&#x200B;文本字段中，输入名称`YouTube Video`，然后选择&#x200B;**[!UICONTROL 创建]**。
1. 在“元数据配置文件编辑器”页面上，选择&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。
1. 通过执行以下操作，将复制的YouTube发布值添加到配置文件中：

   * 在页面的右侧，选择&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡。
   * （可选）将标有&#x200B;**[!UICONTROL 节标题]**&#x200B;的组件拖动到左侧，并将其放到表单区域中。
   * （可选）选择&#x200B;**[!UICONTROL 字段标签]**&#x200B;以选择组件。
   * （可选）在页面右侧的设置选项卡下，在字段标签文本字段中输入`YouTube Publishing`。
   * 选择&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡，然后将标有&#x200B;**[!UICONTROL 多值文本]**&#x200B;的组件拖放到您创建的&#x200B;**[!UICONTROL YouTube发布]**&#x200B;标题下。

   * 要选择组件，请选择&#x200B;**[!UICONTROL 字段标签]**。
   * 在页面的右侧，在“设置”选项卡下方，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上各自的字段中。 将“选项”值粘贴到“默认值”字段中。

1. 通过执行以下操作，将复制的YouTube隐私值添加到配置文件中：

   * 在页面的右侧，选择&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡。
   * （可选）将标有&#x200B;**[!UICONTROL 节标题]**&#x200B;的组件拖动到左侧，并将其放到表单区域中。
   * （可选）选择&#x200B;**[!UICONTROL 字段标签]**&#x200B;以选择组件。
   * （可选）在页面右侧的设置选项卡下，在字段标签文本字段中输入`YouTube Privacy`。
   * 选择&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡，然后将标有&#x200B;**[!UICONTROL 多值文本]**&#x200B;的组件拖放到您创建的&#x200B;**[!UICONTROL YouTube隐私]**&#x200B;标题下。

   * 要选择组件，请选择&#x200B;**[!UICONTROL 字段标签]**。
   * 在页面的右侧，在“设置”选项卡下方，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上各自的字段中。 将“选项”值粘贴到“默认值”字段中。

1. 在页面的右上角附近，选择&#x200B;**[!UICONTROL 保存]**。
1. 将YouTube发布元数据配置文件应用到要上传视频的文件夹。 您必须同时设置元数据配置文件和视频配置文件。

   请参阅 [元数据配置文件](/help/assets/metadata-profiles.md) 和视 [频配置文件](/help/assets/dynamic-media/video-profiles.md)。

### Publish视频到您的YouTube渠道 {#publishing-videos-to-your-youtube-channel}

现在，您将之前添加的标记关联到视频资产。 此过程可告知Experience Manager要发布到YouTube渠道的资产。

>[!NOTE]
>
>Publish不会立即自动发布到YouTube。 设置 Dynamic Media 时，有两种发布选项可供选择：**[!UICONTROL 立即]**&#x200B;或&#x200B;**[!UICONTROL 激活时]**。
>
>**[!UICONTROL Publish立即]**&#x200B;表示上传的资产（在与IPS同步之后）会自动发布到交付系统。 虽然这对Dynamic Media是这样，但对YouTube并非如此。 要发布到YouTube，必须通过Experience Manager创作方式发布。

>[!NOTE]
>
>要从YouTube发布内容，Experience Manager使用&#x200B;**[!UICONTROL Publish到YouTube]**&#x200B;工作流，该工作流允许您监视进度并查看任何失败信息。
>
>请参阅[监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress)。
>
>有关更详细的进度信息，您可以在复制下监视YouTube日志。 但是，请注意，此类监视需要管理员访问权限。

**要将视频发布到YouTube频道：**

1. 在Experience Manager中，导航到要发布到YouTube渠道的视频资源。
1. 选择视频资产（自适应视频集）。
1. 在工具栏上，选择&#x200B;**[!UICONTROL 属性]**。
1. 在“基本”选项卡的“元数据”标题下，选择“标记”字段右侧的&#x200B;**[!UICONTROL 打开选择对话框]**。
1. 在“选择标记”页面上，导航到要使用的标记，然后选择一个或多个标记。

   请记住，标记必须与YouTube渠道关联。

1. 在页面的右上角，选择&#x200B;**[!UICONTROL 选择]**。
1. 在视频属性页面的右上角，选择&#x200B;**[!UICONTROL 保存并关闭]**。
1. 在工具栏上，选择&#x200B;**[!UICONTROL 快速Publish]**。

   另请参阅[在Experience Manager Sites中使用发布管理](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring)。

   您可以选择在YouTube渠道中验证已发布的视频。

### （可选）验证YouTube上发布的视频 {#optional-verifying-the-published-video-on-youtube}

您可以选择监控YouTube发布（或取消发布）的进度。

请参阅[监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress)。

发布时间会因多种因素而有很大差异，这些因素包括主源视频的格式、文件大小和上传流量。 发布过程可能需要几分钟到几小时的时间。 此外，更高分辨率格式的呈现速度要慢得多。 例如，720p和1080p需要比480p更长的时间才能显示。

八小时后，如果您仍然看到一条状态消息，显示&#x200B;**[!UICONTROL 已上传（正在处理，请稍候）]**，请尝试从您的站点中删除视频并重新上传。

### 将YouTube URL关联到您的Web应用程序 {#linking-youtube-urls-to-your-web-application}

您可以获取Dynamic Media在发布视频后生成的YouTube URL字符串。 复制YouTube URL时，它会登陆剪贴板，以便您可以根据需要将其粘贴到网站或应用程序中的页面。

>[!NOTE]
>
>在将视频资产发布到YouTube之前，无法复制YouTube URL。

要将YouTube URL关联到您的Web应用程序，请执行以下操作：

1. 导航到&#x200B;*已发布的YouTube*&#x200B;视频资源，您要复制其URL，然后选择它。

   请记住，YouTube URL仅可在您首次&#x200B;*发布*&#x200B;视频资源到YouTube *后复制*。

1. 在工具栏上，选择&#x200B;**[!UICONTROL 属性]**。
1. 选择&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。
1. 在YouTube发布标题下的YouTube URL列表中，选择URL文本，并将其复制到Web浏览器，以预览资产或添加到Web内容页面。

### 取消发布视频，以便从YouTube中删除它们 {#unpublishing-videos-to-remove-them-from-youtube}

在Experience Manager中取消发布视频资源时，该视频将从YouTube中删除。

>[!CAUTION]
>
>如果直接从YouTube中删除视频，则Experience Manager不会察觉，并继续按照将视频发布到YouTube的方式运行。 始终通过Experience Manager从YouTube中取消发布视频资源。

>[!NOTE]
>
>要从YouTube中删除内容，Experience Manager使用&#x200B;**[!UICONTROL 从YouTube中取消发布]**&#x200B;工作流，该工作流允许您监视进度并查看任何失败信息。
>
>请参阅[监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress)。

**要取消发布视频以将其从YouTube中删除，请执行以下操作：**

1. 导航到要从YouTube渠道取消发布的视频资源。
1. 在资源选择模式下，选择一个或多个已发布的视频资源。
1. 在工具栏上，选择&#x200B;**[!UICONTROL 管理发布]**。 如有必要，请选择工具栏上的三个圆点图标(`. . .`)以查看&#x200B;**[!UICONTROL 管理发布]**。
1. 在“管理发布”页面上，选择&#x200B;**[!UICONTROL 取消发布]**。
1. 在页面的右上角，选择&#x200B;**[!UICONTROL 下一步]**。
1. 在页面的右上角，选择&#x200B;**[!UICONTROL 取消发布]**。

## 监控视频编码和YouTube发布进度 {#monitoring-video-encoding-and-youtube-publishing-progress}

在将新视频上传到应用了视频编码的文件夹时，或者将视频发布到YouTube时，监控视频编码/Youtube发布的进展情况（或失败）。 实际YouTube发布进度只能通过日志提供。 但是，无论成功还是失败，它都将以以下过程中描述的其他方式列出。 此外，当YouTube发布工作流或视频编码完成或中断时，您会收到电子邮件通知。

### 监测进度 {#monitoring-progress}

您可以监控进度，包括失败的编码/YouTube发布。

1. 在assets文件夹中查看视频编码进度：

   * 在卡片视图中，视频编码进度按百分比显示在资源上。 如果出现错误，资产上也会显示此信息。

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * 在列表视图中，视频编码进度显示在&#x200B;**[!UICONTROL 处理状态]**&#x200B;列中。 如果出现错误，则该列中将显示此消息。

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   默认情况下，此列不显示。若要启用该列，请从视图下拉菜单中选择&#x200B;**[!UICONTROL 查看设置]**，然后添加&#x200B;**[!UICONTROL 处理状态]**&#x200B;列，并选择&#x200B;**[!UICONTROL 更新]**。

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. 在资源详细信息中查看进度。 选择资产时，打开下拉菜单并选择&#x200B;**[!UICONTROL 时间轴]**。 要将其缩小到编码或YouTube发布等工作流活动，请选择&#x200B;**[!UICONTROL 工作流]**。

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   任何工作流信息（如编码）都会显示在时间轴中。 对于YouTube发布，工作流时间轴还包括YouTube渠道的名称和YouTube视频URL。 此外，发布完成后，您会在工作流时间轴中看到任何失败通知。

   >[!NOTE]
   >
   >由于来自[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)的&#x200B;**[!UICONTROL 重试]**、**[!UICONTROL 重试延迟]**&#x200B;和&#x200B;**[!UICONTROL 超时]**&#x200B;的多个工作流配置，最终记录失败/错误会花费较长时间，例如：
   >
   >* Apache Sling作业队列配置
   >* AdobeGranite工作流外部进程作业处理程序
   >* Granite工作流超时队列
   >
   >您可以调整这些配置中的&#x200B;**[!UICONTROL 重试]**、**[!UICONTROL 重试延迟]**&#x200B;和&#x200B;**[!UICONTROL 超时]**&#x200B;属性。

1. 有关进行中的工作流，请参阅“工具”>“工作流” **[!UICONTROL >“实例”中提供的“工作流实例]** ” **[!UICONTROL (Workflow]** ) **[!UICONTROL >“]**&#x200B;实例”。

   >[!NOTE]
   >
   >您需要管理权限才能访问&#x200B;**[!UICONTROL 工具]**&#x200B;菜单。

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   选择实例，然后选择&#x200B;**[!UICONTROL 打开历史记录]**。

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   您还可以从“工作流实例”区域暂停、终止或重命名工作流。 有关详细信息，请参阅[管理工作流](/help/sites-cloud/authoring/workflows/overview.md)。

1. 有关失败的作业，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 失败]**&#x200B;中显示的“工作流失败”。**[!UICONTROL 工作流失败]**&#x200B;列出所有失败的工作流活动。

   >[!NOTE]
   >
   >您需要管理权限才能访问&#x200B;**[!UICONTROL 工具]**&#x200B;菜单。

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >由于[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)中的&#x200B;**[!UICONTROL 重试]**、**[!UICONTROL 重试延迟]**&#x200B;和&#x200B;**[!UICONTROL 超时]**&#x200B;存在多个工作流配置，最终记录错误消息会花费较长时间，例如：
   >
   >* Apache Sling作业队列配置
   >* AdobeGranite工作流外部进程作业处理程序
   >* Granite工作流超时队列
   >
   >您可以调整这些配置中的&#x200B;**[!UICONTROL 重试]**、**[!UICONTROL 重试延迟]**&#x200B;和&#x200B;**[!UICONTROL 超时]**&#x200B;属性。

1. 有关已完成的工作流，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 存档]**&#x200B;中的可用工作流存档。**[!UICONTROL 工作流存档]**&#x200B;列出了所有已完成的工作流活动。

   >[!NOTE]
   >
   >您需要管理权限才能访问&#x200B;**[!UICONTROL 工具]**&#x200B;菜单。

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. 您会收到有关已中止或失败的工作流作业的电子邮件通知。 这些电子邮件通知可由管理员配置。 请参阅[配置电子邮件通知](#configuring-e-mail-notifications)。

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then select **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, select **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then select once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, select the Configuration icon (wrench). Select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, select the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, select **[!UICONTROL Sync]**.

-->

## 使用处理配置文件进行转码 {#transcode-video}

[!DNL Experience Manager]作为[!DNL Cloud Service]允许您使用处理配置文件对MP4视频文件进行基本转码。 利用功能，您不仅可以上传，还可以预览和缩放MP4视频文件。

![在[!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)中创建用于视频转码的处理配置文件

*图： [!DNL Experience Manager].*&#x200B;中用于视频转码的处理配置文件

如果只提供宽度或高度，并将其他字段留空，则格式副本将保持长宽比。 H.264视频编解码器可用于转码。

要使用处理配置文件处理资产，请将配置文件添加到文件夹。 请参阅[使用处理配置文件处理资产](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

## 为视频资源作批注 {#annotate-video-assets}

您可以向视频资产添加批注。 在对视频添加注释时，播放器会暂停以允许您在帧上添加注释。 有关详细信息，请参阅[管理视频资产](manage-video-assets.md)。

>[!NOTE]
>
>视频资产注释尚不支持MXF视频格式。

1. 从[!DNL Assets]控制台中，选择资产卡上的&#x200B;**[!UICONTROL 编辑]**&#x200B;以显示资产详细信息页面。
1. 要播放视频，请单击&#x200B;**[!UICONTROL 预览]**。
1. 要对视频添加批注，请单击&#x200B;**[!UICONTROL 批注]**。 在视频中的特定时间（帧）添加注释。 在注释时，可以在画布上绘制并在绘图中包括注释。 评论将自动保存。 要退出注释向导，请单击&#x200B;**[!UICONTROL 关闭]**。
1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。
1. 要在时间轴中查看注释，请单击注释。 要从时间轴中删除注释，请单击&#x200B;**[!UICONTROL 删除]**。

## 最佳实践和限制 {#tips-limitations}

* 如果没有[!DNL Dynamic Media]许可证，您只能使用处理配置文件处理MP4文件。
* 使用处理配置文件对MP4文件进行转码时，适用以下准则和限制：

   * Apple ProRes文件只能转码到最大分辨率1080p。
   * 如果源文件的比特率大于200 Mbps，则只能将代码转码到最大分辨率1080p。
   * 如果源帧速率>=60 fps ，则可以使用的源文件的最大大小为：

      * 400 MB用于4k转码。
      * 1080p转码为800 MB。
      * 720p转码为8 GB。

   * 可以转码为4k分辨率的最大文件大小为2.55 GB MP4文件，分辨率为4k，比特率为12 Mbps，速度为23 fps。

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

>[!MORELIKETHIS]
>
>* [Dynamic Media视频文档](/help/assets/dynamic-media/video.md)。
>* [了解有关处理配置文件的使用、类型和配置的更多信息](/help/assets/asset-microservices-configure-and-use.md)。
