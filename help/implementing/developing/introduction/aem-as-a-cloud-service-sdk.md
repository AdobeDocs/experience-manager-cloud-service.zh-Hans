---
title: AEM作为云服务SDK
description: '待完成 '
translation-type: tm+mt
source-git-commit: a7dc007230632bf8343004794b2bc4c5baaf4e05

---


# AEM作为云服务SDK {#aem-as-a-cloud-service-sdk}

AEM作为云服务SDK由以下对象组成：

* **快速入门Jar** —— 用于本地开发的AEM运行时
* **Java API Jar** - Java Jar/Maven依赖关系，它显示所有允许的Java API，这些API可用作云服务针对AEM进行开发。 以前称为Uberjar
* **Javadoc Jar** - Java API Jar的javadoc
* **Dispatcher Tools** —— 用于针对本地Dispatcher进行开发的工具集。 针对UNIX和Windows的单独对象

此外，某些先前已与AEM 6.5或更早版本一起部署的客户将使用以下对象。 如果本地编译不能与Quickstartjar一起使用，并且您怀疑是由于从作为云服务部署的AEM中删除的接口造成的，请联系客户支持以确定您是否需要访问。 这需要在后端进行更改。

* **6.5已弃用的Java API Jar** —— 自AEM 6.5以来已删除的另一组接口
* **6.5已弃用的Javadoc Jar** —— 用于附加的一组已接口的Javadoc

## 以云服务SDK形式访问AEM {#accessing-the-aem-as-a-cloud-service-sdk}

* 您可以检查AEM Admin Console的“关于 **Adobe Experience Manager** ”图标，以了解您正在生产中运行的AEM版本。
* 快速启动jar和调度程序工具可从软件分发门户下载为 [zip文件](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)。 请注意，对SDK列表的访问权限仅限于将AEM Managed services或AEM作为云服务环境的用户。
* Java API jar和Javadoc Jar可以通过各种工具（命令行或首选IDE）进行下载。
* 主项目窗格应引用以下API Jar包。 此依赖关系也应在任何子包中引用。

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version> 
  <scope>provided</scope>
</dependency>
```

> [!NOTE] SDK的版本条目应与AEM作为云服务的版本匹配。 登录AEM后，转到屏幕右上角的问号，然后选择“关于Adobe Experience Manager”，即可查看您使用的 **[!UICONTROL 版本。]**

* 托管包的主存储库的远程坐标应包含在pom文件中。

```
<repository>
    <id>adobe-aem-releases</id>
    <name>Adobe AEM Repository</name>
    <url>https://downloads.experiencecloud.adobe.com/content/maven/public</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

## 使用新的SDK版本刷新本地项目 {#refreshing-a-local-prokect-with-a-new-skd-version}

何时建议使用新SDK刷新本地项目？

建议至 *少在月度维护版* 本发布后对其进行刷新。

在任何日 *常维护版本发布* 后，都可以对其进行刷新。 客户的生产实例成功升级到新AEM版本后，将通知他们。 对于日常维护版本，新SDK预计不会发生重大更改（如果有）。 但是，建议偶尔使用最新的SDK刷新本地AEM开发人员环境，然后重新构建并测试自定义应用程序。 月度维护版本通常包含更多有影响的更改，因此开发人员应立即刷新、重建和测试。

下面是刷新本地环境的建议过程：

1. 确保任何有用的内容已提交到源控件中的项目，或在可变内容包中提供以供以后导入
1. 本地开发测试内容需要单独存储，以便不作为Cloud manager管道构建的一部分进行部署。 因为只要用于地方开发
1. 停止当前正在运行的快速启动
1. 将文件夹移 `crx-quickstart` 至其他文件夹以保持安全
1. 请注意Cloud manager中介绍的新AEM版本（此版本将用于标识要进一步下载的新QuickStart Jar版本）
1. 从软件分发门户下载其版本与生产AEM版本匹配的QuickStart JAR
1. 创建全新文件夹并放入新的QuickStart Jar
1. 使用所需的运行模式（重命名文件或通过在运行模式中传递）启动新的快速 `-r`启动。
   * 确保文件夹中没有旧快速入门的其余部分。
1. 构建AEM应用程序
1. 通过PackageManager将AEM应用程序部署到本地AEM
1. 通过PackageManager安装本地环境测试所需的任何可变内容包
1. 继续开发并根据需要部署更改

如果每个新AEM快速入门版本都应安装内容，请将其包含在内容包中，并包含在项目的源控件中。 然后，每次安装。

建议经常更新SDK（例如，每周两次），并每天处理完整的本地状态，以免意外依赖于应用程序中的状态数据。

如果您依赖CryptoSupport(通过[在AEM中配置Cloudservices的凭据或SMTP邮件服务，或通过在应用程序中使用CryptoSupport API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html))，加密的属性将由在AEM环境的第一次启动时自动生成的密钥进行加密。 虽然云设置负责自动重用特定于环境的CryptoKey，但是必须将密钥注入到本地开发环境中。

默认情况下，AEM配置为将关键数据存储在文件夹的数据文件夹中，但为了便于在开发中重用，AEM进程可在首次启动时使用“`-Dcom.adobe.granite.crypto.file.disable=true`”初始化。 这将在“”处生成加密数`/etc/key`据。

要能够重复使用包含加密值的内容包，您需要执行以下步骤：

* 最初启动本地quickstart.jar时，请确保添加以下参数：“`-Dcom.adobe.granite.crypto.file.disable=true`”。 建议始终添加它（但是可选）。
* 第一次启动实例时，会创建一个包，其中包含根“”的过滤`/etc/key`器。 这将保留机密，以便在您希望重复使用它们的所有环境中重复使用
* 导出包含机密的任何可变内容，或通过查找加密值，将 `/crx/de` 其添加到将在安装过程中重用的包中
* 每当您启动新实例（要替换为新版本或多个开发环境应共享用于测试的凭据）时，请安装在步骤2和3中生成的包，以便无需手动重新配置即可重复使用内容。 这是因为，现在密钥保持同步。