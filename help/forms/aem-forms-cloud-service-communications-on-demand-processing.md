---
title: 如何设置Forms通信同步API？
description: 为Adobe Experience Manager Forms as a Cloud Service的交互式通信同步API设置开发环境
role: Admin, Developer, User
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: 77da2f4ddcd9074a79883f18a33b6fe50e32b266
workflow-type: tm+mt
source-wordcount: '2396'
ht-degree: 2%

---


# 为AEM Forms Communications同步API配置OAuth服务器到服务器访问

本指南提供有关配置和调用AEM Forms Communications Synchronous API的说明，可通过Adobe Developer Console使用OAuth服务器到服务器身份验证访问这些API。

## 先决条件

要设置用于运行和测试AEM Forms Communications API的环境，请确保您具备以下条件：

### 访问和权限

在开始配置Communications API之前，请确保您具有所需的访问权利和权限。

**用户和角色权限**

- 在Adobe Admin Console中分配的开发人员角色
- 在Adobe Developer Console中创建项目的权限

>[!NOTE]
>
> 要了解有关分配角色和授予用户访问权限的更多信息，请参阅文章[添加用户和角色](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)。

**Git存储库访问权限**

- 访问Cloud Manager Git存储库
- 用于克隆和推送更改的Git凭据

>[!NOTE]
>
> 要了解有关如何集成Adobe Cloud Manager和Adobe Cloud Manager的更多信息，请参阅[Git集成文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html)。

### 使用Adobe Developer Console (ADC)生成访问令牌

- 使用OAuth服务器到服务器身份验证通过Adobe Developer Console生成访问令牌。
- 从Adobe Developer Console检索客户端ID

>[!NOTE]
>
> 有关使用Adobe Developer Console的OAuth服务器到服务器身份验证的详细信息，[单击此处](/help/forms/oauth-api-authetication.md)。

### 开发工具

- 用于运行示例应用程序的&#x200B;**Node.js**
- **Git**&#x200B;的最新版本
- 访问&#x200B;**终端/命令行**
- 用于编辑配置文件（VS代码、IntelliJ等）的&#x200B;**文本编辑器或IDE**
- 用于API测试的&#x200B;**Postman**&#x200B;或类似工具

>[!NOTE]
>
> 这是每个环境的一次性流程，在继续设置AEM Forms Communications API之前必须完成此流程。

## 配置AEM Forms通信同步API

可使用OAuth服务器到服务器身份验证，通过Adobe Developer Console访问AEM Forms通信API。

请按照以下步骤操作，了解如何配置Forms通信同步API，以使用模板和XDP文件生成PDF：

### 步骤1：访问AEM云服务环境和AEM Forms端点

访问您的AEM Cloud Service环境详细信息，以获取API配置所需的URL和标识符。

#### 1.1登录Adobe Cloud Manager

