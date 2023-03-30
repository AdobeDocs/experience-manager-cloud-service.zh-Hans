---
title: 管理视频资源
description: 在 [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 0ba6ce129322df9ad108822e86e5acfdbf99e613
workflow-type: tm+mt
source-wordcount: '4886'
ht-degree: 5%

---

# 管理视频资源 {#manage-video-assets}

视频格式是组织中数字资产的关键部分。 [!DNL Adobe Experience Manager] 提供了成熟的产品和功能，用于在视频资产创建后管理其整个生命周期。

了解如何在 [!DNL Adobe Experience Manager Assets]. 使用处理配置文件和使用 [!DNL Dynamic Media] 集成。 没有 [!DNL Dynamic Media] 许可证， [!DNL Experience Manager] 为视频提供基本支持，例如使用FFmpeg转码、提取支持的文件格式的预览缩略图，以及在用户界面中预览直接支持在浏览器中播放的格式。

## 上传和预览视频资产 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 为扩展名为MP4的视频资产生成预览。 您可以在 [!DNL Assets] 用户界面。

1. 在数字资产文件夹或子文件夹中，导航到要添加数字资产的位置。
1. 要上传资产，请单击 **[!UICONTROL 创建]** 从工具栏中选择 **[!UICONTROL 文件]**. 或者，在用户界面上拖动文件。 请参阅 [上传资产](manage-digital-assets.md#uploading-assets) 以了解详细信息。
1. 要在卡片视图中预览视频，请单击 **[!UICONTROL 播放]** ![播放选项](assets/do-not-localize/play.png) 选项。 您只能在卡片视图中暂停或播放视频。 的 [!UICONTROL 播放] 和 [!UICONTROL 暂停] 选项在列表视图中不可用。
1. 要在资产详细信息页面中预览视频，请选择 **[!UICONTROL 编辑]** 在卡上。 视频在浏览器的本机视频播放器中播放。 您可以播放、暂停、控制音量，以及将视频放大到全屏。

## 发布视频资产 {#publish-video-assets}

发布后，您可以将视频资产作为URL包含在网页中，或直接嵌入资产。 有关详细信息，请参阅 [发布 [!DNL Dynamic Media] 资产](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## 将视频发布到YouTube {#publishing-videos-to-youtube}

您可以将Experience Manager Assets中管理的视频资产直接发布到您之前创建的YouTube渠道。

要将视频资产发布到YouTube，您需要在Experience Manager Assets中为视频资产添加标记，并添加标记。 将这些标记与YouTube渠道相关联。 如果视频资产的标记与YouTube渠道的标记匹配，则该视频会发布到YouTube。 只要使用关联的标记，发布到YouTube时，也会与视频的正常发布一起发生。

YouTube自行编码。 因此，上传到Experience Manager的原始视频文件会发布到YouTube，而不是Dynamic Media编码创建的任何视频演绎版。 虽然使用Dynamic Media无需处理视频，但在播放需要查看器预设时，应该会这样做。

绕过视频处理配置文件并直接发布到YouTube时，这仅意味着Experience Manager资产中的视频资产没有可查看的缩略图。 这还意味着未编码的视频不适用于任何Dynamic Media资产类型。

将视频资产发布到YouTube服务器涉及完成以下任务，以确保通过YouTube进行安全的服务器到服务器验证：

1. [配置Google Cloud设置](#configuring-google-cloud-settings)
1. [创建YouTube渠道](#creating-a-youtube-channel)
1. [添加标记以进行发布](#adding-tags-for-publishing)
1. [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem)
1. [（可选）自动设置已上传视频的默认YouTube属性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [将视频发布到YouTube渠道](#publishing-videos-to-your-youtube-channel)
1. [（可选）验证已发布到YouTube上的视频](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [将YouTube URL关联到您的Web应用程序](#linking-youtube-urls-to-your-web-application)

您还可以 [取消发布视频以将其从YouTube中删除](#unpublishing-videos-to-remove-them-from-youtube).

### 配置Google Cloud设置 {#configuring-google-cloud-settings}

要发布到YouTube，您需要Google帐户。 如果你有Gmail账户，那么你已经有Google账户；如果您没有Google帐户，则可以轻松创建一个帐户。 您需要该帐户，因为您需要凭据才能将视频资产发布到YouTube。 <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

与Google Cloud一起使用的帐户和用于YouTube的Google帐户不必相同。

Google会定期更改其用户界面。 因此，将视频发布到YouTube的步骤可能与下面介绍的步骤略有不同。 当您尝试检查视频是否上传到YouTube时，此注意事项也适用。

>[!NOTE]
>
>编写时，以下步骤是准确的。 但是，Google会定期更新其云网页，恕不另行通知。 因此，某些配置选项在Google用户界面中的名称可能与步骤中使用的名称略有不同。

**要配置Google Cloud设置，请执行以下操作：**

1. 创建Google帐户。
   [https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp](https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp)

   如果您已经拥有Google帐户，则可以跳到下一步。

1. 转到 [https://cloud.google.com/](https://cloud.google.com/).
1. 在 **[!UICONTROL Google Cloud]** 页面的右上角附近，选择 **[!UICONTROL 控制台]**.

   如有必要， **[!UICONTROL 登录]** 使用您的Google帐户凭据查看 **[!UICONTROL 控制台]** 选项。

1. 在 **[!UICONTROL 功能板]** 页面右侧 **[!UICONTROL Google Cloud平台]**，选择 **[!UICONTROL 项目]** 用于打开 **[!UICONTROL 选择项目]** 对话框。
1. 在 **[!UICONTROL 选择项目]** 对话框，选择 **[!UICONTROL 新建项目]**.
1. 在 **[!UICONTROL 新建项目]** 对话框中 **[!UICONTROL 项目名称]** 字段中，键入新项目的名称。

   您的项目ID基于您的项目名称。 因此，请仔细选择项目名称；创建后无法更改。 此外，当您稍后在Experience Manager中设置YouTube时，必须再次输入相同的项目ID。 所以，把它写下来。

1. 选择&#x200B;**[!UICONTROL 创建]**。

1. 执行以下任一操作：

   * 在项目的功能板中， **[!UICONTROL 快速入门]** 卡片，选择 **[!UICONTROL 探索并启用API]**.
   * 在项目的功能板中， **[!UICONTROL API]** 卡片，选择 **[!UICONTROL 转到API概述]**.

1. 在 **[!UICONTROL API和服务]** 页面，选择 **[!UICONTROL 启用API和服务]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. 在 **[!UICONTROL API库]** 页面的左侧，下 **[!UICONTROL 类别]**，选择 **[!UICONTROL YouTube]**. 在页面右侧，选择 **[!UICONTROL YouTube]**.
1. 在 **[!UICONTROL YouTube]** 页面，选择 **[!UICONTROL YouTube Data API v3]**.
1. 在 **[!UICONTROL YouTube Data API v3]** 页面，选择 **[!UICONTROL 管理]**.

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. 要使用API，您需要凭据。 如有必要，请在 **[!UICONTROL API和服务]** 页面，选择 **[!UICONTROL 凭据]**.
1. 在 **[!UICONTROL 凭据]** 页面，在顶部附近，选择 **[!UICONTROL 创建凭据]**，然后选择 **[!UICONTROL OAuth客户端ID]**.
1. 在 **[!UICONTROL 创建OAuth客户端ID]** 页面，在 **[!UICONTROL 应用程序类型]** 下拉列表中，选择 **[!UICONTROL Web应用程序]**.

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. 执行下列操作之一：

   * 在 **[!UICONTROL 名称]** 字段中，输入OAuth 2.0客户端的唯一名称。
   * 使用Google在 **[!UICONTROL 名称]** 字段。

1. 在 **[!UICONTROL 授权的JavaScript源]** 标题，选择 **[!UICONTROL 添加URI]**.

   ![6_5_googleaccount-apis-nameauthorizations](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. 在 **[!UICONTROL URI]** 文本字段，输入以下路径，在路径中替换您自己的域和端口号，然后按 **[!UICONTROL 输入]** 要添加列表路径，请执行以下操作：

   `https://<servername.domain>:<port_number>`

   例如，`https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >上面的URI路径示例是假设的，仅供说明。

1. 在 **[!UICONTROL 授权的重定向URI]** 标题中，选择“添加URI”。
1. 在 **[!UICONTROL URI]** 文本字段，输入以下路径，在路径中替换您自己的域和端口号，然后按 **[!UICONTROL 输入]** 要添加列表路径，请执行以下操作：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如，`https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >上面的URI路径示例是假设的，仅供说明。

1. 在 **[!UICONTROL 创建OAuth客户端ID]** 页面，选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 已创建OAuth客户端]** 对话框中，执行以下操作：

   * （可选）复制 **[!UICONTROL 您的客户ID]** 和 **[!UICONTROL 您的客户端密钥]** 字段，然后保存。
   * 选择 **[!UICONTROL 下载JSON]**，然后保存JSON文件。

   稍后在Adobe Experience Manager中设置YouTube时，您需要此下载的JSON文件。

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. 在 **[!UICONTROL 已创建OAuth客户端]** 对话框，选择 **[!UICONTROL 确定]**.
1. 从Google帐户注销。 现在，创建YouTube渠道。

### 创建YouTube渠道 {#creating-a-youtube-channel}

将视频发布到YouTube要求您拥有一个或多个渠道。 如果已创建YouTube渠道，则可以跳过此任务并转到 [添加标记以进行发布](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>确保您已在YouTube中设置一个或多个渠道 *之前* 您可以在的YouTube设置下添加Experience Manager(请参阅 [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem) )。 如果您未能设置渠道，则系统不会警告您任何现有渠道。 但是，在添加渠道时仍会进行Google验证，但是没有选项可选择发送视频的渠道。

**要创建YouTube渠道，请执行以下操作：**

1. 转到 [https://www.youtube.com](https://www.youtube.com/) 并使用您的Google帐户凭据登录。
1. 在YouTube页面的右上角，选择您的配置文件图片（该图片也可以显示为彩色圆圈中的字母），然后选择 **[!UICONTROL YouTube设置]** （圆齿轮图标）。
1. 在概述页面的其他功能标题下，选择 **[!UICONTROL 查看我的所有渠道或创建渠道]**.
1. 在渠道页面上，选择 **[!UICONTROL 创建新渠道]**.
1. 在品牌帐户页面的品牌帐户名称字段中，输入公司名称或您选择的要在其中发布视频资产的任何其他渠道名称，然后选择 **[!UICONTROL 创建]**.

   请记住您在此处输入的名称；必须在Experience Manager中设置YouTube时，必须再次输入该参数。

1. （可选）根据需要，添加更多渠道。

   现在，您可以添加标记以进行发布。

### 添加标记以进行发布 {#adding-tags-for-publishing}

要将视频发布到YouTube,Experience Manager会将标记关联到一个或多个YouTube渠道。 要添加用于发布的标记，请参阅 [管理标记](/help/sites-cloud/authoring/features/tags.md).

或者，如果您打算在Experience Manager中使用默认标记，则可以跳过此任务并转到 [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem).

>[!NOTE]
>
>配置Cloud Service后，此时无需其他配置即可启用YouTube发布复制代理。 原因是在保存Cloud Service配置时启用了该设置。

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### 在Experience Manager中设置YouTube {#setting-up-youtube-in-aem}

从Experience Manager6.4开始，引入了新的触屏用户界面方法，以在Experience Manager中设置YouTube发布。 根据您所使用的Experience Manager的已安装实例，执行以下操作之一：

* 要在6.4之前的Experience Manager中配置YouTube，请参阅 [在6.4之前的Experience Manager中设置YouTube](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* 要在Experience Manager6.4或更高版本中配置YouTube，请参阅 [在Experience Manager6.4及更高版本中设置YouTube](#setting-up-youtube-in-aem-and-later).

#### 在Experience Manager6.4及更高版本中设置YouTube {#setting-up-youtube-in-aem-and-later}

1. 请确保以管理员身份登录Dynamic Media实例。
1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，导航到 **[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube发布配置]**.
1. 选择 **[!UICONTROL 全球]** （请勿选择它）。

1. 在全局页面的右上角附近，选择 **[!UICONTROL 创建]**.
1. 在“创建 YouTube 配置”页面的“Google Cloud Platform 设置”下的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您在之前最初配置Google Cloud设置时指定了项目ID。
保持打开创建YouTube配置页面；你马上就会重新开始。

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用纯文本编辑器，打开您之前在任务中下载并保存的JSON文件 [配置Google Cloud设置](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**.

   现在，在YouTube中设置Experience Manager。

1. 选择 **[!UICONTROL 添加渠道]**.
1. 在渠道名称字段中，输入您在任务中创建的渠道名称 **[!UICONTROL 向YouTube添加一个或多个渠道]** 早期。

   您可以根据需要选择添加描述。

1. 选择 **[!UICONTROL 添加]**.
1. YouTube/Google验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID和上述JSON文本关联的Google用户名和密码。
   * 根据您的帐户中有多少个渠道，您会看到两个或更多项目。 选择渠道。 不要选择电子邮件地址；它不是频道。
   * 在下一页，选择 **[!UICONTROL 接受]** 以允许访问此渠道。

1. 选择 **[!UICONTROL 允许]**.

   现在，设置用于发布的标记。

1. **[!UICONTROL 设置用于发布的标记]**  — 在“Cloud Services”>“YouTube”页面上，选择铅笔图标以编辑要使用的标记列表。
1. 要在Experience Manager中显示可用标记列表，请选择下拉列表图标（倒置尖角）。
1. 要添加标记，请选择一个或多个标记。

   要删除已添加的标记，请选择该标记，然后选择 **[!UICONTROL X]**.

1. 添加完所需的标记后，选择 **[!UICONTROL 保存]**.

   现在，您将视频发布到YouTube渠道。

#### 在6.4之前的Experience Manager中设置YouTube {#setting-up-youtube-in-aem-before}

1. 请确保以管理员身份登录Dynamic Media实例。

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，导航到 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在“第三方服务”标题下的YouTube下，选择 **[!UICONTROL 立即配置]**.
1. 在“创建配置”对话框的相应字段中输入标题（必填）和名称（可选）。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在“YouTube 帐户设置”对话框的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您最初在 [配置的Google Cloud设置](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) 早期。
保持打开YouTube帐户设置对话框；你马上就会重新开始。

1. 使用纯文本编辑器，打开您之前在配置Google Cloud设置任务中下载并保存的JSON文件。
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 选择 **[!UICONTROL 确定]**.

   现在，在YouTube中设置Experience Manager。

1. 至 **[!UICONTROL 可用渠道]**，选择 **+** （加号图标）。
1. 在“YouTube频道设置”对话框的“标题”字段中，输入您在之前向YouTube添加一个或多个频道任务中创建的频道 **[!UICONTROL 名称]** 。

   您可以根据需要选择添加描述。

1. 选择 **[!UICONTROL 确定]**.
1. YouTube/Google验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID和上述JSON文本关联的Google用户名和密码。
   * 根据您的帐户中有多少个渠道，您会看到两个或更多项目。 选择渠道。 不要选择电子邮件地址；它不是频道。
   * 在下一页，选择 **[!UICONTROL 接受]** 以允许访问此渠道。

1. 选择 **[!UICONTROL 允许]**.

   现在，设置用于发布的标记。

1. **[!UICONTROL 设置用于发布的标记]**  — 在“Cloud Services”>“YouTube”页面上，选择铅笔图标以编辑要使用的标记列表。
1. 要在Experience Manager中显示可用标记列表，请选择下拉列表图标（倒置尖角）。
1. 要添加标记，请选择一个或多个标记。

   要删除已添加的标记，请选择该标记，然后选择 **X**.

1. 添加完所需的标记后，选择 **[!UICONTROL 确定]**.

   现在，您将视频发布到YouTube渠道。

### （可选）自动设置已上传视频的默认YouTube属性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以选择在上传视频时自动设置YouTube属性。 在Experience Manager中创建元数据处理配置文件。

要创建元数据处理配置文件，您首先需要从&#x200B;**[!UICONTROL 字段标签]**、**[!UICONTROL 映射到属性]**&#x200B;和&#x200B;**[!UICONTROL 选择]**&#x200B;字段中复制值，所有这些字段均位于视频的元数据架构中。然后，您可以通过将这些值添加到YouTube视频元数据处理配置文件来构建该配置文件。

**要自动设置已上传视频的默认YouTube属性，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，导航到 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.
1. 选择 **[!UICONTROL 默认]**. （请勿在“默认”左侧的选择框中添加复选标记。）
1. 在 **[!UICONTROL 默认]** 页面左侧的复选框 **[!UICONTROL 视频]**，然后选择 **[!UICONTROL 编辑]**.
1. 在元数据架构编辑器页面上，选择 **[!UICONTROL 高级]** 选项卡。
1. 在YouTube发布标题下，选择 **[!UICONTROL YouTube类别]**.
1. 在页面右侧的 **[!UICONTROL 设置]** 选项卡，请执行以下操作：

   * 在 **[!UICONTROL 映射到属性]** 文本字段中，选择并复制值。
将复制的值粘贴到打开文本编辑器中。 您稍后在创建元数据处理配置文件时将需要此值。 保持文本编辑器处于打开状态。

   * 在 **[!UICONTROL 选择]**，选择并复制您要使用的默认值（如“人员和博客”或“科学与技术”）。
将复制的值粘贴到打开文本编辑器中。 您稍后在创建元数据处理配置文件时将需要此值。 保持文本编辑器处于打开状态。

1. 在YouTube发布标题下，选择 **[!UICONTROL YouTube Privacy]**.
1. 在页面右侧的 **[!UICONTROL 设置]** 选项卡，请执行以下操作：

   * 在 **[!UICONTROL 映射到属性]** 文本字段中，选择并复制值。
将复制的值粘贴到打开文本编辑器中。 您稍后在创建元数据处理配置文件时将需要此值。 保持文本编辑器处于打开状态。

   * 在 **[!UICONTROL 选择]**，选择并复制您要使用的默认值。 请注意，选项分为两对。 对中的底部字段是要复制的默认值，如公共、未列出或私有。
将复制的值粘贴到打开文本编辑器中。 您稍后在创建元数据处理配置文件时将需要此值。 保持文本编辑器处于打开状态。

1. 在元数据架构编辑器页面的右上角附近，选择 **[!UICONTROL 取消]**.
1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中，选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 元数据配置文件]**.

1. 在元数据配置文件页面的右上角附近，选择 **[!UICONTROL 创建]**.
1. 在添加元数据配置文件对话框的 **[!UICONTROL 用户档案标题]** 文本字段，输入名称 `YouTube Video` 然后选择 **[!UICONTROL 创建]**.
1. 在元数据配置文件编辑器页面上，选择 **[!UICONTROL 高级]** 选项卡。
1. 通过执行以下操作，将复制的YouTube Publishing值添加到配置文件：

   * 在页面的右侧，选择 **[!UICONTROL 构建表单]** 选项卡。
   * （可选）拖动已标记为 **[!UICONTROL 节标题]** 并将其放入表单区域。
   * （可选）选择 **[!UICONTROL 字段标签]** 来选择组件。
   * （可选）在页面右侧的设置选项卡的字段标签文本字段中，输入 `YouTube Publishing`.
   * 选择 **[!UICONTROL 构建表单]** 选项卡，然后拖动标有的组件 **[!UICONTROL 多值文本]** 然后把它放下 **[!UICONTROL YouTube发布]** 标题。

   * 要选择组件，请选择 **[!UICONTROL 字段标签]**.
   * 在页面右侧的设置选项卡下，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单中的相应字段中。 将选项值粘贴到默认值字段中。

1. 通过执行以下操作，将复制的YouTube隐私值添加到配置文件：

   * 在页面的右侧，选择 **[!UICONTROL 构建表单]** 选项卡。
   * （可选）拖动已标记为 **[!UICONTROL 节标题]** 并将其放入表单区域。
   * （可选）选择 **[!UICONTROL 字段标签]** 来选择组件。
   * （可选）在页面右侧的设置选项卡的字段标签文本字段中，输入 `YouTube Privacy`.
   * 选择 **[!UICONTROL 构建表单]** 选项卡，然后拖动标有的组件 **[!UICONTROL 多值文本]** 然后把它放下 **[!UICONTROL YouTube Privacy]** 标题。

   * 要选择组件，请选择 **[!UICONTROL 字段标签]**.
   * 在页面右侧的设置选项卡下，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单中的相应字段中。 将选项值粘贴到默认值字段中。

1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**.
1. 将YouTube发布元数据配置文件应用到您要上传视频的文件夹。 您必须同时设置元数据配置文件和视频配置文件。

   请参阅 [元数据配置文件](/help/assets/metadata-profiles.md) 和视 [频配置文件](/help/assets/dynamic-media/video-profiles.md)。

### 将视频发布到YouTube渠道 {#publishing-videos-to-your-youtube-channel}

现在，您可以将之前添加的标记与视频资产相关联。 此过程可让Experience Manager知道要将哪些资产发布到您的YouTube渠道。

>[!NOTE]
>
>立即发布不会自动发布到YouTube。 设置 Dynamic Media 时，有两种发布选项可供选择：**[!UICONTROL 立即]**&#x200B;或&#x200B;**[!UICONTROL 激活时]**。
>
>**[!UICONTROL 立即发布]** 表示上传的资产在与IPS同步后会自动发布到交付系统。 虽然Dynamic Media是如此，但YouTube并非如此。 要发布到YouTube，您必须通过Experience Manager作者方式发布。

>[!NOTE]
要从YouTube发布内容，Experience Manager会使用 **[!UICONTROL 发布到YouTube]** 工作流，可让您监视进度并查看任何故障信息。
请参阅 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).
有关更详细的进度信息，您可以在复制下监视YouTube日志。 但是，请注意，此类监控需要管理员访问权限。

**要将视频发布到您的YouTube渠道，请执行以下操作：**

1. 在Experience Manager中，导航到要发布到YouTube渠道的视频资产。
1. 选择视频资产（自适应视频集）。
1. 在工具栏中，选择 **[!UICONTROL 属性]**.
1. 在基本选项卡的元数据标题下，选择 **[!UICONTROL 打开选择对话框]** 标记字段的右侧。
1. 在“选择标记”页面上，导航到要使用的标记，然后选择一个或多个标记。

   请记住，标记必须与YouTube渠道关联。

1. 在页面的右上角，选择 **[!UICONTROL 选择]**.
1. 在视频属性页面的右上角，选择 **[!UICONTROL 保存并关闭]**.
1. 在工具栏中，选择 **[!UICONTROL 快速发布]**.

   另请参阅 [将发布管理与Experience Manager Sites结合使用](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   您可以选择验证已在YouTube渠道上发布的视频。

### （可选）验证已发布到YouTube上的视频 {#optional-verifying-the-published-video-on-youtube}

您可以选择监控YouTube发布（或取消发布）的进度。

请参阅 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).

发布时间可能会因多种因素而有很大不同，这些因素包括主源视频的格式、文件大小和上传流量。 发布过程可能需要几分钟到几小时不等的时间。 此外，分辨率更高的格式呈现速度要慢得多。 例如，720p和1080p的显示时间比480p要长。

八小时后，如果您仍看到一条状态消息，其中显示 **[!UICONTROL 已上传（正在处理，请稍候）]**，请尝试从您的网站中删除视频，然后重新上传该视频。

### 将YouTube URL关联到您的Web应用程序 {#linking-youtube-urls-to-your-web-application}

您可以获取由Dynamic Media在发布视频后生成的YouTube URL字符串。 复制YouTube URL时，它会登陆到剪贴板，以便您可以根据需要将其粘贴到网站或应用程序中的页面。

>[!NOTE]
在将视频资产发布到YouTube之前，无法复制YouTube URL。

要将YouTube URL关联到您的Web应用程序，请执行以下操作：

1. 导航到 *YouTube发布* 要复制其URL的视频资产，然后将其选中。

   请记住，YouTube URL只能复制 *after* 您首先 *发布* 视频资产到YouTube。

1. 在工具栏中，选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 高级]** 选项卡。
1. 在YouTube发布标题的YouTube URL列表下，选择URL文本，并将其复制到Web浏览器，以预览资产或将其添加到您的Web内容页面。

### 取消发布视频，以便从YouTube中删除它们 {#unpublishing-videos-to-remove-them-from-youtube}

在Experience Manager中取消发布视频资产时，该视频将从YouTube中删除。

>[!CAUTION]
如果您直接从YouTube中删除视频，则Experience Manager不知道该视频，并会继续其行为，如同该视频仍然发布到YouTube一样。 始终通过Experience Manager方式从YouTube取消发布视频资产。

>[!NOTE]
要从YouTube中删除内容，Experience Manager会使用 **[!UICONTROL 从YouTube取消发布]** 工作流，可让您监视进度并查看任何故障信息。
请参阅 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).

**要取消发布视频以将其从YouTube中删除，请执行以下操作：**

1. 导航到要从YouTube渠道中取消发布的视频资产。
1. 在资产选择模式下，选择一个或多个已发布的视频资产。
1. 在工具栏中，选择 **[!UICONTROL 管理发布]**. 如有必要，请选择三个圆点图标(`. . .`)以查看 **[!UICONTROL 管理发布]**.
1. 在“管理发布”页面上，选择 **[!UICONTROL 取消发布]**.
1. 在页面的右上角，选择 **[!UICONTROL 下一个]**.
1. 在页面的右上角，选择 **[!UICONTROL 取消发布]**.

## 监控视频编码和YouTube发布进度 {#monitoring-video-encoding-and-youtube-publishing-progress}

在将新视频上传到应用了视频编码的文件夹时，或者，将视频发布到YouTube，监控视频编码/Youtube发布的进展情况（或失败）。 实际的YouTube发布进度仅通过日志提供。 但是，无论失败还是成功，它都将以下过程中描述的其他方式列出。 此外，当YouTube发布工作流或视频编码完成或中断时，您还会收到电子邮件通知。

### 监控进度 {#monitoring-progress}

您可以监控进度，包括失败的编码/YouTube发布。

1. 在资产文件夹中查看视频编码进度：

   * 在卡片视图中，视频编码进度按百分比显示在资产上。 如果出现错误，此信息也会显示在资产上。

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * 在列表视图中，视频编码进度显示在 **[!UICONTROL 处理状态]** 列。 如果出现错误，则同一列中将显示此消息。

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   默认情况下，此列不显示。要启用列，请选择 **[!UICONTROL 查看设置]** 从“视图”下拉菜单中，添加 **[!UICONTROL 处理状态]** 列和选择 **[!UICONTROL 更新]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. 查看资产详细信息的进度。 选择资产时，打开下拉菜单并选择 **[!UICONTROL 时间轴]**. 要将其缩小到编码或YouTube发布等工作流活动，请选择 **[!UICONTROL 工作流]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   任何工作流信息（如编码）都会显示在时间轴中。 对于YouTube发布，工作流时间轴还包含YouTube渠道的名称和YouTube视频URL。 此外，发布完成后，您会在工作流时间轴中看到任何失败通知。

   >[!NOTE]
   由于上有多个工作流配置，最终记录失败/错误消息可能需要较长时间 **[!UICONTROL 重试]**, **[!UICONTROL 重试延迟]**&#x200B;和 **[!UICONTROL 超时]** 从 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)，例如：
   * Apache Sling作业队列配置
   * AdobeGranite工作流外部进程作业处理程序
   * Granite工作流超时队列

   您可以调整 **[!UICONTROL 重试]**, **[!UICONTROL 重试延迟]**&#x200B;和 **[!UICONTROL 超时]** 属性。

1. 有关进行中的工作流，请参阅“工具”>“工作流” **[!UICONTROL >“实例”中提供的“工作流实例]** ” **[!UICONTROL (Workflow]** ) **[!UICONTROL >“]**&#x200B;实例”。

   >[!NOTE]
   您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   选择实例并选择 **[!UICONTROL 打开历史记录]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   在“工作流实例”区域中，您还可以暂停、终止或重命名工作流。 请参阅 [管理工作流](/help/sites-cloud/authoring/workflows/overview.md) 以了解更多信息。

1. 有关失败的作业，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 失败]**&#x200B;中显示的“工作流失败”。**[!UICONTROL 工作流失败]**&#x200B;列出所有失败的工作流活动。

   >[!NOTE]
   您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   由于上存在多个工作流配置，最终记录错误消息会花费较长时间 **[!UICONTROL 重试]**, **[!UICONTROL 重试延迟]**&#x200B;和 **[!UICONTROL 超时]** 从 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)，例如：
   * Apache Sling作业队列配置
   * AdobeGranite工作流外部进程作业处理程序
   * Granite工作流超时队列

   您可以调整 **[!UICONTROL 重试]**, **[!UICONTROL 重试延迟]**&#x200B;和 **[!UICONTROL 超时]** 属性。

1. 有关已完成的工作流，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 存档]**&#x200B;中的可用工作流存档。**[!UICONTROL 工作流存档]**&#x200B;列出了所有已完成的工作流活动。

   >[!NOTE]
   您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. 您会收到有关工作流作业中止或失败的电子邮件通知。 管理员可配置这些电子邮件通知。 请参阅 [配置电子邮件通知](#configuring-e-mail-notifications).

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

[!DNL Experience Manager] as a [!DNL Cloud Service] 允许您使用处理配置文件对MP4视频文件进行基本转码。 利用功能，不仅可上传，还可预览和缩放MP4视频文件。

![在中为视频转码创建处理配置文件 [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*图：用于在中进行视频转码的处理用户档案 [!DNL Experience Manager].*

如果您仅提供宽度或仅提供高度，并将另一个字段留空，则演绎版将保持宽高比。 H.264视频编解码器可用于转码。

要使用处理配置文件处理资产，请将配置文件添加到文件夹。 请参阅 [使用处理配置文件处理资产](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## 在视频资产中添加批注 {#annotate-video-assets}

您可以向视频资产添加注释。 在对视频添加注释时，播放器会暂停，以允许您对帧添加注释。 有关详细信息，请参阅 [管理视频资产](manage-video-assets.md).

>[!NOTE]
视频资产批注尚不支持MXF视频格式。

1. 从 [!DNL Assets] 控制台，选择 **[!UICONTROL 编辑]** ，以显示资产详细信息页面。
1. 要播放视频，请单击 **[!UICONTROL 预览]**.
1. 要在视频中添加批注，请单击 **[!UICONTROL 注释]**. 注释会在视频中的特定时间（帧）添加。 在添加注释时，您可以在画布上绘制图形，并在绘图中包含注释。 注释会自动保存。 要退出注释向导，请单击 **[!UICONTROL 关闭]**.
1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。
1. 要在时间轴中查看它，请单击注释。 要从时间轴中删除注释，请单击 **[!UICONTROL 删除]**.

## 最佳实践和限制 {#tips-limitations}

* 没有 [!DNL Dynamic Media] 许可证，则只能使用处理配置文件处理MP4文件。
* 使用处理配置文件转码MP4文件时，需遵循以下准则和限制：

   * Apple ProRes文件只能将代码转换为最大分辨率1080p。
   * 如果源文件的比特率大于200 Mbps，则只能将代码转换到最大分辨率1080p。
   * 如果源帧长>=60 fps，则可使用的源文件的最大大小为：

      * 400 MB用于4k转码。
      * 800 MB用于1080p转码。
      * 8 GB，用于720p转码。
   * 最大文件大小可转码为4k分辨率，为2.55 GB MP4文件，分辨率为4k、12 Mbps比特率和23 fps。


>[!MORELIKETHIS]
* [Dynamic Media视频文档](/help/assets/dynamic-media/video.md).
* [详细了解处理配置文件的使用、类型和配置](/help/assets/asset-microservices-configure-and-use.md).

