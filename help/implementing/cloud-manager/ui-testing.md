---
title: UI 测试
description: 自定义 UI 测试是一项可选功能，可用于为自定义应用程序创建和自动运行 UI 测试
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 498a58c89910f41e6b86c5429629ec9282028987
workflow-type: tm+mt
source-wordcount: '2601'
ht-degree: 56%

---


# UI 测试 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI 测试"
>abstract="自定义 UI 测试是一项可选功能，可用于为应用程序创建和自动运行 UI 测试。 UI测试是打包在Docker图像中的基于Selenium的测试，允许在语言和框架中进行广泛选择。 例如Java和Maven、Node和WebDriver.io，或任何其他基于Selenium构建的框架和技术。"

自定义 UI 测试是一项可选功能，可用于为应用程序创建和自动运行 UI 测试。

## 概述 {#custom-ui-testing}

AEM 提供了 [Cloud Manager 质量关卡](/help/implementing/cloud-manager/custom-code-quality-rules.md)集成包，确保对自定义应用程序的顺利更新。 特别是，IT 测试门已支持使用 AEM API 创建和自动化定制测试。

UI 测试被打包为 Docker 映像，以便可选择多种语言和框架（如 Cypress、Selenium、Java 和 Maven 以及 JavaScript）。此外，通过使用[AEM项目原型](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/developing/archetype/overview)，可以轻松生成UI测试项目。

Adobe 建议使用 Cypress，因为它提供实时重新加载和自动等待，而这些功能有助于在测试期间节省时间并提高工作效率。Cypress还提供了简单直观的语法，使其易于学习和使用，即使对于新手测试的用户也是如此。

UI测试在&#x200B;[**自定义UI测试**](/help/implementing/cloud-manager/deploy-code.md)&#x200B;步骤中作为质量关卡运行 — 在[生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)中是必需的，在[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)中是可选的。 任何 UI 测试，包括回归和新功能，都可以检测和报告错误。

