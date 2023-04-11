---
title: 用户映射和主体迁移
description: 用户映射和主迁移概述
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 22%

---

# 用户映射和主体迁移 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用户映射"
>abstract="内容传输工具可帮助您将用户和组从现有 AEM 系统移动到 AEM as a Cloud Service。必须将现有用户映射到其 IMS ID，以免用户在云服务创作实例上重复。"

>[!NOTE]
>有关用户映射工具的早期版本，请参阅 [旧版文档](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## 简介 {#introduction}

在过渡到 Adobe Experience Manager (AEM) as a Cloud Service 的历程中，您需要将用户和组从现有 AEM 系统移至 AEM as a Cloud Service。此操作由内容传输工具完成。

对 AEM as a Cloud Service 的一项重大更改是完全集成使用 Adobe ID 来访问创作层。这需要使用 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 来管理用户和用户组。用户配置文件信息集中存储在 Adobe Identity Management System (IMS) 中，该系统在所有 Adobe 云应用程序之间提供单点登录。有关更多详细信息，请参阅 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html#identity-management)。由于进行了这项更改，现有用户需要映射到其IMS ID，以避免Cloud Service创作实例上出现重复的用户。 由于传统AEM中的组与IMS中的组存在根本上的不同，因此组未映射，但是迁移完成后必须协调这两组组。

## 用户映射和迁移详细信息 {#user-mapping-detail}

内容传输工具和云加速管理器将迁移与所迁移内容关联的任何用户。 此映射会自动完成，并且是否完成可以通过切换来控制，然后才能开始提取。 开始提取时，用户可能会覆盖切换的默认设置。

* 如果源系统是创作实例，则默认情况下选择执行映射 _on_，因为这是推荐的过程。
* 如果源系统是发布实例，则默认情况下选择执行映射 _关闭_，因为用户通常不会迁移或用在发布实例上。

## 映射和迁移用户时的重要注意事项 {#important-considerations}


### 特殊情况 {#exceptional-cases}

记录了以下特定案例：

1. 如果用户在 `profile/email` 字段 *jcr* 可能会迁移有关用户或组的节点，但不会映射该节点。 即使将电子邮件地址用作登录的用户名，也会出现这种情况。

1. 如果用户处于禁用状态，则其处理方式与未禁用状态相同。 它会照常进行映射和迁移，并在云实例上保持禁用状态。

1. 如果目标AEM Cloud Service实例上存在一个用户，该用户与源AEM实例上的某个用户具有相同的用户名(rep:principalName)，则不会迁移该用户或组。

1. 如果用户在迁移时没有首先通过用户映射进行映射，或者其电子邮件地址与用于登录IMS的电子邮件地址不匹配，则在目标云系统上，用户将无法使用其IMS ID登录。 他们可能能够使用传统的AEM方法登录，但请记住，这通常不是想要或期望的。


## 其他注意事项 {#additional-considerations}

* 如果设置 **摄取前擦除云实例上的现有内容** 设置后，Cloud Service实例上已传输的用户将与整个现有存储库一起删除，并将创建新存储库以将内容摄取到中。 此外，这还会重置所有设置，包括目标Cloud Service实例的权限，对于添加到的管理员用户，设置为true **管理员** 群组。 必须将管理员用户重新添加到 **管理员** 组来检索CTT的访问令牌。
* 执行内容增补时，如果内容自上次传输后未发生更改而未进行传输，则与该内容关联的用户和组也不会进行传输，即使用户和组在此期间发生了更改也是如此。 这是因为用户和组以及与其关联的内容一起进行迁移。
* 如果目标AEM Cloud Service实例的用户与源AEM实例上的某个用户具有不同的用户名，但电子邮件地址与其中一个用户相同，并且启用了“用户映射”，则日志中会写入一条错误消息，并且不会传输源AEM用户，因为目标系统上只允许一个具有给定电子邮件地址的用户。
