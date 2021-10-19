---
title: 功能测试 — Cloud Services
description: 功能测试 — Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 058fa606bbc667a36b78d5271947e2741f36240f
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 3%

---

# 功能测试 {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能测试"
>abstract="功能测试分为三种类型：产品功能测试、自定义功能测试和自定义UI测试"

功能测试分为三种类型：


* 产品功能测试
* 自定义功能测试
* 自定义UI测试

## 产品功能测试 {#product-functional-testing}

产品功能测试是一组围绕AEM核心功能（例如创作和复制）的稳定HTTP集成测试(IT)，可阻止客户在应用程序代码更改中断此核心功能时对其应用程序代码进行部署。

每当客户将新代码部署到Cloud Manager且无法跳过时，产品功能测试便会自动运行。

请参阅 [产品功能测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 示例测试。

## 自定义功能测试 {#custom-functional-testing}

管道中的自定义功能测试步骤始终存在，无法跳过。

但是，如果内部版本未生成测试JAR，则测试默认通过。

>[!NOTE]
>“ **下载日志** ”按钮允许访问包含测试执行详细表单日志的ZIP文件。 这些日志不包括实际AEM运行时进程的日志 — 可以使用常规下载或尾日志功能访问这些日志。 请参阅 [访问和管理日志](/help/implementing/cloud-manager/manage-logs.md) 以了解更多详细信息。

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

添加 `testing.properties` 文件，添加 `include` 语句 `assembly-ui-test-docker-context.xml` 文件（在UI测试子模块中）：

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

### 编写功能测试 {#writing-functional-tests}

客户编写的功能测试必须打包为由与要部署到AEM的工件相同的Maven内部版本生成的单独JAR文件。 通常，这将是一个单独的Maven模块。 生成的JAR文件必须包含所有必需的依赖项，并且通常使用maven-assembly-plugin使用jar-with-dependencies描述符创建。

此外，JAR必须将Cloud-Manager-TestType清单标头设置为integration-test。 将来，预计会支持其他标头值。 maven-assembly-plugin的示例配置为：

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

在此JAR文件中，要执行的实际测试的类名必须以IT结尾。

例如，名为 `com.myco.tests.aem.ExampleIT` 将被执行，但是一个名为 `com.myco.tests.aem.ExampleTest` 不会。

测试类必须是常规的JUnit测试。 测试基础架构经过设计和配置，可与aem测试客户端测试库使用的惯例兼容。 我们强烈鼓励开发人员使用此库并遵循其最佳实践。 请参阅 [Git链接](https://github.com/adobe/aem-testing-clients) 以了解更多详细信息。

### 本地测试执行 {#local-test-execution}

由于测试类是JUnit测试，因此它们可以从主流Java IDE（如Eclipse、IntelliJ、NetBeans等）中运行。

但是，在运行这些测试时，需要设置aem测试客户端（和基础Sling测试客户端）预期的各种系统属性。

系统属性如下：

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
