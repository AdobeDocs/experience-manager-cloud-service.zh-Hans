---
title: 使沙盒环境休眠和解除沙盒环境休眠
description: 了解沙盒程序的环境如何自动进入休眠模式，以及如何解除休眠。
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 84%

---


# 使沙盒环境休眠和解除沙盒环境休眠 {#hibernating-introduction}

如果在八小时内未检测到任何活动，沙盒程序的环境将进入休眠模式。休眠是沙盒程序环境所特有的。生产程序环境不休眠。

## 休眠 {#hibernation-introduction}

休眠可以自动或手动进行。

* **自动** – 沙盒程序环境在八小时不活动后自动休眠。 非活动性定义为作者服务和预览或发布服务都不会接收请求。
* **手动** – 作为用户，您可以手动休眠沙盒程序环境。 不需要这样做，因为如前所述，休眠将自动发生。

沙盒程序环境可能需要几分钟才能进入休眠模式。 数据在休眠期间保存。

### 使用手动休眠 {#using-manual-hibernation}

您可以从 Developer Console 手动休眠沙盒程序。 Cloud Manager 的任何用户都可以访问 Developer Console 获取沙盒程序。

按照以下步骤手动休眠沙盒程序环境。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](/help/implementing/cloud-manager/navigation.md#my-programs)** 在控制台中，点按或单击要休眠的程序，以显示其详细信息。

1. 在&#x200B;**环境**&#x200B;信息卡上，单击省略号按钮，然后选择&#x200B;**Developer Console**。

   * 有关 Developer Console 的更多详细信息，请参阅[访问 Developer Console。](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)

   ![Developer Console 菜单选项](assets/developer-console-menu-option.png)

1. 在 Developer Console 中，单击&#x200B;**休眠**。

   ![休眠按钮](assets/hibernate-1.png)

1. 单击&#x200B;**休眠**&#x200B;确认步骤。

   ![确认休眠](assets/hibernate-2.png)

当休眠成功时，您会在中看到针对您环境的休眠进程完成通知 **开发人员控制台** 屏幕。

![休眠确认](assets/hibernate-4.png)

在开发人员控制台中，您还可以单击 **环境** 上面痕迹导航中的链接 **Pod** 要休眠的环境列表的下拉列表。

![要休眠的环境列表](assets/hibernate-1b.png)

## 解除休眠 {#de-hibernation-introduction}

您可以从 Developer Console 手动休眠沙盒程序。

>[!IMPORTANT]
>
>具有&#x200B;**开发人员**&#x200B;角色的用户，可以手动休眠沙盒程序环境。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](/help/implementing/cloud-manager/navigation.md#my-programs)** 在控制台中，点按或单击要解除休眠的程序，以显示其详细信息。

1. 在&#x200B;**环境**&#x200B;信息卡上，单击省略号按钮，然后选择&#x200B;**Developer Console**。

   * 有关 Developer Console 的更多详细信息，请参阅[访问 Developer Console。](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)

1. 单击 **解除休眠**.

   ![解除休眠按钮](assets/de-hibernation-img1.png)

1. 单击&#x200B;**解除休眠**&#x200B;确认步骤。

   ![确认解除休眠](assets/de-hibernation-img2.png)

1. 您会收到通知，告知解除休眠进程已启动，并随进度更新。

   ![休眠进度通知](assets/de-hibernation-img3.png)

1. 一旦过程完成，沙盒程序环境将再次处于活动状态。

   ![解除休眠完成](assets/de-hibernation-img4.png)


在开发人员控制台中，您还可以单击 **环境** 上面痕迹导航中的链接 **Pod** 要解除休眠的环境列表的下拉列表。

![休眠 Pod 列表](assets/de-hibernate-1b.png)

### 解除休眠的权限 {#permissions-de-hibernate}

任何拥有将 AEM as a Cloud Service 访问权限的产品配置文件的用户都应该能够访问&#x200B;**Developer Console**，从而使他们能够解除环境休眠。

## 正在访问休眠环境 {#accessing-hibernated-environment}

当对休眠环境的作者、预览或发布服务发出任何浏览器请求时，用户将看见描述环境休眠状态的登陆页面，以及一个指向可在其中解除服务休眠的 Developer Console 的链接。

![休眠服务登陆页面](assets/de-hibernation-img5.png)

## 部署和 AEM 更新 {#deployments-updates}

休眠环境仍然允许部署和手动 AEM 升级。

* 用户可以使用管道将自定义代码部署到休眠环境。 环境将保持休眠状态，一旦解除休眠，新代码将出现在环境中。

* AEM 升级可应用于休眠环境，并可从 Cloud Manager 手动触发。 环境将保持休眠状态，一旦解除休眠，新版本将出现在环境中。

## 休眠和删除 {#hibernation-deletion}

* 沙盒程序中的环境在八小时不活动后自动休眠。
   * 非活动性定义为作者服务和预览或发布服务都不会接收请求。
   * 休眠后，可以将它们[手动解除休眠](#de-hibernation-introduction)。
* 沙盒程序在连续休眠模式下运行六个月后会被删除，然后可以重新创建。

>[!NOTE]
>
>在连续休眠六个月后，只有沙盒环境会自动删除。保留沙盒程序及其存储库和代码。
