---
title: Adobe Experience Manager as a Cloud Service 预发行渠道
description: 了解如何使用预发行渠道预览 AEM as a Cloud Service 即将推出的功能。
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
feature: Release Information
role: Admin
source-git-commit: e6567c965a026967e7a5baa67050eb5615979531
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 98%

---


# Adobe Experience Manager as a Cloud Service 预发行渠道 {#prerelease-channel}

了解如何使用预发行渠道预览 AEM as a Cloud Service 即将推出的功能。

## 简介 {#introduction}

Adobe Experience Manager as a Cloud Service 会按照固定节奏定期推出新功能。特定版本的新功能及即将发布功能列表将包含在该版本的[发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)中。

即将发布的功能通常通过以下两种方式之一提供：

* 作为Alpha、Beta或有限可用性计划的一部分
* 作为预发布渠道的一部分

本文档介绍如何启用预发布渠道。预发布渠道可让您抢先体验将在未来 AEM 功能版本中引入的新功能。这使您有机会在功能正式发布前进行验证，并提前规划其采纳与部署。有关 AEM 发布计划的详细信息，请参阅 [Adobe Experience Manager (AEM) as a Cloud Service 的发布说明](/help/release-notes/home.md)文档。

## 启用预发布渠道以访问并试用即将发布的功能 {#enable-prerelease}

可以在任何开发或沙盒环境中启用预发行渠道。预发布渠道无法在预发布或生产环境中启用。

预发布渠道可通过以下两种方式访问：

* [云环境](#cloud-environments)
* [本地 SDK](#local-sdk)

### 云环境 {#cloud-environments}

若要将云环境更新为使用预发布渠道，您必须添加一个新的环境变量。您可以使用 Cloud Manager UI 或通过 CLI 执行此操作。

#### 通过 UI 添加环境变量 {#add-with-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 导航至您希望启用预发布渠道的程序。

1. 选择您希望启用预发布渠道的环境，并通过&#x200B;**程序** > **环境** > **环境配置**&#x200B;访问其配置页面。

1. 添加新[环境变量](/help/implementing/cloud-manager/environment-variables.md):

   | 名称 | 值 | 已应用服务 | 类型 |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | 所有 | 变量 |

1. 保存更改后，环境将刷新并启用预发布渠道。

   ![新环境变量](assets/env-configuration-prerelease.png)

#### 通过 CLI 添加环境变量 {#add-with-cli}

您也可以使用 Cloud Manager API 和 CLI 来更新环境变量。

* 使用 [Cloud Manager API 的环境变量端点](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables)将 `AEM_RELEASE_CHANNEL` 环境变量设置为值 `prerelease`。

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
  aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL "prerelease
  ```

如需将环境恢复为标准模式（非预发布渠道），可删除该变量。

### 本地 SDK {#local-sdk}

您可以在本地 Quickstart SDK 中访问预发布渠道的即将发布功能，并通过将 Maven 项目配置为引用位于 Maven Central 的预发布渠道 `API Jar` 来基于新 API 进行开发。您还可以通过以预发布模式启动常规 Quickstart SDK，在本地开发环境中访问预发布渠道。

#### 以预发布模式启动 Quickstart SDK {#prerelease-mode}

1. 从软件分发页面下载 SDK，并按照[访问 AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)中的说明进行安装。
1. 在启动快速入门 SDK 时，请包含参数 `-r prerelease`。

值为 sticky，因此，只能在第一次启动时选择它。重新安装 SDK 可更改命令行选项。

由于每月功能版本之间可能会有多个 AEM 维护版本，因此，您可以下载这些新的 SDK，并在 maven 项目中引用新的 SDK API Jar 版本。维护版本将不会添加额外的预发行版功能，但可能包括其他较小的更改，例如错误修复、安全修复和性能增强。
Javadocs 将发布到 Maven Central。

#### 针对预发行版 SDK 进行构建 {#build-sdk}

1. 修改您的 maven 项目的 `pom.xml`，以引用已发布到 Maven Central 的其他预发行版 SDK API jar。它包含用于预发行版功能的任何新的 Java API，并且与 SDK API jar 存在依赖关系。它使用相同的版本。

   例如，以下父 pom 的依赖项管理部分中引用常规 API jar 的片段：

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

   若要更改预发行版 SDK，只需将依赖关系从 `com.adobe.aem:aem-sdk-api` 更改为 `com.adobe.aem:aem-prerelease-sdk-api`，如下所述：

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

   像往常一样，单个项目可以使用依赖项。

1. 部署到您的本地服务器。

1. 如果您确认其在本地运行符合预期，可将代码提交至开发分支，并通过 Cloud Manager 的非生产流水线部署至[已启用预发布渠道的环境中。](#cloud-environments)

>[!CAUTION]
> 
> 在部署到暂存或生产环境时，绝不能使用 `aem-prerelease-sdk-api` artifactId。在通过生产管道进行部署时，始终使用 `aem-sdk-api`。同样，不应通过生产管道部署引用预发行版 API 的代码。

[AEM CS SDK 构建分析器 Maven 插件 v1.0 和更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=zh-Hans#developing)将通过检查依赖关系，检测项目中是否使用了预发行版 API。如果分析器找到它，将使用预发行版 SDK API 来分析项目。

## 注意事项 {#considerations}

当使用预发行版渠道时，需要注意以下几项。

* 预发行频道不一定包含将在下一版本中推出的所有新功能。
* 预发行版本中的功能已经过严格测试，有质量保证，旨在提供该功能的完整版而非 Beta 版。如果您发现任何问题，请向我们报告，就像在您怀疑常规 AEM 版本中的功能存在错误时所采取的行动一样。
* 要确认某个环境是否已配置为预发布渠道，请前往 AEM 控制台的&#x200B;**关于**&#x200B;页面，查看 AEM 版本号中是否包含类似 `Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE` 的 `PRERELEASE` 后缀。

![关于](/help/release-notes/assets/about.png)
