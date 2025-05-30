---
title: Dynamic Media 疑难解答
description: 了解在Dynamic Media中使用图像、集和查看器时可以尝试的故障排除提示。
contentOwner: Rick Brough
feature: Troubleshooting,Image Sets,Viewers
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: 26afff3a39a2a80c1f730287b99f3fb33bff0673
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 1%

---

# Dynamic Media 疑难解答 {#troubleshooting-dynamic-media-scene-mode}

以下主题介绍了Dynamic Media的疑难解答。

## 新的Dynamic Media配置 {#new-dm-config}

请参阅[新Dynamic Media配置疑难解答](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config)。

## 常规(所有Assets) {#general-all-assets}

以下是适用于所有资产的一些常规提示和技巧。

### 资源同步状态属性 {#asset-synchronization-status-properties}

可以在CRXDE Lite中查看以下资源属性，以确认成功地将资源从Adobe Experience Manager同步到Dynamic Media：

| **属性** | **示例** | **描述** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 表示节点已链接到Dynamic Media的一般指示符。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete**&#x200B;或错误文本 | 将资源上传到Dynamic Media的状态。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必须填充以生成指向Dynamic Media远程资产的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **成功**&#x200B;或&#x200B;**失败：`<error text>`** | 资产（旋转集、图像集等）、图像预设、查看器预设、图像映射更新的同步状态，或者已编辑的图像的同步状态。 |

### 同步日志记录 {#synchronization-logging}

同步错误和问题记录在`error.log`中(Experience Manager服务器目录`/crx-quickstart/logs/`)。 有足够的日志记录功能来确定大多数问题的根本原因，但您可以通过Sling控制台([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))增加对`com.adobe.cq.dam.ips`程序包的DEBUG日志记录以收集更多信息。

### 版本控制 {#version-control}

在替换现有Dynamic Media资源（名称和位置相同）时，您可以保留两个资源或替换/创建版本：

* 保留这两个名称将为已发布的资源URL创建一个具有唯一名称的资源。 例如，`image.jpg`是原始资产，`image1.jpg`是新上传的资产。

* Dynamic Media不支持创建版本。 新版本将替换投放中的现有资产。

## 图像和集 {#images-and-sets}

如果您在使用图像和集时遇到问题，请参阅以下疑难解答指南。

<table>
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>如何调试</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>无法访问资产详细信息视图中的复制URL/嵌入按钮</td>
   <td>
    <ol>
     <li><p>转到CRX/DE ：</p>
      <ul>
       <li>检查JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code>中的预设是否已定义。 如果您从Experience Manager6.x升级到6.4并选择退出迁移，则此位置适用。 否则，位置为<code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>检查以确保JCR中的资产在元数据下有<code>dam:scene7FileStatus</code><strong> </strong>显示为<code>PublishComplete</code>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>刷新页面/导航到其他页面并返回（必须重新编译侧边栏JSP）</p> <p>如果这行不通：</p>
    <ul>
     <li>Publish资源。</li>
     <li>重新上传资源并发布。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>在幻灯片之间切换后，轮播热点四处移动</td>
   <td><p>检查所有幻灯片的大小是否相同。</p> </td>
   <td><p>仅对轮播使用具有相同大小的图像。</p> </td>
  </tr>
  <tr>
   <td>图像未使用Dynamic Media查看器预览</td>
   <td><p>检查资源在元数据属性(CRXDE Lite)中是否包含<code>dam:scene7File</code></p> </td>
   <td><p>检查所有资产是否已完成处理。</p> </td>
  </tr>
  <tr>
   <td>上传的资产未显示在资产选择器中</td>
   <td><p>检查资产具有属性<code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code>(CRXDE Lite)</p> </td>
   <td><p>检查所有资产是否已完成处理。</p> </td>
  </tr>
  <tr>
   <td>当资产尚未开始处理时，卡片视图上的横幅显示<strong>新建</strong></td>
   <td>检查资源<code>jcr:content</code> &gt; <code>dam:assetState</code> =如果<code>unprocessed</code>，则检查该资源未被工作流提取。</td>
   <td>等到工作流拾取资产为止。</td>
  </tr>
  <tr>
   <td>图像或集不显示查看器URL或嵌入代码</td>
   <td>检查查看器预设是否已发布。</td>
   <td><p>转到<strong>工具</strong> &gt; <strong>Assets</strong> &gt; <strong>查看器预设</strong>并发布查看器预设。</p> </td>
  </tr>
 </tbody>
</table>

## 视频 {#video}

如果您遇到视频问题，请参阅以下疑难解答指南。

