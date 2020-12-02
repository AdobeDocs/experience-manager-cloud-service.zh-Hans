---
title: 支持的文件格式和MIME类型
description: ' [!DNL Experience Manager Assets] 作为Cloud Service支持的文件格式和MIME类型。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7e5ea5ccf0110d1fb55449c9c1933aff6aba0065
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 35%

---


# [!DNL Assets] 支持的文件格式  {#supported-file-formats}

[!DNL Adobe Experience Manager] 作为Cloud Service，它支持任何二进制文件的基本内容管理功能-存储、在线管理元数据、版本控制、上传和下载等，而与其格式无关。[!DNL Adobe Experience Manager Assets] 支持各种文件格式，每种产品功能都支持不同格式。

此外，[!DNL Experience Manager Assets]还提供扩展支持，用于生成预览和再现以及提取元数据和文本以进行全文索引。 此扩展支持是使用[资产微服务](asset-microservices-configure-and-use.md)提供的。

使用资产微型服务进行资产转换的亮点包括：

* 密钥[由Adobe应用程序和服务生成的Adobe文件格式](#adobe-formats)，包括[!DNL Adobe Photoshop]、[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe XD]、[!DNL Adobe Dimension]和[!DNL Adobe Acrobat]或PDF。
* 键[成像文件格式](#image-formats)。
* [Camera Raw文](#camera-raw-formats) 件格式，适用于各种相机，包括Canon、Nikon、Fujifilm、Olympus和其他制造商(由Adobe Camera Raw提供支持)。
* 常见[文档格式](#document-formats)，包括Microsoft Office和Open文档格式。
* 各种[视频](#video-formats)和[音频](#audio-formats)格式.

下图说明了支持级别。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| 选定 | 支持 |
| * | 查看表下的注释 |
| - | 不适用 |

## Adobe格式{#adobe-formats}

| 文件格式 | 缩略图生成 | 全文提取 | 元数据提取 | 宽度／高度 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | 选定 | - | 选定 | 选定 |
| COLLAGE | - | - | 选定 | - |
| DN | 选定 | - | 选定 | 选定 |
| 创意 | - | - | 选定 | - |
| INDD | 选定 | - | 选定 | * |
| INDT | - | - | 选定 | - |
| PDF | 选定 | 选定 | 选定 | 选定 |
| PROTO | - | - | 选定 | - |
| PSB | 选定 | - | 选定 | 选定 |
| PSD | 选定 | - | 选定 | 选定 |
| XD | 选定 | - | 选定 | 选定 |

\*对于[!DNL Adobe InDesign]文件(INDD)，再现的大小由嵌入在INDD文件中的预览决定。 在[!DNL InDesign](**[!UICONTROL 首选项>文件处理>始终使用文档保存预览图像，预览大小]**)中配置首选项以嵌入较大的再现。

## 图像格式{#image-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度／高度 | 裁剪 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | 选定 | - | 选定 | 选定 |
| EPS | - | 选定 | - | - |
| GIF | 选定 | 选定 | 选定 | 选定 |
| JPEG | 选定 | 选定 | 选定 | 选定 |
| PNG | 选定 | 选定 | 选定 | 选定 |
| TIFF | 选定 | 选定 | 选定 | - |
| SVG | 选定 | - | 选定 | 选定 |
| SGI | 选定 | 选定 | 选定 | 选定 |
| RGB | 选定 | 选定 | 选定 | 选定 |
| RGBA | 选定 | 选定 | 选定 | 选定 |

## [!DNL Dynamic Media] {#image-support-dynamic-media}中的图像格式

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 传送动态演绎版 | 下载动态演绎版 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | 选定 | 选定 | 选定 | 选定 | 选定 |
| GIF | 选定 | 选定 | 选定 | 选定 | 选定 |
| TIFF | 选定 | 选定 | 选定 | 选定 | 选定 |
| JPEG | 选定 | 选定 | 选定 | 选定 | 选定 |
| BMP | 选定 | - | - | - | - |
| PSD   ‡ | 选定 | - | - | - | - |
| EPS | 选定 | 选定 | 选定 | 选定 | 选定 |
| PICT | 选定 | - | - | - | - |

‡合并的图像从PSD文件中提取。 它是由[!DNL Adobe Photoshop]生成并包含在PSD文件中的图像。 根据设置，合并的图像可能是实际图像，也可能不是实际图像。

[!DNL Dynamic Media]中不支持的以下栅格图像文件格式子类型：

* IDAT区块大小大于100 MB的PNG文件。
* PSB文件。
* 不支持色彩空间不是CMYK、RGB、灰度或位图的PSD文件。 不支持DuoTone、Lab和索引色彩空间。
* 位深度大于16的PSD文件。
* 具有浮点数据的TIFF文件。
* 具有Lab色彩空间的TIFF文件。

## 3D格式{#support-3d-formats}

支持以下3D格式列表。

另请参阅[在Dynamic Media中使用3D资产。](/help/assets/dynamic-media/assets-3d.md)

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 缩略图预览 | 3D预览 | 动态媒体投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | 选定 | 选定 | 选定 | - | 选定 | 选定 | - | - |
| gLB | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 | 选定 |
| gLTF | 选定 | 选定 | 选定 | - | 选定 | - | 选定 | - |
| OBJ | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 | 选定 |
| STL | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 | 选定 |
| USDz | 选定 | 选定 | 选定 | 选定 | 选定 | - | - | 选定 |

## [!DNL Camera RAW] 格式  {#camera-raw-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度／高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | 选定 | 选定 | 选定 |
| ARW | 选定 | 选定 | 选定 |
| CR2 | 选定 | 选定 | 选定 |
| CR3 | 选定 | 选定 | 选定 |
| CRW | 选定 | 选定 | 选定 |
| DCR | 选定 | 选定 | 选定 |
| DNG | 选定 | 选定 | 选定 |
| ERF | 选定 | 选定 | 选定 |
| FFF | 选定 | 选定 | 选定 |
| GPR | 选定 | 选定 | 选定 |
| IIQ | 选定 | 选定 | 选定 |
| KDC | 选定 | 选定 | 选定 |
| MEF | 选定 | 选定 | 选定 |
| MFW | 选定 | 选定 | 选定 |
| MOS | 选定 | 选定 | 选定 |
| MRW | 选定 | 选定 | 选定 |
| NEF | 选定 | 选定 | 选定 |
| NRW | 选定 | 选定 | 选定 |
| ORF | 选定 | 选定 | 选定 |
| PEF | 选定 | 选定 | 选定 |
| RAF | 选定 | 选定 | 选定 |
| RAW | 选定 | 选定 | 选定 |
| RW2 | 选定 | 选定 | 选定 |
| RWL | 选定 | 选定 | 选定 |
| SRF | 选定 | 选定 | 选定 |
| SRW | 选定 | 选定 | 选定 |
| X3F | 选定 | 选定 | 选定 |

## 文档格式{#document-formats}

资产管理功能支持的文档格式如下。

| 文件格式 | 缩略图生成 | 全文提取 | 宽度／高度 | 元数据管理 | [连接的资产](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | 选定 | 选定 | 选定 | 选定 | 选定 |
| DOCX | 选定 | 选定 | 选定 | 选定 | 选定 |
| DOC | - | - | - | 选定 | 选定 |
| PPTX | 选定 | 选定 | 选定 | 选定 | 选定 |
| PPT | - | - | - | 选定 | 选定 |
| XLSX | 选定 | 选定 | 选定 | 选定 | 选定 |
| XLS | - | - | - | 选定 | 选定 |
| ODF | 选定 | 选定 | 选定 | - | - |
| OFG | 选定 | 选定 | 选定 | - | - |
| ODM | 选定 | 选定 | 选定 | - | - |
| ODP | 选定 | 选定 | 选定 | - | - |
| ODS | 选定 | 选定 | 选定 | - | - |
| ODT | 选定 | 选定 | 选定 | 选定 | 选定 |
| EPUB | - | 选定 | - | - | - |
| HTML | - | 选定 | - | 选定 | 选定 |
| PS | - | - | 选定 | - | - |
| RTF | - | 选定 | - | 选定 | 选定 |
| TXT | - | 选定 | - | 选定 | 选定 |
| XML | - | 选定 | - | - | - |

## [!DNL Dynamic Media] {#document-support-dynamic-media}中的文档格式

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 传送动态演绎版 | 下载动态演绎版 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | 选定 | - | - | - | - |
| PDF | 选定 | 选定 | 选定 | 选定 | 选定 |
| INDD | 选定 | - | - | - | - |

## 视频格式{#video-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度／高度 |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | 选定 | - |
| 3GP | - | 选定 | - |
| AVI | 选定 | 选定 | 选定 |
| DIVX | 选定 | - | 选定 |
| F4V | 选定 | 选定 | 选定 |
| FLV | 选定 | 选定 | 选定 |
| M2T | 选定 | - | 选定 |
| M2TS | 选定 | - | 选定 |
| M2V | 选定 | - | 选定 |
| M4V | 选定 | 选定 | 选定 |
| MKV | 选定 | - | 选定 |
| MOV | 选定 | 选定 | 选定 |
| MP4 | 选定 | 选定 | 选定 |
| MPEG | 选定 | 选定 | 选定 |
| MPG | 选定 | 选定 | 选定 |
| MTS | 选定 | - | 选定 |
| OGV | 选定 | - | 选定 |
| QT | 选定 | - | 选定 |
| R3D | - | 选定 | 选定 |
| SWF | 选定 | - | 选定 |
| WebM | 选定 | - | 选定 |
| WMV | 选定 | 选定 | 选定 |

## [!DNL Dynamic Media]中用于转码{#video-dynamic-media-transcoding}的视频格式

| 视频文件扩展名 | 容器 | 推荐的视频编解码器 | 不支持的视频编解码器 |
|------------------------|--------------------|--------|-------|
| MP4 | MPEG-4 | H264/AVC（所有配置文件） | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（矢量动画文件） |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen (MSS2)、Microsoft Photo Story (WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV, OGG | Ogg | Theora、VP3、Dirac | - |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D, RM | Red Raw Video | MJPEG 2000 | - |
| RAM, RM | RealVideo | 不支持 | Real G2 (RV20)、Real 8 (RV30)、Real 10 (RV40) |
| FLAC | Native Flac | 免费的无损音频编解码器 | - |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000编解码器 | - |

## 音频格式{#audio-formats}

[!DNL Assets] 作为Cloud Service，它为AIF、ASF、M4A、MP3、WAV和WMA音频格式提供XMP元数据提取支持。

>[!MORELIKETHIS]
>
>* [使用资产微服务进行资产处理](asset-microservices-overview.md)

