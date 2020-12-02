---
title: 沙箱项目-Cloud Service
description: 沙箱项目-Cloud Service
translation-type: tm+mt
source-git-commit: 8383dc023b35cf76f7dc0e41cedef8cfab7753aa
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 0%

---


# 沙盒程序 {#sandbox-programs}

## 简介 {#introduction}

沙箱项目是AEMCloud Service中可用的两种项目类型之一，另一种是常规项目。

通常，创建沙箱是为了满足培训、运行演示、启用或概念验证(POC)的目的。它们不能载着实时交通。 它们不受[AEM作为Cloud Service承诺的约束](https://www.adobe.com/legal/service-commitments.html)。

在沙箱中创建的环境未配置为自动缩放。 因此，它们不适合用于性能或负载测试。

沙箱项目包括站点和资产，并自动填充Git存储库、开发环境和非生产渠道。  Git存储库会填充基于AEM Project原型的示例项目。

请参阅[了解项目和项目类型](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md)，进一步了解项目类型。

### 沙箱项目{#attributes-sandbox}的属性

沙箱项目具有以下属性：

1. **项目创建：** 沙箱项目创建包括自动：
   * 使用示例代码和内容设置项目
   * 开发环境的创造
   * 创建非生产管道部署到开发环境(主控分支部署到开发环境)

1. **解决方案：** 沙箱项目包括AEM Sites和资产。

1. **AEM更新：** AEM更新可手动应用于沙箱项目中的环境，且不会自动推送。

1. **休眠：** 如果在某一时间段内未检测到环境，沙箱项目中的活动将自动休眠。冬眠环境可以手动解除冬眠。

### 创建沙箱项目{#creating-sandbox-program}

项目创建向导允许您创建沙箱项目。

要了解如何创建沙箱项目，请参阅[创建沙箱项目](/help/onboarding/getting-access-to-aem-in-cloud/creating-a-program.md#create-sandbox-program)以获取更多详细信息。

### 创建沙箱环境{#creating-sandbox-environments}

沙箱项目在创建项目时以自动创建的方式交付给开发环境。 默认情况下，开发环境包括作者层和发布层。

当用户准备好设置生产管道时，可以手动将生产级环境集添加到沙箱项目。

要了解如何手动创建环境，请参阅[添加环境](/help/implementing/cloud-manager/manage-environments.md)以获取更多详细信息。

### 删除沙箱环境{#deleting-sandbox-environments}

具有必要权限的用户可以删除开发或生产／阶段环境或集。

要删除环境，请参阅[删除环境](/help/implementing/cloud-manager/manage-environments.md#deleting-environment)以了解更多详细信息。


## 冬眠和冬眠沙箱环境{#hibernating-introduction}

沙箱项目环境在某段时间内未检测到活动，则进入&#x200B;*休眠模式*。

>[!NOTE]
>休眠是沙箱项目环境特有的。 常规项目环境不休眠。

### 休眠{#hibernation-introduction}

休眠可以自动或手动进行。 沙箱项目环境可能需要几分钟才能进入&#x200B;*休眠模式*。 数据在休眠期间保留。

冬眠分为：

* **自**  动沙箱项目环境在8小时不活动后自动休眠，这意味着作者和发布服务都不会收到请求。

* **手动**:作为用户，您可以手动为沙箱项目环境休眠，但无需这样做，因为休眠将在某段时间（8小时）不活动后自动发生。

>[!CAUTION]
>在最新版本中，直接从云管理器链接到开发人员控制台将不允许您选择休眠沙箱项目环境。 解决方法是在开发人员控制台中添加以下模式，在url `#release-cm-p1234-e5678 where 1234` 1234的末尾添加以下模式：*项目ID*,5678：您的&#x200B;*环境ID*。

#### 使用手动休眠{#using-manual-hibernation}

您可以通过以下两种不同方式从开发人员控制台手动休眠沙箱项目:

* 环境详细信息屏幕
* 环境列表屏幕

>[!NOTE]
>对沙箱项目的开发人员控制台的访问权限适用于Cloud Manager的任何用户。

请按照以下步骤手动为沙箱项目环境休眠：

1. 导航到&#x200B;**开发人员控制台**。
请参阅[访问开发人员控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)，了解如何从&#x200B;**环境**&#x200B;卡访问&#x200B;**开发人员控制台**。
   >[!IMPORTANT]
   >直接从云管理器链接到&#x200B;**开发人员控制台**&#x200B;将不会为您提供让沙箱项目环境休眠的选项。 解决方法是在开发人员控制台中添加以下模式，在url `#release-cm-p1234-e5678 where 1234` 1234的末尾添加以下模式：*项目ID*,5678：您的&#x200B;*环境ID*。

1. 单击&#x200B;**Hibernate**，如下图所示：

   ![](assets/hibernate-1.png)

   或者，

   单击左上方的&#x200B;**环境**&#x200B;链接以视图环境列表，然后单击&#x200B;**Hibernate**，如下图所示：

   ![](assets/hibernate-1b.png)

1. 单击&#x200B;**Hibernate**&#x200B;以确认该步骤。

   ![](assets/hibernate-2.png)

1. 休眠成功后，您将在&#x200B;**开发人员控制台**&#x200B;屏幕中看到环境的休眠过程完成通知。

   ![](assets/hibernate-4.png)


### 解除休眠{#de-hibernation-introduction}

1. 导航到&#x200B;**开发人员控制台**。
请参阅[访问开发人员控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)，了解如何从&#x200B;**环境**&#x200B;卡访问&#x200B;**开发人员控制台**。

   >[!IMPORTANT]
   >直接从云管理器链接到&#x200B;**开发人员控制台**&#x200B;将不会为您提供取消休眠沙箱项目环境的选项。 解决方法是在开发人员控制台中添加以下模式，在url `#release-cm-p1234-e5678 where 1234` 1234的末尾添加以下模式：*项目ID*,5678：您的&#x200B;*环境ID*。

   >[!NOTE]
   >或者，您也可以通过尝试访问已休眠环境的作者或发布服务，导航到&#x200B;**开发人员控制台**&#x200B;以解除休眠；在这种情况下，将显示一个登陆页，其中包含指向“开发人员控制台”的链接。 请参阅下面的访问休眠环境部分。

   >[!IMPORTANT]
   >对开发人员控制台的访问权限由&#x200B;**Admin Console**&#x200B;中的&#x200B;**云管理器——开发人员角色**&#x200B;定义。 具有开发人员角色权限的用户可以解除沙箱项目环境的休眠。

1. 单击&#x200B;**De-hibernate**，如下图所示：

   ![](assets/de-hibernation-img1.png)

   或者，

   单击左上方的&#x200B;**环境**&#x200B;链接以视图环境列表，然后单击&#x200B;**De-hibernate**，如下图所示

   ![](assets/de-hibernate-1b.png)


1. 单击&#x200B;**De Hibernate**&#x200B;以确认该步骤。

   ![](assets/de-hibernation-img2.png)

1. 您将收到解除休眠进程已启动的通知，并将使用进度进行更新。

   ![](assets/de-hibernation-img3.png)

1. 进程完成后，沙箱项目环境将再次处于活动状态。

   ![](assets/de-hibernation-img4.png)

#### 解除休眠的权限{#permissions-de-hibernate}

任何拥有产品用户档案并将Cloud Service访问权限授予AEM的用户都应能够访问&#x200B;**开发人员控制台**，允许他们解除环境的休眠。

#### 访问休眠环境{#accessing-hibernated-environment}

当针对休眠环境的作者层或发布层发出任何浏览器请求时，用户将遇到一个描述该环境的休眠状态的登陆页，如下图所示：

![](assets/de-hibernation-img5.png)

### 重要注意事项{#important-considerations}

与冬眠和脱冬眠环境相关的主要考虑事项很少：

* 用户可以使用管道将自定义代码部署到休眠环境。 环境将保持休眠状态，新代码在解除休眠后将显示在环境中。

* AEM升级可以应用于休眠环境，客户可以从Cloud Manager手动触发这些客户。 环境将保持冬眠状态，新版本在冬眠解除后将显示在环境中。

>[!NOTE]
>目前，云管理器不指示环境是否已休眠。

## AEM对沙箱环境{#aem-updates-sandbox}的更新

有关详细信息，请参阅[AEM版本更新](/help/implementing/deploying/aem-version-updates.md)。

用户可以在沙箱项目中手动将AEM更新应用到环境。

请参阅[更新环境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)以了解如何更新环境。

>[!NOTE]
>* 手动更新只能在目标环境具有正确配置的管道时运行。
>* 手动更新&#x200B;*Production*&#x200B;或&#x200B;*Stage*&#x200B;环境将自动更新另一个。 生产+阶段环境集必须位于同一AEM版本上。






