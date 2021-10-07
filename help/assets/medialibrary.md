---
title: 将Media Library用于基本数字资产管理
description: '[!DNL Experience Manager Assets] 和Media Library进行资产管理。'
contentOwner: AG
feature: Asset Management,Publishing
role: User,Architect,Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: e294ecdefca89bc3fd16ee2166a1a8418d0237ee
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# 将Media Library用于基本资产管理 {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] platform提供了不同的资产管理功能。Media Library允许用户将少量资产上传到存储库、搜索和使用网页中的资产，并完成资产上的简单资产管理任务。

Media Library是一款轻量级的数字资产管理(DAM)解决方案，附带[!DNL Adobe Experience Manager Sites]许可证。 [!DNL Sites] 是Web内容管理(WCM)产品。Media Library可与所有Experience Manager功能配合使用。

[!DNL Adobe Experience Manager Assets] 许可证可单独购买。[!DNL Experience Manager Assets] 允许通过企业用例、元数据、架构、搜索和用户界面的自定义，以及Media Library提供的其他许多功能，对资产进行可靠处理。

## 许可要求 {#avail-media-library-license}

拥有[!DNL Sites]许可证的客户有权使用Media Library。 它适用于[!DNL Experience Manager]的所有组件。

Media Library将作为Sites的一部分进行安装。 除Sites许可证和安装之外，无需其他许可证或包。

## [!DNL Assets] 与Media Library {#assets-and-media-library}

Experience Manager Assets提供企业级DAM功能。 资产功能通过[!DNL Experience Manager]在一个包中提供。 但是，未购买资产许可证的用户无权使用高级DAM功能。 如果没有Assets许可证，则只有[Media Library功能](#use-media-library)可用。

如果要防止意外使用您未获得许可的[!DNL Assets]功能，请从[!DNL Experience Manager]中删除所有特定于[!DNL Assets]的工作流、组件、分类、选项和[!DNL Assets]管理员。 这样做可以防止用户意外使用您未授权的[!DNL Assets]功能。

## 使用Media Library {#use-media-library}

Media Library广泛涵盖以下用例：

* 为使用[!DNL Adobe Experience Manager Sites]创建的网页提供基本的DAM功能。
* 使用[!DNL Adobe Experience Manager Forms]创建的自适应表单和通信。
* 使用[!DNL Adobe Experience Manager Screens]创建的数字屏幕体验。
* [!DNL Assets] 用于无头操作的HTTP REST API。

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions
* Projects, tasks authoring
* Activity stream (timeline)
* Comments and annotation
-->

要使用Media Library功能，您可以使用默认的[!DNL Experience Manager]用户界面。 Media Library是[!DNL Experience Manager Sites]安装的一部分，不需要单独的界面或附加组件。 使用现有界面，Media Library用户有权完成以下任务：

* 创建文件夹以组织资产。
* 上传资产。
* 发布资产。
* 编辑、移动和复制资产。
* 浏览、过滤和搜索（包括相似性搜索）资产。
* 向元数据字段（智能标记字段除外）中的值添加值并进行编辑，这些值默认位于资产[!UICONTROL 属性]页面的[!UICONTROL 基本]选项卡中。
* 添加和删除静态演绎版。
* 下载文件夹、资产和资产演绎版。
* 创建资产版本。
* 创建并执行资产审核任务。
* 在资产中添加批注。
* 通过内容查找器将资产添加到[!DNL Sites]页面。
* 用法 [!DNL Content Fragments].
* 在“站点”许可证下，为[!DNL Content Fragments]和引用的媒体资产使用HTTP REST和GraphQL API。
* Marketing Cloud集成。
* 自定义和扩展资产管理用户界面。
* 访问查询生成器(API)以扩展搜索功能。
* 创建静态标记。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>许多高级DAM用例由[!DNL Experience Manager Assets]完成。 Media Library许可证授权您使用Media Library仅执行列出的用例。 如果未列出用例，请勿将其与Media Library许可证结合使用。 如果您有任何疑问，请联系客户支持。

请注意，您不能使用智能标记、[!DNL Asset]链接、[!DNL Asset]选择器、批量标记、修改没有[!DNL Assets]许可证的资产工作流。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [中的DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] 产品说明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)

