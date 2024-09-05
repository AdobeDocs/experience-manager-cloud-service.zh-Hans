---
title: 管理主体
description: 管理迁移主体，使用Admin Console
exl-id: a75598d0-8f59-466b-984e-dfe527388c2a
source-git-commit: a5bec2c05b46f8db55762b7ee1f346f3bb099d24
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 6%

---

# 管理主体 {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="管理主体"
>abstract="了解在内容迁移期间或之后管理用户需要做什么"

在将内容传输到AEM as a Cloud Service云环境之前，可以在Admin Console上执行几项任务。  它们是：创建用户、创建组并将用户分配给组；这些用户和组将存在于Adobe的Identity Management服务IMS中，该服务用于管理所有基于Adobe云的服务的用户和组。

### 在Admin Console中创建组及其用户

[使用AEM承担者的Admin Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up)提供了有关如何在IMS中创建用户和组，以及如何同时或稍后将用户添加到组的详细说明。  该文档包括三个用于创建它们的选项：通过Admin Console手动创建、通过Admin Console通过CSV上传以及通过User Sync Tool创建。

手动选项允许您一次创建一个组或用户；CSV上传允许您一次创建和链接多个用户和组；用户同步工具允许您使用现有IDP创建和管理IMS用户和组。

用户使用IMS登录AEM后，将创建用户的AEM表示形式。  此外，用户所在的任何IMS组都将在AEM中创建等效的AEM组。  这些IMS创建的AEM用户和组仍主要使用Admin Console进行管理。

内容迁移完成后，IMS组通常需要额外进行一些配置，以便用户能够访问迁移的内容。  请参阅迁移后[迁移主体](/help/journey-migration/managing-principals-after-migration.md)

另请参阅[教程、AEM用户、组和权限](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions)，了解有关AEM和IMS用户和组如何集成和管理的更多信息。
