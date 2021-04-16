---
title: 将AEM Commerce for AEM作为Cloud Service
description: 了解如何使用AEM项目原型生成支持商务的AEM项目。 了解如何使用AEM作为Cloud Service SDK构建项目并将其部署到本地开发环境。
topics: Commerce, Development
feature: Commerce Integration Framework
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
translation-type: tm+mt
source-git-commit: 97574c964e757ffa4d108340f6a4d1819050d79a
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 8%

---

# 将AEM Commerce for AEM开发为Cloud Service{#develop}

以AEM的商务集成框架(CIF)为Cloud Service开发AEM商务项目时，也会遵循与AEM上其他AEM项目一样的相同规则和最佳实践。 请首先查看以下内容：

- [AEM 项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service 开发准则](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## 将AEM作为Cloud Service SDK {#local}的本地开发

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建议当地发展环境与CIF项目合作。 CIF Add-On作为Cloud Service提供给AEM，也可用于当地开发。 可从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载。

CIF Add-On作为Sling功能存档提供。 软件分发门户上提供的zip文件包括两个Sling Feature存档文件，一个用于AEM作者，一个用于AEM发布实例。

**初次使用AEM作为Cloud Service?** 查看更 [详细的指南，使用AEM作为Cloud Service SDK设置本地开发环境](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)。

### 必需软件

应在本地安装以下内容：

- [AEM作为Cloud Service SDK](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) （3.3.9或更高版本）
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 访问CIF加载项

CIF加载项可从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载为zip文件。 zip文件包含CIF加载项作为&#x200B;**Sling Feature归档文件**，它不是AEM包。 请注意，只能以AEM作为Cloud Service许可证的SDK列表访问。

>[!TIP]
>
>确保始终使用最新的CIF Add-On版本。

### 本地设置

对于使用AEM作为Cloud ServiceSDK的本地CIF Add-on开发，请执行以下步骤：

1. 以Cloud Service SDK形式获得最新的AEM
1. 解压缩AEM .jar以创建`crx-quickstart`文件夹，运行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 创建`crx-quickstart/install`文件夹
1. 将CIF加载项的正确Sling Feature存档文件复制到`crx-quickstart/install`文件夹中。

   CIF加载项zip文件包含两个Sling功能存档文件`.far`。 确保为AEM作者或AEM发布使用正确的AEM，具体取决于您计划如何将本地AEM作为Cloud ServiceSDK运行。

1. 创建一个名为`COMMERCE_ENDPOINT`的本地OS环境变量，其中包含MagentoGraphQL端点。

   Mac OSX示例：

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   示例Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   此变量由AEM用于连接到您的商务系统。 此外，CIF加载项包含本地反向代理，使Commerce GraphQL端点可在本地使用。 CIF创作工具（产品控制台和选择器）和执行直接GraphQL调用的CIF客户端组件都使用此功能。

   此变量也必须设置为AEM作为Cloud Service环境。 有关变量的详细信息，请参阅[将AEM的OSGi配置为Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. （可选）要启用分阶段目录功能，您必须为您的Magento实例创建集成令牌。 请按照[入门](./getting-started.md#staging)中的步骤创建令牌。

   将名称为`COMMERCE_AUTH_HEADER`的OSGi机密设置为以下值：

   ```xml
   Authorization: Bearer <Access Token>
   ```

   有关机密的详细信息，请参阅[将AEM的OSGi配置为Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. 将AEM开始为Cloud Service SDK

>[!NOTE]
>
>确保在步骤5中设置了环境变量的同一终端窗口中将AEM开始为Cloud Service SDK。 如果在单独的终端窗口中或通过多次单击.jar文件来开始它，请确保环境变量可见。

通过OSGI控制台验证设置： `http://localhost:4502/system/console/osgi-installer`。 列表应包括特征模型文件中定义的CIF附加包、内容包和OSGI配置。

## 项目设置{#project}

有两种方法可引导您的CIF项目，以便AEM作为Cloud Service。

### 使用AEM Project Archetype

[AEM项目原型](https://github.com/adobe/aem-project-archetype)是引导预配置项目以开始使用CIF的主要工具。 CIF核心组件和所有所需配置都可以包含在生成的项目中，并且还有一个额外选项。

>[!TIP]
>
>使用[AEM Project Archetype 24或更高版本](https://github.com/adobe/aem-project-archetype/releases)生成项目。

有关如何生成AEM项目，请参阅AEM Project Archetype [使用说明](https://github.com/adobe/aem-project-archetype#usage)。 要将CIF包含到项目中，请使用`includeCommerce`选项。

例如：

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=24 \
 -D aemVersion=cloud \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF核心组件可以通过以下方式在任何项目中使用：包括提供的`all`包，或单独使用CIF内容包和相关OSGI包。 要手动将CIF核心组件添加到项目，请使用以下依赖关系：

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### 使用AEM Venia Reference Store

开始CIF项目的第二个选项是克隆并使用[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia Reference Store是示范性参考店面应用程序，用于演示AEM的CIF核心组件的用法。 它旨在作为一组最佳实践示例和开发您自己的功能的潜在起点。

要开始使用Venia Reference Store，只需克隆Git存储库，然后开始根据您的需要自定义项目即可。

>[!NOTE]
>
>Venia Reference Store项目包含两个用于AEM作为Cloud Service和AEM 6.5的构建用户档案。请查看[项目readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)以了解它们的使用方式。

## 其他资源

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
