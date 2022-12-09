---
title: Adobe Experience Manager as a Cloud Service预发行渠道
description: 了解如何使用预发行渠道预览即将推出的功能，以AEMas a Cloud Service。
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: 5b38e7d0ad97cdf8b7d0d5da79cf3d6721fa618a
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 21%

---


# Adobe Experience Manager as a Cloud Service预发行渠道 {#prerelease-channel}

了解如何使用预发行渠道预览即将推出的功能，以AEMas a Cloud Service。

## 简介 {#introduction}

根据，Adobe Experience Manager as a Cloud Service在每月一次的频率上提供了新功能 [Experience Manager发布路线图。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html#aem-as-cloud-service)

为了熟悉计划在下月上线的功能，您可以订阅预发行渠道，该渠道可通过配置开发环境或任何沙盒环境来访问。 您可以预览可通过AEM UI访问的更改，以及针对任何新的预发行API构建代码。

给定月份的预发行功能列表将发布在 [月度发行说明。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## AEMas a Cloud Service版本 {#releases}

AEMas a Cloud Service有两种类型的发行版本。

* **月度版本** 向AEM as a Cloud Service添加功能和特性
* **关键更新** 添加安全更新、性能增强和错误修复，并且每天都会应用。

此模式可确保连续发布，而不会中断服务。

预发行渠道允许您预览计划在即将发布的月度版本中提供的功能，以评估即将推出的功能并针对您自己的项目规划其可能实施。 它允许您提前为下一个月版本进行规划。

例如，如果是5月版，并且您订阅了预发行渠道，则可以评估即将在6月发行的版本中的功能。

![预发行发行频度图](assets/prerelease-cadence.png)

预发行版本为您提供了即将推出的AEMaaCS功能的一个连续的一个月时间，让您有时间评估任何新功能对项目和自定义的影响，并规划此类功能的推出、测试和用户培训。

要有效利用预发行渠道，需要四个步骤。

1. [标记日历](#mark-calendars)
1. [查看发行说明](#release-notes)
1. [访问并尝试新功能](#new-features)
1. [培训用户](#train-users)

## 标记日历 {#mark-calendars}

月度发行日期提前很早计划，发行日期发布在 [Adobe Experience League。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html#aem-as-cloud-service)

请注意发行日期，以便您规划查看和测试即将推出的功能的时间。

## 查看发行说明 {#release-notes}

在日历中标记发行日期后，请务必查看 [Adobe Experience League](/help/release-notes/release-notes-cloud/release-notes-current.md) 网站，以了解最新发行说明。

每个版本都随附有发行说明，其中不仅记录了该版本中的新增功能，还记录了可用于预发行评估的功能。 抢先了解信息，并计划利用AEMaCS的最新功能！

您还可以 [检查已知问题](/help/release-notes/known-issues.md) 与每个版本一起发布的，以便您也能够了解任何技术问题，这些问题可能会对您的评估或最终采用任何新功能构成挑战。

## 启用预发行渠道以访问并尝试新功能 {#new-features}

可在任何开发或沙盒环境中启用预发行渠道。 无法在暂存或生产环境中启用预发行。

可通过不同的方式体验预发行版功能：

* [云环境](#cloud-environments)
* [本地 SDK](#local-sdk)

### 云环境 {#cloud-environments}

要更新云环境以使用预发行版本，您必须添加新的环境变量。 您可以使用Cloud Manager UI或通过CLI来执行此操作。

#### 使用UI添加环境变量 {#add-with-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 导航到要启用预发行功能的程序。

1. 选择要启用预发行版本的环境，并通过访问其配置 **项目** > **环境** > **环境配置**.

1. 添加新 [环境变量:](../implementing/cloud-manager/environment-variables.md)

   | 名称 | 值 | 已应用服务 | 类型 |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | 所有 | 变量 |

1. 保存更改，并且环境将在启用预发布功能后进行刷新。

   ![新环境变量](assets/env-configuration-prerelease.png)

#### 使用CLI添加环境变量 {#add-with-cli}

您还可以使用Cloud Manager API和CLI来更新环境变量。

* 使用 [Cloud Manager API的环境变量端点、](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables) 设置 `AEM_RELEASE_CHANNEL` 环境变量到值 `prerelease`.

   ```text
   PATCH /program/{programId}/environment/{environmentId}/variables
   [
           {
                   "name" : "AEM_RELEASE_CHANNEL",
                   "value" : "prerelease",
                   "type" : "string"
           }
   ]
   ```

* [Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 也可以使用

   ```shell
   aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease
   ```

如果要让环境恢复到常规（非预发行版）渠道的表现，可以删除该变量或者将其设置为其他值。

### 本地 SDK {#local-sdk}

您可以在本地快速入门SDK的站点控制台中看到新功能，并通过将您的Maven项目配置为引用预发行版，在预发行版中看到针对新API的代码 `API Jar` 位于Maven Central。 您还可以通过在预发行模式下启动常规快速入门SDK，在本地开发环境中查看这些预发行功能。

#### 在预发行模式下启动快速启动SDK {#prerelease-mode}

1. 从软件分发门户下载SDK并安装，如 [访问AEMas a Cloud ServiceSDK。](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
1. 在启动快速入门 SDK 时，请包含参数 `-r prerelease`。

值为 sticky，因此，只能在第一次启动时选择它。重新安装SDK以更改命令行选项。

由于每月发布功能间隔可能会有多个 AEM 维护版本，因此，您可以下载这些新的 SDK，并在 maven 项目中引用新的 SDK API Jar 版本。维护版本将不会添加额外的预发行版功能，但可能包括其他较小的更改，例如错误修复、安全修复和性能增强。
Javadocs 将发布到 Maven Central。

#### 针对预发行SDK进行构建 {#build-sdk}

1. 修改maven项目的 `pom.xml` 引用发布到Maven Central的不同预发行SDK API jar。 它包含任何用于预发行功能的新Java API，并且依赖于SDK API Jar。 它使用相同的版本。

   例如，以下是引用常规API Jar的父pom的依赖关系管理部分中的代码片段：

   ```
   <dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
        </dependency>
   ```

   随后是模块中的使用情况：

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   要更改预发行版 SDK，只需将依赖关系从 `com.adobe.aem:aem-sdk-api` 更改为 `com.adobe.aem:aem-prerelease-sdk-api`，如下所述：

   ```
   <dependencyManagement>
    <dependencies>
      <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-prerelease-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
      </dependency>
   <dependencies>
      <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-prerelease-sdk-api</artifactId>
      </dependency>
   ```

   像往常一样，单个项目可以使用依赖关系。

1. 部署到您的本地服务器。。

1. 如果满意地在本地可以按预期工作，请将代码提交到开发分支，然后使用Cloud Manager非生产管道部署到订阅预发行渠道的环境。

>[!CAUTION]
> 
> 的 `aem-prerelease-sdk-api` 部署到暂存或生产时，不得使用artifactId。 始终使用 `aem-sdk-api` 通过生产管道部署时。 同样，引用预发行API的代码也不应通过生产管道进行部署。

的 [AEM CS SDK内部版本分析器maven插件v1.0及更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html#developing) 将通过检查依赖关系来检测项目中是否使用了预发行API。 如果分析器找到它，则将使用预发行的SDK API来分析项目。

## 培训用户 {#train-users}

在预发行渠道中测试了新功能并决定在项目中利用这些功能后，您需要对用户进行培训。

Adobe Experience League提供了大量资源来学习AEMaCS。

* [AEMaCS文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)
* [教程](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-tutorials/overview.html)
* [月度版本概述视频](/help/release-notes/release-notes-cloud/release-notes-current.md#release-video) 发行说明中的

## 注意事项 {#considerations}

使用预发行渠道时，需要注意一些项目。

* 预发行渠道不一定包含要在以下版本中推出的所有新功能。
* 预发行版本中的功能已经过严格测试，有质量保证，旨在提供该功能的完整版而非 Beta 版。如果您发现任何问题，请向我们报告，就像在您怀疑常规 AEM 版本中的功能存在错误时所采取的行动一样。
* 要确定是否为预发行渠道配置了环境，请转到AEM控制台的 **关于** 页面，并检查AEM版本号是否包含 *预发行* 后缀，如 ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![关于](/help/release-notes/assets/about.png)
