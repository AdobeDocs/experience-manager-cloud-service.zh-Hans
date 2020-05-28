---
title: 迁移后阶段
description: 迁移后阶段
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---


# 迁移后 {#post-migration}

在迁移后阶段，您应确保清理临时文件，检查持续开发的最佳实践并管理日志。

以下工具可用于AEM作为云服务环境进行疑难解答：

* **开发人员控制台**
* **CRXDE Lite**
* **管理日志**


## 开发人员控制台 {#developer-console}

在开发人员控制台中，可以将AEM作为云服务开发人员环境进行调试，以用于开发、阶段和生产环境。

请参阅 [将AEM作为云服务实施](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) ，进一步了解开发工具。

## CRXDE Lite {#crxde-lite}

作为用户，您可以在开 **发环境访问** CRXDE Lite，但不能在舞台或生产上访问。

>[重要]
>写入不可改变的存储库(如 `/libs` 和在 `/apps` 运行时写入)将导致错误。 此外，作为客户，您将无权访问用于分阶段和生产环境的开发人员工具。

请参阅 [使用CRXDE Lite开发](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) ，了解如何使用CRXDE Lite开发AEM应用程序。

## 管理日志 {#managing-logs}

用户可以访问选定列表的可用日志文件环境。

请参阅 [访问和管理日志](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) ，了解如何通过UI或通过云管理器从API访问和管理日志。

### 其他支持 {#additional-support}

如果您对访问云服务有任何疑问，请与Adobe代表或Adobe AEM CQ支持门户联系。
