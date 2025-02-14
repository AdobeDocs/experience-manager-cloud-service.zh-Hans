---
title: 在 [!DNL Adobe Experience Manager]中管理您的PDF文档。
description: 在 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]中管理PDF文档。
feature: Asset Management
role: User, Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 1652df9e774d8212b1bcc2898ca5d57e2a0d13bc
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 6%

---

# 在Experience Manager Assets as a Cloud Service中管理PDF文档 {#add-assets-to-experience-manager}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Experience Manager Assets与Document Cloud PDF Viewer无缝集成，这使您能够预览PDF文档的多个页面。 此外，您还可以使用高级Document Cloud PDF查看器功能，如注释、搜索文本、使用书签和缩略图导航PDF文档等等，这些功能位于同一屋檐下。 Experience Manager Assets还允许您上传其他受支持格式的文档，并以PDF格式预览文档。

Document Cloud PDF查看器可通过以下方式为AEM Assets带来好处：

* [支持PDF Document Cloud查看器组件](#pdf-doc-cloud)
* [支持PDF资产的多页面预览和批注](#multi-page)
* [支持其他格式文档的多页预览](#multi-format)

>[!TIP]
>
> 如果您无法获取以前上载的PDF文档的多页预览，请选择PDF并单击![重新处理](/help/assets/assets/Reprocess.svg) **重新处理Assets**。

## 支持PDF Document Cloud查看器组件 {#pdf-doc-cloud}

本机PDF Doc Cloud查看器在AEM Assets中具有以下组件：

* 使用页面缩略图的&#x200B;**PDF查看器**&#x200B;缩略图视图是PDF文档页面的小型预览。 使用缩略图，您可以直接跳转到所需的页面。 您可以通过左窗格中的![缩略图](/help/assets/assets/thumbnail.svg)访问所选PDF文档的缩略图。

* **使用书签的PDF查看器**&#x200B;书签是一个直接链接，可将您导航到文档中的内容。 您可以通过左窗格中的![书签](/help/assets/assets/bookmark.svg)访问所选PDF文档的书签。

* **在PDF中搜索**&#x200B;您可以使用搜索![搜索](/help/assets/assets/Search.svg)在PDF文档中查找文本。

* **Page Up/Page Down**&#x200B;使用Page Up ![Page Up](/help/assets/assets/ArrowUp.svg)或Page Down ![Page Down](/help/assets/assets/ArrowDown.svg)滚动文档。

* **缩小/放大**&#x200B;使用缩小![缩小](/help/assets/assets/Zoom-out.svg)或放大![放大](/help/assets/assets/zoom-in.svg)以扫描文档。

* **页面大小**&#x200B;根据屏幕大小，使用宽度或高度尺寸以适合文档。

* **停靠/取消停靠PDF**&#x200B;使用此选项可以停靠或取消停靠本机PDF查看器的组件。

## 支持PDF资产的多页面预览和批注 {#multi-page}

通过Adobe Experience Manager Assets，您可以预览包含多个页面的PDF文档。 要预览PDF文档的多个页面，请考虑以下步骤：

1. 按照步骤[在AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en)中上传资源。
1. 浏览要上载并预览的PDF文档。
1. 打开文档。
1. 默认情况下，会加载PDF文档查看器。 您还可以在呈现版本面板下选择PDF呈现版本。
1. 在“格式副本”下拉列表下，选择&#x200B;**所有格式副本**。

您还可以在多页预览中将[批注](#pdf-annotations)应用于PDF文档。

>[!NOTE]
>
> 您可以预览的资源大小上限为100 MB。

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**PDF批注{#pdf-annotations}**

Experience Manager Assets允许向PDF文档添加注释。 一个PDF文档可以有多个注释。

要为PDF文档添加批注，请执行以下步骤：

1. 转到Assets界面，导航到要注释的PDF文档。 本机PDF查看器将在右侧打开，显示所选PDF文档的预览。
1. 从顶部菜单中单击&#x200B;**注释**。
以下是可应用于PDF文档的注释：

<table>
        <tr>
             <th> 注释 </th>
            <th> 描述 </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg">备注 </td>
            <td> 选择“注释”以表达观察结果。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg">文本框 </td>
            <td> 选择文本框以输入文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg">便笺 </td>
            <td> 添加小文本或提醒，以便将其添加到PDF上的特定区域。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg">文本荧光笔 </td>
            <td> 选择要以不同颜色加亮的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg">文本下划线 </td>
            <td> 选择要加下划线的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg">删除线 </td>
            <td> 选择要划掉的文本。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg">绘图 </td>
            <td> 将可视化图表插入到PDF。 </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg">擦除绘图 </td>
             <td> 删除或撤消绘图。 </td>
        </tr>
    </table>

>[!NOTE]
>
>您添加到PDF文档的注释在预览模式下可用。 但是，下载或打印PDF文档时不会显示注释。

## 支持其他格式文档的多页预览 {#multi-format}

除了PDF文档之外，您还可以预览其他格式类型文档的多个页面。 支持的文档格式类型为TXT、RTF、DOC、DOCX、PPT、PPTX、XLS和XLSX。 Experience Manager Assets会自动将这些文档格式转换为PDF格式，并且可供预览。

![其他格式文档的多页预览](/help/assets/assets/multi-page-other-formats.png)

对于其他支持的文档格式的多页预览，请执行以下步骤：

1. 按照步骤[在AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en)中上传资源。
1. 浏览要上载和预览的文档。
1. 打开文档。
1. 在左侧面板的静态部分下选择PDF 。 右侧面板可显示资产的多个页面预览。 从左侧面板中选择缩略图以选择要预览的页面。

>[!NOTE]
>
> * 您可以预览的资源大小上限为100 MB。
> * 要预览的XLS或XLSX文件的最大大小为20 MB。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
