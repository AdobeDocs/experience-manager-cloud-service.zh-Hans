---
title: '使用自定义字体 '
description: '使用自定义字体 '
source-git-commit: 10fe582edc8ffc93ea3f8564a64259882bba1d6f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# 使用自定义字体

**Cloud Service通信文档处于测试阶段**

您可以使用Formsas a Cloud Service通信将XDP模板、基于XDP的PDF文档或Acrobat表单(AcroForm)与XML数据结合使用以生成PDF文档。 您可以使用Cloud Service或自定义字体（组织批准的字体）中包含的字体来呈现生成的PDF文档。 您可以使用Cloud Service开发项目向Cloud Service环境添加自定义字体。

## PDF文档的行为

您可以 [嵌入字体](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) 到PDF文档。 嵌入字体后，PDF文档在所有平台上都会显示（外观）相同。 它使用嵌入字体来确保外观和感觉一致。 未嵌入字体时，字体渲染取决于PDF查看器客户端的渲染设置。 如果客户机上提供字体，则PDF会使用指定的字体，否则PDF会以回退字体呈现。

## 将自定义字体添加到Formsas a Cloud Service环境

要向Cloud Service环境添加自定义字体，请执行以下操作：

1. 设置并打开本地开发项目。 您可以使用您选择的任何IDE。
1. 在项目的顶级文件夹结构中，创建一个文件夹以保存自定义字体，并向该文件夹添加自定义字体。 例如， fonts/src/main/resources
   ![字体文件夹](assets/fonts.png)

1. 打开开发项目的顶级pom.xml文件。
1. 添加 `<Font-Archive-Version>` 清单条目到.pom文件，并将版本值设置为1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   </addDefaultEntries>
                   </addDefaultImplementationEntries>
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

1. 签入更新的代码和 [运行管道](/help/implementing/cloud-manager/deploy-code.md) 以将字体部署到Cloud Service环境。
