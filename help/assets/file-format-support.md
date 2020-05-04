---
title: Experience Manager资产作为云服务支持的文件格式和MIME类型
description: Experience Manager资产作为云服务支持的文件格式和MIME类型。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2e73a9bba91f15702bdeb1d57e87b688360661bd

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager作为一项云服务，支持任何二进制文件的基本内容管理功能-存储、在线管理元数据、版本控制、上传和下载等，而不受其格式的限制。 Adobe Experience Manager Assets支持各种文件格式，每种产品功能都支持各种不同格式。

此外，Experience Manager资产还提供扩展支持，可生成预览和演绎版并提取元数据和文本以实现全文索引。 此扩展支持是使用资产微 [型服务提供的](asset-microservices-configure-and-use.md)。

下图说明了支持级别。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| * | 查看表下的注释 |
| - | 不适用 |

## 使用资产微型服务进行资产转换 {#asset-microservices-supported-formats}

主要功能包括：

* 由Adobe [应用程序](#adobe-formats) 和服务（包括Adobe Photoshop、Adobe InDesign、Adobe Illustrator、Adobe XD、Adobe Dimension和Adobe Acrobat或PDF）生成的主要Adobe文件格式。
* 关键 [成像文件格式](#image-formats)。
* [Camera Raw文件格式](#camera-raw-formats) ，适用于各种相机，包括Canon、Nikon、Fujifilm、Olympus和其他制造商（由Adobe Camera Raw提供支持）。
* 常见 [文档格式](#document-formats)，包括Microsoft Office和Open文档格式。
* 各种[视频](#video-formats)和[音频](#audio-formats)格式.

### Adobe格式 {#adobe-formats}

| 文件格式 | 缩略图生成 | 全文提取 | 元数据提取 | 宽度／高度 |
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

\*对于INDD（InDesign文件），再现的大小由嵌入在INDD文件中的预览决定。 在InDesign中配置首选项(“首&#x200B;**[!UICONTROL 选项”>“文件处理”>“始终使用预览保存文档图像、预览大小]**”)以嵌入较大的再现。

### 图像格式 {#image-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度／高度 | 裁剪 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

### Camera RAW格式 {#camera-raw-formats}

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

### 文档格式 {#document-formats}

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

### 视频格式 {#video-formats}

| 文件格式 | 缩略图生成 | 元数据提取 | 宽度／高度 |
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

### 音频格式 {#audio-formats}

资源作为云服务，为AIF、ASF、M4A、MP3、WAV和WMA音频格式提供XMP元数据提取支持。

>[!MORELIKETHIS]
>
>* [使用资产微服务进行资产处理](asset-microservices-overview.md)

