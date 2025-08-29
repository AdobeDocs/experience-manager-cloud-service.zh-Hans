---
title: Content Hub 的新增功能
description: 详细了解最近推出的一些Content Hub功能
role: User
exl-id: 77a5c54c-bbc5-4dfb-9c3a-aa0620e836d0
source-git-commit: 62ac097fca0142265f2e1ef28117619d59045e6c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 66%

---

# Content Hub 的新增功能 {#whats-new-content-hub}

Content Hub 是 Experience Manager Assets as a Cloud Service 的一部分，旨在为组织及其业务合作伙伴提供对品牌内容的普及化访问。它侧重于大规模分发资产以进行激活，并创建品牌内容变体，以提高营销敏捷度。

以下视频演示了Content Hub的关键功能：

>[!VIDEO](https://video.tv.adobe.com/v/3463712)

>[!IMPORTANT]
>
>[Assets Ultimate](/help/assets/assets-ultimate-overview.md) 和 Assets as a Cloud Service 包括 250 名 Content Hub 受限用户。[Assets Prime](/help/assets/assets-prime.md) 包括 50 名 Content Hub 受限用户。

## 发布日期 {#release-date}

Content Hub功能版(2025.8.0)的发布日期为2025年8月28日(与AEM as a Cloud Service版本的发布日期相同)。 下一个功能版本(2025.9.0)计划于2025年9月25日发布。

## 8月版功能 {#august-release-features}

**通过筛选器属性进行批量搜索**

Content Hub现在可帮助您更快地发现所需的资源。 借助新的批量搜索功能，您可以为任何筛选器属性输入多个值(以分隔符（例如，多个SKU ID）分隔)，并使用单个搜索即时检索所有匹配的资产。

[!BADGE 深入了解此功能]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/search-assets-content-hub#bulk-search"}

## 7月版功能 {#july-release-features}

**增强了 Content Hub 中的品牌化灵活性**

在现有的个性化功能的基础上，Content Hub 现在允许管理员通过添加自定义徽标图像来进一步定制他们的部署。还为横幅和徽标图像增加了对 TIFF 文件格式的支持，有助于更大的设计灵活性。

[!BADGE 深入了解此功能]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

**通过带标题的链接促进共享**

现在，您可以在生成共享链接时添加一个标题——可以从资产详细信息视图中添加或者在选择一个或多个资产后。这有助于接收者轻松识别每个链接的用途，尤其是在接收多个共享资产时。

![专用和公开链接](/help/assets/assets/shared-link-for-assets.png)

[!BADGE 深入了解此功能]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

**改进了过滤器导航**

现在，Content Hub 在过滤器中包含一个&#x200B;**显示全部**&#x200B;选项，允许用户查看所有可用的方面以及资产数量，而当前限制只能查看最多十个方面。增强了每个过滤器中的搜索和排序功能，使用户可以更轻松、更有效地发现和管理资产。

## 6月版功能 {#june-release-features}

### 收藏集管理 {#collections-governance}

Content Hub 现在允许您在创建过程中控制对收藏集的访问权限，确保只有授权用户才能查看或管理分组资产。它确保了安全性的提升、协作的优化、资产管理的有序化以及治理的简化。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

[!BADGE 深入了解此功能]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/collections-content-hub#create-collections"}

## 5月发布功能 {#may-release-features}

Content Hub 5月版本包括以下功能：

* [基于属性的访问控制](#attribute-based-access-control)

* [用户界面品牌化](#ui-branding)

* [公共链接共享](#public-link-sharing)

* [以ZIP格式下载多个资产](#download-multiple-assets-as-zip)

* [Content Hub中的Dynamic Media呈现版本](#dynamic-media-renditions)

### 基于属性的访问控制(ABAC) {#attribute-based-access-control}

Content Hub 现在允许您应用基于规则的限制来访问资产。资源权限可确保治理，还可确保用户只能访问相关的资源。

资产限制规则基于元数据定义。当资产的元数据满足规则中设定的条件时，该资产将对相应的用户组可见。

基于属性的访问控制具有以下几个主要优势：

* 消除了权限对文件夹结构的依赖

* 允许管理员上传资产并追溯确定权限结构

* 减少重复数量 - 提高资产完整性。当同一资产被不同组共享时，基于文件夹的权限需要设置副本。

[!BADGE 深入了解此功能]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/attribute-based-access-control"}

### 用户界面品牌化 {#ui-branding}

Content Hub 现在允许管理员使用品牌特定的元素来自定义用户界面，这些元素包括横幅图像、横幅标题和正文，以及主色和辅色。这些改进有助于确保品牌一致性，简化用户引导流程，并建立信任。

![UI 品牌化](/help/assets/assets/content-hub-ui-branding.png)

[!BADGE 深入了解此功能]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

### 公共链接共享 {#public-link-sharing}

Content Hub 现在支持生成可共享的链接，允许外部用户无需应用程序访问权限即可查看资产元数据或下载资产。

![UI 品牌化](/help/assets/assets/public-and-private-link.png)

[!BADGE 深入了解此功能]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

### 以ZIP格式下载多个资产 {#download-multiple-assets-as-zip}

Content Hub 现在还允许您将所选资产及其演绎版下载为 ZIP 文件，而非单独的文件，从而简化文件管理。

[!BADGE 深入了解此功能]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}

### Content Hub中的Dynamic Media呈现版本 {#dynamic-media-renditions}

您可以直接在 Content Hub 用户界面中访问所有 Dynamic Media 预设演绎版和智能裁剪，并进行下载。

&#x200B;![Dynamic Media 演绎版](/help/assets/assets/dm-renditions-content-hub.png)

[!BADGE 深入了解此功能]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}
