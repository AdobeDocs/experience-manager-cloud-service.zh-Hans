---
title: 项目设置
description: 了解如何使用Maven构建AEM项目，以及创建自己的项目时必须遵守的标准。
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 88b4864da30fbf201dbd5bde1ac17d3be977648f
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 68%

---

# 项目设置 {#project-setup}

了解如何使用Maven构建AEM项目，以及创建自己的项目时必须遵守的标准。

## 项目设置详细信息 {#project-setup-details}

要使用Cloud Manager成功构建和部署，AEM项目需要遵循以下准则：

* 必须使用[Apache Maven](https://maven.apache.org)构建项目。
* Git 存储库的根目录中必须有一个 `pom.xml` 文件。 此 `pom.xml` 文件可以根据需要引用尽可能多的子模块（这些子模块又可能包含其他子模块等）。
* 您可以在`pom.xml`文件中添加对其他Maven工件存储库的引用。 配置后，支持访问[受密码保护的工件存储库](#password-protected-maven-repositories)。但是，不支持访问受网络保护的构件存储库。
* 通过扫描包含在名为`target`的目录中的内容包`.zip`文件来发现可部署的内容包。 任意数量的子模块都能生成内容包。
* 通过扫描包含名为`conf`和`conf.d`目录的`.zip`文件（也包含在名为`target`的目录中）发现可部署的Dispatcher工件。
* 如果有多个内容包，则无法保证包部署的排序。 如果需要特定顺序，可以使用内容包依赖关系来定义该顺序。
* 可以在部署期间[跳过](#skipping-content-packages)包。

## 在Cloud Manager中激活Maven配置文件 {#activating-maven-profiles-in-cloud-manager}

在某些限定情况下，在 Cloud Manager 中运行而不是在开发人员工作站上运行时，您可能需要略微更改构建过程。在这些情况下，可使用 [Maven 配置文件](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)定义构建在不同环境（包括 Cloud Manager）中应有哪些不同之处。

应通过查找`CM_BUILD`[环境变量](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)来激活 Cloud Manager 构建环境中的 Maven 配置文件。 同样，只在 Cloud Manager 构建环境之外使用的配置文件应该通过查找是否缺少此变量来激活。

例如，如果您希望仅在 Cloud Manager 中运行构建时输出一条简单消息，则可以这样做：

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
>要在开发人员工作站上测试此配置文件，您可以在命令行上（带 `-PcmBuild`）或集成开发环境 (IDE) 中启用它。

此外，如果您希望仅在 Cloud Manager 外部运行构建时输出一条简单消息，则可以这样做：

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

## 在Cloud Manager中使用受密码保护的Maven存储库 {#password-protected-maven-repositories}

>[!NOTE]
>
>谨慎部署来自受密码保护的Maven存储库的项目，因为Cloud Manager不会使用其[代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)评估此代码。 应当将此方法保留在极少数情况下，并且只应用于与AEM无关的代码。 Adobe建议同时包含Java源和整个项目源代码以及二进制文件。 这样做可确保在整个部署过程中实现更高的透明度和可维护性。

**要在Cloud Manager中使用受密码保护的Maven存储库，请执行以下操作：**

1. 将密码（也可以是用户名）指定为机密[管道变量。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)
1. 然后在 Git 存储库中名为 `.cloudmanager/maven/settings.xml` 的文件中引用该密码，它遵循 [Maven 设置文件](https://maven.apache.org/settings.html)模式。

当 Cloud Manager 构建过程开始时：

* 此文件中的 `<servers>` 元素会合并到 Cloud Manager 提供的默认 `settings.xml` 文件中。
   * 以`adobe`和`cloud-manager`开头的服务器ID被视为保留的。 请勿在自定义服务器上使用它们。
   * Cloud Manager仅镜像与特定前缀或默认ID `central`匹配的那些服务器ID；其他所有服务器ID都排除在镜像之外。
* 有了此文件，将从 `pom.xml` 文件中的 `<repository>` 和/或 `<pluginRepository>` 元素中引用服务器 ID。
* 通常，这`<repository>`和`<pluginRepository>`元素包含在[Cloud Manager特定的配置文件](#activating-maven-profiles-in-cloud-manager)中，但并不严格要求包含它们。

例如，假设存储库位于 `https://repository.myco.com/maven2`，Cloud Manager 应使用的用户名为 `cloudmanager`，密码为 `secretword`。 您将采取以下步骤：

1. 将密码设置为管道中的密钥。

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. 在以下位置从`.cloudmanager/maven/settings.xml`文件中引用此密码：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <settings xmlns="https://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
       <servers>
           <server>
               <id>myco-repository</id>
               <username>cloudmanager</username>
              <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
           </server>
       </servers>
   </settings>
   ```

1. 最后，在 `pom.xml` 文件中引用服务器 ID：

   ```xml
   <profiles>
       <profile>
           <id>cmBuild</id>
           <activation>
                   <property>
                       <name>env.CM_BUILD</name>
                   </property>
           </activation>
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
       </profile>
   </profiles>
   ```

### 部署源 {#deploying-sources}

好的做法是将 Java 源与二进制文件一起部署到 Maven 存储库。

为此，请在项目中配置maven-source-plugin。

```xml
         <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-source-plugin</artifactId>
             <executions>
                 <execution>
                     <id>attach-sources</id>
                     <goals>
                         <goal>jar-no-fork</goal>
                     </goals>
                 </execution>
             </executions>
         </plugin>
```

### 部署项目源 {#deploying-project-sources}

好的做法是将整个项目源与二进制文件一起部署到 Maven 存储库。 这样做可以重建精确的工件。

按照以下方式在项目中配置maven-assembly-plugin：

```xml
         <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-assembly-plugin</artifactId>
             <executions>
                 <execution>
                     <id>project-assembly</id>
                     <phase>package</phase>
                     <goals>
                         <goal>single</goal>
                     </goals>
                     <configuration>
                         <descriptorRefs>
                             <descriptorRef>project</descriptorRef>
                         </descriptorRefs>
                     </configuration>
                 </execution>
             </executions>
         </plugin>
```

## 跳过内容包 {#skipping-content-packages}

在 Cloud Manager 中，构建可以生成任意数量的内容包。出于各种原因，可能需要生成内容包但不部署它。 例如，当仅为测试目的构建内容包或构建过程中的另一个步骤重新打包内容包时。 即，另一个包的子包。

为了适应这些情况，Cloud Manager 会在构建内容包的属性中查找名为 `cloudManagerTarget` 的属性。 如果此属性设置为 `none`，则会跳过并且不会部署包。 

设置此属性的机制取决于生成内容包的方式。 例如，使用 `filevault-maven-plugin` 可以如下配置插件。

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

`content-package-maven-plugin` 拥有相似配置。

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

## 构建构件重用 {#build-artifact-reuse}

在许多情况下，会将同一代码部署到多个 AEM 环境中。如果可能，当 Cloud Manager 检测到在多个全栈管道执行中使用了相同的 git 承诺时，它会避免重建代码库。

开始执行时，系统会提取分支管道的当前 HEAD 承诺。 承诺哈希在 UI 中可见，也可通过 API 查看它。 在构建步骤成功完成时，生成的工件将基于该承诺哈希进行存储，并且可在后续管道执行中重用。

如果包在同一个项目中，则将跨管道重用包。 在查找可重用的包时，AEM 会忽略分支并跨分支重用工件。

在进行重用时，构建和代码质量步骤将有效替换为原始执行所产生的结果。 构建步骤的日志文件列出工件和最初用于构建工件的执行信息。

以下是此类日志输出的示例。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

代码质量步骤的日志包含类似信息。

### 示例 {#example-reuse}

#### 示例 1 {#example-1}

假定您的项目有两个开发管道：

* 管道 1，位于分支 `foo` 上
* 管道 2，位于分支 `bar` 上

两个分支具有同一承诺 ID。

1. 运行管道1首先会正常构建包。
1. 然后，运行管道2会重用管道1创建的包。

#### 示例 2 {#example-2}

假定您的项目有两个分支：

* 分支 `foo`
* 分支 `bar`

两个分支具有同一承诺 ID。

1. 开发管道构建和执行 `foo`。
1. 随后，生产管道构建和执行 `bar`。

在此情况下，由于已识别同一承诺哈希，来自 `foo` 的工件会重用于生产管道。

### 选择退出 {#opting-out}

如果需要，可以通过将管道变量 `CM_DISABLE_BUILD_REUSE` 设置为 `true` 来禁止再次使用特定管道。如果设置了此变量，则系统会提取承诺哈希并存储生成的工件以供以后使用，但会跳过重用任何之前存储的工件。 为了理解此行为，请考虑以下场景：

1. 创建一个新的管道。
1. 执行此管道（执行 #1），当前 HEAD 承诺为 `becdddb`。 执行成功，并且将存储生成的工件。
1. 设置 `CM_DISABLE_BUILD_REUSE` 变量。
1. 重新执行管道而不更改代码。 尽管存在与 `becdddb` 关联的已存储工件，但由于有 `CM_DISABLE_BUILD_REUSE` 变量而不会重用这些工件。
1. 更改代码并执行管道。 HEAD 承诺现在为 `f6ac5e6`。 执行成功，并且将存储生成的工件。
1. 已删除 `CM_DISABLE_BUILD_REUSE` 变量。
1. 重新执行管道而不更改代码。 由于存在与 `f6ac5e6` 关联的已存储构件，因此将再次使用这些构件。

### 注意事项 {#caveats}

* 无论承诺哈希是否相同，构建工件都不会在不同的项目中再次使用。
* 即使分支和/或管道不同，构建工件也将在同一项目中重用。
* [Maven版本处理](/help/implementing/cloud-manager/managing-code/project-version-handling.md)仅在生产管道中替换项目版本。
如果开发部署和生产管道使用同一提交，并且开发部署先运行，则版本将部署到暂存和生产环境，并且保持不变。 不过，在此情况下仍会创建一个标记。
* 如果无法检索已存储的构件，则将运行构建步骤，就像未存储任何构件一样。
* 当 Cloud Manager 决定重用之前创建的构建工件时，不会考虑 `CM_DISABLE_BUILD_REUSE` 之外的管道变量。
