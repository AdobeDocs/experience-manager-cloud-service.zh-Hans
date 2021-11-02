---
title: 提交 AEM 连接器
description: 提交 AEM 连接器
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: cf3273af030a8352044dcf4f88539121249b73e7
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 11%

---

提交 AEM 连接器
===========================

下面提供了有关提交 AEM 连接器的有用信息，应结合有关[实施](implement.md)和[维护](maintain.md)连接器的文章阅读这些信息。

AEM连接器列在 [Adobe交换](https://partners.adobe.com/exchangeprogram/experiencecloud).

在以前的AEM解决方案中， [包管理器](/help/implementing/developing/tools/package-manager.md) 用于在各种AEM实例上安装连接器。 但是，使用AEMas a Cloud Service，在Cloud Manager的CI/CD过程中会部署连接器。 要部署连接器，需要在Maven项目的pom.xml中引用连接器。

有关如何在项目中包含包，有多种选项可供选择：

1. 合作伙伴的公共存储库 — 合作伙伴将将内容包托管在可公开访问的Maven存储库中
1. 合作伙伴的受密码保护的存储库 — 合作伙伴将将内容包托管在受密码保护的Maven存储库中。 请参阅 [受密码保护的maven存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=en#password-protected-maven-repositories) 中。
1. 捆绑的对象 — 在这种情况下，连接器包包含在客户的maven项目的本地中。

无论包托管在何处，都需要按照供应商提供的方式在pom.xml中作为依赖项引用包。

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

如果ISV合作伙伴将连接器托管在可访问Internet（例如可访问Cloud Manager的）Maven存储库上，则ISV应提供可放置pom.xml的存储库配置，以便在构建时（本地和Cloud Manager）可以解决连接器依赖关系（上述）。

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

如果ISV合作伙伴选择将连接器作为可下载文件分发，则ISV应提供有关如何将文件部署到本地文件系统的Maven存储库的说明，该存储库需要作为AEM项目的一部分签入到Git中，以便Cloud Manager能够解决这些依赖关系。
