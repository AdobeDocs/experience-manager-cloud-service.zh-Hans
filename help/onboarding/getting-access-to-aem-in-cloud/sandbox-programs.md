---
title: 沙箱项目-云服务
description: 沙箱项目-云服务
translation-type: tm+mt
source-git-commit: da965462eddae8b359a6d327a7fe3caf6bfe95ae
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---


# 沙箱项目 {#sandbox-programs}

## 简介 {#introduction}

沙箱项目是AEM Cloud Service中可用的两种项目类型之一，另一种是常规项目。

通常，创建沙箱是为了满足培训、运行演示、启用或概念验证(POC)的目的。 它们不能载着实时交通。 他们不受AEM作 [为云服务承诺的约束](https://www.adobe.com/legal/service-commitments.html)。

在沙箱中创建的环境未配置为自动缩放。 因此，它们不适合用于性能或负载测试。

沙箱项目包括站点和资产，并自动填充Git存储库、开发环境和非生产渠道。  Git存储库会填充基于AEM Project原型的示例项目。

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

要了解如何创建沙箱项目，请参阅创 [建沙箱项目以获取更](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-sandbox-program) 多详细信息。

### 创建沙箱环境 {#creating-sandbox-environments}

沙箱项目在创建项目时以自动创建的方式交付给开发环境。 默认情况下，开发环境包括作者层和发布层。

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

* **手动**: 作为用户，您可以手动为沙箱项目环境休眠，但无需这样做，因为休眠将在某段时间（8小时）不活动后自动发生。

>[!CAUTION]
>在最新版本中，直接从云管理器链接到开发人员控制台将不允许您选择休眠沙箱项目环境。 解决方法是在“开发人员控制台”上添加以下模式，在url 1234的末尾添加 `#release-cm-p1234-e5678 where 1234` 以下模式：您的 *项目ID* ,5678是您 *的环境ID*。

#### 使用手动休眠 {#using-manual-hibernation}

您可以通过以下两种不同方式从开发人员控制台手动休眠沙箱项目:

* 环境详细信息屏幕
* 环境列表屏幕

请按照以下步骤手动为沙箱项目环境休眠：

1. 导航到开发 **人员控制台**。
请参阅访 [问开发人员控制台](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) ，了解如何从 **环境卡访** 问开发人 **员控制** 台。
   >[!IMPORTANT]
   >直接从云管 **理器链接到** “开发人员控制台”时，您不能选择让沙箱环境休眠。 解决方法是在“开发人员控制台”上添加以下模式，在url 1234的末尾添加 `#release-cm-p1234-e5678 where 1234` 以下模式：您的 *项目ID* ,5678是您 *的环境ID*。

1. Click **Hibernate**, as shown in the figure below:

   ![](assets/hibernate-1.png)

   或者，

   单击左 **上方** 的环境链接以视图环境列表，然后 **单击Hibernate**，如下图所示：

   ![](assets/hibernate-1b.png)

1. 单击 **Hibernate** 以确认该步骤。

   ![](assets/hibernate-2.png)

1. 休眠成功后，您将在“开发人员控制台”屏幕中看到环境的休眠过 **程完成通知** 。

   ![](assets/hibernate-4.png)


### 解除休眠 {#de-hibernation-introduction}

1. 导航到开发 **人员控制台**。
请参阅访 [问开发人员控制台](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) ，了解如何从 **环境卡访** 问开发人 **员控制** 台。

   >[!IMPORTANT]
   >直接从云管 **理器链接到** “开发人员控制台”时，您不能选择解除沙箱项目环境的休眠。 解决方法是在“开发人员控制台”上添加以下模式，在url 1234的末尾添加 `#release-cm-p1234-e5678 where 1234` 以下模式：您的 *项目ID* ,5678是您 *的环境ID*。

   >[!NOTE]
   >或者，您也可以通过尝试访 **问已休眠环境的作者或发布服务** ，导航到开发人员控制台以解除休眠； 在这种情况下，将显示一个登陆页，其中包含指向“开发人员控制台”的链接。 请参阅下面的访问休眠环境部分。

   >[!IMPORTANT]
   >对开发人员控制台的访问权限由 **Admin Console中的云管理器** -开发人 **员角色定义**。 具有开发人员角色权限的用户可以解除沙箱项目环境的休眠。

1. 单击“ **取消休眠**”，如下图所示：

   ![](assets/de-hibernation-img1.png)

   或者，

   单击左 **上方** 的环境链接以视图环境列表，然后 **单击“取消休眠**”，如下图所示

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

### 重要注意事项 {#important-considerations}

与冬眠和脱冬眠环境相关的主要考虑事项很少：

* 用户可以使用管道将自定义代码部署到休眠环境。 环境将保持休眠状态，新代码在解除休眠后将显示在环境中。

* AEM升级可应用于冬眠环境，客户可以从Cloud Manager手动触发。 环境将保持冬眠状态，新版本在冬眠解除后将显示在环境中。

>[!NOTE]
>目前，云管理器不指示环境是否已休眠。

## 对沙箱环境的AEM更新 {#aem-updates-sandbox}

有关更多 [详细信息，请参](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates) 阅AEM版本更新。

用户可以在沙箱项目中手动将AEM更新应用到环境。

请参阅 [更新环境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#updating-dev-environment) ，了解如何更新环境。

>[!NOTE]
>* 手动更新只能在目标环境具有正确配置的管道时运行。
>* 手动更新生产 *环境* 或 *阶段* 将自动更新其它更新。 生产+阶段环境集必须位于同一AEM版本中。