<table>
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>如何调试</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>无法预览视频</td>
   <td>
    <ul>
     <li>检查文件夹是否分配了视频配置文件（如果文件格式不受支持）。 如果不受支持，则仅显示图像。</li>
     <li>视频配置文件必须包含多个编码预设才能生成AVS集（对于MP4文件，单个编码将被视为视频内容；对于不受支持的文件，与未处理的文件相同）。</li>
     <li>通过确认元数据中的<code>dam:scene7FileAvs</code>个（共<code>dam:scene7File</code>个），检查视频是否已完成处理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>将视频配置文件分配给文件夹。</li>
     <li>编辑视频配置文件以包含多个编码预设。</li>
     <li>等待视频完成处理。</li>
     <li>在重新加载视频之前，请确保Dynamic Media编码视频工作流未运行。<br/> </li>
     <li>重新上传视频。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>视频未编码</td>
   <td>
    <ul>
     <li>检查是否已配置Dynamic MediaCloud Service。</li>
     <li>检查视频配置文件是否与上传文件夹关联。</li>
    </ul> </td>
   <td>
    <ol>
     <li>检查是否已正确设置Cloud Service下的Dynamic Media配置。</li>
     <li>检查文件夹是否具有视频配置文件。 此外，检查视频配置文件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>视频处理耗时过长</td>
   <td><p>要确定视频编码是否仍在进行中或是否已进入失败状态，请执行以下操作：</p>
    <ul>
     <li>检查视频状态<code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>缺少视频演绎版</td>
   <td><p>上传视频时，但没有编码呈现版本：</p>
    <ul>
     <li>检查文件夹是否分配了视频配置文件。</li>
     <li>通过确认元数据中的<code>dam:scene7FileAvs</code>，检查视频是否已完成处理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>将视频配置文件分配给文件夹。</li>
     <li>等待视频完成处理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 查看器 {#viewers}

如果查看者遇到问题，请参阅以下疑难解答指南。

### 问题：查看器预设未发布 {#viewers-not-published}

**如何调试**

1. 继续到示例管理器诊断页面： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`。
1. 观察计算值。 正确操作时，您会看到以下内容： `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`。

   >[!NOTE]
   >
   >配置Dynamic Media云设置后，可能需要大约10分钟才能同步查看器资源。

1. 如果仍有未激活的资源，请选择&#x200B;**列出所有未激活的Assets**&#x200B;按钮之一以查看详细信息。

**解决方案**

1. 导航到管理工具中的查看器预设列表： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. 选择所有查看器预设，然后选择&#x200B;**Publish**。
1. 导航回示例管理器，并观察未激活的资源计数现在为零。

### 问题：查看器预设图稿在资产详细信息中预览或复制URL/嵌入代码中返回404 {#viewer-preset-404}

**如何调试**

在CRXDE Lite中，执行以下操作：

1. 导航到Dynamic Media同步文件夹中的`<sync-folder>/_CSS/_OOTB`文件夹（例如，`/content/dam/_CSS/_OOTB`）。
1. 查找有问题的资源的元数据节点（例如，`<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`）。
1. 检查是否存在`dam:scene7*`属性。 如果资产已成功同步和发布，您会看到`dam:scene7FileStatus`设置为&#x200B;**PublishComplete**。
1. 尝试通过连接以下属性和字符串文本的值来直接从Dynamic Media请求图稿：

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
示例： `https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**解决方案**

如果示例资产或查看器预设图稿尚未同步或发布，请重新启动整个复制/同步过程：

1. 导航到CRXDE Lite。
1. 删除`<sync-folder>/_CSS/_OOTB`。
1. 导航到CRX包管理器： `https://localhost:4502/crx/packmgr/`。
1. 在列表中搜索查看器包；它以`cq-dam-scene7-viewers-content`开头。
1. 选择&#x200B;**重新安装**。
1. 在Cloud Service下，导航到Dynamic Media配置页面，然后打开适用于Dynamic Media - S7配置的配置对话框。
1. 不做更改，选择&#x200B;**保存**。
此save操作会再次触发逻辑以创建并同步示例资产、查看器预设CSS和图稿。

### 问题：查看器预设创作中未加载图像预览 {#image-preview-not-loading}

**解决方案**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**。
1. 在左边栏中，导航到位于以下位置的示例内容文件夹：

   `/content/dam/_DMSAMPLE`

1. 删除`_DMSAMPLE`文件夹。
1. 在左边栏中，导航到位于以下位置的预设文件夹：

   `/conf/global/settings/dam/dm/presets/viewer`

1. 删除`viewer`文件夹。
1. 在CRXDE Lite页面的左上角附近，选择&#x200B;**[!UICONTROL 全部保存]**。
1. 在CRXDE Lite页面的左上角，选择&#x200B;**返回主页**&#x200B;图标。
1. 在Cloud Service[&#128279;](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)中重新创建Dynamic Media配置。
