---
title: UI测试-Cloud Services
description: UI测试-Cloud Services
translation-type: tm+mt
source-git-commit: bf3fb5178bc2ae72e19ecc1de82b08fac5089ecf
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# UI测试{#ui-testing}

>[!CAUTION]
>
>此功能尚不普遍可用。


UI测试是将基于硒的测试打包在Docker图像中，以便在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中做出广泛选择。 Docker图像可以使用标准工具创建，但在执行时必须遵守某些约定。 运行Docker映像时，将自动设置Selenium服务器。 下面描述的运行时约定允许测试代码访问Selenium服务器和测试中的AEM实例。

## 构建UI测试{#building-ui-tests}

UI测试是使用Maven项目生成的Docker生成上下文构建的。 Cloud Manager使用Docker构建上下文生成包含实际UI测试的Docker图像。 总之，Maven项目会生成Docker构建上下文，而Docker构建上下文描述如何创建包含UI测试的Docker图像。

本节将介绍将UI测试项目添加到存储库所需的步骤。 如果您速度较快或对编程语言没有特殊要求，[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)可以为您生成UI测试项目。

### 生成Docker生成上下文{#generate-docker-build-context}

要生成Docker构建上下文，您需要一个Maven模块：

- 生成一个归档文件，其中包含`Dockerfile`和通过测试构建Docker映像所需的所有其他文件。
- 使用`ui-test-docker-context`类元标记存档。

实现此目的的最简单方法是配置[Maven Assembly Plugin](http://maven.apache.org/plugins/maven-assembly-plugin/)以创建Docker构建上下文归档文件并为其分配正确的分类器。

您可以使用不同的技术和框架构建UI测试，但本节假定项目的布局方式与以下内容类似。

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

`pom.xml`文件负责Maven内部版本。 向Maven Assembly插件添加执行操作，如下所示。

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

此执行将指示Maven Assembly插件根据`assembly-ui-test-docker-context.xml`中包含的说明创建存档，该说明在插件的术语中称为“程序集描述符”。 程序集描述符将列表所有必须属于存档的文件。

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

程序集描述符指示插件创建类型为`.tar.gz`的归档文件，并将`ui-test-docker-context`类元分配给该类元。 此外，它还列表了必须包含在存档中的文件：

- `Dockerfile`，构建Docker映像时必填。
- `wait-for-grid.sh`脚本，其用途如下所述。
- 实际UI测试，由`test-module`文件夹中的Node.js项目实现。

程序集描述符还排除在本地运行UI测试时可能生成的某些文件。 这保证了较小的存档和更快的构建。

包含Docker构建上下文的存档由云管理器自动拾取，这将在其部署管道期间构建包含测试的Docker映像。 最终，Cloud Manager将运行Docker映像，以针对您的应用程序执行UI测试。

## 编写UI测试{#writing-ui-tests}

本节介绍包含您的UI测试的Docker图像必须遵循的惯例。 Docker图像是基于上一节所述的Docker构建上下文构建的。

### 环境变量{#environment-variables}

以下环境变量将在运行时传递到Docker图像。

| 变量 | 示例 | 描述 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium服务器的URL |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | Selenium Server使用的浏览器实现 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM作者实例的URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 登录AEM作者实例的用户名 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登录AEM作者实例的口令 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM发布实例的URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 登录AEM发布实例的用户名 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登录AEM发布实例的口令 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 必须保存测试结果的XML报告的路径 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必须将文件上传到的URL，以使Selenium能够访问它们 |

### 正在等待Selenium就绪{#waiting-for-selenium}

在测试开始之前，Docker映像负责确保Selenium服务器已启动并运行。 等待Selenium服务的过程分为两个步骤：

1. 从`SELENIUM_BASE_URL`环境变量中读取Selenium服务的URL。
2. 定期轮询到Selenium API公开的[状态端点](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)。

一旦Selenium的状态端点得到正向响应，测试最终可以开始。

### 生成测试报告{#generate-test-reports}

Docker图像必须以JUnit XML格式生成测试报告，并将其保存在环境变量`REPORTS_PATH`指定的路径中。 JUnit XML格式是一种广泛用于测试结果报告的格式。 如果Docker映像使用Java和Maven，则[Maven Surefire插件](https://maven.apache.org/surefire/maven-surefire-plugin/)和[Maven Failsafe插件](https://maven.apache.org/surefire/maven-failsafe-plugin/)。 如果Docker图像是使用其他编程语言或测试运行者实现的，请查阅所选工具的文档以了解如何生成JUnit XML报告。

### 上传文件(#upload-files)

测试有时必须将文件上传到测试中的应用程序。 为了保持Selenium相对于测试的部署灵活性，无法直接将资产上传到Selenium。 而是上传文件经过一些中间步骤：

1. 在`UPLOAD_URL`环境变量指定的URL上传文件。 上传必须使用多部件表单在一个POST请求中执行。 多部件表单必须具有单个文件字段。 这等效于`curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`。 请查阅Docker图像中使用的编程语言的文档和库，了解如何执行此类HTTP请求。
2. 如果上载成功，则请求返回类型为`text/plain`的`200 OK`响应。 响应的内容是不透明的文件句柄。 您可以使用此句柄代替`<input>`元素中的文件路径来测试应用程序中的文件上传。
