---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: dbdc63db9a9ac954ce6359d3643231d6e195fd53
workflow-type: ht
source-wordcount: '302'
ht-degree: 100%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 15575 {#release-15575}

下面总结了维护版本 15575 的持续改进情况，该版本于 2024 年 3 月 19 日公开发布。上一个维护版本是版本 15262。

2024.3.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-15575}

无。

### 修复的问题 {#fixed-issues-15575}

* ASSETS-36358：无法渲染上传报告。
* GRANITE-50774：GraniteContent 应在初始化时使用属性值的确定性顺序。

### 已知问题 {#known-issues-15575}

无。

### 更改通知 {#change-notice-15575}

**必需执行的操作**

#### 将 CM Java 版本设置为 11 {#set-java-version-11}

新版本的 aem-sdk-api 包含使用 Java 11 目标编译的类，该目标与 Cloud Manager 生成环境默认 JDK 版本 1.8 不兼容。此更新要求使用 JDK 11 执行 Maven。

建议客户将 `.cloudmanager/java-version` 文件添加到其 git 存储库的根目录中，其中的内容为：`11`。请参阅[生成环境/设置 Maven JDK 版本](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version)。

#### 将 aem-cloud-testing-clients 更新到 1.2.1 {#update-aem-cloud-testing-clients}

即将发生的更改需要将您在自定义功能测试中使用的库 [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) 更新到至少 **1.2.1** 版本

确保您在 `it.tests/pom.xml` 中的依赖项已经升级。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

此更改需要在 2024 年 4 月 6 日之前执行。

如果未更新依赖项库，则会导致“自定义功能测试”步骤中的管道失败。

### 嵌套的技术 {#embedded-tech-15575}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
