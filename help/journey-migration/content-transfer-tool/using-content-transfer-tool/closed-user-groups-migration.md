---
title: 迁移封闭用户组
description: 了解在将内容迁移到Adobe Experience Manager as a Cloud Service后启用封闭用户组所需的特殊注意事项。
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
source-git-commit: 29ffb48d23b4a2fe4973b005c98c5720b4196367
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 10%

---

# 迁移封闭用户组 {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="封闭用户组的迁移"
>abstract="封闭用户组 (CUG) 的迁移当前需要少量检查和步骤以使其在迁移后正常发挥作用。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=zh-Hans" text="AEM 中的封闭用户组"

目前，封闭用户组(CUG)需要一些额外的步骤才能在迁移的目标环境中正常运行。 本文档将介绍此方案，以及要求它们以预期方式保护节点所需的步骤。

## 组迁移

如果主体（包括组）通过内容的ACL与迁移的内容相关联，则它们会自动包含在迁移到Adobe Experience Manager as a Cloud Service的操作中，如果它们在该内容的CUG策略中被引用，则它们也会包含在内。

## 迁移中的封闭用户组

应在上线之前验证组及其成员是否存在。 通过“引入作业”视图下载的“主体报表”可用于查看相关组是否包括，或是否包括，因为它不在ACL或CUG策略中。

接下来，必须触发进程，并且必须设置属性以启用CUG。 为此，请重新发布与CUG策略关联的所有页面。 这将校准Publish实例以跟踪策略。

这会在发布上启用CUG策略，并且内容仅供那些是与策略关联的组的经过身份验证的用户访问。

## 摘要

总之，以下是迁移后启用CUG的步骤：

1. 确保在迁移后，发布上存在CUG策略中使用的每个组。
   - 如果某个组包含在迁移内容的CUG策略中，或包含在该内容的ACL中，则该组可能存在。
   - 如果不包含，请使用包将其安装在目标实例上（或在其中手动创建），并激活它及其成员。 然后，验证它在Publish上是否存在。
1. 重新发布与CUG策略关联的所有页面，确保通过先编辑页面等方法发布这些页面。 重新发布所有这些内容很重要。
   - 重新发布所有页面后，验证每个受CUG保护的页面的功能。
