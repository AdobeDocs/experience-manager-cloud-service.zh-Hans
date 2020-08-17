---
title: AEM应用程序项目-Cloud Service
description: AEM应用程序项目-Cloud Service
translation-type: tm+mt
source-git-commit: 696014ea61c049e719c8c9fdccc2a85b087c2466
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 9%

---


# 创建 AEM 应用程序项目 {#aem-application-project}

## 使用向导创建AEM应用程序项目 {#using-wizard-to-create-an-aem-application-project}

为了帮助新客户入门，Cloud Manger现在能够创建最少的AEM项目作为起点。 此过程基于AEM Project [**Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。


请按照以下步骤在Cloud Manager中创建AEM应用程序项目：

1. 登录到Cloud Manager并完成基本程序设置后，如果存储库为空，“ **Overview** ”屏幕上将显示一张特殊的行动动员卡。

   ![](assets/create-wizard1.png)

1. 单击 **创建** ，导航到创建 **分支和项目屏幕** 。

   ![](assets/create-wizard2.png)

1. “正 **在创建的项目** ”拼贴显示在“ *项目概述* ”屏幕上。

   ![](assets/create-wizard3.png)

1. 程序创建完成后，“程序概 **述”(Program Overview** )页面上会显 *示“添加环境* ”(Add Environment)拼贴。
   ![](assets/create-wizard4.png)

   请参阅 [管理环境](/help/implementing/cloud-manager/manage-environments.md) ，了解如何添加或管理环境。

## 设置项目 {#setting-up-your-project}

### 修改项目设置详细信息 {#modifying-project-setup-details}

为了成功构建和部署Cloud Manager，现有AEM项目需要遵守一些基本规则：

* 项目必须使用Apache Maven构建。
* 在Git存储 *库的根目录中* ，必须有pom.xml文件。 此 *pom.xml* 文件可以引用多个子模块（这些子模块又可能具有其他子模块等） 必要时。

* 您可以在pom.xml文件中添加对其他Maven *项目存储库的引* 用。 配置时 [支持访问受密码保护](#password-protected-maven-repositories) 的对象存储库。 但是，不支持访问受网络保护的对象存储库。
* 可部署的内容包是通过扫描内容包 *zip* 文件来发现的，这些文件包含在名为 *目标的目录中*。 任何数量的子模块都可以生成内容包。

* 通过扫描zip文件(同样，包含在名为 *目标的目录中* )发现可部署的调度程序对象，该目录具有名 *为conf**和conf.d***&#x200B;的目录。

* 如果有多个内容包，则无法保证包部署的顺序。 如果需要特定的订单，可以使用内容包依赖关系定义订单。 可以从部署 [中跳](#skipping-content-packages) 过包。


## 构建环境详细信息 {#build-environment-details}

Cloud Manager使用专用构建环境构建和测试您的代码。 此环境具有以下属性：

* 构建环境基于Linux，源自Ubuntu 18.04。
* Apache Maven 3.6.0已安装。
* 安装的Java版本为Oracle JDK 8u202和11.0.2。
* 还安装了一些其他系统包，这是必需的：

   * bzip2
   * 解压缩
   * libpng
   * imagemagick
   * graphicsmagick

* 其他软件包可以在构建时安装，如 [下所述](#installing-additional-system-packages)。
* 每栋建筑都建在原始环境上；构建容器不会在执行之间保持任何状态。
* Maven始终使用以下命令运行： *mvn —batch-mode clean org.jacoco:jaco-maven-plugin:prepare-agent包*
* Maven在系统级别上配置了settings.xml文件，该文件自动包括公共Adobe **项库** 。 (有关更多详 [细信息，请参阅Adobe](https://repo.adobe.com/) 公共Maven存储库。)

>[!NOTE]
>尽管Cloud Manager未定义特定版本，但 `jacoco-maven-plugin`使用的版本至少必须为 `0.7.5.201505241946`。

### 使用Java 11支持 {#using-java-support}

Cloud Manager现在支持使用Java 8和Java 11构建客户项目。 默认情况下，项目是使用Java 8构建的。

希望在其项目中使用Java 11的客户可以使用Apache Maven Toolchains [插件进行此操作](https://maven.apache.org/plugins/maven-toolchains-plugin/)。

为此，请在pom.xml文件中添加一个 `<plugin>` 如下的条目：

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
>支持的供应商值 `oracle` 是和 `sun`。
>
>支持的版本 `1.8`值 `1.11`有、和 `11`。

## 环境变量 {#environment-variables}

### 标准环境变量 {#standard-environ-variables}

在某些情况下，客户发现有必要根据有关项目或管道的信息改变构建流程。

例如，如果正在通过gulp等工具完成构建时间JavaScript微型化，则在为开发环境构建时可能希望使用不同的微型化级别，而不是为舞台和生产构建。

为支持此功能，Cloud Manager会将这些标准环境变量添加到每次执行的构建容器中。

| **变量名称** | **定义** |
|---|---|
| CM_BUILD | 始终设置为“true” |
| 分支 | 为执行配置的分支 |
| CM_PIPELINE_ID | 数字管线标识符 |
| CM_PIPELINE_NAME | 管道名称 |
| CM_项目_ID | 数字项目标识符 |
| CM_项目_NAME | 项目名称 |
| AFTRACTS_VERSION | 对于舞台或生产管道，由Cloud Manager生成的合成版本 |
| CM_AEM_PRODUCT_VERSION | 版本名称 |

### 管道变量 {#pipeline-variables}

在某些情况下，客户的构建过程可能取决于特定配置变量，这些变量不适合放置在Git存储库中，或者需要在使用同一分支的管道执行之间有所不同。

Cloud Manager允许通过Cloud Manager API或Cloud Manager CLI按管道配置这些变量。 变量可以以纯文本形式存储，也可以在静态时加密。 在任何一种情况下，生成环境中的变量都作为环境变量可用，然后可以从文件或其他生成脚本 `pom.xml` 中引用该变量。

要使用CLI设置变量，请运行如下命令：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

可以列出当前变量：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

变量名称只能包含字母数字和下划线(_)字符。 按照惯例，这些名称应全部为大写。 每个管道限制为200个变量，每个名称必须少于100个字符，每个值必须少于2048个字符。

在文件内使 `Maven pom.xml` 用时，通常可以使用类似于下面的语法将这些变量映射到Maven属性：

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


## 在Cloud Manager中激活Maven用户档案 {#activating-maven-profiles-in-cloud-manager}

在某些有限情况下，在Cloud Manager中运行时，您可能需要稍微改变构建过程，而不是在开发人员工作站上运行。 对于这些情 [况，Maven用户档案](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用于定义不同环境（包括Cloud Manager）中构建内容的不同方式。

在Cloud Manager构建激活中环境Maven用户档案，应通过查找上述CM_BUILD环境变量来完成。 相反，只有在Cloud Manager构建用户档案之外才能使用的环境应通过查找此变量的基本含义来完成。

例如，如果您希望仅在构建在云管理器中运行时输出简单消息，您可以执行以下操作：

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>要在开发人员工作站上测试此用户档案，您可以在命令行上（通过）或在集 `-PcmBuild`成开发环境(IDE)中启用它。

如果您希望仅在构建在Cloud Manager外部运行时输出简单消息，您可以执行以下操作：

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## 受密码保护的Maven存储库支持 {#password-protected-maven-repositories}

要从Cloud Manager中使用受密码保护的Maven存储库，请将密码（以及用户名）指定为机密管 [线变量](#pipeline-variables) ，然后在git存储库中名为的文件中引 `.cloudmanager/maven/settings.xml` 用该机密。 此文件遵循“主设 [置文件”模式](https://maven.apache.org/settings.html) 。 当Cloud Manager构建流程开始时，此 `<servers>` 文件中的元素将合并到Cloud Manager提 `settings.xml` 供的默认文件中。 服务器ID从开 `adobe` 始 `cloud-manager` ，被视为保留ID，不应由自定义服务器使用。 Cloud Manager **将** 永远不会镜像与这些前缀之 `central` 一不匹配的服务器ID或默认ID。 在此文件就位后，服务器ID将从文件内的 `<repository>` 和／或 `<pluginRepository>` 元素中引 `pom.xml` 用。 通常，这 `<repository>` 些和/ `<pluginRepository>` 或元素将包含在特 [定于Cloud Manager的用户档案中](#activating-maven-profiles-in-cloud-manager)，尽管这并不是严格必需的。

例如，假设存储库位于https://repository.myco.com/maven2，则Cloud Manager应使用的用户名为， `cloudmanager` 密码为 `secretword`。

首先，将密码设置为管道上的机密：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

然后从文件中引 `.cloudmanager/maven/settings.xml` 用它：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>myco-repository</id>
            <username>cloudmanager</username>
            <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
        </server>
    </servers>
</settings>
```

最后引用文件中的服务 `pom.xml` 器ID:

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
        <build>
            <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
        </build>
    </profile>
</profiles>
```

## 安装其他系统包 {#installing-additional-system-packages}

某些构建需要安装额外的系统包才能完全运行。 例如，生成可能调用Python或ruby脚本，因此需要安装相应的语言解释器。 这可以通过调用exec- [maven-plugin来调用](https://www.mojohaus.org/exec-maven-plugin/) APT来完成。 此执行通常应包含在特定于Cloud Manager的Maven用户档案中。 例如，安装python:

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

此技术同样可用于安装语言特定的软件包，即用于 `gem` RubyGems或 `pip` Python软件包。

>[!NOTE]
>
>以这种方式安装系统包不 **会将** 它安装在用于运行Adobe Experience Manager的运行时环境中。 如果需要在AEM环境上安装系统包，请与Adobe代表联系。

## 跳过内容包 {#skipping-content-packages}

在Cloud Manager中，构建可能生成任意数量的内容包。
由于各种原因，可能希望生成内容包，但不要部署它。 这可能很有用，例如，在构建仅用于测试的内容包时，或者在构建过程中的另一步骤（即作为另一个包的子包）重新打包的内容包时。

为了适应这些情况，Cloud manager将在构建内容包的属性中 ***查找名为cloudManagerTarget*** 的属性。 如果此属性设置为none，则将跳过并且不部署包。 设置此属性的机制取决于构建生成内容包的方式。 例如，使用filevault-maven-plugin可以配置插件，如下所示：

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

使用content-package-maven-plugin时，它类似：

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## 其他资源 {#additional-resources}

请参阅以下部分，了解如何在Cloud Service中使用Cloud Manager:

* [管理环境](/help/implementing/cloud-manager/manage-environments.md)
* [配置CI-CD管道](/help/implementing/cloud-manager/configure-pipeline.md)
* [部署代码](/help/implementing/cloud-manager/deploy-code.md)
* [了解测试结果](/help/implementing/developing/introduction/understand-test-results.md)