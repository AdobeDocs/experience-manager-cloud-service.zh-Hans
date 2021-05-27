---
title: 预览内容
description: 了解如何在上线之前使用AEM预览服务预览内容。
source-git-commit: 9b4ac173c55380cbc06de64677470818aa801df4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# 预览内容{#previewing-content}

>[!NOTE]
>
>“预览”功能是2021.5.0版本的一部分，将在未来几周逐步推出。

AEM提供了“站点预览”服务，旨在让开发人员和内容作者在网站到达发布环境之前预览网站的最终体验并公开提供。

它有助于预览在创作环境中不可见的页面体验，如页面过渡和其他仅发布端内容。

## 将内容发布到预览{#publishing-content-to-preview}

您可以使用管理的发布UI将内容发布到预览服务，如下所示：

1. 选择要在站点控制台中进行预览的一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮
1. 在下面的向导中，选择&#x200B;**预览**&#x200B;作为目标

   ![托管出版物](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 单击&#x200B;**Next**，然后单击&#x200B;**Publish**&#x200B;以确认。

请参阅预览内容，将&#x200B;**preview**&#x200B;附加到生产实例的发布URL。 URL的构建方式如下：

```
https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
```

有关如何获取环境URL的更多信息，请参阅[管理环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en)。

