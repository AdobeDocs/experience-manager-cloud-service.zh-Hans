---
title: UI 测试
description: 自定义 UI 测试是一项可选功能，可用于为自定义应用程序创建和自动运行 UI 测试
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: b1eacc8432a73f015529975e6960afbe9dee7565
workflow-type: tm+mt
source-wordcount: '2143'
ht-degree: 56%

---


# UI 测试 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI 测试"
>abstract="自定义 UI 测试是一项可选功能，可用于为应用程序创建和自动运行 UI 测试。 UI 测试是打包在 Docker 图像中的基于 Selenium 的测试，允许在语言和框架（如 Java 和 Maven、Node 和 WebDriver.io，或任何其他基于 Selenium 构建的框架和技术）中进行广泛选择。"

自定义 UI 测试是一项可选功能，可用于为应用程序创建和自动运行 UI 测试。

## 概述 {#custom-ui-testing}

AEM 提供了 [Cloud Manager 质量关卡](/help/implementing/cloud-manager/custom-code-quality-rules.md)集成包，确保对自定义应用程序的顺利更新。 特别是，IT测试门已经支持使用AEM API创建和自动化自定义测试。

UI 测试是打包在 Docker 图像中的基于 Selenium 的测试，允许在语言和框架（如 Java 和 Maven、Node 和 WebDriver.io，或任何其他基于 Selenium 构建的框架和技术）中进行广泛选择。 此外，使用 [AEM项目原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

UI 测试作为每个 Cloud Manager 管道的特定质量关卡的一部分，通过[专用&#x200B;**自定义 UI 测试**&#x200B;步骤执行。](/help/implementing/cloud-manager/deploy-code.md) 任何 UI 测试，包括回归和新功能，都可以检测和报告错误。

与自定义功能测试（用 Java 编写的 HTTP 测试）不同，UI 测试可以是 Docker 映像，其中包含用任何语言编写的测试，只要它们遵循[构建 UI 测试](#building-ui-tests)一节中定义的约定。

>[!TIP]
>
>Adobe 建议遵循 [AEM 项目原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)中提供的结构和语言（JavaScript 和 WDIO）。
>
>Adobe还提供了基于Java和WebDriver的UI测试模块示例。 请参阅 [AEM测试示例存储库](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver) 以了解详细信息。

## UI测试入门 {#get-started-ui-tests}

本节介绍在Cloud Manager中设置执行UI测试所需的步骤。

1. 确定要使用的编程语言。

   * 对于JavaScript和WDIO，请使用在 `ui.tests` 文件夹。

      >[!NOTE]
      >
      >如果您的存储库是在Cloud Manager自动创建之前创建的 `it.tests` 文件夹，则还可以使用 [AEM项目原型。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)

   * 对于Java和WebDriver，请使用 [AEM测试示例存储库。](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)

   * 有关其他编程语言，请参阅 [构建UI测试](#building-ui-tests) 以设置测试项目。

1. 确保根据部分激活UI测试 [客户选择加入](#customer-opt-in) 在本文档中。

1. 开发测试案例和 [在本地运行测试。](#run-ui-tests-locally)

1. 将代码提交到Cloud Manager存储库并执行Cloud Manager管道。

## 构建 UI 测试 {#building-ui-tests}

Maven 项目生成 Docker 构建上下文。 此Docker构建上下文介绍如何创建包含UI测试的Docker图像，Cloud Manager将使用该UI测试生成包含实际UI测试的Docker图像。

本节介绍将 UI 测试项目添加到存储库所需的步骤。

>[!TIP]
>
>的 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 如果您对编程语言没有特殊要求，则可以为您生成符合以下描述的UI测试项目。

### 生成 Docker 构建上下文 {#generate-docker-build-context}

为了生成 Docker 构建上下文，您需要一个 Maven 模块：

* 生成一份档案，其中包含 `Dockerfile` 以及用测试构建 Docker 图像所需的其他所有文件。
* 使用 `ui-test-docker-context` 分类器标记档案。

最简单的方法是配置 [Maven Assembly 插件](https://maven.apache.org/plugins/maven-assembly-plugin/)创建 Docker 构建上下文档案并为其分配正确的分类器。

您可以使用不同的技术和框架构建 UI 测试，但本节假设您的项目的布局方式与以下类似。

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

`pom.xml` 文件负责 Maven 构建。 将执行添加到 Maven Assembly 插件，如下所示。

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

此执行指示 Maven Assembly 插件根 `assembly-ui-test-docker-context.xml` 上下文中包含的指令创建档案，在插件的行话中称为&#x200B;**Assembly 描述符**。 Assembly 描述符列出了必须作为档案的一部分的所有文件。

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

Assembly 描述符指示插件创建 `.tar.gz` 类型的档案，并将 `ui-test-docker-context` 分类器分配给它。 此外，它还列出了必须包含在档案中的文件，包括以下内容。

* 构建 Docker 图像时必须使用 `Dockerfile`
* `wait-for-grid.sh` 脚本，其用途如下所述
* 实际的 UI 测试，由 `test-module` 文件夹中的 Node.js 项目实现

Assembly 描述符还排除了在本地运行 UI 测试时可能生成的一些文件。 这保证了更小的档案和更快的构建。

Cloud Manager 会自动拾取包含 Docker 构建上下文的档案，它将在部署管道期间构建包含测试的 Docker 图像。最终，Cloud Manager 将运行 Docker 图像，对应用程序执行 UI 测试。

构建应该生成零或一个档案。 如果它生成零个档案，则默认通过测试步骤。 如果构建生成多个档案，那么选择哪个档案是不确定的。

### 客户选择启用 {#customer-opt-in}

要使Cloud Manager生成并执行您的UI测试，您必须通过向存储库添加文件来选择加入此功能。

* 文件名称必须为 `testing.properties`。
* 文件内容必须为 `ui-tests.version=1`。
* 文件必须位于maven子模块下方，以便UI测试位于 `pom.xml` 文件来测试子模块。
* 该文件必须位于内置 `tar.gz` 文件的根目录下。

如果此文件不存在，将跳过 UI 测试生成和执行。

要在构建工件中包含 `testing.properties` 文件，请在 `assembly-ui-test-docker-context.xml` 文件中添加 `include` 语句。

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!-- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>如果您的项目不包括此行，则需要编辑该文件并选择进行 UI 测试。
>
>文件可能包含行，建议不要编辑它。 这是因为该行是在引入选择启用 UI 测试之前引入到您的项目中的，而客户不打算编辑该文件。可放心忽略。

如果您使用的是由Adobe提供的示例：

* 对于基于JavaScript的 `ui.tests` 根据 [AEM项目原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)，则可以执行以下命令以添加所需的配置。

   ```shell
   echo "ui-tests.version=1" > testing.properties
   
   if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
     awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
   fi
   ```

* 提供的Java测试示例已经设置了选择加入标记。

## 编写 UI 测试 {#writing-ui-tests}

本节描述包含 UI 测试的 Docker 图像必须遵循的惯例。 Docker 图像是根据上一节所述 Docker 构建上下文构建的。

### 环境变量 {#environment-variables}

以下环境变量将在运行时传递给 Docker 图像。

| 变量 | 示例 | 描述 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium 服务器的 URL |
| `SELENIUM_BROWSER` | `chrome` | Selenium 服务器使用的浏览器实施 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM 作者实例的 URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 登录到AEM创作实例的用户名 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登录到AEM创作实例的密码 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM 发布实例的 URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 登录到AEM发布实例的用户名 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登录到AEM发布实例的密码 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 必须保存测试结果的 XML 报告的路径 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 要使 Selenium 能够访问文件，必须将文件上载到的 URL |

Adobe测试示例提供了用于访问配置参数的帮助程序函数：

* JavaScript:请参阅 [lib/config.js](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/config.js) 模块
* Java:请参阅 [配置](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) 类

### 等待 Selenium 就绪 {#waiting-for-selenium}

在测试开始之前，Docker 图像负责确保 Selenium 服务器启动并运行。 等待 Selenium 服务需要两个步骤。

1. 从 `SELENIUM_BASE_URL` 环境变量中读取 Selenium 服务的 URL。
1. 定期轮询 Selenium API 公开的[状态端点](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)。

一旦 Selenium 的状态端点得到肯定响应，测试就可以开始了。

AdobeUI测试示例使用脚本处理此问题 `wait-for-grid.sh`，在Docker启动时执行，并且仅在网格准备就绪后才开始实际测试执行。

### 生成测试报告 {#generate-test-reports}

Docker 图像必须以 JUnit XML 格式生成测试报告，并将其保存在环境变量 `REPORTS_PATH` 指定的路径中。JUnit XML 格式是一种广泛使用的报告测试结果的格式。 如果 Docker 图像使用 Java 和 Maven，则诸如 [Maven Surefire 插件](https://maven.apache.org/surefire/maven-surefire-plugin/)和 [Maven Failsafe 插件](https://maven.apache.org/surefire/maven-failsafe-plugin/)等标准测试模块可以立即生成此类报告。

如果 Docker 图像是用其他编程语言或测试运行程序实现的，请查看文档，了解如何生成 JUnit XML 报告。

>[!NOTE]
>
>UI测试步骤的结果仅基于测试报表进行评估。 请确保生成相应的报表以执行测试。
>
>使用断言，而不是仅将错误记录到STDERR或返回非零退出代码，否则您的部署管道可能会正常进行。

### 捕获屏幕快照和视频 {#capture-screenshots}

Docker图像可以生成其他测试输出（例如屏幕截图或视频），并将它们保存在环境变量指定的路径中 `REPORTS_PATH`. 测试结果存档中包括任何可在 `REPORTS_PATH` 下找到的文件。

默认情况下，Adobe提供的测试示例会为任何失败的测试创建屏幕截图。

您可以使用帮助程序函数通过测试创建屏幕截图。

* JavaScript: [takeScreenshot命令](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [命令](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java)

如果在UI测试执行期间创建了测试结果存档，则测试日志文件包含对测试结果存档在末尾位置的引用。

```
[...]

===============================================================
The detailed test results can be downloaded from the URL below.
Note: the link will expire after 60 days

    https://results-host/test-results.zip

===============================================================
```

### 上载文件 {#upload-files}

测试有时必须将文件上载到正在测试的应用程序。 为了使 Selenium 的部署相对于您的测试保持灵活性，不可能直接将资产上传到 Selenium。 相反，上载文件需要以下步骤。

1. 在 `UPLOAD_URL` 环境变量指定的 URL 处上载文件。
   * 上载必须在一个带有多部分表单的 POST 请求中执行。
   * 多部分表单必须有一个文件字段。
   * 这相当于 `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`。
   * 查阅 Docker 图像中使用的编程语言的文档和库，了解如何执行此类 HTTP 请求。
   * Adobe测试示例提供了用于上传文件的帮助程序函数：
      * JavaScript:请参阅 [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) 命令。
      * Java:请参阅 [FileHandler](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) 类。
1. 如果上载成功，请求将返回 `200 OK` 响应，响应类型为 `text/plain`。
   * 响应的内容是一个不透明的文件句柄。
   * 您可以使用此句柄代替 `<input>` 元素中的文件路径来测试应用程序中的文件上载。

## 在本地运行UI测试 {#run-ui-tests-locally}

在Cloud Manager管道中激活UI测试之前，建议在本地对 [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 或在实际的AEMas a Cloud Service实例中。

### 前提条件 {#prerequisites}

Cloud Manager中的测试将使用技术管理员用户执行。

要从本地计算机运行UI测试，请创建具有类似管理员权限的用户以实现相同的行为。

### JavaScript测试示例 {#javascript-sample}

1. 打开外壳程序并导航到 `ui.tests` 您的存储库中的文件夹

1. 执行以下命令以使用Maven启动测试

   ```shell
   mvn verify -Pui-tests-local-execution \
   -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
   -DAEM_AUTHOR_USERNAME=<user> \
   -DAEM_AUTHOR_PASSWORD=<password> \
   -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
   -DAEM_PUBLISH_USERNAME=<user> \
   -DAEM_PUBLISH_PASSWORD=<password> \
   -DHEADLESS_BROWSER=true \
   -DSELENIUM_BROWSER=chrome
   ```

>[!NOTE]
>
>* 这会启动一个独立的selenium实例并针对它执行测试。
>* 日志文件存储在 `target/reports` 存储库的文件夹
>* 由于测试会自动下载最新版本的ChromeDriver进行测试，因此您需要确保您使用的是最新的Chrome版本。
>
>有关详细信息，请参阅 [AEM项目原型存储库。](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/README.md)

### Java测试示例 {#java-sample}

1. 打开外壳程序并导航到 `ui.tests/test-module` 您的存储库中的文件夹

1. 执行以下命令以使用Maven启动测试

   ```shell
   # Start selenium docker image (for x64 CPUs)
   docker run --platform linux/amd64 -d -p 4444:4444 selenium/standalone-chrome-debug:latest
   
   # Start selenium docker image (for ARM CPUs)
   docker run -d -p 4444:4444 seleniarm/standalone-chromium
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:<port>
   ```

>[!NOTE]
>
>* 日志文件将存储在 `target/reports` 文件夹。
>
>有关详细信息，请参阅 [AEM测试示例存储库。](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver/README.MD)
