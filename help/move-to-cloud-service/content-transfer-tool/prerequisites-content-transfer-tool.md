---
title: 内容传输工具的先决条件
description: 内容传输工具的先决条件
source-git-commit: c760b97cdb565244cf20f5193de3e3ebab1579ad
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# 内容传输工具的先决条件 {#prerequisites}

下表总结了使用内容传输工具之前的先决条件。 请查看下面列出的所有注意事项：

| 注意事项 | 当前支持的内容 |
|--- |--- |
| AEM 版本 | 内容传输工具只能在AEM 6.3或更高版本上运行。 要将内容传输工具与AEM 6.2或更早版本结合使用，需要将内容存储库就地升级到AEM 6.5。 无需将代码升级到AEM 6.5即可实现此目的。 |
| 区段存储的大小 | 内容传输工具当前支持&#x200B;*Author*&#x200B;上最多83 GB，在&#x200B;*Publish*&#x200B;上最多31 GB。 |
| 内容存储库的总大小（内容存储+数据存储） | 内容传输工具可传输多达10 TB的内容。 当前不支持任何高于10 TB的数据。 与Adobe客户关怀团队一起创建支持票证，以讨论大于10 TB的内容选项。 |
| 不可变路径中的内容 | 内容传输工具无法迁移不可变路径（如`“/etc”`）中的内容。 请参阅[通用存储库重组](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) ，了解有关存储库重组和工作流模型的更多信息。 |