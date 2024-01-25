---
title: 管理视频资源
description: 在中上传、预览、注释和发布视频资源 [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: fd1c3d1e524e5882ae04ca784b618ddba123bdd6
workflow-type: tm+mt
source-wordcount: '4975'
ht-degree: 6%

---

# 管理视频资源 {#manage-video-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=en) |
| AEM as a Cloud Service | 本文 |

视频格式是组织数字资产的重要组成部分。 [!DNL Adobe Experience Manager] 提供了一些成熟的产品和功能，用于在创建视频资产后管理其整个生命周期。

了解如何在中管理和编辑视频资产 [!DNL Adobe Experience Manager Assets]. 视频编码和转码（例如FFmpeg转码）可以使用处理配置文件和使用 [!DNL Dynamic Media] 集成。 不含 [!DNL Dynamic Media] 许可证， [!DNL Experience Manager] 为视频提供基本支持，例如使用FFmpeg进行转码、针对支持的文件格式提取预览缩略图，以及在用户界面中针对支持直接在浏览器中播放的格式进行预览。

## 上传和预览视频资产 {#upload-and-preview-video-assets}

您可以上传和预览受支持格式的视频资产，以 [!DNL Experience Manager Assets].
<!-- It generates previews for video assets with the extension MP4. -->

### 上传视频资产

要上传视频资产，请执行以下步骤：

1. 在数字资源文件夹或子文件夹中，导航到需要添加资源的位置。
1. 单击 **[!UICONTROL 创建]** 从工具栏中选择 **[!UICONTROL 文件]**. <br>或者，在用户界面上拖动文件。
了解有关 [上传资产](manage-digital-assets.md#uploading-assets) 在 [!DNL Experience Manager Assets].

<!-- 1. To preview a video in the card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. You can pause or play video in the card view only. The [!UICONTROL Play] and [!UICONTROL Pause] options are not available in the list view.
1. To preview the video in the asset details page, select **[!UICONTROL Edit]** on the card. The video plays in the native video player of the browser. You can play, pause, control the volume, and zoom the video to full screen. -->

### 预览视频资产

您可以在 [!DNL Assets] 用户界面。 要预览视频资源，请执行以下步骤：

1. 将支持格式的视频资产上传到 [!DNL Experience Manager Assets]. 了解关于 [支持的视频格式](file-format-support.md#video-formats). <br>上传后，将处理视频资产，并生成预览演绎版。
1. 单击资产，然后选择 ![详细信息选项](assets/do-not-localize/details_icon.svg) **[!UICONTROL 详细信息]**  从顶部工具栏中。 视频资产将在视频查看器中打开。
1. 单击 ![播放选项](assets/do-not-localize/play.png) 图标（位于视频缩略图上）。 <br>您可以播放、暂停、控制音量以及将视频缩放到全屏。

对于中的现有视频资产 [!DNL Experience Manager Assets]，您需要 **[!UICONTROL 重新处理]** 中的资产 [!DNL Experience Manager] 以启用视频预览功能。 了解如何 [重新处理数字资产](reprocessing.md) 在 [!DNL Experience Manager].

### 视频预览的限制

* 即使生成了演绎版，MXF文件也不会显示视频预览。
* WebM文件不会生成预览呈现版本，因为它们可以由Web浏览器本机播放。

## 发布视频资产 {#publish-video-assets}

发布后，您可以将视频资产作为URL包含在网页中，或直接嵌入这些资产。 有关详细信息，请参阅 [发布 [!DNL Dynamic Media] 资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## 将视频发布到YouTube {#publishing-videos-to-youtube}

您可以将在Experience Manager Assets中管理的视频资产直接发布到之前创建的YouTube渠道。

要将视频资源发布到YouTube，您需要在Experience Manager Assets中使用标记来标记视频资源。 将这些标记与YouTube渠道关联。 如果视频资产的标记与YouTube渠道的标记匹配，则视频将发布到YouTube。 只要使用关联的标记，发布到YouTube就会与正常发布视频同时发生。

YouTube自行编码。 因此，上传到Experience Manager的原始视频文件会发布到YouTube，而不是Dynamic Media的编码创建的任何视频演绎版。 虽然无需使用Dynamic Media处理视频，但预计可在播放时需要查看器预设时这样做。

当您绕过视频处理配置文件并直接发布到YouTube时，这仅仅意味着您在Experience Manager资源中的视频资源没有获取可查看的缩略图。 它还意味着未编码的视频不适用于任何Dynamic Media资源类型。

将视频资产发布到YouTube服务器需要完成以下任务，以确保通过YouTube进行安全可靠的服务器到服务器验证：

1. [配置Google云设置](#configuring-google-cloud-settings)
1. [创建YouTube渠道](#creating-a-youtube-channel)
1. [添加标记以进行发布](#adding-tags-for-publishing)
1. [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem)
1. [（可选）自动为您上传的视频设置默认YouTube属性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [将视频发布到YouTube渠道](#publishing-videos-to-your-youtube-channel)
1. [（可选）验证YouTube上发布的视频](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [将YouTube URL关联到您的Web应用程序](#linking-youtube-urls-to-your-web-application)

您还可以 [取消发布视频以从YouTube中删除它们](#unpublishing-videos-to-remove-them-from-youtube).

### 配置Google云设置 {#configuring-google-cloud-settings}

要发布到YouTube，您需要Google帐户。 如果您拥有GMAIL帐户，则表明您已经拥有Google帐户；如果您没有Google帐户，则可以轻松创建一个帐户。 您需要帐户，因为您需要凭据才能将视频资产发布到YouTube。 <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

用于Google Cloud的帐户和用于YouTube的Google帐户不需要相同。

Google会定期更改其用户界面。 因此，将视频发布到YouTube的步骤可能与以下文档记录的内容略有不同。 当您尝试检查视频是否已上传到YouTube时，此警告也适用。

>[!NOTE]
>
>在编写本报告时，以下步骤是准确的。 但是，Google会定期更新其云网页，恕不另行通知。 因此，某些配置选项在Google用户界面中的名称可能与步骤中使用的名称略有不同。

**要配置Google云设置，请执行以下操作：**

1. 创建一个Google帐户。

   如果您已经拥有Google帐户，则可以跳至下一步。

1. 转到 [https://cloud.google.com/](https://cloud.google.com/).
1. 在 **[!UICONTROL Google Cloud]** 页面，在右上角附近，选择 **[!UICONTROL 控制台]**.

   如有必要， **[!UICONTROL 登录]** 使用您的Google帐户凭据查看 **[!UICONTROL 控制台]** 选项。

1. 在 **[!UICONTROL 仪表板]** 页面，右侧 **[!UICONTROL Google Cloud平台]**，选择 **[!UICONTROL 项目]** 下拉列表以打开 **[!UICONTROL 选择项目]** 对话框。
1. 在 **[!UICONTROL 选择项目]** 对话框，选择 **[!UICONTROL 新建项目]**.
1. 在 **[!UICONTROL 新建项目]** 对话框，在 **[!UICONTROL 项目名称]** 字段中，键入新项目的名称。

   您的项目ID基于您的项目名称。 因此，请仔细选择项目名称；在创建项目后无法对其进行更改。 此外，稍后在Experience Manager中设置YouTube时，必须再次输入相同的项目ID。 所以，写下来。

1. 选择&#x200B;**[!UICONTROL 创建]**。

1. 执行以下任一操作：

   * 在项目的仪表板上，在 **[!UICONTROL 快速入门]** 卡片，选择 **[!UICONTROL 浏览和启用API]**.
   * 在项目的仪表板上，在 **[!UICONTROL API]** 卡片，选择 **[!UICONTROL 转到API概述]**.

1. 靠近中上部 **[!UICONTROL API和服务]** 页面，选择 **[!UICONTROL 启用API和服务]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. 在 **[!UICONTROL API库]** 页面，左侧，下 **[!UICONTROL 类别]**，选择 **[!UICONTROL YouTube]**. 在页面的右侧，选择 **[!UICONTROL YouTube]**.
1. 在 **[!UICONTROL YouTube]** 页面，选择 **[!UICONTROL YouTube数据API v3]**.
1. 在 **[!UICONTROL YouTube数据API v3]** 页面，选择 **[!UICONTROL 管理]**.

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. 要使用API，您需要凭据。 如有必要，在 **[!UICONTROL API和服务]** 页面，选择 **[!UICONTROL 凭据]**.
1. 在 **[!UICONTROL 凭据]** 页面，在顶部附近，选择 **[!UICONTROL 创建凭据]**，然后选择 **[!UICONTROL OAuth客户端ID]**.
1. 在 **[!UICONTROL 创建OAuth客户端ID]** 页面，在 **[!UICONTROL 应用程序类型]** 下拉列表，选择 **[!UICONTROL Web应用程序]**.

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. 执行下列操作之一：

   * 在 **[!UICONTROL 名称]** 字段中，为您的OAuth 2.0客户端输入唯一名称。
   * 使用Google已在中提供的默认名称 **[!UICONTROL 名称]** 字段。

1. 在 **[!UICONTROL 授权的JavaScript源]** 标题，选择 **[!UICONTROL 添加URI]**.

   ![6_5_google帐户 — apis-nameauthorizations](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. 在 **[!UICONTROL URI]** 文本字段，输入以下路径，用您自己的域和路径中的端口号替代，然后按 **[!UICONTROL 输入]** 要将路径添加到列表，请执行以下操作：

   `https://<servername.domain>:<port_number>`

   例如，`https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >上述URI路径示例是假设性的，仅用于解释。

1. 在 **[!UICONTROL 授权的重定向URI]** 标题，选择添加URI。
1. 在 **[!UICONTROL URI]** 文本字段，输入以下路径，用您自己的域和路径中的端口号替代，然后按 **[!UICONTROL 输入]** 要将路径添加到列表，请执行以下操作：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如，`https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >上述URI路径示例是假设性的，仅用于解释。

1. 接近底部 **[!UICONTROL 创建OAuth客户端ID]** 页面，选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 已创建OAuth客户端]** 对话框中，执行以下操作：

   * （可选）将值复制到 **[!UICONTROL 您的客户端ID]** 和 **[!UICONTROL 您的客户端密码]** 字段并保存。
   * 选择 **[!UICONTROL 下载JSON]**，然后保存JSON文件。

   稍后在Adobe Experience Manager中设置YouTube时，您需要此下载的JSON文件。

   ![6_5_google帐户 — apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. 在 **[!UICONTROL 已创建OAuth客户端]** 对话框，选择 **[!UICONTROL 确定]**.
1. 注销Google帐户。 现在创建一个YouTube渠道。

### 创建YouTube渠道 {#creating-a-youtube-channel}

将视频发布到YouTube要求您拥有一个或多个渠道。 如果您已创建YouTube渠道，则可以跳过此任务并转到 [添加标记以进行发布](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>确保您已在YouTube中设置一个或多个渠道 *早于* 您可以在Experience Manager的“YouTube设置”下添加渠道(请参阅 [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem) 下)。 如果无法设置渠道，则不会警告您不存在任何现有渠道。 但是，在添加频道时，Google验证仍会进行，但无法选择发送视频的频道。

**要创建YouTube渠道：**

1. 转到 [https://www.youtube.com](https://www.youtube.com/) 并使用您的Google帐户凭据登录。
1. 在YouTube页面的右上角，选择您的个人资料图片（也可以显示为实色圆圈中的字母），然后选择 **[!UICONTROL YouTube设置]** （圆齿轮图标）。
1. 在概述页面的其他功能标题下，选择 **[!UICONTROL 查看我的所有渠道或创建渠道]**.
1. 在渠道页面上，选择 **[!UICONTROL 创建新渠道]**.
1. 在“品牌帐户”页面的品牌帐户名称字段中，输入公司名称或您选择要将视频资产发布到的任何其他渠道名称，然后选择 **[!UICONTROL 创建]**.

   请记住您在此处输入的名称；在必须在Experience Manager中设置YouTube时，必须再次输入该名称。

1. （可选）如有必要，请添加更多渠道。

   现在，您可以添加标记以进行发布。

### 添加标记以进行发布 {#adding-tags-for-publishing}

要将视频发布到YouTube，Experience Manager会将标记与一个或多个YouTube渠道关联。 要添加标记以进行发布，请参阅 [管理标记](/help/sites-cloud/authoring/features/tags.md).

或者，如果您打算在Experience Manager中使用默认标记，则可以跳过此任务并转到 [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem).

>[!NOTE]
>
>配置Cloud Service后，无需进行其他配置即可在此时启用YouTube发布复制代理。 原因是保存Cloud Service配置时启用了它。

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### 在Experience Manager中设置YouTube {#setting-up-youtube-in-aem}

从Experience Manager6.4开始，引入了一种新的触屏用户界面方法，用于在Experience Manager中设置YouTube发布。 根据您所使用的Experience Manager的安装实例，执行以下操作之一：

* 要在6.4之前的Experience Manager中配置YouTube，请参阅 [在6.4之前的Experience Manager中设置YouTube](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* 要在Experience Manager6.4或更高版本中配置YouTube，请参阅 [在Experience Manager6.4及更高版本中设置YouTube](#setting-up-youtube-in-aem-and-later).

#### 在Experience Manager6.4及更高版本中设置YouTube {#setting-up-youtube-in-aem-and-later}

1. 确保以管理员身份登录到Dynamic Media实例。
1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中导航到 **[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL Cloud Service]** > **[!UICONTROL YouTube发布配置]**.
1. 选择 **[!UICONTROL 全局]** （请勿选择它）。

1. 在全局页面的右上角附近，选择 **[!UICONTROL 创建]**.
1. 在“创建 YouTube 配置”页面的“Google Cloud Platform 设置”下的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   在之前配置Google Cloud设置时指定了项目ID。
保持创建YouTube配置页面处于打开状态；稍后您将返回到此页面。

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用纯文本编辑器，打开您之前在任务中下载并保存的JSON文件 [配置Google云设置](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**.

   现在在Experience Manager中设置YouTube渠道。

1. 选择 **[!UICONTROL 添加渠道]**.
1. 在渠道名称字段中，输入您在任务中创建的渠道的名称 **[!UICONTROL 向YouTube添加一个或多个渠道]** 更早。

   如果需要，您可以选择添加描述。

1. 选择&#x200B;**[!UICONTROL 添加]**。
1. 将显示YouTube/Google验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID关联的Google用户名和密码，以及上面的JSON文本。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择渠道。 不要选择电子邮件地址；它不是渠道。
   * 在下一页，选择 **[!UICONTROL Accept]** 以允许对此渠道的访问。

1. 选择 **[!UICONTROL 允许]**.

   现在设置标记以进行发布。

1. **[!UICONTROL 设置标记以进行发布]**  — 在Cloud Service> YouTube页面上，选择铅笔图标以编辑要使用的标记列表。
1. 要在Experience Manager中显示可用标签列表，请选择下拉列表图标（上下倒置插入号）。
1. 要添加这些标记，请选择一个或多个标记。

   要删除已添加的标记，请选择该标记，然后选择 **[!UICONTROL X]**.

1. 添加完所需的标记后，选择 **[!UICONTROL 保存]**.

   现在，您可以将视频发布到YouTube渠道。

#### 在6.4之前的Experience Manager中设置YouTube {#setting-up-youtube-in-aem-before}

1. 确保以管理员身份登录到Dynamic Media实例。

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中导航到 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 部署]** > **[!UICONTROL Cloud Service]**.
1. 在第三方服务标题下方的YouTube下，选择 **[!UICONTROL 立即配置]**.
1. 在创建配置对话框中，在相应字段中输入标题（必填）和名称（可选）。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在“YouTube 帐户设置”对话框的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您在最初指定项目ID时 [已配置Google云设置](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) 更早。
保持YouTube帐户设置对话框处于打开状态；稍后您将返回到此对话框。

1. 使用纯文本编辑器，打开您之前在配置Google云设置任务中下载并保存的JSON文件。
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 选择 **[!UICONTROL 确定]**.

   现在在Experience Manager中设置YouTube渠道。

1. 右侧 **[!UICONTROL 可用渠道]**，选择 **+** （加号图标）。
1. 在“YouTube频道设置”对话框的“标题”字段中，输入您在之前向YouTube添加一个或多个频道任务中创建的频道 **[!UICONTROL 名称]** 。

   如果需要，您可以选择添加描述。

1. 选择 **[!UICONTROL 确定]**.
1. 将显示YouTube/Google验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID关联的Google用户名和密码，以及上面的JSON文本。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择渠道。 不要选择电子邮件地址；它不是渠道。
   * 在下一页，选择 **[!UICONTROL Accept]** 以允许对此渠道的访问。

1. 选择 **[!UICONTROL 允许]**.

   现在设置标记以进行发布。

1. **[!UICONTROL 设置标记以进行发布]**  — 在Cloud Service> YouTube页面上，选择铅笔图标以编辑要使用的标记列表。
1. 要在Experience Manager中显示可用标签列表，请选择下拉列表图标（上下倒置插入号）。
1. 要添加这些标记，请选择一个或多个标记。

   要删除已添加的标记，请选择该标记，然后选择 **X**.

1. 添加完所需的标记后，选择 **[!UICONTROL 确定]**.

   现在，您可以将视频发布到YouTube渠道。

### （可选）自动为您上传的视频设置默认YouTube属性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以选择在上传视频时自动设置YouTube属性。 在Experience Manager中创建元数据处理配置文件。

要创建元数据处理配置文件，您首先需要从&#x200B;**[!UICONTROL 字段标签]**、**[!UICONTROL 映射到属性]**&#x200B;和&#x200B;**[!UICONTROL 选择]**&#x200B;字段中复制值，所有这些字段均位于视频的元数据架构中。然后，您可以通过向处理配置文件添加这些值来构建您的YouTube视频元数据处理配置文件。

**要为上传的视频自动设置默认YouTube属性，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中导航到 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.
1. 选择 **[!UICONTROL 默认]**. （请勿在“default”左侧的选择框中添加复选标记。）
1. 在 **[!UICONTROL 默认]** 页面，选中左侧的框 **[!UICONTROL 视频]**，然后选择 **[!UICONTROL 编辑]**.
1. 在元数据架构编辑器页面上，选择 **[!UICONTROL 高级]** 选项卡。
1. 在YouTube发布标题下，选择 **[!UICONTROL YouTube类别]**.
1. 在页面的右侧，在 **[!UICONTROL 设置]** 选项卡，执行以下操作：

   * 在 **[!UICONTROL 映射到属性]** 文本字段，选择并复制值。
将复制的值粘贴到打开的文本编辑器中。 稍后在创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

   * 下 **[!UICONTROL 选项]**，选择并复制您要使用的默认值（例如“人员”和“博客”或“科学与技术”）。
将复制的值粘贴到打开的文本编辑器中。 稍后在创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

1. 在YouTube发布标题下，选择 **[!UICONTROL YouTube隐私]**.
1. 在页面的右侧，在 **[!UICONTROL 设置]** 选项卡，执行以下操作：

   * 在 **[!UICONTROL 映射到属性]** 文本字段，选择并复制值。
将复制的值粘贴到打开的文本编辑器中。 稍后在创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

   * 下 **[!UICONTROL 选项]**，选择并复制要使用的默认值。 请注意，“选择”成对分组为两个组。 该对中的底部字段是您要复制的默认值，例如public、unlisted或private。
将复制的值粘贴到打开的文本编辑器中。 稍后在创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

1. 在元数据架构编辑器页面的右上角附近，选择 **[!UICONTROL 取消]**.
1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 元数据配置文件]**.

1. 在元数据配置文件页面右上角附近，选择 **[!UICONTROL 创建]**.
1. 在添加元数据配置文件对话框中，在 **[!UICONTROL 配置文件标题]** 文本字段，输入名称 `YouTube Video` 然后选择 **[!UICONTROL 创建]**.
1. 在元数据配置文件编辑器页面上，选择 **[!UICONTROL 前进]** 选项卡。
1. 通过执行以下操作，将复制的YouTube发布值添加到配置文件中：

   * 在页面的右侧，选择 **[!UICONTROL 构建表单]** 选项卡。
   * （可选）拖动标记为 **[!UICONTROL 章节标题]** 左侧，并将其放入表单区域。
   * （可选）选择 **[!UICONTROL 字段标签]** 以选择组件。
   * （可选）在页面右侧的设置选项卡下，在字段标签文本字段中输入 `YouTube Publishing`.
   * 选择 **[!UICONTROL 构建表单]** 选项卡，然后拖动标记为的组件 **[!UICONTROL 多值文本]** 然后将其放在 **[!UICONTROL YouTube发布]** 您创建的标题。

   * 要选择组件，请选择 **[!UICONTROL 字段标签]**.
   * 在页面的右侧，在“设置”选项卡下方，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上各自的字段中。 将“选项”值粘贴到“默认值”字段中。

1. 通过执行以下操作，将复制的YouTube隐私值添加到配置文件中：

   * 在页面的右侧，选择 **[!UICONTROL 构建表单]** 选项卡。
   * （可选）拖动标记为 **[!UICONTROL 章节标题]** 左侧，并将其放入表单区域。
   * （可选）选择 **[!UICONTROL 字段标签]** 以选择组件。
   * （可选）在页面右侧的设置选项卡下，在字段标签文本字段中输入 `YouTube Privacy`.
   * 选择 **[!UICONTROL 构建表单]** 选项卡，然后拖动标记为的组件 **[!UICONTROL 多值文本]** 然后将其放在 **[!UICONTROL YouTube隐私]** 您创建的标题。

   * 要选择组件，请选择 **[!UICONTROL 字段标签]**.
   * 在页面的右侧，在“设置”选项卡下方，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上各自的字段中。 将“选项”值粘贴到“默认值”字段中。

1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**.
1. 将YouTube发布元数据配置文件应用到要上传视频的文件夹。 您必须同时设置元数据配置文件和视频配置文件。

   请参阅 [元数据配置文件](/help/assets/metadata-profiles.md) 和视 [频配置文件](/help/assets/dynamic-media/video-profiles.md)。

### 将视频发布到YouTube渠道 {#publishing-videos-to-your-youtube-channel}

现在，您将之前添加的标记关联到视频资产。 此过程可告知Experience Manager要发布到YouTube渠道的资产。

>[!NOTE]
>
>立即发布不会自动发布到YouTube。 设置 Dynamic Media 时，有两种发布选项可供选择：**[!UICONTROL 立即]**&#x200B;或&#x200B;**[!UICONTROL 激活时]**。
>
>**[!UICONTROL 立即发布]** 这意味着上传的资产（与IPS同步后）会自动发布到交付系统。 虽然这对Dynamic Media是这样，但对YouTube并非如此。 要发布到YouTube，必须通过Experience Manager创作方式发布。

>[!NOTE]
>
要从YouTube发布内容，Experience Manager使用 **[!UICONTROL 发布到YouTube]** 工作流，用于监视进度和查看任何故障信息。
>
请参阅 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).
>
有关更详细的进度信息，您可以在复制下监视YouTube日志。 但是，请注意，此类监视需要管理员访问权限。

**要将视频发布到YouTube渠道，请执行以下操作：**

1. 在Experience Manager中，导航到要发布到YouTube渠道的视频资源。
1. 选择视频资产（自适应视频集）。
1. 在工具栏上，选择 **[!UICONTROL 属性]**.
1. 在基本选项卡的元数据标题下，选择 **[!UICONTROL 打开选择对话框]** 标记字段的右侧。
1. 在“选择标记”页面上，导航到要使用的标记，然后选择一个或多个标记。

   请记住，标记必须与YouTube渠道关联。

1. 在页面的右上角，选择 **[!UICONTROL 选择]**.
1. 在视频属性页面的右上角，选择 **[!UICONTROL 保存并关闭]**.
1. 在工具栏上，选择 **[!UICONTROL 快速发布]**.

   另请参阅 [将发布管理与Experience Manager Sites结合使用](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   您可以选择在YouTube渠道中验证已发布的视频。

### （可选）验证YouTube上发布的视频 {#optional-verifying-the-published-video-on-youtube}

您可以选择监控YouTube发布（或取消发布）的进度。

请参阅 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).

发布时间会因多种因素而有很大差异，这些因素包括主源视频的格式、文件大小和上传流量。 发布过程可能需要几分钟到几小时的时间。 此外，更高分辨率格式的呈现速度要慢得多。 例如，720p和1080p需要比480p更长的时间才能显示。

8小时后，如果您仍然看到一条状态消息，显示 **[!UICONTROL 已上传（正在处理，请稍候）]**，请尝试从您的站点中删除视频并重新上传。

### 将YouTube URL关联到您的Web应用程序 {#linking-youtube-urls-to-your-web-application}

您可以获取Dynamic Media在发布视频后生成的YouTube URL字符串。 复制YouTube URL时，它会登陆剪贴板，以便您可以根据需要将其粘贴到网站或应用程序中的页面。

>[!NOTE]
>
在将视频资产发布到YouTube之前，无法复制YouTube URL。

要将YouTube URL关联到您的Web应用程序，请执行以下操作：

1. 导航至 *YouTube已发布* 要复制其URL的视频资源，然后选择它。

   请记住，YouTube URL仅可供复制 *之后* 您拥有 *已发布* 将视频资源移至YouTube。

1. 在工具栏上，选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 高级]** 选项卡。
1. 在YouTube发布标题下的YouTube URL列表中，选择URL文本，并将其复制到Web浏览器，以预览资产或添加到Web内容页面。

### 取消发布视频，以便从YouTube中删除它们 {#unpublishing-videos-to-remove-them-from-youtube}

在Experience Manager中取消发布视频资源时，该视频将从YouTube中删除。

>[!CAUTION]
>
如果直接从YouTube中删除视频，则Experience Manager不会察觉，并继续按照将视频发布到YouTube的方式运行。 始终通过Experience Manager从YouTube中取消发布视频资源。

>[!NOTE]
>
要从YouTube中删除内容，Experience Manager使用 **[!UICONTROL 从YouTube取消发布]** 工作流，用于监视进度和查看任何故障信息。
>
请参阅 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).

**要取消发布视频以从YouTube中删除它们，请执行以下操作：**

1. 导航到要从YouTube渠道取消发布的视频资源。
1. 在资源选择模式下，选择一个或多个已发布的视频资源。
1. 在工具栏上，选择 **[!UICONTROL 管理发布]**. 如有必要，请选择三个圆点图标(`. . .`)，以查看 **[!UICONTROL 管理发布]**.
1. 在管理发布页面上，选择 **[!UICONTROL 取消发布]**.
1. 在页面的右上角，选择 **[!UICONTROL 下一个]**.
1. 在页面的右上角，选择 **[!UICONTROL 取消发布]**.

## 监控视频编码和YouTube发布进度 {#monitoring-video-encoding-and-youtube-publishing-progress}

在将新视频上传到应用了视频编码的文件夹时，或者将视频发布到YouTube时，监控视频编码/Youtube发布的进展情况（或失败）。 实际YouTube发布进度只能通过日志提供。 但是，无论成功还是失败，它都将以以下过程中描述的其他方式列出。 此外，当YouTube发布工作流或视频编码完成或中断时，您会收到电子邮件通知。

### 监测进度 {#monitoring-progress}

您可以监控进度，包括失败的编码/YouTube发布。

1. 在assets文件夹中查看视频编码进度：

   * 在卡片视图中，视频编码进度按百分比显示在资源上。 如果出现错误，资产上也会显示此信息。

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * 在列表视图中，视频编码进度显示在 **[!UICONTROL 处理状态]** 列。 如果出现错误，则该列中将显示此消息。

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   默认情况下，此列不显示。要启用该列，请选择 **[!UICONTROL 查看设置]** 从“视图”下拉菜单中，添加 **[!UICONTROL 处理状态]** 列并选择 **[!UICONTROL 更新]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. 在资源详细信息中查看进度。 选择资产后，打开下拉菜单并选择 **[!UICONTROL 时间线]**. 要将其缩小到编码或YouTube发布等工作流活动，请选择 **[!UICONTROL 工作流]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   任何工作流信息（如编码）都会显示在时间轴中。 对于YouTube发布，工作流时间轴还包括YouTube渠道的名称和YouTube视频URL。 此外，发布完成后，您会在工作流时间轴中看到任何失败通知。

   >[!NOTE]
   >
   由于上的多个工作流配置，最终记录失败/错误会花费较长时间。 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 从 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   >
   * Apache Sling作业队列配置
   * AdobeGranite工作流外部进程作业处理程序
   * Granite工作流超时队列
   >
   您可以调整 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 属性。

1. 有关进行中的工作流，请参阅“工具”>“工作流” **[!UICONTROL >“实例”中提供的“工作流实例]** ” **[!UICONTROL (Workflow]** ) **[!UICONTROL >“]**&#x200B;实例”。

   >[!NOTE]
   >
   您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   选择实例，然后选择 **[!UICONTROL 打开历史记录]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   您还可以从“工作流实例”区域暂停、终止或重命名工作流。 请参阅 [管理工作流](/help/sites-cloud/authoring/workflows/overview.md) 以了解更多信息。

1. 有关失败的作业，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 失败]**&#x200B;中显示的“工作流失败”。**[!UICONTROL 工作流失败]**&#x200B;列出所有失败的工作流活动。

   >[!NOTE]
   >
   您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   >
   由于上的多个工作流配置，最终记录错误消息会花费较长时间 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 从 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   >
   * Apache Sling作业队列配置
   * AdobeGranite工作流外部进程作业处理程序
   * Granite工作流超时队列
   >
   您可以调整 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 属性。

1. 有关已完成的工作流，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 存档]**&#x200B;中的可用工作流存档。**[!UICONTROL 工作流存档]**&#x200B;列出了所有已完成的工作流活动。

   >[!NOTE]
   >
   您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. 您会收到有关已中止或失败的工作流作业的电子邮件通知。 这些电子邮件通知可由管理员配置。 请参阅 [配置电子邮件通知](#configuring-e-mail-notifications).

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

[!DNL Experience Manager] as a [!DNL Cloud Service] 允许您使用处理配置文件对MP4视频文件进行基本转码。 利用功能，您不仅可以上传，还可以预览和缩放MP4视频文件。

![在中创建视频转码的处理配置文件 [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*图：中用于视频转码的处理配置文件 [!DNL Experience Manager].*

如果只提供宽度或高度，并将其他字段留空，则格式副本将保持长宽比。 H.264视频编解码器可用于转码。

要使用处理配置文件处理资产，请将配置文件添加到文件夹。 请参阅 [使用处理配置文件处理资产](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## 为视频资源作批注 {#annotate-video-assets}

您可以向视频资产添加批注。 在对视频添加注释时，播放器会暂停以允许您在帧上添加注释。 有关详细信息，请参阅 [管理视频资产](manage-video-assets.md).

>[!NOTE]
>
视频资产注释尚不支持MXF视频格式。

1. 从 [!DNL Assets] 控制台，选择 **[!UICONTROL 编辑]** ，以显示资产详细信息页面。
1. 要播放视频，请单击 **[!UICONTROL 预览]**.
1. 要在视频中添加批注，请单击 **[!UICONTROL 批注]**. 在视频中的特定时间（帧）添加注释。 在注释时，可以在画布上绘制并在绘图中包括注释。 评论将自动保存。 要退出注释向导，请单击 **[!UICONTROL 关闭]**.
1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。
1. 要在时间轴中查看注释，请单击注释。 要从时间轴中删除注释，请单击 **[!UICONTROL 删除]**.

## 最佳实践和限制 {#tips-limitations}

* 不含 [!DNL Dynamic Media] 许可证，您只能使用处理配置文件来处理MP4文件。
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

>[!MORELIKETHIS]
>
* [Dynamic Media视频文档](/help/assets/dynamic-media/video.md).
* [了解有关处理配置文件的使用、类型和配置的更多信息](/help/assets/asset-microservices-configure-and-use.md).
