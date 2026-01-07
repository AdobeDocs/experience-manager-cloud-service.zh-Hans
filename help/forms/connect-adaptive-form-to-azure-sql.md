---
Title: How to Connect AEM Adaptive Forms with Azure SQL Storage
Description: Learn how to configure an Azure SQL Database connection in AEM Forms and integrate it with your Adaptive Forms to store or retrieve data efficiently using JDBC.
Keywords: Azure SQL integration with AEM Forms, Connecting Adaptive Forms to Azure SQL Database, JDBC connection for Azure SQL in AEM Forms, Storing Adaptive Form data in Azure SQL
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 40193d89f2a4ef864a564eb9932403531eaf1ff7
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 2%

---

# 将自适应表单连接到Azure SQL存储

Adobe Experience Manager (AEM)中的自适应Forms可与外部数据库集成以存储或检索数据。
本文概述如何通过AEM as a Cloud Service使用JDBC将自适应表单连接到Azure SQL数据库。

> 
> 
> 本指南适用于启用了高级联网的非沙盒AEM as a Cloud Service环境。

## 优点

将自适应Forms与Azure SQL集成具有以下几个好处：

* **实时数据交互：**&#x200B;支持在表单和Azure数据库之间实时读取和写入数据。
* **可伸缩性：** Azure SQL提供了适用于企业级应用程序的可伸缩数据库性能。
* **集中数据存储：**&#x200B;将表单提交和检索的数据安全地存储在一个中心位置。
* **安全合规性：**&#x200B;利用Azure的内置网络、防火墙和加密选项确保安全通信。
* **云原生集成：**&#x200B;非常适合使用AEM as a Cloud Service的云优先的现代体系结构。

## 先决条件

* 创建[Azure SQL数据库](https://learn.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal)并确保已启用&#x200B;**代理连接**。

  >[!NOTE]
  >
  > 导航到`Azure Portal → SQL Server → Security → Networking → Connectivity`以启用&#x200B;**代理连接**。

  ![创建Azure Db](/help/forms/assets/create-azure-db.png)

* 为创建的Azure数据库启用使用专用出口IP[配置的](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/dedicated-egress-ip-address)高级网络。

  >[!NOTE]
  >
  >    启用专用出口IP后。 转到`Azure Portal → SQL Server → Security → Networking → Public Access`并将出口IP添加到防火墙规则。

  ![出口IP](/help/forms/assets/cretae-azure-db-egress-ip.png)

* 在云环境中使用以下内容设置端口转发：
   * **portOrigin**：介于`30000–30999`之间
   * **portDest**： `1433` （Azure SQL的默认端口）
例如： `portOrigin: 30433 → portDest: 1433`

     > 
     > 
     > 您可以联系Adobe Cloud Manager支持以配置端口转发。


## 将自适应Forms连接到Azure SQL的步骤

**步骤1：克隆AEM as a Cloud Service Git存储库**

1. 打开命令行并选择要存储AEM as a Cloud Service存储库的目录，如`/cloud-service-repository/`。

1. 运行以下命令以克隆存储库：

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **在何处查找此信息？**

   有关查找这些详细信息的分步说明，请参阅Adobe Experience League文章“[访问Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)”。

   当命令成功完成时，您会看到在本地目录中创建了一个新文件夹。 此文件夹以您的应用程序命名。

1. 在编辑器中打开存储库文件夹。

**步骤2：添加所需的JAR**

通过[包将](https://central.sonatype.com/artifact/com.microsoft.sqlserver/mssql-jdbc/12.8.0.jre11?smo=true)SQL驱动程序依赖项`all`包含到AEM项目：

>[!NOTE]
>
> 要在项目中包括SQL依赖项，请参阅[SQL驱动程序依赖项](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool#mysql-driver-dependencies)部分。

**步骤3：添加JDBC配置**

1. 导航到`<application folder>`中的以下目录，该目录应放置JDBC池的OSGi配置：

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**步骤4：创建Azure SQL连接配置文件**

1. 创建文件：

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-sql.cfg.json
   ```

1. 添加以下代码行：

   ```json
   {
   "datasource.name": "azuredbshr",
   "jdbc.driver.class": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
   "jdbc.username": "<azureuser>",
   "jdbc.connection.uri": "jdbc:sqlserver://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30433;database=testdb;user=<azureuser>;password=<azurepassword>;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;",
   "jdbc.password": "******",
   "jdbc.validation.query": "SELECT 1"
       }
   ```

   > 
   >
   > 将`jdbc.username`替换为实际的Azure用户名，将`jdbc.password`替换为实际的安全密码。

**步骤5：提交并推送更改**

打开终端，运行以下命令：

```bash
git add .
git commit -m "<commit message>"
git push 
```

**步骤6：通过Cloud Manager管道部署更改**

1. 登录到&#x200B;**AEM Cloud Manager**。
1. 导航到您的项目并运行管道以部署更改。

**步骤7：创建表单数据模型(FDM)**

完成AEM和Azure设置并部署代码更改后：

1. 转到AEM创作实例。
1. 导航到&#x200B;**工具** > **Forms** > **数据集成**。
1. 新建&#x200B;**表单数据模型**。
1. 在&#x200B;**数据源**&#x200B;选项卡中，选择已创建的JDBC配置。
1. 单击&#x200B;**[!UICONTROL 创建]**&#x200B;并验证连接。

![创建表单数据模型](/help/forms/assets/create-azure-sql-fdm.png)

**步骤8：在自适应表单中使用创建的FDM**

1. 在编辑模式下打开自适应表单。
1. 选择上一步中创建的FDM作为数据模型。
1. 使用[数据绑定将表单字段与Azure SQL数据源](/help/forms/work-with-form-data-model.md#add-data-model-objects-and-services)连接并配置提交操作。

## 最佳做法

* 使用&#x200B;**密码管理**&#x200B;避免在配置文件中对密码进行硬编码。
* 定期轮换数据库凭据并安全地更新配置。
* 监测JDBC连接日志中的故障和延迟。
* 遵循Azure保护SQL数据库和防火墙配置的最佳做法。
* 避免使用高权限数据库帐户进行表单访问。

## 相关文章

{{af-submit-action}}