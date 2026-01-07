---
title: 如何配置数据源？
description: 了解如何将RESTful Web服务、基于SOAP的Web服务和OData服务配置为表单数据模型(FDM)的数据源。
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: f913871da16b44d7a465e0fa00608835524ba7e3
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 4%

---


# 配置数据源 {#configure-data-sources}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/configure-data-sources.html) |
| AEM as a Cloud Service | 本文 |

![数据集成](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms]数据集成允许您配置并连接到不同的数据源。 支持开箱即用的以下类型：

* 关系数据库 — MySQL、[!DNL Microsoft® SQL Server]、[!DNL IBM® DB2®]、postgreSQL、Azure SQL和[!DNL Oracle RDBMS]
* RESTful Web服务
* 基于SOAP的Web服务
* OData服务（版本4.0）
* Microsoft® Dynamics
* Salesforce
* Microsoft® Azure Blob存储

数据集成支持现成的OAuth2.0（[授权代码](https://oauth.net/2/grant-types/authorization-code/)、[客户端凭据](https://oauth.net/2/grant-types/client-credentials/)）、基本身份验证和API密钥身份验证类型，并允许实施自定义身份验证以访问Web服务。 在[!DNL Experience Manager] as a Cloud Service中配置了RESTful、基于SOAP和OData服务，而在[!DNL Experience Manager] Web控制台中配置了关系数据库的JDBC和[!DNL Experience Manager]用户配置文件的连接器。

## 配置关系数据库 {#configure-relational-database}

### 先决条件

在使用[!DNL Experience Manager] Web控制台配置配置关系数据库之前，必须：

* [通过Cloud Manager API启用高级联网](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)，因为默认情况下已禁用端口。
* [在Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies)中添加JDBC驱动程序依赖项。


### 配置关系数据库的步骤

可以使用[!DNL Experience Manager] Web控制台配置来配置关系数据库。 执行以下操作：

**步骤1：克隆AEM as a Cloud Service Git存储库**

1. 打开命令行并选择要存储AEM as a Cloud Service存储库的目录，如`/cloud-service-repository/`。

2. 运行以下命令以克隆存储库：

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **在何处查找此信息？**

   有关查找这些详细信息的分步说明，请参阅Adobe Experience League文章“[访问Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)”。

   当命令成功完成时，您会看到在本地目录中创建了一个新文件夹。 此文件夹以您的应用程序命名。

**步骤2：导航到配置文件夹**

1. 在编辑器中打开存储库文件夹。

1. 导航到`<application folder>`中的以下目录，该目录应放置JDBC池的OSGi配置：

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**步骤3：创建MySQL连接配置文件**

1. 创建文件：

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-mysql.cfg.json
   ```

1. 添加以下代码行：

```json
{
  "jdbc.driver.class": "com.mysql.cj.jdbc.Driver",
  "jdbc.connection.uri": "jdbc:mysql://<hostname>:<port>/<database>?useSSL=false",
  "jdbc.username": "<your-db-username>",
  "jdbc.password": "<your-db-password>",
  "datasource.name": "<application folder>-mysql",
  "datasource.svc.prop.name": "<application folder>-mysql"
}
```

> 
>
> 将占位符（如`<application folder>`、`<hostname>`、`<database>`、`<your-db-username>`和`<your-db-password>`）替换为实际值。

**步骤4：提交并推送更改**

打开终端，运行以下命令：

```bash
git add .
git commit -m "<commit message>"
git push 
```

**步骤5：通过Cloud Manager管道部署更改**

1. 登录到&#x200B;**AEM Cloud Manager**。
1. 导航到您的项目并运行管道以部署更改。

>[!NOTE]
>
> 有关更多详细信息，请参阅使用JDBC DataSourcePool[的](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html)SQL连接。

<!--
1. Go to [!DNL Experience Manager] web console at `https://server:host/system/console/configMgr`.
2. Locate **[!UICONTROL Day Commons JDBC Connections Pools]** configuration. Select to open the configuration in edit mode.

   ![JDBC Connector Pool](/help/forms/assets/jdbc_connector.png)

3. In the configuration dialog, specify the details for the database you want to configure, such as:

    * Java&trade; class name for the JDBC driver
    * JDBC connection URI
    * Username and password to establish connection with the JDBC driver
    * Specify a SQL SELECT query in the **[!UICONTROL Validation Query]** field to validate connections from the pool. The query must return at least one row. Based on your database, specify one of the following:
      * SELECT 1 (MySQL and MS&reg; SQL) 
      * SELECT 1 from dual (Oracle)
    * Name of the data source

   Sample strings for configuring a relational database:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```


    
4. Select **[!UICONTROL Save]** to save the configuration.

Now, you can use the configured relational database with your Form Data Model (FDM). 

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and select to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties are available for use in form data model (FDM). Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model (FDM) can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Select **[!UICONTROL Save]** to save the configuration. -->

## 为云服务配置配置文件夹 {#cloud-folder}

配置RESTful、SOAP和OData服务的云服务需要配置云服务文件夹。

[!DNL Experience Manager]中的所有云服务配置都已合并到`/conf`存储库的[!DNL Experience Manager]文件夹中。 默认情况下，`conf`文件夹包含`global`文件夹，您可以在其中创建云服务配置。 但是，必须为云配置手动启用它。 您还可以在`conf`中创建其他文件夹以创建和组织Cloud Service配置。

要为云服务配置配置文件夹，请执行以下操作：

1. 转到&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。
   * 有关详细信息，请参阅[配置浏览器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html)文档。
1. 执行以下操作可为云配置启用全局文件夹，或跳过此步骤为云服务配置创建和配置其他文件夹。

   1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，选择`global`文件夹并选择&#x200B;**[!UICONTROL 属性]**。

   1. 在&#x200B;**[!UICONTROL 配置属性]**&#x200B;对话框中，启用&#x200B;**[!UICONTROL 云配置]**。

   1. 选择&#x200B;**[!UICONTROL 保存并关闭]**，以保存配置并退出对话框。

1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，指定文件夹的标题，并启用&#x200B;**[!UICONTROL 云配置]**。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建为云服务配置启用的文件夹。

## 配置RESTful Web服务 {#configure-restful-web-services}

可在[定义文件或服务终结点中使用JSON或YAML格式的](https://swagger.io/specification/v2/)Swagger规范[!DNL Swagger]描述RESTful Web服务。

>[!NOTE]
> 要在[!DNL Experience Manager] as a Cloud Service中配置RESTful Web服务，请确保您的文件系统上有[!DNL Swagger]文件（[Swagger版本2.0](https://swagger.io/specification/v2/)）或[!DNL Swagger]文件（[Swagger版本3.0](https://swagger.io/specification/v3/)），或者文件托管的URL上有。

### 为Open API规范版本2.0配置RESTful服务 {#configure-restful-services-open-api-2.0}

1. 转到&#x200B;**[!UICONTROL 工具>云服务>数据源]**。 选择以选择要创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置文件夹](configure-data-sources.md#cloud-folder)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据Source配置向导]**。 指定配置的名称和标题，从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL RESTful服务]**，浏览并选择配置的缩略图图像，然后选择&#x200B;**[!UICONTROL 下一步]**。
1. 为RESTful服务指定以下详细信息：

   * 从[!UICONTROL Swagger Source]下拉列表中选择URL或文件，并相应地指定[!DNL Swagger URL]定义文件的[!DNL &#x200B; Swagger]或从本地文件系统上传[!DNL Swagger]文件。
   * 根据[!DNL &#x200B; Swagger] Source输入，以下字段已预填充值：

      * 方案：REST API使用的传输协议。 下拉列表中显示的方案类型数取决于[!DNL Swagger]源中定义的方案。
      * 主机：提供REST API的主机的域名或IP地址。 它是必填字段。
      * 基本路径：所有API路径的URL前缀。 它是一个可选字段。\
        如有必要，请编辑这些字段的预填充值。

   * 选择身份验证类型 — None、OAuth2.0（[授权代码](https://oauth.net/2/grant-types/authorization-code/)、[客户端凭据](https://oauth.net/2/grant-types/client-credentials/)）、基本身份验证、API密钥或自定义身份验证 — 以访问RESTful服务，并相应地提供身份验证的详细信息。

   如果选择&#x200B;**[!UICONTROL API密钥]**&#x200B;作为身份验证类型，请指定API密钥的值。 API密钥可作为请求标头或查询参数发送。 从&#x200B;**[!UICONTROL 位置]**&#x200B;下拉列表中选择其中一个选项，并在&#x200B;**[!UICONTROL 参数名称]**&#x200B;字段中相应地指定标头名称或查询参数。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建RESTful服务的云配置。

### 为Open API规范版本3.0配置RESTful服务 {#configure-restful-services-open-api-3.0}

1. 转到&#x200B;**[!UICONTROL 工具>云服务>数据源]**。 选择以选择要创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置文件夹](configure-data-sources.md#cloud-folder)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据Source配置向导]**。 指定配置的名称和标题，从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL RESTful服务]**，浏览并选择配置的缩略图图像，然后选择&#x200B;**[!UICONTROL 下一步]**。
1. 为RESTful服务指定以下详细信息：

   * 从[!UICONTROL Swagger Source]下拉列表中选择URL或文件，并相应地指定[!DNL Swagger 3.0 URL]定义文件的[!DNL &#x200B; Swagger]或从本地文件系统上传[!DNL Swagger]文件。
   * 根据[!DNL &#x200B; Swagger] Source输入，显示与目标服务器的连接信息。
   * 选择身份验证类型 — None、OAuth2.0（[授权代码](https://oauth.net/2/grant-types/authorization-code/)、[客户端凭据](https://oauth.net/2/grant-types/client-credentials/)）、基本身份验证、API密钥或自定义身份验证 — 以访问RESTful服务，并相应地提供身份验证的详细信息。

   如果选择&#x200B;**[!UICONTROL API密钥]**&#x200B;作为身份验证类型，请指定API密钥的值。 API密钥可作为请求标头或查询参数发送。 从&#x200B;**[!UICONTROL 位置]**&#x200B;下拉列表中选择其中一个选项，并在&#x200B;**[!UICONTROL 参数名称]**&#x200B;字段中相应地指定标头名称或查询参数。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建RESTful服务的云配置。

RESTful服务Open API规范版本3.0不支持的一些操作包括：

* 回调
* oneof/anyof
* 远程引用
* 链接
* 针对单次操作的不同MIME类型的不同请求主体

有关详细信息，请参阅[OpenAPI 3.0规范](https://swagger.io/specification/v3/)。

### 使用服务端点配置RESTful服务 {#configure-restful-services-service-endpoint}

<span class="preview">服务终结点功能在早期采用程序下，仅适用于核心组件。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

1. 转到&#x200B;**[!UICONTROL 工具>云服务>数据源]**。 选择以选择要创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置文件夹](configure-data-sources.md#cloud-folder)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据Source配置向导]**。

1. 指定配置的名称和标题，从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL RESTful服务]**，浏览并选择配置的缩略图图像，然后选择&#x200B;**[!UICONTROL 下一步]**。

1. 在下一页上，从&#x200B;**[!UICONTROL RESTful服务下拉列表]**&#x200B;中选择&#x200B;**[!UICONTROL 服务终结点]**。

   ![服务终结点](/help/forms/assets/select-service-endpoint.png)

1. 指定&#x200B;**[!UICONTROL 服务终结点URL]**。

   >[!NOTE]
   > 默认情况下，“方法类型”为“POST”。
1. 从下拉列表中选择一种内容类型。 内容类型包括多部分表单数据、JSON和URL编码（键值对）。
1. 现在，您可以从下拉列表中选择任意身份验证类型，如OAuth 2.0、基本身份验证、API密钥、自定义身份验证。
   ![服务终结点身份验证类型](/help/forms/assets/service-endpoint-authtype.png)
1. 单击“创建”。

### 表单数据模型(FDM) HTTP客户端配置可优化性能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms]在与RESTful Web服务集成时形成数据模型，因为数据源包括用于性能优化的HTTP客户端配置。

为REST数据源&#x200B;**[!UICONTROL 配置设置]**&#x200B;表单数据模型HTTP客户端配置的以下属性以指定正则表达式：

* 使用`http.connection.max.per.route`属性设置表单数据模型(FDM)和RESTful Web服务之间允许的最大连接数。 默认值为20个连接。

* 使用`http.connection.max`属性为每个路由指定允许的最大连接数。 默认值为40个连接。

* 使用`http.connection.keep.alive.duration`属性指定持久HTTP连接保持活动状态的持续时间。 默认值为15秒。

* 使用`http.connection.timeout`属性指定[!DNL Experience Manager Forms]服务器等待建立连接的持续时间。 默认值为10秒。

* 使用`http.socket.timeout`属性指定两个数据包之间不活动的最长时间。 默认值为30秒。

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

1. 为REST数据源&#x200B;**[!UICONTROL 选择]**&#x200B;表单数据模型HTTP客户端配置。

1. 在[!UICONTROL REST数据源]的表单数据模型HTTP客户端配置对话框中：

   * 在&#x200B;**[!UICONTROL 连接限制的]**&#x200B;字段中指定表单数据模型(FDM)和RESTful Web服务之间允许的最大连接数。 默认值为20个连接。

   * 在&#x200B;**[!UICONTROL 每个路由的连接限制]**&#x200B;字段中为每个路由指定允许的最大连接数。 缺省值为两个连接。

   * 在&#x200B;**[!UICONTROL 保持活动]**&#x200B;字段中指定持续HTTP连接保持活动状态的持续时间。 默认值为15秒。

   * 在[!DNL Experience Manager Forms]连接超时&#x200B;**[!UICONTROL 字段中指定]**&#x200B;服务器等待连接建立的持续时间。 默认值为10秒。

   * 在&#x200B;**[!UICONTROL 套接字超时]**&#x200B;字段中指定两个数据包之间的最长不活动时间段。 默认值为30秒。

## 配置SOAP Web服务 {#configure-soap-web-services}

基于SOAP的Web服务使用[Web服务描述语言(WSDL)规范](https://www.w3.org/TR/wsdl)进行描述。 [!DNL Experience Manager Forms]不支持RPC样式的WSDL模型。

要在[!DNL Experience Manager] as a Cloud Service中配置基于SOAP的Web服务，请确保您拥有该Web服务的WSDL URL，并执行以下操作：

1. 转到&#x200B;**[!UICONTROL 工具>云服务>数据源]**。 选择以选择要创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置文件夹](configure-data-sources.md#cloud-folder)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据Source配置向导]**。 指定配置的名称和标题，从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL SOAP Web服务]**，浏览并选择配置的缩略图图像，然后选择&#x200B;**[!UICONTROL 下一步]**。
1. 为SOAP Web服务指定以下内容：

   * Web服务的WSDL URL。
   * 服务端点。 在此字段中指定一个值以覆盖WSDL中提到的服务端点。
   * 选择身份验证类型 — None、OAuth2.0（[授权代码](https://oauth.net/2/grant-types/authorization-code/)、[客户端凭据](https://oauth.net/2/grant-types/client-credentials/)）、Basic Authentication或Custom Authentication — 以访问SOAP服务，并相应地提供身份验证的详细信息。

     <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
     <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

     <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建SOAP Web服务的云配置。

### 在SOAP Web服务WSDL中启用导入语句 {#enable-import-statements}

您可以指定一个正则表达式，用作在SOAP Web服务WSDL中允许作为import语句的绝对URL的过滤器。 默认情况下，此字段中没有值。 因此，[!DNL Experience Manager]将阻止WSDL中所有可用的导入语句。 如果在此字段中指定`.*`作为值，[!DNL Experience Manager]将允许所有import语句。

设置`importAllowlistPattern`表单数据模型SOAP Web服务导入允许列表&#x200B;**[!UICONTROL 配置的]**&#x200B;属性以指定正则表达式。 以下JSON文件显示了一个示例：

```json
{
  "importAllowlistPattern": ".*"
}
```

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hans#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hans#deployment-process)。

## 配置OData服务 {#config-odata}

OData服务由其服务根URL标识。 要在[!DNL Experience Manager] as a Cloud Service中配置OData服务，请确保您拥有该服务的服务根URL，并执行以下操作：

>[!NOTE]
>
> 表单数据模型(FDM)支持[OData版本4](https://www.odata.org/documentation/)。
>有关配置[!DNL Microsoft®® Dynamics 365]的分步指南（在线或本地），请参阅[[!DNL Microsoft® Dynamics] OData配置](ms-dynamics-odata-configuration.md)。

1. 转到&#x200B;**[!UICONTROL 工具>云服务>数据源]**。 选择以选择要创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置文件夹](#cloud-folder)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据Source配置向导]**。 指定配置的名称和标题，从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL OData服务]**，浏览并选择配置的缩略图图像，然后选择&#x200B;**[!UICONTROL 下一步]**。
1. 为OData服务指定以下详细信息：

   * 要配置的OData服务的服务根URL。
   * 选择身份验证类型 — 无、OAuth2.0（[授权代码](https://oauth.net/2/grant-types/authorization-code/)、[客户端凭据](https://oauth.net/2/grant-types/client-credentials/)）、基本身份验证、API密钥或自定义身份验证 — 以访问OData服务，并相应地提供身份验证的详细信息。

   如果选择&#x200B;**[!UICONTROL API密钥]**&#x200B;作为身份验证类型，请指定API密钥的值。 API密钥可作为请求标头或查询参数发送。 从&#x200B;**[!UICONTROL 位置]**&#x200B;下拉列表中选择其中一个选项，并在&#x200B;**[!UICONTROL 参数名称]**&#x200B;字段中相应地指定标头名称或查询参数。

   >[!NOTE]
   >
   >选择OAuth 2.0身份验证类型以使用OData端点作为服务根与[!DNL Microsoft®® Dynamics]服务连接。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建OData服务的云配置。

<!--
## Configure Microsoft&reg; SharePoint List {#config-sharepoint-list}

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

To save data in a tabular form use, Microsoft&reg; SharePoint List. To configure a Microsoft SharePoint List in [!DNL Experience Manager] as a Cloud Service, do the following:

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft&reg; SharePoint]**.   
1. Select a **Configuration Container**. The configuration is stored in the selected Configuration Container. 
1. Click **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** from the drop-down list. The SharePoint configuration wizard appears.  
1. Specify the **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** and **[!UICONTROL OAuth URL]**. For information on how to retrieve Client ID, Client Secret, Tenant ID for OAuth URL, see [Microsoft&reg; Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
    * You can retrieve the `Client ID` and `Client Secret` of your app from the Microsoft&reg; Azure portal.
    * In the Microsoft&reg; Azure portal, add the Redirect URI as `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Replace `[author-instance]` with the URL of your Author instance.
    * Add the API permissions `offline_access` and `Sites.Manage.All` in the **Microsoft&reg; Graph** tab to provide read/write permissions. Add `AllSites.Manage` permission in the **Sharepoint** tab to interact remotely with SharePoint data.
    * Use OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` with the `tenant-id` of your app from the Microsoft&reg; Azure portal.

      >[!NOTE]
      >
      > The **client secret** field is mandatory or optional depends upon your Azure Active Directory application configuration. If your application is configured to use a client secret, it is mandatory to provide the client secret.

1. Click **[!UICONTROL Connect]**. On a successful connection, the `Connection Successful` message appears.
1. Select **[!UICONTROL SharePoint Site]** and **[!UICONTROL SharePoint List]** from the drop-down list.
1. Select **[!UICONTROL Create]** to create the cloud configuration for the Microsoft&reg; SharePointList.

-->

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model (FDM), both the data source and [!DNL Experience Manager] Server running Form Data Model (FDM) authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model (FDM) on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and select **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and select **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, select **[!UICONTROL Select Certificate File]**, upload the certificate, and select **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## 后续步骤 {#next-steps}

您已配置数据源。 接下来，您可以创建表单数据模型(FDM)，或者，如果您已经在不使用数据源的情况下创建了表单数据模型(FDM)，则可以将其与配置的数据源关联。 有关详细信息，请参阅[创建表单数据模型](create-form-data-models.md)。

<!--

>[!MORELIKETHIS]
>
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>*  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->