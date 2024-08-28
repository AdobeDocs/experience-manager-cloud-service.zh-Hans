---
title: 用户映射工具的重要注意事项（旧版）
description: 用户映射工具的重要注意事项（旧版）
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: 13a2386c099624a46e84126a939a9470e9b3a5f2
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 1%

---

# 用户映射工具的重要注意事项（旧版） {#important-considerations}

>[!INFO]
>
>本文档参考该工具的已弃用版本。 有关最新版本的更多信息，请参阅[组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)。

## 特殊情况 {#exceptional-cases}

将记录以下特定案例：

1. 如果用户在其&#x200B;*jcr*&#x200B;节点的`profile/email`字段中没有电子邮件地址，则相关用户或组已迁移，但未映射。 即使电子邮件地址用作登录的用户名，此规则也是如此。

1. 如果在AdobeIdentity Management System (IMS)系统上未找到所使用ID的电子邮件（或者如果无法检索IMS ID），则迁移用户或组，但不映射它们。

1. 如果用户被禁用，则其处理方式与未禁用时相同。 它按常规方式进行映射和迁移，并在云实例上保持禁用状态。

1. 如果目标AEM Cloud Service实例上存在与源AEM实例上用户具有相同用户名(rep：principalName)的用户，则不会迁移该用户或组。

1. 如果用户在未首先通过用户映射进行映射的情况下进行迁移，则他们在目标云系统上将无法使用其IMS ID登录。 他们也许可以使用传统的AEM方法登录，但此工作流通常不是所需或期望的。

## 其他注意事项 {#additional-considerations}

* 如果设置了&#x200B;**在引入**&#x200B;之前擦除云实例上的现有内容，则将删除Cloud Service实例上已转移的用户。 系统还会删除整个现有存储库，并创建一个新存储库以将内容摄取到其中。 此操作还会重置所有设置，包括目标Cloud Service实例的权限，对于添加到&#x200B;**管理员**&#x200B;组的管理员用户为true。 必须将管理员用户读入&#x200B;**管理员**&#x200B;组，才能检索CTT的访问令牌。

* Adobe建议您在使用“用户映射”运行CTT之前，从目标Cloud ServiceAEM实例中删除任何现有用户。 要防止在将用户从源AEM实例迁移到目标AEM实例时出现任何冲突，必须执行此操作。 如果源AEM实例和目标AEM实例中存在相同的用户，则在引入期间可能会发生冲突。

* 执行内容增补时，如果由于上次传输后内容未更改而未传输内容，则与该内容关联的用户和组也不会传输。 即使用户和组在此期间已发生更改，此规则仍然适用。 原因在于，用户和组将随其关联的内容一起迁移。

* 如果AEM Cloud Service中有一个用户与源AEM实例中的用户具有不同的用户名但电子邮件地址相同，并且启用了“用户映射”，则会记录一条错误消息。 此外，不会传输源AEM用户，因为目标系统上只允许一个具有给定电子邮件地址的用户。

* 如果源AEM实例上的两个用户具有相同的电子邮件地址，并且启用了“用户映射”，则会记录一条错误消息。 此外，还会传输一个源AEM用户，因为目标系统上只允许一个具有给定电子邮件地址的用户。

### 后续内容 {#whats-next}

了解了重要注意事项和例外情况后，您现在就可以使用该工具了。 有关更多详细信息，请参阅[使用用户映射工具](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md)。
