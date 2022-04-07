---
title: How to Configure Data Sources?
description: Experience Manager Forms Data Integration allows you to configure and connect to disparate data sources. Learn how to configure RESTful web services, SOAP-based web services, and OData services as data sources and use them to create form data models.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: b6c654f5456e1a7778b453837f04cbed32a82a77
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 3%

---

# 配置数据源 {#configure-data-sources}

![数据集成](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 数据集成允许您配置不同的数据源并将其连接到不同的数据源。 The following types are supported out-of-the-box. 但是，通过少量自定义，您也可以集成其他数据源。

<!-- * Relational databases - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2], and [!DNL Oracle RDBMS] 
* [!DNL Experience Manager] user profile  -->
* RESTful Web服务
* 基于SOAP的Web服务
* OData服务

数据集成支持开箱即用的OAuth2.0、基本身份验证和API密钥身份验证类型，并允许实施自定义身份验证以访问Web服务。 而RESTful、基于SOAP和OData服务在 [!DNL Experience Manager] as a Cloud Service <!--, JDBC for relational databases --> 和连接器 [!DNL Experience Manager] 用户配置文件配置在 [!DNL Experience Manager] web控制台。

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] 不支持关系数据库。

<!-- ## Configure relational database {#configure-relational-database}

You can configure relational databases using [!DNL Experience Manager] Web Console Configuration. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://server:host/system/console/configMgr`.
1. Look for **[!UICONTROL Apache Sling Connection Pooled DataSource]** configuration. Tap to open the configuration in edit mode.
1. In the configuration dialog, specify the details for the database you want to configure, such as:

    * Name of the data source
    * Data source service property that stores the data source name
    * Java class name for the JDBC driver
    * JDBC connection URI
    * Username and password to establish connection with the JDBC driver

   >[!NOTE]
   >
   >Ensure that you encrypt sensitive information like passwords before configuring the data source. To encrypt:
   >
   >    
   >    
   >    1. Go to https://'[server]:[port]'/system/console/crypto.
   >    1. In the **[!UICONTROL Plain Text]** field, specify the password or any string to encrypt and tap **[!UICONTROL Protect]**.
   >    
   >    
   >    
   >The encrypted text appears in the Protected Text field that you can specify in the configuration.

1. Enable **[!UICONTROL Test on Borrow]** or **[!UICONTROL Test on Return]** to specify that the objects are validated before being borrowed or returned from and to the pool, respectively.
1. Specify a SQL SELECT query in the **[!UICONTROL Validation Query]** field to validate connections from the pool. The query must return at least one row. Based on your database, specify one of the following:

    * SELECT 1 (MySQL and MS SQL) 
    * SELECT 1 from dual (Oracle)

1. Tap **[!UICONTROL Save]** to save the configuration. -->

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties will be available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Tap **[!UICONTROL Save]** to save the configuration. -->

## 为云服务配置配置文件夹 {#cloud-folder}

为RESTful、SOAP和OData服务配置云服务时，需要配置云服务文件夹。

中的所有云服务配置 [!DNL Experience Manager] 在 `/conf` 文件夹 [!DNL Experience Manager] 存储库。 By default, the `conf` folder contains the `global` folder where you can create cloud service configurations. 但是，您必须为云配置手动启用它。 您还可以在 `conf` 创建和组织云服务配置。

要为云服务配置配置文件夹，请执行以下操作：

1. 转到 **[!UICONTROL 工具>常规>配置浏览器]**.
   * 请参阅 [配置浏览器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) 文档以了解更多信息。
1. Do the following to enable the global folder for cloud configurations or skip this step to create and configure another folder for cloud service configurations.

   1. 在 **[!UICONTROL 配置浏览器]**，选择 `global` 文件夹，然后点按 **[!UICONTROL 属性]**.

   1. 在 **[!UICONTROL 配置属性]** 对话框，启用 **[!UICONTROL 云配置]**.

   1. 点按 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

