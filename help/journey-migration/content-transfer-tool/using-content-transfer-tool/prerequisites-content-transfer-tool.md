---
title: 内容转移工具的先决条件
description: 内容转移工具的先决条件
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: 4ccebe19d38f1ece58ea7170344ef2fd86a513d2
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 4%

---

# 内容转移工具的先决条件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="使用内容传输工具的重要注意事项"
>abstract="查看有关使用内容传输工具的重要注意事项，包括Java和AEM版本、支持的数据存储类型、用户组注意事项等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="使用内容传输工具的重要注意事项"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="最佳实践和准则"

下表概述了使用内容传输工具的先决条件。

请查看下面列出的所有注意事项：

| 注意事项 | 当前支持的内容 |
|--- |--- |
| AEM 版本 | 内容传输工具只能在AEM 6.3或更高版本上运行。 |
| 区段存储的大小 | 现有存储库，其JCR节点数少于5500万，且在 *作者* 和50 GB on *发布* 当前支持。 与Adobe客户关怀团队一起创建支持票证，以讨论区段存储大小超过这些限制的选项。 |
| 内容存储库的总大小 <br>*（区段存储+数据存储）* | 内容传输工具旨在为文件数据存储类型的数据存储传输高达20 TB的内容。 当前不支持任何高于20 TB的数据。 与Adobe客户关怀团队一起创建支持票证，以讨论大于20 TB的内容选项。 <br>为显着加快大型存储库的内容传输过程，可选 [预拷贝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) 步骤。 这适用于文件数据存储、Amazon S3和Azure数据存储类型的数据存储。 对于Amazon S3和Azure数据存储，支持大于20TB的存储库大小。 |
| Lucene索引总大小 | 最大Lucene索引总大小为25GB，不包括 `/oak:index/lucene` 和 `/oak:index/damAssetLucene` 当前支持。 与Adobe客户关怀团队一起创建支持票证，以讨论索引大小超过此限制的选项。 |
| 节点名称长度 | 当节点父路径大于=（等于或大于）350字节时，节点名称的长度必须小于或等于150字节。 这些节点名称必须缩短为&lt;= 150字节，才能在AEMas a Cloud Service中由文档节点存储支持。 如果未修复这些长节点名称，则摄取将失败。 |
| 不可变路径中的内容 | 内容传输工具不能用于迁移不可变路径中的内容。 从 `/etc` 仅限于 `/etc` 允许选择路径，但仅支持 [AEM Forms至AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). 有关所有其他用例，请参阅 [公共存储库重组](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) 以了解有关存储库重组的更多信息。 |
| MongoDB中的节点属性值 | MongoDB中存储的节点属性值不能超过16MB。 这由MongoDB强制执行。 如果存在大于此限制的属性值，则摄取将失败。 运行提取之前，请运行此 [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) 脚本。 检查所有大属性值，并验证是否需要它们。 超过16MB的数据需要转换为二进制值。 |

## 下一步 {#whats-next}

查看先决条件并确定是否可以在迁移项目中使用内容传输工具后，请参阅 [使用内容传输工具的准则和最佳实践](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
