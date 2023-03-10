---
title: 内容转移工具的先决条件
description: 内容转移工具的先决条件
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: fac037b59753ba1de960df47311c1febc2059d27
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 4%

---

# 内容转移工具的先决条件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="使用内容传输工具的重要注意事项"
>abstract="查看有关使用内容传输工具的重要注意事项，包括Java和AEM版本、支持的数据存储类型、用户组注意事项等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#pre-reqs" text="使用内容传输工具的重要注意事项"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#best-practices" text="最佳实践和准则"

下表总结了使用内容传输工具的先决条件。

请查看以下列出的所有注意事项：

| 注意事项 | 当前支持的功能 |
|--- |--- |
| AEM 版本 | 内容传输工具只能在AEM 6.3或更高版本上运行。 |
| 区段存储的大小 | 现有存储库少于5500万个JCR节点，上最大250 GB（在线压缩大小） *作者* 和50 GB *Publish* 当前受支持。 与Adobe客户关怀部门一起创建支持工单，讨论超出这些限制的区段存储大小选项。 |
| 内容存储库的总大小 <br>*（区段存储+数据存储）* | 内容传输工具旨在为文件数据存储类型传输高达20 TB的内容。 当前不支持任何大于20 TB的内容。 与Adobe客户关怀部门一起创建支持工单，讨论大于20 TB内容的选项。 <br>要显着加快大型存储库的内容传输过程，可以选择此选项 [预复制](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html#setting-up-pre-copy-step) 步骤可以使用。 这适用于文件数据存储、Amazon S3和Azure数据存储类型的数据存储。 对于Amazon S3和Azure数据存储区，支持大于20TB的存储库大小。 |
| Lucene索引总大小 | Lucene索引总大小最大为25GB，不包括 `/oak:index/lucene` 和 `/oak:index/damAssetLucene` 当前支持。 与Adobe客户关怀部门一起创建支持工单，讨论超出此限制的索引大小选项。 |
| 节点名称长度 | 当节点父路径>=（等于或大于）350字节时，节点名称的长度必须为150字节或更少。 这些节点名称必须缩短为&lt;= 150字节，以便AEMas a Cloud Service中的Document节点存储支持它们。 如果未修复这些长节点名称，则摄取将失败。 |
| 不可变路径中的内容 | 内容传输工具无法用于迁移不可变路径中的内容。 要传输内容来源，请执行以下操作 `/etc` 仅确定 `/etc` 允许选择路径，但只能支持 [AEM Forms到AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html#paths-of-various-aem-forms-specific-assets). 有关所有其他用例，请参阅 [常见存储库重组](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html#restructuring) 了解有关存储库重构的更多信息。 |
| MongoDB中的节点属性值 | 存储在MongoDB中的节点属性值不能超过16MB。 这由MongoDB强制执行。 如果属性值大于此限制，则摄取将失败。 运行提取之前，请运行此 [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) 脚本。 查看所有大型属性值并验证是否需要它们。 超过16MB的需要转换为二进制值。 |

## 后续内容 {#whats-next}

在查看了先决条件并确定您能否在迁移项目中使用内容传输工具后，请参阅 [使用内容传输工具的准则和最佳实践](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
