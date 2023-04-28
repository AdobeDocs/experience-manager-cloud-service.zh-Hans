---
title: 在中管理PDF文档 [!DNL Adobe Experience Manager].
description: 在中管理PDF文档 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 3%

---

# 在Experience Manager Assets中管理PDF文档as a Cloud Service {#add-assets-to-experience-manager}

Experience Manager Assets与Document CloudPDF查看器无缝集成，允许您预览PDF文档的多个页面。 此外，您还可以使用高级Document CloudPDF查看器功能(如批注、搜索文本、使用书签和缩略图浏览PDF文档等)，以及在同一屋顶下执行更多操作。 Experience Manager Assets还允许您上传其他支持格式的文档，并以PDF格式预览它们。

Document CloudPDF查看器使AEM Assets在以下方面受益：
* [支持PDFDocument Cloud查看器组件](#pdf-doc-cloud)
* [支持对PDF资产进行多个页面预览和注释](#multi-page)
* [支持对其他格式的文档进行多页面预览](#multi-format)

> 提示
> 如果无法获取以前上传的PDF文档的多个页面预览，请选择PDF并单击 **![重新处理](/help/assets/assets/Reprocess.svg) 重新处理资产**.

## 支持PDFDocument Cloud查看器组件 {#pdf-doc-cloud}

本机PDFDoc Cloud查看器在AEM Assets中具有以下组件：

* **PDF查看器（使用页面缩略图）** 缩略图视图是PDF文档页面的小型预览。 使用缩略图，您可以直接跳转到所需的页面。 您可以通过 ![缩略图](/help/assets/assets/thumbnail.svg) 在左窗格中。

* **PDF查看器使用书签** 书签是一个直接链接，可导航到文档中的内容。 您可以通过访问所选PDF文档的书签 ![书签](/help/assets/assets/bookmark.svg) 在左窗格中。

* **搜索PDF** 您可以使用搜索 ![搜索](/help/assets/assets/Search.svg) 查找PDF文档中的文本。

* **页面向上/向下** Use Page Up ![Page Up](/help/assets/assets/ArrowUp.svg) 或Page Down ![Page Down](/help/assets/assets/ArrowDown.svg) 滚动浏览文档。

* **缩小/放大** 使用缩小 ![缩小](/help/assets/assets/ZoomOut.svg) 或放大 ![放大](/help/assets/assets/ZoomIn.svg) 来扫描文档。

* **页面适合** 根据屏幕大小，使用宽度或高度尺寸来适合文档。

* **停放/取消停放PDF** 您可以使用此选项停放或取消停放本机PDF查看器的组件。

## 支持对PDF资产进行多个页面预览和注释 {#multi-page}

Adobe Experience Manager Assets允许您预览包含多个页面的PDF文档。 要预览PDF文档的多个页面，请考虑以下步骤：

1. 按照 [在AEM中上传资产](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. 浏览要上传和预览的PDF文档。
1. 打开文档。
1. 默认情况下，PDF文档查看器会加载。 您还可以在演绎版面板下选择PDF演绎版。
1. 在演绎版下拉列表下，选择 **所有演绎版**.

您还可以应用 [批注](#pdf-annotations) 到PDF文档。

> 注意
> 您可以预览的资产的最大大小为100 MB。

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF批注{#pdf-annotations}**

Experience Manager Assets允许您向PDF文档添加注释。 PDF文档可以有多个批注。

要对PDF文档添加注释，请执行以下步骤：
1. 转到PDF界面，导航到要添加批注的资产文档。 在右侧打开本机PDF查看器，该查看器显示所选PDF文档的预览。
1. 单击 **注释** 中。
以下是可应用于PDF文档的注释：

<table>
        <tr>
             <th> 注释 </th>
            <th> 描述 </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> 注释 </td>
            <td> 选择注释以表示观察。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> 文本框 </td>
            <td> 选择文本框以输入文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> 附注 </td>
            <td> 添加小文本或提醒，以告知您可以添加到PDF上的特定区域。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> 文本高亮器 </td>
            <td> 选择要以不同颜色突出显示的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> 文本底线 </td>
            <td> 选择要加下划线的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> 三振 </td>
            <td> 选择要划出的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> 绘图 </td>
            <td> 将可视化图稿插入PDF。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> 拭除绘图 </td>
             <td> 移除或撤消绘图。 </td>
        </tr>
    </table>

## 支持对其他格式的文档进行多页面预览 {#multi-format}

除了PDF文档之外，您还可以预览其他格式类型文档的多个页面。 支持的文档格式类型为TXT、RTF、DOC、DOCX、PPT、PPTX、XLS和XLSX。 Experience Manager Assets会自动将这些文档格式转换为PDF格式，并使其可供预览。

![其他格式文档的多页预览](/help/assets/assets/multi-page-other-formats.png)

对于其他受支持文档格式的多页预览，请执行以下步骤：
1. 按照 [在AEM中上传资产](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. 浏览要上传和预览的文档。
1. 打开文档。
1. 在左侧面板的静态部分下选择PDF。 右侧面板显示资产的多个页面预览。 从左侧面板中选择缩略图以选择要预览的页面。

> 注意
> * 您可以预览的资产的最大大小为100 MB。
> * 要预览的XLS或XLSX文件的最大大小为20 MB。
>


**另请参阅**

* [翻译资产](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资产支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资产](use-assets-across-connected-assets-instances.md)
* [资源报表](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
