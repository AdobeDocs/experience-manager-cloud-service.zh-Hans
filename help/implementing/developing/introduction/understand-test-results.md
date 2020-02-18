---
title: 了解测试结果——云服务
description: 了解测试结果——云服务
translation-type: tm+mt
source-git-commit: c34137ba6f49785304ab21355eaad75798f26267

---


# 了解测试结果 {#understand-test-results}

Cloud Manager for Cloud services管道执行将支持执行针对舞台环境运行的测试。 这与在构建和单元测试步骤中运行的测试形成鲜明对比，这些测试在脱机状态下运行，无需访问任何正在运行的AEM环境。
在此上下文中运行的测试有两种类型：
* 客户编写的测试
* Adobe编写的测试

这两种测试都在为运行这些测试而设计的容器化基础架构中运行。


## 代码质量测试 {#code-quality-testing}

作为管道的一部分，将扫描源代码以确保部署符合特定质量标准。 目前，这是通过SonarQube和使用OakPAL的内容包级别检查的组合来实现的。 有100多个规则，这些规则结合了通用Java规则和特定于AEM的规则。 下表总结了测试标准的等级：

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全等级 | A = 0漏洞 <br/>B =至少1个次要漏洞<br/> C =至少1个主要漏洞 <br/>D =至少1个关键漏洞 <br/>E =至少1个阻止程序漏洞 | 关键 | &lt; B |
| 可靠性等级 | A = 0错误 <br/>B =至少1个次要错误 <br/>C =至少1个主要错误 <br/>D =至少1个关键错误E =至少1个阻止程序错误 | 重要信息 | &lt; C |
| 可维护性等级 | 代码气味的未支付补救成本是： <br/><ul><li>&lt;=5%已进入应用程序的时间，评级为A </li><li>评级在6%到10%之间为B </li><li>在11%到20%的评级是C </li><li>21%到50%的评级是D</li><li>超过50%的东西</li></ul> | 重要信息 | &lt; A |
| 范围 | 单位测试线覆盖率和条件覆盖率的组合，使用以下公式：其 <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/>中：CT =在运行单元测试时已至少评估为“true”的条件，而运行单元测试时 <br/>CF =已评估为“false”的条件至少评估一次， <br/>LC =覆盖行= lines_to_cover - unvered_lines <br/><br/> B =条件 <br/>EL =可执行行的总数(lines_to_cover) | 重要信息 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数。 | 信息 | > 1 |
| 未解决问题 | 总体问题类型——漏洞、错误和代码气味 | 信息 | > 1 |
| 复制行 | 重复块中涉及的行数。 <br/>对于要视为重复的代码块： <br/><ul><li>**非Java项目：**</li><li>至少应有100个连续的和重复的令牌。</li><li>这些令牌至少应该在以下位置传播： </li><li>COBOL的30行代码 </li><li>ABAP的20行代码 </li><li>10行代码（适用于其他语言）</li><li>**Java项目：**</li><li> 无论令牌和行的数量如何，都至少应有10个连续和重复的语句。</li></ul> <br/>在检测重复时，会忽略缩进和字符串文本中的差异。 | 信息 | > 1% |


>[!NOTE]
>
>有关更详细 [的定义](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) ，请参阅度量定义。

您可以在此处下载 [规则列表code-quality-rules.xlsx](/help/implementing/cloud-manager/assets/CodeQuality-Rules-new-one.xlsx)

>[!NOTE]
>
>要进一步了解由 [!UICONTROL Cloud Manager执行的自定义代码质量规则]，请参阅自定 [义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

### 处理误报 {#dealing-with-false-positives}

质量扫描过程并不完美，有时会错误地识别实际没有问题的问题。 这称为&quot;假阳性&quot;。

在这些情况下，可以使用标准Java注释对源代码进行注释， `@SuppressWarnings` 该标准Java注释将规则ID指定为注释属性。 例如，一个常见问题是用于检测硬编码密码的SonarQube规则在如何识别硬编码密码方面可能具有攻击性。

要查看特定示例，此代码在AEM项目中很常见，该项目中有连接到某些外部服务的代码：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然后，SonarQube将引发阻止程序漏洞。 查看代码后，您会发现这不是一个漏洞，并可以使用相应的规则ID对此进行注释。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但是，另一方面，如果代码实际上是这样的：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然后，正确的解决方案是删除硬编码密码。

>[!NOTE]
>
>尽管最佳做法是尽可能使注释具体 `@SuppressWarnings` （即仅对导致问题的特定语句或块进行注释），但可以在类级别进行注释。

## 编写功能测试 {#writing-functional-tests}

客户编写的功能测试必须打包为由与要部署到AEM的对象相同的Maven版本生成的单独JAR文件。 通常，这将是一个单独的Maven模块。 生成的JAR文件必须包含所有必需的依赖关系，并且通常使用maven-assembly-plugin使用jar-with-dependencies描述符创建。

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

在此JAR文件中，要执行的实际测试的类名必须以IT结束。

例如，将执行名 `com.myco.tests.aem.ExampleIT` 为的类，但名为的类 `com.myco.tests.aem.ExampleTest` 不执行。

测试类必须是常规JUnit测试。 测试基础架构的设计和配置为与aem-testing-clients测试库使用的惯例兼容。 强烈建议开发人员使用此库并遵循其最佳做法。 有关更多 [详细信息](https://github.com/adobe/aem-testing-clients) ，请参阅Git链接。

## 自定义功能测试 {#custom-functional-test}

管道中的“自定义功能”测试步骤始终存在，并且无法跳过。

但是，如果构建未生成测试JAR，则默认情况下测试通过。 此步骤是在阶段部署后立即执行的。

> 注意:
>“ **下载日志** ”按钮允许访问包含测试执行详细表单日志的ZIP文件。 这些日志不包括实际AEM运行时进程的日志——可以使用常规下载或尾日志功能访问这些日志。 有关更多 [详细信息，请参阅访问和管理日志](/help/implementing/cloud-manager/manage-logs.md) 。

## 本地测试执行 {#local-test-execution}

由于测试类是JUnit测试，它们可以从Eclipse、IntelliJ、NetBeans等主流Java IDE中运行。

但是，当运行这些测试时，必须设置aem-testing-clients（和基础Sling Testing Clients）所期望的各种系统属性。

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