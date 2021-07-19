---
title: 构建环境详细信息
description: 构建环境详细信息 — Cloud Services
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# 了解构建环境 {#understanding-build-environment}

## 构建环境详细信息 {#build-environment-details}

Cloud Manager使用专门的构建环境来构建和测试您的代码。 此环境具有以下属性：

* 构建环境基于Linux，源自Ubuntu 18.04。
* 已安装Apache Maven 3.6.0。
* 安装的Java版本是OracleJDK 8u202和11.0.2。
* 安装了一些其他系统包，这是必需的：

   * bzip2
   * 解压缩
   * libpng
   * imagemagick
   * graphsmagick

* 其他软件包可在生成时安装，如[下](#installing-additional-system-packages)所述。
* 每栋建筑都是在原始环境下完成的；执行两次时，生成容器不会保留任何状态。
* Maven始终使用以下三个命令运行：

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent packageco-maven-plugin:prepare-agent package`
* Maven在系统级别配置了settings.xml文件，该文件使用名为`adobe-public`的配置文件自动包含公共Adobe **Artifact**&#x200B;存储库。 (有关更多详细信息，请参阅[Adobe公共Maven存储库](https://repo.adobe.com/))。

>[!NOTE]
>尽管Cloud Manager未定义`jacoco-maven-plugin`的特定版本，但使用的版本必须至少为`0.7.5.201505241946`。

### 使用Java 11支持 {#using-java-support}

Cloud Manager现在支持使用Java 8和Java 11构建客户项目。 默认情况下，使用Java 8构建项目。

希望在其项目中使用Java 11的客户可以使用[Apache Maven Toolchains Plugin](https://maven.apache.org/plugins/maven-toolchains-plugin/)执行此操作。

为此，请在pom.xml文件中添加如下所示的`<plugin>`条目：

```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
        <execution>
            <goals>
                <goal>toolchain</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <toolchains>
            <jdk>
                <version>11</version>
                <vendor>oracle</vendor>
           </jdk>
        </toolchains>
    </configuration>
</plugin>
```

>[!NOTE]
>支持的供应商值为`oracle`和`sun`，支持的版本值为`1.8`、`1.11`和`11`。

>[!NOTE]
>Cloud Manager项目内部版本仍在使用Java 8调用Maven，因此通过诸如[Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/)之类的插件检查或强制实施工具链插件中配置的Java版本不起作用，因此不得使用此类插件。

## 环境变量 {#environment-variables}

### 标准环境变量 {#standard-environ-variables}

在某些情况下，客户会发现有必要根据有关项目或管道的信息来更改构建流程。

例如，如果正在通过gulp之类的工具完成构建时的JavaScript缩小，则在为开发环境构建时，可能会希望使用不同的缩小级别，而不是为舞台和生产构建。

为了支持此功能，Cloud Manager会将这些标准环境变量添加到每次执行的生成容器中。

| **变量名称** | **定义** |
|---|---|
| CM_BUILD | 始终设置为“true” |
| 分支 | 为执行配置的分支 |
| CM_PIPELINE_ID | 数值管道标识符 |
| CM_PIPELINE_NAME | 管道名称 |
| CM_PROGRAM_ID | 数字程序标识符 |
| CM_PROGRAM_NAME | 项目名称 |
| ANTRACTS_VERSION | 对于暂存或生产管道，由Cloud Manager生成的合成版本 |
| CM_AEM_PRODUCT_VERSION | 版本名称 |

### 管道变量 {#pipeline-variables}

在某些情况下，客户的构建过程可能取决于特定的配置变量，这些变量不适合放置在Git存储库中，或者需要在使用同一分支的管道执行之间进行更改。

Cloud Manager允许在每个管道基础上通过Cloud Manager API或Cloud Manager CLI配置这些变量。 变量可以存储为纯文本，也可以在静态时加密。 无论哪种情况，变量都可作为环境变量在生成环境中使用，然后可从`pom.xml`文件或其他生成脚本中引用该环境变量。

要使用CLI设置变量，请运行如下命令：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

可列出当前变量：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

变量名称只能包含字母数字和下划线(_)字符。 按照惯例，名字应全部为大写。 每个管道限制为200个变量，在字符串类型变量中，每个名称必须少于100个字符，在secretString类型变量中，每个值必须少于2048个字符，在secretString类型变量中，每个值必须少于500个字符。

当在`Maven pom.xml`文件中使用时，通常会使用类似于下面的语法将这些变量映射到Maven属性：

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```

## 安装其他系统包 {#installing-additional-system-packages}

某些内部版本需要安装其他系统包才能完全正常运行。 例如，内部版本可能会调用Python或ruby脚本，因此需要安装适当的语言解释器。 这可以通过调用[exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/)来调用APT来完成。 此执行通常应包含在特定于Cloud Manager的Maven配置文件中。 例如，要安装python:

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

此技术可用于安装语言特定的软件包，例如，使用`gem`（用于RubyGems）或`pip`（用于Python包）。

>[!NOTE]
>以这种方式安装系统包会&#x200B;**不**&#x200B;将其安装在用于运行Adobe Experience Manager的运行时环境中。 如果您需要在AEM环境中安装系统包，请联系您的Adobe代表。
