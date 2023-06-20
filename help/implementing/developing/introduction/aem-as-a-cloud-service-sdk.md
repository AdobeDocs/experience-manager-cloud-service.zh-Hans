---
title: AEM as a Cloud Service SDK
description: AEMas a Cloud Service软件开发工具包概述
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 1%

---

# AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEMas a Cloud ServiceSDK由以下工件组成：

* **快速入门Jar**  — 用于本地开发的AEM运行时
* **Java API Jar** - Java Jar/Maven依赖项，该依赖项公开所有允许的Java API，这些API可用于针对AEM as aCloud Service进行开发。 以前称为Uberjar
* **Javadoc Jar** - Java API Jar的Javadoc
* **Dispatcher工具**  — 用于针对本地Dispatcher开发的一组工具。 为unix和windows分隔对象

此外，以前使用AEM 6.5或更早版本部署的一些客户将使用以下工件。 如果本地编译不能使用快速入门jar，并且您怀疑这是由于接口已从AEM部署的as a Cloud Service中删除，请联系客户支持以确定您是否需要访问权限。 这将需要在后端进行更改。

* **6.5已弃用的Java API Jar**  — 自AEM 6.5之后已移除的另一组接口
* **6.5已弃用的Javadoc Jar**  — 用于其他接口集的Javadoc

## 针对SDK构建 {#building-for-the-sdk}

AEMas a Cloud ServiceSDK用于生成和部署自定义代码。 欲知更多详情，请参见 [AEM项目原型文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). 在高级别上，将执行以下步骤：

* **编译代码**. 如预期，将编译源代码，生成生成的内容包
* **生成工件**. 在此过程中会生成工件
* **分析包**. 使用Maven分析器插件分析包，该插件会查找Maven项目中的问题，例如缺少依赖项
* **部署工件**. 工件将部署到本地服务器。

Cloud Manager在部署到云环境时执行相同的步骤。 在本地执行生成允许本地开发和测试，因此开发人员可以有效地发现代码或结构问题，而无需提交源代码控制并触发Cloud Manager部署（这可能需要更长时间）。

## 访问AEMas a Cloud ServiceSDK {#accessing-the-aem-as-a-cloud-service-sdk}

* 您可以检查AEMAdmin Console **关于Adobe Experience Manager** 图标以了解您正在生产环境中运行的AEM的版本。
* 快速入门jar和Dispatcher工具可以作为zip文件从 [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). 请注意，对SDK列表的访问仅限于具有AEM Managed Services或AEMas a Cloud Service环境的用户。
* Java API Jar和Javadoc Jar可以通过maven工具（命令行或首选IDE）下载。
* Maven项目Pom应引用以下API Jar包。 此外，还应在任何子包pom中引用此依赖项。

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
>SDK的版本条目应与AEMas a Cloud Service的版本匹配。 您可以通过登录到AEM，然后转到屏幕右上角的问号并选择 **[!UICONTROL 关于Adobe Experience Manager]**


## 使用新SDK版本刷新本地项目 {#refreshing-a-local-project-with-a-new-skd-version}

建议何时使用新的SDK刷新本地项目？

它是 *推荐* ，以至少在每月维护版本发布后进行刷新。

它是 *可选* 以在发布任何日常维护版本后对其进行刷新。 当客户的生产实例成功升级到新的AEM版本时，会通知客户。 对于每日维护版本，新的SDK预计不会发生显着变化（如果有的话）。 但是，建议偶尔使用最新的SDK刷新本地AEM开发人员环境，然后重建和测试自定义应用程序。 每月维护版本通常包括更具影响力的更改，因此开发人员应立即刷新、重建和测试。

以下是刷新本地环境的推荐过程：

1. 确保任何有用的内容都提交到源代码管理中的项目，或者可以在可变内容包中用于以后导入
1. 本地开发测试内容需要单独存储，以便不会部署为Cloud Manager管道构建的一部分。 这是因为它只需要用于本地开发
1. 停止当前正在运行的快速启动
1. 移动 `crx-quickstart` 文件夹到其他文件夹以便安全保存
1. 请注意新的AEM版本，Cloud Manager中对其进行了说明（用于标识新的快速入门Jar版本，以便进一步下载）
1. 从软件分发门户下载其版本与生产AEM版本相匹配的QuickStart JAR
1. 创建一个全新的文件夹，并将新的QuickStart Jar放入
1. 使用所需的运行模式启动新的QuickStart（重命名文件或通过以运行模式传递） `-r`)。
   * 确保文件夹中没有剩余的旧快速入门。
1. 构建AEM应用程序
1. 通过PackageManager将AEM应用程序部署到本地AEM
1. 通过PackageManager安装本地环境测试所需的任何可变内容包
1. 根据需要继续开发和部署更改

如果有应随每个新AEM快速入门版本一起安装的内容，请将其包含在内容包和项目的源代码控制中。 然后，每次都安装它。

建议频繁更新SDK（例如每两周）并每天处理完整的本地状态，以免意外依赖于应用程序中的有状态数据。

如果您依赖CryptoSupport ([通过在AEM中配置Cloudservices或SMTP邮件服务的凭据，或在应用程序中使用CryptoSupport API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html))，加密的属性由在AEM环境首次启动时自动生成的密钥加密。 虽然cloudsetup可自动重用特定于环境的CryptoKey，但必须将加密密钥注入本地开发环境中。

默认情况下，AEMAEM配置为将关键数据存储在一个文件夹的数据文件夹中，但为了便于在开发中重复使用，可以在首次启动时使用&quot;`-Dcom.adobe.granite.crypto.file.disable=true`“。 这将在“ ”处生成加密数据`/etc/key`“。

要能够重用包含加密值的内容包，您需要执行以下步骤：

* 最初启动本地quickstart.jar时，请确保添加以下参数： ”`-Dcom.adobe.granite.crypto.file.disable=true`“。 建议始终添加此标记，但可根据需要进行添加。
* 第一次启动实例时，请创建包含根“ ”筛选器的包`/etc/key`“。 这将包含要在您希望重复使用它们的所有环境中重复使用的密码
* 导出任何包含密码的可变内容，或通过以下方式查找加密值 `/crx/de` 以将其添加到可跨安装重复使用的包中
* 每当您启动新实例（用新版本替换或者多个开发环境应共享凭据进行测试）时，请安装步骤2和3中生成的包，以便能够重用内容，而无需手动重新配置。 这是因为现在加密密钥处于同步状态。
