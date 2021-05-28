---
title: AEM as a Cloud Service SDK
description: AEM as a Software Development Kit概述
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---

# AEM as aCloud ServiceSDK {#aem-as-a-cloud-service-sdk}

AEM as a Cloud ServiceSDK由以下工件组成：

* **快速入门Jar**  — 用于本地开发的AEM运行时
* **Java API Jar**  - Java Jar/Maven依赖项，它公开了所有允许的Java API，这些API可用于针对AEM进行开发，并用作Cloud Service。以前称为Uberjar
* **Javadoc Jar**  - Java API Jar的javadoc
* **Dispatcher工具**  — 用于针对本地Dispatcher进行开发的一组工具。Unix和Windows的单独工件

此外，一些之前已与AEM 6.5或更早版本一起部署的客户将使用以下工件。 如果本地编译不适用于快速入门Jar，并且您怀疑是由于从作为Cloud Service部署的AEM中删除的接口所致，请联系客户支持团队以确定您是否需要访问。 这将需要在后端进行更改。

* **6.5已弃用的Java API Jar**  — 自AEM 6.5以来已删除的一组额外接口
* **6.5已弃用的Javadoc Jar**  — 额外的一组接口的Javaoc

## 构建SDK {#building-for-the-sdk}

AEM as a Cloud ServiceSDK用于构建和部署自定义代码。 有关更多详细信息，请参阅[AEM项目原型文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en)。 在高级别，将执行以下步骤：

* **编译代码**。如预期，将编译源代码，生成生成的内容包
* **生成工件**。在此过程中会生成工件
* **分析包**。使用Maven分析器插件分析包，该插件可查找Maven项目中的问题，如缺少依赖项
* **部署工件**。工件将部署到本地服务器。

部署到云环境时，Cloud Manager会执行相同的步骤。 在本地执行内部版本允许进行本地开发和测试，这样开发人员就可以在提交到源代码控制并触发Cloud Manager部署之前，很好地发现代码或结构问题，这可能需要较长的时间。

## 访问AEM as a Analytics SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* 您可以检查AEMAdmin Console的&#x200B;**关于Adobe Experience Manager**&#x200B;图标，以了解您在生产中运行的AEM的版本。
* 快速入门Jar和Dispatcher工具可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载为zip文件。 请注意，对SDK列表的访问权限仅限于将AEM Managed Services或AEM作为Cloud Service环境的用户。
* Java API Jar和Javadoc Jar可通过Maven工具（命令行或首选IDE）下载。
* Maven项目窗体应引用以下API Jar包。 还应在任何子包窗体中引用此依赖项。

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version>
  <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>SDK的版本条目应与AEM的版本作为Cloud Service匹配。 登录到AEM，然后转到屏幕右上角的问号并选择&#x200B;**[!UICONTROL 关于Adobe Experience Manager]**，可查看您使用的版本


## 使用新SDK版本{#refreshing-a-local-project-with-a-new-skd-version}刷新本地项目

何时建议使用新SDK刷新本地项目？

建议&#x200B;*至少在月度维护版本发布后刷新它。*

在任何每日维护版本发布后，要刷新它，*是可选的*。 客户的生产实例成功升级到新的AEM版本后，系统会通知客户。 对于每日维护版本，新SDK预计不会发生重大更改（如果根本不变）。 但是，仍建议有时使用最新的SDK刷新本地AEM开发人员环境，然后重新构建并测试自定义应用程序。 月度维护版本通常将包含更具影响力的更改，因此开发人员应当立即刷新、重建和测试。

以下是刷新本地环境的建议过程：

1. 确保任何有用内容已提交到源代码管理中的项目，或者可在可变内容包中使用，以供以后导入
1. 本地开发测试内容需要单独存储，以便不会将其部署为Cloud Manager管道构建的一部分。 这是因为它只需要用于本地开发
1. 停止当前正在运行的快速启动
1. 将`crx-quickstart`文件夹移到其他文件夹中以进行安全保留
1. 请注意Cloud Manager中介绍的新AEM版本（该版本将用于标识要进一步下载的新快速入门Jar版本）
1. 从软件分发门户下载版本与生产AEM版本匹配的快速入门JAR
1. 创建一个全新文件夹，并将新的快速入门Jar放入其中
1. 使用所需的运行模式启动新的快速启动（重命名文件或通过`-r`传入运行模式）。
   * 确保文件夹中没有旧快速启动的剩余内容。
1. 构建AEM应用程序
1. 通过PackageManager将您的AEM应用程序部署到本地AEM
1. 通过PackageManager安装本地环境测试所需的任何可变内容包
1. 根据需要继续开发和部署更改

如果每个新的AEM快速入门版本中都应安装相应的内容，请将其包含在内容包中以及项目的源代码控件中。 然后，每次安装它。

建议经常更新SDK（例如每两周更新一次），并每天处理完整的本地状态，以免意外依赖于应用程序中的状态数据。

如果您依赖CryptoSupport([通过在AEM中配置Cloudservices或SMTP邮件服务的凭据，或通过在应用程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/adobe/granite/crypto/CryptoSupport.html)中使用CryptoSupport API)，加密属性将由AEM环境首次启动时自动生成的密钥进行加密。 虽然cloudsetup负责自动重用特定于环境的CryptoKey，但有必要将该密钥注入到本地开发环境中。

默认情况下，AEM配置为将关键数据存储在文件夹的数据文件夹中，但为便于在开发中重复使用，可以在首次启动时使用“`-Dcom.adobe.granite.crypto.file.disable=true`”初始化AEM进程。 这将在“`/etc/key`”处生成加密数据。

要重复使用包含加密值的内容包，您需要执行以下步骤：

* 最初启动本地quickstart.jar时，请确保添加以下参数：&quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;。 建议始终添加该变量，但是这是可选的。
* 首次启动实例时，创建的包中包含根“`/etc/key`”的过滤器。 这将保留密钥，以便在您希望重复使用的所有环境中重复使用
* 导出任何包含机密的可变内容，或通过`/crx/de`查找加密值，以将其添加到将在安装期间重复使用的包中
* 每当您启动新实例时（要替换为新版本，或者当多个开发环境应共享凭据以进行测试时），请安装步骤2和3中生成的包，以便能够重复使用内容，而无需手动重新配置。 这是因为现在密钥保持同步。
