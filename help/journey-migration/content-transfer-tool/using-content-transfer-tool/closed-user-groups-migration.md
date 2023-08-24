---
title: 迁移封闭用户组
description: 本页提供了在迁移到Adobe Experience Manager as a Cloud Service内容后启用封闭用户组所需的特别注意事项。
hide: true
hidefromtoc: true
source-git-commit: 9da813d39d154e81da5b9814aa86b8318dc0bb3a
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 9%

---

# 迁移封闭用户组 {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="封闭用户组的迁移"
>abstract="封闭用户组 (CUG) 的迁移当前需要少量检查和步骤以使其在迁移后正常发挥作用。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html" text="AEM 中的封闭用户组"

目前，封闭用户组(CUG)需要一些额外的步骤才能在迁移的目标环境中正常运行。  本文档将介绍此方案，以及要求它们以预期方式保护节点所需的步骤。

## 组迁移

如果主体（包括组）通过内容的ACL与迁移的内容相关联，则它们会自动包含在迁移到Adobe Experience Manager as a Cloud Service的操作中。

## 迁移中的封闭用户组

当前，关联的组 *仅限* 使用封闭用户组(CUG)策略时 *非* 自动包含在摄取中。 如上所述，如果它们通过ACL与任何内容相关联，则将迁移它们。 应在上线之前验证组及其成员是否存在。 主体报表是通过“引入作业”视图下载的，可用于查看相关组是否包括，或是否包括，因为它不在ACL中。 如果组不存在，则应在创作实例中创建该组（包括添加相应成员），并激活该组以使它存在于发布实例上。 可使用在源上创建的包来完成此操作。

最后，必须触发流程，并设置属性以启用CUG。 为此，请重新发布与CUG策略关联的所有页面。 这将校准Publish实例以跟踪策略。

这将在“发布”上启用CUG策略，并且内容将只能由那些经过身份验证的用户（与策略关联的组的成员）访问。

## 主动开发

迁移团队正在努力使CUG策略自动迁移并正常运行，而无需在摄取内容后执行任何其他步骤。
在尝试上线之前，建议在任何测试流程中包含CUG功能。

## 摘要

总之，以下是迁移后启用CUG的步骤：

1. 确保在迁移后，发布上存在CUG策略中使用的每个组。
   - 如果某个组包含在迁移内容的ACL中，则该组可能已存在。
   - 如果不包含，请使用包将其安装在目标实例上（或在其中手动创建），并激活它及其成员。 然后，验证它在Publish上是否存在。
1. 重新发布与CUG策略关联的所有页面，确保通过先编辑页面等方法发布该策略。 重新发布所有这些组件很重要。
   - 重新发布所有页面后，验证每个受CUG保护的页面的功能。

