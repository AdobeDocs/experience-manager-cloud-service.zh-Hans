---
title: AEM as a Cloud Service SDK
description: AEM作为Cloud Service软件开发工具包的概述
translation-type: tm+mt
source-git-commit: 0b46cc8ce4229138df84c70193cf9068e1200f0a
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---


# AEM作为Cloud ServiceSDK {#aem-as-a-cloud-service-sdk}

AEM作为Cloud ServiceSDK由以下对象组成：

* **快速启动Jar**  —— 用于本地开发的AEM运行时
* **Java API Jar** - Java Jar/Maven依赖关系，它显示所有允许的Java API，这些API可用于针对AEM作为Cloud Service进行开发。以前称为Uberjar
* **Javadoc Jar**  - Java API Jar的javadoc
* **Dispatcher Tools**  —— 用于针对本地Dispatcher进行开发的工具集。针对unix和windows的单独对象

此外，一些以前使用AEM 6.5或更早版本部署的客户将使用以下对象。 如果本地编译不能与快速启动jar一起使用，并且您怀疑是由于从作为Cloud Service部署的AEM中删除的接口，请联系客户支持以确定您是否需要访问。 这将需要在后端进行更改。

* **6.5已弃用的Java**  API Jar-自AEM 6.5以来已删除的另一组接口
* **6.5已弃用的Javadoc**  Jar —— 附加接口集的Javadoc

## 为SDK {#building-for-the-sdk}构建

AEM作为Cloud ServiceSDK用于构建和部署自定义代码。 有关更多详细信息，请参阅[AEM Project Archetype文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en)。 在高级别上，将执行以下步骤：

* **编译代码**。如预期，将编译源代码，生成生成内容包
* **生成伪像**。在此过程中会生成工件
* **分析捆绑**。使用Maven Analyzer插件分析捆绑包，它查找Maven项目中的问题，如缺少依赖项
* **部署对象**。对象将部署到本地服务器。

部署到云环境时，Cloud Manager会执行相同的步骤。 在本地执行构建允许进行本地开发和测试，这样开发人员可以在承诺进行源代码控制和触发Cloud Manager部署之前，很早就高效地发现代码或结构问题，这可能需要更长的时间。

## 将AEM作为Cloud ServiceSDK {#accessing-the-aem-as-a-cloud-service-sdk}访问

* 您可以检查AEMAdmin Console的&#x200B;**关于Adobe Experience Manager**&#x200B;图标，以找出在生产上运行的AEM的版本。
* 快速启动jar和调度程序工具可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载为zip文件。 请注意，访问SDK列表仅限于AEMManaged Services或AEM作为Cloud Service环境的。
* Java API Jar和Javadoc Jar可通过各种工具（命令行或首选IDE）进行下载。
* 主项目窗体应引用以下API Jar包。 此依赖关系也应在任何子包表单中引用。

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
>SDK的版本条目应与AEM的版本匹配，作为Cloud Service。 登录AEM，然后转到屏幕右上角的问号并选择&#x200B;**[!UICONTROL 关于Adobe Experience Manager]**，即可查看您使用的版本


## 使用新SDK版本{#refreshing-a-local-project-with-a-new-skd-version}刷新本地项目

建议何时使用新SDK刷新本地项目？

建议&#x200B;*至少在月度维护版本发布后刷新它。*

在任何日常维护版本发布后，都&#x200B;*可选*&#x200B;进行刷新。 客户的生产实例成功升级到新的AEM版本后，将获得通知。 对于日常维护版本，新SDK预计不会发生重大变化（如果有）。 但是，建议偶尔使用最新的SDK刷新本地AEM开发人员环境，然后重新构建并测试自定义应用程序。 月度维护版本通常包含更多影响力较大的更改，因此开发人员应立即刷新、重建和测试。

以下是刷新本地环境的建议过程：

1. 确保任何有用的内容已提交到源代码控件中的项目，或者在可变内容包中可用，以供以后导入
1. 本地开发测试内容需要单独存储，以便不将其部署为Cloud Manager管道构建的一部分。 因为它只需用于本地开发
1. 停止当前正在运行的快速启动
1. 将`crx-quickstart`文件夹移至其他文件夹以保持安全
1. 请注意云管理器中注明的新AEM版本（此版本将用于标识要进一步下载的新快速入门Jar版本）
1. 从软件分发门户下载其版本与生产AEM版本匹配的QuickStart JAR
1. 创建全新文件夹并放入新的快速入门Jar
1. 将新的QuickStart与所需的运行模式开始（重命名文件或通过`-r`在运行模式中传递）。
   * 确保文件夹中没有旧快速启动项的剩余部分。
1. 构建AEM应用程序
1. 通过PackageManager将AEM应用程序部署到本地AEM
1. 通过PackageManager安装本地环境测试所需的任何可变内容包
1. 根据需要继续开发和部署更改

如果每个新AEM quickstart版本都应安装内容，请将其包含在内容包中，并包含在项目的源控件中。 然后，每次安装。

建议经常更新SDK（例如每两周更新一次），并每天处理完整的本地状态，以避免意外依赖应用程序中的状态数据。

如果依赖CryptoSupport([通过在AEM中配置Cloudservices或SMTP邮件服务的凭据，或通过在应用程序](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)中使用CryptoSupport API)，加密的属性将由在AEM环境的第一个开始上自动生成的密钥进行加密。 虽然cloudsetup负责自动重用环境特定的CryptoKey，但是必须将加密密钥注入本地开发环境。

默认情况下，AEM配置为在文件夹的数据文件夹中存储关键数据，但为了便于在开发中重用，AEM进程可在首次启动时使用“`-Dcom.adobe.granite.crypto.file.disable=true`”进行初始化。 这将在“`/etc/key`”处生成加密数据。

要能够重用包含已加密值的内容包，您需要执行以下步骤：

* 最初开始本地quickstart.jar时，请确保添加以下参数：&quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;。 建议始终添加它（但是可选）。
* 第一次启动实例时，会创建一个包，其中包含根“`/etc/key`”的过滤器。 这将保留机密，以便在您希望重复使用的所有环境中重复使用
* 导出任何包含机密的可变内容，或通过`/crx/de`查找加密值，将其添加到将在安装过程中重复使用的包中
* 只要您启动新实例(要替换为新版本，或者多个开发环境应共享用于测试的凭据)，请安装步骤2和3中生成的包，以便无需手动重新配置即可重用内容。 这是因为现在密码键处于同步状态。
