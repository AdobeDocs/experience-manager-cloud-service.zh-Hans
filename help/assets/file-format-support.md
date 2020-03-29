---
title: Experience Manager资产作为云服务支持的文件格式和MIME类型
description: Experience Manager资产作为云服务支持的文件格式和MIME类型。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68b2214a4c8941365120bdef670e89b4c9058966

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager作为云服务，支持基本的内容管理功能— 存储、在线管理元数据、版本控制、上传和下载等- 对于任何二进制文件，与其格式无关。 Adobe Experience Manager Assets支持各种文件格式，每种产品功能都支持各种不同格式。

此外，Experience Manager资产还提供扩展支持，可生成预览和演绎版并提取元数据和文本以实现全文索引。 此扩展支持使用资产 [微服务](asset-microservices-configure-and-use.md)。

以下图例描述了支持级别。

| 支持级别 | 描述 |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | 支持 |
| * | 查看表下的注释 |
| - | 不适用 |

## 使用资产微服务进行资产转换 {#asset-microservices-supported-formats}

主要功能包括：

* 由Adobe应用程序和服务(包括Adobe Photoshop [](#adobe-formats) 、InDesign、Illustrator、XD、Dimension和Acrobat / PDF)生成的主要Adobe文件格式。
* 关键 [成像文件格式](#image-formats)。
* [Camera Raw文件格式](#camera-raw-formats) ，适用于各种相机，包括Canon、Nikon、Fujifilm、Olympus和其他制造商（由Adobe Camera Raw提供支持）。
* 常见 [文档格式](#document-formats)，包括 [Microsoft Office](#microsoft-office-formats) (Word、Excel、PowerPoint)和 [Open文档格式](#opendocument-formats) 。
* 各种[视频](#video-formats)和[音频](#audio-formats)格式.

下表的列提供以下信息：

| 列 | 描述 |
| ------------ | --------------------------------------------------------------- |
| 格式 | 资产原始二进制文件的文件格式（文件扩展名） |
| GIF | 用于生成再现的GIF格式 |
| JPEG | 用于生成再现的JPEG格式 |
| PNG | 生成再现的PNG格式 |
| XMP | 提取原始二进制文件中的元数据 |
| TXT | 提取文本以从文档中索引 |
| 宽度／高度 | 支持定义再现的宽度和高度（像素） |

### Adobe格式 {#adobe-formats}

| 文件格式 | GIF | JPEG | PNG | TXT | XMP | 宽度／高度 |
| ----------- | --- | ---- | --- | --- | --- | ------------ |
| AI | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| 拼贴 | - | - | - | - | ✓ | - |
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| 创意 | - | - | - | - | ✓ | - |
| INDD | ✓ | ✓ | ✓ | - | ✓ | ✓* |
| INDT | - | - | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | - | - | ✓ | - |
| PSB | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| PSD | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| XD | ✓ | ✓ | ✓ | - | ✓ | ✓ |

\*对于INDD（InDesign文件），再现的大小由嵌入在INDD文件中的预览决定。 在InDesign中配置首选项(“首&#x200B;**[!UICONTROL 选项”>“文件处理”>“始终保存带有预览的预览图像”、“文档大小”]**)以嵌入较大的再现。

### 图像格式 {#image-formats}

| 文件格式 | GIF | JPEG | PNG | XMP | 宽度／高度 |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

### Camera RAW格式 {#camera-raw-formats}

| 文件格式 | GIF | JPEG | PNG | XMP | 宽度／高度 |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3FR | ✓ | ✓ | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ | ✓ | ✓ |

### 文档格式 {#document-formats}

| 文件格式 | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| 文本 | ✓ | - |
| XML | ✓ | - |

### Microsoft Office格式 {#microsoft-office-formats}

| 文件格式 | GIF | JPEG | PNG | 文本 | 宽度／高度 |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

### OpenDocument格式 {#opendocument-formats}

| 文件格式 | GIF | JPEG | PNG | 文本 | 高度 |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

### 视频格式 {#video-formats}

| 文件格式 | GIF | JPEG | PNG | XMP | 宽度／高度 |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3G2 | - | - | - | ✓ | - |
| 3GP | - | - | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ | ✓ | ✓ |
| DIVX | ✓ | ✓ | ✓ |  | ✓ |
| F4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ | ✓ | ✓ |
| M2T | ✓ | ✓ | ✓ | - | ✓ |
| M2TS | ✓ | ✓ | ✓ | - | ✓ |
| M2V | ✓ | ✓ | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| MKV | ✓ | ✓ | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MTS | ✓ | ✓ | ✓ | - | ✓ |
| OGV | ✓ | ✓ | ✓ | - | ✓ |
| QT | ✓ | ✓ | ✓ | - | ✓ |
| R3D | ✓ | ✓ | ✓ | - | ✓ |
| SWF | ✓ | ✓ | ✓ | - | ✓ |
| WEBM | ✓ | ✓ | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | ✓ |

### 音频格式 {#audio-formats}

作为云服务的资产提供了对以下音频格式的XMP支持：AIF、ASF、M4A、MP3、WAV和WMA。

## Supported document formats {#doc-formats}

资产管理功能支持的文档格式如下。

| 文件格式 | 存储 | 元数据管理 | [连接的资产](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|
| DOC | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ |
| PDF | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |
| RTF | ✓ | ✓ | ✓ |
| TXT | ✓ | ✓ | ✓ |
| XLS | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ |
| PPT | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ |

>[!MORELIKETHIS]
>
>* [使用资产微服务进行资产处理](asset-microservices-overview.md)

