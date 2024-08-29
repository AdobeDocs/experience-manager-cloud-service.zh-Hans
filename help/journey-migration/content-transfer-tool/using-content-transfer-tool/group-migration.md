---
title: 组迁移
description: AEM as a Cloud Service中的组迁移概述。
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---


# 组迁移 {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="组迁移"
>abstract="内容传输工具可帮助您将组从现有Adobe Experience Manager (AEM)系统复制到AEM as a Cloud Service。"

>[!NOTE]
>有关用户映射工具的早期版本，请参阅[旧文档](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)。

## 简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="用户未迁移"
>abstract="内容传输工具不再迁移用户。 用户应在Admin Console中进行管理。"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="AEMAdmin Console文档"
>additional-url="https://adminconsole.adobe.com/" text="AEMAdmin Console"

在过渡到Adobe Experience Manager (AEM)as a Cloud Service的过程中，必须将组从现有AEM系统迁移到AEM as a Cloud Service。 此任务由内容传输工具完成。

AEM as a Cloud Service的一项重大更改是完全集成使用AdobeID来访问创作层。 此过程需要使用[Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)来管理用户和用户组。 用户配置文件信息集中存储在AdobeIdentity Management System (IMS)中，可通过所有Adobe云应用程序提供单点登录。 有关详细信息，请参阅[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management)。 由于此更改，用户首次通过IMS登录时将在AEM上自动创建。  因此，CTT不会将用户迁移到云系统。  必须将IMS用户放置到IMS组中，这些组可以是迁移组，也可以是放置在AEM组中且已获得访问正在迁移的AEM内容的权限的新组。  通过这种方式，云系统上的用户将拥有与其源AEM系统相同的访问权限。

## 组迁移详细信息 {#group-migration-detail}

内容传输工具和Cloud Acceleration Manager会将与要迁移的内容关联的任何组迁移到云系统。 内容传输工具通过在提取过程中从源AEM系统复制所有组来实现这一点。 然后，CAM摄取将仅选择和迁移某些组：

* 目标云系统中已经存在许多内置的组；这些组永远不会迁移。
* 任何内置组的直接成员组（在已迁移内容的ACL或CUG策略中直接或间接引用）都将进行迁移，以确保作为此类组直接或间接成员的用户能够保持对已迁移内容的访问权限。
* 如果某个组位于已迁移内容的ACL或CUG策略上，则将迁移该组。
* 其他组（如ACL或CUG策略中找不到的组、目标系统中已存在的组，以及目标系统中已存在任何唯一性受限数据的组）将不会迁移。

请注意，为某个组记录/报告的路径只是触发该组进行迁移的第一个路径，并且该组可能位于其他内容路径上。

大多数迁移的组都配置为由IMS管理。  这意味着IMS中具有相同名称的组将链接到AEM中的组，并且IMS组中的任何IMS用户都将成为AEM中的AEM用户和组的成员。  这允许这些用户根据组的ACL或CUG策略访问内容。

此IMS配置的例外情况是Assets收藏集创建的组。 在AEM上创建收藏集后，将创建组以访问该收藏集；此类组将迁移到云系统，但不会配置为由IMS管理。  要将IMS用户添加到这些组，必须在Assets UI的“组属性”页面中单独或集体地将这些用户添加为其他IMS组的一部分。


## 选择退出组迁移 {#group-migration-option}

CTT版本3.0.20及更高版本包含用于禁用组迁移的选项。  此操作在OSGI控制台中进行配置，如下所示：

* 打开OSGI配置`(http://<server> /system/console/configMgr)`
* 单击名为&#x200B;**内容传输工具提取服务配置**&#x200B;的配置
* 取消选中&#x200B;**在迁移中包含组**&#x200B;以禁用组迁移
* 单击&#x200B;**保存**&#x200B;以确保配置在服务器上已保存并处于活动状态

禁用此设置后，将不会迁移组，并且不会有主体迁移报告或用户报告。

## 用户报告 {#user-report}

在迁移过程中，不会迁移用户，但源系统上的用户 — 组关系将丢失，除非以某种方式捕获这些用户。  用户报表以文本格式在用户报表中捕获某些此类信息。 在该报表中，将报告每个用户（每行一个）及其所属的组列表（但未迁移的组不会放入此列表中），除非其组列表为空，在此情况下，不会显示用户。 与每个用户一起报告的组是用户直接或间接属于源系统的组；由于源系统中的组可能嵌套，而目标系统中的组却不是，因此此组列表支持IMS中新的扁平化组结构。

如果先进行划出，然后再进行非划出摄取，则用户列表中的组将包括这两个阶段中迁移的组。

除了每个用户的组之外，报告中还有一个字段，可以在其中为用户添加注释（报告中还详细描述了注释的含义）。  可能的注释包括：

* 直接在ACL中引用的用户在其注释部分中将有&#x200B;*注释 — A*，因为这不是推荐的使用案例或最佳实践。
* 作为内置组的直接成员的用户在其注释部分将具有&#x200B;*注释 — B*，因为这不是推荐的使用案例或最佳实践。

这些情况可以同时发生，并且与前几个情况相同。

用户报告添加到主体迁移报告的末尾（因此是其中的一部分）（请参阅下面的[最终摘要和报告](#final-summary-and-report)）。

## 其他注意事项 {#additional-considerations}

* 如果设置了&#x200B;**在摄取之前擦除云实例上的现有内容**，则以前传输到Cloud Service实例的组将随整个现有存储库一起删除；将创建一个内容摄取到的新存储库。 此过程还会重置所有设置，包括目标Cloud Service实例的权限，对于添加到&#x200B;**管理员**&#x200B;组的任何用户，此过程均为true。 必须将管理员用户重新添加到&#x200B;**管理员**&#x200B;组，以检索CTT/CAM摄取的访问令牌。
* 执行非擦除摄取时（取消设置&#x200B;**擦除现有内容**），如果由于上次传输后内容未更改而未传输内容，则与该内容关联的组也不会传输。 即使在源系统上更改了组，此规则仍然适用。 这是因为组仅随与其关联的内容一起迁移。 因此，在这种情况下，任何属于源系统上某个组的组都将不会迁移，除非这些组属于正在迁移的其他组，或者位于正在迁移的其他内容的ACL中。 要在以后迁移这些组，请考虑使用包，从目标中删除组并重新迁移相关内容，或使用划出摄取重新迁移。
* 在非划出提取期间，如果源AEM实例和目标AEM Cloud Service实例上存在具有任何唯一性约束数据（rep：principalName、rep：authorizableId、jcr：uuid或rep：externalId）的组，则相关组是&#x200B;_未_&#x200B;迁移，并且云系统上以前存在的组保持不变。 这将记录在“主体迁移报告”中。
* 有关在封闭用户组(CUG)策略中使用的组的额外注意事项，请参阅[迁移封闭用户组](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)。

## 最终摘要和报告

成功完成提取和摄取后，将生成一个报告，其中显示组迁移详细信息。 有关详细信息，请参阅[如何验证组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration)。
