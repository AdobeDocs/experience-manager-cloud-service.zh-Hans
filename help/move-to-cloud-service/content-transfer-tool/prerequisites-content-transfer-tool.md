---
title: 内容传输工具的先决条件
description: 内容传输工具的先决条件
source-git-commit: f70959efd9d0382c083ac05b9ccd63cf79947bc2
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# 内容传输工具的先决条件 {#prerequisites}

下表概述了使用内容传输工具的先决条件。

请查看下面列出的所有注意事项：

| 注意事项 | 当前支持的内容 |
|--- |--- |
| AEM 版本 | 内容传输工具只能在AEM 6.3或更高版本上运行。 要将内容传输工具与AEM 6.2或更早版本结合使用，需要将内容存储库就地升级到AEM 6.5。 无需将代码升级到AEM 6.5即可实现此目的。 |
| 区段存储的大小 | 内容传输工具当前支持&#x200B;*Author*&#x200B;上最多83 GB，在&#x200B;*Publish*&#x200B;上最多31 GB。 |
| 内容存储库的总大小&#x200B;<br>*（内容存储+数据存储）* | 内容传输工具可传输多达10 TB的内容。 当前不支持任何高于10 TB的数据。 与Adobe客户关怀团队一起创建支持票证，以讨论大于10 TB的内容选项。 |
| 不可变路径中的内容 | 内容传输工具无法迁移不可变路径（如`“/etc”`）中的内容。 <br>请参阅常用 [存储库重](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) 组，了解有关存储库重组和工作流模型的更多信息。 |

## 下一步是什么{#whats-next}

查看先决条件后，您现在可以了解如何运行内容传输工具。 有关更多详细信息，请参阅[使用内容传输工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) 。
