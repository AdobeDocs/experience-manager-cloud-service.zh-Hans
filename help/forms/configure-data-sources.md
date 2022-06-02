---
title: 如何配置数据源？
description: Experience Manager Forms数据集成允许您配置不同的数据源并将其连接到不同的数据源。 了解如何将RESTful Web服务、基于SOAP的Web服务和OData服务配置为数据源，并使用它们创建表单数据模型。
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: 983f1b815fd213863ddbcd83ac7e3f076c57d761
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 5%

---

# 配置数据源 {#configure-data-sources}

![数据集成](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 数据集成允许您配置不同的数据源并将其连接到不同的数据源。 支持开箱即用的以下类型：

<!-- * Relational databases - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2], and [!DNL Oracle RDBMS] 
* [!DNL Experience Manager] user profile  -->
* RESTful Web服务
* 基于SOAP的Web服务
* OData服务（版本4.0）
* Microsoft Dynamics
* SalesForce
* Microsoft Azure Blob Storage

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

中的所有云服务配置 [!DNL Experience Manager] 在 `/conf` 文件夹 [!DNL Experience Manager] 存储库。 默认情况下， `conf` 文件夹包含 `global` 您可以在其中创建云服务配置的文件夹。 但是，您必须为云配置手动启用它。 您还可以在 `conf` 创建和组织云服务配置。

要为云服务配置配置文件夹，请执行以下操作：

1. 转到 **[!UICONTROL 工具>常规>配置浏览器]**.
   * 请参阅 [配置浏览器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) 文档以了解更多信息。
1. 执行以下操作可为云配置启用全局文件夹，或跳过此步骤以为云服务配置创建和配置其他文件夹。

   1. 在 **[!UICONTROL 配置浏览器]**，选择 `global` 文件夹，然后点按 **[!UICONTROL 属性]**.

   1. 在 **[!UICONTROL 配置属性]** 对话框，启用 **[!UICONTROL 云配置]**.

   1. 点按 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

1. 在 **[!UICONTROL 配置浏览器]**，点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框中，为文件夹指定标题并启用 **[!UICONTROL 云配置]**.
1. 点按 **[!UICONTROL 创建]** 创建云服务配置启用的文件夹。

## 配置RESTful Web服务 {#configure-restful-web-services}

