---
title: 用户映射和主体迁移
description: 用户映射和主体迁移概述
source-git-commit: aeb8f633b45908a87f15f9feeb3723f90470be92
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 18%

---

# 用户映射和主体迁移 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用户映射"
>abstract="内容传输工具可帮助您将用户和组从现有 AEM 系统移动到 AEM as a Cloud Service。现有用户必须映射到其IMS ID，以避免在Cloud Service创作实例上复制它们。"

>[!NOTE]
>有关用户映射工具的早期版本，请参阅 [旧版文档](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## 简介 {#introduction}

在过渡到 Adobe Experience Manager (AEM) as a Cloud Service 的历程中，您需要将用户和组从现有 AEM 系统移至 AEM as a Cloud Service。此操作由内容传输工具完成。

对 AEM as a Cloud Service 的一项重大更改是完全集成使用 Adobe ID 来访问创作层。这需要使用 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 来管理用户和用户组。用户配置文件信息集中存储在 Adobe Identity Management System (IMS) 中，该系统在所有 Adobe 云应用程序之间提供单点登录。有关更多详细信息，请参阅 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)。由于此更改，现有用户需要映射到其IMS ID，以避免Cloud Service创作实例上的重复用户。 由于传统AEM中的组与IMS中的组存在根本上的不同，因此不会映射组，但在迁移完成后必须协调两组组。

## 用户映射和迁移详细信息 {#user-mapping-detail}

内容传输工具和Cloud Acceleration Manager将迁移与正在迁移的内容关联的任何用户。 此映射是自动完成的，是否完成可以在开始提取之前通过切换进行控制。 用户在开始提取时可以覆盖切换的默认设置。

* 如果源系统是一个创作实例，则默认情况下，执行映射的选择是 _日期_，因为这是推荐的流程。
* 如果源系统是发布实例，则默认情况下，执行映射的选择是 _关闭_，因为通常不会迁移用户或在发布实例上使用用户。

## 映射和迁移用户时的重要注意事项 {#important-considerations}


### 例外情况 {#exceptional-cases}

将记录以下特定案例：

1. 如果用户在 `profile/email` 字段 *jcr* 节点可以迁移有问题的用户或组，但不会对其进行映射。 即使电子邮件地址用作登录的用户名，也是如此。

1. 如果用户被禁用，则其处理方式与未禁用时相同。 它按常规方式进行映射和迁移，并在云实例上保持禁用状态。

1. 如果目标AEM Cloud Service实例中存在与源AEM实例中的某个用户具有相同用户名(rep：principalName)的用户，则不会迁移有问题的用户或组。

1. 如果用户迁移时没有首先通过用户映射进行映射，或者如果用户的电子邮件地址与用于登录IMS的电子邮件地址不匹配，则用户将无法在目标云系统上使用其IMS ID登录。 他们也许可以使用传统的AEM方法登录，但请记住，这通常不是所需或期望的。


## 其他注意事项 {#additional-considerations}

* 如果设置 **在引入之前擦除云实例上的现有内容** 设置，Cloud Service实例上已转移的用户将与整个现有存储库一起删除，并将创建一个新存储库以将内容摄取到。 这也会重置所有设置，包括目标Cloud Service实例的权限，对于添加到中的管理员用户，也是如此 **管理员** 组。 管理员用户必须已阅读 **管理员** 组以检索CTT的访问令牌。
* 在执行内容增补时，如果内容未传输，因为自上次传输以来内容未发生更改，则与该内容关联的用户和组也不会传输，即使用户和组在此期间发生了更改也是如此。 这是因为用户和组将随其关联的内容一起迁移。
* 如果目标AEM Cloud Service实例中的某个用户与源AEM实例中的某个用户具有不同的用户名，但电子邮件地址相同，并且启用了用户映射，则会在日志中写入错误消息，并且不会传输源AEM用户，因为目标系统上只允许有一个具有给定电子邮件地址的用户。
