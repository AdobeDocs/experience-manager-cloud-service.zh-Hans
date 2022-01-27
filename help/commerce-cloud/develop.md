---
title: 开发AEM Commerce for AEMas a Cloud Service
description: 了解如何使用AEM项目原型生成启用商务的AEM项目。 了解如何使用AEMas a Cloud ServiceSDK构建项目并将其部署到本地开发环境。
topics: Commerce, Development
feature: Commerce Integration Framework
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
source-git-commit: 3778ed83453ab3e1e01e662a43d4f86988da1668
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 7%

---

# 开发AEM Commerce for AEMas a Cloud Service {#develop}

根据AEM Commerce Integration Framework(CIF)为as a Cloud Service Commerce开发AEM Commerce项目时，也会遵循与AEM as a Cloud Service上的其他AEM项目相同的规则和最佳实践。 请首先查看以下内容：

- [AEM 项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service 开发准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## 使用AEMas a Cloud ServiceSDK进行本地开发 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建议在当地开发环境下与CIF项目合作。 为AEMas a Cloud Service提供的CIF附加组件也可用于本地开发。 可以从 [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

CIF附加组件作为Sling功能存档提供。 Software Distribution门户上提供的zip文件包括两个Sling功能存档文件，一个用于AEM作者，一个用于AEM发布实例。

**是AEMas a Cloud Service的新用户？** 查看 [有关使用AEMas a Cloud Service SDK设置本地开发环境的更详细指南](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html).

### 必需软件

应在本地安装以下内容：

- [AEMas a Cloud ServiceSDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [阿帕奇·马文](https://maven.apache.org/) （3.3.9或更高版本）
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 访问CIF附加组件

CIF附加组件可以从 [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). zip文件包含CIF附加组件，如下所示 **Sling功能存档**，则不是AEM包。 请注意，对SDK列表的访问权限仅限于具有AEMas a Cloud Service许可证的用户。

>[!TIP]
>
>确保始终使用最新的CIF附加组件版本。

### 本地设置

对于使用AEMas a Cloud ServiceSDK进行本地CIF附加组件开发，请执行以下步骤：

1. 获取最新的AEMas a Cloud ServiceSDK
1. 解压缩AEM .jar以创建 `crx-quickstart` 文件夹，运行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 创建 `crx-quickstart/install` 文件夹
1. 将正确的CIF加载项的Sling功能存档文件复制到 `crx-quickstart/install` 文件夹。

   CIF附加组件zip文件包含两个Sling功能存档 `.far` 文件。 确保为AEM创作或AEM发布使用正确的SDK，具体取决于您计划如何运行本地AEMas a Cloud ServiceSDK。

1. 创建名为的本地操作系统环境变量 `COMMERCE_ENDPOINT` 保留Adobe Commerce GraphQL端点。

   Mac OSX示例：

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   示例窗口：

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   AEM使用此变量连接到您的商务系统。 此外，CIF附加组件包含本地反向代理，以使Commerce GraphQL端点在本地可用。 CIF创作工具（产品控制台和选取器）以及执行直接GraphQL调用的CIF客户端组件均使用此功能。

   还必须为AEMas a Cloud Service环境设置此变量。 有关变量的更多信息，请参阅 [为AEMas a Cloud Service配置OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. （可选）要启用暂存目录功能，您必须为Adobe Commerce实例创建集成令牌。 请按照 [快速入门](./getting-started.md#staging) 创建令牌。

   使用名称设置OSGi密钥 `COMMERCE_AUTH_HEADER` 值：

   ```xml
   Authorization: Bearer <Access Token>
   ```

   有关机密的更多信息，请参阅 [为AEMas a Cloud Service配置OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. 启动AEMas a Cloud ServiceSDK

>[!NOTE]
>
>确保在步骤5中设置了环境变量的同一终端窗口中启动AEMas a Cloud ServiceSDK。 如果在单独的终端窗口中启动该变量，或双击.jar文件，请确保显示环境变量。

通过OSGI控制台验证设置： `http://localhost:4502/system/console/osgi-installer`. 该列表应包括特征模型文件中定义的与CIF附加组件相关的包、内容包和OSGI配置。

## 项目设置 {#project}

有两种方法可引导您的CIF项目以用于AEMas a Cloud Service。

### 使用AEM项目原型

的 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 是引导预配置项目以开始使用CIF的主要工具。 CIF核心组件和所有必需的配置都可以包含在生成的项目中，并且还包含一个额外的选项。

>[!TIP]
>
>始终使用 [AEM项目原型](https://github.com/adobe/aem-project-archetype/releases) 以生成项目。

请参阅AEM项目原型 [使用说明](https://github.com/adobe/aem-project-archetype#usage) 关于如何生成AEM项目。 要将CIF包含到项目中，请使用 `includeCommerce` 选项。

例如：

```bash
mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
 -D archetypeGroupId=com.adobe.aem \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=35 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D includeCommerce=y
```

CIF核心组件可通过包含提供的 `all` 包或单独使用CIF内容包和相关OSGi包。 要手动将CIF核心组件添加到项目，请使用以下依赖项：

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

启动CIF项目的第二个选项是克隆和使用 [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store是一个示例参考店面应用程序，用于演示AEM的CIF核心组件的用法。 它旨在作为一组最佳实践示例，以及开发您自己功能的潜在起点。

要开始使用Venia Reference Store，只需克隆Git存储库，然后根据您的需求开始自定义项目即可。

>[!NOTE]
>
>Venia Reference Store项目包含AEM as a Cloud Service和AEM 6.5的两个构建配置文件。请检查 [project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) 以了解它们的使用方式。

## 其他资源

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
