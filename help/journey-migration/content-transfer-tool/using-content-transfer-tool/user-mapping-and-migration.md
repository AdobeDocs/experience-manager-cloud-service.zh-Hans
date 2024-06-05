---
title: 用户映射和主体迁移
description: AEMas a Cloud Service中的用户映射和主体迁移概述。
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 5%

---

# 用户映射和主体迁移 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用户迁移"
>abstract="内容转移工具可帮助您将用户和组从现有 Adobe Experience Manager (AEM) 系统移动到 AEM as a Cloud Service。必须映射现有用户，以便他们可以通过其 IMS ID 登录。"

>[!NOTE]
>有关用户映射工具的早期版本，请参阅 [旧版文档](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## 简介 {#introduction}

在过渡到Adobe Experience Manager (AEM)as a Cloud Service的过程中，用户和组（或“承担者”）必须从现有AEM系统迁移到AEMas a Cloud Service。 此任务由内容传输工具完成。

AEMas a Cloud Service的一项重大更改是完全集成使用AdobeID来访问创作层。 此过程需要使用 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 用于管理用户和用户组。 用户配置文件信息集中存储在AdobeIdentity Management System (IMS)中，可通过所有Adobe云应用程序提供单点登录。 有关更多详细信息，请参阅 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). 由于此更改，现有用户必须映射到其IMS ID，以便他们可以使用其IMS配置文件访问AEMaaCS。 由于传统AEM中的组与IMS中的组存在根本上的不同，因此不会映射组，但在迁移完成后必须协调两组组。

## 主体迁移详细信息 {#principal-migration-detail}

内容传输工具和Cloud Acceleration Manager会将与正在迁移的内容关联的任何主体迁移到云系统。 内容传输工具通过在提取过程中从源AEM系统复制所有主体来执行此操作。 然后，CAM摄取将仅选择和迁移与正在摄取的内容关联的主体。 如果主体位于已迁移内容的ACL或CUG策略上，则该主体及其所在的所有组及其祖先（父）组都将迁移。 此外，如果内容上的承担者是一个组，则其所有后代（子）组和用户也将被迁移。

## 用户映射详细信息 {#user-mapping-detail}

AEM用户可映射到具有相同电子邮件地址的相应Adobe IMS用户。 此映射可以在CTT中自动完成（在提取步骤期间），并且可以在开始提取之前通过切换来控制映射是否完成。 此切换的默认设置可由用户在开始提取时覆盖。

* 如果源系统是一个创作实例，则默认情况下，执行映射的选择是 _日期_，因为这是推荐的流程。
* 如果源系统是发布实例，则默认情况下，执行映射的选择是 _关_，因为通常不会迁移用户或在发布实例上使用用户；或者，如果使用了用户，通常会对他们使用不同的身份验证系统（即，非IMS）。

无论用户在提取期间是否进行映射，如果用户在提取期间与正在迁移的内容相关联，则他们会与组一起迁移到云系统。

## 映射和迁移用户时的重要注意事项 {#important-considerations}

### 特殊情况 {#exceptional-cases}

将记录以下特定案例：

1. 如果用户在 `profile/email` 字段 *jcr* 节点，相关用户可能会被迁移，但未被映射。 即使电子邮件地址用作登录的用户名，也会发生这种情况。
2. 如果用户被禁用，则它将被视为与其他用户相同；它将作为正常用户被映射和迁移，并在云实例上保持禁用状态。
3. 如果源AEM实例和目标AEM Cloud Service实例上存在具有任何唯一性约束数据（rep：principalName、rep：authorizableId、jcr：uuid或rep：externalId）的承担者，则不会迁移有问题的承担者，并且云系统上以前存在的承担者将保持不变。 这将记录在“主体迁移报告”中。
4. 如果用户未通过用户映射映射到IMS，则IMS将不能识别Cloud AEM系统上的用户配置文件；在这种情况下，如果用户通过IMS登录，将在AEM上创建一个新的（重复的）配置文件，但该配置文件不会包含用户以前的配置文件信息。 原始用户配置文件将存在于云AEM系统上，但他们将无法通过IMS登录到原始用户配置文件，只能使用传统的AEM方法（本地登录）。 因此，强烈建议为所有作者迁移映射所有用户。

## 其他注意事项 {#additional-considerations}

* 如果设置 **请擦除云实例上的现有内容后再引入** 设置，将删除以前传输到Cloud Service实例的主体以及整个现有存储库；将创建一个新存储库，并在其中摄取内容。 此过程还会重置所有设置，包括目标Cloud Service实例的权限，对于添加到中的管理员用户，此过程同样有效。 **管理员** 组。 必须将管理员用户重新添加到 **管理员** 组以检索CTT/CAM摄取的访问令牌。
* 执行非划出提取时(**擦除现有内容** 如果未传输内容，因为在上次传输后内容未发生更改，则与该内容关联的用户和组也不会传输。 即使在源系统上更改了用户和组，此规则仍然适用。 这是因为用户和组仅随其关联的内容一起迁移。 因此，源系统上任何新到组的主体都不会迁移，除非它们属于正在迁移的其他组，或者位于正在迁移的不同内容的ACL中。 要随后迁移这些承担者，请考虑使用包，或从目标中删除承担者并重新迁移相关内容（使用覆盖内容进行提取，使用划出内容进行摄取）。
* IMS中不允许存在重复的电子邮件地址，但在AEM中允许存在重复的电子邮件地址（本地和云中）。 用户可以使用其电子邮件地址通过IMS登录AEM，并且他们将登录到IMS引用的用户配置文件。
* 请参阅 [迁移封闭用户组](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) 有关在封闭用户组(CUG)策略中使用的主体的其他注意事项。

## 最终摘要和报告 {#final-report}

成功完成提取和引入后，将生成一个报告，其中显示主体迁移详细信息。 请参阅 [如何验证主体迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) 了解详细信息。
