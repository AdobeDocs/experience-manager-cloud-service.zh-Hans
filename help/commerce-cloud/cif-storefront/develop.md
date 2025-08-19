---
title: 为AEM as a Cloud Service开发AEM Commerce
description: 了解如何使用AEM项目原型生成支持商务的AEM项目。 了解如何使用AEM as a Cloud Service SDK构建项目并将项目部署到本地开发环境。
topics: Commerce, Development
feature: Commerce Integration Framework
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
index: false
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 5%

---


# 为AEM as a Cloud Service开发AEM Commerce {#develop}

基于适用于AEM的Commerce integration framework (CIF)开发AEM as a Cloud Service Commerce项目时，遵循与AEM as a Cloud Service上的其他AEM项目相同的规则和最佳实践。 请先查看以下内容：

* [AEM 项目结构](/help/implementing/developing/introduction/aem-project-content-package-structure.md)
* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [AEM as a Cloud Service 开发准则](/help/implementing/developing/introduction/development-guidelines.md)

## 使用AEM as a Cloud Service SDK进行本地开发 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

建议使用本地开发环境来处理CIF项目。 为AEM as a Cloud Service提供的CIF加载项也可用于本地开发。 可从[软件分发门户下载。](/help/implementing/developing/tools/package-manager.md#software-distribution)

CIF加载项是作为Sling功能存档提供的。 软件分发门户上提供的zip文件包括两个Sling功能存档文件，一个用于AEM创作，一个用于AEM发布实例。

>[!TIP]
>
>**是AEM as a Cloud Service新用户？**
>&#x200B;>查看[有关使用AEM as a Cloud Service SDK设置本地开发环境的更详细指南。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)

### 所需的软件 {#required-software}

下列内容应本地安装：

* [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
* [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
* [Apache Maven](https://maven.apache.org/)（3.3.9 或更新版本）
* [Node.js v10+](https://nodejs.org/en)
* [npm 6+](https://www.npmjs.com/)
* [Git](https://git-scm.com/)

### 访问CIF加载项 {#accessing-add-on}

可以从[软件分发门户以zip文件的形式下载CIF加载项。](/help/implementing/developing/tools/package-manager.md) zip文件包含CIF加载项作为&#x200B;**Sling功能存档**，它不是AEM包。 可使用SDK许可证访问AEM as a Cloud Service列表。

>[!TIP]
>
>确保始终使用最新的CIF加载项版本。

### 本地设置 {#local-setup}

对于使用CIF SDK进行本地AEM as a Cloud Service加载项开发，请执行以下步骤：

1. 获取最新的AEM as a Cloud Service SDK。
1. 解压缩AEM .jar，以便创建`crx-quickstart`文件夹。 运行以下命令：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 创建`crx-quickstart/install`文件夹。
1. 将CIF加载项的正确Sling功能存档文件复制到`crx-quickstart/install`文件夹中。

   * CIF加载项zip文件包含两个Sling功能存档`.far`文件。
   * 请确保为AEM创作或AEM发布使用正确的编辑器，具体取决于您计划如何运行本地AEM as a Cloud Service SDK。

1. 创建一个名为`COMMERCE_ENDPOINT`的本地OS环境变量，该变量包含Adobe Commerce GraphQL端点。

   * AEM使用此变量连接到您的商务系统。 CIF加载项包括一个本地反向代理，用于使Commerce GraphQL端点可在本地使用。 此代理由CIF创作工具（产品控制台和选取器）和用于执行直接GraphQL调用的CIF客户端组件使用。

   * 此外，还必须为AEM as a Cloud Service环境设置此变量。 有关变量的详细信息，请参阅[为AEM as a Cloud Service配置OSGi。](/help/implementing/deploying/configuring-osgi.md#local-development)

   * macOS下的示例：

     ```bash
     export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

   * Windows下的示例：

     ```bash
     set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

1. （可选）要启用暂存目录功能，必须为Adobe Commerce实例创建集成令牌。 按照[快速入门](/help/commerce-cloud/cif-storefront/getting-started.md#staging)中的步骤创建令牌。

   * 将名为`COMMERCE_AUTH_HEADER`的OSGi密钥设置为以下值：

     ```xml
     Authorization: Bearer <Access Token>
     ```

   * 有关密钥的详细信息，请参阅[为AEM as a Cloud Service配置OSGi。](/help/implementing/deploying/configuring-osgi.md#local-development)

1. 启动AEM as a Cloud Service SDK。

>[!NOTE]
>
>确保在步骤5中设置的同一终端窗口中启动AEM as a Cloud Service SDK 。 如果在单独的终端窗口中或通过双击.jar文件启动它，请确保环境变量可见。

通过OSGi控制台验证设置： `http://localhost:4502/system/console/osgi-installer`。 该列表应包含与功能模型文件中定义的CIF附加组件相关包、内容包和OSGi配置。

## 项目设置 {#project}

可通过两种方式为AEM as a Cloud ServiceBootstrapCIF项目。

### 使用AEM项目原型 {#project-archetype}

[AEM项目原型](https://github.com/adobe/aem-project-archetype)是Bootstrap预配置项目以开始使用CIF的主要工具。 CIF核心组件和所有必需的配置都可以通过一个附加选项包含在生成的项目中。

>[!TIP]
>
>始终使用最新版本的[AEM项目原型](https://github.com/adobe/aem-project-archetype/releases)，以便生成项目。

有关如何生成AEM项目，请参阅AEM项目原型[使用说明](https://github.com/adobe/aem-project-archetype#usage)。 要将CIF包含在项目中，请使用`includeCommerce`选项。

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

CIF核心组件可以通过包括提供的`all`包或者单独使用CIF内容包和相关OSGi捆绑包在任何项目中使用。 要手动将CIF核心组件添加到项目，请使用以下依赖项：

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

### 使用AEM Venia Reference Store {#venia-reference}

启动CIF项目的第二个选项是克隆并使用[AEM Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia参考存储区是一个示例参考存储区应用程序，用于演示如何将CIF核心组件用于AEM。 它旨在作为一组最佳实践示例以及开发您自己的功能的潜在起点。

要开始使用Venia引用存储，请克隆Git存储库并开始根据您的需求自定义项目。

>[!NOTE]
>
>Venia Reference Store项目包含AEM as a Cloud Service和AEM 6.5的两个生成配置文件。查看[project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)，以便了解它们的使用方式。

## 其他资源 {#additional-resources}

* [AEM项目原型](https://github.com/adobe/aem-project-archetype)
* [AEM Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
* [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
