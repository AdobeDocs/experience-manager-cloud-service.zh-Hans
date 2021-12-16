---
title: 支持的文件格式和MIME类型
description: 支持的文件格式和MIME类型 [!DNL Experience Manager Assets] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 479cfffd17dcde12bda7d53a7acddfbb46782a8f
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 26%

---

# [!DNL Assets] 支持的文件格式 {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 支持任何二进制文件的基本内容管理功能（存储、在线管理元数据、版本控制、上传和下载等），与其格式无关。 [!DNL Adobe Experience Manager Assets] 支持多种文件格式，每种产品功能都支持不同格式。

此外， [!DNL Experience Manager Assets] 提供了扩展支持，可生成预览和演绎版，以及提取用于全文索引的元数据和文本。 使用 [资产微服务](asset-microservices-configure-and-use.md).

使用资产微服务进行资产转换的功能亮点包括：

* 键 [Adobe文件格式](#adobe-formats) 由Adobe应用程序和服务(包括 [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension]和 [!DNL Adobe Acrobat] 或PDF。
* 键 [成像文件格式](#image-formats).
* [Camera Raw文件格式](#camera-raw-formats) 包括佳能、尼康、富士胶片、奥林匹斯和其他制造商(由Adobe Camera Raw提供动力)在内的各种相机。
* 常用 [文档格式](#document-formats)，包括Microsoft Office和Open Document格式。
* 各种[视频](#video-formats)和[音频](#audio-formats)格式.

下图描述了每种格式的支持级别。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| * | 请参阅表下的注释 |
| - | 不适用 |

## Adobe格式 {#adobe-formats}

| 文件格式 | 缩略图生成 | 全文提取 | 元数据提取 | 宽度/高度 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| 构思 | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\*对于 [!DNL Adobe InDesign] 文件(INDD)，则再现的大小由INDD文件中嵌入的预览决定。 在中配置首选项 [!DNL InDesign] (**[!UICONTROL 首选项>文件处理>始终保存带有文档的预览图像、预览大小]**)以嵌入较大的演绎版。

## 图像格式 {#image-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度/高度 | 裁剪 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |

## 3D格式 {#support-3d-formats}

支持以下3D格式。

另请参阅 [在Dynamic Media中使用3D资产](/help/assets/dynamic-media/assets-3d.md).

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 缩略图预览 | 3D预览 | Dynamic Media交付 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## [!DNL Camera RAW] 格式 {#camera-raw-formats}

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
| 探地雷达 | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| 奥夫 | ✓ | ✓ | ✓ |
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

| 文件格式 | 缩略图生成 | 全文提取 | 宽度/高度 | 元数据管理 | [连接的资产](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| DOC | - | - | - | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

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

## 支持的音频和视频转录输入格式 {#audio-video-transcription-formats}

* FLV（带H.264和AAC编解码器）(.flv)
* MXF(.mxf)
* MPEG2-PS、MPEG2-TS、3GP(.ts、.ps、.3gp、.3gpp、.mpg)
* Windows Media视频(WMV)/ASF(.wmv、.asf)
* AVI（未压缩8位/10位）(.avi)
* MP4(.mp4、.m4a、.m4v)
* Microsoft数字视频录制(DVR-MS)(.dvr-ms)
* 马特罗斯卡/WebM(.mkv)
* WAVE/WAV(.wav)
* QuickTime(.mov)

## 提示和限制 {#limitations-and-tips}

* 目前，元数据提取的文件大小限制约为15 GB。 上传超大型资产时，有时元数据提取操作会失败。

## Dynamic Media — 支持的用于转码的输入视频格式 {#video-dynamic-media-transcoding}

| 视频文件扩展名 | 容器 | 推荐的视频编解码器 | 不支持的视频编解码器 |
| --- | --- | --- | --- |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft Video 1 (MS-CRAM) |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（矢量动画文件） |
| M4V | Apple iTunes | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| MP4 | MPEG-4 | H264/AVC（所有配置文件） | - |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| MXF ‡ | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| OGV、OGG | Ogg | Theora、VP3、Dirac | - |
| WebM | WebM | Google VP8 | - |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen (MSS2)、Microsoft Photo Story (WVP2) |

‡尚不支持在Dynamic Media中将此视频格式用于交互式视频，或在Experience Manager Assets中将其与“注释”一起使用。

## Dynamic Media — 支持的文档格式 {#document-support-dynamic-media}

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 传送动态演绎版 | 下载动态演绎版 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| 人工智能 | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |

## Dynamic Media — 支持的栅格图像格式 {#image-support-dynamic-media}

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 传送动态演绎版 | 下载动态演绎版 | 设置支持此格式的类型 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- | ---------------------------------- |
| BMP | ✓ | - | - | - | - | [图像](/help/assets/dynamic-media/image-sets.md), [混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)和 [旋转](/help/assets/dynamic-media/spin-sets.md) |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/dynamic-media/image-sets.md), [混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)和 [旋转](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | - | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/dynamic-media/image-sets.md), [混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)和 [旋转](/help/assets/dynamic-media/spin-sets.md) |
| PSD   ‡ | ✓ | - | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [图像](/help/assets/dynamic-media/image-sets.md), [混合媒体](/help/assets/dynamic-media/mixed-media-sets.md)和 [旋转](/help/assets/dynamic-media/spin-sets.md) |

从PSD文件中提取合并的图像。 它是由 [!DNL Adobe Photoshop] 和包含在PSD文件中。 根据设置，合并的图像可能是实际的图像，也可能不是实际的图像。

## Dynamic Media — 不支持的栅格图像格式 {#unsupported-raster-image-formats-dm}

以下栅格图像文件格式的子类型： *not* 支持 [!DNL Dynamic Media]:

* IDAT区块大于100 MB的PNG文件。
* PSB文件。
* 不支持具有CMYK、RGB、灰度或位图以外的色彩空间的PSD文件。 不支持DuoTone、Lab和索引色彩空间。
* PSD位深度大于16的文件。
* TIFF具有浮点数据的文件。
* TIFF具有Lab色彩空间的文件。

## Dynamic Media — 支持的3D文件格式 {#support-3d-formats-dynamic-media}

另请参阅 [支持的3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary | 将材料和纹理作为单个资产包含在内。 |
| OBJ | WaveFront 3D对象文件 | application/x-tgif |  |
| STL | 立体成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | *仅支持摄取；无法查看或进行交互。* USDZ是一种专有的3D格式，Safari或iOS可在本地查看。 |

>[!MORELIKETHIS]
>
>* [使用资产微服务进行资产处理](asset-microservices-overview.md)
>* [支持基于文本的资产智能标记的文件格式](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

