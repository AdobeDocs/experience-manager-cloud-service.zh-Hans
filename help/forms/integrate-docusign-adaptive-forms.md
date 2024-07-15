---
title: 如何将DocuSign与自适应表单集成？
description: 了解如何将DocuSign与自适应表单一起使用来收集电子签名。
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 7%

---

# 将DocuSign与自适应表单结合使用 {#integrate-aem-forms-with-DocuSign}

DocuSign是一个著名的电子签名解决方案。 您可以用它来电子签署协议。 您可以将DocuSign与自适应表单集成。 它有助于您将电子签名的自适应表单发送给多个收件人。 使用电子签名可帮助您：

- 使用完全自动化的计划书、报价和合同流程从任何设备完成交易。
- 更快地完成人力资源流程，并为员工提供数字体验。
- 缩短合同周期，更快地吸引供应商。

AEM Formsas a Cloud Service为DocuSign](#deploy-custom-submit-action)提供了[自定义提交操作。 提交操作可帮助您使用DocuSign API发送电子签名自适应表单。

| 您还可以使用Adobe的电子签名解决方案Adobe Sign对自适应表单进行电子签名。 AEM Forms与Adobe Sign的集成更深入了，它提供了更精细的控制，如顺序和并行签名、多种身份验证方法、表单内签名体验等。 有关详细信息，请参阅[在自适应表单中使用Adobe Sign](working-with-adobe-sign.md)。 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## 先决条件 {#prerequisites}

要将DocuSign与AEM Forms集成，需要以下项：

- DocuSign [开发人员帐户](https://developers.docusign.com/platform/account/)
- DocuSign应用程序
- DocuSign API应用程序的凭据（客户端ID和客户端密码）。
- [自定义提交操作和DocuSign的云服务](https://github.com/adobe/aem-forms-docusign-sample)
- （仅适用于本地开发环境）[设置记录文档](setup-local-development-environment.md#docker-microservices)。

## 配置自定义提交操作和DocuSign云服务 {#deploy-custom-submit-action}

AEM Formsas a Cloud Service为DocuSign提供了一个自定义提交操作。 提交操作可帮助您使用DocuSign API发送电子签名自适应表单。 自定义提交操作的代码在[AEM Forms示例公共Git存储库](https://github.com/adobe/aem-forms-docusign-sample)上可用。 您可以在您的AEM Forms环境中按原样部署代码，也可以根据贵组织的要求自定义代码。

执行以下步骤以配置现成的自定义提交操作和DocuSignCloud Service：

1. [克隆AEM Formsas a Cloud Service项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment)或基于[AEM Archetype 27](https://github.com/adobe/aem-project-archetype)或更高版本将[!DNL Experience Manager Forms]创建为[!DNL Cloud Service]项目。 要基于AEM原型将[!DNL Experience Manager Forms]创建为[!DNL Cloud Service]项目，请执行以下操作：
   </br>打开命令提示符并运行以下命令以创建[!DNL Experience Manager Forms]as a Cloud Service项目：

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   此外，更改上述命令中的`appTitle`、`appId`和`groupId`以反映您的环境。

1. 克隆[aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample)存储库。 此存储库包含用于DocuSign的自定义提交操作以及连接到DocuSign服务器的配置详细信息。

1. 打开在步骤1中创建的AEM Formsas a Cloud Service项目，以便在您选择的IDE中进行编辑。

1. 打开`[AEM Forms as a Cloud Service project]\pom.xml`文件进行编辑，并进行以下更改：

   1. 在`<properties>`标记的末尾添加以下文本：

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. 在`<repositories>`标记的末尾添加以下文本：

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      如果没有`<repositories>`标记，请在`<properties>`标记下创建标记。

   1. 在`<dependencyManagement>`标记的末尾添加以下文本：

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. 在Cloud Service项目文件夹中可用的`all/pom.xml`文件中执行以下步骤：

   1. 在`<embeddeds>`标记的末尾添加以下文本：

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. 在`<dependencies>`标记的末尾添加以下文本：

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. 打开命令提示符并导航到`aem-forms-samples\forms-integration-docusign`（在步骤3中克隆）并运行以下命令：

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>`引用在此过程的步骤1中创建的文件夹的名称。

1. 将项目部署到您的本地开发环境。 您可以使用以下命令部署到本地开发环境

   `mvn -PautoInstallPackage clean install`

   执行这些步骤后，您可以查看本地开发环境中的自适应表单和[DocuSign云服务配置](#configure-docusign-with-aem-forms)的提交选项列表中提供的新的自定义提交操作[使用DocuSign电子签名提交](#enabledocusign)。

1. 编译代码并将其[部署到您的 [!DNL AEM Forms] as a Cloud Service环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases)。

## 将[!DNL DocuSign]与[!DNL AEM Forms]集成 {#configure-docusign-with-aem-forms}

满足前提条件后，执行以下步骤以在创作实例上将[!DNL DocuSign]与[!DNL AEM Forms]集成。

1. 导航到&#x200B;**[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL DocuSign]**，然后选择要承载配置的文件夹。

1. 在配置页面上，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以在AEM Forms中创建[!DNL DocuSign]配置。
1. 在&#x200B;**[!UICONTROL 创建DocuSign配置]**&#x200B;页面的&#x200B;**[!UICONTROL 常规]**&#x200B;选项卡中，为该配置指定一个&#x200B;**[!UICONTROL 名称]**，然后选择&#x200B;**[!UICONTROL 下一步]**。 您可以选择指定&#x200B;**[!UICONTROL 标题]**。

1. 将当前浏览器窗口中的 URL 复制到记事本。在下一个步骤中使用 [!DNL AEM Forms] 配置 [!DNL DocuSign] 应用程序时需要此 URL。

1. 配置 [!DNL DocuSign] 应用程序的 OAuth 设置：

   1. 打开浏览器窗口并登录到您的[!DNL DocuSign] [开发人员帐户](https://admindemo.docusign.com/apps-and-keys)。
   1. 打开为[!DNL AEM Forms]配置的应用。
   1. 在&#x200B;**[!UICONTROL 重定向URI]**&#x200B;框中，添加上一步中复制的URL，然后单击&#x200B;**[!UICONTROL 保存]**。
   1. 记下集成和密钥。

   有关为 [!DNL DocuSign] 应用程序配置 OAuth 设置并获取密钥的分步信息，请参阅[为应用程序配置 OAuth 设置](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys)开发人员文档。

1. 返回&#x200B;**[!UICONTROL 创建DocuSign配置]**&#x200B;页面。 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，**[!UICONTROL OAuth URL]**&#x200B;字段提及以下默认URL：

   `https://account-d.docusign.com/oauth/auth`

1. 指定&#x200B;**[!UICONTROL 客户端ID]** （DocuSign集成密钥）和&#x200B;**[!UICONTROL 客户端密钥]** （DocuSign密钥）。

1. 选择&#x200B;**[!UICONTROL 连接到DocuSign]**。 在系统提示输入凭据时，提供在创建 [!DNL DocuSign] 应用程序时所用帐户的用户名和密码。当要求您确认`your developer account`的访问时，请单击&#x200B;**[!UICONTROL 允许访问]**。 如果凭据正确，将显示一条成功消息。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建[!DNL DocuSign]配置。

1. 选择配置并单击&#x200B;**[!UICONTROL Publish]**，选择配置，然后单击&#x200B;**[!UICONTROL Publish]**。 这会将配置复制到相应的发布环境。

1. 在开发人员实例、暂存实例和生产实例（以剩下的实例为准）上重复上述所有步骤以使用 [!DNL AEM Forms] 为环境配置 [!DNL DocuSign]。

现在，您的AEM Forms环境配置为使用DocuSign。 确保将用于 Cloud Service 的配置容器添加到为 [!DNL DocuSign] 启用的所有自适应表单。您可以从自适应表单的属性中指定配置容器。

### 在自适应表单中使用[!DNL DocuSign] {#enabledocusign}

您可以为现有的自适应表单启用[!DNL DocuSign]或创建启用[!DNL DocuSign]的自适应表单。 选择下列选项之一：

- [创建启用 [!DNL DocuSign] 的自适应表单](#create-an-adaptive-form-for-docusign)
- 为现有的自适应表单](#editafsign)启用[启用 [!DNL DocuSign] 。

#### 创建DocuSign自适应表单 {#create-an-adaptive-form-for-docusign}

要创建启用签名的自适应表单，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;并选择&#x200B;**[!UICONTROL 自适应表单]**。 此时将显示模板列表。 选择模板并选择&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中：

   1. 为自适应表单指定&#x200B;**[!UICONTROL 名称]**&#x200B;和&#x200B;**[!UICONTROL 标题]**。

   1. 选择在[集成 [!DNL DocuSign] 与 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)时创建的[配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)。

   配置容器包含为您的环境配置的[!DNL DocuSign]Cloud Service。 这些服务可在自适应表单编辑器中选择。

1. 在&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡中，选择以下选项之一：

   - 如果您有自定义表单模板，并且需要基于表单模板的记录文档，请选择&#x200B;**[!UICONTROL 关联表单模板作为记录文档模板]**&#x200B;选项，然后选择记录文档模板。 使用选项时，发送以供签名的文档仅显示基于关联表单模板的字段。 它不会显示自适应表单的所有字段。

   - 如果没有自定义表单模板，请选择&#x200B;**[!UICONTROL 生成记录文档]**&#x200B;选项。 使用选项时，发送以供签名的文档显示自适应表单的所有字段。

1. 选择&#x200B;**[!UICONTROL 创建。]**&#x200B;已创建启用签名的自适应表单。 您可以将[!DNL DocuSign]字段添加到表单并发送以供签名。
1. 在编辑模式下打开自适应表单。 在&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL 表单容器]**，然后选择![配置](assets/configure-icon.svg)。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;部分中，从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 使用DocuSign电子签名提交]**。

1. 在&#x200B;**[!UICONTROL 操作配置]**&#x200B;部分中，选择&#x200B;**[!UICONTROL 添加]**&#x200B;以添加收件人并指定收件人的电子邮件地址。 再次选择&#x200B;**[!UICONTROL 添加]**&#x200B;以添加更多收件人。

1. 在&#x200B;**[!UICONTROL 电子邮件主题]**&#x200B;字段中指定电子邮件的主题。 选择&#x200B;**包含附件**&#x200B;以在电子邮件中包含附件。

1. 选择![保存](assets/save_icon.svg)以保存属性。

#### 为自适应表单启用[!DNL DocuSign] {#editafsign}

要在现有自适应表单中使用[!DNL DocuSign]，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择自适应表单并选择&#x200B;**[!UICONTROL 属性]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中，选择将[!DNL DocuSign]与[!DNL AEM Forms]集成时创建的[配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)。
1. 在&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡中，选择以下选项之一：

   - 如果您有自定义表单模板，并且需要基于表单模板的记录文档，请选择&#x200B;**[!UICONTROL 关联表单模板作为记录文档模板]**&#x200B;选项，然后选择记录文档模板。 使用选项时，发送以供签名的文档仅显示基于关联表单模板的字段。 它不会显示自适应表单的所有字段。

   - 如果没有自定义表单模板，请选择&#x200B;**[!UICONTROL 生成记录文档]**&#x200B;选项。 使用选项时，发送以供签名的文档显示自适应表单的所有字段。

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**。 已为[!DNL DocuSign]启用自适应表单。 现在，您可以将[!DNL DocuSign]字段添加到表单并发送以供签名。

1. 在编辑模式下打开自适应表单。 在&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL 表单容器]**，然后选择![配置](assets/configure-icon.svg)。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;部分中，从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 使用DocuSign电子签名提交]**。

1. 在&#x200B;**[!UICONTROL 操作配置]**&#x200B;部分中，选择&#x200B;**[!UICONTROL 添加]**&#x200B;以添加收件人并指定收件人的电子邮件地址。 再次选择&#x200B;**[!UICONTROL 添加]**&#x200B;以添加更多收件人。

1. 在&#x200B;**[!UICONTROL 电子邮件主题]**&#x200B;字段中指定电子邮件的主题。 选择&#x200B;**包含附件**&#x200B;以在电子邮件中包含附件。

1. 选择![保存](assets/save_icon.svg)以保存属性。
