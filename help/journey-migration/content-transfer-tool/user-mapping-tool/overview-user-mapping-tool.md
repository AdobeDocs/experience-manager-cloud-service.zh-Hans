---
title: 用户映射工具概述
description: 用户映射工具概述
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
source-git-commit: 99af299c3f401ce898366a75563d2b933f120e40
workflow-type: ht
source-wordcount: '361'
ht-degree: 100%

---

# 用户映射工具概述 {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用户映射工具"
>abstract="内容传输工具可帮助您将用户和组从现有 AEM 系统移动到 AEM as a Cloud Service。需将现有用户和组映射到其 IMS ID，以避免云服务创作实例上出现重复的用户和组。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="有关使用用户映射工具的重要注意事项"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="使用用户映射工具"

## 简介 {#introduction}

在过渡到 Adobe Experience Manager (AEM) as a Cloud Service 的历程中，您需要将用户和组从现有 AEM 系统移至 AEM as a Cloud Service。此操作由内容传输工具完成。

对 AEM as a Cloud Service 的一项重大更改是完全集成使用 Adobe ID 来访问创作层。这需要使用 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 来管理用户和用户组。用户配置文件信息集中存储在 Adobe Identity Management System (IMS) 中，该系统在所有 Adobe 云应用程序之间提供单点登录。有关更多详细信息，请参阅 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)。由于此更改，需将现有用户和组映射到其 IMS ID，以避免云服务创作实例上出现重复的用户和组。

## 用户映射工具 {#mapping-tool}

内容传输工具（无用户映射）将迁移与正在迁移的内容关联的任何用户和组。用户映射工具是内容传输工具的一部分，其唯一用途是修改用户，以便他们能够由 IMS 正确识别，后者是由 AEM as a Cloud Service 使用的单点登录功能。完成这些修改后，内容传输工具会像往常一样迁移指定内容的用户和组。

### 后续内容 {#whats-next}

了解用户映射工具的含义后，您现在可以在使用用户映射工具之前查看重要注意事项和例外情况。有关更多详细信息，请参阅[用户映射工具的重要注意事项](/help/journey-migration/content-transfer-tool/user-mapping-tool/considerations-user-mapping-tool.md)。
