---
title: 项目设置
description: 了解AEM项目如何使用Maven构建，以及在创建您自己的项目时必须遵守的标准。
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 1%

---

# 项目设置 {#project-setup}

了解AEM项目如何使用Maven构建，以及在创建您自己的项目时必须遵守的标准。

## 项目设置详细信息 {#project-setup-details}

要使用Cloud Manager成功构建和部署AEM项目，需要遵循以下准则：

* 必须使用 [阿帕奇·马文。](https://maven.apache.org)
* 一定有 `pom.xml` 文件。 此 `pom.xml` 文件可以引用任意数量的子模块（这些子模块又可能具有其他子模块等） 视需要。
* 您可以在 `pom.xml` 文件。
   * 访问 [受密码保护的项目存储库](#password-protected-maven-repositories) 配置时支持。 但是，不支持访问受网络保护的对象存储库。
* 通过扫描内容包来发现可部署的内容包 `.zip` 文件，包含在名为 `target`.
   * 任意数量的子模块可以生成内容包。
* 通过扫描发现可部署的调度程序工件 `.zip` 文件(也包含在名为 `target`)，其目录名为 `conf` 和 `conf.d`.
* 如果有多个内容包，则无法保证包部署的顺序。
   * 如果需要特定顺序，可以使用内容包依赖关系来定义顺序。
* 包可以 [跳过](#skipping-content-packages) 部署期间。

## 在Cloud Manager中激活Maven配置文件 {#activating-maven-profiles-in-cloud-manager}

在某些有限情况下，在Cloud Manager内运行时，您可能需要略微改变构建过程，而不是在开发人员工作站上运行。 对于这些情况， [Maven用户档案](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用于定义在包括Cloud Manager在内的不同环境中，内部版本应有何不同。

在Cloud Manager内部版本环境中，激活Maven配置文件的方法是：查找 `CM_BUILD` [环境变量。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 同样，应通过查找此变量的缺失来完成仅在Cloud Manager构建环境之外使用的配置文件。

例如，如果您希望仅在Cloud Manager中运行内部版本时才输出简单消息，则可以执行此操作。

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
>要在开发人员工作站上测试此配置文件，您可以在命令行中启用它(使用 `-PcmBuild`)或集成开发环境(IDE)中。

如果您希望仅在内部版本在Cloud Manager之外运行时才输出简单消息，则可以执行此操作。

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

>[!NOTE]
>
>受密码保护的Maven存储库中的对象只应非常谨慎地使用，因为通过此机制部署的代码当前并未在所有 [代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md) 在Cloud Manager的质量门户中实施。 因此，它只应用于极少数情况下以及未绑定到AEM的代码。 建议还应将Java源以及整个项目源代码与二进制文件一起部署。

要在Cloud Manager中使用受密码保护的Maven存储库，请执行以下操作：

1. 将密码（和可选用户名）指定为密码 [管道变量。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)
1. 然后在名为 `.cloudmanager/maven/settings.xml` 在git存储库中，该存储库将遵循 [Maven设置文件](https://maven.apache.org/settings.html) 架构。

当Cloud Manager构建过程开始时：

* 的 `<servers>` 此文件中的元素将合并到默认 `settings.xml` 文件。
   * 服务器ID以 `adobe` 和 `cloud-manager` 视为保留，不应被自定义服务器使用。
   * 服务器ID与这些前缀或默认ID中的一个不匹配 `central` 将永远不会被Cloud Manager镜像。
* 此文件就位后，服务器ID将从 `<repository>` 和/或 `<pluginRepository>` 元素内部 `pom.xml` 文件。
* 通常， `<repository>` 和/或 `<pluginRepository>` 元素将包含在 [特定于Cloud Manager的配置文件](#activating-maven-profiles-in-cloud-manager)，尽管这并非严格必要。

例如，假设存储库位于 `https://repository.myco.com/maven2`，则Cloud Manager应使用的用户名为 `cloudmanager`，密码为 `secretword`. 您将采取以下步骤。

1. 将密码设置为管道中的密钥。

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. 在 `.cloudmanager/maven/settings.xml` 文件。

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

1. 最后，在 `pom.xml` 文件：

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

最好将Java源与二进制文件一起部署到Maven存储库。

为此，请在项目中配置maven-source-plugin 。

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

最好将整个项目源与二进制文件一起部署到Maven存储库。 这允许重建确切的对象。

为此，请在项目中配置maven-assembly-plugin。

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

在Cloud Manager中，内部版本可能会生成任意数量的内容包。 出于各种原因，可能需要生成内容包，但不部署它。 例如，在构建仅用于测试的内容包时，或者在构建过程中的其他步骤（即，作为其他包的子包）中重新打包的内容包时，可能会出现这种情况。

为了适应这些情况，Cloud manager将在构建内容包的属性中 `cloudManagerTarget`查找名为 的属性。 如果此属性设置为 `none`，则会跳过并且不部署包。

设置此属性的机制取决于内部版本生成内容包的方式。 例如，使用 `filevault-maven-plugin` 您可以按如下方式配置插件。

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

的 `content-package-maven-plugin` 具有类似的配置。

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

## 构建对象重用 {#build-artifact-reuse}

在许多情况下，会将相同的代码部署到多个AEM环境。 如果Cloud Manager检测到在多个全堆栈管道执行中使用相同的git提交，则将尽可能避免重建代码库。

启动执行时，将提取分支管道的当前HEAD提交。 提交哈希在UI中和通过API可见。 成功完成构建步骤后，将基于提交哈希存储生成的工件，并可在后续管道执行中重复使用。 当重复使用时，构建和代码质量步骤会被有效地替换为原始执行的结果。 生成步骤的日志文件将列出最初用于生成对象的工件和执行信息。

以下是此类日志输出的示例。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

代码质量步骤的日志将包含类似信息。

### 选择退出 {#opting-out}

如果需要，可以通过设置管道变量来禁用特定管道的重复使用行为 `CM_DISABLE_BUILD_REUSE` to `true`. 如果设置了此变量，则仍会提取提交哈希，并且将存储所生成的工件以供日后使用，但之前存储的任何工件将不会重复使用。 要了解此行为，请考虑以下情景。

1. 将创建新管道。
1. 将执行(执行#1)并且当前HEAD提交为 `becdddb`. 执行成功，并且会存储所生成的工件。
1. 的 `CM_DISABLE_BUILD_REUSE` 变量。
1. 将在不更改代码的情况下重新执行管道。 尽管存储了与 `becdddb`，由于 `CM_DISABLE_BUILD_REUSE` 变量。
1. 将更改代码并执行管道。 HEAD提交现在为 `f6ac5e6`. 执行成功，并且会存储所生成的工件。
1. 的 `CM_DISABLE_BUILD_REUSE` 变量。
1. 将在不更改代码的情况下重新执行管道。 由于存储了与 `f6ac5e6`，则这些工件将被重复使用。

### 注意事项 {#caveats}

* [Maven版本处理](/help/implementing/cloud-manager/managing-code/project-version-handling.md) 仅在生产管道中替换项目版本。 因此，如果开发部署执行和生产管道执行都使用相同的提交，并且首先执行开发部署管道，则这些版本将部署到暂存和生产环境，而不会发生更改。 但是，在这种情况下仍将创建标记。
* 如果存储的工件检索失败，则执行生成步骤，如同尚未存储任何工件一样。
* 管道变量(而非 `CM_DISABLE_BUILD_REUSE` 当Cloud Manager决定重复使用之前创建的内部版本对象时，不会考虑使用该对象。
