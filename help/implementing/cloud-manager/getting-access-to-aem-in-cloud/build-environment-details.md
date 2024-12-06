---
title: Cloud Manager的构建环境
description: 了解 Cloud Manager 的构建环境以及它如何构建和测试您的代码。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3bc9ec12de604818f6be1c0717566a5f16c6a7b9
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 58%

---


# 构建环境 {#build-environment}

了解 Cloud Manager 的构建环境以及它如何构建和测试您的代码。

## 构建环境详细信息 {#build-environment-details}

Cloud Manager 使用专门的构建环境构建和测试代码。

* 该构建环境基于 Linux，并派生自 Ubuntu 22.04。
* 安装了 Apache Maven 3.9.4。
   * Adobe 建议用户[更新其 Maven 存储库以使用 HTTPS 代替 HTTP](#https-maven)。
* <!-- OLD --> 安装的Java版本为OracleJDK 11.0.22和OracleJDK 8u401。
<!-- NEW but needed to be removed 12/5/24 * The Java versions installed are Oracle JDK 11.0.22, Oracle JDK 17.0.10, and Oracle JDK 21.0.4. -->
<!-- OLD --> * **重要信息：**&#x200B;默认情况下，JAVA_HOME环境变量设置为`/usr/lib/jvm/jdk1.8.0_401`，其中包含OracleJDK 8u401。 AEM Cloud项目应覆盖此默认值才能使用JDK 11。 有关更多详细信息，请参阅设置Maven JDK版本部分。
<!-- NEW but needed to be removed 12/5/24 * **IMPORTANT:** By default, the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. ***This default should be overridden for AEM Cloud Projects to use JDK 21 (preferred), 17, or 11***. See the [Setting the Maven JDK Version](#alternate-maven-jdk-version) section for more details. -->
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

<!-- OLD below -->

### 使用特定的Java版本

默认情况下，Cloud Manager构建过程使用Oracle8 JDK构建项目，但AEM Cloud Service客户应将Maven执行JDK版本设置为11。

<!-- OLD below -->

#### 设置Maven JDK版本

Adobe建议在`.cloudmanager/java-version file`中将整个Maven执行的JDK版本设置为`11`。

为此，请在管道使用的Git存储库分支中创建一个名为`.cloudmanager/java-version`的文件。 编辑文件，使其仅包含文本`11`。 虽然Cloud Manager也接受值`8`，但AEM Cloud Service项目不再支持此版本。 任何其他值将被忽略。 当指定`11`时，使用Oracle11，并且`JAVA_HOME`环境变量设置为`/usr/lib/jvm/jdk-11.0.22`。

<!-- NEW but needed to be removed 12/5/24 ### Use a specific Java version {#using-java-support}

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 21 (preferred), 17, or 11.

#### Set the Maven JDK version {#alternate-maven-jdk-version}

Adobe recommends setting the Maven execution JDK version to `21` or `17` in a `.cloudmanager/java-version` file.

To do so, create a file named `.cloudmanager/java-version` in the Git repository branch used by the pipeline. Edit the file so that it contains only the text, `21` or `17`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `21` or `17` is specified, Oracle Java 21 or Oracle Java 17 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-21` or `/usr/lib/jvm/jdk-17`.

#### Prerequisites for migrating to building with Java 21 or Java 17 {#prereq-for-building}

>[!NOTE]
>
>*When migrating your application to a new Java build version and runtime version, thoroughly test in dev and stage environments before deploying to production.
>Of special note, the following features have not yet been formally validated with Java 21 runtime: [Forms](/help/forms/home.md), [Workflows](/help/sites-cloud/authoring/workflows/overview.md), [Inbox](/help/sites-cloud/authoring/inbox.md), and [Projects](/help/sites-cloud/authoring/projects/overview.md). If your application relies on these features, ensure comprehensive testing to verify functionality.*

##### About some translation features {#translation-features}

The following features might not function correctly when building with Java 21 or Java 17, and Adobe expects to resolve them by early 2025:

* `XLIFF` (XML Localization Interchange File Format) fails when using Human Translation.  
* `I18n` (Internationalization) does not properly handle language locales Hebrew (`he`), Indonesian (`in`), and Yiddish (`yi`) due to changes in the Locale constructor in newer Java versions.

#### Runtime requirements {#runtime-requirements}

The Java 21 runtime is used for builds on Java 21, Java 17, and Java 11 starting in February 2025. To ensure compatibility, the following adjustments are necessary. 

Library updates can be applied anytime, as they remain compatible with older Java versions.

* **Minimum version of `org.objectweb.asm`:**
Update the usage of `org.objectweb.asm` to version 9.5 or higher to ensure support for newer JVM runtimes.

* **Minimum version of `org.apache.groovy`:**
Update the usage of `org.apache.groovy` to version 4.0.22 or higher to ensure support for newer JVM runtimes.

  This bundle can be indirectly included by adding third party dependencies such as the AEM Groovy Console.

* **Edit a runtime parameter:**
When running AEM locally with Java 21, the start scripts (`crx-quickstart/bin/start` or `crx-quickstart/bin/start.bat`) fail due to the `MaxPermSize` parameter. As a remedy, either remove `-XX:MaxPermSize=256M` from the script or define the environment variable `CQ_JVM_OPTS`, setting it to `-Xmx1024m -Djava.awt.headless=true`.

  Adobe plans to resolve this issue in a future release.

>[!NOTE]
>
>When `.cloudmanager/java-version` is set to `21` or `17`, the Java 21 runtime is deployed. In February or March 2025, the Java 21 runtime is planned for deployment to all customers, even if Java 11 is used to build your code. 

#### Build time requirements

The following adjustments are required to allow building the project with Java 21 and Java 17. They can be updated at any time as they are compatible with older versions of Java.

* **Minimum version of `bnd-maven-plugin`:**
Update the usage of `bnd-maven-plugin` to version 6.4.0 to ensure support for newer JVM runtimes. 

  Versions 7 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended.

* **Minimum version of `aemanalyser-maven-plugin`:**
Update the usage of `aemanalyser-maven-plugin` to version 1.6.6 or higher to ensure support for newer JVM runtimes.

* **Minimum version of `maven-bundle-plugin`:**
Update the usage of `maven-bundle-plugin` to version 5.1.5 or higher to ensure support for newer JVM runtimes. 

  Versions 6 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended.

* **Update dependencies in `maven-scr-plugin`:**
The `maven-scr-plugin` is not directly compatible with Java 21 or Java 17. However, descriptor files can be generated by updating the ASM dependency version in the plugin configuration, as shown in the following example:

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
-->


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
