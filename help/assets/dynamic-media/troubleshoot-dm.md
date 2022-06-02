---
title: Dynamic Media 疑难解答
description: 使用Dynamic Media时的疑难解答提示。
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: a7152785e8957dcc529d1e2138ffc8c895fa5c29
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 1%

---

# Dynamic Media 疑难解答 {#troubleshooting-dynamic-media-scene-mode}

以下主题介绍Dynamic Media的疑难解答。

## 新Dynamic Media配置 {#new-dm-config}

请参阅 [对新的Dynamic Media配置进行故障诊断](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config).

## 常规（所有资产） {#general-all-assets}

以下是所有资产的一些常规提示和技巧。

### 资产同步状态属性 {#asset-synchronization-status-properties}

可以在CRXDE Lite中审阅以下资产属性，以确认将资产从Adobe Experience Manager成功同步到Dynamic Media:

| **属性** | **示例** | **描述** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 节点已链接到Dynamic Media的常规指示符。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** 或错误文本 | 资产上传到Dynamic Media的状态。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必须填充以生成指向Dynamic Media远程资产的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **成功** 或 **失败：`<error text>`** | 集（旋转集、图像集等）、图像预设、查看器预设、资产的图像映射更新或已编辑图像的同步状态。 |

### 同步日志记录 {#synchronization-logging}

已登录同步错误和问题 `error.log` (Experience Manager服务器目录 `/crx-quickstart/logs/`)。 有足够的日志记录来确定导致大多数问题的根本原因，但您可以将 `com.adobe.cq.dam.ips` 包([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))以收集更多信息。

### 版本控制 {#version-control}

替换现有Dynamic Media资产（名称和位置相同）时，您可以保留两个资产或替换/创建版本：

* 同时保留这两个属性，会为已发布的资产URL创建一个具有唯一名称的资产。 例如， `image.jpg` 是原始资产和 `image1.jpg` 是新上传的资产。

* Dynamic Media不支持创建版本。 新版本会替换交付中的现有资产。

## 图像和集 {#images-and-sets}

如果您在图像和集合方面遇到问题，请参阅以下疑难解答指南。

<table>
 <tbody>
  <tr>
   <td><strong>带有 OS 剪贴板</strong></td>
   <td><strong>如何调试</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>无法在资产详细信息视图中访问复制URL/嵌入按钮</td>
   <td>
    <ol>
     <li><p>转到CRX/DE:</p>
      <ul>
       <li>检查JCR中的预设是否 <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> 定义。 如果您从Experience Manager6.x升级到6.4并选择退出迁移，则此位置适用。 否则，位置为 <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>检查以确保JCR中的资产具有 <code>dam:scene7FileStatus</code><strong> </strong>在元数据下显示为 <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>刷新页面/导航到另一页并返回（必须重新编译边栏JSP）</p> <p>如果这不起作用：</p>
    <ul>
     <li>发布资产。</li>
     <li>重新上传资产并发布它。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>在幻灯片之间切换后，轮播热点会四处移动</td>
   <td><p>检查所有幻灯片的大小是否相同。</p> </td>
   <td><p>仅对轮播使用大小相同的图像。</p> </td>
  </tr>
  <tr>
   <td>图像不使用Dynamic Media查看器预览</td>
   <td><p>检查资产是否包含 <code>dam:scene7File</code> (CRXDE Lite)</p> </td>
   <td><p>检查所有资产是否都已完成处理。</p> </td>
  </tr>
  <tr>
   <td>上传的资产不会显示在资产选择器中</td>
   <td><p>检查资产是否具有属性 <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>检查所有资产是否都已完成处理。</p> </td>
  </tr>
  <tr>
   <td>卡片视图中的横幅显示 <strong>新建</strong> 资产未开始处理时</td>
   <td>检查资产 <code>jcr:content</code> &gt; <code>dam:assetState</code> =if <code>unprocessed</code> 工作流未提取它。</td>
   <td>等待工作流提取资产。</td>
  </tr>
  <tr>
   <td>图像或图像集不显示查看器URL或嵌入代码</td>
   <td>检查查看器预设是否已发布。</td>
   <td><p>转到 <strong>工具</strong> &gt; <strong>资产</strong> &gt; <strong>查看器预设</strong> 并发布查看器预设。</p> </td>
  </tr>
 </tbody>
</table>

## 视频 {#video}

如果您在视频中遇到问题，请参阅以下疑难解答指南。

