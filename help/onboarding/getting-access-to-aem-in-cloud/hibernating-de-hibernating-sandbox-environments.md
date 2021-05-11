---
title: '冬眠和冬眠沙箱环境 '
description: 冬眠和冬眠沙箱环境
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
translation-type: tm+mt
source-git-commit: 3b57acc47dd60d050ceebebb12bd9080b7fc5cf5
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# 冬眠和冬眠沙箱环境{#hibernating-introduction}

沙箱项目环境在某段时间内未检测到活动，则进入&#x200B;*休眠模式*。

>[!NOTE]
>休眠是沙箱项目环境特有的。 生产项目环境不休眠。

## 休眠{#hibernation-introduction}

休眠可以自动或手动进行。 沙箱项目环境进入&#x200B;*休眠模式*&#x200B;可能需要几分钟的时间。 数据会在休眠期间保留。

休眠分为：

* **自**  动沙箱项目环境在八小时不活动后自动休眠，这意味着作者和发布服务都不会接收请求。

* **手动**:作为用户，您可以手动休眠沙箱项目环境，但无需这样做，因为休眠将在特定时间段（八小时）不活动后自动发生。

>[!CAUTION]
>在最新版本中，直接从Cloud Manager链接到开发人员控制台不会让您选择休眠沙箱项目环境。 解决方法是在开发人员控制台中添加一次以下模式，在url `#release-cm-p1234-e5678 where 1234` 1234的末尾添加以下模式：您的&#x200B;*项目ID*，而5678是您的&#x200B;*环境ID*。

### 使用手动休眠{#using-manual-hibernation}

您可以通过以下两种不同的方式从开发人员控制台手动休眠沙箱项目:

* 环境细节屏幕
* 环境列表屏幕

>[!NOTE]
>Cloud Manager的任何用户都可以访问沙箱项目的开发人员控制台。

请按照以下步骤手动休眠沙箱项目环境:

1. 导航到&#x200B;**开发人员控制台**。
请参阅[访问开发人员控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)，了解如何从&#x200B;**环境**&#x200B;卡访问&#x200B;**开发人员控制台**。
   >[!IMPORTANT]
   >直接从Cloud Manager链接到&#x200B;**开发人员控制台**&#x200B;时，您不能选择将沙箱项目环境休眠。 解决方法是在开发人员控制台中添加一次以下模式，在url `#release-cm-p1234-e5678 where 1234` 1234的末尾添加以下模式：您的&#x200B;*项目ID*，而5678是您的&#x200B;*环境ID*。

1. 单击&#x200B;**Hibernate**，如下图所示：

   ![](assets/hibernate-1.png)

   或者，

   单击左上方的&#x200B;**环境**&#x200B;链接以视图环境列表，然后单击&#x200B;**Hibernate**，如下图所示：

   ![](assets/hibernate-1b.png)

1. 单击&#x200B;**Hibernate**&#x200B;以确认该步骤。

   ![](assets/hibernate-2.png)

1. 休眠成功后，您将在&#x200B;**开发人员控制台**&#x200B;屏幕中看到您的环境的休眠进程完成通知。

   ![](assets/hibernate-4.png)


## 去休眠{#de-hibernation-introduction}

1. 导航到&#x200B;**开发人员控制台**。
请参阅[访问开发人员控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)，了解如何从&#x200B;**环境**&#x200B;卡访问&#x200B;**开发人员控制台**。

   >[!IMPORTANT]
   >直接从Cloud Manager链接到&#x200B;**开发人员控制台**&#x200B;时，您不能选择取消休眠沙箱项目环境。 解决方法是在开发人员控制台中添加一次以下模式，在url `#release-cm-p1234-e5678 where 1234` 1234的末尾添加以下模式：您的&#x200B;*项目ID*，而5678是您的&#x200B;*环境ID*。

   >[!NOTE]
   >或者，您也可以通过尝试访问已休眠环境的作者或发布服务，导航到&#x200B;**开发人员控制台**&#x200B;以取消休眠；在这种情况下，将显示一个登陆页，其中包含指向“开发人员控制台”的链接。 请参阅下面的访问休眠环境部分。

   >[!IMPORTANT]
   >对开发人员控制台的访问权限由&#x200B;**Admin Console**&#x200B;中的&#x200B;**云管理器 — 开发人员角色**&#x200B;定义。 具有开发人员角色权限的用户可以解除沙箱项目环境的休眠。

1. 单击&#x200B;**De-hibernate**，如下图所示：

   ![](assets/de-hibernation-img1.png)

   或者，

   单击左上方的&#x200B;**环境**&#x200B;链接以视图环境列表，然后单击&#x200B;**解除休眠**，如下图所示

   ![](assets/de-hibernate-1b.png)


1. 单击&#x200B;**取消Hibernate**&#x200B;以确认该步骤。

   ![](assets/de-hibernation-img2.png)

1. 您将收到解除休眠进程已启动的通知，并将随进度进行更新。

   ![](assets/de-hibernation-img3.png)

1. 进程完成后，沙箱项目环境将再次处于活动状态。

   ![](assets/de-hibernation-img4.png)

### 对De-hibernate {#permissions-de-hibernate}的权限

任何拥有产品用户档案的用户都应能够访问&#x200B;**开发人员控制台** ，允许他们解除环境的休眠。

## 访问休眠环境{#accessing-hibernated-environment}

当针对已休眠环境的作者层或发布层发出任何浏览器请求时，用户将会遇到描述该环境已休眠状态的登陆页，如下图所示：

![](assets/de-hibernation-img5.png)

## 重要注意事项{#important-considerations}

与冬眠和脱冬环境相关的几个主要考虑事项包括：

* 用户可以使用管道将自定义代码部署到休眠环境。 环境将保持休眠状态，新代码在解除休眠后将显示在环境中。

* AEM升级可应用于冬眠环境，客户可从Cloud Manager手动触发。 环境将保持冬眠状态，在冬眠后，新版本将显示在环境中。

* 沙箱在8小时不活动后被置于休眠节点中，在此之后，它们可以解除休眠。

* 沙箱在连续休眠模式下运行6个月后被删除，之后可以重新创建。

   >[!NOTE]
   >目前，Cloud Manager不指示环境是否已休眠。

## AEM对沙箱环境{#aem-updates-sandbox}的更新

有关详细信息，请参阅[AEM版本更新](/help/implementing/deploying/aem-version-updates.md)。

用户可以在沙箱项目中手动将AEM更新应用到环境。

请参阅[更新环境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)以了解如何更新环境。

>[!NOTE]
>* 只有目标环境具有正确配置的管线时，才能运行手动更新。
>* 手动更新至&#x200B;*Production*&#x200B;或&#x200B;*Stage*&#x200B;环境将自动更新至另一个。 Production+Stage环境集必须位于同一AEM版本上。

