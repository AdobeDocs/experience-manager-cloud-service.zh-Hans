---
title: 支援的檔案格式和MIME型別
description: 支援的檔案格式和MIME型別 [!DNL Experience Manager Assets] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 10%

---

# [!DNL Assets] 支援的檔案格式 {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 支援任何二進位檔案的基本內容管理功能 — 儲存、線上管理中繼資料、版本設定、上傳和下載等，不受檔案格式限制。 [!DNL Adobe Experience Manager Assets] 支援廣泛的檔案格式，而且每種產品功能對於不同的格式都有不同的支援。

此外， [!DNL Experience Manager Assets] 提供延伸支援，可產生預覽和轉譯，以及擷取中繼資料和文字以用於全文索引。 此延伸支援是透過以下方式提供： [資產微服務](asset-microservices-configure-and-use.md).

使用資產微服務進行資產轉換的重點包括：

* 金鑰 [Adobe檔案格式](#adobe-formats) 由Adobe應用程式和服務所產生，包括 [!DNL Adobe Photoshop]， [!DNL Adobe InDesign]， [!DNL Adobe Illustrator]， [!DNL Adobe XD]， [!DNL Adobe Dimension]、和 [!DNL Adobe Acrobat] 或PDF。
* 金鑰 [影像檔案格式](#image-formats).
* [Camera Raw檔案格式](#camera-raw-formats) 適用於多種相機，包括Canon、Nikon、Fujifilm、Olympus和其他製造商(由Adobe Camera Raw提供)。
* 通用 [檔案格式](#document-formats)，包括Microsoft Office和Open Document格式。
* 各种[视频](#video-formats)和[音频](#audio-formats)格式.

下列圖例說明每種格式的支援等級。

| 支援等級 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| * | 請參閱表格下方的註解 |
| - | 不适用 |

## Adobe格式 {#adobe-formats}

| 檔案格式 | 產生縮圖 | 全文檢索擷取 | 中繼資料擷取 | 寬度/高度 |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| 拼貼 | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| 構思 | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\*用於 [!DNL Adobe InDesign] 檔案(INDD)，轉譯的大小由內嵌在INDD檔案中的預覽決定。 設定偏好設定於 [!DNL InDesign] (**[!UICONTROL 偏好設定>檔案處理>一律儲存包含檔案的預覽影像，預覽大小]**)以內嵌較大的轉譯。

## 影像格式 {#image-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度/高度 | 裁剪 |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |
| WebP | ✓ | ✓ | ✓ | ✓ |

## 3D格式 {#support-3d-formats}

支援下列3D格式。

另請參閱 [在Dynamic Media中使用3D資產](/help/assets/dynamic-media/assets-3d.md).

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 存取控制 | 縮圖預覽 | 3D預覽 | Dynamic Media傳遞 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| 物件 | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## [!DNL Camera RAW] 格式 {#camera-raw-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度/高度 |
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

## 檔案格式 {#document-formats}

資產管理功能支援的檔案格式如下。

| 檔案格式 | 產生縮圖 | 全文檢索擷取 | 寬度/高度 | 中繼資料管理 | [连接的资产](use-assets-across-connected-assets-instances.md) | 完整檔案預覽 |
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

## 視訊格式 {#video-formats}

| 檔案格式 | 產生縮圖 | 中繼資料擷取 | 寬度/高度 |
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

## 音訊格式 {#audio-formats}

[!DNL Assets] as a [!DNL Cloud Service] 為AIF、ASF、M4A、MP3、WAV和WMA音訊格式提供XMP中繼資料擷取支援。

## 音訊和視訊轉錄支援的輸入格式 {#audio-video-transcription-formats}

* FLV （含H.264和AAC轉碼器） (.flv)
* MXF (.mxf)
* MPEG2-PS、MPEG2-TS、3GP (.ts、.ps、.3gp、.3gpp、.mpg)
* Windows Media Video (WMV)/ASF (.wmv、.asf)
* AVI （未壓縮8位元/10位元） (.avi)
* MP4 (.mp4， .m4a， .m4v)
* Microsoft數位視訊錄製(DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## 提示和限制 {#limitations-and-tips}

* 目前，中繼資料擷取的檔案大小限制約為15 GB。 上傳超大型資產時，有時中繼資料擷取作業會失敗。

## Dynamic Media — 支援的輸入視訊格式可轉碼 {#video-dynamic-media-transcoding}

| 視訊副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
| --- | --- | --- | --- |
| AVI | A/V交錯 | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft Video 1 (MS-CRAM) |
| FLV、F4V | AdobeFlash | H264/AVC、Flix VP6、H263、Sorenson | SWF（向量動畫檔案） |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422和HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate， Apple動畫 |
| MP4 | MPEG-4 | H264/AVC （所有設定檔） | − |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | − |
| MXF ‡ | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | − |
| OGV， OGG | Ogg | Theora， VP3， Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting (G2M2、G2M3、G2M4) | Microsoft畫面(MSS2)、Microsoft像片故事(WVP2) |

‡目前尚不支援將此視訊格式用於Dynamic Media中的互動式視訊，或用於Experience Manager Assets中的註解。

## Dynamic Media — 支援的檔案格式 {#document-support-dynamic-media}

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 傳遞動態轉譯 | 下載動態轉譯 |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF（請見下方附註） | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>對於安全PDF，僅支援上傳。

## Dynamic Media — 支援的點陣影像格式 {#image-support-dynamic-media}

| 格式 | 上傳（輸入格式） | 建立影像預設集（輸出格式） | 預覽動態轉譯 | 傳遞動態轉譯 | 下載動態轉譯 | 設定支援此格式的型別 |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- | ---------------------------------- |
| BMP | ✓ | - | - | - | - | [影像](/help/assets/dynamic-media/image-sets.md)， [混合媒體](/help/assets/dynamic-media/mixed-media-sets.md)、和 [迴轉](/help/assets/dynamic-media/spin-sets.md) |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/dynamic-media/image-sets.md)， [混合媒體](/help/assets/dynamic-media/mixed-media-sets.md)、和 [迴轉](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | - | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/dynamic-media/image-sets.md)， [混合媒體](/help/assets/dynamic-media/mixed-media-sets.md)、和 [迴轉](/help/assets/dynamic-media/spin-sets.md) |
| PSD   ‡ | ✓ | - | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/dynamic-media/image-sets.md)， [混合媒體](/help/assets/dynamic-media/mixed-media-sets.md)、和 [迴轉](/help/assets/dynamic-media/spin-sets.md) |

‡合併的影像會從PSD檔案中擷取。 這是由產生的影像 [!DNL Adobe Photoshop] 和包含在PSD檔案中。 視設定而定，合併的影像不一定是實際影像。

## Dynamic Media — 不支援的點陣影像格式 {#unsupported-raster-image-formats-dm}

下列點陣影像檔案格式的子型別 *not* 支援 [!DNL Dynamic Media]：

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援色彩空間不是CMYK、RGB、灰階或點陣圖的PSD檔案。 不支援DuoTone、Lab和索引色域。
* 位元深度大於16的PSD檔案。
* TIFF含有浮點資料的檔案。
* TIFF具有Lab色域的檔案。

## Dynamic Media — 支援的3D檔案格式 {#support-3d-formats-dynamic-media}

另請參閱 [支援的3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D副檔名 | 檔案格式 | MIME型別 | 注释 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary | 將材質和紋理納入為單一資產。 |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體光刻 | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene說明Zip封存 | model/vnd.usdz+zip | *僅支援內嵌；不提供檢視或互動。* USDZ是專屬的3D格式，可由Safari或iOS以原生方式檢視。 |

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
>* [使用資產微服務進行資產處理](asset-microservices-overview.md)
>* [文字型資產的智慧型標籤支援的檔案格式](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

