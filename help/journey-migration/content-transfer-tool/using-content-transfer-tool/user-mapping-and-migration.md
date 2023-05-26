---
title: 用户映射和主体迁移
description: 用户映射和主体迁移概述
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 91a13f8b23136298e0ccf494e51fccf94fa1e0b4
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 9%

---

# 用户映射和主体迁移 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用户映射"
>abstract="内容传输工具可帮助您将用户和组从现有Adobe Experience Manager (AEM)系统移动到AEMas a Cloud Service。 必须将现有用户映射到其 IMS ID，以免用户在云服务创作实例上重复。"

>[!NOTE]
>有关用户映射工具的早期版本，请参阅 [旧版文档](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## 简介 {#introduction}

在过渡到Adobe Experience Manager (AEM) as a Cloud Service的过程中，您必须将用户和组从现有AEM系统移动到AEMas a Cloud Service。 此任务由内容传输工具完成。

对 AEM as a Cloud Service 的一项重大更改是完全集成使用 Adobe ID 来访问创作层。此过程需要使用 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 用于管理用户和用户组。 用户配置文件信息集中存储在AdobeIdentity Management System (IMS)中，可在所有Adobe云应用程序之间提供单点登录。 有关更多详细信息，请参阅 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management)。由于此更改，现有用户必须映射到其IMS ID，以避免在Cloud Service创作实例上出现重复用户。 由于传统AEM中的组与IMS中的组存在根本上的不同，因此不会映射组，但在迁移完成后必须协调两组组。

## 用户映射和迁移详细信息 {#user-mapping-detail}

内容传输工具和Cloud Acceleration Manager会迁移与正在迁移的内容关联的任何用户。 此映射是自动完成的，是否完成可以在开始提取之前通过切换进行控制。 用户在开始提取时可以覆盖切换的默认设置。

* 如果源系统是一个创作实例，则默认情况下，执行映射的选择是 _日期_，因为这是推荐的流程。
* 如果源系统是发布实例，则默认情况下，执行映射的选择是 _关闭_，因为通常不会迁移用户或在发布实例上使用用户。

## 映射和迁移用户时的重要注意事项 {#important-considerations}


### 例外情况 {#exceptional-cases}

将记录以下特定案例：

1. 如果用户在 `profile/email` 字段 *jcr* 节点，相关用户或组可能会被迁移，但未被映射。 即使电子邮件地址用作登录的用户名，也会发生这种情况。

1. 如果用户被禁用，则其处理方式与未禁用时相同。 它按常规方式进行映射和迁移，并在云实例上保持禁用状态。

1. 如果目标AEM Cloud Service实例中存在与源AEM实例中的某个用户具有相同用户名(rep：principalName)的用户，则不会迁移有问题的用户。

1. 如果迁移的用户未通过用户映射进行映射，则他们在目标云系统上将无法使用其IMS ID登录。 或者，如果他们的电子邮件地址与用于登录IMS的电子邮件地址不匹配，则他们也无法在目标云系统上使用其IMS ID登录。 他们也许可以使用传统的AEM方法登录，但此方法通常不是所需或期望的。


## 其他注意事项 {#additional-considerations}

* 如果设置 **在引入之前擦除云实例上的现有内容** 设置，Cloud Service实例上已转移的用户将与整个现有存储库一起删除。 此外，还创建一个新存储库，内容将摄取到该存储库中。 此过程还会重置所有设置(包括目标Cloud Service实例的权限)，对于已添加到 **管理员** 组。 管理员用户必须已阅读 **管理员** 组以检索CTT的访问令牌。
* 执行内容增补时，如果内容未传输，因为自上次传输以来内容未发生更改，则与该内容关联的用户和组也不会传输。 即使用户和组在此期间已更改，此规则也适用。 原因在于，用户和组将随其关联的内容一起迁移。
* 如果目标AEM Cloud Service实例中的某个用户与源AEM实例中的某个用户具有不同的用户名，但电子邮件地址相同，并且启用了用户映射，则日志会记录一条错误消息。 此外，不会传输源AEM用户，因为目标系统上只允许一个具有给定电子邮件地址的用户。

## 最终摘要和报告 {#final-report}

成功完成提取和引入后，将生成一个报告，其中显示主体迁移详细信息。 参见 [如何验证主体迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) 了解详细信息。