<table>
 <tbody>
  <tr>
   <td><strong>带有 OS 剪贴板</strong></td>
   <td><strong>如何调试</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>无法预览视频</td>
   <td>
    <ul>
     <li>检查文件夹是否分配了视频配置文件（如果不支持文件格式）。 如果不受支持，则仅显示图像。</li>
     <li>视频配置文件必须包含多个编码预设才能生成AVS集(单个编码被视为MP4文件的视频内容；对于不支持的文件，将其视为与未处理文件相同)。</li>
     <li>通过确认来检查视频是否已完成处理 <code>dam:scene7FileAvs</code> of <code>dam:scene7File</code> 元数据中。</li>
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
     <li>检查是否配置了Dynamic MediaCloud Service。</li>
     <li>检查视频配置文件是否与上传文件夹关联。</li>
    </ul> </td>
   <td>
    <ol>
     <li>检查Cloud Services下的Dynamic Media配置是否正确设置。</li>
     <li>检查文件夹是否包含视频配置文件。 此外，还应检查视频配置文件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>视频处理过长</td>
   <td><p>要确定视频编码是否仍在进行中或是否已进入失败状态，请执行以下操作：</p>
    <ul>
     <li>检查视频状态 <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>缺少视频呈现版本</td>
   <td><p>上传视频时，但没有经过编码的演绎版：</p>
    <ul>
     <li>检查文件夹是否分配了视频配置文件。</li>
     <li>通过确认来检查视频是否已完成处理 <code>dam:scene7FileAvs</code> 元数据中。</li>
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

如果您在查看器方面遇到问题，请参阅以下疑难解答指南。

### 问题：查看器预设未发布 {#viewers-not-published}

**如何调试**

1. 继续执行示例管理器诊断页面： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`.
1. 观察计算值。 正确操作时，您会看到以下内容： `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >配置Dynamic Media云设置后，可能需要大约10分钟才能同步查看器资产。

1. 如果未激活的资产仍保留，请选择 **列出所有未激活的资产** 按钮以查看详细信息。

**解决方案**

1. 在管理工具中导航到查看器预设列表： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. 选择所有查看器预设，然后选择 **发布**.
1. 导航回示例管理器，并观察未激活的资产计数现在为零。

### 问题：查看器预设图稿会从资产详细信息的“预览”或“复制URL/嵌入代码”中返回404 {#viewer-preset-404}

**如何调试**

在CRXDE Lite中，执行以下操作：

1. 导航到 `<sync-folder>/_CSS/_OOTB` 文件夹(例如， `/content/dam/_CSS/_OOTB`)。
1. 查找有问题资产的元数据节点(例如， `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`)。
1. 检查是否存在 `dam:scene7*` 属性。 如果资产已成功同步和发布，您会看到 `dam:scene7FileStatus` 设置为 **PublishComplete**.
1. 尝试通过连接以下属性的值和字符串文字，直接从Dynamic Media请求图稿：

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
示例: 
`https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**解决方案**

如果示例资产或查看器预设图稿未同步或发布，请重新启动整个复制/同步过程：

1. 导航到CRXDE Lite。
1. 删除 `<sync-folder>/_CSS/_OOTB`.
1. 导航到CRX包管理器： `https://localhost:4502/crx/packmgr/`.
1. 在列表中搜索查看器包；开始于 `cq-dam-scene7-viewers-content`.
1. 选择 **重新安装**.
1. 在“Cloud Services”下，导航到Dynamic Media配置页面，然后打开Dynamic Media - S7配置的配置对话框。
1. 不进行更改，请选择 **保存**.
此保存操作会再次触发逻辑，以创建和同步示例资产、查看器预设CSS和图稿。

### 问题：在查看器预设创作中未加载图像预览 {#image-preview-not-loading}

**解决方案**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在左边栏中，导航到位于以下位置的示例内容文件夹：

   `/content/dam/_DMSAMPLE`

1. 删除 `_DMSAMPLE` 文件夹。
1. 在左边栏中，导航到位于以下位置的预设文件夹：

   `/conf/global/settings/dam/dm/presets/viewer`

1. 删除 `viewer` 文件夹。
1. 在CRXDE Lite页面的左上角附近，选择 **[!UICONTROL 全部保存]**.
1. 在CRXDE Lite页面的左上角，选择 **返回主页** 图标。
1. 重新创建 [Dynamic Media在Cloud Services中的配置](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
