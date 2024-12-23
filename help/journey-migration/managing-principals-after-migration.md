---
title: 迁移后管理主体
description: 学习如何在 IMS 和 AEM 中设置用户和群组
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: a5bec2c05b46f8db55762b7ee1f346f3bb099d24
workflow-type: ht
source-wordcount: '773'
ht-degree: 100%

---

# 迁移后管理主体 {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="迁移后管理主体"
>abstract="学习如何在 IMS 和 AEM 中设置用户和群组"

本文档介绍了客户在 IMS 和 AEM 中设置其用户和群组以将其与 AEM as a Cloud Service 环境一同使用时应采取的高级步骤。

## 管理主体 {#managing-principals}

对于 AEM as a Cloud Service，必须主要使用 Admin Console 来管理用户和群组。当考虑迁移时，其中一些任务可以在内容迁移发生之前执行。本质上，在这些主要任务组中

* 在 IMS 中创建用户和群组
* 将用户分配到 IMS 中的群组
* 将 IMS 组分配给 AEM 群组（如有必要）

前两个可以在内容迁移之前或之后进行。这些步骤仅影响 IMS 中的用户和群组，可能包括与外部 IDP（例如 Active Directory 或 LDAP）的集成。这些步骤在[使用 Admin Console 管理 IMS 中的主体](/help/journey-migration/managing-principals.md)中有所说明。

在将内容迁移到 AEM as a Cloud Service 环境后，就可以执行第三步。

### 迁移群组

在迁移的引入阶段，如果群组需要满足迁移内容的 ACL 或 CUG 策略，则会迁移群组。请参阅[迁移群组](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)，以了解更多详情。

迁移的组（不是通过创建资产收藏集而创建的组 - 请参阅下面的收藏集）被配置为 IMS 群组。这意味着在 IMS 中创建的任何同名组（例如通过 Admin Console 创建的组）都将链接到 AEM 中的群组，并且 IMS 组的成员用户也将会成为 AEM 中组的成员。为了实现这种链接，还必须首先在 IMS 中创建该群组。使用 Admin Console 在 AEM 实例中单独或批量创建群组，如[使用 Admin Console 管理 IMS 中的主体](/help/journey-migration/managing-principals.md)中所述。

使用 AEM 安全性 UI 将 IMS 组分配给本地 AEM 群组。请参阅[创建和配置群组](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-groups#edit-a-group)。虽然本文档适用于 AEM 6.5，但它也适用于将组添加到 AEM as a Cloud Service 中的其他群组。

### IMS 用户

由于用户未迁移，因此必须在 IMS 中创建用户，以便在 AEM 中使用它们。有几种方法可以实现这一点，但重要的是将创建的用户分配给正确的 IMS 群组，以便用户能够像在以前的 AEM 系统中一样访问内容。可用于此目的的工具之一是 Admin Console 中的批量上传功能；使用批量上传器上传用户及其必须加入的群组。在执行此操作之前，必须首先在 IMS 中创建群组，如上所述。

要了解每个用户应属于哪些组，您可以使用用户报告（参见[群组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)）。此报告列出了每个用户应所属的群组，并且此列表可包含在 Admin Console 批量上传功能的输入文件中。

### 收藏集

创建资产收藏集还会自动创建一些组来管理对该收藏集的访问。如果这些组在迁移的集合中被提及，则会迁移这些群组，但它们不会被配置为直接关联到 IMS 组；在 AEM 中，它们仍然是“本地组”，并且不能通过 IMS 进行管理。

由于这些群组不在 IMS 中，因此无法使用批量上传工具来创建用户作为其直接成员。同样在 AEM 中的 IMS 用户也可以单独添加到这些群组中，但批量添加需要额外的步骤。这里有一种方法可以实现这一点：
* 在 Admin Console/IMS 中创建一个或多个新群组以访问收藏集并为 AEM 配置它们。
* 以组成员的身份登录，以便在 AEM 中创建群组。
* 对于已迁移的收藏集，使用资产收藏集 UI 将新组添加为编辑器/所有者/查看者。
* 将用户添加（或批量上传）到 Admin Console 中的新群组。
* 当用户首次登录时，他们的 IMS 用户会在 AEM 中创建，并且他们应该能够访问新群组，从而访问原始收藏集群组。

注意：对于批量分配用户，必须使用上述步骤在 IMS 中创建用户；IMS 中已经存在的用户无法通过批量上传再次创建。
