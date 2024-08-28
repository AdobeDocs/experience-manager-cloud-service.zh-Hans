---
title: 迁移封闭用户组
description: 了解在将内容迁移到Adobe Experience Manager as a Cloud Service后启用封闭用户组所需的特殊注意事项。
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: 5b0dfb847a1769665899d6dd693a7946832fe7d1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 12%

---


# 迁移封闭用户组 {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="封闭用户组的迁移"
>abstract="封闭用户组 (CUG) 的迁移当前需要少量检查和步骤以使其在迁移后正常发挥作用。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html#" text="AEM 中的封闭用户组"

目前，封闭用户组(CUG)需要一些额外的步骤才能在迁移的目标环境中正常运行。 本文档将介绍此方案，以及要求它们以预期方式保护节点所需的步骤。

## 封闭用户组(CUG)的迁移

如果组通过所迁移内容的ACL或其CUG策略节点与所迁移内容相关联，则这些组会自动包含在向Adobe Experience Manager as a Cloud Service的CTT/CAM迁移中。 验证组及其成员是否存在应该在上线之前完成。 在CUG策略上引用的组在这里称为“CUG组”。

要在AEM as a Cloud Service中使用CUG，用户必须位于创作实例上并且是相关CUG组的成员。  这可以使用包完成，或者，如果CUG用户是IMS用户，则它们可能已存在。  然后，CUG用户必须成为AEM CUG组的成员。

要在Publish实例上启用CUG行为，
1. 必须激活CUG组(这会将它们及其成员复制到Publish实例)，并且
1. 必须发布受CUG策略保护的页面(这可以启用Publish实例并跟踪策略)。
1. 发布所有页面后，验证每个受CUG保护的页面的功能。

有关其他信息，请参阅[已关闭的用户组](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html#)。
