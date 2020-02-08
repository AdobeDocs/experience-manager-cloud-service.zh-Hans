---
title: 提交AEM Connector
description: 提交AEM Connector
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f

---


提交AEM Connector
===========================

下面提供了有关提交AEM连接器的有用信息，应结合有关实施和维护连接器 [的文章](implement.md)[阅读](maintain.md) 。

AEM Connectors列在 [Adobe exchange上](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace.html)。

在以前的AEM解决方案中，包管理器用于在各种AEM实例上安装连接器。 但是，在AEM作为云服务的情况下，在Cloud manager的CI/CD过程中会部署连接器。 为了部署连接器，需要在maven项目的pom.xml中引用连接器。

项目中如何包含包有多种选项：

1. 合作伙伴的公共存储库——合作伙伴将将内容包托管在一个可公开访问的主存储库中
1. 捆绑的伪像——在这种情况下，连接器包包含在客户的主项目中的本地。

无论包的托管位置如何，都需要像供应商提供的那样，在pom.xml中将包作为依赖关系进行引用。

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

如果ISV合作伙伴将连接器托管在可访问Internet（如可访问Cloud manager的）主要存储库上，则ISV应提供可放置pom.xml的存储库配置，以便在构建时（本地和Cloud Manager）解决连接器依赖关系（上述）。

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

如果ISV合作伙伴选择将连接器作为可下载文件分发，则ISV应提供有关如何将文件部署到本地文件系统主存储库的说明，这些存储库需要作为AEM项目的一部分签入Git，以便Cloud manager能够解析这些依赖关系。
