---
title: 新建视频查看器
description: Dynamic Media中的新Video Viewer通过改进的性能、可访问性和可配置性提供了增强的视频播放体验。
role: User
source-git-commit: f069e2cfaaa3c82a1d2391403b23f1ccf1ec2866
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 2%

---


# Dynamic Media中的新视频查看器 {#new-video-viewer-dynamic-media}

新的Dynamic Media视频查看器在Adobe Experience Manager (AEM)中提供了现代化的视频播放体验。 它在创作、预览和站点环境中提供一致且可扩展的查看体验，同时继续使用现有Dynamic Media工作流。

Dynamic Media中的现有视频查看器支持核心播放要求，但为现代分析和集成方案提供了有限的可扩展性和事件级集成

新的视频查看器通过以下方式解决这些限制：

* 提供更一致的播放体验
* 允许显式选择查看器
* 发送用于程序化消耗的结构化回放事件
* 支持与外部分析和外部系统的集成

查看器是作为附加选项提供的，在支持的地方需要明确选择。 它不会自动替换现有的视频查看器。

新的视频查看器适用于需要增强的可扩展视频体验且不会中断现有实施的组织。

> **注释**
>
> 新的视频查看器是有限的可用性功能。 您可以通过创建[支持票证](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)来启用它。


## 新视频查看器的工作方式 {#how-it-works}

新视频查看器的工作方式如下：

1. 视频资产将摄取到与Dynamic Media同步的文件夹中。
2. 可使用&#x200B;**视频（新）**&#x200B;从资产详细信息页面预览视频。
3. 在创作Sites页面时，可以在&#x200B;**Dynamic Media**&#x200B;组件中选择新的视频查看器。
4. 在播放期间，查看器向父窗口发送结构化事件。
5. 可选的查看器修饰符可用于控制播放行为。

## 与现有Video Viewer的主要区别 {#key-differences}

| 区域 | 描述 |
|------|-------------|
| 查看器可用性 | 显示为名为&#x200B;**视频（新）**&#x200B;的新选项 |
| 查看器选择 | 必须显式选择 |
| 可扩展性 | 发送结构化播放事件 |
| 集成 | 继续使用现有Dynamic Media工作流 |

## 先决条件 {#prerequisites}

在使用新的视频查看器之前，请确保满足以下先决条件：

| 要求 | 描述 |
|------------|-------------|
| Dynamic Media同步 | 资源文件夹必须与Dynamic Media同步。 |
| 视频配置文件 | 必须将视频配置文件应用于文件夹。 |
| 视频资产 | 必须将视频摄取到文件夹中。 |

新的视频查看器从&#x200B;**AEM as a Cloud Service版本2025.7.0**&#x200B;开始提供。

要启用或禁用“新建视频查看器”，请联系Adobe客户关怀团队。

## 预览新的视频查看器 {#preview}

执行以下步骤，从资源详细信息页面预览新视频查看器：

1. 导航到&#x200B;**Assets** > **文件**，然后打开包含视频资源的文件夹。
2. 单击视频资产，以打开资产详细信息页面。
3. 在左侧面板中，单击&#x200B;**查看器**。
4. 在&#x200B;**查看器**&#x200B;面板中，选择&#x200B;**视频（新）**。
5. 单击&#x200B;**URL**以复制预览链接。
   ![复制URL](/help/assets/assets/Copy-url1.jpg)

## 在站点中使用新的视频查看器 {#use-in-sites}

新的视频查看器可通过AEM Sites中的现有&#x200B;**Dynamic Media**&#x200B;组件使用。

### 添加Dynamic Media组件

执行以下步骤，使用Dynamic Media组件添加视频：

1. 在&#x200B;**站点编辑器**&#x200B;中打开该页面。
2. 将&#x200B;**Dynamic Media**&#x200B;组件拖动到页面上所需的位置。
3. 在页面上选择&#x200B;**Dynamic Media**&#x200B;组件。
4. 单击组件以打开资产选择器。
5. 选择视频资产。

![拖动Dynamic Media组件](/help/assets/assets/drag-component.jpeg)

### 配置查看器

执行以下步骤可配置查看器预设：

1. 在页面上选择&#x200B;**Dynamic Media**&#x200B;组件。
2. 单击组件工具栏中的&#x200B;**配置**。
   ![打开Dynamic Media设置](/help/assets/assets/configure-asset.png)

3. 在&#x200B;**Dynamic Media设置对话框**&#x200B;中，从&#x200B;**查看器预设**&#x200B;下拉列表中选择&#x200B;**视频（新）**。
   ![选择视频（新）查看器预设](/help/assets/assets/viewer-preset.jpeg)

4. 在&#x200B;**查看器修饰符**&#x200B;字段中输入任何必需的修饰符（例如，`autoplay=true&muted=true`）。
   ![查看器修饰符](/help/assets/assets/additional-modifiers.jpeg)

5. 保存更改。

使用新的视频查看器在页面上加载视频。

> **注意：**&#x200B;新的视频查看器不会自动替换现有视频。 使用Dynamic Media组件时，用户必须在&#x200B;**查看器预设**&#x200B;中手动选择&#x200B;**视频（新）**，或者在需要时更新指向新视频查看器的直接URL。

### 使用直接URL迁移视频

如果通过直接URL而不是Dynamic Media组件访问您的视频，则可以通过更新URL将它们切换为新的视频查看器。 例如：`https://s7d1.scene7.com/dmviewers/html5/VideoViewer.html?asset=<video-asset>`

## 查看器修饰符 {#viewer-modifiers}

查看器修饰符允许您控制资源加载、播放行为、流格式选择和查看器演示。