1. 导航到[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
2. 使用您的Adobe ID登录

#### 1.2导航到项目概述

从列表中选择您的项目。 您被重定向到&#x200B;**项目概述**&#x200B;页面

![项目概述页面](/help/forms/assets/program-overview.png)

#### 1.3访问和查看AEM Cloud Service环境

您可以使用以下两个选项之一查看或访问AEM Cloud Service环境详细信息：

>[!BEGINTABS]

>[!TAB 选项1：从概述页面]

1. 在&#x200B;**项目概述**&#x200B;页面上
2. 单击左侧菜单中的&#x200B;**“环境”**。  您可以看到所有环境的列表
3. 单击特定环境名称以查看详细信息

   ![查看所有环境](/help/forms/assets/all-env.png)

>[!TAB 选项2：从环境部分]

1. 在&#x200B;**项目概述**&#x200B;页面上
2. 找到&#x200B;**环境**&#x200B;部分
3. 单击&#x200B;**“全部显示”**&#x200B;查看所有环境
4. 单击环境旁边的&#x200B;**省略号菜单(...)**
5. 选择&#x200B;**“查看详细信息”**

   ![选项1 — 环境详细信息](/help/forms/assets/option2-env-details.png)

>[!ENDTABS]

#### 1.4.查找您的AEM Forms端点

从&#x200B;**环境**&#x200B;详细信息页面，记下您的AEM URL实例。

![选项1 — 环境详细信息](/help/forms/assets/option1-env.png)

>[!NOTE]
>
> 要了解如何访问AEM云服务环境和AEM Forms端点，请参阅[管理环境文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html)。

### 步骤2：克隆Git存储库

克隆Cloud Manager Git存储库以管理API配置文件。

#### 2.1找到“存储库”部分

1. 在&#x200B;**项目概述**&#x200B;页面上，单击&#x200B;**存储库**&#x200B;选项卡
2. 找到存储库名称，然后单击省略号菜单(...)
3. 复制存储库URL

   ![复制存储库URL](/help/forms/assets/copy-repo-url.png)

>[!NOTE]
>
> URL格式通常为`https://git.cloudmanager.adobe.com/<org>/<program>/`

#### 2.2使用Git命令进行克隆

1. 打开命令提示符或终端
2. 运行`git clone`命令以克隆Git存储库。

   ```bash
   git clone [repository-url]
   ```

>[!NOTE]
>
> 要克隆Git存储库，请使用Adobe Cloud Manager提供的凭据。

例如，要克隆Git存储库，请执行以下命令：

```bash
https://git.cloudmanager.adobe.com/formsinternal01/AEMFormsInternal-ReleaseSanity-pXXX-ukYYYY/
```

![克隆Git存储库](/help/forms/assets/repo-clone.png)

要了解有关如何集成Adobe Cloud Manager和Adobe Cloud Manager的更多信息，请参阅[Git集成文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html)。

### 步骤3：Adobe Developer Console项目设置

#### 3.1访问Adobe Developer Console

1. 导航到[Adobe Developer Console](https://developer.adobe.com/console)
2. 使用您的Adobe ID登录
3. 创建新项目或导航到现有项目

>[!BEGINTABS]

>[!TAB 创建新项目]

1. 在&#x200B;**快速入门**&#x200B;部分中，单击&#x200B;**新建项目**
2. 使用默认名称创建新项目

   ![创建ADC项目](/help/forms/assets/adc-home.png)

3. 单击右上角的&#x200B;**编辑项目**

   ![编辑项目](/help/forms/assets/adc-edit-project.png)

4. 提供有意义的名称（例如“formsproject”）
5. 单击&#x200B;**保存**

   ![编辑项目名称](/help/forms/assets/adc-edit-projectname.png)

>[!TAB 导航到现有项目]

1. 从Adobe Developer Console单击&#x200B;**所有项目**

   ![搜索项目](/help/forms/assets/search-adc-project.png)

2. 找到您的项目并单击以将其打开。

   ![查找项目](/help/forms/assets/locate-adc-project.png)

>[!ENDTABS]

#### 3.2添加Forms通信API

1. 单击&#x200B;**添加API**

   ![添加API](/help/forms/assets/adc-add-api.png)

2. 在&#x200B;_添加API_&#x200B;对话框中，按&#x200B;**Experience Cloud**&#x200B;筛选
3. 选择&#x200B;**“Forms通信API”**

   ![添加Forms通信API](/help/forms/assets/adc-add-forms-api.png)

4. 点击&#x200B;**下一个**
5. 选择&#x200B;**OAuth服务器到服务器**&#x200B;身份验证方法

   ![选择身份验证方法](/help/forms/assets/adc-add-authentication-method.png)
6. 点击&#x200B;**下一个**

#### 3.3添加产品配置文件

1. 选择与您的AEM实例URL (**)匹配的**&#x200B;产品配置文件`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`。

2. 单击&#x200B;**保存配置的 API**。API和产品配置文件已添加到您的项目中

   ![选择项目配置](/help/forms/assets/adc-add-product-profile.png)

3. 查看&#x200B;**凭据详细信息**&#x200B;部分

   ![查看凭据](/help/forms/assets/adc-view-credential.png)

**记录API凭据**

```text
    API Credentials:
    ================
    Client ID: <your_client_id>
    Client Secret: <your_client_secret>
    Technical Account ID: <tech_account_id>
    Organization ID: <org_id>
    Scopes: AdobeID,openid,read_organizations
```

#### 3.4生成访问权限

>[!BEGINTABS]

>[!TAB 用于测试的] 

在Adobe Developer Console中手动生成访问令牌：

1. 单击项目API部分中的&#x200B;**“生成访问令牌”**&#x200B;按钮
2. 复制生成的访问令牌

   ![生成访问令牌](/help/forms/assets/adc-access-token.png)

>[!NOTE]
>
> 访问令牌仅在&#x200B;**24小时**&#x200B;内有效
>[!TAB 用于生产 的]

使用[Adobe IMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service) API以编程方式生成令牌：

**必需的凭据：**

- 客户端 ID
- 客户端密码
- 范围（通常： `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`）

**令牌终结点：**

```
    https://ims-na1.adobelogin.com/ims/token/v3
```

**示例请求(curl)：**

```bash
    curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    -d 'grant_type=client_credentials' \
    -d 'client_id=<YOUR_CLIENT_ID>' \
    -d 'client_secret=<YOUR_CLIENT_SECRET>' \
    -d 'scope=AdobeID,openid,read_organizations'
```

**响应：**

```json
        {
        "access_token": "eyJhbGciOiJSUz...",
        "token_type": "bearer",
        "expires_in": 86399
        }
```

>[!ENDTABS]

您现在可以使用生成的访问令牌为开发、暂存或生产环境进行API调用。

>[!NOTE]
>
> 要了解有关通过Adobe Developer Console进行OAuth服务器到服务器身份验证的更多信息，请参阅[OAuth服务器到服务器身份验证](/help/forms/oauth-api-authetication.md)文章。

### 步骤4：在AEM环境中注册客户端ID

要使ADC项目的客户端ID能够与AEM实例进行通信，您必须使用YAML配置文件注册它，并通过配置管道进行部署。

#### 4.1查找或创建配置目录

1. 导航到克隆的AEM项目存储库并找到`config`文件夹
2. 如果该文件不存在，请在项目根级别创建它：

   ```bash
   mkdir config
   ```

3. 在`api.yaml`目录中创建一个名为`config`的新文件：

   ```bash
   touch config/api.yaml
   ```

4. 在`api.yaml`文件中添加以下代码：

   ```yaml
   kind: "API"
   version: "1"
   metadata:
   envTypes: ["dev"]  # or ["prod", "stage"] for production environments
   data:
   allowedClientIDs:
       author:
       - "<your_client_id>"
       publish:
       - "<your_client_id>"
       preview:
       - "<your_client_id>"
   ```

以下内容说明了配置参数：

- **kind**：始终设置为`"API"`（标识为API配置）
- **版本**： API版本，通常为`"1"`或`"1.0"`
- **envTypes**：此配置适用的环境类型数组
   - `["dev"]` — 仅开发环境
   - `["stage"]` — 仅暂存环境
   - `["prod"]` — 仅生产环境
- **allowedClientIDs**：允许客户端ID访问您的AEM实例
   - **作者**：作者层的客户端ID
   - **发布**：发布层的客户端ID
   - **预览**：预览层的客户端ID

![正在添加配置文件](/help/forms/assets/create-api-yaml-file.png)

#### 4.2提交和推送更改

1. 导航到克隆的存储库的根文件夹，然后执行以下命令：


   ```bash
       git add config/api.yaml
       git commit -m "Whitelist client id for api invocation"
       git push origin <your-branch>
   ```

   ![推送Git更改](/help/forms/assets/push-yaml-changes-in-git.png)


### 步骤5：设置配置管道

#### 5.1登录Adobe Cloud Manager

1. 导航到[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
2. 使用您的Adobe ID登录

#### 5.1找到管道信息卡

1. 在项目概述页面上找到&#x200B;**管道**&#x200B;信息卡
2. 单击&#x200B;**添加**&#x200B;按钮

   ![添加管道](/help/forms/assets/add-pipeline.png)

#### 5.2选择管道类型

- **对于开发环境**：选择&#x200B;**“添加非生产管道”**。 非生产管道适用于开发和暂存环境

- 生产环境&#x200B;**&#x200B;**：选择&#x200B;**“添加生产管道”**。 生产管道需要额外的批准

>[!NOTE]
>
> 在这种情况下，请创建一个非生产管道，因为开发环境可用。

**1. 配置管道 — 配置选项卡**

在&#x200B;**配置**&#x200B;选项卡中：

a. **管道类型**

- 选择&#x200B;**“部署管道”**

b. **管道名称**

- 提供描述性名称，例如，将管道命名为`api-config-pipieline`

c. **部署触发器**

- **手动**：仅在手动触发时部署（建议用于初始设置）
- **在Git发生更改时**：将更改推送到分支时自动部署

d. **重要量度失败行为**

- **每次询问**：失败时提示操作（默认）
- **立即失败**：在度量失败时自动使管道失败
- **立即继续**：失败后继续

e.单击&#x200B;**“继续”**&#x200B;以继续访问&#x200B;**Source代码**&#x200B;选项卡

![配置管道](/help/forms/assets/add-config-pipeline.png)

**2. 配置管道 — Source代码选项卡**

在&#x200B;**Source代码**&#x200B;选项卡中：

a. **部署类型**

- 选择&#x200B;**“目标部署”**

b. **部署选项**

- 选择&#x200B;**“配置”**（仅部署配置文件）。 它告知Cloud Manager这是一个配置部署。

c. **选择符合条件的部署环境**

- 选择要部署配置的环境。 在这种情况下，它是一个`dev`环境。

d. **定义Source代码详细信息**

- **存储库**：选择包含`api.yaml`文件的存储库。 例如，选择`AEMFormsInternal-ReleaseSanity-pXXXXX-ukYYYYY`存储库。
- **Git分支**：选择您的分支。 例如，在本例中，我们的代码部署在`main`分支中。
- **代码位置**：输入`config`目录的路径。 由于`api.yaml`位于根目录的`config`文件夹中，因此请输入`/config`

e.单击&#x200B;**“保存”**&#x200B;以创建管道

![配置管道](/help/forms/assets/confirm-pipeline-1.png)

### 步骤6：部署配置

现已创建管道，请部署您的`api.yaml`配置

#### 6.1来自管道概述

1. 在项目概述页面上，找到&#x200B;**管道**&#x200B;信息卡
2. 在列表中导航到新创建的配置管道。 例如，查找您创建的管道名称（例如，“api-config-pipeline”）。 您可以查看管道详细信息，包括状态和上次运行。

#### 6.2开始部署**

1. 单击管道旁边的&#x200B;**“生成”**&#x200B;按钮（或播放图标▶）
2. 如果出现提示并且管道执行开始，请确认部署

![运行管道](/help/forms/assets/run-config-pipeline.png)

#### 6.3验证部署是否成功

- 等待管道完成。
   - 如果成功，状态将更改为“成功”（绿色复选标记✓）。
   - 如果失败，则状态将更改为“失败”（红叉✗）。 单击&#x200B;**下载日志**&#x200B;以查看错误详细信息。

     ![管道成功](/help/forms/assets/pipeline-suceess.png)

现在，您可以开始测试Forms Communications API。 出于测试目的，您可以使用Postman、curl或任何其他REST客户端调用API。

### 步骤7： API规范和测试

现在您的环境已配置，您可以使用Swagger UI或以编程方式通过开发NodeJS应用程序开始测试AEM Forms Communication API。

>[!BEGINTABS]

>[!TAB A。使用Swagger UI进行API测试]

Swagger UI提供了一个用于测试API而不编写代码的交互式界面。使用&#x200B;**尝试它**&#x200B;功能调用和测试[生成PDF](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) Forms通信API。

1. 导航到[Forms Communication API引用](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)，并在浏览器中打开[Forms Communication API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document)文档。
2. 展开&#x200B;**Document Generation**&#x200B;部分并选择[从XDP或PDF模板生成可填写的PDF表单，可以选择合并数据](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm)。
3. 在右窗格中，单击&#x200B;**尝试**。

   ![针对API的Swagger测试](/help/forms/assets/api-doc-generation.png)
4. 输入以下值：

   | **节** | **参数** | **值** |
   |--------------|---------------|------------|
   | 分段 | AEM实例 | AEM实例名称不带Adobe域名(`.adobeaemcloud.com`)。例如，使用`pXXXXX-eYYYYY`作为存储桶。 |
   | 安全性 | 持有者令牌 | 使用Adobe Developer Console项目的OAuth服务器到服务器凭据中的[访问令牌](/help/forms/oauth-api-authetication.md#how-to-generate-an-access-token-using-oauth-server-to-server-authentication) |
   | 主体 | 模板 | 上传XDP以生成PDF表单。 例如，您可以使用此[XDP](/help/forms/assets/ClosingForm.xdp)生成PDF。 |
   | 主体 | 数据 | 包含要与模板合并以生成预填充PDF表单的数据的可选XML文件。 例如，您可以使用[此XML](/help/forms/assets/ClosingForm.xml)来生成PDF。 |
   | 参数 | X-Adobe-Accept-Experimental | 1 |

5. 单击&#x200B;**发送**&#x200B;以调用API

   ![发送API](/help/forms/assets/api-send.png)

6. 检查&#x200B;**响应**&#x200B;选项卡中的响应：
   - 如果响应代码为`200`，则表示已成功创建PDF。
   - 如果响应代码为`400`，则表示请求参数无效或格式不正确。
   - 如果响应代码为`500`，则表示存在内部服务器错误。
   - 如果响应代码为`403`，则表示存在授权错误。

   在这种情况下，响应代码为`200`，这表示已成功生成PDF：

   ![查看响应](/help/forms/assets/api-success.png)

   现在，您可以使用[下载](/help/forms/assets/create-pdf.pdf)按钮下载&#x200B;**创建的PDF**&#x200B;并在PDF查看器中查看它：

   ![查看PDF](/help/forms/assets/create-pdf.png)

   >[!NOTE]
   >
   > 出于测试目的，您还可以使用[Postman](https://www.postman.com/)、[curl](https://curl.se/)或任何其他REST客户端调用AEM API。

>[!TAB B。通过开发NodeJS应用程序以编程方式完成]

开发Node.js应用程序以使用&#x200B;**Document Services API**&#x200B;从&#x200B;**XDP**&#x200B;模板和&#x200B;**XML**&#x200B;数据文件生成可填写的PDF表单

**先决条件**

- 系统上安装的Node.js
- 活动AEM as a Cloud Service实例
- 来自Adobe Developer Console的API身份验证的持有者令牌
- 示例XDP文件： [ClosingForm.xdp](/help/forms/assets/ClosingForm.xdp)
- 示例XML文件： [ClosingForm.xml](/help/forms/assets/ClosingForm.xml)

要开发Node.js应用程序，请按照分步开发操作：

**步骤1：创建新的Node.js项目**

打开cmd/terminal并执行以下命令：

```bash
# Create a new directory
mkdir demo-nodejs-generate-pdf
cd demo-nodejs-generate-pdf

##### Initialize Node.js project
npm init -y
```

![创建新节点js项目](/help/forms/assets/api-1.png)

**步骤2：安装所需的依赖项**

安装&#x200B;**node-fetch**、**dotenv**&#x200B;和&#x200B;**form-data**&#x200B;库以分别发出HTTP请求、读取环境变量和处理表单数据。

```bash
npm install node-fetch
npm install dotenv
npm install form-data
```

![安装npm依赖项](/help/forms/assets/api-2.png)

**步骤3：更新包.json**

1. 打开cmd/terminal并运行命令：

   ```bash
   code .
   ```

   ![在编辑器中打开项目](/help/forms/assets/api-3.png)

   它将在代码编辑器中打开项目。

2. 更新`package.json`文件以将`type`添加到`module`。

   ```bash
   {
   "name": "demo-nodejs-generate-pdf",
   "version": "1.0.0",
   "type": "module",
   "main": "index.js",
   }
   ```

   ![更新包文件](/help/forms/assets/api-4.png)

**步骤4：创建.env文件**

1. 在项目的根级别创建.env文件
2. 添加以下配置，并使用ADC项目的OAuth服务器到服务器凭据中的实际值替换占位符。

   ```bash
   CLIENT_ID=<ADC Project OAuth Server-to-Server credential ClientID>
   CLIENT_SECRET=<ADC Project OAuth Server-to-Server credential Client Secret>
   SCOPES=<ADC Project OAuth Server-to-Server credential Scopes>
   ```

   ![创建环境文件](/help/forms/assets/api-5.png)

   >[!NOTE]
   >
   > 您可以从Adobe Developer Console项目中复制`CLIENT_ID`、`CLIENT_SECRET`和`SCOPES`。

**步骤5：创建src/index.js**

1. 在项目的根级别创建`index.js`文件
2. 添加以下代码，并将占位符替换为实际值：

```javascript
// Import the dotenv configuration to load environment variables from the .env file
import "dotenv/config";

// Import fetch for making HTTP requests
import fetch from "node-fetch";
import fs from "fs";
import FormData from "form-data";

// REPLACE THE FOLLOWING VALUE WITH YOUR OWN
const bucket = <bucket-value>; // Your AEM Cloud Service Bucket name
const xdpFilePath = <xdp-file>;
const xmlFilePath = <xml-file>;

// Load environment variables
const clientId = process.env.CLIENT_ID;
const clientSecret = process.env.CLIENT_SECRET;
const scopes = process.env.SCOPES;

// Adobe IMS endpoint for obtaining an access token
const adobeIMSV3TokenEndpointURL = "https://ims-na1.adobelogin.com/ims/token/v3";

// Function to get an access token
const getAccessToken = async () => {
    console.log("Getting access token from IMS...");

    const options = {
        method: "POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded",
        },
        body: `grant_type=client_credentials&client_id=${clientId}&client_secret=${clientSecret}&scope=${scopes}`,
    };

    const response = await fetch(adobeIMSV3TokenEndpointURL, options);
    const responseJSON = await response.json();

    console.log("Access token received.");
    return responseJSON.access_token;
};

// Function to generate PDF form from XDP and XML
const generatePDF = async () => {
    const accessToken = await getAccessToken();

    console.log("Generating PDF form from XDP and XML...");

    // Read XDP and XML files
    const xdpFile = fs.readFileSync(xdpFilePath);
    const xmlFile = fs.readFileSync(xmlFilePath);

    const url = `https://${bucket}.adobeaemcloud.com/adobe/document/generate/pdfform`;

    const formData = new FormData();
    formData.append("template", xdpFile, {
        filename: "form.xdp",
        contentType: "application/vnd.adobe.xdp+xml"
    });
    formData.append("data", xmlFile, {
        filename: "data.xml",
        contentType: "application/xml"
    });

    const response = await fetch(url, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${accessToken}`,
            "X-Api-Key": clientId,
            "X-Adobe-Accept-Experimental": "1",
            ...formData.getHeaders()
        },
        body: formData,
    });

    if (response.ok) {
        const arrayBuffer = await response.arrayBuffer();
        fs.writeFileSync("generatedForm.pdf", Buffer.from(arrayBuffer));
        console.log("✅ PDF form generated successfully (saved as generatedForm.pdf)");
    } else {
        console.error("❌ Failed to generate PDF. Status:", response.status);
        console.error(await response.text());
    }
};

// Run the PDF generation function
generatePDF();
```

![创建index.js](/help/forms/assets/api-6.png)

**步骤6：运行应用程序**

```bash
node src/index.js
```

![运行应用程序](/help/forms/assets/api-7.png)

在`demo-nodejs-generate-pdf`文件夹中创建PDF。 导航到文件夹以查找名为`generatedForm.pdf`的生成文件。

![查看创建的pdf](/help/forms/assets/api-8.png)

![查看PDF](/help/forms/assets/create-pdf.png)

>[!ENDTABS]

您可以打开[生成的PDF](/help/forms/assets/create-pdf.png)进行查看。

## 疑难解答

### 常见问题和可能的原因

#### 问题1： 403禁止的错误

**症状：**

- API请求返回`403 Forbidden`
- 错误消息： *未经授权的访问*

**可能的原因：**

- 未在AEM实例的`api.yaml`配置中注册客户端ID

#### 问题2： 401未授权错误

**症状：**

- API请求返回`401 Unauthorized`
- 错误消息： *令牌无效或过期*

**可能的原因：**

- 访问令牌已过期（仅在24小时内有效）
- 客户端ID和客户端密钥不正确或不匹配

#### 问题3:404 “未找到”错误

**症状：**

- API请求返回`404 Not Found`
- 错误消息：*未找到资源*&#x200B;或找不到&#x200B;*API终结点*

**可能的原因：**

- 存储段参数不正确(不符合AEM实例标识符)

#### 问题4：管道部署失败

**症状：**

- 配置管道执行失败
- 部署日志显示与`api.yaml`相关的错误

**可能的原因：**

- YAML语法无效（缩进、引号或数组格式问题）
- `api.yaml`放置在不正确的目录中
- 配置中的客户端ID格式不正确或不正确
- 客户端密码无效

#### 问题5：Forms Communication API无法执行

**症状：**

- API请求返回错误，指示不支持的功能或不可用的功能。
- 使用XDP和XML生成PDF不起作用。
- 管道部署成功完成，但运行时API调用失败。

**可能的原因：**

AEM环境运行的版本是在引入或支持Forms通信API之前发布的。
要更新AEM环境，请参阅[更新AEM实例](#update-aem-instance)部分。

## 更新AEM实例

要更新AEM实例以查找环境详细信息，请执行以下操作：

1. 选择环境名称旁边的`ellipsis`(...)图标，然后单击&#x200B;**更新**
2. 单击&#x200B;**提交**&#x200B;按钮并运行建议的全栈管道。

   ![更新环境](/help/forms/assets/update-env.png)

## 相关文章

- 要了解如何为批处理（异步API）设置环境，请参阅[AEM Forms as a Cloud Service Communications批处理](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)。