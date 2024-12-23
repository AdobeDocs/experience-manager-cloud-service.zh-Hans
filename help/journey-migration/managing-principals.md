---
title: 管理主体
description: 使用 Admin Console 管理迁移主体
exl-id: a75598d0-8f59-466b-984e-dfe527388c2a
source-git-commit: a5bec2c05b46f8db55762b7ee1f346f3bb099d24
workflow-type: ht
source-wordcount: '311'
ht-degree: 100%

---

# 管理主体 {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="管理主体"
>abstract="了解在内容迁移期间或之后管理用户需要做什么"

在将内容传输到 AEM as a Cloud Service 云环境之前，可以在 Admin Console 上执行一些任务。这些任务是：创建用户、创建组以及将用户分配到组；这些用户和组将存在于 IMS（Adobe 的身份管理服务）中，该服务用于管理所有 Adobe 基于云的服务的用户和组。

### 在 Admin Console 中创建组及其用户

[使用 Admin Console 管理 AEM 主体](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up)提供了有关如何在 IMS 中创建用户和组以及如何同时或稍后将用户添加到组的详细说明。该文档包括三个创建选项：通过 Admin Console 手动创建、通过 Admin Console 上传 CSV 创建以及通过用户同步工具创建。

手动选项允许您一次创建一个组或一个用户；CSV 上传允许您一次创建和关联多个用户和组；用户同步工具允许您使用现有的 IDP 来创建和管理 IMS 用户和组。

在用户使用 IMS 登录 AEM 后，就会创建该用户的 AEM 展现方案。此外，用户所在的任何 IMS 组都将在 AEM 中创建等效的 AEM 组。这些由 IMS 创建的 AEM 用户和组仍然主要通过 Admin Console 进行管理。

内容迁移完成后，IMS 组通常需要进行一些额外配置，以便用户可以访问迁移的内容。请参阅[迁移后迁移主体](/help/journey-migration/managing-principals-after-migration.md)

还请参阅[教程、AEM 用户、组和权限](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions)，了解有关如何集成和管理 AEM 和 IMS 用户和组的更多信息。
