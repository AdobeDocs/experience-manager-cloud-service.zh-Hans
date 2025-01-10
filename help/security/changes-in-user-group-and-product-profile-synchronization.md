---
title: 用户组和产品配置文件同步中的更改
description: 了解AEM as a Cloud Service在用户群组和产品配置文件同步方面的更改
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: ccfcecb77c7999784d6eaf6c1c6cfcb4269f5c80
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 用户组和产品配置文件同步中的更改 {#changes-in-user-group-and-product-profile-synchronization}

每当用户登录到AEM as a Cloud Service或使用访问令牌时，Adobe Admin Console用户组、产品配置文件和产品配置文件服务都会作为组同步到AEM存储库中。

1月28日，为了减少UI混乱并优化性能，将对同步行为进行一些更改，从而减少AEM中出现的组。 将删除两种类别的AEM组：

1. 后缀为`GROUP_NAME_SUFFIX`的AEM组。 这些组不会显示在Adobe Developer Console中，而是显示在AEM组管理屏幕中，如下所示。 在您的AEM应用程序引用这些组（这不太可能）的情况下，请确保引用不带该后缀的Adobe Admin Console用户组。

   ![已删除组1](/help/security/assets/removed-groups-1.png)

1. 与Adobe Admin Console产品配置文件关联的AEM组与特定环境无关。 这可能包括以下产品配置文件：

   * 与其他Adobe产品相关
   * 与其他AEM项目相关
   * 与同一AEM项目中的其他AEM环境相关
   * 与Cloud Manager相关（例如，`Business Owner - Cloud Service`）

   例如，在下图中，有许多行具有模式`AEM Administrators-<suffix>`或`AEM Users-<suffix>`，后缀与当前环境无关。

   ![已删除组2](/help/security/assets/removed-groups-2.png)

您可以通过在Cloud Manager中的环境操作菜单中选择管理&#x200B;**访问 — 作者配置文件**(或&#x200B;**Publish配置文件**)来检查哪个后缀与当前环境相关。

![检查后缀](/help/security/assets/suffix-check.png)

这将导航到Adobe Admin Console，如下面的屏幕快照中所述。 请注意，`<suffix>`可以是随机字符集或层，也可以是程序和环境ID（例如，`author - Program 12345 - Environment 45678`）。

Admin Console中的![后缀](/help/security/assets/admin-console-profile-suffixes.png)

在极少数情况下，您的AEM应用程序会引用将不再出现在AEM中的组，请确保改用i)正确的AEM实例中的产品配置文件或ii) Adobe Admin Console用户组。

