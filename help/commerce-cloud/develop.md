---
title: 开发AEM Commerce for AEM作为Cloud Service
description: 了解如何使用AEM项目原型生成支持商务的AEM项目。 了解如何使用AEM作为Cloud ServiceSDK构建项目并将其部署到本地开发环境。
topics: Commerce, Development
feature: Commerce Integration Framework
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 8%

---


# 开发AEM Commerce for AEM作为Cloud Service {#develop}

根据AEM的商务集成框架(CIF)作为Cloud Service开发AEM商务项目，也遵循相同的规则和最佳做法，如其他AEM项目作为Cloud Service。 请首先查看以下内容：

- [AEM 项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM 云服务 SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM 云服务开发准则](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## 以AEM作为Cloud ServiceSDK的本地开发 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建议建立一个地方发展环境，与CIF项目合作。 CIF Add-On作为Cloud Service环境提供给AEM，也可用于本地开发。 可从软件分发门 [户下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。

CIF Add-On作为Sling功能存档提供。 软件分发门户上提供的zip文件包括两个Sling Feature存档文件，一个用于AEM作者，一个用于AEM发布实例。

**刚从AEM当Cloud Service?** 查看更 [详细的指南，使用AEM作为环境SDK设置本地开发Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)。

### 所需软件

应在本地安装以下内容：

- [AEM 云服务 SDK](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) （3.3.9或更高版本）
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 访问CIF加载项

The CIF add-on can be downloaded as a zip file from the [Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). zip文件包含CIF加载项作为Sling功 **能存档**，它不是AEM包。 请注意，对SDK列表的访问仅限于AEM作为Cloud Service许可证的用户。

>[!TIP]
>
>确保始终使用最新的CIF加载项版本。

### 本地设置

对于将AEM用作Cloud ServiceSDK的本地CIF Add-on开发，请执行以下步骤：

1. 获取最新的AEM作为Cloud ServiceSDK
2. 解压缩AEM .jar以创建文 `crx-quickstart` 件夹，运行：

   ```bash
   java -jar <jar name> -unpack
   ```

3. Create a `crx-quickstart/install` folder
4. 将CIF加载项的正确Sling功能存档文件复制到文 `crx-quickstart/install` 件夹。

   CIF加载项zip文件包含两个Sling Feature存档 `.far` 文件。 请确保为AEM作者或AEM发布使用正确的版本，具体取决于您计划如何将本地AEM作为Cloud ServiceSDK运行。

5. 创建一个名为保存环境GraphQL端点 `COMMERCE_ENDPOINT` 的本地OSMagento变量。

   Mac OSX示例：

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   示例Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   此变量也必须设置为AEM的Cloud Service环境。

6. 开始AEM作为Cloud ServiceSDK

7. 开始本地GraphQL代理服务器

   要使MagentoGraphQL端点在本地可用于CIF加载项和CIF组件，请使用以下命令。 GraphQL端点随后将在上可用 `http://localhost:3002/graphql`。
Mac OSX示例：

   ```bash
   npx local-cors-proxy --proxyUrl https://demo.magentosite.cloud --port 3002 --proxyPartial ''
   ```

   示例Windows:

   ```bash
   npx local-cors-proxy --proxyUrl https://demo.magentosite.cloud --port 3002 --proxyPartial '""'
   ```
   该参 `--proxyPartial` 数需要接收空字符串。

   可以通过指向GraphQL查询工具测试本地GraphQL代理，并 `http://localhost:3002/graphql` 测试几个查询。

8. 登录AEM SDK并配置CIF以使用本地GraphQL代理服务器

   导航到CIFCloud Service配置(“工具”>“Cloud Services”>“CIF配置”)。 打开项目所使用的配置的属性视图符。

   对于该 `GraphQL Proxy Path` 属性，请使用本地代理服务器端点 `http://localhost:3002/graphql`。 保存配置。

>[!NOTE]
>
>请勿将步骤8的配置推入项目回购。 仅本地开发设置需要此配置。 AEM作为Cloud Service环境已在入门过程中使用GraphQL代理设置。

通过OSGI控制台验证设置：`http://localhost:4502/system/console/osgi-installer`。 列表应包括特征模型文件中定义的CIF附加捆绑包、内容包和OSGI配置。

## 项目设置 {#project}

有两种方法可以将AEM作为Cloud Service引导CIF项目。

### 使用AEM Project Archetype

AEM [Project Archetype](https://github.com/adobe/aem-project-archetype) 是引导预配置项目以开始使用CIF的主要工具。 CIF核心组件和所有所需配置都可以包含在一个生成的项目中，同时还有一个额外的选项。

>[!TIP]
>
>使 [用AEM Project Archetype 24或更高版本](https://github.com/adobe/aem-project-archetype/releases) ，生成项目。

请参阅AEM项目原型 [使用说明](https://github.com/adobe/aem-project-archetype#usage) ，了解如何生成AEM项目。 要将CIF包括到项目中，请使用 `includeCommerce` 选项。

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

CIF核心组件可以在任何项目中使用，包括提供的 `all` 包或单独使用CIF内容包和相关OSGI包。 要将CIF核心组件手动添加到项目，请使用以下相关性：

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
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

开始CIF项目的第二个选项是克隆并使用AEM [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia Reference Store是示范AEM CIF核心组件用法的参考店面应用程序示例。 它旨在作为一组最佳实践示例，也是开发您自己功能的潜在起点。

要开始使用Venia Reference Store，只需克隆Git存储库，并根据您的需要自定义项目的开始即可。

>[!NOTE]
>
>Venia Reference Store项目包含两个构建用户档案，作为Cloud Service和AEM 6.5。请查 [看项目readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) ，了解如何使用它们。

## 其他资源

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
