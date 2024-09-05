---
title: 迁移后管理主体
description: 学习如何在 IMS 和 AEM 中设置用户和群组
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: a5bec2c05b46f8db55762b7ee1f346f3bb099d24
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 5%

---

# 迁移后管理主体 {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="迁移后管理主体"
>abstract="学习如何在 IMS 和 AEM 中设置用户和群组"

本文档介绍了客户应采取的高级步骤，以便在IMS和AEM中设置用户和组以使用其AEM as a Cloud Service环境。

## 管理主体 {#managing-principals}

对于AEM as a Cloud Service，必须主要使用Admin Console管理用户和组。  考虑迁移时，可以在内容迁移发生之前执行其中的某些任务。  基本上，这些主要任务组中的

* 在IMS中创建用户和组
* 在IMS中将用户分配给组
* 将IMS组分配给AEM组（如有必要）

前两个可以在内容迁移之前或之后执行。  这些步骤仅影响IMS中的用户和组，可能包括与外部IDP（如Active Directory或LDAP）的集成。  使用Admin Console](/help/journey-migration/managing-principals.md)在IMS中管理承担者中介绍了这些步骤[。

将内容迁移到AEM as a Cloud Service环境后，可以执行第三步。

### 迁移组

在迁移的摄取阶段，如果需要组满足已迁移内容上的ACL或CUG策略，则会迁移这些组。  有关详细信息，请参阅[组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)。

已迁移的组(不是由Assets收藏集创建创建的组 — 请参阅下面的收藏集)配置为IMS组。  这意味着，在IMS中创建的任何同名组(例如，通过Admin Console)都将链接到AEM中的组，并且作为IMS组成员的用户也将成为AEM中的组的成员。  为了进行此链接，还必须首先在IMS中创建组。  使用Admin Console在AEM实例中单独或批量创建组，如[使用Admin Console管理IMS中的主体](/help/journey-migration/managing-principals.md)中所述。

使用AEM安全UI将IMS组分配给本地AEM组。  请参阅[创建和配置组](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-groups#edit-a-group)。  尽管本文档适用于AEM 6.5，但它也适用于将组添加到AEM as a Cloud Service中的其他组。

### IMS用户

由于不迁移用户，因此必须在IMS中创建这些用户，以便在AEM中使用它们。  虽然可通过多种方法做到这一点，但必须将创建的用户分配给正确的IMS组，以便这些用户能够像以前的AEM系统中一样访问其内容，这一点非常重要。  可用于此功能的工具之一是Admin Console中的批量上传功能；使用批量上传程序连同用户必须是其成员的组一起上传用户。  在执行此操作之前，必须首先在IMS中创建组，如上所述。

要了解每个用户应属于哪些组，您可以使用用户报告（请参阅[组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)）。  此报告列出了每个Admin Console应成为其成员的组，此列表可包含在User批量上传功能的输入文件中。

### 收藏集

创建Assets收藏集也会自动创建一些组以管理对该收藏集的访问。  如果迁移的收藏集中提到了这些组，则会迁移这些组，但它们未配置为直接链接到IMS组；在AEM中，它们仍是“本地组”，无法通过IMS对其进行管理。

由于这些组不在IMS中，因此无法使用批量上传工具将用户创建为其直接成员。  也可以将也位于AEM中的IMS用户单独添加到这些组中，但批量执行此操作需要额外的步骤。  下面是实现此操作的一种方法：
* 在Admin Console/IMS中新建一个或多个组以访问收藏集，并为AEM配置这些收藏集。
* 以组成员的身份登录，以便在AEM中创建组。
* 对于已迁移的收藏集，使用Assets收藏集UI将新组添加为编辑器/所有者/查看器。
* 在Admin Console中将用户添加（或批量上传）到新组。
* 当用户首次登录时，将会在AEM中创建其IMS用户，并且他们应该有权访问新组，从而有权访问原始收藏集组。

注意：对于批量分配用户，必须使用上述步骤在IMS中创建用户；无法通过批量上传再次创建IMS中已存在的用户。
