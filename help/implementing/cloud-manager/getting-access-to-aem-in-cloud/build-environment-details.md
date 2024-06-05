---
title: 构建环境
description: 了解 Cloud Manager 的构建环境以及它如何构建和测试您的代码。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 77%

---


# 构建环境 {#build-environment}

了解 Cloud Manager 的构建环境以及它如何构建和测试您的代码。

## 构建环境详细信息 {#build-environment-details}

Cloud Manager 使用专门的构建环境构建和测试代码。

* 构建环境基于 Linux，并派生自 Ubuntu 22.04。
* 安装了 Apache Maven 3.9.4。
   * Adobe 建议用户[更新其 Maven 存储库以使用 HTTPS 代替 HTTP](#https-maven)。
* 安装的Java版本为OracleJDK 11.0.22和OracleJDK 8u401。
* **重要**：默认情况下， `JAVA_HOME` 环境变量设置为 `/usr/lib/jvm/jdk1.8.0_401` 其中包含OracleJDK 8u401。 *_AEM Cloud项目应覆盖此默认值才能使用JDK 11_*. 请参阅 [设置Maven JDK版本](#alternate-maven-jdk-version) 部分以了解更多详细信息。
* 安装了一些其他的必要系统包。
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* 可以在构建时安装其他包，如[安装其他系统包](#installing-additional-system-packages)部分所述。
* 每次构建都是在一个原始的环境中完成的；构建容器在执行之间不保持任何状态。
* Maven 始终通过以下三条命令运行。
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* 使用 `settings.xml` 文件在系统级别配置 Maven，并将自动包含使用名为 `adobe-public` 的配置文件的公共 Adobe 构件存储库。（有关更多详细信息，请参阅 [Adobe 公共 Maven 存储库](https://repo1.maven.org/)）。

>[!NOTE]
>
>虽然 Cloud Manager 未定义 `jacoco-maven-plugin` 的具体版本，但使用的版本必须至少为 `0.7.5.201505241946`。

## HTTPS Maven 存储库 {#https-maven}

Cloud Manager [版本 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) 开始了对构建环境的一项滚动更新（在推出版本 2023.12.0 时完成更新），其中包括对 Maven 3.8.8 的更新。Maven 3.8.1 中引入的一项重大更改是旨在减少潜在漏洞的一项安全增强。具体来说，Maven 现在默认禁用所有不安全的 `http://*` 镜像，如 [Maven 发行说明中所述。](http://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291)

此安全增强导致某些用户可能在构建步骤中遇到问题，尤其是从使用不安全 HTTP 连接的 Maven 存储库下载工件时。

为了确保更新版本的流畅体验，Adobe 建议用户更新其 Maven 存储库以使用 HTTPS 代替 HTTP。此调整与行业日益转向安全通信协议的趋势一致，并有助于构建过程保持安全可靠。

### 使用特定的 Java 版本 {#using-java-support}

默认情况下，项目通过使用Oracle8 JDK的Cloud Manager构建过程构建，但强烈建议AEM Cloud Service客户将用于执行Maven的JDK版本设置为 `11`.

#### 设置Maven JDK版本 {#alternate-maven-jdk-version}

建议将整个Maven执行的JDK版本设置为 `11` 在 `.cloudmanager/java-version` 文件。

为此，请在管道使用的 Git 存储库分支中创建一个名为 `.cloudmanager/java-version` 的文件。 编辑文件，使其仅包含文本， `11`. 而Cloud Manager也接受值 `8`，AEM Cloud Service项目不再支持此版本。 任何其他值将被忽略。 时间 `11` 指定，使用Oracle11，并且 `JAVA_HOME` 环境变量设置为 `/usr/lib/jvm/jdk-11.0.22`.

## 环境变量 {#environment-variables}

### 标准环境变量 {#standard-environ-variables}

您可能会发现必须根据项目或管道的相关信息来更改构建过程。

例如，如果构建时 JavaScript 缩小是通过 gulp 等工具完成的，那么在为开发环境构建而不是为暂存和生产环境构建时，可能需要使用不同的缩小级别。

为此，Cloud Manager 会为每个执行将这些标准环境变量添加到构建容器中。

| 变量名称 | 定义 |
|---|---|
| `CM_BUILD` | 始终设置为 `true` |
| `BRANCH` | 执行的已配置分支 |
| `CM_PIPELINE_ID` | 数值管道标识符 |
| `CM_PIPELINE_NAME` | 管道名称 |
| `CM_PROGRAM_ID` | 数值项目标识符 |
| `CM_PROGRAM_NAME` | 项目名称 |
| `ARTIFACTS_VERSION` | 对于暂存或生产管道，为由 Cloud Manager 生成的合成版本 |
| `CM_AEM_PRODUCT_VERSION` | 发行版本 |

### 管道变量 {#pipeline-variables}

您的构建过程可能取决于特定的配置变量，这些变量不适合放置在 Git 存储库中，或您可能需要在使用同一分支的管道执行之间切换这些变量。

请参阅文档 [配置管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) 了解更多信息

## 安装其他系统包 {#installing-additional-system-packages}

一些版本需要安装其他系统包才能完全运行。 例如，内部版本可能会调用Python或Ruby脚本，并且必须安装适当的语言解释程序。 可以通过在 `pom.xml` 中调用 [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) 来调用 APT，从而达到此目的。此执行通常应封装在特定于 Cloud Manager 的 Maven 配置文件中。此示例安装 Python。

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

可使用相同的方法安装语言特定的包，例如，使用 `gem` 安装 RubyGems 包或使用 `pip` 安装 Python 包。

>[!NOTE]
>
>通过此方式安装系统包并不会将它安装在用于运行 Adobe Experience Manager 的运行时环境中。 如果您需要在 AEM 环境中安装系统包，请联系您的 Adobe 代表。

>[!TIP]
>
>有关前端构建环境的详细信息，请参阅[使用前端管道开发站点。](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)
