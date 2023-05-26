---
title: Dynamic Media 视频配置文件
description: Dynamic Media已随附预定义的自适应视频编码配置文件。 此现成配置文件中的设置已经过优化，可为您的客户提供最佳观看体验。 您还可以向视频添加智能裁剪。
contentOwner: Rick Brough
feature: Asset Management,Video Profiles,Renditions
role: User
exl-id: 07bfd353-c105-4677-a094-b70c1098fb7f
source-git-commit: 2009e549eadd97d4d2bfcccd728ece17ecfeede5
workflow-type: tm+mt
source-wordcount: '3716'
ht-degree: 7%

---

# Dynamic Media 视频配置文件{#video-profiles}

Dynamic Media已随附预定义的自适应视频编码配置文件。 此现成配置文件中的设置已经过优化，可为您的客户提供最佳观看体验。 当您使用自适应视频编码配置文件对主要源视频进行编码时，在播放期间，视频播放器会根据客户的Internet连接速度自动调整视频流的质量。 此操作称为自适应比特率流。

以下是决定视频质量的其他因素：

* **上传的主源视频的分辨率**

   如果MP4视频是以较低分辨率（如240p或360p）录制的，则无法以高清晰度流式传输。

* **视频播放器大小**

   默认情况下，自适应视频编码配置文件中的“宽度”设置为“自动”。 同样，在播放期间，将根据播放器的大小使用最佳质量。

