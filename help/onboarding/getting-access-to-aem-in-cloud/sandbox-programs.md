---
title: 沙箱项目-云服务
description: 沙箱项目-云服务
translation-type: tm+mt
source-git-commit: eb874176c71d7f3d03d953f7bae4cb3db2ffb3b9
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# 沙箱项目 {#sandbox-programs}

## 简介 {#introduction}

沙箱项目是AEM Cloud Service中可用的两种项目类型之一，另一种是常规项目。

通常，创建沙箱是为了满足培训、运行演示、启用或POC的目的。 它们不能载着实时交通。

沙箱项目包括站点和资产，将自动填充包含示例代码、开发环境和非生产渠道的Git分支。

有关项目类型的详细信息，请参 [阅了解项目和项目类型](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html)。

### 沙箱项目的属性 {#attributes-sandbox}

沙箱项目具有以下属性：

1. **项目创建：** 沙箱项目创建包括自动：
   * 使用示例代码和内容设置项目
   * 开发环境的创造
   * 创建非生产管道部署到开发环境(主分支部署到开发环境)

1. **解决方案包括：** 沙箱项目包括站点和资源。

1. **AEM更新：** AEM更新可手动应用于沙箱项目中的环境，且不会自动推送。

1. **休眠：** 如果在某段时间内未检测到环境，沙箱项目中的活动将自动休眠。 冬眠环境可以手动解除冬眠。

### 创建沙箱项目 {#creating-sandbox-program}

项目创建向导将要求用户提交详细信息。

有关如何创建沙箱项目的信息，请参 [阅创建沙箱项目](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)。

### 创建沙箱环境 {#creating-sandbox-environments}

在创建项目时，沙箱项目将以自动创建的方式交付开发环境。 默认情况下，开发环境包含作者层和发布层。

当用户准备好设置生产管道时，可以手动将生产级环境集添加到沙箱项目。

有关如何手动创建环境的信息，请参阅添 [加环境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)。

### 删除沙箱环境  {#deleting-sandbox-environments}

具有必要权限的用户将能够删除开发或生产／阶段环境/集。

有关如何删除环境的信息，请参阅删 [除环境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment)。


## 冬眠和冬眠沙箱环境 {#hibernating-introduction}

沙箱项目 *环境在一段时* 间不活动后将进入休眠模式。

>[!NOTE]
>休眠是沙箱项目环境特有的。 普通项目环境不会冬眠。

### 冬眠 {#hibernation-introduction}

休眠可以自动或手动进行。 环境可能需要几分钟才能冬眠。 数据在休眠期间保留。

冬眠分为：

* **自动沙箱** 项目环境在8小时不活动后自动休眠，这意味着作者或发布服务都不会收到请求。

* **手动**: 客户可以手动为沙箱项目环境休眠，但无需这样做，因为休眠将在一段不活动期后自动发生。

#### 使用手动休眠 {#using-manual-hibernation}


手动休眠可以从开发人员控制台中的两个屏幕中的任何一个完成。

请按照以下步骤手动为项目环境休眠：

1. 导航到开发人员控制台。
1. 单击“休眠”
1. 单击“休眠”进行确认。
1. 休眠成功后，您将看到以下屏幕。
1. 在环境列表屏幕（如下图所示）上，单击环境详细信息屏幕中的环境链接即可访问该屏幕)，可以在预期环境的行中单击Hibernate按钮。 随后将显示确认屏幕。

### 解除休眠 {#de-hibernation-introduction}

>[!IMPORTANT]
>对开发人员控制台的访问权限由管理控制台中的“云管理者——开发人员角色”定义。 通过该权限，用户可以解除环境的休眠。

### 访问休眠环境 {#accessing-hibernated-environment}

当针对休眠环境的作者层或发布层发出任何浏览器请求时，用户将遇到描述该环境的休眠状态的登陆页，如下所示：

具有“云管理器——开发人员角色”的用户可以单击“开发人员控制台”按钮以访问开发人员控制台并解除环境。 有关设置角色的信息，请参阅云管理器文档。

如果组织中的用户无法单击“开发人员控制台”按钮以进入开发人员控制台，则可能需要为他们提供“云管理器——开发人员角色”。




## 对沙箱环境的AEM更新 {#aem-updates-sandbox}


请参阅 [AEM版本更新](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates)。

用户可以在沙箱项目中手动将AEM更新应用到环境（请参阅下图）。 当显示的状态为“可用更新”时，可以执行此操作。 “更新”选项将从环境卡的下拉菜单中可用。 也可以从环境屏幕的“管理”菜单中选择它。

>[!NOTE]
>必须配置部署到所关注开发环境的非生产管线，以便启动手动更新管线。

>[!NOTE]
>必须配置生产管线，以便启动手动更新管线至“生产+阶段”环境集。

>[!NOTE]
>手动更新生产或阶段环境将自动更新另一个。 生产+阶段环境集必须位于同一AEM版本中。





