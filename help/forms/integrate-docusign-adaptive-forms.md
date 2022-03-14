---
title: 将DocuSign与自适应表单集成
description: 了解如何将DocuSign与自适应表单结合使用来收集电子签名。
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 8%

---

# 将DocuSign与自适应表单结合使用 {#integrate-aem-forms-with-DocuSign}

DocuSign是一个著名的电子签名解决方案。 您可以使用它在电子邮件中签署协议。 您可以将DocuSign与自适应表单相集成。 它可帮助您向多个收件人发送电子签名的自适应表单。 使用电子签名可帮助您：

- 通过完全自动化的建议书、报价和合同流程，与任何设备达成交易。
- 更快地完成人力资源流程，并为员工提供数字体验。
- 缩短合同周期并更快地载入您的供应商。

AEM Formsas a Cloud Service提供 [DocuSign的自定义提交操作](#deploy-custom-submit-action). 提交操作可帮助您使用DocuSign API发送电子签名的自适应表单。

| 您还可以使用Adobe的电子签名解决方案Adobe Sign对自适应表单进行电子签名。 AEM Forms与Adobe Sign的集成要深得多，提供了更精细的控制，如顺序和并行签名、多种身份验证方法、表单签名体验等。 有关更多信息，请参阅 [在自适应表单中使用Adobe Sign](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## 前提条件 {#prerequisites}

要将DocuSign与AEM Forms集成，需要满足以下条件：

- DocuSign [开发人员帐户](https://developers.docusign.com/platform/account/)
- DocuSign应用程序
- DocuSign API应用程序的凭据（客户端ID和客户端密钥）。
- [DocuSign的自定义提交操作和云服务](https://github.com/adobe/aem-forms-docusign-sample)
- （仅用于本地开发环境） [设置记录文档](setup-local-development-environment.md#docker-microservices).

## 为DocuSign配置自定义提交操作和云服务 {#deploy-custom-submit-action}

AEM Formsas a Cloud Service为DocuSign提供自定义提交操作。 提交操作可帮助您使用DocuSign API发送电子签名的自适应表单。 自定义提交操作的代码在 [AEM Forms示例公共git存储库](https://github.com/adobe/aem-forms-docusign-sample). 您可以在AEM Forms环境中部署该代码，也可以根据组织的要求对其进行自定义。

执行以下步骤以配置即装即用的自定义提交操作和DocuSignCloud Service:

1. [克隆AEM Formsas a Cloud Service项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment) 或创建 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 项目基于 [AEM原型27](https://github.com/adobe/aem-project-archetype) 或更晚。 创建 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 基于AEM原型的项目：
   </br> 打开命令提示符并运行以下命令以创建 [!DNL Experience Manager Forms] as a Cloud Service项目：

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   此外，更改 `appTitle`, `appId`和 `groupId`，以反映您的环境。

1. 克隆 [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) 存储库。 此存储库包含DocuSign的自定义提交操作以及与DocuSign服务器连接的配置详细信息。

1. 打开在步骤1中创建的AEM Formsas a Cloud Service项目，以在您选择的IDE中进行编辑。

1. 打开 `[AEM Forms as a Cloud Service project]\pom.xml` 文件进行编辑，并进行以下更改：

   1. 在 `<properties>` 标记：

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. 在 `<repositories>` 标记：

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      如果没有 `<repositories>` 标记，请在 `<properties>` 标记。

   1. 在 `<dependencyManagement>` 标记：

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. 在 `all/pom.xml` 文件在Cloud Service项目文件夹中可用：

   1. 在 `<embeddeds>` 标记：

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. 在 `<dependencies>` 标记：

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. 打开命令提示符，然后导航到 `aem-forms-samples\forms-integration-docusign` （在步骤3中克隆）并运行以下命令：

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` 是指在此过程的步骤1中创建的文件夹的名称。

1. 将项目部署到本地开发环境。 您可以使用以下命令部署到本地开发环境

   `mvn -PautoInstallPackage clean install`

   执行这些步骤后，您可以查看新的自定义提交操作 [使用DocuSign电子签名提交](#enabledocusign) 自适应表单和 [DocuSign云服务配置](#configure-docusign-with-aem-forms) 在本地开发环境中。

1. 编译和 [将代码部署到 [!DNL AEM Forms] as a Cloud Service环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## 集成 [!DNL DocuSign] with [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

在满足先决条件后，执行以下步骤以集成 [!DNL DocuSign] with [!DNL AEM Forms] 在创作实例上。

1. 导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** 并选择用于托管配置的文件夹。

1. 在配置页面上，点按 **[!UICONTROL 创建]** 创建 [!DNL DocuSign] 配置AEM Forms。
1. 在 **[!UICONTROL 常规]** 选项卡 **[!UICONTROL 创建DocuSign配置]** 页面，指定 **[!UICONTROL 名称]** 对于配置，请点按 **[!UICONTROL 下一个]**. 您可以选择指定 **[!UICONTROL 标题]**.

1. 将当前浏览器窗口中的 URL 复制到记事本。在下一个步骤中使用 [!DNL AEM Forms] 配置 [!DNL DocuSign] 应用程序时需要此 URL。

1. 配置 [!DNL DocuSign] 应用程序的 OAuth 设置：

   1. 打开浏览器窗口并登录到 [!DNL DocuSign] [开发人员帐户](https://admindemo.docusign.com/apps-and-keys).
   1. 打开为 [!DNL AEM Forms].
   1. 在 **[!UICONTROL 重定向URI]** 框中，添加在上一步中复制的URL并单击 **[!UICONTROL 保存]**.
   1. 记下集成密钥和密钥。

   有关为 [!DNL DocuSign] 应用程序配置 OAuth 设置并获取密钥的分步信息，请参阅[为应用程序配置 OAuth 设置](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys)开发人员文档。

1. 返回到 **[!UICONTROL 创建DocuSign配置]** 页面。 在 **[!UICONTROL 设置]** 选项卡 **[!UICONTROL OAuth URL]** 字段会提及以下默认URL:

   `https://account-d.docusign.com/oauth/auth`

1. 指定 **[!UICONTROL 客户端ID]** （DocuSign集成密钥）和 **[!UICONTROL 客户端密钥]** （DocuSign密钥）。

1. 点按 **[!UICONTROL 连接到DocuSign]**. 在系统提示输入凭据时，提供在创建 [!DNL DocuSign] 应用程序时所用帐户的用户名和密码。当要求确认访问 `your developer account`，单击 **[!UICONTROL 允许访问]**. 如果凭据正确，则会显示成功消息。

1. 点按 **[!UICONTROL 创建]** 创建 [!DNL DocuSign] 配置。

1. 选择配置并单击 **[!UICONTROL 发布]**，选择配置，然后单击 **[!UICONTROL 发布]**. 这会将配置复制到相应的发布环境。

1. 在开发人员实例、暂存实例和生产实例（以剩下的实例为准）上重复上述所有步骤以使用 [!DNL AEM Forms] 为环境配置 [!DNL DocuSign]。

现在，您的AEM Forms环境已配置为使用DocuSign。 确保将用于 Cloud Service 的配置容器添加到为 [!DNL DocuSign] 启用的所有自适应表单。您可以在自适应表单的属性中指定配置容器。

### 使用 [!DNL DocuSign] 在自适应表单中 {#enabledocusign}

您可以启用 [!DNL DocuSign] 或创建 [!DNL DocuSign] 启用了自适应表单。 选择以下选项之一：

- [创建 [!DNL DocuSign] 启用自适应表单](#create-an-adaptive-form-for-docusign)
- [启用 [!DNL DocuSign] （对于现有自适应表单）](#editafsign).

#### 为DocuSign创建自适应表单 {#create-an-adaptive-form-for-docusign}

要创建启用符号的自适应表单，请执行以下操作：

1. 导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 点按 **[!UICONTROL 创建]** 选择 **[!UICONTROL 自适应表单]**. 此时将显示模板列表。 选择模板并点按 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL 基本]** 选项卡：

   1. 指定 **[!UICONTROL 名称]** 和 **[!UICONTROL 标题]** （在自适应表单中）。

   1. 选择 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 创建时间 [集成 [!DNL DocuSign] with [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   配置容器包含 [!DNL DocuSign] Cloud Services。 这些服务可在自适应表单编辑器中进行选择。

1. 在 **[!UICONTROL 表单模型]** 选项卡，选择以下选项之一：

   - 如果您有自定义表单模板，并且需要基于表单模板的记录文档，请选择 **[!UICONTROL 将表单模板关联为记录文档模板]** 选项，然后选择记录文档模板。 使用选项时，发送进行签名的文档将仅显示基于关联表单模板的那些字段。 它不会显示自适应表单的所有字段。

   - 如果没有自定义表单模板，请选择 **[!UICONTROL 生成记录文档]** 选项。 使用选项时，发送以供签名的文档将显示自适应表单的所有字段。

1. 点按&#x200B;**[!UICONTROL 创建。]** 将创建启用符号的自适应表单。 您可以将 [!DNL DocuSign] 字段并将其发送以进行签名。
1. 在编辑模式下打开自适应表单。 在 **[!UICONTROL 内容]** ，点按 **[!UICONTROL 表单容器]** 点按 ![配置](assets/configure-icon.svg).

1. 在 **[!UICONTROL 提交]** 选择 **[!UICONTROL 使用DocuSign电子签名提交]** 从 **[!UICONTROL 提交操作]** 下拉列表。

1. 在 **[!UICONTROL 操作配置]** 部分，点按 **[!UICONTROL 添加]** 添加收件人并指定收件人的电子邮件地址。 点按 **[!UICONTROL 添加]** 再次添加更多收件人。

1. 在 **[!UICONTROL 电子邮件主题]** 字段。 选择 **包含附件** 以在电子邮件中包含附件。

1. 点按 ![保存](assets/save_icon.svg) 以保存属性。

#### 启用 [!DNL DocuSign] 自适应表单 {#editafsign}

使用 [!DNL DocuSign] 在现有自适应表单中：

1. 导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择自适应表单并点按 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 基本]** 选项卡，选择 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 集成时创建 [!DNL DocuSign] with [!DNL AEM Forms].
1. 在 **[!UICONTROL 表单模型]** 选项卡，选择以下选项之一：

   - 如果您有自定义表单模板，并且需要基于表单模板的记录文档，请选择 **[!UICONTROL 将表单模板关联为记录文档模板]** 选项，然后选择记录文档模板。 使用选项时，发送进行签名的文档将仅显示基于关联表单模板的那些字段。 它不会显示自适应表单的所有字段。

   - 如果没有自定义表单模板，请选择 **[!UICONTROL 生成记录文档]** 选项。 使用选项时，发送以供签名的文档将显示自适应表单的所有字段。

1. 点按 **[!UICONTROL 保存并关闭]**. 自适应表单已启用 [!DNL DocuSign]. 现在，您可以将 [!DNL DocuSign] 字段并将其发送以进行签名。

1. 在编辑模式下打开自适应表单。 在 **[!UICONTROL 内容]** ，点按 **[!UICONTROL 表单容器]** 点按 ![配置](assets/configure-icon.svg).

1. 在 **[!UICONTROL 提交]** 选择 **[!UICONTROL 使用DocuSign电子签名提交]** 从 **[!UICONTROL 提交操作]** 下拉列表。

1. 在 **[!UICONTROL 操作配置]** 部分，点按 **[!UICONTROL 添加]** 添加收件人并指定收件人的电子邮件地址。 点按 **[!UICONTROL 添加]** 再次添加更多收件人。

1. 在 **[!UICONTROL 电子邮件主题]** 字段。 选择 **包含附件** 以在电子邮件中包含附件。

1. 点按 ![保存](assets/save_icon.svg) 以保存属性。
