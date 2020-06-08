---
title: AEM应用程序项目——云服务
description: AEM应用程序项目——云服务
translation-type: tm+mt
source-git-commit: 57206e36725e28051b2468d47da726e318bd763b
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 11%

---


# 创建 AEM 应用程序项目 {#aem-application-project}

## 使用向导创建AEM应用程序项目 {#using-wizard-to-create-an-aem-application-project}

为了帮助新客户入门，Cloud Manger现在可以创建最少的AEM项目作为起点。 此过程基于AEM项 [**目原型&#x200B;**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。


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

* 您可以在pom.xml文件中添加对其他Maven *项目存储库的引* 用。 但是，不支持访问受密码保护或受网络保护的对象存储库。
* 可部署的内容包是通过扫描内容包 *zip* 文件来发现的，这些文件包含在名为 *目标的目录中*。 任何数量的子模块都可以生成内容包。

* 通过扫描zip文件(同样，包含在名为 *目标的目录中* )发现可部署的调度程序对象，该目录具有名 *为conf**和conf.d***&#x200B;的目录。

* 如果有多个内容包，则无法保证包部署的顺序。 如果需要特定的订单，可以使用内容包依赖关系定义订单。 可以从部署 [中跳](#skipping-content-packages) 过包。


## 构建环境详细信息 {#build-environment-details}

Cloud Manager使用专用构建环境构建和测试您的代码。 此环境具有以下属性：

* 构建环境基于Linux，源自Ubuntu 18.04。
* Apache Maven 3.6.0已安装。
* 安装的Java版本为Oracle JDK 8u202。
* 还安装了一些其他系统包，这是必需的：

   * bzip2
   * 解压缩
   * libpng
   * imagemagick
   * graphicsmagick

* 其他软件包可以在构建时安装，如 [下所述](#installing-additional-system-packages)。
* 每栋建筑都建在原始环境上； 构建容器不会在执行之间保持任何状态。
* Maven始终使用以下命令运行： *mvn —batch-mode clean org.jacoco:jaco-maven-plugin:prepare-agent包*
* Maven在系统级别上配置了一个settings.xml文件，该文件自动包括公共Adobe Artifact **存储库** 。 (有关更多详 [细信息，请参阅Adobe](https://repo.adobe.com/) Public Maven Repository)。


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


### 自定义环境变量 {#custom-environ-variables}

在某些情况下，客户的构建过程可能取决于特定配置变量，这些变量不适合放置在git存储库中。 Cloud Manager允许Adobe代表按客户配置这些变量。 这些变量存储在安全存储位置，并且仅在特定客户的构建容器中可见。 希望使用此功能的客户需要联系其Adobe代表来配置其变量。

配置后，这些变量将作为环境变量可用。 为了将它们用作Maven属性，您可以在pom.xml文件中引用它们，可能在上述用户档案中引用它们：

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <properties>
                  <my.custom.property>${env.MY_CUSTOM_PROPERTY}</my.custom.property>  
            </properties>
        </profile>
```

>[!NOTE]
>
>环境变量名称只能包含字母数字和下划线(_)字符。 按照惯例，这些名称应全部为大写。

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
>以这种方式安装系统包不 **会将** 它安装在用于运行Adobe Experience Manager的运行时环境中。 如果您需要在AEM环境上安装系统包，请与Adobe代表联系。

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
