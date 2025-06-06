---
title: 用户映射工具（旧版）概述
description: 用户映射工具（旧版）概述
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 21%

---


# 用户映射工具（旧版）概述 {#overview-user-mapping-tool}

>[!INFO]
>
>本文档参考该工具的已弃用版本。 有关最新版本的更多信息，请参阅[组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)。

<!-- Alexandru: drafting this for now

NOTE: "LEGACY" for user mapping includes everything before (that is, not including) 2.0.16 of CTT.

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=zh-Hans#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=zh-Hans#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## 简介 {#introduction}

在过渡到Adobe Experience Manager (AEM)as a Cloud Service的过程中，您必须将用户和组从现有AEM系统移动到AEM as a Cloud Service。 此迁移由内容传输工具完成。

AEM as a Cloud Service的一项重大更改是完全集成使用AdobeID来访问创作层。 此集成需要使用[Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)来管理用户和用户组。 用户配置文件信息集中存储在AdobeIdentity Management System (IMS)中，可通过单点登录功能访问所有Adobe云应用程序。 有关详细信息，请参阅[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=zh-Hans#identity-management)。 由于此更改，现有用户和组必须映射到其IMS ID，以避免Cloud Service创作实例上的重复用户和组。

## 用户映射工具 {#mapping-tool}

内容传输工具（不含用户映射）可迁移与正在迁移的内容关联的任何用户和组。 用户映射工具是内容传输工具的一部分。 其唯一用途是编辑用户，以使其可被IMS正确识别，IMS是AEM as a Cloud Service使用的单点登录功能。 完成这些修改后，内容传输工具会像往常一样迁移指定内容的用户和组。

### 后续内容 {#whats-next}

了解用户映射工具的含义后，您现在可以在使用用户映射工具之前查看重要注意事项和例外情况。有关更多详细信息，请参阅[用户映射工具的重要注意事项](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)。
