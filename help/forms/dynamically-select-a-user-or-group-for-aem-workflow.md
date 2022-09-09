---
title: 为以AEM Forms为中心的工作流步骤动态选择用户或组
description: 了解如何为 [!DNL AEM Forms] 工作流。
content-type: troubleshooting
topic-tags: publish
source-git-commit: 3c2a66ac13ccee9eef87ed3c97288a7475ac64d0
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---


# 为以AEM Forms为中心的工作流步骤动态选择用户或组 {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

了解如何为 [!DNL AEM Forms] 工作流。

在大型组织中，需要动态选择某个流程的用户。 例如，根据座席与客户的接近度，选择现场座席来为客户服务。 在这种情况下，动态选择代理。

分配任务和 [!DNL Adobe Sign] 步骤 [OSGi上以Forms为中心的工作流](aem-forms-workflow.md) 提供用于动态选择用户的选项。 您可以使用ECMAScript或OSGi包动态地选择“分配任务”步骤的代理人，或选择“签名文档”步骤的签名人。

## 使用ECMAScript动态选择用户或组 {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript是一种脚本语言。 它用于客户端脚本和服务器应用程序。 执行以下步骤以使用ECMAScript动态选择用户或组：

1. 打开CRXDE Lite。 URL为 `https://'[server]:[port]'/crx/de/index.jsp`
1. 在以下路径中创建扩展名为.ecma的文件。 如果路径（节点结构）不存在，请创建路径：

   * （分配任务步骤的路径） `/apps/fd/dashboard/scripts/participantChooser`
   * （签名步骤的路径） `/apps/fd/workflow/scripts/adobesign`

1. 将具有动态选择用户逻辑的ECMAScript添加到.ecma文件中。 单击 **[!UICONTROL 全部保存]**.

   有关示例脚本，请参阅 [用于动态选择用户或组的ECMAScript示例](dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. 添加脚本的显示名称。 此名称显示在工作流步骤中。 要指定名称，请执行以下操作：

   1. 展开脚本节点，右键单击 **[!UICONTROL jcr:content]** 节点，然后单击 **[!UICONTROL 混合]**.
   1. 添加 `mix:title` 属性，然后单击 **确定**.
   1. 将以下属性添加到脚本的jcr:content节点：

      | 名称 | 类型 | 值 |
      |--- |--- |--- |
      | jcr:title | 字符串 | 指定脚本的名称。 例如，选择最接近的字段代理。 此名称显示在“分配任务”和“签署文档”步骤中。 |

   1. 单击 **全部保存**. 该脚本在AEM工作流的组件中可供选择。

      ![脚本](assets/script.png)

### 用于动态选择用户或组的示例ECMAScript {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

以下示例ECMAScript动态地为“分配任务”步骤选择一个代理人。 在此脚本中，会根据有效负载的路径选择用户。 在使用此脚本之前，请确保脚本中提及的所有用户都存在于AEM中。 如果脚本中提到的用户在AEM中不存在，则相关过程可能会失败。

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

以下示例ECMAScript动态地为 [!DNL Adobe Sign] 中。 在使用以下脚本之前，请确保脚本中提到的用户信息（电子邮件地址和电话号码）正确无误。 如果脚本中提及的用户信息不正确，则相关过程可能会失败。

>[!NOTE]
>
>关于使用ECMAScript for [!DNL Adobe Sign]，则脚本必须位于crx-repository中/apps/fd/workflow/scripts/adobesign/，且应具有名为getAdobeSignRecipients的函数，以返回用户列表。

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## 使用Java界面动态选择用户或组 {#use-java-interface-to-dynamically-choose-a-user-or-group}

您可以使用 [RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) 用于动态选择用户或组的Java界面 [!DNL Adobe Sign] 和分配任务步骤。 您可以创建使用 [RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java界面并将其部署到 [!DNL AEM Forms] 服务器。 该选项可供在“分配任务”和 [!DNL Adobe Sign] AEM工作流的组件。

您需要 [[!DNL AEM Forms] 客户端SDK](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 罐子 [花岗岩](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) 文件来编译下面列出的代码示例。 将这些jar文件作为外部依赖项添加到OSGi包项目中。 可以使用任何Java IDE创建OSGi包。 以下过程提供了使用Eclipse创建OSGi包的步骤：

1. 打开Eclipse IDE。 导航到 **[!UICONTROL 文件]**> **[!UICONTROL 新建项目]**.
1. 在选择向导屏幕上，选择 **[!UICONTROL Maven项目]**，然后单击 **[!UICONTROL 下一个]**.
1. 在New Maven项目中，保留默认值，然后单击 **[!UICONTROL 下一个]**. 选择原型并单击 **[!UICONTROL 下一个]**. 例如，maven-archetype-quickstart。 指定 **[!UICONTROL 组ID]**, **[!UICONTROL 项目ID]**, **[!UICONTROL 版本]**&#x200B;和 **[!UICONTROL 软件包]** ，然后单击 **[!UICONTROL 完成]**. 随即会创建项目。
1. 打开pom.xml文件进行编辑，并将文件的所有内容替换为以下内容：

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. 添加使用 [RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java界面，用于动态选择“分配”任务步骤的用户或组。 有关示例代码，请参阅 [使用Java界面动态选择用户或组的示例](#-sample-scripts-for).
1. 打开命令提示符，然后导航到包含OSGi包项目的目录。 使用以下命令创建OSGi包：

   `mvn clean install`

1. 将包上载到 [!DNL AEM Forms] 服务器。 您可以使用AEM包管理器将包导入到 [!DNL AEM Forms] 服务器。

导入包后，用于动态选择用户或组的Java界面选项将在中可用，用于Adobe Sign和“分配任务”步骤。

### 用于动态选择用户或组的Java代码示例 {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

以下示例代码可动态选择Adobe Sign步骤的代理人。 在OSGi包中使用代码。 在使用下面列出的代码之前，请确保代码中提及的用户信息（电子邮件地址和电话号码）正确无误。 如果代码中提及的用户信息不正确，则相关过程可能会失败。

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```
