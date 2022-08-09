---
title: 已知问题
description: Adobe Experience Manager as a Cloud Service 的已知问题
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 755c0072148ad73486df2ccfed69248b9d73ec2a
workflow-type: ht
source-wordcount: '177'
ht-degree: 100%

---

# 已知问题 {#known-issues}

本文列出了 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 产品的已知问题。该列表会随每次连续发行的 [!DNL Experience Manager] 进行修订和更新。

有关已知问题的更多信息，请[联系支持人员](https://experienceleague.adobe.com/?lang=zh-hans&amp;support-solution=Experience+Manager#support)。

<!-- 
## Platform {#platform}
-->

## Sites {#sites}

[!DNL Sites] 中的一些已知问题包括：

* 在 GraphQL IDE 中，您可以[管理保留查询的缓存](/help/headless/graphql-api/graphiql-ide.md##managing-cache)。
   * 在首次保存时，为标题保存的值将设置为 `0` （而不是默认值） – 如果用户未在对话框中更改这些值。
   * 在后续保存时，值会正确保存。
   * 因此，用户必须保存两次标头。

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

[!DNL Assets] 中的一些已知问题包括：

* **下载**：如果下载空文件夹，[!DNL Experience Manager] 会传达有关创建 ZIP 存档的成功消息，但并未创建该存档。

* **元数据架构**：资产评级构件曾导致 JSP 编译错误。已从元数据架构将其删除。<!-- CQ-4282865, CQ-4284633 -->

另请参阅[对  [!DNL Experience Manager Assets]](/help/assets/assets-cloud-changes.md) 的重要更改。

<!-- This content was added at GA. Not sure if we should continue to have this commitment about upcoming features/enh. in the docs. Commenting it for now.

### Upcoming Assets capabilities {#upcoming-assets-capabilities}

A few capabilities of Adobe Experience Manager Assets that depend on foundation capabilities, which are not yet available in the Experience Manager as a Cloud Service deployment architecture, are expected to be enabled at a later stage:

* Capabilities not enabled at this stage due to dependency on Commerce Integration Framework APIs:
  * Photoshoot workflow models.
  * Product information tab in the asset properties user interface is not populated.

* Capabilities not enabled at this stage due to dependency on InDesign Server integration:
  * Asset Templates and Asset Catalogs.
  * Multi-page preview of Adobe InDesign files.
-->

>[!MORELIKETHIS]
>
>* [ [!DNL Experience Manager]](aem-cloud-changes.md) 中的主要更改
>* [已弃用和已删除的功能](deprecated-removed-features.md)
>* [发行说明](home.md)

