---
title: 支持的文件格式和MIME类型
description: ' [!DNL Experience Manager Assets] 作为 [!DNL Cloud Service]支持的文件格式和MIME类型。'
contentOwner: AG
feature: 资产管理，演绎版
role: 业务从业者，管理员
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 34%

---


# [!DNL Assets] 支持的文件格式  {#supported-file-formats}

[!DNL Adobe Experience Manager] 作为支 [!DNL Cloud Service] 持任何二进制文件的基本内容管理功能(存储、在线管理元数据、版本控制、上传和下载等)，与其格式无关。[!DNL Adobe Experience Manager Assets] 支持各种文件格式，每种产品功能都支持不同格式。

此外，[!DNL Experience Manager Assets]还提供扩展支持，用于生成预览和再现以及提取元数据和文本以实现全文索引。 此扩展支持是使用[asset microservices](asset-microservices-configure-and-use.md)提供的。

使用资产微型服务进行资产转换的亮点包括：

* 键[由Adobe应用程序和服务生成的Adobe文件格式](#adobe-formats)，包括[!DNL Adobe Photoshop]、[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe XD]、[!DNL Adobe Dimension]和[!DNL Adobe Acrobat]或PDF。
* 键[映像文件格式](#image-formats)。
* [Camera Raw文](#camera-raw-formats) 件格式，适用于各种相机，包括Canon、Nikon、Fujifilm、Olympus和其他制造商(由Adobe Camera Raw提供支持)。
* 常见[文档格式](#document-formats)，包括Microsoft Office和Open文档格式。
* 各种[视频](#video-formats)和[音频](#audio-formats)格式.

下图例描述了每种格式的支持级别。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| * | 查看表下的注释 |
| - | 不适用 |

## Adobe格式{#adobe-formats}

| 文件格式 | 缩略图生成 | 全文提取 | 元数据提取 | 宽度/高度 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| 创意 | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\*对于[!DNL Adobe InDesign]文件(INDD)，再现的大小由嵌入在INDD文件中的预览决定。 在[!DNL InDesign](**[!UICONTROL “首选项”>“文件处理”>“始终使用文档保存预览图像”、“预览大小”]**)中配置首选项，以嵌入较大的再现。

## 图像格式{#image-formats}

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

## [!DNL Dynamic Media] {#image-support-dynamic-media}中的图像格式

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 传送动态演绎版 | 下载动态演绎版 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| BMP | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PSD   ‡ | ✓ | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

‡合并的图像会从PSD文件中提取。 它是由[!DNL Adobe Photoshop]生成并包含在PSD文件中的图像。 根据设置，合并的图像可能是实际图像，也可能不是实际图像。

[!DNL Dynamic Media]中不支持的栅格图像文件格式的以下子类型：

* IDAT区块大小大于100 MB的PNG文件。
* PSB文件。
* 不支持具有CMYK、RGB、灰度或位图以外的色彩空间的PSD文件。 不支持DuoTone、Lab和索引色彩空间。
* 位深度大于16的PSD文件。
* 具有浮点数据的TIFF文件。
* 具有Lab色彩空间的TIFF文件。

## 3D格式{#support-3d-formats}

支持以下3D格式。

另请参阅[在Dynamic Media中使用3D资源。](/help/assets/dynamic-media/assets-3d.md)

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 缩略图预览 | 3D预览 | Dynamic Media 投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## [!DNL Camera RAW] 格式  {#camera-raw-formats}

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

## 文档格式{#document-formats}

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
| TXT | - | ✓ | - | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## [!DNL Dynamic Media] {#document-support-dynamic-media}中的文档格式

| 格式 | 上传（输入格式） | 创建图像预设（输出格式） | 预览动态演绎版 | 传送动态演绎版 | 下载动态演绎版 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |

## 视频格式{#video-formats}

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

## 用于转码{#video-dynamic-media-transcoding}的[!DNL Dynamic Media]中的视频格式

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
| OGV、OGG | Ogg | Theora、VP3、Dirac | - |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D， RM | Red Raw Video | MJPEG 2000 | - |
| RAM、RM | RealVideo | 不支持 | Real G2 (RV20)、Real 8 (RV30)、Real 10 (RV40) |
| FLAC | Native Flac | 自由无损音频编解码器 | - |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000编解码器 | - |

## 音频格式{#audio-formats}

[!DNL Assets] as为 [!DNL Cloud Service] AIF、ASF、M4A、MP3、WAV和WMA音频格式提供XMP元提取支持。

## 提示和限制{#limitations-and-tips}

* 目前，元数据提取的文件大小限制约为10 GB。 上传超大型资产时，有时元数据提取操作会失败。

>[!MORELIKETHIS]
>
>* [使用资产微服务进行资产处理](asset-microservices-overview.md)
>* [支持的文件格式，用于智能标记基于文本的资产](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

