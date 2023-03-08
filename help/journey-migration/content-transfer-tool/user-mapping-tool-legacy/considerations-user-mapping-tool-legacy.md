---
title: 用户映射工具的重要注意事项（旧版）
description: 用户映射工具的重要注意事项（旧版）
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
source-git-commit: 69dfe7f98628ab67cc3a994c32b1530550ec6a01
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# 用户映射工具的重要注意事项 {#important-considerations}


## 例外情况 {#exceptional-cases}

将记录以下特定案例：

1. 如果用户在 `profile/email` 字段 *jcr* 节点将迁移有问题的用户或组，但不会对其进行映射。  即使电子邮件地址用作登录的用户名，也会出现这种情况。

1. 如果在AdobeIdentity Management System (IMS)系统中未找到所用ID的给定电子邮件（或者如果由于其他原因无法检索IMS ID），则将迁移相关用户或组，但不会映射它们。

1. 如果用户当前处于禁用状态，则会被视为与未处于禁用状态时相同。 它将按正常方式进行映射和迁移，并在云实例上保持禁用状态。

1. 如果目标AEM Cloud Service实例上存在与源AEM实例上用户之一具有相同用户名(rep：principalName)的用户，则不会迁移有问题的用户或组。

1. 如果用户迁移时没有首先通过用户映射进行映射，则他们在目标云系统上将无法使用其IMS ID登录。  他们也许可以使用传统的AEM方法登录，但请记住，这通常不是所需或期望的。

## 其他注意事项 {#additional-considerations}

* 如果设置 **在引入之前擦除云实例上的现有内容** 设置，Cloud Service实例上已转移的用户将与整个现有存储库一起删除，并将创建一个新存储库以将内容摄取到。 这也会重置所有设置，包括目标Cloud Service实例的权限，对于添加到中的管理员用户，也是如此 **管理员** 组。 管理员用户需要重新添加到 **管理员** 组以检索CTT的访问令牌。

* 建议先从目标Cloud ServiceAEM实例中删除任何现有用户，然后再使用用户映射运行CTT。 这是为了防止在将用户从源AEM实例迁移到目标AEM实例时出现任何冲突。 如果源AEM实例和目标AEM实例中存在相同的用户，则在引入期间将会发生冲突。

* 在执行内容增补时，如果内容未传输，因为自上次传输以来内容未发生更改，则与该内容关联的用户和组也不会传输，即使用户和组在此期间发生了更改也是如此。 这是因为用户和组将随其关联的内容一起迁移。

* 如果目标AEM Cloud Service实例中的某个用户与源AEM实例中的某个用户具有不同的用户名，但电子邮件地址相同，并且启用了用户映射，则将在日志中写入错误消息，并且不会传输源AEM用户，因为目标系统上只允许有一个具有给定电子邮件地址的用户。

* 如果源AEM实例上的两个用户具有相同的电子邮件地址，并且启用了用户映射，则日志中将写入一条错误消息，并且不会传输源AEM用户之一，因为目标系统上只允许一个具有给定电子邮件地址的用户。

### 后续内容 {#whats-next}

了解了重要注意事项和例外情况后，您现在就可以使用该工具了。 有关更多详细信息，请参阅[使用用户映射工具](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md)。
