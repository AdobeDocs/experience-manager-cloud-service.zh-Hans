---
title: '[!DNL Adobe Experience Manager] 作为Cloud Service预发行渠道'
description: '[!DNL Adobe Experience Manager] 作为Cloud Service预发行渠道'
source-git-commit: 4ee9a5744cdcec00dd497a00b0d8dbf288a5adcb
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 作为Cloud Service预发行渠道  {#prerelease-channel}


## 简介 {#introduction}

[!DNL Adobe Experience Manager] as aCloud Service根据Experience Manager版路线图计划，在每月的频率下提 [供新功能](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service)。为了熟悉计划在下月上线的功能，客户可以订阅预发行渠道，该渠道可通过在标准项目开发环境或任何沙盒项目环境中进行适当配置来访问。 客户可以预览站点控制台的更改，并针对任何新的预发行API构建代码。

给定月份的预发行功能列表将发布在[月度发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)中。

>[！视频](/help/release-notes/assets/prerelease-overview.mp4)

## 如何启用预发行版本{#enable-prerelease}

预发行功能的体验方式不同：

* 云环境（标准项目开发环境或任何沙盒项目环境类型）
* 本地SDK

### 云环境{#cloud-environments}

要在云开发环境的站点控制台中查看新增功能以及任何项目自定义的结果，请执行以下操作：

* 使用[Cloud Manager API的环境变量端点](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables)，将&#x200B;**AEM_RELEASE_CHANNEL**&#x200B;环境变量设置为值&#x200B;**prerelease**。

```
PATCH /program/{programId}/environment/{environmentId}/variables
[
        {
                "name" : "AEM_RELEASE_CHANNEL",
                "value" : "prerelease",
                "type" : "string"
        }
]
```

按照[https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)中的说明，也可以使用Cloud Manager CLI
```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


如果您希望将环境恢复为常规（非预发行）渠道的行为，则可以删除该变量或将其重新设置为其他值

### 本地SDK {#local-sdk}

您可以在本地快速入门SDK的站点控制台中看到新功能，并通过让您的Maven项目引用预发行版`API Jar`（位于Maven Central）来在预发行版中针对新API编码。 您还可以通过在预发行模式下启动常规快速启动SDK，在本地计算机上查看以下预发行功能：

* 从软件分发门户下载SDK并安装，如[访问AEM as a Software SDK](/help/implementing/developing/aem-as-a-cloud-service-sdk.md#accessing-the-aem-as-a-cloud-service-sdk.)中所述
* 启动SDK快速启动时，请包含参数`-r prerelease`。
* 该值为&#x200B;*sticky*，因此只能在首次启动时选择该值。 重新安装SDK以更改命令行选项。

由于每月发布的功能之间可能有多个AEM维护版本，因此您可以下载这些新的SDK并在Maven项目中引用新的SDK API Jar版本。 维护版本不会添加其他预发行功能，但可能会包含其他较小的更改，例如错误修复、安全修复和性能增强。
Javaoc将发布到Maven Central。

要针对预发行SDK进行构建，请执行以下操作：

1. 修改maven项目的pom.xml以引用一个不同的预发行sdk api jar，该api jar将发布到Maven中心。 它包含预发行功能的任何新Java api，并且依赖于sdk api jar。 它使用相同的版本。

   例如，以下是父pom的依赖关系管理部分中引用常规API Jar的代码片段：

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

   然后，在模块中使用：

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   要更改到预发行SDK，只需将依赖项从`com.adobe.aem:aem-sdk-api`更改为`com.adobe.aem:aem-prerelease-sdk-api`，如下所述：

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

   与往常一样，单个项目可以使用依赖项。

1. 部署到本地服务器
1. 如果满意地在本地可以按预期工作，请将代码提交到开发分支，然后使用Cloud Manager非生产管道部署到订阅预发行渠道的环境

>[!CAUTION]
部署到Stage或Production时，不得使用`aem-prerelease-sdk-api` artifactId。 在通过生产管道部署时，始终使用aem-sdk-api。 同样，引用预发行API的代码也不应通过生产管道进行部署。

[AEM CS SDK构建分析器maven插件v1.0及更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)将通过检查依赖关系来检测项目中是否使用了预发行api。 如果分析器找到它，则将使用预发行sdk api来分析项目。

## 注意事项 {#considerations}

在涉及预发行渠道时，请注意以下几点：

* 下月版本中将推出的某些功能可能未包含在预发行渠道中。
* 预发行版中的功能经过严格的质量保证，旨在实现功能完整而不是测试版质量。 如果您发现任何问题，请像报告常规AEM版本中的功能中存在错误一样报告这些问题。
* 要确定是否为预发行渠道配置了环境，请转到AEM控制台的&#x200B;**关于**&#x200B;页面，并检查AEM版本号是否包含&#x200B;*预发行*&#x200B;后缀，如```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```。

![关于](/help/release-notes/assets/about.png)