参见 [视频编码的最佳实践](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

另请参阅 [组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md).


>[!NOTE]
>
>要生成视频的元数据和关联的视频图像缩略图，视频本身必须经过Dynamic Media中的编码过程。 在Adobe Experience Manager中， **[!UICONTROL Dynamic Media编码视频]** 如果您已启用Dynamic Media并设置了视频Cloud Services，则工作流会对视频进行编码。 此工作流会捕获工作流进程历史记录和失败信息。参见 [监控视频编码和YouTube发布进度](/help/assets/dynamic-media/video.md#monitoring-video-encoding-and-youtube-publishing-progress). 如果您已启用Dynamic Media并设置了视频Cloud Services，则 **[!UICONTROL Dynamic Media编码视频]** 上传视频时，工作流会自动生效。 (如果您没有使用Dynamic Media，则 **[!UICONTROL DAM更新资产]** 工作流将生效。)
>
>在搜索资源时，元数据很有用。 缩略图是在编码期间生成的静态视频图像。 它们是Experience Manager系统必需的，并用于用户界面中，以帮助您在“卡片”视图、“搜索结果”视图和“资源列表”视图中直观地识别视频。 当您选择已编码视频的“演绎版”图标（画家的调色板）时，可以查看生成的缩略图。

创建完视频配置文件后，可将其应用到一个或多个文件夹。 参见 [将视频配置文件应用到文件夹](#applying-a-video-profile-to-folders).

要为其它资产类型定义高级处理参数，请参阅 [配置资源处理](/help/assets/dynamic-media/config-dm.md#configuring-asset-processing).

另请参阅 [用于处理元数据、图像和视频的配置文件](/help/assets/dynamic-media/about-image-video-profiles.md).

## 自适应视频编码预设 {#adaptive-video-encoding-presets}

下表列出了将自适应视频流的配置文件编码到移动设备和平板电脑以及台式计算机时的最佳实践。 您可以将这些预设用于任何长宽比视频。

<table>
 <tbody>
  <tr>
   <td><strong>视频格式编解码器</strong></td>
   <td><strong>视频大小 — 宽度（像素）</strong></td>
   <td><strong>视频大小 — 高度（像素）</strong></td>
   <td><strong>保持宽高比？</strong></td>
   <td><strong>视频比特率(Kbps)</strong></td>
   <td><strong>视频帧速率(Fps)</strong></td>
   <td><strong>音频编解码器</strong></td>
   <td><strong>音频比特率(Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>是</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>540</td>
   <td>是</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>720<br /> </td>
   <td>是</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## 关于在视频配置文件中使用智能裁剪 {#about-smart-crop-video}

视频智能裁剪是视频配置文件中一项可选功能。 该工具使用Adobe Sensei自动检测和裁切您上传的任何自适应视频或渐进视频中的焦点，而不管其大小。

智能裁剪支持的视频格式包括MP4、MKV、MOV、AVI、FLV和WMV。

智能裁剪支持的最大视频文件大小符合以下条件：

* 持续5分钟。
* 每秒30帧(FPS)。
* 文件大小为300 MB。

Adobe Sensei限制为9000帧。 即，30 FPS时为5分钟。 如果视频的FPS较高，则支持的最大视频持续时间会缩短。 例如，60 FPS视频的长度必须为2分半钟，才能得到Adobe Sensei和智能裁剪的支持。

![视频智能裁剪](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>要使视频智能裁剪正常工作，您必须在视频配置文件中包含一个或多个视频编码预设。

要将智能裁剪用于视频，您需要创建自适应或渐进式视频编码配置文件。 在您的个人资料中，使用 **[!UICONTROL 智能裁剪比率]** 工具来选择预定义的纵横比。 例如，在定义视频编码预设后，您可以添加“移动设备横向”定义（纵横比为16x9）和“移动设备纵向”定义（纵横比为9x16）。 可以选择包括1x1、4x3和4x5的其他长宽比或裁切比。

![使用智能裁剪编辑视频编码配置文件](assets/edit-smart-crop-video2.png)

您可以使用的最右侧的滑块，打开或关闭视频配置文件中的视频智能裁切 **[!UICONTROL 智能裁剪比率]** 在用户界面中。

创建并保存视频配置文件后，可将其应用到所需的文件夹。

参见 [将视频配置文件应用到特定文件夹](#applying-video-profiles-to-specific-folders) 或 [全局应用视频配置文件](#applying-a-video-profile-globally).

另请参阅 [图像智能裁剪](image-profiles.md).

## 为自适应比特率流创建视频配置文件 {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media已随附预定义的自适应视频编码配置文件 — 一组用于MP4 H.264的视频上传设置 — 该配置文件已针对最佳观看体验进行了优化。 您可以在上传视频时使用此配置文件。

但是，如果此预定义配置文件不符合您的需求，您可以选择创建自己的自适应视频编码配置文件。 作为最佳实践，当您使用设置时 **[!UICONTROL 自适应流播放的编码]**，则会验证您添加到配置文件的所有编码预设。 此功能确保所有视频具有相同的宽高比。 此外，将编码的视频视为用于流的多比特率集。

在创建视频编码配置文件时，您会注意到大多数编码选项都已预填充了推荐的默认设置，以便为您提供帮助。 但是，如果您选择的值不是推荐的默认值，则可能会导致播放期间的视频质量变差以及其他性能问题。

因此，对于配置文件中的所有MP4 H.264视频编码预设，将验证以下值以确保它们在配置文件中的各个编码预设中相同，从而实现自适应比特率流：

* 视频格式编解码器 — MP4 H.264 (.mp4)
* 音频编解码器
* 音频比特率
* 保持宽高比
* 两次编码
* 恒定比特率
* H264 配置文件
* 音频采样速率

如果值不同，可以继续按原样创建配置文件。 但是，自适应比特率流是不可能的。 相反，用户体验单比特率流。 建议您编辑编码设置，以在配置文件中的各个编码预设中使用相同的值。 （如果启用了“自适应流播放的编码”，则视频配置文件/预设编辑器将强制自适应视频编码设置的奇偶校验。）

另请参阅 [为渐进式流创建视频编码配置文件](#creating-a-video-encoding-profile-for-progressive-streaming).

另请参阅 [视频编码的最佳实践](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

要为其它资产类型定义高级处理参数，请参阅 [配置资源处理](/help/assets/dynamic-media/config-dm.md#configuring-asset-processing).

**为自适应比特率流创建视频配置文件**，

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频配置文件]**.
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 输入配置文件的名称和说明。
1. 在“创建/编辑视频编码预设”页面上，选择 **[!UICONTROL 添加视频编码预设]**.
1. 在 **[!UICONTROL 基本]** 选项卡，设置视频和音频选项。
选择每个选项旁边的信息图标，以了解更多说明或基于所选视频格式编解码器的推荐设置。
1. 在“Video Size（视频大小）”标题下，确保 **[!UICONTROL 保持宽高比]** 已选中。
1. 设置视频帧大小分辨率（像素）。 使用 **[!UICONTROL 自动]** 值，可自动缩放以匹配源宽高比（宽高比）。 例如，Auto x 480或640 x Auto。

1. 执行下列操作之一：

   * 在 **[!UICONTROL 宽度]** 字段，输入 **[!UICONTROL 自动]**. 在 **[!UICONTROL 高度]** 字段中，输入像素值。

   * 要帮助您可视化视频的大小，请选择右侧的信息图标(i) **[!UICONTROL 高度]** 以打开“大小计算器”页面。 使用 **[!UICONTROL 大小计算器]** 设置您想要的视频尺寸（由蓝色框表示）。 选择 **[!UICONTROL X]** 完成时位于右上角。

1. （可选）选择 **[!UICONTROL 高级]** 选项卡，并确保 **[!UICONTROL 使用默认值]** 复选框处于选中状态（推荐）。 或者，修改高级视频和音频设置。
1. 在页面的右上角，选择 **[!UICONTROL 保存]** 以保存预设。
1. 执行下列操作之一：
   * 重复步骤4 - 10以创建更多编码预设。 （自适应视频流需要多个视频预设。）
   * 继续下一步骤。

1. （可选）要将视频智能裁剪添加到应用此配置文件的视频中，请执行以下操作：
   * 在“编辑视频配置文件”页面的“智能裁剪比率”标题右侧，选择 **[!UICONTROL 新增]**.
   * 在名称字段中，键入有助于轻松识别该裁切率的名称。
   * 从 **[!UICONTROL 裁剪比率]** 下拉列表中，选择要使用的比率。

1. 执行下列操作之一：

   * 根据需要继续添加新裁切比率。
   * 继续下一步骤。

1. 在页面的右上角，选择 **[!UICONTROL 保存]** 以保存配置文件。

您现在可以将配置文件应用到包含视频的文件夹。 参见 [将视频配置文件应用到文件夹](#applying-a-video-profile-to-folders) 或 [全局应用视频配置文件](#applying-a-video-profile-globally).

## 为渐进式流创建视频配置文件 {#creating-a-video-encoding-profile-for-progressive-streaming}

如果您选择不使用选项 **[!UICONTROL 自适应流播放的编码]**，您添加到配置文件的所有编码预设都将被视为单比特率流或渐进式视频交付的单个视频演绎版。 此外，不会进行验证，以确保所有视频呈现具有相同的纵横比。

支持的视频格式编解码器为H.264 (.mp4)和WebM。

另请参阅 [为自适应比特率流创建视频编码配置文件](#creating-a-video-encoding-profile-for-adaptive-streaming).

另请参阅 [视频编码的最佳实践](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

要为其它资产类型定义高级处理参数，请参阅 [配置资源处理](/help/assets/dynamic-media/config-dm.md#configuring-asset-processing).

**要为渐进式流创建视频配置文件，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频配置文件]**.
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 输入配置文件的名称和说明。
1. 在“创建/编辑视频编码预设”页面上，选择 **[!UICONTROL 添加视频编码预设]**.
1. 在 **[!UICONTROL 基本]** 选项卡，设置视频和音频选项。
选择每个选项旁边的信息图标，以了解更多说明或基于所选视频格式编解码器的推荐设置。
1. （可选）在“视频大小”标题下，取消选中 **[!UICONTROL 保持宽高比]**.
1. 执行以下操作：
   * 在 **[!UICONTROL 宽度]** 字段，输入 **[!UICONTROL 自动]**.
   * 在 **[!UICONTROL 高度]** 字段中，输入像素值。
要帮助您可视化视频的大小，请选择“高度”的信息图标以打开 **[!UICONTROL 大小计算器]** 页面。 使用 **[!UICONTROL 大小计算器]** 页面进一步设置所需视频大小（蓝框）。 完成后，在对话框的右上角，选择 **[!UICONTROL X]**.
1. （可选）执行以下操作之一：

   * 选择 **[!UICONTROL 高级]** 选项卡，并确保 **[!UICONTROL 使用默认值]** 复选框处于选中状态（推荐）。

   * 清除 **[!UICONTROL 使用默认值]** 复选框，并指定所需的视频设置和音频设置。
选择每个选项旁边的信息图标，以了解更多说明或基于所选视频格式编解码器的推荐设置。

1. 在页面的右上角，选择 **[!UICONTROL 保存]** 以保存预设。
1. 执行下列操作之一：

   * 重复步骤4 - 9以创建更多编码预设。
   * 继续下一步骤。

1. （可选）要将视频智能裁剪添加到应用此配置文件的视频中，请执行以下操作：

   * 在“编辑视频配置文件”页面的“智能裁剪比率”标题右侧，选择 **[!UICONTROL 新增]**.
   * 在名称字段中，键入有助于您轻松识别裁切率的名称。
   * 从 **[!UICONTROL 裁剪比率]** 下拉列表中，选择要使用的比率。

1. 执行下列操作之一：

   * 根据需要继续添加新裁切比率。
   * 继续下一步骤。

1. 在页面的右上角，选择 **[!UICONTROL 保存]** 以保存配置文件。

您现在可以将配置文件应用到包含视频的文件夹。 参见 [将视频配置文件应用到文件夹](#applying-a-video-profile-to-folders) 或 [全局应用视频配置文件](#applying-a-video-profile-globally).

## 使用添加自定义的视频编码参数 {#using-custom-added-video-encoding-parameters}

您可以编辑视频的现有编码配置文件，以利用在Experience Manager中创建或编辑视频配置文件时未在用户界面中找到的高级视频编码参数。 您可以自定义向现有配置文件添加一个或多个高级参数，例如minBitrate和maxBitrate。

**要使用自定义添加的视频编码参数，请执行以下操作：**

1. 选择Experience Manager徽标，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在“CRXDE Lite”页面的左侧“资源管理器”面板中，导航到以下内容：

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. 在页面右下方的面板中，从“属性”选项卡中，指定要使用的参数的&#x200B;**[!UICONTROL 名称]**、**[!UICONTROL 类型]**&#x200B;和&#x200B;**[!UICONTROL 值]**。

   可以使用以下高级参数：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>描述</strong><br /> </td>
   <td><strong>类型</strong><br /> </td>
   <td><strong>价值</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>用于编码的H.264级别。 通常，此级别会根据您使用的编码设置自动确定。</td>
   <td><code>String</code></td>
   <td><p>10 * h264级</p> <p>例如，3.0 = 30,1.3 = 13)</p> <p>无默认值。</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>关键帧之间的目标帧数。 计算此值以便每2-10秒生成一次关键帧。 例如，以每秒30帧的速度，关键帧间隔为60-300。<br /> <br /> 较低的关键帧间隔改善了自适应视频编码的流搜索和流切换行为，并且还可以提高具有大量运动的视频的质量。 但是，由于关键帧会增加文件的大小，因此较低的关键帧间隔通常会导致在给定比特率下整体视频质量较低。</td>
   <td><code>String</code></td>
   <td><p>正数。</p> <p>默认值为300。</p> <p>HLS或DASH（自适应比特率流）的建议值为60-90。 (若要将DASH用于视频，必须先由您帐户上的Adobe技术支持启用。 参见 <a href="/help/assets/dynamic-media/video.md#enable-dash">在您的帐户上启用DASH</a>.)</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>允许可变比特率编码的最小比特率，以Kbps为单位（千位/秒）。</p> <p>此参数仅在<strong> 使用恒定比特率</strong> 创建或编辑视频编码配置文件时，取消选中高级选项卡中的选项。</p> <p>另请参阅 <a href="/help/assets/dynamic-media/video.md#bitrate">比特率</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>正数，以Kbps为单位。</p> <p>无默认值。</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>允许可变比特率编码的最大比特率（以Kbps为单位）。</p> <p>此参数仅在<strong> 使用恒定比特率</strong> 创建或编辑视频编码配置文件时，取消选中高级选项卡中的选项。</p> <p>另请参阅 <a href="/help/assets/dynamic-media/video.md#bitrate">比特率</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>正数（以Kbps为单位）。</p> <p>无默认值。 但是，推荐值最多为编码比特率的两倍。</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>将值设置为 <code>true</code> 强制音频流采用恒定比特率（如果音频编解码器支持）。</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>默认为 <code>false</code>.</p> <p>HLS或DASH的建议值为 <code>false</code>. (若要将DASH用于视频，必须先由您帐户上的Adobe技术支持启用。 参见 <a href="/help/assets/dynamic-media/video.md#enable-dash">在您的帐户上启用DASH</a>.)</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. 在页面的右下角附近，选择 **[!UICONTROL 添加]**.
1. 执行下列操作之一：

   * 重复步骤3和4，向视频编码配置文件中添加其他参数。
   * 在页面的左上角附近，选择 **[!UICONTROL 全部保存]**.

1. 在“CRXDE Lite”页面的左上角，选择 **[!UICONTROL 返回主页]** 图标以返回Experience Manager。

### 编辑视频配置文件 {#editing-a-video-encoding-profile}

您可以编辑已创建的任何视频配置文件，以添加、编辑或删除该配置文件中的视频预设。

默认情况下，您无法编辑预定义的、现成可用的 **[!UICONTROL 自适应视频编码]** Dynamic Media随附的资料。 相反，您可以轻松复制配置文件并使用新名称保存它。 然后，您可以在复制的配置文件中编辑所需的预设。

另请参阅 [视频编码的最佳实践](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

要为其它资产类型定义高级处理参数，请参阅 [配置资源处理](/help/assets/dynamic-media/config-dm.md#configuring-asset-processing).

**要编辑视频配置文件：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频配置文件]**.
1. 在“视频配置文件”页面上，检查一个视频配置文件名称。
1. 在工具栏上，选择 **[!UICONTROL 编辑]**.
1. 在“视频编码配置文件”页面上，根据需要编辑名称和描述。
1. 作为最佳实践，请确保选中“自 **[!UICONTROL 适应流播放的编码]** ”复选框。选择信息图标以查看自适应比特率流的描述。 （如果您正在编辑渐进式视频配置文件，请不要选中此复选框。）
1. 在视频编码预设标题下，添加、编辑或删除构成配置文件的视频编码预设。

   选择上每个选项旁边的信息图标 **[!UICONTROL 基本]** 和 **[!UICONTROL 高级]** 选项卡以了解更多描述或基于所选视频格式编解码器的推荐设置。

1. 在页面的右上角，选择 **[!UICONTROL 保存]**.

### 复制视频配置文件 {#copying-a-video-encoding-profile}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频配置文件]**.
1. 在“视频配置文件”页面上，检查一个视频配置文件名称。
1. 在工具栏上，选择 **[!UICONTROL 复制]**.
1. 在视频编码配置文件页面上，输入配置文件的新名称。
1. 作为最佳实践，请确保选中“自 **[!UICONTROL 适应流播放的编码]** ”复选框。 选择信息图标以查看自适应比特率流的描述。 （如果要复制渐进式视频配置文件，请勿选中该复选框。）

   在Dynamic Media — 混合模式下，如果WebM视频预设是视频配置文件的一部分，则 **[!UICONTROL 自适应流播放的编码]** 因为所有预设都必须是MP4，所以不可能实现。
1. 在视频编码预设标题下，添加、编辑或删除构成配置文件的视频编码预设。

   在“基本”和“高级”选项卡上选择每个选项旁边的信息图标，以查看建议的设置和描述。

1. 在页面的右上角，选择 **[!UICONTROL 保存]**.

### 删除视频配置文件 {#deleting-a-video-encoding-profile}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频配置文件]**.
1. 在“视频配置文件”页面上，检查一个或多个视频配置文件名称。
1. 在工具栏上，选择 **[!UICONTROL 删除]**.
1. 选择 **[!UICONTROL 确定]**.

## 将视频配置文件应用到文件夹 {#applying-a-video-profile-to-folders}

将视频配置文件分配给文件夹时，任何子文件夹都会自动从其父文件夹继承配置文件。 因此，您只能将一个视频配置文件分配给文件夹。 因此，请仔细考虑上传、存储、使用和存档资产的位置的文件夹结构。

如果为文件夹分配了不同的视频配置文件，则新配置文件将覆盖以前的配置文件。 以前现有的文件夹资产保持不变。 新配置文件将应用于稍后添加到此文件夹的资产。

在用户界面中，会使用卡片名称中显示的配置文件名称指示已为其分配配置文件的文件夹。

![chlimage_1-517](assets/chlimage_1-517.png)

您可以将视频配置文件应用到特定文件夹，也可以全局应用到所有资产。

如果文件夹中已有您后来更改的现有“视频配置文件”，您可以重新处理该文件夹中的资产。 请参阅[重新处理文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

### 将视频配置文件应用到特定文件夹 {#applying-video-profiles-to-specific-folders}

您可以将视频配置文件应用到中的文件夹 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中，则从 **[!UICONTROL 属性]**. 本节将介绍这两种将视频配置文件应用到文件夹的方法。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

另请参阅 [编辑文件夹的处理配置文件后，重新处理文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### 通过“配置文件”用户界面将视频配置文件应用到文件夹 {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频配置文件]**.
1. 选择要应用于一个或多个文件夹的视频配置文件。
1. 选择 **[!UICONTROL 将配置文件应用到文件夹]** 并选择一个或多个用于接收新上传资源的文件夹，然后选择 **[!UICONTROL 应用]**. 在&#x200B;**[!UICONTROL 卡片视图]**&#x200B;中，如果文件夹已经分配了配置文件，则文件夹名称的正下方会显示配置文件的名称。您可以 [监控视频配置文件处理作业的进度](#monitoring-the-progress-of-an-encoding-job).

#### 将视频配置文件从“属性”应用到文件夹 {#applying-video-profiles-to-folders-from-properties}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]** ，然后转到要将视频配置文件应用到的文件夹。
1. 在文件夹上，选中复选标记以将其选中，然后选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 视频配置文件]** 选项卡，然后从下拉菜单中选择配置文件，然后选择 **[!UICONTROL 保存并关闭]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

   ![chlimage_1-518](assets/chlimage_1-518.png)
您可以 [监控视频配置文件处理作业的进度](#monitoring-the-progress-of-an-encoding-job).

### 全局应用视频配置文件 {#applying-a-video-profile-globally}

除了将配置文件应用到文件夹外，您还可以全局应用配置文件，以便上传到任何文件夹中Experience Manager资源中的任何内容均已应用选定的配置文件。

另请参阅 [重新处理文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**要全局应用视频配置文件，请执行以下操作：**

* 导航到CRXDE Lite以下节点： `/content/dam/jcr:content`. 添加属性 `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` 并选择 **[!UICONTROL 全部保存]**.

   ![chlimage_1-519](assets/chlimage_1-519.png)
* 您可以 [监控视频配置文件处理作业的进度](#monitoring-the-progress-of-an-encoding-job).

## 监控视频配置文件处理作业的进度 {#monitoring-the-progress-of-an-encoding-job}

将显示处理指示器（或进度条），以便您可以直观地监视视频配置文件处理作业的进度。

您还可以查看 `error.log` 文件，用于监视编码作业的进度、查看编码是否已完成或查看任何作业错误。 此 `error.log` 可在以下位置找到： `logs` 安装Experience Manager实例的文件夹。

## 从文件夹中删除视频配置文件 {#removing-a-video-profile-from-folders}

当您从文件夹中删除视频配置文件时，任何子文件夹都会自动继承从其父文件夹中删除配置文件的操作。 但是，在文件夹内发生的任何文件处理都保持不变。

您可以从中的文件夹删除视频配置文件 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中，则从 **[!UICONTROL 文件夹设置]**. 本节将介绍这两种将视频配置文件从文件夹删除的方法。

### 通过“配置文件”用户界面从文件夹中删除视频配置文件 {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频配置文件]**.
1. 选择要从一个或多个文件夹中删除的视频配置文件。
1. 选择 **[!UICONTROL 从文件夹中删除配置文件]** 并选择一个或多个要从中删除配置文件的文件夹，然后选择 **[!UICONTROL 移除]**.

   您可以确认视频配置文件不再应用于文件夹，因为文件夹名称下方不再显示该名称。

### 通过属性从文件夹中删除视频配置文件 {#removing-video-profiles-from-folders-by-way-of-properties}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]** ，然后转到要从中删除视频配置文件的文件夹。
1. 在文件夹上，选中复选标记以将其选中，然后选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 视频配置文件]** 选项卡并选择 **[!UICONTROL 无]** 从下拉菜单中，选择 **[!UICONTROL 保存并关闭]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
