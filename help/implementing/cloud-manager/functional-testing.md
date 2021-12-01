---
title: 功能测试 — Cloud Services
description: 功能测试 — Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 778fa187df675eada645c73911e6f02e8a112753
workflow-type: tm+mt
source-wordcount: '485'
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

内部版本应生成零个或一个测试JAR。 如果它生成零个测试JAR，则测试步骤默认会通过。 如果生成的测试JAR多个，则选择的JAR是非确定性的。

>[!NOTE]
>“ **下载日志** ”按钮允许访问包含测试执行详细表单日志的ZIP文件。 这些日志不包括实际AEM运行时进程的日志 — 可以使用常规下载或尾日志功能访问这些日志。 请参阅 [访问和管理日志](/help/implementing/cloud-manager/manage-logs.md) 以了解更多详细信息。


## 编写功能测试 {#writing-functional-tests}

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

在此JAR文件中，要执行的实际测试的类名必须在 `IT`.

例如，名为 `com.myco.tests.aem.it.ExampleIT` 会被执行，但是一个名为 `com.myco.tests.aem.it.ExampleTest` 不会。

此外，要从代码扫描的覆盖范围检查中排除测试代码，测试代码必须位于名为 `it` (覆盖范围排除过滤器为 `**/it/**/*.java`)。

测试类必须是常规的JUnit测试。 测试基础架构经过设计和配置，可与aem测试客户端测试库使用的惯例兼容。 我们强烈鼓励开发人员使用此库并遵循其最佳实践。 请参阅 [Git链接](https://github.com/adobe/aem-testing-clients) 以了解更多详细信息。

## 本地测试执行 {#local-test-execution}

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
