---
title: '休眠和解除休眠沙盒环境 '
description: 休眠和解除休眠沙盒环境
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
source-git-commit: f06fe7f30d9f5e2eb5dcc6c8d542ace5f5e2f419
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---

# 休眠和解除休眠沙盒环境 {#hibernating-introduction}

如果在特定时间段内未检测到任何活动，则沙盒项目环境会进入&#x200B;*休眠模式*。

>[!NOTE]
>休眠是沙盒项目环境特有的。 生产程序环境不休眠。

## 休眠 {#hibernation-introduction}

休眠可以自动或手动进行。 沙盒项目环境可能需要多达几分钟时间才能进入&#x200B;*休眠模式*。 数据在休眠期间保留。

休眠分为：

* ****  自动沙盒项目环境在处于不活动状态八小时后会自动休眠，这意味着创作、预览或发布服务都不会收到请求。

* **手动**:作为用户，您可以手动将沙盒项目环境休眠，但是无需这样做，因为休眠将在特定时间段（八小时）不活动后自动发生。

>[!CAUTION]
>在最新版本中，直接从Cloud Manager链接到开发人员控制台将不允许您选择将沙盒项目环境休眠。 解决方法是在开发人员控制台中添加一次，在url `#release-cm-p1234-e5678 where 1234` 1234的末尾添加以下模式： *程序ID* , 5678是您的&#x200B;*环境ID*。

### 使用手动休眠 {#using-manual-hibernation}

您可以使用以下两种不同的方法从开发人员控制台手动将沙盒项目休眠：

* 环境详细信息屏幕
* 环境列表屏幕

>[!NOTE]
>Cloud Manager的任何用户都可以访问沙盒项目的开发人员控制台。

请按照以下步骤手动休眠沙盒项目环境：

1. 导航到&#x200B;**开发人员控制台**。
请参阅[访问开发人员控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) ，以了解如何从&#x200B;**Environments**&#x200B;卡访问&#x200B;**开发人员控制台**。
   >[!IMPORTANT]
   >直接从Cloud Manager链接到&#x200B;**开发人员控制台**&#x200B;将不会为您提供将沙盒项目环境休眠的选项。 解决方法是在开发人员控制台中添加一次，在url `#release-cm-p1234-e5678 where 1234` 1234的末尾添加以下模式： *程序ID* , 5678是您的&#x200B;*环境ID*。

1. 单击&#x200B;**Hibernate**，如下图所示：

   ![](assets/hibernate-1.png)

   或者，

   单击左上角的&#x200B;**Environments**&#x200B;链接以查看环境列表，然后单击&#x200B;**Hibernate**，如下图所示：

   ![](assets/hibernate-1b.png)

1. 单击&#x200B;**Hibernate**&#x200B;以确认步骤。

   ![](assets/hibernate-2.png)

1. 成功休眠后，您将在&#x200B;**开发人员控制台**&#x200B;屏幕中看到环境的休眠进程结束通知。

   ![](assets/hibernate-4.png)


## 取消休眠 {#de-hibernation-introduction}

1. 导航到&#x200B;**开发人员控制台**。
请参阅[访问开发人员控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) ，以了解如何从&#x200B;**Environments**&#x200B;卡访问&#x200B;**开发人员控制台**。

   >[!IMPORTANT]
   >直接从Cloud Manager链接到&#x200B;**开发人员控制台**&#x200B;将不会为您提供将沙盒项目环境解除休眠的选项。 解决方法是在开发人员控制台中添加一次，在url `#release-cm-p1234-e5678 where 1234` 1234的末尾添加以下模式： *程序ID* , 5678是您的&#x200B;*环境ID*。

   >[!NOTE]
   >或者，您也可以通过尝试访问已休眠环境的创作、预览或发布服务，导航到&#x200B;**开发人员控制台**&#x200B;以解除休眠；在这种情况下，将显示一个登陆页面，其中包含指向开发人员控制台的链接。 请参阅下面的访问休眠环境部分。

   >[!IMPORTANT]
   >对开发人员控制台的访问权限由&#x200B;**Admin Console**&#x200B;中的&#x200B;**Cloud Manager - Developer Role**&#x200B;定义。 具有开发人员角色权限的用户可以将沙盒项目环境解除休眠。

1. 单击&#x200B;**De-hibernate**，如下图所示：

   ![](assets/de-hibernation-img1.png)

   或者，

   单击左上角的&#x200B;**Environments**&#x200B;链接以查看环境列表，然后单击&#x200B;**De-hibernate**，如下图所示

   ![](assets/de-hibernate-1b.png)


1. 单击&#x200B;**取消休眠**&#x200B;以确认该步骤。

   ![](assets/de-hibernation-img2.png)

1. 您将收到取消休眠过程已开始的通知，并且您将随进度进行更新。

   ![](assets/de-hibernation-img3.png)

1. 流程完成后，沙盒项目环境将再次处于活动状态。

   ![](assets/de-hibernation-img4.png)

### 解除休眠的权限 {#permissions-de-hibernate}

任何具有产品配置文件(该配置文件为用户授予其访问AEM的Cloud Service)的用户都应能够访问&#x200B;**开发人员控制台**，从而允许他们将环境解除休眠。

## 访问休眠环境 {#accessing-hibernated-environment}

当针对休眠环境的创作、预览或发布层发出任何浏览器请求时，用户将会遇到一个登陆页面，用于描述该环境的休眠状态，如下图所示：

![](assets/de-hibernation-img5.png)

## 重要注意事项 {#important-considerations}

与休眠和解除休眠环境相关的几个关键注意事项包括：

* 用户可以使用管道将自定义代码部署到休眠环境。 环境将保持休眠状态，在解除休眠后，新代码将显示在环境中。

* AEM升级可应用于休眠环境，客户可以从Cloud Manager手动触发该环境。 环境将保持休眠状态，在解除休眠后，新版本将显示在环境中。

* 沙盒在处于非活动状态8小时后会进入休眠节点，在此之后，它们可以解除休眠。

* 沙箱在连续休眠模式下6个月后被删除，之后可以重新创建。

   >[!NOTE]
   >目前，Cloud Manager未指示环境是否已休眠。

## AEM对沙盒环境的更新 {#aem-updates-sandbox}

有关更多详细信息，请参阅[AEM版本更新](/help/implementing/deploying/aem-version-updates.md)。

用户可以手动将AEM更新应用到沙盒项目中的环境。

请参阅[更新环境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)以了解如何更新环境。

>[!NOTE]
>* 只有在目标环境具有正确配置的管道时，才能运行手动更新。
>* 手动更新&#x200B;*Production*&#x200B;或&#x200B;*Stage*&#x200B;环境将自动更新另一个环境。 生产+暂存环境集必须位于同一AEM版本上。

