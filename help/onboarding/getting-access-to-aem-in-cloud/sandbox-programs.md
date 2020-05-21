---
title: 沙箱项目-云服务
description: 沙箱项目-云服务
translation-type: tm+mt
source-git-commit: e25e22c5d61defb3402e51b97c1d5364465e1027
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---


# 沙箱项目 {#sandbox-programs}

## 简介 {#introduction}

沙箱项目是AEM Cloud Service中可用的两种项目类型之一，另一种是常规项目。

通常，创建沙箱是为了满足培训、运行演示、启用或概念验证(POC)的目的。 它们不能载着实时交通。

沙箱项目包括站点和资产，并自动填充Git分支，该分支包括示例代码、开发环境和非生产渠道。

请参阅了 [解项目和项目类型](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html) ，进一步了解项目类型。

### 沙箱项目的属性 {#attributes-sandbox}

沙箱项目具有以下属性：

1. **项目创建：** 沙箱项目创建包括自动：
   * 使用示例代码和内容设置项目
   * 开发环境的创造
   * 创建非生产管道部署到开发环境(主分支部署到开发环境)

1. **解决方案：** 沙箱项目包括AEM Sites和资产。

1. **AEM更新：** AEM更新可手动应用于沙箱项目中的环境，且不会自动推送。

1. **休眠：** 如果在某段时间内未检测到环境，沙箱项目中的活动会自动休眠。 冬眠环境可以手动解除冬眠。

### 创建沙箱项目 {#creating-sandbox-program}

项目创建向导允许您创建沙箱项目。

要了解如何创建沙箱项目，请参阅。

### 创建沙箱环境 {#creating-sandbox-environments}

沙箱项目在创建项目时以自动创建的方式交付开发环境。 默认情况下，开发环境包括作者层和发布层。

当用户准备好设置生产管道时，可以手动将生产级环境集添加到沙箱项目。

要了解如何手动创建环境，请参阅添 [加环境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments) ，了解详细信息。

### 删除沙箱环境 {#deleting-sandbox-environments}

具有必要权限的用户可以删除开发或生产／阶段环境或集。

要删除环境，请参阅删 [除环境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment) ，了解详细信息。


## 冬眠和冬眠沙箱环境 {#hibernating-introduction}

如果在某一时间段内 *未检测到项目* ，沙箱活动环境将进入休眠模式。

>[!NOTE]
>休眠是沙箱项目环境特有的。 常规项目环境不休眠。

### 冬眠 {#hibernation-introduction}

休眠可以自动或手动进行。 沙箱项目环境进入休眠模式可能需要几分钟 *时间*。 数据在休眠期间保留。

冬眠分为：

* **自动沙箱** 项目环境在8小时不活动后自动休眠，这意味着作者和发布服务都不会收到请求。

* **手动**: 作为用户，您可以手动为沙箱项目环境休眠，但无需这样做，因为休眠将在特定时间段（8小时）不活动后自动发生。

#### 使用手动休眠 {#using-manual-hibernation}

您可以通过以下两种不同方式从开发人员控制台手动休眠沙箱项目:

* 环境详细信息屏幕
* 环境列表屏幕

请按照以下步骤手动为沙箱项目环境休眠：

1. 导航到开发 **人员控制台**。
请参阅访 [问开发人员控制台](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) ，了解如何从 **环境卡访** 问开发人 **员控制** 台。

1. Click **Hibernate**, as shown in the figure below:

   ![](assets/hibernate-1.png)

   或者，

   从 **环境** 列表中单击Hibernate，如下图所示：

   ![](assets/hibernate-1b.png)

1. 单击 **Hibernate** 以确认该步骤。

   ![](assets/hibernate-2.png)

1. 休眠成功后，您将在“开发人员控制台”屏幕中看到环境的休眠过 **程完成通知** 。

   ![](assets/hibernate-4.png)


### 解除休眠 {#de-hibernation-introduction}

1. 导航到开发 **人员控制台**。
请参阅访 [问开发人员控制台](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) ，了解如何从 **环境卡访** 问开发人 **员控制** 台。

   >[!IMPORTANT]
   >对开发人员控制台的访问权限由 **Admin Console中的云管理器** -开发人 **员角色定义**。 具有开发人员角色权限的用户可以解除沙箱项目环境的休眠。

1. 单击“ **取消休眠**”，如下图所示：

   ![](assets/de-hibernation-img1.png)

   或者，

   单击 **环境** 列 **表中的** De-hibernate，如下图所示：

   ![](assets/de-hibernate-1b.png)


1. 单击 **“取消** Hibernate”以确认该步骤。

   ![](assets/de-hibernation-img2.png)

1. 您将收到解除休眠进程已启动的通知，并将使用进度进行更新。

   ![](assets/de-hibernation-img3.png)

1. 进程完成后，沙箱项目环境将再次处于活动状态。

   ![](assets/de-hibernation-img4.png)

#### 访问休眠环境 {#accessing-hibernated-environment}

当针对休眠环境的作者层或发布层发出任何浏览器请求时，用户将遇到一个描述该环境的休眠状态的登陆页，如下图所示：

![](assets/de-hibernation-img5.png)


具有云管理 **器——开发人员角色的用户** ，可以单 **击开发人员控制台** 以访问开发人员控制台，并解除环境的休眠。

>[!NOTE]
> Cloud Manager中的许多功能需要特定权限才能运行。 要进一步了解控制特定功能可用性的用户的角色，请参阅添[加用户和角色](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html)。

## 对沙箱环境的AEM更新 {#aem-updates-sandbox}

有关更多 [详细信息，请参](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates) 阅AEM版本更新。

用户可以在沙箱项目中手动将AEM更新应用到环境。

请参阅 [更新环境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#updating-dev-environment) ，了解如何更新环境。

>[!NOTE]
>必须 *配置部署到所关注开发环境* 的非生产管道，以便启动手动更新管道。

>[!NOTE]
>必 *须配置生* 产管道，以便启动手动更新管道至“生产+阶段”环境集。

>[!NOTE]
>手动更新生产 *环境* 或 *阶段* 将自动更新其他产品。 生产+阶段环境集必须位于同一AEM版本中。





