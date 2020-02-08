---
title: Experience Manager资产作为云服务支持的文件格式和MIME类型
description: Experience Manager资产作为云服务支持的文件格式和MIME类型。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 776b089a322cc4f86fdcb9ddf1c3cc207fc85d39

---


# 资产支持的文件格式 {#supported-file-formats}

Adobe Experience manager作为云服务，支持任何二进制文件的基本内容管理功能——存储、在线管理元数据、版本控制、上传和下载等，而不受其格式的限制。 此外，对于图像、Adobe专有、文档和视频等常用文件格式，它提供扩展支持，可生成预览和再现以及提取元数据和文本以进行全文索引。 此扩展支持使用资产 [微服务](asset-microservices-configure-and-use.md)。

具有扩展支持的文件格式的一些亮点包括：

* 由Adobe应用程序和服务(包括Adobe Photoshop [](#adobe-formats) 、InDesign、Illustrator、XD、Dimension和Acrobat / PDF)生成的主要Adobe文件格式。
* 关键 [成像文件格式](#image-formats)
* [适用于各种相机的Camera Raw文件格式](#camera-raw-formats) ，包括Canon、Nikon、Fujifilm、Olympus和其他制造商（由Adobe Camera Raw提供支持）
* 常见 [文档格式](#document-formats)，包括 [Microsoft Office](#microsoft-office-formats) (Word、Excel、PowerPoint)和 [Open Document](#opendocument-formats) 格式
* 各种视 [频](#video-formats) 和音 [频格式](#audio-formats)

## 详细支持信息的图例 {#legend-for-detailed-support-information}

以下图例描述了功能的支持级别：

| 支持级别 | 描述 |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | 受支持 |
| * | 查看表下的注释 |
| - | 不适用 |

支持表的列提供以下信息：

| 列 | 描述 |
| ------------ | --------------------------------------------------------------- |
| 格式 | 资产原始二进制文件的文件格式（文件扩展名） |
| GIF | 用于生成再现的GIF格式 |
| JPEG | 用于生成再现的JPEG格式 |
| PNG | 生成再现的PNG格式 |
| XMP | 从原始二进制中提取元数据 |
| TXT | 从文档提取文本以进行索引 |
| 宽度／高度 | 支持定义再现的宽度和高度（像素） |

<!-- Adding this checkmark icon ✓ does not look good in table. The icon's shade and size has to be toned down for good readability and less clutter.
@gklebus: I suggest using a checkmark character, either U+2713 ✓ CHECK MARK or U+2714 ✔ HEAVY CHECK MARK
-->

## Adobe格式 {#adobe-formats}

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

\*对于INDD（InDesign文件），再现的大小由嵌入在INDD文件中的预览决定。 在InDesign中配置首选项(“首&#x200B;**[!UICONTROL 选项”>“文件处理”>“始终保存带有文档的预览图像和预览大小]**”)以嵌入较大的再现。

## 图像格式 {#image-formats}

| 文件格式 | GIF | JPEG | PNG | XMP | 宽度／高度 |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |


## Camera RAW格式 {#camera-raw-formats}

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

## 文档格式 {#document-formats}

| 文件格式 | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| 文本 | ✓ | - |
| XML | ✓ | - |

## Microsoft office格式 {#microsoft-office-formats}

| 文件格式 | GIF | JPEG | PNG | 文本 | 宽度／高度 |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

## OpenDocument格式 {#opendocument-formats}

| 文件格式 | GIF | JPEG | PNG | 文本 | 高度 |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

## 视频格式 {#video-formats}

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

## 音频格式 {#audio-formats}

作为云服务的资产提供了对以下音频格式的XMP支持：AIF、ASF、M4A、MP3、WAV和WMA。

<!-- TBD: Some items from https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedinputvideoformatsforDynamicMediatranscoding may be applicable.

Bring more parity with https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedMIMEtypes.
https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#Supportedmultimediaformats
-->

>[!MORELIKETHIS]
>
>* [使用资产微服务进行资产处理](asset-microservices-overview.md)

