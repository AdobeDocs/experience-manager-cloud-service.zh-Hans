---
title: 功能测试
description: 了解 AEM as a Cloud Service 部署过程内置的三种不同类型的功能测试，确保代码的质量和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: cd0b40ffa54eac0d7488b23329c4d2666c992da7
workflow-type: ht
source-wordcount: '1124'
ht-degree: 100%

---


# 功能测试 {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能测试"
>abstract="了解 AEM as a Cloud Service 部署过程内置的三种不同类型的功能测试，确保代码的质量和可靠性。"

了解 [AEM as a Cloud Service 部署过程](/help/implementing/cloud-manager/deploy-code.md)内置的三种不同类型的功能测试，确保代码的质量和可靠性。

## 概述 {#overview}

AEM as a Cloud Service 中有三种不同类型的功能测试。

* [产品功能测试](#product-functional-testing)
* [自定义功能测试](#custom-functional-testing)
* [自定义 UI 测试](#custom-ui-testing)

对于所有功能测试，可以使用构建概述屏幕中的&#x200B;**下载构建日志**&#x200B;按钮作为[部署过程](/help/implementing/cloud-manager/deploy-code.md)的一部分，将测试的详细结果作为 `.zip` 文件下载。

这些日志不包括实际 AEM 运行时进程的日志。 要访问这些日志，请参阅文档[访问和管理日志](/help/implementing/cloud-manager/manage-logs.md)，了解更多详细信息。

产品功能测试和样本自定义功能测试都基于 [AEM 测试客户端](https://github.com/adobe/aem-testing-clients)。

### 产品功能测试 {#product-functional-testing}

产品功能测试是 AEM 中核心功能（如创作和复制任务）的一组稳定 HTTP 集成测试 (IT)。这些测试由 Adobe 维护，旨在防止在破坏核心功能的情况下部署对自定义应用程序代码的更改。

* [生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)：每当您将新代码部署到 Cloud Manager 时，产品功能测试都会自动运行，不能跳过。
* [非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)：可以选择在执行非生产管道时运行产品功能测试。

产品功能测试作为开源项目进行维护。有关详细信息，请参阅 GitHub 中的[产品功能测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)。

### 自定义功能测试 {#custom-functional-testing}

虽然产品功能测试由 Adobe 定义，但您可以为自己的应用程序编写自己的质量测试。 这类质量测试将作为自定义功能测试执行，作为[生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)或（可选）[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)的一部分，用以确保应用程序的质量。

自定义功能测试既可用于自定义代码部署，也可用于推送升级，这对于编写良好的功能测试（防止 AEM 代码更改破坏应用程序代码）尤为重要。自定义功能测试步骤始终存在，不能跳过。

### 自定义 UI 测试 {#custom-ui-testing}

自定义 UI 测试是一项可选功能，可用于为应用程序创建和自动运行 UI 测试。 UI 测试是打包在 Docker 映像中的基于 Selenium 的测试，允许在语言和框架（如 Java 和 Maven、Node 和 WebDriver.io，或任何其他基于 Selenium 构建的框架和技术）中进行广泛选择。

请参阅[自定义 UI 测试](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)文档，了解更多信息。

## 功能测试快速入门 {#getting-started-functional-tests}

在 Cloud Manager 中创建新的代码存储库后，系统会使用示例测试案例自动创建 `it.tests` 文件夹。

>[!NOTE]
>
>如果您的存储库先于 Cloud Manager 自动创建的 `it.tests` 文件夹之前创建，则也可以使用 [AEM 项目原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)生成最新版本。

在 `it.tests` 文件夹中包含内容后，您可以基于该内容创建自己的测试，然后：

1. [开发您的测试案例。](#writing-functional-tests)
1. [本地运行测试。](#local-test-execution)
1. 将代码提交到 Cloud Manager 存储库并执行 Cloud Manager 管道。

## 编写自定义功能测试 {#writing-functional-tests}

Adobe 用来编写产品功能测试的工具也可以用来编写自定义功能测试。 使用 GitHub 中的[产品功能测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)作为如何编写测试的示例。

自定义功能测试的代码是位于 `it.tests` 文件夹中的 Java 代码。 它应该生成一个包含所有功能测试的 JAR。 如果构建生成多个测试 JAR，那么选择哪个 JAR 是不确定的。 如果它生成零个测试 JAR，则默认通过测试步骤。 有关样本测试，[请参阅 AEM 项目原型](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests)。

测试在 Adobe 维护的测试基础设施上执行，包括至少两个作者实例、两个发布实例和一个 Dispatcher 配置。这意味着您的自定义功能测试将针对整个 AEM 堆栈运行。

### 功能测试结构 {#functional-tests-structure}

自定义功能测试必须打包为一个单独的 JAR 文件，该文件由与要部署到 AEM 的工件相同的 Maven 构建生成。 通常这是一个单独的 Maven 模块。 生成的 JAR 文件必须包含所有必需的依赖项，通常使用 `jar-with-dependencies` 描述符的 `maven-assembly-plugin` 创建。

此外，JAR 必须将 `Cloud-Manager-TestType` 清单头设置为 `integration-test`。

以下是 `maven-assembly-plugin` 的示例配置。

```java
<build>
    <plugins>
        <!-- Create self-contained jar with dependencies -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifestEntries>
                        <Cloud-Manager-TestType>integration-test</Cloud-Manager-TestType>
                    </manifestEntries>
                </archive>
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
    </plugins>
```

在这个 JAR 文件中，要执行的实际测试的类名必须以 `IT` 结尾。

例如，名为 `com.myco.tests.aem.it.ExampleIT` 类将被执行，但名为 `com.myco.tests.aem.it.ExampleTest` 的类将不会执行。

此外，要从代码扫描的覆盖率检查中排除测试代码，测试代码必须位于名为 `it` 的程序包下面（覆盖排除过滤器是 `**/it/**/*.java`）。

测试类需要是正常的 JUnit 测试。 测试基础设施的设计和配置与 `aem-testing-clients` 测试库使用的约定兼容。强烈建议开发人员使用此库并遵循其最佳实践。

请参阅文档 [`aem-testing-clients`GitHub 存储库](https://github.com/adobe/aem-testing-clients)，了解更多详细信息。

>[!TIP]
>
>[观看此视频](https://www.youtube.com/watch?v=yJX6r3xRLHU)，了解如何使用自定义功能测试提高您对 CI/CD 管道的信心。

### 本地测试执行 {#local-test-execution}

在 Cloud Manager 管道中激活功能测试之前，建议使用 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 或实际的 AEM as a Cloud Service 实例本地运行功能测试。

#### 前提条件 {#prerequisites}

Cloud Manager 中的测试将使用具有技术管理员身份的用户执行。

要从本地计算机中运行功能测试，请创建一个具有类似管理员权限的用户来执行相同的行为。

#### 在 IDE 中运行 {#running-in-an-ide}

由于测试类是 JUnit 测试，因此，它们可以从主流 Java IDE（如 Eclipse、IntelliJ 和 NetBeans）运行。由于产品功能测试和自定义功能测试都基于相同的技术，因此可以通过将产品测试复制到自定义测试中来在本地运行这两个测试。

但是，在运行这些测试时，需要设置 `aem-testing-clients`（和底层 Sling 测试客户端）库所需的各种系统属性。

系统属性如下。

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, for example, admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

#### 使用 Maven 运行所有测试 {#using-maven}

1. 打开 shell 并导航到存储库中的 `it.tests` 文件夹。

1. 执行以下命令，并提供必要的参数以使用 Maven 启动测试。

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```
