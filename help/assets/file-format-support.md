---
title: 支持的文件格式和MIME类型
description: 支持的文件格式和MIME类型 [!DNL Experience Manager Assets] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: d00e1f49438ad36339a09f8914496faeda3d4de6
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 10%

---

# [!DNL Assets] 支持的文件格式 {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 支持任何二进制文件的基本内容管理功能 — 存储、在线管理元数据、版本控制、上传和下载等，与文件格式无关。 [!DNL Adobe Experience Manager Assets] 支持广泛的文件格式，并且每种产品功能支持的格式也各不相同。

此外， [!DNL Experience Manager Assets] 提供扩展支持以生成预览和演绎版，并提取元数据和文本以进行全文索引。 此扩展支持通过以下方式提供 [资源微服务](asset-microservices-configure-and-use.md).

使用资产微服务进行资产转换的功能亮点包括：

* 键 [Adobe文件格式](#adobe-formats) 由Adobe应用程序和服务生成，包括 [!DNL Adobe Photoshop]， [!DNL Adobe InDesign]， [!DNL Adobe Illustrator]， [!DNL Adobe XD]， [!DNL Adobe Dimension]、和 [!DNL Adobe Acrobat] 或PDF。
* 键 [图像文件格式](#image-formats).
* [Camera Raw文件格式](#camera-raw-formats) 适用于各种相机，包括佳能、尼康、富士胶片、奥林巴斯和其他厂商(由Adobe Camera Raw提供支持)。
* 公共 [文档格式](#document-formats)，包括Microsoft®Office和Open Document格式。
* 各种[视频](#video-formats)和[音频](#audio-formats)格式.

以下图例描述了每种格式的支持级别。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| * | 请参阅表格下方的说明 |
| - | 不适用 |

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

\*表示 [!DNL Adobe InDesign] 文件(INDD)，格式副本的大小由嵌入到INDD文件中的预览决定。 在中配置首选项 [!DNL InDesign] (**[!UICONTROL 首选项>文件处理>始终保存预览图像和文档，预览大小]**)以便嵌入更大的演绎版。

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

## 3D格式 {#support-3d-formats}

支持以下3D格式。

另请参阅 [在Dynamic Media中使用3D资源](/help/assets/dynamic-media/assets-3d.md).

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 缩略图预览 | 3D预览 | Dynamic Media投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| 对象 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| FBX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| 3DS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| 美元z | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| SBSAR | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |

## [!DNL Camera Raw] 格式 {#camera-raw-formats}

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

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度/高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ | - | ✓ |
| F4V | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ |
| M2T | ✓ | - | ✓ |
| M2TS | ✓ | - | ✓ |
| M2V | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ |
| MKV | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ |
| MTS | ✓ | - | ✓ |
| MXF | ✓ | - | ✓ |
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | - | ✓ | ✓ |
| SWF | ✓ | - | ✓ |
| WebM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## 音频格式 {#audio-formats}

[!DNL Assets] as a [!DNL Cloud Service] 为AIF、ASF、M4A、MP3、WAV和WMA音频格式提供XMP元数据提取支持。

## 音频和视频转录支持的输入格式 {#audio-video-transcription-formats}

* FLV（带有H.264和AAC编解码器）(.flv)
* MXF (.mxf)
* MPEG2-PS、MPEG2-TS、3GP(.ts、.ps、.3gp、.3gpp、.mpg)
* Windows Media Video (WMV)/ASF (.wmv、.asf)
* AVI（未压缩8位/10位） (.avi)
* MP4 (.mp4、.m4a、.m4v)
* Microsoft®数字视频录制(DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## 提示和限制 {#limitations-and-tips}

* 目前，元数据提取的文件大小限制约为15 GB。 上传大型资产时，有时元数据提取操作失败。

## Dynamic Media — 支持的用于转码的输入视频格式 {#video-dynamic-media-transcoding}

| 视频文件扩展名 | 容器 | 推荐的视频编解码器 | 不支持的视频编解码器 |
| --- | --- | --- | --- |
| AVI | A/V交错 | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft®视频1 (MS-CRAM) |
| FLV、F4V | AdobeFlash | H264/AVC、Flix VP6、H263、Sorenson | SWF（矢量动画文件） |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422和HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple中级， Apple动画 |
| MP4 | MPEG-4 | H264/AVC（所有配置文件） | − |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | − |
| MXF ‡ | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | − |
| OGV， OGG | OGG | 狄拉克副总裁Theora | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting (G2M2、G2M3、G2M4) | Microsoft®屏幕(MSS2)、Microsoft®照片故事(WVP2) |

‡尚不支持将此视频格式用于Dynamic Media中的交互式视频，也不支持将其用于Experience Manager Assets中的注释。

## Dynamic Media — 支持的文档格式 {#document-support-dynamic-media}

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 投放动态演绎版 | 下载动态演绎版 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| 人工智能 | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF（请参阅下面的注释） | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>对于安全PDF，仅支持上传。

## Dynamic Media — 支持的栅格图像格式 {#image-support-dynamic-media}

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 投放动态演绎版 | 下载动态演绎版 | 设置支持此格式的类型 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- | ---------------------------------- |
| BMP | ✓ | - | - | - | - | [图像](/help/assets/dynamic-media/image-sets.md)， [混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)、和 [旋转](/help/assets/dynamic-media/spin-sets.md) |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/dynamic-media/image-sets.md)， [混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)、和 [旋转](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | - | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/dynamic-media/image-sets.md)， [混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)、和 [旋转](/help/assets/dynamic-media/spin-sets.md) |
| PSD   ‡ | ✓ | - | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/dynamic-media/image-sets.md)， [混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)、和 [旋转](/help/assets/dynamic-media/spin-sets.md) |

‡将从PSD文件中提取合并的图像。 它是由生成的图像 [!DNL Adobe Photoshop] 和包含在PSD文件中。 根据设置，合并的图像不一定是实际图像。

## Dynamic Media — 不支持的栅格图像格式 {#unsupported-raster-image-formats-dm}

栅格图像文件格式的以下子类型 *非* 在中支持 [!DNL Dynamic Media]：

* IDAT区块大小大于100 MB的PNG文件。
* psb文件。
* 不支持使用CMYK、RGB、灰度或位图以外的PSD空间的颜色文件。 不支持DuoTone、Lab和索引色域。
* PSD位深度大于16的文件。
* TIFF包含浮点数据的文件。
* TIFF具有Lab色彩空间的文件。

## Dynamic Media — 支持的3D文件格式 {#support-3d-formats-dynamic-media}

另请参阅 [支持的3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary | 将材料和纹理作为单个资产包含在内。 |
| 对象 | WaveFront 3D对象文件 | application/x-tgif | |
| STL | 立体光刻 | application/vnd.ms-pki.stl | |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | *支持摄取和缩略图生成；尚不支持3D预览。* USDZ是一种3D格式，可供Safari或iOS本机查看。 |

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

>[!MORELIKETHIS]
>
>* [使用资源微服务处理资源](asset-microservices-overview.md)
>* [基于文本的资源智能标记支持的文件格式](/help/assets/smart-tags.md#smart-tags-supported-file-formats)