RESTful Web服务可使用 [Swagger规范](https://swagger.io/specification/v2/) JSON或YAML格式 [!DNL Swagger] 定义文件。 要在 [!DNL Experience Manager] as a Cloud Service，确保您 [!DNL Swagger] 文件([Swagger版本2.0](https://swagger.io/specification/v2/))或托管文件的URL上。

请执行以下操作以配置RESTful服务：

1. 转到 **[!UICONTROL 工具>Cloud Services>数据源]**. 点按以选择要在其中创建云配置的文件夹。

   请参阅 [为云服务配置配置文件夹](configure-data-sources.md#cloud-folder) 有关为云服务配置创建和配置文件夹的信息。

1. 点按 **[!UICONTROL 创建]** 打开 **[!UICONTROL 创建数据源配置向导]**. 为配置指定名称和（可选）标题，选择 **[!UICONTROL RESTful服务]** 从 **[!UICONTROL 服务类型]** （可选）浏览并选择配置的缩略图，然后点按 **[!UICONTROL 下一个]**.
1. 为RESTful服务指定以下详细信息：

   * 从 [!UICONTROL Swagger源] 下拉列表，并相应地指定 [!DNL Swagger URL] 到[!DNL  Swagger] 定义文件或上传 [!DNL Swagger] 文件。
   * 基于[!DNL  Swagger] 源输入中，以下字段预填充了值：

      * 方案：REST API使用的传输协议。 下拉列表中显示的方案类型数取决于 [!DNL Swagger] 来源。
      * 主机：提供REST API的主机的域名或IP地址。 它是必填字段。
      * 基本路径：所有API路径的URL前缀。 它是一个可选字段。\
         如有必要，请编辑这些字段的预填充值。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证、API密钥或自定义身份验证）以访问RESTful服务，并相应地提供身份验证详细信息。

   如果您选择 **[!UICONTROL API密钥]** 对于身份验证类型，指定API密钥的值。 API密钥可以作为请求标头或查询参数发送。 从 **[!UICONTROL 位置]** 下拉列表中，并在 **[!UICONTROL 参数名称]** 字段中，将会显示相应的内容。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 点按 **[!UICONTROL 创建]** 为RESTful服务创建云配置。

### 形成数据模型HTTP客户端配置以优化性能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 由于数据源包含用于性能优化的HTTP客户端配置，因此在与RESTful Web服务集成时会生成数据模型。

设置 **[!UICONTROL REST数据源的表单数据模型HTTP客户端配置]** 指定正则表达式的配置：

* 使用 `http.connection.max.per.route` 属性来设置表单数据模型与RESTful Web服务之间允许的最大连接数。 默认值为20个连接。

* 使用 `http.connection.max` 属性，以指定每个路由允许的连接的最大数。 默认值为40个连接。

* 使用 `http.connection.keep.alive.duration` 属性来指定持续时间，持久HTTP连接将保持活动状态。 默认值为15秒。

* 使用 `http.connection.timeout` 属性以指定持续时间，其 [!DNL Experience Manager Forms] 服务器等待连接建立。 默认值为10秒。

* 使用 `http.socket.timeout` 属性，以指定两个数据包之间不活动的最长时间段。 默认值为30秒。

以下JSON文件显示一个示例：

```json
{   
   "http.connection.keep.alive.duration":"15",   
   "http.connection.max.per.route":"20",   
   "http.connection.timeout":"10",   
   "http.socket.timeout":"30",   
   "http.connection.idle.connection.timeout":"15",   
   "http.connection.max":"40" 
} 
```

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)。


执行以下步骤以配置表单数据模型HTTP客户端：

1. 登录到 [!DNL Experience Manager Forms] 以管理员身份创作实例，然后转到 [!DNL Experience Manager] web控制台包。 默认URL为 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. 点按 **[!UICONTROL REST数据源的表单数据模型HTTP客户端配置]**.

1. 在 [!UICONTROL REST数据源的表单数据模型HTTP客户端配置] 对话框：

   * 指定表单数据模型与RESTful Web服务之间允许的最大连接数 **[!UICONTROL 总连接限制]** 字段。 默认值为20个连接。

   * 指定中每个路由允许的最大连接数 **[!UICONTROL 每条路由的连接限制]** 字段。 默认值为2个连接。

   * 在 **[!UICONTROL 保持活力]** 字段。 默认值为15秒。

   * 指定持续时间，持续时间 [!DNL Experience Manager Forms] 服务器等待连接建立，在 **[!UICONTROL 连接超时]** 字段。 默认值为10秒。

   * 指定 **[!UICONTROL 套接字超时]** 字段。 默认值为30秒。

## 配置SOAP Web服务 {#configure-soap-web-services}

使用 [Web服务描述语言(WSDL)规范](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] 不支持RPC样式WSDL模型。

要在 [!DNL Experience Manager] as a Cloud Service的是，确保您具有Web服务的WSDL URL，并执行以下操作：

1. 转到 **[!UICONTROL 工具>Cloud Services>数据源]**. 点按以选择要在其中创建云配置的文件夹。

   请参阅 [为云服务配置配置文件夹](configure-data-sources.md#cloud-folder) 有关为云服务配置创建和配置文件夹的信息。

1. 点按 **[!UICONTROL 创建]** 打开 **[!UICONTROL 创建数据源配置向导]**. 为配置指定名称和（可选）标题，选择 **[!UICONTROL SOAP Web服务]** 从 **[!UICONTROL 服务类型]** （可选）浏览并选择配置的缩略图，然后点按 **[!UICONTROL 下一个]**.
1. 为SOAP Web服务指定以下内容：

   * Web服务的WSDL URL。
   * 服务端点. 在此字段中指定一个值，以覆盖WSDL中提到的服务端点。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证或自定义身份验证）以访问SOAP服务，并相应地提供身份验证的详细信息。

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 点按 **[!UICONTROL 创建]** 为SOAP web服务创建云配置。

### 允许在SOAP Web服务WSDL中使用import语句 {#enable-import-statements}

可以指定一个正则表达式作为绝对URL的过滤器，该绝对URL允许作为SOAP Web服务WSDL中的导入语句。 默认情况下，此字段中没有值。 因此， [!DNL Experience Manager] 会阻止WSDL中可用的所有import语句。 如果您指定 `.*` 作为此字段中的值， [!DNL Experience Manager] 允许所有import语句。

设置 `importAllowlistPattern` 属性 **[!UICONTROL 表单数据模型SOAP Web服务导入允许列表]** 用于指定正则表达式的配置。 以下JSON文件显示一个示例：

```json
{
  "importAllowlistPattern": ".*"
}
```

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)。

## 配置OData服务 {#config-odata}

OData服务由其服务根URL标识。 在 [!DNL Experience Manager] as a Cloud Service的是，确保您具有服务的服务根URL，并执行以下操作：

>[!NOTE]
>
> 表单数据模型支持 [OData版本4](https://www.odata.org/documentation/).
>有关配置的分步指南 [!DNL Microsoft Dynamics 365]，请参阅 [[!DNL Microsoft Dynamics] OData配置](ms-dynamics-odata-configuration.md).

1. 转到 **[!UICONTROL 工具>Cloud Services>数据源]**. 点按以选择要在其中创建云配置的文件夹。

   请参阅 [为云服务配置配置文件夹](#cloud-folder) 有关为云服务配置创建和配置文件夹的信息。

1. 点按 **[!UICONTROL 创建]** 打开 **[!UICONTROL 创建数据源配置向导]**. 为配置指定名称和（可选）标题，选择 **[!UICONTROL OData服务]** 从 **[!UICONTROL 服务类型]** （可选）浏览并选择配置的缩略图，然后点按 **[!UICONTROL 下一个]**.
1. 为OData服务指定以下详细信息：

   * 要配置的OData服务的服务根URL。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证、API密钥或自定义身份验证）以访问OData服务，并相应地提供身份验证的详细信息。

   如果您选择 **[!UICONTROL API密钥]** 对于身份验证类型，指定API密钥的值。 API密钥可以作为请求标头或查询参数发送。 从 **[!UICONTROL 位置]** 下拉列表中，并在 **[!UICONTROL 参数名称]** 字段中，将会显示相应的内容。

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
