---
title: AEM as a Cloud Service SDK
description: AEM as a Cloud Service Software Development Kit概述
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 8ccf03ebcb4a96b66a15dc9a1161a857888278a7
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 1%

---

# AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEM as a Cloud Service SDK包含以下工件：

* **快速入门Jar** — 用于本地开发的AEM运行时
* **Java™ API Jar** - Java™ Jar/Maven依赖项，它公开可用于针对AEM as a Cloud Service开发的所有允许的Java™ API。 以前称为Uberjar
* **Javadoc Jar** - Java™ API Jar的Javadocs
* **Dispatcher Tools** — 用于针对本地Dispatcher开发的工具集。 为UNIX®和Windows分隔对象

此外，以前部署了AEM 6.5或更早版本的一些客户使用以下工件。 如果本地编译不能用于Quickstart jar，并且您怀疑它来自从AEM部署的as a Cloud Service中删除界面，请联系客户支持。 他们可以确定您是否需要访问权限。 它需要在后端进行更改。

* **6.5已弃用的Java™ API Jar** — 自AEM 6.5之后已移除的额外接口集
* **6.5已弃用的Javadoc Jar** — 用于附加接口集的Javadoc

>[!NOTE]
> 
> AEM as a Cloud Service和SDK在许多不同方面存在差异。 对于需要快速和反复更改的情况，Adobe引入了快速开发环境。 有关详细信息，请查看[快速开发环境](/help/implementing/developing/introduction/rapid-development-environments.md)。

## 适用于SDK的构建 {#building-for-the-sdk}

AEM as a Cloud Service SDK用于构建和部署自定义代码。 请参阅[AEM项目原型文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html)。 在高级别上，将执行以下步骤：

* **编译代码**。 如预期，将编译源代码，并生成生成的内容包
* **生成项目**。 在此过程中将生成工件
* **分析包**。 使用Maven分析器插件分析包，该插件会查找Maven项目中的问题，例如缺少依赖项
* **部署项目**。 工件将部署到本地服务器。

在部署到云环境时，Cloud Manager会执行相同的步骤。 在本地执行内部版本允许本地开发和测试。 开发人员可以在提交到源代码控制并触发Cloud Manager部署（可能需要更长时间）之前高效地发现代码或结构问题。

>[!NOTE]
>
>AEM as a Cloud Service SDK应使用[Cloud Manager的构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)支持的Java分发和版本进行构建。 由于AEM as a Cloud Service针对OracleJava技术(用于Adobe Experience Manager项目)的许可和支持条款，Adobe客户可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载OracleJDK并获得Java 11延长支持直至2026年9月。

## 访问AEM as a Cloud Service SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* 您可以检查AEMAdmin Console的&#x200B;**关于Adobe Experience Manager**&#x200B;图标，以了解您正在生产环境中运行的AEM版本。
* 可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)以zip文件的形式下载快速入门jar和Dispatcher工具。 仅限在AEM Managed Services或AEM as a Cloud Service上具有环境的人访问SDK列表。
* Java™ API Jar和Javadoc Jar可以通过maven工具（命令行或首选IDE）下载。
* maven项目pom应引用以下API Jar包。 还应该引用对任何子包pom的依赖关系。

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
>SDK的版本条目应与AEM as a Cloud Service的版本匹配。 您可以通过登录到AEM来查看您所使用的版本。 在屏幕的右上角，转到问号并选择&#x200B;**[!UICONTROL 关于Adobe Experience Manager]**。


## 使用新SDK版本刷新本地项目 {#refreshing-a-local-project-with-a-new-skd-version}

建议何时使用新的SDK刷新本地项目？

Adobe *建议*&#x200B;在每月维护版本发布后刷新它。

在任何每日维护版本发布后刷新它是&#x200B;*可选的*。 当客户的生产实例成功升级到新的AEM版本时，将通知客户。 对于每日维护版本，新的SDK可能不会发生重大变化（如果有的话）。 但是，建议偶尔使用最新的SDK刷新本地AEM开发人员环境，然后重建和测试自定义应用程序。 每月维护版本通常包括更具影响力的更改，因此开发人员应立即刷新、重建和测试。

以下是刷新本地环境的推荐过程：

1. 请确保任何有用的内容都提交到源代码管理中的项目，或者可以在可变内容包中用于以后导入。
1. 本地开发测试内容必须单独存储，以便不会部署为Cloud Manager管道构建的一部分。 原因是它仅用于本地开发。
1. 停止当前正在运行的快速启动。
1. 将`crx-quickstart`文件夹移动到其他文件夹以进行安全保留。
1. 请注意新的AEM版本，Cloud Manager中对其进行了说明（用于标识新的快速入门Jar版本，以便进一步下载）。
1. 从软件分发门户下载其版本与生产AEM版本相匹配的QuickStart JAR。
1. 创建一个全新的文件夹，并将新的QuickStart Jar放入其中。
1. 使用所需的运行模式启动新的QuickStart（重命名文件或通过`-r`在运行模式中传递）。
   * 确保文件夹中没有遗留的旧快速入门。
1. 构建AEM应用程序。
1. 通过包管理器将AEM应用程序部署到本地AEM。
1. 通过包管理器安装本地环境测试所需的任何可变内容包。
1. 根据需要继续开发和部署更改。

如果有应随每个新AEM快速入门版本一起安装的内容，请将其包含在内容包和项目的源代码控制中。 然后，每次都安装它。

建议频繁更新SDK（例如，每两周）并每天处理完整的本地状态以免意外依赖于应用程序中的有状态数据。

如果依赖于CryptoSupport ([通过在AEM中配置Cloud Services或SMTP Mail服务的凭据或在应用程序](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)中使用CryptoSupport API)，则加密的属性将通过密钥进行加密。 此密钥在AEM环境首次启动时自动生成。 虽然云设置负责自动重用特定于环境的CryptoKey，但必须将加密密钥注入本地开发环境。

默认情况下，AEM配置为将关键数据存储在一个文件夹的数据文件夹中，但为了便于在开发中重复使用，AEM进程可以在首次启动时使用“`-Dcom.adobe.granite.crypto.file.disable=true`”进行初始化。 此进程在“`/etc/key`”处生成加密数据。

要能够重用包含加密值的内容包，请执行以下步骤：

* 初次启动本地quickstart.jar时，请确保添加以下参数：“`-Dcom.adobe.granite.crypto.file.disable=true`”。 建议始终添加此标记（但可选择）。
* 首次启动实例时，请创建一个包，其中包含根“`/etc/key`”的筛选器。 此包包含要在您希望重复使用它们的所有环境中重复使用的密码。
* 导出任何包含密码的可变内容，或通过`/crx/de`查找加密值，以便将其添加到跨安装重复使用的包中。
* 每当启动新实例（要以新版本替换，或者多个开发环境应共享凭据进行测试）时，请安装步骤2和步骤3中生成的包。 这样，您就可以重复使用内容，而无需手动重新配置。 原因是现在加密密钥处于同步状态。
