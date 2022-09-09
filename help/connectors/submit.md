---
title: 提交 AEM 连接器
description: 提交 AEM 连接器
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: cf3273af030a8352044dcf4f88539121249b73e7
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 100%

---

提交 AEM 连接器
===========================

下面提供了有关提交 AEM 连接器的有用信息，应结合有关[实施](implement.md)和[维护](maintain.md)连接器的文章阅读这些信息。

[Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud) 上列出了 AEM 连接器。

在以前的 AEM 解决方案中，[包管理器](/help/implementing/developing/tools/package-manager.md)用于在各种 AEM 实例上安装连接器。但是，对于 AEM as a Cloud Service，连接器是在 Cloud Manager 中的 CI/CD 流程中部署的。要部署连接器，需要在 maven 项目的 pom.xml 中引用连接器。

对于如何将包包含在项目中，有多种选择：

1. 合作伙伴的公共存储库 – 合作伙伴将在可公开访问的 maven 存储库中托管内容包
1. 合作伙伴的受密码保护的存储库 – 合作伙伴将在受密码保护的 maven 存储库中托管内容包。有关说明，请参阅[受密码保护的 maven 存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=zh-Hans#password-protected-maven-repositories)。
1. 捆绑式构件 – 在这种情况下，连接器包将本地包含在客户的 maven 项目中。

无论包的托管位置如何，都需要在 pom.xml 中将包作为依赖项引用，如供应商提供的那样。

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

如果 ISV 合作伙伴在接入 Internet（例如可访问的 Cloud Manager）的 maven 存储库上托管连接器，则 ISV 应提供可放置 pom.xml 的存储库配置，以便能够在构建时（本地和通过 Cloud Manager）解析连接器依赖项（上文）。

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

如果 ISV 合作伙伴选择将连接器作为可下载文件分发，则 ISV 应提供有关如何将文件部署到本地文件系统 maven 存储库的说明，需将该存储库作为 AEM 项目的一部分签入 Git，以便 Cloud Manager 能够解析这些依赖项。
