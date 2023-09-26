---
title: 提交 AEM 连接器
description: 了解如何在Adobe Experience Manager (AEM)as a Cloud Service正确引用和部署连接器。
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 30%

---

# 提交 AEM 连接器

下面提供了有关提交Adobe Experience Manager (AEM)连接器的有用信息，应阅读其中关于 [实施](implement.md) 和  [维护](maintain.md) 连接器。

[Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html) 上列出了 AEM 连接器。

在以前的 AEM 解决方案中，[包管理器](/help/implementing/developing/tools/package-manager.md)用于在各种 AEM 实例上安装连接器。但是，对于 AEM as a Cloud Service，连接器是在 Cloud Manager 中的 CI/CD 流程中部署的。对于要部署的连接器，必须在maven项目的pom.xml中引用连接器。

对于如何将包包含在项目中，有多种选择：

1. 合作伙伴的公共存储库 – 合作伙伴将在可公开访问的 maven 存储库中托管内容包
1. 合作伙伴的受密码保护的存储库 — 合作伙伴将在受密码保护的maven存储库中托管内容包。 请参阅 [受密码保护的maven存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=en#password-protected-maven-repositories) 以获取说明。
1. 捆绑式构件 – 在这种情况下，连接器包将本地包含在客户的 maven 项目中。

无论包的托管位置如何，都必须在pom.xml中将包作为依赖项引用，如供应商提供的那样。

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

如果ISV合作伙伴在接入Internet（例如可访问的Cloud Manager）的maven存储库上托管连接器，则ISV应提供存储库配置，其中 `pom.xml` 可以放置。 这是因为，连接器依赖项（上述）可以在构建时通过Cloud Manager在本地解析。

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

如果ISV合作伙伴选择将连接器作为可下载文件分发，则ISV应提供说明。 此说明应介绍如何将文件部署到本地文件系统maven存储库，您必须将该存储库作为AEM项目的一部分签入Git。 这可确保Cloud Manager能够解析这些依赖项。
