---
title: 功能测试 — Cloud Services
description: 功能测试 — Cloud Services
translation-type: tm+mt
source-git-commit: 765334cff443d56e37f578647af4bcd133509481
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 2%

---


# 功能测试{#functional-testing}

功能测试分为三类：

* 产品功能测试
* 自定义功能测试
* 自定义UI测试

## 产品功能测试{#product-functional-testing}

产品功能测试是一组围绕AEM中核心功能（例如，创作和复制）的稳定HTTP集成测试(IT)，可防止客户在应用程序代码中断此核心功能时部署对其应用程序代码所做的更改。

只要客户将新代码部署到Cloud Manager且无法跳过，产品功能测试就会自动运行。

有关示例测试，请参阅[产品功能测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)。

## 自定义功能测试{#custom-functional-testing}

管道中的“自定义功能”测试步骤始终存在，无法跳过。

但是，如果生成未生成测试JAR，则默认情况下测试通过。

>[!NOTE]
>“ **下载日志** ”按钮允许访问包含测试执行详细表单日志的ZIP文件。 这些日志不包括实际AEM运行时进程的日志 — 可以使用常规下载或尾日志功能访问这些日志。 有关详细信息，请参阅[访问和管理日志](/help/implementing/cloud-manager/manage-logs.md)。

## 自定义UI测试{#custom-ui-testing}

AEM为其客户提供了一套集成的Cloud Manager质量门户，以确保顺利更新其应用程序。 特别是，IT测试门已经允许客户创建并使用AEM API的自动测试。

自定义UI测试功能是一项可选功能[客户选择](#customer-opt-in)，它使我们的客户能够为其应用程序创建和自动运行UI测试。 UI测试是在Docker图像中打包的基于Selenium的测试，以允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛的选择。 您可以从此处进一步了解如何构建UI和编写UI测试。 此外，使用AEM Project Archetype可轻松生成UI测试项目。

客户可以（通过GIT）为用户界面创建自定义测试和测试套件。 UI测试将作为每个Cloud Manager管道的特定质量门的一部分执行，并包含其特定步骤和反馈信息。 任何UI测试（包括回归和新功能）都将允许在客户上下文中检测和报告错误。

客户UI测试在“自定义UI测试”步骤下的生产管道上自动运行。

与使用java编写的HTTP测试（自定义功能测试）不同，UI测试可以是使用任何语言编写测试的文档程序图像，只要它们遵循在[构建UI测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests)中定义的惯例。

>[!NOTE]
>建议以[AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)中便捷提供的结构和语言&#x200B;*（js和wdio）*&#x200B;为起点。

### 客户选择加入{#customer-opt-in}

要构建并执行其UI测试，客户需要通过在UI测试的主子模块（UI测试子模块的pom.xml文件旁边）下的代码存储库中添加一个文件来“选择加入”，并确保此文件位于生成的`tar.gz`文件的根文件中。

*文件名*:  `testing.properties`

*内容*:  `one line: ui-tests.version=1`

如果内置的`tar.gz`文件中不存在此问题，将跳过UI测试生成和执行

>[!NOTE]
>在2021年2月10日之前创建的生产管道需要更新，才能使用本节中所述的UI测试。 这实质上意味着用户必须编辑生产管线，并从UI中单击&#x200B;**保存**，即使未进行任何更改。
>有关管道配置的更多信息，请参阅[配置CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)。

### 编写功能测试{#writing-functional-tests}

必须将客户编写的功能测试打包为由与要部署到AEM的对象相同的Maven生成的单独JAR文件。 通常，这将是一个单独的Maven模块。 生成的JAR文件必须包含所有必需的依赖项，并且通常使用maven-assembly-plugin使用jar-with-dependencies描述符创建。

此外，JAR必须将Cloud-Manager-TestType清单标头设置为integration-test。 将来，预计会支持其他标头值。 maven-assembly-plugin的一个示例配置是：

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

例如，将执行名为`com.myco.tests.aem.ExampleIT`的类，但名为`com.myco.tests.aem.ExampleTest`的类不会执行。

测试类需要是正常的JUnit测试。 测试基础结构设计并配置为与aem-testing-clients测试库使用的惯例兼容。 强烈建议开发人员使用此库并遵循其最佳做法。 有关详细信息，请参阅[Git Link](https://github.com/adobe/aem-testing-clients)。

### 本地测试执行{#local-test-execution}

由于测试类是JUnit测试，它们可以从Eclipse、IntelliJ、NetBeans等主流Java IDE中运行。

但是，在运行这些测试时，需要设置aem-testing-clients（和基础Sling Testing Clients）预期的各种系统属性。

系统属性如下所示：

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

