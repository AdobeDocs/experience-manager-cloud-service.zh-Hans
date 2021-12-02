---
title: UI测试 — Cloud Services
description: UI测试 — Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 710f156e606902ab5548169661d4a82c8cf4f819
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 1%

---

# UI测试 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI测试"
>abstract="UI测试是在Docker图像中打包的基于硒的测试，以便允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛选择。 Docker图像可以使用标准工具创建，但在执行时必须遵守某些约定。 运行Docker映像时，将自动配置Selenium服务器。 下面描述的运行时约定允许您的测试代码同时访问Selenium服务器和受测AEM实例。"

UI测试是在Docker图像中打包的基于硒的测试，以便允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛选择。 Docker图像可以使用标准工具创建，但在执行时必须遵守某些约定。 运行Docker映像时，将自动配置Selenium服务器。 下面描述的运行时约定允许您的测试代码同时访问Selenium服务器和受测AEM实例。

>[!NOTE]
> 需要更新在2021年2月10日之前创建的暂存和生产管道，才能使用此页面中所述的UI测试。
> 请参阅 [Cloud Manager中的CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 有关管道配置的信息。

## 自定义UI测试 {#custom-ui-testing}

AEM为其客户提供了一套集成的Cloud Manager质量门户，以确保顺利更新其应用程序。 特别是，IT测试门已经允许客户创建使用AEM API的测试并自动执行这些测试。

自定义UI测试功能是 [可选功能](#customer-opt-in) 这样，我们的客户便能够为其应用程序创建并自动运行UI测试。 UI测试是在Docker图像中打包的基于硒的测试，以便允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛选择。 您可以从此处了解有关如何构建UI和编写UI测试的更多信息。 此外，使用AEM项目原型可以轻松生成UI测试项目。

客户可以为UI创建（通过GIT）自定义测试和测试包。 UI测试将作为每个Cloud Manager管道的特定质量门的一部分执行，并包含其特定步骤和反馈信息。 任何UI测试（包括回归和新功能）都允许在客户上下文中检测和报告错误。

客户UI测试在“自定义UI测试”步骤下的生产管道上自动运行。

与使用java编写的HTTP测试不同，UI测试可以是使用任何语言编写的测试的文档图像，前提是这些测试遵循 [构建UI测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests).

>[!NOTE]
>建议遵循结构和语言 *（js和wdio）* 在 [AEM项目原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) 作为起点。

### 客户选择加入 {#customer-opt-in}

要构建并执行其UI测试，客户需要通过以下方法来“选择加入”：在UI测试的Maven子模块下（UI测试子模块的pom.xml文件旁边），将文件添加到其代码存储库中，并确保此文件位于构建的根文件中 `tar.gz` 文件。

*文件名*: `testing.properties`

*内容*: `ui-tests.version=1`

如果不在内置中 `tar.gz` 文件中，将跳过生成和执行UI测试的过程

添加 `testing.properties` 文件，添加 `include` 语句 `assembly-ui-test-docker-context.xml` 文件（在UI中测试子模块）。

>[!NOTE]
>如果您的项目不包含该行，则您将需要编辑此文件以选择加入UI测试。 如果文件有一行建议不编辑，请忽略该建议。

    &quot;
    [...]
    &lt;includes>
    &lt;include>Dockerfile&lt;/include>
    &lt;include>wait-for-grid.sh&lt;/include>
    &lt;include>testing.properties&lt;/include> &lt;!>- Cloud Manager中的选择加入测试模块 — >
    &lt;/includes>
    [...]
    &quot;

>[!NOTE]
>需要更新在2021年2月10日之前创建的生产管道，才能使用本节中所述的UI测试。 这实质上意味着用户必须编辑生产管道并单击 **保存** ，即使未进行任何更改也是如此。
>请参阅 [配置CI-CD管线](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) 了解有关管道配置的更多信息。

## 构建UI测试 {#building-ui-tests}

UI测试是基于由Maven项目生成的Docker内部版本上下文构建的。 Cloud Manager使用Docker内部版本上下文生成包含实际UI测试的Docker图像。 总之，Maven项目会生成Docker生成上下文，而Docker生成上下文介绍如何创建包含UI测试的Docker图像。

本节将介绍将UI测试项目添加到存储库所需的步骤。 如果您匆忙或对编程语言没有特殊要求，请 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 可以为您生成UI测试项目。

### 生成Docker生成上下文 {#generate-docker-build-context}

要生成Docker生成上下文，您需要Maven模块：

- 生成包含 `Dockerfile` 以及通过测试构建Docker映像所需的其他文件。
- 使用标记存档 `ui-test-docker-context` 分类器。

实现此目的的最简单方法是配置 [Maven Assembly插件](http://maven.apache.org/plugins/maven-assembly-plugin/) 创建Docker构建上下文存档并为其分配正确的分类器。

您可以使用不同的技术和框架构建UI测试，但此部分假定您的项目布局方式与以下类似。

```
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

此执行会指示Maven Assembly插件根据 `assembly-ui-test-docker-context.xml`，在插件的行话中称为“程序集描述符”。 程序集描述符列出了必须包含在存档中的所有文件。

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

程序集描述符指示插件创建类型的存档 `.tar.gz` 并分配 `ui-test-docker-context` 分类器。 此外，它还列出了必须包含在存档中的文件：

- A `Dockerfile`，用于生成Docker图像。
- 的 `wait-for-grid.sh` 脚本，其目的如下所述。
- 实际的UI测试，由 `test-module` 文件夹。

程序集描述符还会排除在本地运行UI测试时可能生成的某些文件。 这样可保证存档更小，生成速度更快。

Cloud Manager会自动提取包含Docker构建上下文的存档，以便在其部署管道期间生成包含测试的Docker图像。 最终，Cloud Manager将运行Docker图像，以针对您的应用程序执行UI测试。

内部版本应生成零个或一个存档。 如果生成零存档，则测试步骤默认会通过。 如果内部版本生成多个存档，则选择哪个存档是不确定的。

## 编写UI测试 {#writing-ui-tests}

本节介绍包含您的UI测试的Docker图像必须遵循的惯例。 Docker图像是基于上一节中所述的Docker构建上下文构建的。

### 环境变量 {#environment-variables}

在运行时，以下环境变量将传递到您的Docker映像。

| 变量 | 示例 | 描述 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium服务器的URL |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | Selenium Server使用的浏览器实施 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM创作实例的URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 登录AEM创作实例的用户名 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登录AEM创作实例的密码 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM发布实例的URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 登录AEM发布实例的用户名 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登录AEM发布实例的密码 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 必须保存测试结果的XML报告的路径 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必须将文件上传到的URL，以便Selenium能够访问这些文件 |

### 等待硒准备就绪 {#waiting-for-selenium}

在测试开始之前， Docker映像负责确保Selenium服务器已启动并运行。 等待Selenium服务的过程分为两步：

1. 从 `SELENIUM_BASE_URL` 环境变量。
2. 以常规间隔轮询 [状态端点](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) 由Selenium API公开。

一旦Selenium的状态端点以正面响应进行回答，测试就可以最终开始。

### 生成测试报告 {#generate-test-reports}

Docker图像必须以JUnit XML格式生成测试报告，并将其保存在环境变量指定的路径中 `REPORTS_PATH`. JUnit XML格式是一种广泛用于报告测试结果的格式。 如果Docker图像使用Java和Maven，则 [Maven Surefire插件](https://maven.apache.org/surefire/maven-surefire-plugin/) 和 [Maven Failsafe插件](https://maven.apache.org/surefire/maven-failsafe-plugin/). 如果Docker图像是使用其他编程语言或测试运行者实施的，请查看所选工具的文档，以了解如何生成JUnit XML报告。

### 上传文件 {#upload-files}

测试有时必须将文件上传到正在测试的应用程序。 为了保持Selenium相对于测试的部署保持灵活，无法直接将资产上传到Selenium。 而上传文件将会完成一些中间步骤：

1. 在指定的URL上传文件 `UPLOAD_URL` 环境变量。 必须在包含多部分表单的一个POST请求中执行上传。 多部件表单必须具有单个文件字段。 这等同于 `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. 请查阅Docker图像中使用的编程语言的文档和库，了解如何执行此类HTTP请求。
2. 如果上传成功，则请求会返回 `200 OK` 类型响应 `text/plain`. 响应的内容是不透明的文件句柄。 您可以使用此句柄来替代 `<input>` 元素来测试应用程序中的文件上传。