与自定义功能测试（用Java编写的HTTP测试）不同，UI测试可以是Docker映像。 测试可以使用任何语言编写，只要它们遵循[生成UI测试](#building-ui-tests)一节中定义的约定即可。

>[!TIP]
>
>Adobe 建议使用 Cypress，遵循 [AEM 测试示例存储库](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)中提供的代码进行 UI 测试。
> 
>Adobe 还提供了一些 UI 测试模块示例，分别基于 JavaScript WebdriverIO（请参考 [AEM 项目原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)）以及基于 Java WebDriver（请参考 [AEM 测试示例存储库](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)）。

## 开始使用 UI 测试 {#get-started-ui-tests}

此部分介绍了设置 UI 测试以在 Cloud Manager 中执行所需的步骤。

1. 决定要使用的测试框架。

   * 对于Cypress（默认），请使用[AEM测试示例存储库](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)中的示例代码，或者使用在Cloud Manager存储库的`ui.tests`文件夹中自动生成的示例代码。

   * 对于Playwright，请使用[AEM测试示例存储库](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright)中的示例代码。

   * 对于Webdriver.IO，请使用[AEM测试示例存储库](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio)中的示例代码。

   * 对于Selenium WebDriver，请使用[AEM测试示例存储库](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)中的示例代码。

   * 对于其他编程语言，请参阅本文档中的[构建 UI 测试](#building-ui-tests)部分来设置测试项目。

1. 确保根据本文档的[客户选择启用](#customer-opt-in)部分中的说明操作来激活 UI 测试。

1. 开发您的测试案例，并[在本地运行测试](#run-ui-tests-locally)。

1. 将代码提交到 Cloud Manager 存储库并执行 Cloud Manager 管道。

## 构建 UI 测试 {#building-ui-tests}

Maven 项目生成 Docker 构建上下文。 此 Docker 构建上下文描述了如何创建包含 UI 测试的 Docker 映像，Cloud Manager 将使用它生成包含实际 UI 测试的 Docker 映像。

此部分介绍将 UI 测试项目添加到存储库所需的步骤。

>[!TIP]
>
>如果您对编程语言没有特殊要求，[AEM 项目原型](https://github.com/adobe/aem-project-archetype)会为您生成符合以下说明的 UI 测试项目。

### 生成 Docker 构建上下文 {#generate-docker-build-context}

要生成 Docker 构建上下文，您需要一个 Maven 模块执行以下操作：

* 生成一份档案，其中包含 `Dockerfile` 以及用测试构建 Docker 映像所需的其他所有文件。
* 使用 `ui-test-docker-context` 分类器标记档案。

最简单的方法是配置[Maven Assembly插件](https://maven.apache.org/plugins/maven-assembly-plugin/)以创建Docker构建上下文档案并为其分配正确的分类器。

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

Assembly 描述符指示插件创建 `.tar.gz` 类型的档案，并将 `ui-test-docker-context` 分类器分配给它。 此外，它还列出了必须包含在档案中的文件，包括以下内容：

* 构建 Docker 映像时必须使用 `Dockerfile`
* `wait-for-grid.sh` 脚本，其用途如下所述
* 实际的 UI 测试，由 `test-module` 文件夹中的 Node.js 项目实现

Assembly 描述符还排除了在本地运行 UI 测试时可能生成的一些文件。 这保证了更小的档案和更快的构建。

Cloud Manager在部署管道期间自动选取Docker build-context存档并构建测试映像。 最终，Cloud Manager运行Docker图像，对应用程序执行UI测试。

构建应该生成零或一个档案。 如果它生成零个档案，则默认通过测试步骤。 如果构建生成多个档案，那么选择哪个档案是不确定的。

### 客户选择启用 {#customer-opt-in}

对于 Cloud Manager，要构建和执行 UI 测试，您必须通过向存储库添加文件来选择此功能。

* 文件名称必须为 `testing.properties`。
* 文件内容必须为 `ui-tests.version=1`。
* 该文件必须在 UI 测试子模块的 `pom.xml` 文件旁边的 maven 子模块下。
* 该文件必须位于内置 `tar.gz` 文件的根目录下。

如果此文件不存在，则会跳过 UI 测试生成和执行。

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
>如果您的项目不包括此行，请编辑该文件以选择进行UI测试。
>
>文件可能包含行，建议不要编辑它。 原因在于，该文件是在引入选择加入UI测试之前引入到您的项目中的，并且客户端不打算编辑该文件。 您可以放心地忽略该建议。

如果您使用的是 Adobe 提供的示例：

* 对于从 [AEM 项目原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)生成的基于 JavaScript 的 `ui.tests` 文件夹，您可以执行以下命令来添加所需的配置。

  ```shell
  echo "ui-tests.version=1" > testing.properties
  
  if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
    awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
  fi
  ```

* Adobe提供的Cypress和Java Selenium测试示例已设置选择加入标志。

## 编写 UI 测试 {#writing-ui-tests}

本节描述包含 UI 测试的 Docker 映像必须遵循的惯例。 Docker 映像是根据上一节所述 Docker 构建上下文构建的。

### 环境变量 {#environment-variables}

根据您的框架，以下环境变量会在运行时传递给 Docker 映像。

>[!NOTE]
>
> 这些值在管道执行期间自动设置；无需将其作为管道变量手动设置。

| 变量 | 示例 | 描述 | 测试框架 |
|----------------------------|----------------------------------|----------------------------------------------------------------------------------------------------|---------------------|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium服务器的URL | 仅 Selenium |
| `SELENIUM_BROWSER` | `chrome` | Selenium服务器使用的浏览器实施 | 仅 Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM创作实例的URL | 所有 |
| `AEM_AUTHOR_USERNAME` | `admin` | 用于登录到AEM创作实例的用户名 | 所有 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 用于登录到AEM创作实例的密码 | 所有 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM发布实例的URL | 全部* |
| `AEM_PUBLISH_USERNAME` | `admin` | 用于登录到AEM发布实例的用户名 | 全部* |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登录AEM发布实例的密码 | 全部* |
| `REPORTS_PATH` | `/usr/src/app/reports` | 必须保存测试结果的XML报告的路径 | 所有 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必须将文件上传到的URL以使测试框架可以访问它们 | 所有 |
| `PROXY_HOST` | `proxy-host` | 测试框架使用的内部HTTP代理的主机名 | 除Selenium之外的所有其他产品 |
| `PROXY_HTTPS_PORT` | `8071` | 用于HTTPS连接的代理服务器侦听端口（可以为空） | 除Selenium之外的所有其他产品 |
| `PROXY_HTTP_PORT` | `8070` | 用于HTTP连接的代理服务器侦听端口（可以为空） | 除Selenium之外的所有其他产品 |
| `PROXY_CA_PATH` | `/path/to/root_ca.pem` | 测试框架使用的CA证书的路径 | 除Selenium之外的所有其他产品 |
| `PROXY_OBSERVABILITY_PORT` | `8081` | 代理服务器的HTTP `healthcheck`端口 | 除Selenium之外的所有其他产品 |
| `PROXY_RETRY_ATTEMPTS` | `12` | 等待代理服务器就绪时重试尝试的建议次数 | 除Selenium之外的所有其他产品 |
| `PROXY_RETRY_DELAY` | `5` | 等待代理服务器就绪时重试尝试之间的建议延迟 | 除Selenium之外的所有其他产品 |

`* these values will be empty if there is no publish instance`

Adobe 测试示例提供了帮助程序函数来访问配置参数：

Cypress：使用标准函数 `Cypress.env('VARIABLE_NAME')`
<!-- BOTH URLs are 404 JavaScript: See the [`lib/config.js`](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests.wdio/test-module/lib/config.js) module
* Java: See the [`Config`](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) class -->

### 生成测试报告 {#generate-test-reports}

Docker 映像必须以 JUnit XML 格式生成测试报告，并将其保存在环境变量 `REPORTS_PATH` 指定的路径中。JUnit XML 格式是一种广泛使用的报告测试结果的格式。如果 Docker 映像使用 Java 和 Maven，则诸如 [Maven Surefire 插件](https://maven.apache.org/surefire/maven-surefire-plugin/)和 [Maven Failsafe 插件](https://maven.apache.org/surefire/maven-failsafe-plugin/)等标准测试模块可以立即生成此类报告。

如果 Docker 映像是用其他编程语言或测试运行程序实现的，请查看文档，了解如何生成 JUnit XML 报告。

>[!NOTE]
>
>仅根据测试报告评估 UI 测试步骤的结果。请确保为您的测试执行生成相应报告。
>
>使用断言而不是仅仅将错误记录到 STDERR 或返回非零退出代码，否则，您的部署管道可能会正常进行。
>
>如果在测试执行期间使用了HTTP代理，则结果包括`request.log`文件。

### 前提条件 {#prerequisites}

* Cloud Manager 中的测试会使用具有技术管理员身份的用户运行。

>[!NOTE]
>
>要从本地计算机中运行功能测试，请创建一个具有类似管理员权限的用户来执行相同的行为。

* 用于功能测试的容器化基础架构受以下边界限制：

| 类型 | 价值 | 描述 |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | 每次测试执行保留的CPU时间量。 |
| 内存 | 1Gi | 分配给测试的内存量。 值以GB为单位。 |
| 超时 | 30m | 测试运行的时长。 |
| 推荐持续时间 | 15m | Adobe建议在此时间限制内进行测试。 |

>[!NOTE]
>
> 如果您需要更多资源，请创建客户关怀案例并描述您的用例；Adobe会审查您的请求并提供适当的帮助。

## 特定于 Selenium 详细信息

>[!NOTE]
>
>此部分仅在选择 Selenium 作为测试基础设施时适用。

### 等待 Selenium 就绪 {#waiting-for-selenium}

在测试开始之前，Docker 映像负责确保 Selenium 服务器启动并运行。 等待 Selenium 服务需要两个步骤。

1. 从 `SELENIUM_BASE_URL` 环境变量中读取 Selenium 服务的 URL。
1. 定期轮询Selenium API公开的[状态终结点](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)。

一旦 Selenium 的状态端点得到肯定响应，测试就可以开始了。

Adobe的UI测试示例使用`wait-for-grid.sh`。 它在Docker启动时运行，仅在网格就绪后启动测试。


### 捕获屏幕快照和视频 {#capture-screenshots}

Docker 映像可能会产生额外的测试输出（例如，屏幕快照或视频），并将其保存在环境变量 `REPORTS_PATH` 指定的路径中。测试结果存档中包括任何可在 `REPORTS_PATH` 下找到的文件。

默认情况下，Adobe 提供的测试示例将为任何失败的测试创建屏幕快照。

您可以使用辅助程序函数通过测试创建屏幕快照。

<!-- BOTH URLS ARE 404
* JavaScript: [takeScreenshot command](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [Commands](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java) -->

如果在执行UI测试期间创建了测试结果存档，则可以通过单击`Download Details`自定义UI测试&#x200B;[**步骤**&#x200B;下的](/help/implementing/cloud-manager/deploy-code.md)按钮从Cloud Manager下载该存档。

### 上载文件 {#upload-files}

测试有时必须将文件上载到正在测试的应用程序。 为了使Selenium的部署相对于您的测试保持灵活性，无法将资产直接上传到Selenium。 相反，上载文件需要以下步骤。

1. 在 `UPLOAD_URL` 环境变量指定的 URL 处上载文件。
   * 上载必须在一个带有多部分表单的 POST 请求中执行。
   * 多部分表单必须有一个文件字段。
   * 相当于`curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`。
   * 查阅 Docker 图像中使用的编程语言的文档和库，了解如何执行此类 HTTP 请求。

   <!-- BOTH URLS ARE 404
   * The Adobe test samples provide helper functions for uploading files:
     * JavaScript: See the [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) command.
     * Java: See the [FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) class. -->

1. 如果上载成功，请求将返回 `200 OK` 响应，响应类型为 `text/plain`。
   * 响应的内容是一个不透明的文件句柄。
   * 您可以使用此句柄代替 `<input>` 元素中的文件路径来测试应用程序中的文件上载。

## Cypress特定的详细信息

>[!NOTE]
>
>此部分仅在Cypress是选定的测试基础结构时适用。

### 设置HTTP代理

Docker容器的入口点需要检查`PROXY_HOST`环境变量的值。

如果此值为空，则无需执行其他步骤，并且无需使用HTTP代理即可执行测试。

如果不为空，则入口点脚本需要：

1. 通过导出使用以下值生成的`HTTP_PROXY`环境变量，配置用于运行UI测试的HTTP代理连接：
   * 代理主机，由`PROXY_HOST`变量提供
   * 代理端口，由`PROXY_HTTPS_PORT`或`PROXY_HTTP_PORT`变量提供（使用具有非空值的变量）
2. 设置连接到HTTP代理时使用的CA证书。 其位置由`PROXY_CA_PATH`变量提供。
   * 导出`NODE_EXTRA_CA_CERTS`环境变量。
3. 等待HTTP代理准备就绪。
   * 要检查准备情况，可以使用环境变量`PROXY_HOST`、`PROXY_OBSERVABILITY_PORT`、`PROXY_RETRY_ATTEMPTS`和`PROXY_RETRY_DELAY`。
   * 您可以使用cURL请求进行检查，并确保在`Dockerfile`中安装cURL。

在[GitHub](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/run.sh)上的Cypress示例测试模块的Entrypoint中可以找到示例实施。

## 特定于播放器的详细信息

>[!NOTE]
>
> 此部分仅在`Playwright`为所选测试基础结构时适用。

### 设置HTTP代理

>[!NOTE]
>
> 在所示的示例中，Adobe假定将Chrome用作项目浏览器。

与Cypress类似，如果提供了非空的`PROXY_HOST`环境变量，则测试需要使用HTTP代理。

在这种情况下，需要进行以下编辑。

#### Dockerfile

安装cURL和`libnss3-tools`，后者提供`certutil.`

```dockerfile
RUN apt -y update \
    && apt -y --no-install-recommends install curl libnss3-tools \
    && rm -rf /var/lib/apt/lists/*
```

#### 入口点脚本

包括一个bash脚本，在提供`PROXY_HOST`环境变量时，该脚本将执行以下操作：

1. 导出与代理相关的变量，如`HTTP_PROXY`和`NODE_EXTRA_CA_CERTS`
2. 使用`certutil`安装Chromium™的代理CA证书。
3. 等待HTTP代理准备就绪（或失败时退出）。

实施示例：

```bash
# setup proxy environment variables and CA certificate
if [ -n "${PROXY_HOST:-}" ]; then
  if [ -n "${PROXY_HTTPS_PORT:-}" ]; then
    export HTTP_PROXY="https://${PROXY_HOST}:${PROXY_HTTPS_PORT}"
  elif [ -n "${PROXY_HTTP_PORT:-}" ]; then
    export HTTP_PROXY="http://${PROXY_HOST}:${PROXY_HTTP_PORT}"
  fi
  if [ -n "${PROXY_CA_PATH:-}" ]; then
    echo "installing certificate"
    mkdir -p $HOME/.pki/nssdb
    certutil -d sql:$HOME/.pki/nssdb -A -t "CT,c,c" -n "EaaS Client Proxy Root" -i $PROXY_CA_PATH
    export NODE_EXTRA_CA_CERTS=${PROXY_CA_PATH}
  fi
  if [ -n "${PROXY_OBSERVABILITY_PORT:-}" ] && [ -n "${HTTP_PROXY:-}" ]; then
    echo "waiting for proxy"
    curl --silent  --retry ${PROXY_RETRY_ATTEMPTS:-3} --retry-connrefused --retry-delay ${PROXY_RETRY_DELAY:-10} \
      --proxy ${HTTP_PROXY} --proxy-cacert ${PROXY_CA_PATH:-""} \
      ${PROXY_HOST}:${PROXY_OBSERVABILITY_PORT}
    if [ $? -ne 0 ]; then
      echo "proxy is not ready"
      exit 1
    fi
  fi
fi
```

#### 播放器配置

修改播放器配置（例如在`playwright.config.js`中）以在设置`HTTP_PROXY`环境变量时使用代理。

实施示例：

```javascript
const proxyServer = process.env.HTTP_PROXY || ''
```

```javascript
// enable proxy if set
if (proxyServer !== '') {
 cfg.use.proxy = {
  server: proxyServer,
 }
}
```

>[!NOTE]
>
> 在[GitHub](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright)上的Playwright示例测试模块中可以找到示例实施。


## 本地运行 UI 测试 {#run-ui-tests-locally}

在Cloud Manager管道中激活UI测试之前，Adobe建议您针对[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)在本地运行UI测试。 或者，针对实际的AEM as a Cloud Service实例运行。

### Cypress 测试示例 {#cypress-sample}

1. 打开 shell 并导航到存储库中的 `ui.tests/test-module` 文件夹

1. 安装 Cypress 和其他先决条件

   ```shell
   npm install
   ```

1. 设置测试执行所需的环境变量

   ```shell
   export AEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_AUTHOR_USERNAME=<user>
   export AEM_AUTHOR_PASSWORD=<password>
   export AEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_PUBLISH_USERNAME=<user>
   export AEM_PUBLISH_PASSWORD=<password>
   export REPORTS_PATH=target/
   ```

1. 使用以下命令之一运行测试

   ```shell
   npm test              # Using default Cypress browser
   npm run test-chrome   # Using Google Chrome browser
   npm run test-firefox  # Using Firefox browser
   ```

>[!NOTE]
>
>日志文件存储在存储库的 `target/` 文件夹中.
>
>有关详细信息，请参阅[AEM测试示例存储库](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md)。

### JavaScript WebdriverIO 测试示例 {#javascript-sample}

1. 打开 shell 并导航到存储库中的 `ui.tests` 文件夹。

1. 执行以下命令以使用Maven启动测试。

   ```shell
   mvn verify -Pui-tests-local-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>* 此命令启动独立的Selenium实例并对其执行测试。
>* 日志文件存储在存储库的 `target/reports` 文件夹中
>* 您需要确保计算机运行的是最新版本的 Chrome，因为测试会自动下载最新版本的 ChromeDriver 以进行测试。
>
>有关详细信息，请参阅[AEM测试示例存储库](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio)。

### Playwright测试示例 {#playwright-sample}

1. 打开 shell 并导航到存储库中的 `ui.tests` 文件夹

1. 执行以下命令以使用Maven构建Docker映像

   ```shell
   mvn clean package -Pui-tests-docker-build
   ```

1. 执行以下命令以使用 Maven 启动测试

   ```shell
   mvn verify -Pui-tests-docker-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>日志文件存储在存储库的 `target/` 文件夹中.
>
>有关详细信息，请参阅[AEM测试示例存储库](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright)。


### Java Selenium WebDriver 测试示例 {#java-sample}

1. 打开 shell 并导航到存储库中的 `ui.tests/test-module` 文件夹

1. 执行以下命令以使用 Maven 启动测试

   ```shell
   # Start selenium docker image
   # we mount /tmp/shared as a shared volume that will be used between selenium and the test module for uploads
   docker run -d -p 4444:4444 -v /tmp/shared:/tmp/shared selenium/standalone-chromium:latest
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:4444
   ```

>[!NOTE]
>
>日志文件存储在存储库的 `target/reports` 文件夹中.
>
>有关详细信息，请参阅[AEM测试示例存储库](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md)。
