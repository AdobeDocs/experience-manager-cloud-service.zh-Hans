---
title: 内容转移工具的先决条件
description: 熟悉内容传输工具的先决条件
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
feature: Migration
role: Admin
source-git-commit: 3e3d018dfd4babce9abef858e487bf1c116ed3a6
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 13%

---


# 内容转移工具的先决条件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="有关使用内容转移工具的重要注意事项"
>abstract="查看有关使用内容转移工具的重要注意事项，包括 Java™ 和 AEM 版本、支持的数据存储类型、用户组注意事项等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=zh-Hans" text="有关使用内容转移工具的重要注意事项"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=zh-Hans#best-practices" text="最佳实践和准则"

下表总结了使用内容传输工具的先决条件。

请查阅下面列出的所有注意事项：

| 注意事项 | 当前支持的内容 |
|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AEM 版本 | 内容传输工具只能在AEM 6.3或更高版本上运行。 |
| 区段存储的大小 | 当前支持现有存储库，其JCR节点数小于7.5亿，在&#x200B;*作者*&#x200B;上最大为500 GB（在线压缩大小），在&#x200B;*发布*&#x200B;上最大为50 GB。 通过Adobe客户关怀部门创建支持工单，以便您能够讨论超出这些限制的区段存储大小选项。 |
| 内容存储库的总大小&#x200B;<br>*（区段存储+数据存储）* | 内容传输工具旨在为文件数据存储类型传输高达20 TB的内容。 当前不支持任何大于20 TB的内容。 与Adobe客户关怀部门一起创建支持工单，以便您能够讨论大于20 TB内容的选项。 <br>要显着加快大型存储库的内容传输过程，可以使用可选的[预复制](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=zh-Hans#setting-up-pre-copy-step)步骤。 此过程适用于文件数据存储、Amazon S3和Azure数据存储类型的数据存储。 对于Amazon S3和Azure数据存储，支持大于20 TB的存储库大小。 |
| Lucene索引总大小 | 支持Lucene索引总大小最大为25 GB，不包括`/oak:index/lucene`和`/oak:index/damAssetLucene`。 通过Adobe客户关怀创建支持工单，以便您能够讨论超出此限制的索引大小选项。 |
| 不可变路径中的内容 | 内容传输工具无法用于迁移不可变路径中的内容。 若要从`/etc`传输内容，您可以选择某些`/etc`路径，但仅支持将[AEM Forms传输到AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=zh-Hans#paths-of-various-aem-forms-specific-assets)。 对于所有其他用例，请参阅[通用存储库重构](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html?lang=zh-Hans)，了解有关存储库重构的更多信息。 |
| MongoDB中的节点属性值 | MongoDB中存储的节点属性值不能超过16 MB。 此规则由MongoDB强制执行。 如果属性值大于此限制，则摄取失败。 运行提取之前，请运行此[oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar)脚本。 查看所有大型属性值，并验证是否需要它们。 超过16 MB的数据必须转换为二进制值。 |

## 后续内容 {#whats-next}

在查看了先决条件并确定是否可以在迁移项目中使用内容传输工具后，请参阅[使用内容传输工具的准则和最佳实践](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=zh-Hans)。