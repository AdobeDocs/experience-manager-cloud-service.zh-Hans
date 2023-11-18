---
title: 组织您的数字资产
description: 使用Experience Manager整理您的数字资源、图像、文件、文件夹等。
contentOwner: AG
feature: Asset Management, Search
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 5%

---

# 组织您的数字资产 {#organize-digital-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/organize-assets.html?lang=en) |
| AEM as a Cloud Service | 本文 |

Microsoft®Office和PDF文档的所有数字资源、元数据和内容都将进行提取并使其可搜索。 搜索允许对资产进行复杂的筛选，并完全尊重适当的权限。 数字资产管理中的元数据详细介绍了元数据。

[!DNL Experience Manager Assets] 支持多种内容组织方式。 您可以使用文件夹以分层方式组织它们，也可以以无序、临时方式组织它们，例如标记。 用户可以在DAM资产编辑器中编辑显示子资产、演绎版和元数据的标记。

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a folder.
1. In the menu, click **[!UICONTROL Create]**. Select **[!UICONTROL New Folder]**.
1. In the **[!UICONTROL Title]** field, provide a folder name. By default, DAM uses the title that you provided as the folder name. Once the folder is created, you can override the default and specify another folder name.
1. Click **[!UICONTROL Create]**. Your folder is displayed in the digital assets folder.

## Add CUG properties to folders {#add-cug-properties-to-folders}

You can limit who can access certain folders in Assets by making the folder part of a closed user group (CUG). To make a folder part of a CUG:

1. In Assets, right-click the folder you want to add closed user group properties for and select **Properties**.  
1. Click the **CUG** tab.
1. Select the **Enabled** check box to make the folder and its assets available only to a closed user group.  
1. Browse to the login page, if there is one, to add that information. Add admitted groups by clicking **Add item**. If necessary, add the realm. Click **OK** to save your changes.

## Use tags to organize assets {#use-tags-to-organize-assets}

You can use folders or tags or both to organize assets. Adding tags to assets makes them easier to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## 在文件夹中组织资源 {#organize-using-folders}

组织资源的最基本方法是将资源保存在文件夹中。 这类似于在本地文件系统的文件夹中组织文件。 有关如何创建和管理文件夹的详细信息，请参阅 [管理资源](manage-digital-assets.md). 如何命名文件和文件夹、如何排列子文件夹以及如何处理这些文件夹中的文件可能会对这些资源的处理方式产生重大影响。 通过使用一致且适用的文件和文件夹命名策略以及良好的元数据做法，您可以充分利用数字资源存储库。

* 通常，您的数字资产存储库会一直不断增长。 因此，在内容创建周期早期将元数据的使用、文件夹结构和文件命名正规化非常重要。
* 仅使用文件夹为您的数字资产强制实施一致的存储结构。 此一致性可帮助您的流程更好地管理您的资产。 例如，放置在以下类型文件夹中的资产可以帮助您分离资产：

   * **开发文件夹**：包含您当前正在处理的数字资产。
   * **客户端文件夹**：包含基于客户端或项目名称的数字资源。
   * **主文件夹**：包含原始的源数字资源。
   * **节目文件夹**：包含原始源数字资产的演绎版和副本。
   * **文件大小文件夹**：包含基于小型、中型或大型文件大小的数字资源。
   * **暂存文件夹**：包含准备在网站上实时发布的数字资产。
   * **MIME类型文件夹**：包含特定于MIME类型的数字资产，例如图像、文档和多媒体。
   * **存档文件夹**：包含已弃用的数字资产。
   * **基于日期的文件夹**：包含基于创建日期或上次修改日期的数字资源。

* 创建不太可能更改的文件夹的目录，以便任何自定义或自动化均可继续工作。 例如，分配的处理配置文件将继续工作。
* 如果资产已发布，则使用 [!DNL Experience Manager] 以将资产移动到另一个文件夹，并从其新位置重新发布。 原始发布的资产位置仍然可以与新重新发布的资产一起使用。 然而，最初发布的资产是 *丢失* 到 [!DNL Experience Manager] 和无法取消发布。 因此，作为最佳实践，首先取消发布资产，然后将其移动到其他文件夹。

## 使用标记组织资源 {#use-tags-to-organize-assets}

向资源添加标记可使其在搜索期间更易于检索、使用搜索结果创建收藏集、提升某些资源的搜索排名，以及将Adobe Sensei的AI算法应用于资源发现。

[!DNL Adobe Experience Manager Assets] 使用自学习算法创建具有高度描述性的标记，让您只需单击几下即可找到所需的资产。 智能标记使用Adobe Sensei、人工智能和机器学习框架，可以通过培训来识别标准标记和业务特定标记，并将其应用于图像。 智能标记还可以识别内容、单个单词或短语，并自动将描述性标记应用于资产。

以下是将标记添加到资源的步骤：

1. 登录 [!DNL Experience Manager Assets].
1. 单击 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**，选择资产并单击 **[!UICONTROL 属性]** 以打开资产属性。
1. 在 **[!UICONTROL 基本]** 选项卡，单击中的文件夹图标 **[!UICONTROL 标记]** 元数据。 随即会打开一个弹出窗口。
1. 从中的现有标记中搜索或选择相应的标记 `cq-tags`. 您可以为资产分配多个标记。

   您可以根据 **[!UICONTROL 名称]** （按字母顺序）， **[!UICONTROL 已创建]** 日期，或 **[!UICONTROL 修改时间]** 日期。 在下图中，标记结构根据 **[!UICONTROL 名称]**.

   ![添加标记](assets/add-tags-to-asset.png)

1. 单击 **保存** 以更新资源元数据更改。

有关更多信息，请参阅以下文章：

* [编辑资源元数据](meta-edit.md)
* [Assets中的智能标记](smart-tags.md)
* [将标记谓词添加到搜索面板](/help/assets/search-facets.md/#adding-a-tags-predicate)

## 组织为收藏集 {#organize-as-collections}

在中使用资产收藏集 [!DNL Experience Manager Assets]，您可以简化在用户之间创建、编辑和共享资源的功能。 根据您的使用方式创建多种类型的收藏集，包括包含资产、文件夹和收藏集的静态引用列表的收藏集，以及根据搜索条件拉入资产的收藏集。 您可以使用不同位置的资源创建收藏集，并与具有不同访问级别、查看和编辑权限的多个用户共享这些收藏集。

有关更多信息，请参阅 [管理收藏集](manage-collections.md)


## 使用用户档案组织您的资源 {#organize-to-use-profiles}

处理配置文件包含 [!DNL Assets] 处理应用于上传到预定义文件夹的资源的命令。 配置文件用于自动处理文件夹的内容或最新上传的资产。 您可以使用用户档案更好地组织资源。

标准化元数据使用、文件命名和文件夹结构可确保随着数字资产池的增长，您可以更精确和一致地将处理配置文件应用到文件夹。

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

>[!MORELIKETHIS]
>
>* [使用资产微服务和处理配置文件](asset-microservices-configure-and-use.md)
>* [元数据配置文件](metadata-profiles.md)
>* [视频配置文件](/help/assets/dynamic-media/video-profiles.md)
>* [Dynamic Media图像配置文件](/help/assets/dynamic-media/image-profiles.md)

