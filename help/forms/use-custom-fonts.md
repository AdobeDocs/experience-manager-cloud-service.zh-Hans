---
title: 使用自定义字体
description: 使用自定义字体
exl-id: 88214d36-fb97-4d46-a9fe-71dbc7826eb1
source-git-commit: d60659f443d130a195fd81cfe4773cd87df28264
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# 使用自定义字体

**Cloud Service通信文档处于测试阶段**

您可以使用Formsas a Cloud Service通信将XDP模板、基于XDP的PDF文档或Acrobat表单(AcroForm)与XML数据结合使用以生成PDF文档。 您还可以使用“通信”来组合、重新排列和扩充PDF和XDP文档，并获取有关PDF文档的信息。

除了之前提到的操作之外，您还可以使用Cloud Service或自定义字体（组织批准的字体）中包含的字体来呈现生成的PDF文档。 您可以使用Cloud Service开发项目向Cloud Service环境添加自定义字体。

## PDF文档的行为

您可以 [嵌入字体](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions) 到PDF文档。 嵌入字体后，PDF文档在所有平台上都会显示（外观相同）。 它使用嵌入字体来确保外观和感觉的一致性。 未嵌入字体时，字体渲染取决于Acrobat或Acrobat Reader等PDF查看器客户端的渲染设置。 如果客户机上提供字体，则PDF使用指定的字体，否则PDF将使用默认的回退字体呈现。

## 将自定义字体添加到Formsas a Cloud Service环境 {#custom-fonts-cloud-service}

要向Cloud Service环境添加自定义字体，请执行以下操作：

1. 设置并打开 [地方开发项目](setup-local-development-environment.md). 您可以使用您选择的任何IDE。
1. 在项目的顶级文件夹结构中，创建一个文件夹（模块）以保存自定义字体，并将自定义字体添加到文件夹。 例如， fonts/src/main/resources
   ![字体文件夹](assets/fonts.png)

1. 打开开发项目字体模块的pom.xml文件。
1. 将jar插件添加到pom文件：

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
           </archive>
       </configuration>
   </plugin>
   ```


1. 添加 `<Font-Archive-Version>` 清单输入.pom文件，并将版本值设置为1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
               <manifestEntries>
                   <Font-Archive-Version>1</Font-Archive-Version>
                   <Font-Archive-Contents>/</Font-Archive-Contents>
               </manifestEntries> 
           </archive>
       </configuration>
   </plugin>
   ```

1. 将字体文件夹添加到 `<modules>` 在pom文件中列出。 例如：

   ```xml
   <modules>
       <module>all</module>
       <module>core</module>
       <module>ui.frontend</module>
       <module>ui.apps</module>
       <module>ui.apps.structure</module>
       <module>ui.config</module>
       <module>ui.content</module>
       <module>it.tests</module>
       <module>dispatcher</module>
       <module>dispatcher.ams</module>
       <module>dispatcher.cloud</module>
       <module>ui.tests</module>
       <module>fonts</module>
   </modules>
   ```

   字体文件夹包含所有自定义字体。

1. 签入更新的代码和 [运行管道](/help/implementing/cloud-manager/deploy-code.md) 以将字体部署到Cloud Service环境。

1. （可选）打开命令提示符，导航到本地项目文件夹，然后运行以下命令。 该命令将字体打包到.jar文件中，并包含相关信息。 您可以使用.jar文件将自定义字体添加到FormsCloud Service本地开发环境。

   ```shell
   mvn clean install
   ```

## 将自定义字体添加到本地FormsCloud Service开发环境 {#custom-fonts-cloud-service-sdk}

1. 启动本地开发环境。
1. 导航到 `<aem install directory>/crx-quickstart/install` 文件夹。
1. 将 `<jar file contaning custom fonts and relevant deployment code>.jar` 到安装文件夹。 如果您没有.jar文件，请执行 [将自定义字体添加到Formsas a Cloud Service环境](#custom-fonts-cloud-service) 部分来生成文件。
1. 运行 [基于文档的SDK环境](setup-local-development-environment.md#docker-microservices)


   >[!NOTE]
   >
   >每当您将更新的自定义字体.jar文件部署到本地开发环境时，请重新启动基于Docker的SDK环境。
