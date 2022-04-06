---
title: UI 测试
description: 自定义UI测试是一项可选功能，通过该功能，您可以为自定义应用程序创建并自动运行UI测试
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 05f9e9de0d5dbcc332466dc964e2d01569d16110
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 1%

---


# UI 测试 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI 测试"
>abstract="自定义UI测试是一项可选功能，允许您为应用程序创建并自动运行UI测试。 UI测试是在Docker图像中打包的基于硒的测试，以便允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛选择。"

自定义UI测试是一项可选功能，允许您为应用程序创建并自动运行UI测试。

## 概述 {#custom-ui-testing}

AEM提供了 [Cloud Manager质量门](/help/implementing/cloud-manager/custom-code-quality-rules.md) 以确保对自定义应用程序进行顺利更新。 特别是，IT测试已开始使用AEM API创建和自动化自定义测试。

UI测试是在Docker图像中打包的基于硒的测试，以便允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛选择。 此外，使用 [AEM项目原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

UI测试将作为每个Cloud Manager管道(具有 [专用 **自定义UI测试** 中。](/help/implementing/cloud-manager/deploy-code.md) 任何UI测试（包括回归和新功能）都允许检测和报告错误。

与使用Java编写的HTTP测试（自定义功能测试）不同，UI测试可以是使用任何语言编写的测试的Docker图像，前提是这些测试遵循部分中定义的惯例 [构建UI测试。](#building-ui-tests)

>[!TIP]
>
>Adobe建议遵循 [AEM项目原型。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### 客户选择加入 {#customer-opt-in}

要使Cloud Manager能够构建和执行您的UI测试，您必须通过向存储库添加文件来选择加入此功能。

* 文件名必须为 `testing.properties`.
* 文件内容必须为 `ui-tests.version=1`.
* 文件必须位于maven子模块下方，以便UI测试位于 `pom.xml` 文件来测试子模块。
* 文件必须位于已构建的的根 `tar.gz` 文件。

如果不存在此文件，则将跳过UI测试生成和执行。

包含 `testing.properties` 文件，添加 `include` 语句 `assembly-ui-test-docker-context.xml` 文件。

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>如果您的项目不包含此行，您将需要编辑文件以选择启用UI测试。
>
>文件可能包含一行建议不编辑该文件。 这是因为在引入选择加入UI测试之前，已将其引入项目，并且客户端的不打算编辑文件。 这可以安全地忽略。

## 构建UI测试 {#building-ui-tests}

Maven项目会生成Docker生成上下文。 此Docker构建上下文介绍如何创建包含UI测试的Docker图像，Cloud Manager用户将该图像生成包含实际UI测试的Docker图像。

本节介绍将UI测试项目添加到存储库所需的步骤。

>[!TIP]
>
>的 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 可以为您生成没有编程语言特殊要求的UI测试项目。

### 生成Docker生成上下文 {#generate-docker-build-context}

要生成Docker生成上下文，您需要Maven模块：

* 生成包含 `Dockerfile` 以及通过测试构建Docker映像所需的其他文件。
* 使用标记存档 `ui-test-docker-context` 分类器。

执行此操作的最简单方法是配置 [Maven Assembly插件](http://maven.apache.org/plugins/maven-assembly-plugin/) 创建Docker构建上下文存档并为其分配正确的分类器。

您可以使用不同的技术和框架构建UI测试，但此部分假定您的项目布局方式与以下类似。

```text
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

的 `pom.xml` 文件会处理Maven内部版本。 向Maven Assembly插件添加执行，如下所示。

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
        <descriptors>
            <descriptor>${project.basedir}/assembly-ui-test-docker-context.xml</descriptor>
        </descriptors>
        <tarLongFileMode>gnu</tarLongFileMode>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

此执行会指示Maven Assembly插件根据 `assembly-ui-test-docker-context.xml`，称为 **装配描述符** 插件的术语。 程序集描述符列出了必须包含在存档中的所有文件。

```xml
<assembly>
    <id>ui-test-docker-context</id>
    <includeBaseDirectory>false</includeBaseDirectory>
    <formats>
        <format>tar.gz</format>
    </formats>
    <fileSets>
        <fileSet>
            <directory>${basedir}</directory>
            <includes>
                <include>Dockerfile</include>
                <include>wait-for-grid.sh</include>
            </includes>
        </fileSet>
        <fileSet>
            <directory>${basedir}/test-module</directory>
            <excludes>
                <exclude>node/**</exclude>
                <exclude>node_modules/**</exclude>
                <exclude>reports/**</exclude>
            </excludes>
        </fileSet>
    </fileSets>
</assembly>
```

程序集描述符指示插件创建类型的存档 `.tar.gz` 并分配 `ui-test-docker-context` 分类器。 此外，它还列出了必须包含在存档中的文件，包括以下内容。

* A `Dockerfile`，用于生成Docker图像的必需参数
* 的 `wait-for-grid.sh` 脚本，其目的如下所述
* 实际的UI测试，由 `test-module` 文件夹

程序集描述符还会排除在本地运行UI测试时可能生成的某些文件。 这样可保证存档更小，生成速度更快。

Cloud Manager会自动提取包含Docker构建上下文的存档，Cloud Manager将在其部署管道期间构建包含测试的Docker图像。 最终，Cloud Manager将运行Docker图像，以针对您的应用程序执行UI测试。

内部版本应生成零个或一个存档。 如果生成零存档，则测试步骤默认会通过。 如果内部版本生成多个存档，则选择哪个存档是不确定的。

## 编写UI测试 {#writing-ui-tests}

本节介绍包含您的UI测试的Docker图像必须遵循的惯例。 Docker图像是基于上一节中所述的Docker构建上下文构建的。

### 环境变量 {#environment-variables}

在运行时，以下环境变量将传递到您的Docker映像。

| 变量 | 示例 | 描述 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium服务器的URL |
| `SELENIUM_BROWSER` | `chrome` | Selenium Server使用的浏览器实施 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM创作实例的URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 登录AEM创作实例的用户名 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登录AEM创作实例的密码 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM发布实例的URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 登录AEM发布实例的用户名 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登录AEM发布实例的密码 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 必须保存测试结果的XML报告的路径 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必须将文件上传到的URL，以便Selenium能够访问这些文件 |

### 等待硒准备好 {#waiting-for-selenium}

在测试开始之前， Docker映像负责确保Selenium服务器已启动并运行。 等待Selenium服务的过程分为两步。

1. 从 `SELENIUM_BASE_URL` 环境变量。
1. 以常规间隔轮询 [状态端点](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) 由Selenium API公开。

当Selenium的状态端点以正面响应回答时，测试即可开始。

### 生成测试报表 {#generate-test-reports}

Docker图像必须以JUnit XML格式生成测试报告，并将其保存在环境变量指定的路径中 `REPORTS_PATH`. JUnit XML格式是一种广泛用于报告测试结果的格式。 如果Docker图像使用Java和Maven，则标准测试模块如 [Maven Surefire插件](https://maven.apache.org/surefire/maven-surefire-plugin/) 和 [Maven Failsafe插件](https://maven.apache.org/surefire/maven-failsafe-plugin/) 可以开箱即用地生成此类报告。

如果Docker图像是使用其他编程语言或测试运行者实施的，请查看所选工具的文档以了解如何生成JUnit XML报告。

### 上传文件 {#upload-files}

测试有时必须将文件上传到正在测试的应用程序。 为了保持Selenium的部署相对于测试的灵活性，无法直接将资产上传到Selenium。 而上传文件需要执行以下步骤。

1. 在指定的URL上传文件 `UPLOAD_URL` 环境变量。
   * 必须在包含多部分表单的一个POST请求中执行上传。
   * 多部件表单必须具有单个文件字段。
   * 这等同于 `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * 请查阅Docker图像中使用的编程语言的文档和库，了解如何执行此类HTTP请求。
1. 如果上传成功，则请求会返回 `200 OK` 类型响应 `text/plain`.
   * 响应的内容是不透明的文件句柄。
   * 您可以使用此句柄来替代 `<input>` 元素来测试应用程序中的文件上传。
