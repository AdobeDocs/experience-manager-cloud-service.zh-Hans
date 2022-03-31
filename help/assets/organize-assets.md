---
title: 组织您的数字资产
description: 使用Experience Manager整理数字资产、图像、文件、文件夹等。
contentOwner: AG
feature: Asset Management, Search
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 54b83598a5d48832ecdea666c059e91b3dfa3ef9
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 1%

---

# 组织您的数字资产 {#organize-digital-assets}

Microsoft® Office和PDF文档的所有数字资产、元数据和内容都将被提取并进行搜索。 搜索允许对资产进行复杂的筛选，并完全尊重正确的权限。 数字资产管理的元数据中详细介绍了元数据。

[!DNL Experience Manager Assets] 支持多种内容组织方式。 您可以使用文件夹以分层方式组织它们，也可以按未排序的临时方式（例如标记）组织它们。 用户可以在DAM资产编辑器中编辑标记，其中显示了子资产、演绎版和元数据。

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a new folder.
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

You can use folders or tags or both to organize assets. Adding tags to assets makes them more easy to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## 在文件夹中组织资产 {#organize-using-folders}

组织资产的最基本方式是将资产保存在文件夹中。 它类似于在本地文件系统的文件夹中组织文件。 有关如何创建和管理文件夹的更多信息，请参阅 [管理资产](manage-digital-assets.md). 您如何命名文件和文件夹、如何排列子文件夹以及如何处理这些文件夹中的文件，可能会对这些资产的处理方式产生重大影响。 通过使用一致且适当的文件和文件夹命名策略以及良好的元数据实践，您可以充分利用数字资产存储库。

* 通常，数字资产存储库会一直在增长。 因此，在内容创建周期的早期，务必要正规化元数据的使用、文件夹结构和文件命名。
* 仅使用文件夹来为数字资产强制实施一致的存储结构。 此一致性有助于您的流程并更好地管理资产。 例如，放置在以下类型文件夹中的资产可以帮助您分隔资产：

   * **开发文件夹**:包含您当前正在处理的数字资产。
   * **客户端文件夹**:包含基于客户或项目名称的数字资产。
   * **主文件夹**:包含原始的源数字资产。
   * **演绎版文件夹**:包含原始源数字资产的演绎版和副本。
   * **文件大小文件夹**:包含基于小、中或大文件大小的数字资产。
   * **暂存文件夹**:包含已准备好在您的网站上实时发布的数字资产。
   * **MIME类型文件夹**:包含特定于MIME类型（如图像、文档和多媒体）的数字资产。
   * **存档文件夹**:包含已停用的数字资产。
   * **基于日期的文件夹**:包含基于创建日期或上次修改日期的数字资产。

* 创建不太可能更改的文件夹目录，以便任何自定义或自动操作都可以继续运行。 例如，分配的处理配置文件可继续工作。
* 如果资产已发布，则您可以使用 [!DNL Experience Manager] 要将资产移动到其他文件夹，并从其新位置重新发布。 原始已发布的资产位置与新重新发布的资产一起仍可用。 但是，原始发布的资产是 *丢失* to [!DNL Experience Manager] 和无法取消发布。 因此，作为最佳实践，请先取消发布资产，然后将其移动到其他文件夹。

## 使用标记组织资产 {#use-tags-to-organize-assets}

<!--
Using tags, as a metadata, you can easily search assets, create collections using the search results, boost search ranking for some assets, and apply AI algorithms of Adobe Sensei for asset discovery.

[!DNL Adobe Experience Manager Assets] uses a self-learning algorithm to create highly descriptive tags that allow you to find the right asset in just a few clicks. Smart tagging uses Adobe Sensei, artificial intelligence and machine learning framework, which can be trained to recognize and apply both standard and business-specific tags to imagery. Smart Tags can also identify content, individual words, or phrases and automatically apply descriptive tags to assets

For more information, see the following articles:

* [Edit asset metadata](meta-edit.md)
* [Smart Tags in Assets](smart-tags.md)
-->

向资产添加标记可在搜索期间更轻松地检索标记，使用搜索结果创建收藏集，提升某些资产的搜索排名，以及将Adobe Sensei的AI算法应用于资产发现。

[!DNL Adobe Experience Manager Assets] 使用自学算法创建高度描述性的标记，以便您只需单击几下即可找到正确的资产。 智能标记使用Adobe Sensei、人工智能和机器学习框架，经过培训后，该框架可以识别标准标记和特定于业务的标记并将其应用于图像。 智能标记还可以识别内容、单个词或短语，并自动将描述性标记应用于资产。

以下是向资产添加标记的步骤：

1. 登录到 [!DNL Experience Manager Assets].
1. 单击 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**，选择资产并单击 **[!UICONTROL 属性]** 以打开资产属性。
1. 在 **[!UICONTROL 基本]** ，单击 **[!UICONTROL 标记]** 元数据。 随即会打开一个弹出窗口。
1. 从 `cq-tags`. 您可以为资产分配多个标记。

   您可以根据 **[!UICONTROL 名称]** （按字母顺序）， **[!UICONTROL 已创建]** 日期，或 **[!UICONTROL 已修改]** 日期。 在下图中，标签结构根据 **[!UICONTROL 名称]**.

   ![添加标记](assets/add-tags-to-asset.png)

1. 单击 **保存** 以更新资产元数据更改。

>[!NOTE]
>
>在创建智能标记时以及使用标记谓词应用搜索过滤器时，可以对标记结构进行排序。
>
>预发行渠道中提供了排序标记功能。 请参阅 [预发行渠道文档](/help/release-notes/prerelease.md#enable-prerelease) 以了解为环境启用该功能的信息。

有关更多信息，请参阅以下文章：

* [编辑资产元数据](meta-edit.md)
* [资产中的智能标记](smart-tags.md)
* [将标记谓词添加到搜索面板](/help/assets/search-facets.md/#adding-a-tags-predicate)

## 组织为收藏集 {#organize-as-collections}

将资产收藏集放在 [!DNL Experience Manager Assets]，您可以简化在用户之间创建、编辑和共享资产的功能。 根据您使用收藏集的方式创建多种类型的收藏集，包括包含资产、文件夹和收藏集的静态引用列表的收藏集，以及根据搜索条件提取资产的收藏集。 您可以使用不同位置的资产创建收藏集，并与具有不同访问、查看和编辑权限级别的多个用户共享这些收藏集。

有关更多信息，请参阅 [管理收藏集](manage-collections.md)


## 使用用户档案组织资产 {#organize-to-use-profiles}

处理配置文件包含 [!DNL Assets] 处理命令，这些命令适用于上传到预定义文件夹的资产。 配置文件用于自动处理文件夹或新上传资产的内容。 您可以使用用户档案更好地组织资产。

标准化元数据使用、文件命名和文件夹结构可确保随着数字资产池的增长，您可以更精确、更一致地将处理配置文件应用到文件夹。

>[!MORELIKETHIS]
>
>* [使用资产微服务和处理配置文件](asset-microservices-configure-and-use.md)
>* [元数据配置文件](metadata-profiles.md)
>* [视频配置文件](/help/assets/dynamic-media/video-profiles.md)
>* [Dynamic Media图像配置文件](/help/assets/dynamic-media/image-profiles.md)


