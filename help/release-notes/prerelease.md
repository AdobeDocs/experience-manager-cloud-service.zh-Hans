---
title: Adobe Experience Manager as a Cloud Service 预发行渠道
description: 了解如何使用预发行渠道预览 AEM as a Cloud Service 即将推出的功能。
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
feature: Release Information
role: Admin
source-git-commit: 36da09746f02daad82875329b0aa53ee4eb7c074
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 58%

---


# Adobe Experience Manager as a Cloud Service 预发行渠道 {#prerelease-channel}

了解如何使用预发行渠道预览 AEM as a Cloud Service 即将推出的功能。

## 简介 {#introduction}

Adobe Experience Manager as a Cloud Service会定期提供新功能。 [发行说明中发布了给定功能版本的新增功能和即将推出的功能列表。](/help/release-notes/release-notes-cloud/release-notes-current.md)

即将推出的功能通常通过以下两种方式之一提供：

* 作为率先采用者方案的一部分
* 作为预发行渠道的一部分

本文档介绍如何启用预发行版渠道。 通过预发行渠道可访问将在AEM的未来功能版本中引入的早期功能。 这样，您就有机会在未来版本发布之前验证新功能并规划其采用情况。 有关Adobe Experience Manager (AEM) as a Cloud Service[&#128279;](/help/release-notes/home.md)发行计划的详细信息，请参阅文档AEM发行说明。

## 启用预发行渠道以访问和尝试即将推出的功能 {#enable-prerelease}

可以在任何开发或沙盒环境中启用预发行渠道。无法在暂存或生产环境中启用预发行渠道。

可通过两种不同的方式访问预发行版渠道：

* [云环境](#cloud-environments)
* [本地 SDK](#local-sdk)

### 云环境 {#cloud-environments}

要更新云环境以使用预发行版渠道，您必须添加新的环境变量。 您可以使用 Cloud Manager UI 或通过 CLI 执行此操作。

#### 通过 UI 添加环境变量 {#add-with-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 导航到要启用预发行版渠道的程序。

1. 选择要启用预发行渠道的环境，并通过&#x200B;**项目** > **环境** > **环境配置**&#x200B;访问其配置。

1. 添加新[环境变量](/help/implementing/cloud-manager/environment-variables.md):

   | 名称 | 值 | 已应用服务 | 类型 |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | 所有 | 变量 |

1. 保存更改，环境将在启用预发行版渠道的情况下进行刷新。

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

* [也可以使用 Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)

  ```shell
  aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL "prerelease
  ```

如果要将环境恢复为标准行为（非预发行渠道），可以删除该变量。

### 本地 SDK {#local-sdk}

通过配置您的Maven项目引用Maven Central中的预发行版渠道`API Jar`，您可以在本地快速入门SDK的预发行版渠道中访问即将推出的功能，并针对新API进行编码。 您还可以通过在预发行版模式下启动常规快速入门SDK，在本地开发环境中查看访问预发行版渠道。

#### 以预发行模式启动“快速启动 SDK” {#prerelease-mode}

1. 按照[访问SDK SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)中的说明从软件分发和安装下载AEM as a Cloud Service。
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

1. 如果对它在本地按预期方式工作感到满意，请将代码提交到开发分支，并使用Cloud Manager非生产管道部署到启用了预发行版渠道的[环境。](#cloud-environments)

>[!CAUTION]
> 
> 在部署到暂存或生产环境时，绝不能使用 `aem-prerelease-sdk-api` artifactId。在通过生产管道进行部署时，始终使用 `aem-sdk-api`。同样，不应通过生产管道部署引用预发行版 API 的代码。

[AEM CS SDK 构建分析器 Maven 插件 v1.0 和更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=zh-Hans#developing)将通过检查依赖关系，检测项目中是否使用了预发行版 API。如果分析器找到它，将使用预发行版 SDK API 来分析项目。

## 注意事项 {#considerations}

当使用预发行版渠道时，需要注意以下几项。

* 预发行频道不一定包含将在下一版本中推出的所有新功能。
* 预发行版本中的功能已经过严格测试，有质量保证，旨在提供该功能的完整版而非 Beta 版。如果您发现任何问题，请向我们报告，就像在您怀疑常规 AEM 版本中的功能存在错误时所采取的行动一样。
* 要确定是否为预发行版渠道配置了环境，请转到AEM控制台的&#x200B;**关于**&#x200B;页面，并检查AEM版本号是否包含`PRERELEASE`后缀，如`Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE`。

![关于](/help/release-notes/assets/about.png)
