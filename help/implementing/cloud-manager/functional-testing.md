---
title: 功能测试-Cloud Services
description: 功能测试-Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 4%

---


# 功能测试 {#functional-testing}

功能测试分为两类：

* 产品功能测试
* 自定义功能测试

## 产品功能测试 {#product-functional-testing}

产品功能测试是围绕AEM中核心功能（例如，创作和复制）的一组稳定的HTTP集成测试(IT)，可防止客户在中断此核心功能时部署对其应用程序代码所做的更改。

只要客户将新代码部署到Cloud Manager且无法跳过，产品功能测试就会自动运行。

有关示例 [测试，请参阅](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) “Product Functionality tests（产品功能测试）”。

## 自定义功能测试 {#custom-functional-testing}

管道中的“自定义功能”测试步骤始终存在，无法跳过。

但是，如果生成未生成测试JAR，则默认情况下测试通过。

>[!NOTE]
>“ **下载日志** ”按钮允许访问包含测试执行详细表单日志的ZIP文件。 这些日志不包含实际AEM运行时进程的日志——可以使用常规下载或尾日志功能访问这些日志。 有关更多 [详细信息，请参阅](/help/implementing/cloud-manager/manage-logs.md) “访问和管理日志”。


### 编写功能测试 {#writing-functional-tests}

必须将客户编写的功能测试打包为由与要部署到AEM的对象相同的Maven版本生成的单独JAR文件。 通常，这将是一个单独的Maven模块。 生成的JAR文件必须包含所有必需的依赖关系，并且通常使用maven-assembly-plugin使用jar-with-dependencies描述符创建。

此外，JAR必须将Cloud-Manager-TestType清单头设置为integration-test。 将来，预计会支持其他标题值。 maven-assembly-plugin的示例配置是：

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

例如，将执行名 `com.myco.tests.aem.ExampleIT` 为的类，但名为的类 `com.myco.tests.aem.ExampleTest` 不会执行。

测试类必须是普通JUnit测试。 测试基础架构设计并配置为与aem-testing-clients测试库使用的惯例兼容。 强烈建议开发人员使用此库并遵循其最佳实践。 有关更多 [详细信息](https://github.com/adobe/aem-testing-clients) ，请参阅Git链接。

### 本地测试执行 {#local-test-execution}

由于测试类是JUnit测试，它们可以从主流Java IDE（如Eclipse、IntelliJ、NetBeans等）运行。

但是，在运行这些测试时，需要设置aem-testing-clients（和基础Sling Testing Clients）预期的各种系统属性。

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