1. 在 **[!UICONTROL 配置浏览器]**，点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框中，为文件夹指定标题并启用 **[!UICONTROL 云配置]**.
1. 点按 **[!UICONTROL 创建]** 创建云服务配置启用的文件夹。

## 配置RESTful Web服务 {#configure-restful-web-services}

RESTful Web服务可使用 [Swagger规范](https://swagger.io/specification/) JSON或YAML格式 [!DNL Swagger] 定义文件。 To configure RESTful web service in [!DNL Experience Manager] as a Cloud Service, ensure that you have either the [!DNL Swagger] file on your file system or the URL where the file is hosted.

请执行以下操作以配置RESTful服务：

1. Go to **[!UICONTROL Tools > Cloud Services > Data Sources]**. 点按以选择要在其中创建云配置的文件夹。

   请参阅 [为云服务配置配置文件夹](configure-data-sources.md#cloud-folder) 有关为云服务配置创建和配置文件夹的信息。

1. 点按 **[!UICONTROL 创建]** 打开 **[!UICONTROL 创建数据源配置向导]**. 为配置指定名称和（可选）标题，选择 **[!UICONTROL RESTful服务]** 从 **[!UICONTROL 服务类型]** （可选）浏览并选择配置的缩略图，然后点按 **[!UICONTROL 下一个]**.
1. 为RESTful服务指定以下详细信息：

   * 从 [!UICONTROL Swagger源] 下拉列表，并相应地指定 [!DNL Swagger URL] 到[!DNL  Swagger] 定义文件或上传 [!DNL Swagger] 文件。
   * 基于[!DNL  Swagger] 源输入中，以下字段预填充了值：

      * 方案：REST API使用的传输协议。 The number of scheme types that display in the drop-down list depend on the schemes defined in the [!DNL Swagger] source.
      * Host: The domain name or IP address of the host that serves the REST API. 它是必填字段。
      * 基本路径：所有API路径的URL前缀。 它是一个可选字段。\
         If necessary, edit the pre-populated values for these fields.
   * 选择身份验证类型（无、OAuth2.0、基本身份验证、API密钥或自定义身份验证）以访问RESTful服务，并相应地提供身份验证详细信息。

   如果您选择 **[!UICONTROL API密钥]** 对于身份验证类型，指定API密钥的值。 API密钥可以作为请求标头或查询参数发送。 Select one of these options from the **[!UICONTROL Location]** drop-down list and specify the name of the header or the query parameter in the **[!UICONTROL Parameter Name]** field accordingly.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Tap **[!UICONTROL Create]** to create the cloud configuration for the RESTful service.

### 形成数据模型HTTP客户端配置以优化性能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 由于数据源包含用于性能优化的HTTP客户端配置，因此在与RESTful Web服务集成时会生成数据模型。
Perform the following steps to configure the form data model HTTP client:

1. 登录到 [!DNL Experience Manager Forms] 以管理员身份创作实例，然后转到 [!DNL Experience Manager] web控制台包。 默认URL为 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. 点按 **[!UICONTROL REST数据源的表单数据模型HTTP客户端配置]**.

1. 在 [!UICONTROL REST数据源的表单数据模型HTTP客户端配置] 对话框：

   * 指定表单数据模型与RESTful Web服务之间允许的最大连接数 **[!UICONTROL 总连接限制]** 字段。 默认值为20个连接。

   * Specify the maximum number of permitted connections for each route in the **[!UICONTROL Connection limit on per route basis]** field. 默认值为2个连接。

   * Specify the duration, for which a persistent HTTP connection is kept alive, in the **[!UICONTROL Keep alive]** field. 默认值为15秒。

   * 指定持续时间，持续时间 [!DNL Experience Manager Forms] 服务器等待连接建立，在 **[!UICONTROL 连接超时]** 字段。 The default value is 10 seconds.

   * 指定 **[!UICONTROL 套接字超时]** 字段。 默认值为30秒。


## 配置SOAP Web服务 {#configure-soap-web-services}

使用 [Web服务描述语言(WSDL)规范](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] 不支持RPC样式WSDL模型。

要在 [!DNL Experience Manager] as a Cloud Service的是，确保您具有Web服务的WSDL URL，并执行以下操作：

1. 转到 **[!UICONTROL 工具>Cloud Services>数据源]**. 点按以选择要在其中创建云配置的文件夹。

   See [Configure folder for cloud service configurations](configure-data-sources.md#cloud-folder) for information about creating and configuring a folder for cloud service configurations.

1. Tap **[!UICONTROL Create]** to open the **[!UICONTROL Create Data Source Configuration wizard]**. 为配置指定名称和（可选）标题，选择 **[!UICONTROL SOAP Web服务]** 从 **[!UICONTROL 服务类型]** （可选）浏览并选择配置的缩略图，然后点按 **[!UICONTROL 下一个]**.
1. 为SOAP Web服务指定以下内容：

   * WSDL URL for the web service.
   * 服务端点. 在此字段中指定一个值，以覆盖WSDL中提到的服务端点。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证或自定义身份验证）以访问SOAP服务，并相应地提供身份验证的详细信息。

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 点按 **[!UICONTROL 创建]** 为SOAP web服务创建云配置。

### 允许在SOAP Web服务WSDL中使用import语句 {#enable-import-statements}

可以指定一个正则表达式作为绝对URL的过滤器，该绝对URL允许作为SOAP Web服务WSDL中的导入语句。 默认情况下，此字段中没有值。 因此， [!DNL Experience Manager] 会阻止WSDL中可用的所有import语句。 如果您指定 `.*` 作为此字段中的值， [!DNL Experience Manager] 允许所有import语句。

Set the `importAllowlistPattern` property of the **[!UICONTROL Form Data Model SOAP Web Services Import Allowlist]** configuration to specify the regular expression. 以下JSON文件显示一个示例：

```json
{
  "importAllowlistPattern": ".*"
}
```

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)。

## 配置OData服务 {#config-odata}

An OData service is identified by its service root URL. 在 [!DNL Experience Manager] as a Cloud Service的是，确保您具有服务的服务根URL，并执行以下操作：

>[!NOTE]
>
> 表单数据模型支持 [OData版本4](https://www.odata.org/documentation/).
>有关配置的分步指南 [!DNL Microsoft Dynamics 365]，请参阅 [[!DNL Microsoft Dynamics] OData配置](ms-dynamics-odata-configuration.md).

1. 转到 **[!UICONTROL 工具>Cloud Services>数据源]**. 点按以选择要在其中创建云配置的文件夹。

   See [Configure folder for cloud service configurations](#cloud-folder) for information about creating and configuring a folder for cloud service configurations.

1. 点按 **[!UICONTROL 创建]** 打开 **[!UICONTROL 创建数据源配置向导]**. 为配置指定名称和（可选）标题，选择 **[!UICONTROL OData服务]** 从 **[!UICONTROL 服务类型]** （可选）浏览并选择配置的缩略图，然后点按 **[!UICONTROL 下一个]**.
1. 为OData服务指定以下详细信息：

   * Service Root URL for the OData service to be configured.
   * Select the authentication type — None, OAuth2.0, Basic Authentication, API Key, or Custom Authentication — to access the OData service, and accordingly provide the details for authentication.

   If you select **[!UICONTROL API Key]** as the authentication type, specify the value for the API key. The API key can be sent as a request header or as a query parameter. 从 **[!UICONTROL 位置]** 下拉列表中，并在 **[!UICONTROL 参数名称]** 字段中，将会显示相应的内容。

   >[!NOTE]
   >
   >您必须选择OAuth 2.0身份验证类型才能连接 [!DNL Microsoft Dynamics] 使用OData端点作为服务根的服务。

1. 点按 **[!UICONTROL 创建]** 为OData服务创建云配置。

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other’s identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## 下面的步骤 {#next-steps}

您已配置数据源。 接下来，您可以创建表单数据模型，或者如果已经创建了没有数据源的表单数据模型，则可以将其与您刚刚配置的数据源相关联。 请参阅 [创建表单数据模型](create-form-data-models.md) 以了解详细信息。
