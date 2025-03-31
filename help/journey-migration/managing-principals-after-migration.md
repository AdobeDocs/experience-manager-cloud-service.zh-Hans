---
title: 迁移后管理主体
description: 学习如何在 IMS 和 AEM 中设置用户和群组
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: 50c8dd725e20cbd372a7d7858fc67b0f53a8d6d4
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 81%

---

# 迁移后管理主体 {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="迁移后管理主体"
>abstract="学习如何在 IMS 和 AEM 中设置用户和群组"

本文档介绍了客户在 IMS 和 AEM 中设置其用户和群组以将其与 AEM as a Cloud Service 环境一同使用时应采取的高级步骤。

有关组迁移和每次摄取时可用的主体迁移报告的信息，请参阅[组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)。

有关在 Admin Console 中使用批量组和用户文件的指南，请参阅[使用 CTT 后将主体批量上传到 IMS](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md)。

## 管理主体 {#managing-principals}

对于 AEM as a Cloud Service，必须主要使用 Admin Console 来管理用户和群组。当考虑迁移时，其中一些任务可以在内容迁移发生之前执行。本质上，在这些主要任务组中

* 在 IMS 中创建用户和群组
* 将用户分配到 IMS 中的群组
* 将 IMS 组分配给 AEM 群组（如有必要）

前两个可以在内容迁移之前或之后进行。这些步骤仅影响 IMS 中的用户和群组，可能包括与外部 IDP（例如 Active Directory 或 LDAP）的集成。这些步骤在[使用 Admin Console 管理 IMS 中的主体](/help/journey-migration/managing-principals.md)中有所说明。

在将内容迁移到 AEM as a Cloud Service 环境后，就可以执行第三步。

### 迁移群组

在迁移的引入阶段，如果群组需要满足迁移内容的 ACL 或 CUG 策略，则会迁移群组。请参阅[迁移群组](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)，以了解更多详情。

迁移的组(不是由Assets收藏集或专用文件夹创建创建的组 — 请参阅下面的收藏集和专用文件夹)配置为IMS组。  这意味着在 IMS 中创建的任何同名组（例如通过 Admin Console 创建的组）都将链接到 AEM 中的群组，并且 IMS 组的成员用户也将会成为 AEM 中组的成员。为了实现这种链接，还必须首先在 IMS 中创建该群组。使用 Admin Console 在 AEM 实例中单独或批量创建群组，如[使用 Admin Console 管理 IMS 中的主体](/help/journey-migration/managing-principals.md)中所述。

使用 AEM 安全性 UI 将 IMS 组分配给本地 AEM 群组。为此，前往 AEM 中的“工具”页面，单击“安全性”，然后选择群组。

### IMS 用户

由于用户未迁移，因此必须在 IMS 中创建用户，以便在 AEM 中使用它们。有几种方法可以实现这一点，但重要的是将创建的用户分配给正确的 IMS 群组，以便用户能够像在以前的 AEM 系统中一样访问内容。可用于此目的的工具之一是 Admin Console 中的批量上传功能；使用批量上传器上传用户及其必须加入的群组。在执行此操作之前，必须首先在 IMS 中创建群组，如上所述。

要了解每个用户应属于哪些组，您可以使用用户报告（参见[群组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)）。此报告列出了每个用户应所属的群组，并且此列表通常会包含在用于 Admin Console 批量上传功能的批量用户输入文件中。

### 收藏集和专用文件夹

创建Assets收藏集或专用文件夹也会自动创建一些组，以管理对该Assets内容的访问。  如果迁移内容中提到了这些组，则会迁移这些组，但是它们未配置为直接链接到IMS组；在AEM中，它们仍是“本地组”，并且无法通过IMS对其进行管理。

由于这些群组不在 IMS 中，因此无法使用批量上传工具来创建用户作为其直接成员。同样在 AEM 中的 IMS 用户也可以单独添加到这些群组中，但批量添加需要额外的步骤。这里有一种方法可以实现这一点：
* 在Admin Console/IMS中新建一个或多个组以访问收藏集/专用文件夹，并为AEM配置这些文件夹。
* 以组成员的身份登录，以便在 AEM 中创建群组。
* 对于已迁移的收藏集或专用文件夹，使用Assets UI将新组添加为编辑器/所有者/查看器。
* 将用户添加（或批量上传）到 Admin Console 中的新群组。
* 当用户首次登录时，他们的IMS用户将在AEM中创建，并且他们应有权访问新组，从而有权访问原始收藏集或专用文件夹组。

注意：要进行批量用户分配，必须使用上述步骤在 IMS 中创建用户；IMS 中已存在的用户无法通过批量上传再次创建，但可以使用批量编辑器进行这类更改（请参阅 [Admin Console 批量用户上传](https://helpx.adobe.com/cn/enterprise/using/bulk-upload-users.html)中的&#x200B;**编辑用户详细信息**）。