| 修饰符 | 描述 |
|--------|-------------|
| `asset` | 指定视频或自适应视频集的资产ID。 |
| `posterimage` | 指定开始播放前显示的图像。 |
| `serverurl` | 指定图像服务根路径。 |
| `contenturl` | 指定内容根路径。 |
| `videoserverurl` | 指定视频服务器根路径。 |
| `sources.dash` | 指定用于播放的DASH清单URL。 |
| `sources.hls` | 指定用于播放的HLS清单URL。 |
| `autoplay=true` | 加载视频时自动开始播放。 |
| `controls=true/false` | 显示或隐藏视频播放控件。 |
| `loop=true` | 在视频结束后自动重新启动播放。 |
| `muted=true` | 在静音状态下开始播放。 |
| `playbackrates` | 指定可用的播放速度选项。 |
| `playback` | 指定流格式（自动、hls、短划线或渐进式）。 |
| `progressivebitrate` | 指定渐进式播放的比特率。 |
| `initialbitrate` | 指定自适应流播放的初始比特率。 |
| `isletterboxed=true/false` | 控制视频是信箱式还是拉伸式。 |
| `customcss` | 指定用于查看器样式的自定义CSS文件。 |
| `transition` | 指定查看器控件的显示或隐藏过渡行为。 |

修饰符在&#x200B;**查看器修饰符**&#x200B;字段中指定为查询参数。

## 受支持的事件 {#supported-events}

新的视频查看器在播放期间会发送以下事件：

| 事件类型 | 描述 |
|-----------|-------------|
| play | 视频开始播放 |
| pause | 视频已暂停 |
| 搜寻 | 用户在视频中搜寻 |
| 加载 | 视频已加载 |
| 关闭 | 播放器已关闭 |
| 元数据 | 元数据，例如持续时间 |
| 里程碑 | 已达到播放里程碑 |
| current_time | 定期播放位置 |
| 全屏 | 输入全屏 |
| un_fullscreen | 退出全屏 |

## 在父窗口中处理事件 {#handling-events}

新的视频查看器会在视频交互期间向父页面发送与播放相关的消息。

要处理这些事件，父应用程序必须侦听浏览器消息事件并在处理数据之前验证消息来源。

事件有效负载包括事件类型、播放状态、当前播放时间和其他元数据等信息。 这些事件可用于支持Analytics跟踪、自定义交互或与外部系统的集成。

Adobe建议验证消息源，以确保仅处理来自受信任的Dynamic Media域的事件。

## 新视频查看器的视频参与报告 {#video-engagement-report}

视频参与报表为Dynamic Media中使用新增的视频查看器播放的视频提供分析量度。 此报表可提供指定月份的汇总性能数据，并支持每月报告。

报告是根据请求生成的。 要请求报告，请创建[支持票证](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)并提供以下详细信息：

* 报告月份 — 指定需要报告的月份（例如，2026年1月）。
* 投放电子邮件地址 — 提交报告的组（推荐）或个人的电子邮件地址

该报告提供了每个视频的参与量度，包括查看次数、展示次数、观看时间、完成率和参与度分数。

### 报告格式

* 报表以CSV格式交付。
* 每一行表示一个视频。
* 系统会汇总选定报表期间的量度。
* 从报表中排除已删除的资源。
* 支持按`tenant_name`筛选。

### 报告字段

视频参与报表包含以下字段：

| 字段 | 描述 | 计算 |
|-------|------------|-------------|
| `video_id` | 唯一视频标识符。 | NA |
| `video_name` | 视频资产的名称。 | NA |
| `video_created_date` | 创建视频的日期。 | NA |
| `duration_in_seconds` | 视频持续时间（以秒为单位）。 | NA |
| `video_views` | 在选定报告期间发生的视频播放事件总数。 | NA |
| `video_impressions` | 视频加载的总次数。 | NA |
| `video_watched_seconds` | 在所有播放事件中观看的总秒数。 | 在所有播放事件中观看的秒数总和 |
| `play_rate` | 相对于视频加载的视频播放百分比。 | (`video_views` ÷ `video_impressions`) × 100 |
| `avg_time_watched_in_seconds` | 每次查看的平均观看秒数。 | `video_watched_seconds` ÷ `video_views` |
| `avg_completion_rate` | 达到完整视频完成的查看次数的百分比。 | （已完成视图÷ `video_views`） × 100 |
| `engagement_score` | 所有播放事件的平均观看百分比。 | （在`video_views`÷的所有会话中查看的视频时间轴的总百分比） |
| `tenant_name` | 与数据关联的公司或租户的标识符。 | NA |

## 常见问题解答 {#faq-video-engagement}

+++如果视频被设置为自动播放，是自动计为观看还是仅在用户观看了最少时段后计为观看次数？

自动播放将被计为视频查看。 自动启动的播放将记录为视图。

+++

+++如果用户只观看部分视频（例如，10秒视频的前2秒和后2秒），则是否将其计为已完成的查看？

当播放到达视频时间轴结尾时，即使跳过部分视频，也会将视图计为已完成。

+++

+++如果用户向后滚动并重新观看视频的各个部分，它是否会增加video_views计数、engagement_score计数，还是同时增加两者？

重新观看部分视频不会增加video_views计数。 其他播放将参与engagement_score。

+++

+++如果同一用户多次观看同一视频而没有重新加载页面，那么将如何计算video_views和engagement_score？

重复播放而不重新加载页面不会增加video_views计数。 其他播放将参与engagement_score。

+++

+++暂停和恢复视频是否会影响参与跟踪或完成率的计算？

暂停和恢复播放不会影响参与跟踪或完成率计算。

+++
