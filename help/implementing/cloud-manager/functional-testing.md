---
title: 功能测试
description: 了解AEMas a Cloud Service部署流程中内置的三种不同类型的功能测试，以确保代码的质量和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: a936f056685f2233a272b4b3105d845f832d143c
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---


# 功能测试 {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能测试"
>abstract="了解AEMas a Cloud Service部署流程中内置的三种不同类型的功能测试，以确保代码的质量和可靠性。"

了解中内置的三种不同类型的功能测试 [AEMas a Cloud Service部署流程](/help/implementing/cloud-manager/deploy-code.md) 以确保代码的质量和可靠性。

## 概述 {#overview}

AEMas a Cloud Service中有三种不同类型的功能测试。

* [产品功能测试](#product-functional-testing)
* [自定义功能测试](#custom-functional-testing)
* [自定义UI测试](#custom-ui-testing)

对于所有功能测试，可以将测试的详细结果下载为 `.zip` 使用 **下载内部版本日志** “构建概述”屏幕中的按钮(作为 [部署过程。](/help/implementing/cloud-manager/deploy-code.md)

这些日志不包括实际AEM运行时进程的日志。 要访问这些日志，请参阅此文档 [访问和管理日志](/help/implementing/cloud-manager/manage-logs.md) 以了解更多详细信息。

产品功能测试和示例自定义功能测试均基于 [AEM测试客户端。](https://github.com/adobe/aem-testing-clients)

## 产品功能测试 {#product-functional-testing}

产品功能测试是AEM中一组稳定的HTTP集成测试(IT)的核心功能，如创作和复制任务。 这些测试由Adobe维护，旨在防止在自定义应用程序代码更改破坏核心功能时对其进行部署。

每当您将新代码部署到Cloud Manager时，都会自动运行产品功能测试，并且无法跳过。

产品功能测试作为开源项目进行维护。 请参阅 [产品功能测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) （详细信息）。

## 自定义功能测试 {#custom-functional-testing}

虽然产品功能测试由Adobe定义，但您可以为自己的应用程序编写自己的质量测试。 此操作将作为生产管道的一部分执行，作为自定义功能测试，以确保应用程序的质量。

自定义功能测试既适用于自定义代码部署，也适用于推送升级，因此编写良好的功能测试可防止AEM代码更改破坏您的应用程序代码时，这一点尤为重要。 自定义功能测试步骤始终存在，无法跳过。

### 编写自定义功能测试 {#writing-functional-tests}

Adobe用于编写产品功能测试的工具可用于编写自定义功能测试。 使用 [产品功能测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 作为如何编写测试的示例。

自定义功能测试的代码是位于 `it.tests` 文件夹。 它应该生成一个包含所有功能测试的JAR。 如果生成的测试JAR多个，则选择的JAR是非确定性的。 如果它生成零个测试JAR，则测试步骤默认会通过。 [请参阅AEM项目原型](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) 示例测试。

测试在Adobe维护的测试基础架构上执行，该基础架构至少包括两个创作实例、两个发布实例和调度程序配置。 这表示您的自定义功能测试针对整个AEM堆栈运行。

自定义功能测试必须打包为与要部署到AEM的工件由同一Maven内部版本生成的单独JAR文件。 通常，这将是一个单独的Maven模块。 生成的JAR文件必须包含所有必需的依赖项，且通常使用 `maven-assembly-plugin` 使用 `jar-with-dependencies` 描述符。

此外，JAR必须具有 `Cloud-Manager-TestType` manifest标头设置为 `integration-test`.

以下是 `maven-assembly-plugin`.

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

在此JAR文件中，要执行的实际测试的类名必须在 `IT`.

例如，名为 `com.myco.tests.aem.it.ExampleIT` 会被执行，但是一个名为 `com.myco.tests.aem.it.ExampleTest` 不会。

此外，要从代码扫描的覆盖范围检查中排除测试代码，测试代码必须位于名为 `it` (覆盖范围排除过滤器为 `**/it/**/*.java`)。

测试类必须是常规的JUnit测试。 测试基础架构的设计和配置是与 `aem-testing-clients` 测试库。 我们强烈鼓励开发人员使用此库并遵循其最佳实践。

请参阅 [`aem-testing-clients` GitHub存储库](https://github.com/adobe/aem-testing-clients) 以了解更多详细信息。

>[!TIP]
>
>[观看此视频](https://www.youtube.com/watch?v=yJX6r3xRLHU) 了解如何使用自定义功能测试来提高您对CI/CD管道的置信度。

## 自定义UI测试 {#custom-ui-testing}

自定义UI测试是一项可选功能，允许您为应用程序创建并自动运行UI测试。 UI测试是在Docker图像中打包的基于硒的测试，以便允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛选择。

请参阅该文档 [自定义UI测试](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) 以了解更多信息。

## 本地测试执行 {#local-test-execution}

由于测试类是JUnit测试，因此它们可以从主流Java IDE（如Eclipse、IntelliJ、NetBeans等）中运行。 由于产品功能测试和自定义功能测试都基于相同的技术，因此通过将产品测试复制到自定义测试中，可以在本地运行这两种测试。

但是，在运行这些测试时，需要设置 `aem-testing-clients` （和基础Sling测试客户端）库。

系统属性如下所示。

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
