---
title: 用户组和产品轮廓同步变更
description: 了解加入 AEM as a Cloud Service 的用户组和产品轮廓同步变更
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: 5c103fcce1ae47bc89f4f572d89967c62c1f7603
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 79%

---

# 用户组和产品轮廓同步变更 {#changes-in-user-group-and-product-profile-synchronization}

当用户登录 AEM as a Cloud Service 或使用访问令牌时，Adobe Admin Console 用户组、产品轮廓和产品轮廓服务都会作为组同步到 AEM 存储库中。

从AEM维护版本19149开始，更改组同步行为以减少UI混乱并优化性能。 具体来说，以下两类AEM组的用户组成员资格将不再同步：

1. 具有后缀 `GROUP_NAME_SUFFIX` 的 AEM 组。这些组不会出现在 Adobe Developer Console 中，但会出现在 AEM 群组管理屏幕中，如下所示。如果您的 AEM 应用程序引用这些组（这种情况不太可能发生），请确保引用不带该后缀的 Adobe Admin Console 用户组。

   ![已移除第 1 组](/help/security/assets/removed-groups-1.png)

1. 与 Adobe Admin Console 产品轮廓关联的 AEM 组与特定环境无关。这可能包括以下产品轮廓：

   * 与其他 Adobe 产品相关
   * 与其他 AEM 程序相关
   * 与同一 AEM 程序中的其他 AEM 环境相关
   * 与 Cloud Manager 相关（例如 `Business Owner - Cloud Service`）

   例如，在下图中，有许多行具有模式 `AEM Administrators-<suffix>` 或 `AEM Users-<suffix>`，其后缀与当前环境无关。

   ![已移除第 2 组](/help/security/assets/removed-groups-2.png)

您可以通过在 Cloud Manager 中的环境动作菜单选择管理&#x200B;**访问 - 作者轮廓**（或&#x200B;**发布轮廓**）来检查哪些后缀与当前环境相关。

![检查后缀](/help/security/assets/suffix-check.png)

这将导航到 Adobe Admin Console，如下面的屏幕快照所示。请注意，`<suffix>` 可以是一组随机字符，也可以是层级、程序和环境 ID（例如，`author - Program 12345 - Environment 45678`）。

![Admin Console 中的后缀](/help/security/assets/admin-console-profile-suffixes.png)

如果您的 AEM 应用程序引用了不再出现在 AEM 中的组（这种情况不太可能发生），请确保改用 i) 来自正确 AEM 实例的产品轮廓或 ii) Adobe Admin Console 用户组。

用户的组成员资格将在用户登录到环境时同步，并从与当前环境无关的组中删除。 这些组本身将保留，并包括自启用该功能以来未登录的用户。
