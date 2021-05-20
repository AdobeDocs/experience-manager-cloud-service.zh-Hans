---
title: UI测试 — Cloud Services
description: UI测试 — Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# UI测试{#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI测试"
>abstract="UI测试是在Docker图像中打包的基于硒的测试，以便允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛选择。 Docker图像可以使用标准工具创建，但在执行时必须遵守某些约定。 运行Docker映像时，将自动配置Selenium服务器。 下面描述的运行时约定允许您的测试代码同时访问Selenium服务器和受测AEM实例。"

UI测试是在Docker图像中打包的基于硒的测试，以便允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛选择。 Docker图像可以使用标准工具创建，但在执行时必须遵守某些约定。 运行Docker映像时，将自动配置Selenium服务器。 下面描述的运行时约定允许您的测试代码同时访问Selenium服务器和受测AEM实例。

>[!NOTE]
> 需要更新在2021年2月10日之前创建的暂存和生产管道，才能使用此页面中所述的UI测试。
> 有关管道配置的信息，请参阅[配置CI-CD管道](/help/implementing/cloud-manager/configure-pipeline.md)。

## 构建UI测试{#building-ui-tests}

UI测试是基于由Maven项目生成的Docker内部版本上下文构建的。 Cloud Manager使用Docker内部版本上下文生成包含实际UI测试的Docker图像。 总之，Maven项目会生成Docker生成上下文，而Docker生成上下文介绍如何创建包含UI测试的Docker图像。

本节将介绍将UI测试项目添加到存储库所需的步骤。 如果您匆忙或对编程语言没有特殊要求，[AEM项目原型](https://github.com/adobe/aem-project-archetype)可以为您生成UI测试项目。

### 生成Docker生成上下文{#generate-docker-build-context}

要生成Docker生成上下文，您需要Maven模块：

- 生成一个存档文件，其中包含`Dockerfile`和通过测试构建Docker映像所需的所有其他文件。
- 使用`ui-test-docker-context`分类器标记存档。

实现此目的的最简单方法是配置[Maven Assembly Plugin](http://maven.apache.org/plugins/maven-assembly-plugin/)以创建Docker构建上下文存档并为其分配正确的分类器。

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

`pom.xml`文件负责Maven内部版本。 向Maven Assembly插件添加执行，如下所示。

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

此执行会指示Maven Assembly插件根据`assembly-ui-test-docker-context.xml`中包含的说明创建存档，该说明在插件的术语中称为“程序集描述符”。 程序集描述符列出了必须包含在存档中的所有文件。

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

程序集描述符指示插件创建类型为`.tar.gz`的存档，并将`ui-test-docker-context`分类器分配给该插件。 此外，它还列出了必须包含在存档中的文件：

- `Dockerfile`，对于生成Docker映像是必填项。
- `wait-for-grid.sh`脚本，其目的如下所述。
- 实际的UI测试，由`test-module`文件夹中的Node.js项目实施。

程序集描述符还排除了在本地运行UI测试时可能生成的某些文件。 这样可保证存档更小，生成速度更快。

Cloud Manager会自动提取包含Docker构建上下文的存档，以便在其部署管道期间生成包含测试的Docker图像。 最终，Cloud Manager将运行Docker图像，以针对您的应用程序执行UI测试。

## 编写UI测试{#writing-ui-tests}

本节介绍包含您的UI测试的Docker图像必须遵循的惯例。 Docker图像是基于上一节中所述的Docker构建上下文构建的。

### 环境变量{#environment-variables}

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

### 等待Selenium准备就绪{#waiting-for-selenium}

在测试开始之前， Docker映像负责确保Selenium服务器已启动并运行。 等待Selenium服务的过程分为两步：

1. 从`SELENIUM_BASE_URL`环境变量中读取Selenium服务的URL。
2. 以常规间隔轮询由Selenium API公开的[状态端点](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)。

一旦Selenium的状态端点以正面响应进行回答，测试就可以最终开始。

### 生成测试报告{#generate-test-reports}

Docker图像必须以JUnit XML格式生成测试报告，并将其保存在环境变量`REPORTS_PATH`指定的路径中。 JUnit XML格式是一种广泛用于报告测试结果的格式。 如果Docker图像使用Java和Maven，则[Maven Surefire插件](https://maven.apache.org/surefire/maven-surefire-plugin/)和[Maven Failsafe插件](https://maven.apache.org/surefire/maven-failsafe-plugin/)。 如果Docker图像是使用其他编程语言或测试运行者实施的，请查看所选工具的文档，以了解如何生成JUnit XML报告。

### 上传文件(#upload-files)

测试有时必须将文件上传到正在测试的应用程序。 为了保持Selenium相对于测试的部署保持灵活，无法直接将资产上传到Selenium。 而上传文件将会完成一些中间步骤：

1. 在`UPLOAD_URL`环境变量指定的URL上载文件。 必须在包含多部分表单的一个POST请求中执行上传。 多部件表单必须具有单个文件字段。 这等同于`curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`。 请查阅Docker图像中使用的编程语言的文档和库，了解如何执行此类HTTP请求。
2. 如果上传成功，请求将返回类型为`text/plain`的`200 OK`响应。 响应的内容是不透明的文件句柄。 您可以使用此句柄代替`<input>`元素中的文件路径，以测试应用程序中的文件上载。
