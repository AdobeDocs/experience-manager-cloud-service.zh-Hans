---
title: Cloud Manager的构建环境
description: 了解 Cloud Manager 的构建环境以及它如何构建和测试您的代码。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 7b9b9f3b957b27812c4a7e8f2dbcf96d8786b73e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 构建环境 {#build-environment}

了解 Cloud Manager 的构建环境以及它如何构建和测试您的代码。

## 构建环境详细信息 {#build-environment-details}

Cloud Manager 使用专门的构建环境构建和测试代码。

* 该构建环境基于 Linux，并派生自 Ubuntu 22.04。
* 安装了 Apache Maven 3.9.4。
   * Adobe 建议用户[更新其 Maven 存储库以使用 HTTPS 代替 HTTP](#https-maven)。
* 安装的Java版本包括OracleJDK 11.0.22、OracleJDK 17.0.10和OracleJDK 21.0.4。
* **重要信息：**&#x200B;默认情况下，`JAVA_HOME`环境变量设置为`/usr/lib/jvm/jdk1.8.0_401`，其中包含OracleJDK 8u401。 ***AEM Cloud项目应覆盖此默认值以使用JDK 21（首选）、17或11***。 有关更多详细信息，请参阅[设置Maven JDK版本](#alternate-maven-jdk-version)部分。
* 安装了一些其他的必要系统包。
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* 可以在构建时安装其他包，如[安装其他系统包](#installing-additional-system-packages)部分中所述。
* 每个构建都在干净的环境中运行，并且构建容器在执行之间不保留任何状态。
* Maven 始终通过以下三条命令运行。
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* 使用 `settings.xml` 文件在系统级别配置 Maven，并将自动包含使用名为 `adobe-public` 的配置文件的公共 Adobe 构件存储库。（有关更多详细信息，请参阅 [Adobe 公共 Maven 存储库](https://repo1.maven.org/)）。

>[!NOTE]
>
>虽然 Cloud Manager 未定义 `jacoco-maven-plugin` 的具体版本，但使用的版本必须至少为 `0.7.5.201505241946`。

## HTTPS Maven 存储库 {#https-maven}

Cloud Manager [版本 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) 开始了对构建环境的一项滚动更新（在推出版本 2023.12.0 时完成更新），其中包括对 Maven 3.8.8 的更新。Maven 3.8.1 中引入的一项重大更改是旨在减少潜在漏洞的一项安全增强。具体来说，Maven 现在默认禁用所有不安全的 `http://*` 镜像，如 [Maven 发行说明中所述](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291)。

此安全增强导致某些用户可能在构建步骤中遇到问题，尤其是从使用不安全 HTTP 连接的 Maven 存储库下载工件时。

为了确保更新版本的流畅体验，Adobe 建议用户更新其 Maven 存储库以使用 HTTPS 代替 HTTP。此调整与行业日益转向安全通信协议的趋势一致，并有助于构建过程保持安全可靠。

### 使用特定的Java版本 {#using-java-support}

默认情况下，Cloud Manager构建过程使用Oracle8 JDK构建项目，但AEM Cloud Service客户应将Maven执行JDK版本设置为21（首选）、17或11。

#### 设置Maven JDK版本 {#alternate-maven-jdk-version}

Adobe建议在`.cloudmanager/java-version`文件中将Maven执行JDK版本设置为`21`或`17`。

为此，请在管道使用的Git存储库分支中创建一个名为`.cloudmanager/java-version`的文件。 编辑文件，使其仅包含文本`21`或`17`。 虽然Cloud Manager也接受值`8`，但AEM Cloud Service项目不再支持此版本。 任何其他值将被忽略。 当指定`21`或`17`时，使用OracleJava 21或OracleJava 17，并且`JAVA_HOME`环境变量设置为`/usr/lib/jvm/jdk-21`或`/usr/lib/jvm/jdk-17`。

#### 迁移到使用Java 21或Java 17进行构建的先决条件 {#prereq-for-building}

>[!NOTE]
>
>*将应用程序迁移到新的Java内部版本和运行时版本时，请先在开发和暂存环境中进行全面测试，然后再部署到生产环境。
>需要特别指出的是，以下功能尚未正式通过Java 21运行时验证：[Forms](/help/forms/home.md)、[工作流](/help/sites-cloud/authoring/workflows/overview.md)、[收件箱](/help/sites-cloud/authoring/inbox.md)和[项目](/help/sites-cloud/authoring/projects/overview.md)。 如果您的应用程序依赖这些功能，请确保进行全面测试以验证功能。*

##### 关于某些翻译功能 {#translation-features}

使用Java 21或Java 17构建时，以下功能可能无法正确运行，Adobe预计将在2025年初解决这些问题：

* 使用人工翻译时，`XLIFF` （XML本地化交换文件格式）失败。
* 由于较新Java版本中的语言环境构造函数发生了更改，`I18n` （国际化）不能正确处理希伯来语(`he`)、印尼语(`in`)和意第绪语(`yi`)的语言环境。

#### 运行时要求 {#runtime-requirements}

从2025年2月开始，Java 21运行时用于在Java 21、Java 17和Java 11上进行构建。 为确保兼容性，需要进行以下调整。

库更新可以随时应用，因为它们仍与旧版Java兼容。

* **最低版本`org.objectweb.asm`：**
将`org.objectweb.asm`的使用更新到9.5或更高版本，以确保支持较新的JVM运行时。

* **最低版本`org.apache.groovy`：**
将`org.apache.groovy`的使用更新到4.0.22或更高版本，以确保支持较新的JVM运行时。

  可以通过添加第三方依赖项（例如 AEM Groovy Console）间接包含此捆绑包。

* **编辑运行时参数：**
使用Java 21在本地运行AEM时，由于`MaxPermSize`参数，启动脚本（`crx-quickstart/bin/start`或`crx-quickstart/bin/start.bat`）失败。 作为补救措施，请从脚本中删除`-XX:MaxPermSize=256M`或定义环境变量`CQ_JVM_OPTS`，并将其设置为`-Xmx1024m -Djava.awt.headless=true`。

  Adobe计划在以后的版本中解决此问题。

>[!NOTE]
>
>当`.cloudmanager/java-version`设置为`21`或`17`时，将部署Java 21运行时。 2025年2月或3月，计划向所有客户部署Java 21运行时，即使使用Java 11构建代码也是如此。

#### 构建时间要求

需要进行以下调整以允许使用Java 21和Java 17构建项目。 它们可以随时更新，因为它们与旧版本的Java兼容。

* **最低版本`bnd-maven-plugin`：**
将`bnd-maven-plugin`的使用更新到版本6.4.0，以确保支持较新的JVM运行时。

  版本7或更高版本与Java 11或更低版本不兼容，因此不建议升级到该版本。

* **最低版本`aemanalyser-maven-plugin`：**
将`aemanalyser-maven-plugin`的使用更新到版本1.6.6或更高版本，以确保支持较新的JVM运行时。

* **最低版本`maven-bundle-plugin`：**
将`maven-bundle-plugin`的使用更新到版本5.1.5或更高版本，以确保支持较新的JVM运行时。

  版本6或更高版本与Java 11或更低版本不兼容，因此不建议升级到该版本。

* **更新`maven-scr-plugin`中的依赖项：**
`maven-scr-plugin`不直接与Java 21或Java 17兼容。 但是，可以通过更新插件配置中的ASM依赖项版本来生成描述符文件，如以下示例所示：

```XML
<project>
  ...
  <build>
    ...
    <plugins>
      ...
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-scr-plugin</artifactId>
        <version>1.26.4</version>
        <executions>
          <execution>
            <id>generate-scr-scrdescriptor</id>
            <goals>
              <goal>scr</goal>
            </goals>
          </execution>
        </executions>
        <dependencies>
          <dependency>
            <groupId>org.ow2.asm</groupId>
            <artifactId>asm-analysis</artifactId>
            <version>9.7.1</version>
            <scope>compile</scope>
          </dependency>
        </dependencies>
      </plugin>
      ...
    </plugins>
    ...
  </build>
  ...
</project>
```


## 环境变量 — 标准 {#environment-variables}

您可能会发现必须根据项目或管道的相关信息来更改构建过程。

例如，如果在构建时使用gulp等工具进行JavaScript缩小，则不同环境可能首选不同的缩小级别。 与暂存和生产版本相比，开发版本可能使用更轻的缩小级别。

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

## 环境变量 — 管道 {#pipeline-variables}

您的构建过程可能需要特定的配置变量，这些变量不应存储在Git存储库中。 此外，您可能需要在使用同一分支的管道执行之间调整这些变量。

有关详细信息，另请参阅[配置管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)。

## 安装其他系统包 {#installing-additional-system-packages}

一些构建需要其他系统包才能完全运行。 例如，内部版本可能会调用Python或Ruby脚本，并且必须安装适当的语言解释程序。 可以通过在`pom.xml`中调用[`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/)以调用APT来管理此安装过程。 此执行通常应封装在特定于 Cloud Manager 的 Maven 配置文件中。此示例安装 Python。

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
