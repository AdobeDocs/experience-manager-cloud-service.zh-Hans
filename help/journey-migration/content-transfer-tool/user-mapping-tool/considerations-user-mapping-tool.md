---
title: 有关用户映射工具的重要注意事项
description: 有关用户映射工具的重要注意事项
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 有关用户映射工具的重要注意事项 {#important-considerations}


## 特殊情况 {#exceptional-cases}

将记录以下特定案例：

1. 如果用户在 `profile/email` 字段 *jcr* 将迁移相关用户或组的节点，但未映射该节点。

1. 如果在AdobeIdentity Management系统(IMS)系统中没有找到所用组织ID的给定电子邮件（或者，如果IMS ID因其他原因无法检索），则相关用户或组将被迁移，但未映射。

1. 如果用户当前处于禁用状态，则其处理方式与未禁用时相同。 它将照常进行映射和迁移，并在云实例上保持禁用状态。

1. 如果目标AEM Cloud Service实例上存在与源AEM实例上的某个用户同名(rep:principalName)的用户，则将不会迁移相关用户或组。

## 其他注意事项 {#additional-considerations}

* 如果设置 **摄取前擦除云实例上的现有内容** 设置后，Cloud Service实例上已传输的用户将与整个现有存储库一起删除，并将创建新存储库以将内容摄取到中。 此外，这还会重置所有设置，包括目标Cloud Service实例的权限，对于添加到的管理员用户，设置为true **管理员** 群组。 需要将管理员用户重新添加到 **管理员** 组来检索CTT的访问令牌。

* 建议在通过“用户映射”运行CTT之前，从目标Cloud ServiceAEM实例中删除任何现有用户。 这是为了防止将用户从源AEM实例迁移到目标AEM实例之间发生任何冲突。 如果源AEM实例和目标AEM实例上存在相同的用户，则在摄取期间将会发生冲突。

* 执行内容增补时，如果内容自上次传输后未发生更改而未进行传输，则与该内容关联的用户和组也将不会进行传输，即使用户和组在此期间发生更改也是如此。 这是因为用户和组以及与其关联的内容一起进行迁移。

* 如果目标AEM Cloud Service实例的用户与源AEM实例上的某个用户具有不同的用户名，但其电子邮件地址与该用户中的某个用户相同，并且启用了“用户映射”，则日志中将写入一条错误消息，并且不会传输源AEM用户，因为目标系统上只允许一个具有给定电子邮件地址的用户。

* 如果源AEM实例上的两个用户具有相同的电子邮件地址，并且启用了“用户映射”，则日志中将写入一条错误消息，并且不会传输源AEM用户之一，因为目标系统上只允许一个具有给定电子邮件地址的用户。

### 下一步 {#whats-next}

了解重要注意事项和特殊案例后，您即可使用该工具。 请参阅 [使用用户映射工具](/help/journey-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.md) 以了解更多详细信息。
