---
title: 如何配置数据源？
description: 了解如何将RESTful Web服务、基于SOAP的Web服务和OData服务配置为表单数据模型的数据源。
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: b9fb484135fb2d16758548c525b59f5ba011afb5
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 4%

---


# 配置数据源 {#configure-data-sources}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/configure-data-sources.html) |
| AEM as a Cloud Service | 本文 |

![数据集成](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 通过数据集成，您可以配置并连接到不同的数据源。 支持开箱即用的以下类型：

* 关系数据库 — MySQL、 [!DNL Microsoft® SQL Server]， [!DNL IBM® DB2®]、 postgreSQL和 [!DNL Oracle RDBMS]
* RESTful Web服务
* 基于SOAP的Web服务
* OData服务（版本4.0）
* Microsoft® Dynamics
* SalesForce
* Microsoft® Azure Blob存储

数据集成支持OAuth2.0([授权码](https://oauth.net/2/grant-types/authorization-code/)， [客户端凭据](https://oauth.net/2/grant-types/client-credentials/))、基本身份验证和API密钥身份验证是现成的类型，允许实施自定义身份验证以访问Web服务。 在中配置RESTful、基于SOAP和OData服务的同时 [!DNL Experience Manager] as a Cloud Service，关系数据库的JDBC和连接器 [!DNL Experience Manager] 用户配置文件配置于 [!DNL Experience Manager] Web控制台。

## 配置关系数据库 {#configure-relational-database}

### 前提条件

在使用配置关系数据库之前 [!DNL Experience Manager] Web控制台配置，必须：
* [通过Cloud Manager API启用高级联网](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)，因为默认情况下端口处于禁用状态。
* [在Maven中添加JDBC驱动程序依赖项](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies).


### 配置关系数据库的步骤

可以使用配置关系数据库 [!DNL Experience Manager] Web控制台配置。 执行以下操作：

1. 转到 [!DNL Experience Manager] Web控制台位于 `https://server:host/system/console/configMgr`.
1. 定位 **[!UICONTROL Day Commons JDBC连接池]** 配置。 点按以在编辑模式下打开配置。

   ![JDBC连接器池](/help/forms/assets/jdbc_connector.png)

1. 在配置对话框中，指定要配置的数据库的详细信息，例如：

   * JDBC驱动程序的Java™类名称
   * JDBC连接URI
   * 用于与JDBC驱动程序建立连接的用户名和密码
   * 在中指定SQL SELECT查询 **[!UICONTROL 验证查询]** 用于验证池中的连接的字段。 查询必须至少返回一行。 根据您的数据库，指定以下选项之一：
      * SELECT 1 (MySQL和MS® SQL)
      * 从双选件中选择1(Oracle)
   * 数据源的名称

   用于配置关系数据库的示例字符串：

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > 请参阅 [使用JDBC数据源池的SQL连接](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) 以了解更多详细信息。

1. 点按 **[!UICONTROL 保存]** 以保存配置。

现在，您可以将配置的关系数据库与表单数据模型结合使用。

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties are available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Tap **[!UICONTROL Save]** to save the configuration. -->

## 为云服务配置配置文件夹 {#cloud-folder}

配置RESTful、SOAP和OData服务的云服务需要配置云服务文件夹。

中的所有云服务配置 [!DNL Experience Manager] 于综合全面收益表内 `/conf` 文件夹位置 [!DNL Experience Manager] 存储库。 默认情况下， `conf` 文件夹包含 `global` 文件夹，您可以在该文件夹中创建云服务配置。 但是，必须为云配置手动启用它。 您还可以创建其他文件夹，位于 `conf` 创建和组织云服务配置。

要为云服务配置配置文件夹，请执行以下操作：

1. 转到 **[!UICONTROL “工具”>“常规”>“配置浏览器”]**.
   * 请参阅 [配置浏览器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) 文档，以了解更多信息。
1. 执行以下操作可为云配置启用全局文件夹，或跳过此步骤为云服务配置创建和配置其他文件夹。

   1. 在 **[!UICONTROL 配置浏览器]**，选择 `global` 文件夹并点按 **[!UICONTROL 属性]**.

   1. 在 **[!UICONTROL 配置属性]** 对话框，启用 **[!UICONTROL 云配置]**.

   1. 点按 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

1. 在 **[!UICONTROL 配置浏览器]**，点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框，为文件夹指定标题，然后启用 **[!UICONTROL 云配置]**.
1. 点按 **[!UICONTROL 创建]** 以创建为云服务配置启用的文件夹。

## 配置RESTful Web服务 {#configure-restful-web-services}

可以使用对RESTful Web服务进行描述 [Swagger规范](https://swagger.io/specification/v2/) 格式为JSON或YAML，格式为 [!DNL Swagger] 定义文件。 在中配置RESTful Web服务 [!DNL Experience Manager] as a Cloud Service，确保您拥有 [!DNL Swagger] 文件([Swagger版本2.0](https://swagger.io/specification/v2/))或 [!DNL Swagger] 文件([Swagger版本3.0](https://swagger.io/specification/v3/))，或者托管文件的URL上。

### 为Open API规范版本2.0配置RESTful服务 {#configure-restful-services-open-api-2.0}

1. 转到&#x200B;**[!UICONTROL 工具 > Cloud Services > 数据源]**。点按以选择要创建云配置的文件夹。

   请参阅 [为云服务配置配置文件夹](configure-data-sources.md#cloud-folder) 有关为云服务配置创建和配置文件夹的信息。

1. 点按 **[!UICONTROL 创建]** 以打开 **[!UICONTROL 创建数据源配置向导]**. 指定配置的名称和（可选）标题，选择 **[!UICONTROL RESTful服务]** 从 **[!UICONTROL 服务类型]** 下拉列表（可选）浏览并选择配置的缩略图图像，然后点按 **[!UICONTROL 下一个]**.
1. 为RESTful服务指定以下详细信息：

   * 从中选择URL或文件 [!UICONTROL Swagger源] 下拉列表，并相应地指定 [!DNL Swagger URL] 到[!DNL  Swagger] 定义文件或上传 [!DNL Swagger] 从本地文件系统删除文件。
   * 基于[!DNL  Swagger] 源输入。，以下字段已预填充了值：

      * 方案：REST API使用的传输协议。 下拉列表中显示的方案类型数取决于中定义的方案 [!DNL Swagger] 源。
      * 主机：提供REST API的主机的域名或IP地址。 它是必填字段。
      * 基本路径：所有API路径的URL前缀。 它是一个可选字段。\
        如有必要，请编辑这些字段的预填充值。

   * 选择身份验证类型 — 无、OAuth2.0([授权码](https://oauth.net/2/grant-types/authorization-code/)， [客户端凭据](https://oauth.net/2/grant-types/client-credentials/))、基本身份验证、API密钥或自定义身份验证 — 用于访问RESTful服务，并相应地提供身份验证的详细信息。

   如果您选择 **[!UICONTROL API密钥]** 作为身份验证类型，指定API密钥的值。 API密钥可作为请求标头或查询参数发送。 从中选择以下选项之一 **[!UICONTROL 位置]** 下拉列表，并在中指定标头的名称或查询参数 **[!UICONTROL 参数名称]** 字段输入相应的。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 点按 **[!UICONTROL 创建]** 以创建RESTful服务的云配置。

### 为Open API规范版本3.0配置RESTful服务 {#configure-restful-services-open-api-3.0}

1. 转到&#x200B;**[!UICONTROL 工具 > Cloud Services > 数据源]**。点按以选择要创建云配置的文件夹。

   请参阅 [为云服务配置配置文件夹](configure-data-sources.md#cloud-folder) 有关为云服务配置创建和配置文件夹的信息。

1. 点按 **[!UICONTROL 创建]** 以打开 **[!UICONTROL 创建数据源配置向导]**. 指定配置的名称和（可选）标题，选择 **[!UICONTROL RESTful服务]** 从 **[!UICONTROL 服务类型]** 下拉列表（可选）浏览并选择配置的缩略图图像，然后点按 **[!UICONTROL 下一个]**.
1. 为RESTful服务指定以下详细信息：

   * 从中选择URL或文件 [!UICONTROL Swagger源] 下拉列表，并相应地指定 [!DNL Swagger 3.0 URL] 到[!DNL  Swagger] 定义文件或上传 [!DNL Swagger] 从本地文件系统删除文件。
   * 基于[!DNL  Swagger] 源输入，显示与目标服务器的连接信息。
   * 选择身份验证类型 — 无、OAuth2.0([授权码](https://oauth.net/2/grant-types/authorization-code/)， [客户端凭据](https://oauth.net/2/grant-types/client-credentials/))、基本身份验证、API密钥或自定义身份验证 — 用于访问RESTful服务，并相应地提供身份验证的详细信息。

   如果您选择 **[!UICONTROL API密钥]** 作为身份验证类型，指定API密钥的值。 API密钥可作为请求标头或查询参数发送。 从中选择以下选项之一 **[!UICONTROL 位置]** 下拉列表，并在中指定标头的名称或查询参数 **[!UICONTROL 参数名称]** 字段输入相应的。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 点按 **[!UICONTROL 创建]** 以创建RESTful服务的云配置。

RESTful服务Open API规范版本3.0不支持的一些操作包括：
* 回调
* oneof/anyof
* 远程引用
* 链接
* 针对单次操作的不同MIME类型的不同请求主体

请参阅 [OpenAPI 3.0规范](https://swagger.io/specification/v3/) 以了解详细信息。

### 表单数据模型HTTP客户端配置可优化性能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 在与RESTful Web服务集成时形成数据模型，因为数据源包括用于性能优化的HTTP客户端配置。

设置以下属性 **[!UICONTROL REST数据源的表单数据模型HTTP客户端配置]** 用于指定正则表达式的配置：

* 使用 `http.connection.max.per.route` 属性，用于设置表单数据模型和RESTful Web服务之间允许的最大连接数。 默认值为20个连接。

* 使用 `http.connection.max` 属性，指定每个路由允许的最大连接数。 默认值为40个连接。

* 使用 `http.connection.keep.alive.duration` 属性，指定持久HTTP连接保持活动状态的持续时间。 默认值为15秒。

* 使用 `http.connection.timeout` 属性，指定持续时间，其中 [!DNL Experience Manager Forms] 服务器等待建立连接。 默认值为10秒。

* 使用 `http.socket.timeout` 属性，指定两个数据包之间不活动的最长时间。 默认值为30秒。

以下JSON文件显示了一个示例：


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

1. 点按 **[!UICONTROL REST数据源的表单数据模型HTTP客户端配置]**.

1. 在 [!UICONTROL REST数据源的表单数据模型HTTP客户端配置] 对话框：

   * 在中指定表单数据模型和RESTful Web服务之间允许的最大连接数 **[!UICONTROL 连接限制总数]** 字段。 默认值为20个连接。

   * 指定中每个路由允许的最大连接数 **[!UICONTROL 每个路由的连接限制]** 字段。 缺省值为两个连接。

   * 指定持续HTTP连接保持活动状态的持续时间，在 **[!UICONTROL 保持活动状态]** 字段。 默认值为15秒。

   * 指定持续时间，持续时间为 [!DNL Experience Manager Forms] 服务器等待连接建立，在 **[!UICONTROL 连接超时]** 字段。 默认值为10秒。

   * 指定中两个数据包之间不活动的最长时间 **[!UICONTROL 套接字超时]** 字段。 默认值为30秒。

## 配置SOAP Web服务 {#configure-soap-web-services}

使用对基于SOAP的Web服务进行描述 [Web服务描述语言(WSDL)规范](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] 不支持RPC样式的WSDL模型。

在中配置基于SOAP的Web服务 [!DNL Experience Manager] as a Cloud Service，确保您具有Web服务的WSDL URL，并执行以下操作：

1. 转到&#x200B;**[!UICONTROL 工具 > Cloud Services > 数据源]**。点按以选择要创建云配置的文件夹。

   请参阅 [为云服务配置配置文件夹](configure-data-sources.md#cloud-folder) 有关为云服务配置创建和配置文件夹的信息。

1. 点按 **[!UICONTROL 创建]** 以打开 **[!UICONTROL 创建数据源配置向导]**. 指定配置的名称和（可选）标题，选择 **[!UICONTROL SOAP Web服务]** 从 **[!UICONTROL 服务类型]** 下拉列表（可选）浏览并选择配置的缩略图图像，然后点按 **[!UICONTROL 下一个]**.
1. 为SOAP Web服务指定以下内容：

   * Web服务的WSDL URL。
   * 服务端点. 在此字段中指定一个值以覆盖WSDL中提到的服务端点。
   * 选择身份验证类型 — 无、OAuth2.0([授权码](https://oauth.net/2/grant-types/authorization-code/)， [客户端凭据](https://oauth.net/2/grant-types/client-credentials/))、基本身份验证或自定义身份验证 — 用于访问SOAP服务，并相应地提供身份验证的详细信息。

     <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
     <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

     <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 点按 **[!UICONTROL 创建]** 创建SOAP Web服务的云配置。

### 在SOAP Web服务WSDL中启用导入语句的使用 {#enable-import-statements}

可以指定用作绝对URL的过滤器的正则表达式，这些绝对URL允许作为SOAP Web服务WSDL中的导入语句。 默认情况下，此字段中没有值。 因此， [!DNL Experience Manager] 阻止WSDL中所有可用的import语句。 如果您指定 `.*` 作为该字段中的值， [!DNL Experience Manager] 允许所有import语句。

设置 `importAllowlistPattern` 的属性 **[!UICONTROL 列入允许列表表单数据模型SOAP Web服务导入]** 用于指定正则表达式的配置。 以下JSON文件显示了一个示例：

```json
{
  "importAllowlistPattern": ".*"
}
```

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hans#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hans#deployment-process)。

## 配置OData服务 {#config-odata}

OData服务由其服务根URL标识。 在中配置OData服务 [!DNL Experience Manager] as a Cloud Service，请确保您拥有服务的服务根URL，然后执行以下操作：

>[!NOTE]
>
> 表单数据模型支持 [OData版本4](https://www.odata.org/documentation/).
>有关配置的分步指南 [!DNL Microsoft®® Dynamics 365]，在线或内部部署，请参阅 [[!DNL Microsoft® Dynamics] OData配置](ms-dynamics-odata-configuration.md).

1. 转到&#x200B;**[!UICONTROL 工具 > Cloud Services > 数据源]**。点按以选择要创建云配置的文件夹。

   请参阅 [为云服务配置配置文件夹](#cloud-folder) 有关为云服务配置创建和配置文件夹的信息。

1. 点按 **[!UICONTROL 创建]** 以打开 **[!UICONTROL 创建数据源配置向导]**. 指定配置的名称和（可选）标题，选择 **[!UICONTROL OData服务]** 从 **[!UICONTROL 服务类型]** 下拉列表（可选）浏览并选择配置的缩略图图像，然后点按 **[!UICONTROL 下一个]**.
1. 为OData服务指定以下详细信息：

   * 要配置的OData服务的服务根URL。
   * 选择身份验证类型 — 无、OAuth2.0([授权码](https://oauth.net/2/grant-types/authorization-code/)， [客户端凭据](https://oauth.net/2/grant-types/client-credentials/))、基本身份验证、API密钥或自定义身份验证 — 用于访问OData服务，并相应地提供身份验证的详细信息。

   如果您选择 **[!UICONTROL API密钥]** 作为身份验证类型，指定API密钥的值。 API密钥可作为请求标头或查询参数发送。 从中选择以下选项之一 **[!UICONTROL 位置]** 下拉列表，并在中指定标头的名称或查询参数 **[!UICONTROL 参数名称]** 字段输入相应的。

   >[!NOTE]
   >
   您必须选择要连接的OAuth 2.0身份验证类型 [!DNL Microsoft®® Dynamics] 使用OData端点作为服务根的服务。

1. 点按 **[!UICONTROL 创建]** 以创建OData服务的云配置。

<!--
## Configure Microsoft® SharePoint List {#config-sharepoint-list}

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

To save data in a tabular form use, Microsoft® SharePoint List. To configure a Microsoft SharePoint List in [!DNL Experience Manager] as a Cloud Service, do the following:

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.   
1. Select a **Configuration Container**. The configuration is stored in the selected Configuration Container. 
1. Click **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** from the drop-down list. The SharePoint configuration wizard appears.  
1. Specify the **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** and **[!UICONTROL OAuth URL]**. For information on how to retrieve Client ID, Client Secret, Tenant ID for OAuth URL, see [Microsoft&reg; Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
    * You can retrieve the `Client ID` and `Client Secret` of your app from the Microsoft&reg; Azure portal.
    * In the Microsoft&reg; Azure portal, add the Redirect URI as `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Replace `[author-instance]` with the URL of your Author instance.
    * Add the API permissions `offline_access` and `Sites.Manage.All` in the **Microsoft® Graph** tab to provide read/write permissions. Add `AllSites.Manage` permission in the **Sharepoint** tab to interact remotely with SharePoint data.
    * Use OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` with the `tenant-id` of your app from the Microsoft&reg; Azure portal.

      >[!NOTE]
      >
      > The **client secret** field is mandatory or optional depends upon your Azure Active Directory application configuration. If your application is configured to use a client secret, it is mandatory to provide the client secret.

1. Click **[!UICONTROL Connect]**. On a successful connection, the `Connection Successful` message appears.
1. Select **[!UICONTROL SharePoint Site]** and **[!UICONTROL SharePoint List]** from the drop-down list.
1. Tap **[!UICONTROL Create]** to create the cloud configuration for the Microsoft® SharePointList.

-->

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## 后续步骤 {#next-steps}

您已配置数据源。 接下来，您可以创建一个表单数据模型，或者，如果您已创建没有数据源的表单数据模型，则可以将其与您配置的数据源关联。 请参阅 [创建表单数据模型](create-form-data-models.md) 以了解详细信息。


<!--

>[!MORELIKETHIS]
>
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>*  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->