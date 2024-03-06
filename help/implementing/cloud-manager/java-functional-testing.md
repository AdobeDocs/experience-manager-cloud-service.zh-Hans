---
title: Java&trade; 功能测试
description: 了解如何为 AEM as a Cloud Service 编写 Java&trade; 功能测试
exl-id: e014b8ad-ac9f-446c-bee8-adf05a6b4d70
source-git-commit: e463979df1f705283f29d954f9869d85f0a96465
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 92%

---

# Java™ 功能测试

了解如何为 AEM as a Cloud Service 编写 Java™ 功能测试

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

自定义功能测试的代码是位于 `it.tests` 文件夹中的 Java™ 代码。 它应该生成一个包含所有功能测试的 JAR。 如果构建生成多个测试 JAR，那么选择哪个 JAR 是不确定的。 如果它生成零个测试 JAR，则默认通过测试步骤。 有关样本测试，[请参阅 AEM 项目原型](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests)。

测试在 Adobe 维护的测试基础设施上运行，其中包括至少两个作者实例、两个发布实例和一个 Dispatcher 配置。这种设置意味着您的自定义功能测试将针对整个 AEM 堆栈运行。

### 功能测试结构 {#functional-tests-structure}

自定义功能测试必须打包为一个单独的 JAR 文件，该文件由与要部署到 AEM 的工件相同的 Maven 构建生成。 通常这种版本是一个单独的 Maven 模块。 生成的 JAR 文件必须包含所有必需的依赖项，通常使用 `jar-with-dependencies` 描述符的 `maven-assembly-plugin` 创建。

此外，JAR 必须将 `Cloud-Manager-TestType` 清单头设置为 `integration-test`。

以下是 `maven-assembly-plugin` 的示例配置。

```XML
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
</build>
```

在这个 JAR 文件中，要执行的实际测试的类名必须以 `IT` 结尾。

例如，名为 `com.myco.tests.aem.it.ExampleIT` 类将被执行，但名为 `com.myco.tests.aem.it.ExampleTest` 的类将不会执行。

此外，要从代码扫描的覆盖率检查中排除测试代码，测试代码必须位于名为 `it` 的程序包下面（覆盖排除过滤器是 `**/it/**/*.java`）。

测试类必须是正常的 JUnit 测试。 测试基础设施的设计和配置与 `aem-testing-clients` 测试库使用的约定兼容。建议开发人员使用此库并遵循其最佳实践。

有关更多信息，请参阅[`aem-testing-clients` GitHub repo。](https://github.com/adobe/aem-testing-clients)

>[!TIP]
>
>[观看此视频](https://www.youtube.com/watch?v=yJX6r3xRLHU)，了解如何使用自定义功能测试提高您对 CI/CD 管道的信心。

### 前提条件 {#prerequisites}

1. Cloud Manager 中的测试会使用具有技术管理员身份的用户运行。

>[!NOTE]
>
>要从本地计算机中运行功能测试，请创建一个具有类似管理员权限的用户来执行相同的行为。

1. 用于功能测试的容器化基础架构受以下边界限制：


| 类型 | 价值 | 描述 |
|----------------------|-------|--------------------------------------------------------------------|
| CPU | 0.5 | 每次执行测试保留的 CPU 时间量 |
| 内存 | 0.5Gi | 分配给测试的内存量，该值以 GB 为单位 |
| 超时 | 30m | 测试终止后的持续时间。 |
| 推荐持续时间 | 15m | Adobe 建议编写测试的时间不要超过这个时间。 |

>[!NOTE]
>
> 如果您需要更多资源，请创建客户服务案例，并描述您的用例。Adobe 团队会审核您的请求并提供适当的帮助。

#### 依赖项

* aem-cloud-testing-clients：

即将更改用于执行功能测试的容器化基础架构，将需要库 [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) 用于自定义功能测试，将至少更新为版本 **1.2.1**
确保您在中依赖项 `it.tests/pom.xml` 已更新。

```
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

>[!NOTE]
>
>2024年4月6日之后需要此更改。
>如果未更新依赖关系库，将导致“自定义功能测试”步骤中的管道失败。

### 本地测试执行 {#local-test-execution}

在 Cloud Manager 管道中激活功能测试之前，建议使用 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 或实际的 AEM as a Cloud Service 实例本地运行功能测试。

#### 在 IDE 中运行 {#running-in-an-ide}

由于测试类是 JUnit 测试，因此，它们可以从主流 Java™ IDE（如 Eclipse、IntelliJ 和 NetBeans）运行。由于产品功能测试和自定义功能测试都基于相同的技术，因此可以通过将产品测试复制到自定义测试中来在本地运行这两个测试。

但是，在运行这些测试时，需要设置 `aem-testing-clients`（和底层 Sling 测试客户端）库所需的各种系统属性。

系统属性如下。

| 属性 | 描述 | 示例 |
|-------------------------------------|------------------------------------------------------------------|-------------------------|
| `sling.it.instances` | 匹配 Cloud Service 的实例数量应设置为 `2` | `2` |
| `sling.it.instance.url.1` | 应设置为作者 URL | `http://localhost:4502` |
| `sling.it.instance.runmode.1` | 第一个实例的运行模式应设置为 `author` | `author` |
| `sling.it.instance.adminUser.1` | 应设置为作者管理员用户。 | `admin` |
| `sling.it.instance.adminPassword.1` | 应设置为作者管理员密码。 |                         |
| `sling.it.instance.url.2` | 应设置为发布 URL | `http://localhost:4503` |
| `sling.it.instance.runmode.2` | 第二个实例的运行模式应设置为 `publish` | `publish` |
| `sling.it.instance.adminUser.2` | 应设置为发布管理员用户。 | `admin` |
| `sling.it.instance.adminPassword.2` | 应设置为发布管理员密码。 |                         |



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

