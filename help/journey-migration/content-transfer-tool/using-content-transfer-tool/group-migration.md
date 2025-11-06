---
title: 群组迁移
description: AEM as a Cloud Service中的组迁移概述。
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 3%

---


# 群组迁移 {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="群组迁移"
>abstract="内容传输工具可帮助您将组从现有的 Adob&#x200B;&#x200B;e Experience Manager (AEM) 系统复制到 AEM as a Cloud Service."

>[!NOTE]
>有关用户映射工具的早期版本，请参阅[旧文档](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)。

## 简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="用户未迁移"
>abstract="内容转移工具不再迁移用户。用户应在 Admin Console 中进行管理。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="AEM Admin Console 文档"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

在过渡到Adobe Experience Manager (AEM) as a Cloud Service的过程中，必须将组从现有AEM系统迁移到AEM as a Cloud Service。 此任务由内容传输工具完成。

AEM as a Cloud Service的一项重大更改是完全集成使用Adobe ID来访问创作层。 此过程需要使用[Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)来管理用户和用户组。 用户配置文件信息集中存储在Adobe Identity Management System (IMS)中，可通过单点登录功能访问所有Adobe云应用程序。 有关详细信息，请参阅[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=zh-Hans#identity-management)。 由于此更改，用户首次通过IMS登录时将在AEM上自动创建。  因此，CTT不会将用户迁移到云系统。  必须将IMS用户放置到IMS组中，这些组可以是迁移组，也可以是放置在AEM组中、已获得要迁移的AEM内容访问权限的新组。  通过这种方式，云系统上的用户将拥有与其源AEM系统相同的访问权限。

## 组迁移详细信息 {#group-migration-detail}

内容传输工具和Cloud Acceleration Manager会将与要迁移的内容关联的任何组迁移到云系统。 内容传输工具通过在提取过程中从源AEM系统复制所有组来实现这一点。 然后，CAM摄取将仅选择和迁移某些组：

* 如果某个组位于已迁移内容的ACL或CUG策略上，则会迁移该组，但下面列出了一些例外。
* 目标云系统中已经存在许多内置的组；这些组永远不会迁移。
   * 某些内置组可能包含&#x200B;_非_&#x200B;内置的成员组；将迁移迁移迁移内容的ACL或CUG策略中引用的任何此类成员组（直接成员或成员等），以确保属于这些组成员的用户能够（直接或间接）保持对迁移内容的访问权限。
* 其他组（如ACL或CUG策略中找不到的组、目标系统中已存在的组，以及目标系统中已存在任何唯一性受限数据的组）将不会迁移。

请注意，为某个组记录/报告的路径只是触发该组进行迁移的第一个路径，并且该组可能位于其他内容路径上。

大多数迁移的组都配置为由IMS管理。  这意味着IMS中具有相同名称的组将链接到AEM中的组，并且IMS组中的任何IMS用户都将成为AEM中的AEM用户和组的成员。  这允许这些用户根据组的ACL或CUG策略访问内容。

请注意，已迁移的组不再被视为AEM的“本地组”；它们是AEM中支持IMS的组，但IMS中可能尚不存在它们。  必须单独在IMS中重新创建它们，以便它们可以在AEM和IMS之间同步。  可以通过Admin Console和其他方法在IMS中单独或批量创建组。  有关在Admin Console上单独或批量创建组的详细信息，请参阅[管理用户组](https://helpx.adobe.com/cn/enterprise/using/user-groups.html)。

此IMS配置的例外情况是Assets收藏集和专用文件夹创建的组。 在AEM上创建收藏集或专用文件夹后，将创建组以访问该内容；此类组将迁移到云系统，但不会配置为由IMS管理。  要将IMS用户添加到这些组，必须在Assets UI的“组属性”页面中单独或集体地将这些用户添加为其他IMS组的一部分。


## 选择退出组迁移 {#group-migration-option}

CTT版本3.0.20及更高版本包含用于禁用组迁移的选项。  此操作在OSGI控制台中进行配置，如下所示：

* 打开OSGI配置`(http://<server>/system/console/configMgr)`
* 单击名为&#x200B;**内容传输工具提取服务配置**&#x200B;的配置
* 取消选中&#x200B;**在迁移中包含组**&#x200B;以禁用组迁移
* 单击&#x200B;**保存**&#x200B;以确保配置在服务器上已保存并处于活动状态

禁用此设置后，将不会迁移组，并且不会有主体迁移报告或用户报告（请参阅下文）。

## 主体迁移报告和用户报告 {#principal-migration-report}

如果在迁移期间包括组（默认），则会保存一份主体迁移报告，其中概述了迁移期间每个组所发生的情况。  要在成功摄取后下载此报表，请执行以下操作：

* 在CAM中，转到内容传输并选择摄取作业。
* 单击相关摄取行上的省略号(...)，然后选择“查看主体摘要”。
* 在出现的对话框中，从“下载文件……”下的下拉列表中选择“主体迁移报告”，然后单击“下载”按钮。
* 保存生成的CSV文件。

每个组记录的一些信息是：

* 如果迁移，则为导致组迁移的第一个ACL或CUG的路径。
* 是否先前已迁移该组；如果当前摄取是非划出摄取，则某些组可能已在上次摄取期间迁移。
* 该组是否为内置组；这些组不会迁移，因为它们始终位于目标AEMaaCS环境中。
* 如果该组不是已迁移内容的ACL或CUG的一部分，则不会迁移该组。
* 如果该组是本地组(例如Assets收藏集创建的组)，则它可能已迁移，在这种情况下，“本地”一词将添加到该组的报表中。

在迁移过程中，不会迁移用户，但除非以某种方式捕获用户，否则源系统上的用户 — 组关系将丢失。 摄取过程以文本格式在用户报告中捕获某些此类信息，该报告位于主体迁移报告末尾。

### 用户报告 {#user-report}

在用户报表部分中，将报告用户（每行一个），以及在此引入期间迁移的用户电子邮件地址和启用了IMS的组的列表。  列表中不包含未迁移的组、在上次引入期间迁移的组或本地组。   如果用户不在任何迁移的启用IMS的组中，并且它没有额外的注释指示它是一个特殊情况（请参阅下面的&#x200B;**注释**），则该用户&#x200B;_不_&#x200B;显示在报表中。 与每个用户一起报告的组是源系统中用户直接或间接为其中成员的组；由于源系统中的组可能嵌套，而目标系统中的组不是，因此此组列表支持IMS中新的扁平化组结构。

如果先进行擦除，然后再进行非擦除摄取，则非擦除摄取中用户列表中的组将只是那些在非擦除阶段迁移的组。

#### 注释 {#user-report-notes}

除了每个用户的组外，用户报告中还有一个字段，可提供有关用户的说明（报告中也提供了有关该说明含义的详细说明）以供参考。  可能的注意事项包括：

* **Note-A**&#x200B;直接在ACL中引用的用户在其注释部分将具有&#x200B;*Note-A*，因为这不是推荐的使用案例或最佳实践。
* **Note-B**&#x200B;作为内置组的直接成员的用户在其Notes部分将具有&#x200B;*Note-B*，因为这不是推荐的使用案例或最佳实践。
* **Note-C**&#x200B;作为已迁移本地组(例如，由Assets集合创建的组)的间接成员的用户，在其Notes节中将具有&#x200B;*Note-C*，因为未将本地组配置为由IMS管理。

这些情况可以同时发生，并且与前几个情况相同。  _有关每个备注针对每个用户引用哪些组的详细信息，请检查引入日志；它会为每个用户报告此信息。_

用户报告将添加到主体迁移报告的末尾（因此是其中的一部分）（请参阅下面的[最终摘要和报告](#final-summary-and-report)），以使客户更全面地了解组和用户及其关系。

## 批量上传文件 {#bulk-upload-files}

由于组仅迁移到AEM as a Cloud Service，因此仍必须将其添加到IMS，以便它们可以在云中与AEM正常配合使用。 此外，不会迁移用户，因此也需要将用户添加到IMS。 CTT/CAM迁移工具不会执行此步骤，但摄取过程会创建两个批量上传文件，一个用于组，一个用于用户。 这些文件可以编辑，然后与Admin Console的批量上传功能一起使用，根据您的AEM组和用户创建IMS组和用户。

有关如何使用Admin Console批量上传文件来创建用户和组的详细信息，请参阅[批量将组和用户上传到IMS](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md)。

有关管理AEM as a Cloud Service用户的更多详细信息，另请参阅[管理用户](https://helpx.adobe.com/ca/enterprise/using/users.html)。

## 其他注意事项 {#additional-considerations}

* 如果设置了&#x200B;**在摄取之前擦除云实例上的现有内容**，则以前传输到Cloud Service实例的组将与整个现有存储库一起删除；将创建一个内容摄取到的新存储库。 此过程还会重置所有设置，包括目标Cloud Service实例的权限，对于添加到&#x200B;**管理员**&#x200B;组的任何用户均适用。 必须将管理员用户重新添加到&#x200B;**管理员**&#x200B;组，以检索CTT/CAM摄取的访问令牌。
* 执行非擦除摄取时（取消设置&#x200B;**擦除现有内容**），如果由于上次传输后内容未更改而未传输内容，则与该内容关联的组也不会传输。 即使在源系统上更改了组，此规则仍然适用。 这是因为组仅随与其关联的内容一起迁移。 因此，在这种情况下，任何属于源系统上某个组的组都将不会迁移，除非这些组属于正在迁移的其他组，或者位于正在迁移的其他内容的ACL中。 要在以后迁移这些组，请考虑使用包，从目标中删除组并重新迁移相关内容，或使用划出摄取重新迁移。
* 在非划出引入期间，如果源AEM实例和目标AEM Cloud Service实例上存在具有任何唯一性约束数据（rep:principalName、rep:authorizableId、jcr:uuid或rep:externalId）的组，则相关组是&#x200B;_未_&#x200B;迁移，并且云系统上以前存在的组保持不变。 这将记录在“主体迁移报告”中。
* 有关在封闭用户组(CUG)策略中使用的组的额外注意事项，请参阅[迁移封闭用户组](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)。

## 最终摘要和报告

成功完成提取和摄取后，将生成一个报告，其中显示组迁移详细信息。 有关详细信息，请参阅[如何验证组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration)。
