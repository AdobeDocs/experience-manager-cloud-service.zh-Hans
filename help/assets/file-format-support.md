---
title: 支持的文件格式和MIME类型
description: ' [!DNL Experience Manager Assets] as a [!DNL Cloud Service]支持的文件格式和MIME类型。'
contentOwner: AG
feature: Asset Management, Renditions
role: User, Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 0129bf13301a208b777b61f65623222cdf2b4b18
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 9%

---

# [!DNL Assets]支持的文件格式 {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service]支持任何二进制文件的基本内容管理功能 — 存储、联机管理元数据、版本控制、上载和下载等，而不依赖于其格式。 [!DNL Adobe Experience Manager Assets]支持多种文件格式，每种产品功能支持的格式也各不相同。

此外，[!DNL Experience Manager Assets]还提供了扩展支持，用于生成预览和演绎版，以及提取元数据和文本以进行全文索引。 此扩展支持是使用[资产微服务](asset-microservices-configure-and-use.md)提供的。

使用资产微服务的资产转换功能亮点包括：

* Adobe应用程序和服务生成的密钥[Adobe文件格式](#adobe-formats)，包括[!DNL Adobe Photoshop]、[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe XD]、[!DNL Adobe Dimension]和[!DNL Adobe Acrobat]或PDF。
* 密钥[映像文件格式](#image-formats)。
* 适用于各种相机的[Camera Raw文件格式](#camera-raw-formats)，这些相机包括Canon、Nikon、Fujifilm、Olympus和其他制造商(由Adobe Camera Raw提供支持)。
* 常用的[文档格式](#document-formats)，包括Microsoft®Office和Open Document格式。
* [视频](#video-formats)和[音频](#audio-formats)格式范围广泛。

以下图例描述了每种格式的支持级别。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| * | 请参阅表下方的说明 |
| - | 不适用 |

>[!IMPORTANT]
>
>[!DNL Adobe Experience Manager Assets]仅支持本文中列出的文件格式。
>&#x200B;>某些功能可能与其他格式配合使用，但这些格式不受正式支持。 结果可能不一致，并且功能可能无法按预期工作。
>&#x200B;>要确保一致和可靠的结果，请仅使用支持的格式。

## Adobe格式 {#adobe-formats}

| 文件格式 | 缩略图生成 | 全文提取 | 元数据提取 | 宽度/高度 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| 人工智能 | ✓ | - | ✓ | ✓ |
| 拼贴 | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| SBSAR | ✓ | - | ✓ | ✓ |
| 构思 | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| 原始 | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\*对于[!DNL Adobe InDesign]文件(INDD)，演绎版的大小由INDD文件中嵌入的预览决定。 在[!DNL InDesign]中配置首选项（**[!UICONTROL 首选项>文件处理>始终将预览图像与文档一起保存，预览大小]**），以便嵌入更大的呈现版本。

## 图像格式 {#image-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度/高度 | 裁剪 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI™ | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |
| WebP | ✓ | ✓ | ✓ | ✓ |

## 三维格式 {#support-3d-formats}

支持以下3D格式。

另请参阅[在Dynamic Media中使用3D资产](/help/assets/dynamic-media/assets-3d.md)。

| 格式化 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 缩略图预览 | 3D预览 | Dynamic Media投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| 对象 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| FBX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| 3DS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| 美元z | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| SBSAR | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |

## [!DNL Camera Raw]格式 {#camera-raw-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度/高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ |
| 月 | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| 原始 | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## 文档格式 {#document-formats}

资产管理功能支持的文档格式如下。

| 文件格式 | 缩略图生成 | 全文提取 | 宽度/高度 | 元数据管理 | [连接的资产](use-assets-across-connected-assets-instances.md) | 完整文档预览 |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |--------|
| DOC | - | - | - | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| ePub | - | ✓ | - | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ | - |
| ODF | ✓ | ✓ | ✓ | - | - | - |
| ODM | ✓ | ✓ | ✓ | - | - | - |
| ODP | ✓ | ✓ | ✓ | - | - | - |
| ODS | ✓ | ✓ | ✓ | - | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| OFG | ✓ | ✓ | ✓ | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - | - |
| RTF | - | ✓ | - | ✓ | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - | - |

## 视频格式 {#video-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度/高度 | 预览 | 输出 |
| ----------- | -------------------- | ------------------- | ------------ | ------- | ------- |
| 3G2 | - | ✓ | - | - | - |
| 3GP | - | ✓ | - | - | - |
| AVI | ✓ | ✓ | ✓ | ✓ | - |
| DIVX | ✓ | - | ✓ | ✓ | - |
| F4V | ✓ | ✓ | ✓ | ✓ | - |
| FLV | ✓ | ✓ | ✓ | ✓ | - |
| M2T | ✓ | - | ✓ | ✓ | - |
| M2TS | ✓ | - | ✓ | ✓ | - |
| M2V | ✓ | - | ✓ | ✓ | - |
| M4V | ✓ | ✓ | ✓ | ✓ | - |
| MKV | ✓ | - | ✓ | ✓ | - |
| MOV | ✓ | ✓ | ✓ | ✓ | - |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | - |
| MPG | ✓ | ✓ | ✓ | ✓ | - |
| MTS | ✓ | - | ✓ | ✓ | - |
| MXF | ✓ | - | ✓ | ✓ | - |
| OGV | ✓ | - | ✓ | ✓ | - |
| QT | ✓ | - | ✓ | ✓ | - |
| R3D | - | ✓ | ✓ | ✓ | - |
| SWF | ✓ | - | ✓ | ✓ | - |
| WebM | ✓ | - | ✓ | ✓ | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | - |

## 音频格式 {#audio-formats}

[!DNL Assets] as a [!DNL Cloud Service]提供对AIF、ASF、M4A、MP3、WAV和WMA音频格式的XMP元数据提取支持。

## 音频和视频转录支持的输入格式 {#audio-video-transcription-formats}

* FLV（带有H.264和AAC编解码器）(.flv)
* MXF (.mxf)
* MPEG2-PS、MPEG2-TS、3GP(.ts、.ps、.3gp、.3gpp、.mpg)
* Windows Media Video (WMV)/ASF (.wmv、.asf)
* AVI（未压缩8位/10位）(.avi)
* MP4 (.mp4、.m4a、.m4v)
* Microsoft®数字视频录制(DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## 提示和限制 {#limitations-and-tips}

* 目前，元数据提取的文件大小限制约为15 GB。 上传大型资源时，元数据提取操作有时会失败。

## Dynamic Media — 支持的用于转码的输入视频格式 {#video-dynamic-media-transcoding}

| 视频文件扩展名 | 容器 | 推荐的视频编解码器 | 不支持的视频编解码器 |
| --- | --- | --- | --- |
| AVI | A/V交错 | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft®视频1(MS-CRAM) |
| FLV， F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（矢量动画文件） |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV， QT | Apple QuickTime | H264/AVC、Apple ProRes422和HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple中级，Apple动画 |
| MP4 | MPEG-4 | H264/AVC（所有配置文件） | − |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | − |
| MXF‡ | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | − |
| OGV， OGG | OGG | 狄拉克副总裁Theora | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting (G2M2、G2M3、G2M4) | Microsoft® Screen (MSS2)、Microsoft® Photo Story (WVP2) |

‡尚不支持将此视频格式与Dynamic Media中的交互式视频一起使用，也不支持将其与Experience Manager Assets中的批注一起使用。

## Dynamic Media — 支持的文档格式 {#document-support-dynamic-media}

| 格式化 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 投放动态演绎版 | 下载动态演绎版 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| 人工智能 | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF（请参阅下面的注释） | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>对于安全PDF，仅支持上传。

## Dynamic Media — 支持的栅格图像格式 {#image-support-dynamic-media}

| 格式化 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 投放动态演绎版 | 下载动态演绎版 | 设置支持此格式的类型 |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [图像](/help/assets/dynamic-media/image-sets.md)、[混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)和[旋转](/help/assets/dynamic-media/spin-sets.md) |
| [EPS](/help/assets/dynamic-media/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/dynamic-media/image-sets.md)、[混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)和[旋转](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/dynamic-media/image-sets.md)、[混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)和[旋转](/help/assets/dynamic-media/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/dynamic-media/image-sets.md)、[混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)和[旋转](/help/assets/dynamic-media/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |

<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡将从PSD文件中提取合并的图像。 它是由[!DNL Adobe Photoshop]生成并包含在PSD文件中的图像。 根据设置，合并的图像不一定是实际图像。

## Dynamic Media — 不支持的栅格图像格式 {#unsupported-raster-image-formats-dm}

*不支持*&#x200B;的[!DNL Dynamic Media]光栅图像文件格式的以下子类型：

* IDAT区块大小大于100 MB的PNG文件。
* psb文件。
* 不支持色彩空间不是CMYK、RGB、灰度或位图的PSD文件。 不支持DuoTone、Lab和Indexed色彩空间。
* 位深度大于16的PSD文件。
* 包含浮点数据的TIFF文件。
* 具有Lab色彩空间的TIFF文件。

## Dynamic Media — 支持的3D文件格式 {#support-3d-formats-dynamic-media}

另请参阅[支持的3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary | 将材料和纹理作为单个资产包含在内。 |
| 对象 | WaveFront 3D对象文件 | application/x-tgif | |
| STL | 立体成形 | application/vnd.ms-pki.stl | |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | *支持摄取和缩略图生成；尚不支持3D预览。* USDZ是3D格式，可由Safari或iOS以本机方式查看。 |

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
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
>* [使用资源微服务处理资源](asset-microservices-overview.md)。
>* [基于文本的资源的智能标记支持的文件格式](/help/assets/smart-tags.md#smart-tags-supported-file-formats)
