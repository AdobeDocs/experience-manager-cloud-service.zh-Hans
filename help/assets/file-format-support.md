---
title: File formats and MIME types supported by Experience Manager Assets as a Cloud Service
description: File formats and MIME types supported by Experience Manager Assets as a Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b44e6a522b6f2363daa40c6c6f9640ba2fadd35e
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 34%

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager作为Cloud Service，支持任何二进制文件的基本内容管理功能-存储、在线管理元数据、版本控制、上传和下载等，而与其格式无关。 Adobe Experience Manager资产支持各种文件格式，每种产品功能都支持不同格式。

此外，Experience Manager资产还提供扩展支持，用于生成预览和演绎版以及提取元数据和文本以进行全文索引。 此扩展支持是使用资产微 [型服务提供的](asset-microservices-configure-and-use.md)。

使用资产微型服务进行资产转换的亮点包括：

* 由Adobe [应用程序](#adobe-formats) 和服务（包括Adobe Photoshop、Adobe InDesign、Adobe Illustrator、Adobe XD、Adobe Dimension和Adobe Acrobat或PDF）生成的主要Adobe文件格式。
* 关键 [成像文件格式](#image-formats)。
* [Camera Raw文件格式](#camera-raw-formats) ，适用于各种相机，包括Canon、Nikon、Fujifilm、Olympus和其他制造商（由Adobe Camera Raw提供支持）。
* 常见 [文档格式](#document-formats)，包括Microsoft Office和Open文档格式。
* 各种[视频](#video-formats)和[音频](#audio-formats)格式.

下图说明了支持级别。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| * | 查看表下的注释 |
| - | 不适用 |

## Adobe formats {#adobe-formats}

| File format | 缩略图生成 | 全文提取 | 元数据提取 | Width/Height |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ |  | ✓ | ✓ |
| 创意 | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* For [!DNL Adobe InDesign] files (INDD), the size of rendition is determined by the preview embedded in the INDD file. 在(“首选项”>“ [!DNL InDesign] 文&#x200B;**[!UICONTROL 件处理”>“始终使用预览保存文档图像、预览大小]**”)中配置首选项以嵌入较大的再现。

## 图像格式 {#image-formats}

| File format | 缩略图生成 | 元数据提取 | Width/Height | 裁剪 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

## 在 [!DNL Dynamic Media] {#image-support-dynamic-media}

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 传送动态演绎版 | 下载动态演绎版 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD   ‡ | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |

‡合并的图像从PSD文件中提取。 它是由PSD文件生 [!DNL Adobe Photoshop] 成并包含在PSD文件中的图像。 根据设置，合并的图像可能是实际图像，也可能不是实际图像。

不支持以下栅格图像文件格式的子类型 [!DNL Dynamic Media]:

* IDAT区块大小大于100 MB的PNG文件。
* PSB文件。
* 不支持色彩空间不是CMYK、RGB、灰度或位图的PSD文件。 不支持DuoTone、Lab和索引色彩空间。
* 位深度大于16的PSD文件。
* 具有浮点数据的TIFF文件。
* 具有Lab色彩空间的TIFF文件。

## 支持3D格式 {#support-3d-formats}

支持以下3D格式列表。

请参 [阅在Dynamic Media中使用3D资产。](/help/assets/dynamic-media/assets-3d.md)

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 缩略图预览 | 3D预览 | Dynamic Media投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |  |  |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ |  | ✓ |  |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |

## [!DNL Camera RAW] 格式 {#camera-raw-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度／高度 |
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
| MOS | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## 文档格式 {#document-formats}

资产管理功能支持的文档格式如下。

| 文件格式 | 缩略图生成 | 全文提取 | 宽度／高度 | 元数据管理 | [连接的资产](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| OFG | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | - | ✓ | - | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## Document formats in [!DNL Dynamic Media] {#document-support-dynamic-media}

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 传送动态演绎版 | 下载动态演绎版 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| INDD | ✓ | - | - | - | - |

## Video formats {#video-formats}

| File format | 缩略图生成 | 元数据提取 | 宽度／高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ |  | ✓ |
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
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | ✓ | - | ✓ |
| SWF | ✓ | - | ✓ |
| WEBM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Video formats in [!DNL Dynamic Media] for transcoding {#video-dynamic-media-transcoding}

| 视频文件扩展名 | 容器 | 推荐的视频编解码器 | 不支持的视频编解码器 |
|------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| MP4 | MPEG-4 | H264/AVC（所有配置文件） |  |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（矢量动画文件） |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen (MSS2)、Microsoft Photo Story (WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora、VP3、Dirac |  |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Red Raw Video | MJPEG 2000 |  |
| RAM, RM | RealVideo | 不支持 | Real G2 (RV20)、Real 8 (RV30)、Real 10 (RV40) |
| FLAC | Native Flac | 免费的无损音频编解码器 |  |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000编解码器 |  |

## 音频格式 {#audio-formats}

Assets as a Cloud Service provides XMP metadata extraction support for AIF, ASF, M4A, MP3, WAV, and WMA audio formats.

>[!MORELIKETHIS]
>
>* [使用资产微服务进行资产处理](asset-microservices-overview.md)

