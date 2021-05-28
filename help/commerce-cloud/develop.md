---
title: 开发AEM Commerce for AEM as aCloud Service
description: 了解如何使用AEM项目原型生成启用商务的AEM项目。 了解如何使用AEM as a Prodement SDK构建项目并将其部署到本地开发环境。
topics: Commerce, Development
feature: 商务集成框架
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 5%

---

# 开发AEM Commerce for AEM as aCloud Service {#develop}

根据AEM as a AEM的商务集成框架(CIF)开发Cloud Service Commerce项目时，也会遵循与AEM上的其他AEM项目一样的规则和最佳实践，作为Cloud Service。 请首先查看以下内容：

- [AEM 项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service 开发准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## 使用AEM as a Cloud ServiceSDK进行本地开发 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建议在当地开发环境下与CIF项目合作。 AEM作为Cloud Service提供的CIF附加组件也可用于本地开发。 可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载。

CIF附加组件作为Sling功能存档提供。 Software Distribution门户上提供的zip文件包括两个Sling功能存档文件，一个用于AEM作者，一个用于AEM发布实例。

**初次使用AEM as aCloud Service?** 请查 [看更详细的指南，以便使用AEM as a Cloud ServiceSDK设置本地开发环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)。

### 必需软件

应在本地安装以下内容：

- [AEM as a Cloud ServiceSDK](https://experienceleague.adobe.com/docs/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) （3.3.9或更高版本）
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 访问CIF附加组件

CIF加载项可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载为zip文件。 zip文件包含CIF附加组件作为&#x200B;**Sling功能存档**，但它不是AEM包。 请注意，对SDK列表的访问权限仅限于那些将AEM作为Cloud Service许可证的用户。

>[!TIP]
>
>确保始终使用最新的CIF附加组件版本。

### 本地设置

对于使用AEM作为Cloud ServiceSDK的本地CIF附加组件开发，请执行以下步骤：

1. 获取最新的AEM as a Cloud ServiceSDK
1. 解压缩AEM .jar以创建`crx-quickstart`文件夹，运行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 创建`crx-quickstart/install`文件夹
1. 将正确的CIF加载项的Sling功能存档文件复制到`crx-quickstart/install`文件夹中。

   CIF附加组件zip文件包含两个Sling功能存档`.far`文件。 确保为AEM创作或AEM发布使用正确的SDK，具体取决于您计划如何将本地AEM作为Cloud ServiceSDK运行。

1. 创建名为`COMMERCE_ENDPOINT`的本地OS环境变量，其中包含MagentoGraphQL端点。

   Mac OSX示例：

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   示例窗口：

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   AEM使用此变量连接到您的商务系统。 此外，CIF附加组件包含本地反向代理，以使Commerce GraphQL端点在本地可用。 CIF创作工具（产品控制台和选取器）以及执行直接GraphQL调用的CIF客户端组件均使用此功能。

   还必须为AEM as a Target环境设置此变量。 有关变量的更多信息，请参阅[为AEM配置OSGi as aCloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. （可选）要启用暂存目录功能，您必须为Magento实例创建集成令牌。 请按照[快速入门](./getting-started.md#staging)中的步骤创建令牌。

   将名称为`COMMERCE_AUTH_HEADER`的OSGi密钥设置为以下值：

   ```xml
   Authorization: Bearer <Access Token>
   ```

   有关密钥的更多信息，请参阅[为AEM配置OSGi as aCloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)。

1. 将AEM作为Cloud ServiceSDK启动

>[!NOTE]
>
>确保在步骤5中设置的环境变量所在的终端窗口中将AEM作为Cloud ServiceSDK启动。 如果在单独的终端窗口中启动该变量，或双击.jar文件，请确保显示环境变量。

通过OSGI控制台验证设置： `http://localhost:4502/system/console/osgi-installer`。 该列表应包括特征模型文件中定义的与CIF附加组件相关的包、内容包和OSGI配置。

## 项目设置 {#project}

有两种方法可引导您的CIF项目，以便将AEM作为Cloud Service。

### 使用AEM项目原型

[AEM项目原型](https://github.com/adobe/aem-project-archetype)是引导预配置项目以开始使用CIF的主要工具。 CIF核心组件和所有必需的配置都可以包含在生成的项目中，并且还包含一个额外的选项。

>[!TIP]
>
>使用[AEM项目原型24或更高版本](https://github.com/adobe/aem-project-archetype/releases)生成项目。

请参阅AEM项目原型[使用说明](https://github.com/adobe/aem-project-archetype#usage)，了解如何生成AEM项目。 要将CIF包含到项目中，请使用`includeCommerce`选项。

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

CIF核心组件可以在任何项目中使用，方法是包含提供的`all`包，或单独使用CIF内容包和相关OSGI包。 要手动将CIF核心组件添加到项目，请使用以下依赖项：

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

启动CIF项目的第二个选项是克隆并使用[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia Reference Store是一个示例参考店面应用程序，用于演示AEM的CIF核心组件的用法。 它旨在作为一组最佳实践示例，以及开发您自己功能的潜在起点。

要开始使用Venia Reference Store，只需克隆Git存储库，然后根据您的需求开始自定义项目即可。

>[!NOTE]
>
>Venia Reference Store项目包含两个AEM as a Cloud Service和AEM 6.5的生成配置文件。请查看[项目readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)以了解它们的使用方式。

## 其他资源

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
