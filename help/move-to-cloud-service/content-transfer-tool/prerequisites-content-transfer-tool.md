---
title: 内容传输工具的先决条件
description: 内容传输工具的先决条件
exl-id: ef6d0e1a-0ed2-4485-adab-df6e0cf3ac4d
source-git-commit: bf69ee0a033412e632236975cc772b91c554fd87
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---

# 内容传输工具的先决条件 {#prerequisites}

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
| AEM 版本 | 内容传输工具只能在AEM 6.3或更高版本上运行。 要将内容传输工具与AEM 6.2或更早版本结合使用，需要将内容存储库就地升级到AEM 6.5。 无需将代码升级到AEM 6.5即可实现此目的。 |
| 区段存储的大小 | 当前支持&#x200B;*Author*&#x200B;上最高83 GB， *Publish*&#x200B;上最高31 GB。 与Adobe客户关怀团队一起创建支持票证，以讨论区段存储大小超过这些限制的选项。 |
| 内容存储库的总大小&#x200B;<br>*（区段存储+数据存储）* | 内容传输工具旨在为文件数据存储类型的数据存储传输高达10 TB的内容。 当前不支持任何高于10 TB的数据。 与Adobe客户关怀团队一起创建支持票证，以讨论大于10 TB的内容选项。 <br>对于Amazon S3和Azure Data Store类型的数据存储，可使用可选的 [](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) 复制前步骤来显着加快内容传输过程，并支持大于10TB的数据存储大小。 |
| 不可变路径中的内容 | 内容传输工具不能用于迁移不可变路径中的内容。 要从`/etc`传输内容，只允许选择某些`"/etc"`路径，但仅支持将[AEM Forms作为Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets)传输到AEM Forms。 有关所有其他用例，请参阅[通用存储库重组](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) ，了解有关存储库重组的更多信息。 |

## 下一步 {#whats-next}

查看先决条件并确定是否可以在迁移项目中使用内容传输工具后，请在使用内容传输工具时参阅[其他最佳实践和注意事项](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md)。
