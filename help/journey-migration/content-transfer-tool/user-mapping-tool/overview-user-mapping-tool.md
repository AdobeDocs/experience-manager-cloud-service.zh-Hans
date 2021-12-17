---
title: 用户映射工具概述
description: 用户映射工具概述
source-git-commit: bcbf4e4ba1330bef9f2c8c473419903e40ac0e58
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---


# 用户映射工具概述 {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用户映射工具"
>abstract="内容传输工具可帮助您将用户和组从现有AEM系统移至AEMas a Cloud Service。 现有用户和组需要映射到其IMS ID，以避免Cloud Service创作实例上出现重复的用户和组。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用用户映射工具的重要注意事项"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="使用用户映射工具"

## 简介 {#introduction}

在过渡到Adobe Experience Manager(AEM)as a Cloud Service的历程中，您需要将用户和组从现有AEM系统移至AEMas a Cloud Service。 这由内容传输工具完成。

AEMas a Cloud Service的一项主要更改是完全集成地使用AdobeID访问创作层。  这需要使用 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 用于管理用户和用户组。 AdobeIdentity Management系统(IMS)中集中了用户配置文件信息，该系统可在所有Adobe云应用程序中提供单点登录。 有关更多详细信息，请参阅 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). 由于进行了这项更改，现有用户和组需要映射到其IMS ID，以避免Cloud Service创作实例上出现重复的用户和组。

## 用户映射工具 {#mapping-tool}

内容传输工具（无用户映射）将迁移与所迁移内容关联的任何用户和组。 用户映射工具是内容传输工具的一部分，其唯一目的是修改用户和组，以便IMS(AEMas a Cloud Service使用的单点登录功能)能够正确识别它们。 完成这些修改后，内容传输工具会照常迁移指定内容的用户和组。

### 下一步 {#whats-next}

了解了用户映射工具的含义后，您现在可以在使用用户映射工具之前查看重要注意事项和特殊案例。 请参阅 [有关用户映射工具的重要注意事项](/help/journey-migration/content-transfer-tool/user-mapping-tool/considerations-user-mapping-tool.md) 以了解更多详细信息。