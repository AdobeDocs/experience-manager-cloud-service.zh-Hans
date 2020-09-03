---
title: 提交 AEM 连接器
description: 提交 AEM 连接器
translation-type: tm+mt
source-git-commit: d4e376ab30bb3e1fb533ed32f6ac43580775787c
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 11%

---


提交 AEM 连接器
===========================

下面提供了有关提交 AEM 连接器的有用信息，应结合有关[实施](implement.md)和[维护](maintain.md)连接器的文章阅读这些信息。

AEM连接器列在 [AdobeExchange](https://partners.adobe.com/exchangeprogram/experiencecloud)。

在以前的AEM解决方案中，包管理器用于在各种AEM实例上安装连接器。 但是，在AEM为Cloud Service的情况下，在云管理器的CI/CD过程中部署连接器。 为了部署连接器，需要在主项目的pom.xml中引用连接器。

项目中如何包含包有多种选项：

1. 合作伙伴的公共存储库——合作伙伴将将内容包托管在一个可公开访问的主存储库中
1. 合作伙伴的受密码保护的存储库——合作伙伴将将内容包托管在受密码保护的主存储库中。 有关说 [明，请参阅](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories) ()的受密码保护的主资料库。
1. 捆绑的伪像——在本例中，连接器包包含在客户的主项目中本地。

无论包的托管位置如何，都需要像供应商提供的一样，在pom.xml中作为依赖项引用包。

```xml
<!-- UberJAR Dependency to be added to the project's Reactor pom.xml -->
<dependency>
  <groupId>com.partnername</groupId>
  <artifactId>my-artifact</artifactId>
  <version>V123</version> <!-- use the latest! -->
  <scope>provided</scope>
  <classifier>my_classifier</classifier>
</dependency>
```

如果ISV合作伙伴将连接器托管在可访问Internet（如可访问Cloud Manager的）主要存储库上，则ISV应提供可放置pom.xml的存储库配置，以便在构建时（本地和云管理器）解析连接器依赖关系（上述）。

```xml
<repository>
    <id>the-repository</id>
    <name>The Repository Where the Connector is Hosted</name>
    <url>https://repo.partnername.com/repositories/aem_connector_repo</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

如果ISV合作伙伴选择将连接器作为可下载文件进行分发，则ISV应提供有关如何将这些文件部署到本地文件系统主存储库的说明，这些存储库需要作为AEM项目的一部分签入到Git中，以便Cloud Manager能够解析这些依赖关系。
