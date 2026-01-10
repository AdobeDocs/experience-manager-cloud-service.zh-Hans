---
title: 如何设置OAuth服务器到服务器身份验证？
description: 了解如何为Adobe Experience Manager Forms as a Cloud Service配置OAuth服务器到服务器身份验证
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: 6bd2e1698cceaf8fe47e19e0645d0782c916644a
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 3%

---


# OAuth服务器到服务器身份验证

OAuth服务器到服务器身份验证允许对AEM Forms Communications API进行基于令牌的安全访问，而无需用户交互。 Adobe Developer Console支持OAuth服务器到服务器身份验证。

## 先决条件

在开始之前，请确保满足以下先决条件：

* 确保您具有[访问特定于您使用环境的Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/access-rights)的权限。
* [在Adobe Admin Console中分配系统管理员或开发人员角色](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions)以启用对Adobe Developer Console的访问。

## 如何使用OAuth服务器到服务器身份验证生成访问令牌？

按照以下步骤从Adobe Developer控制台生成访问令牌，并通过OAuth服务器到服务器身份验证进行首次API调用。

### &#x200B;1. Adobe Developer Console项目设置

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

### 2.添加Forms API

根据您想要执行的操作添加Forms API：

* **AEM Forms Communications API**：在需要生成、转换、汇编或保护文档(PDF和相关格式)时使用。
* **自适应Forms运行时API** — 在运行时需要渲染、提交或处理自适应Forms时使用。

>[!BEGINTABS]

>[!TAB 用于AEM Forms Communications API的] 

1. 单击&#x200B;**添加API**

   ![添加API](/help/forms/assets/adc-add-api.png)

2. 选择&#x200B;**Forms通信API**
   1. 在&#x200B;_添加API_&#x200B;对话框中，按&#x200B;**Experience Cloud**&#x200B;筛选
   2. 选择&#x200B;**“Forms通信API”**

      ![添加Forms通信API](/help/forms/assets/adc-add-forms-api.png)

   3. 点击&#x200B;**下一个**
   4. 选择&#x200B;**OAuth服务器到服务器**&#x200B;身份验证方法

      ![选择身份验证方法](/help/forms/assets/adc-add-authentication-method.png)

>[!TAB 自适应Forms运行时API的] 

1. **单击添加API**

   ![添加API](/help/forms/assets/adc-add-api.png)

2. **选择AEM Forms交付和运行时API**
   1. 在&#x200B;_添加API_&#x200B;对话框中，按&#x200B;**Experience Cloud**&#x200B;筛选
   2. 选择&#x200B;**“AEM Forms交付和运行时API”**
      ![添加Forms通信API](/help/forms/assets/adc-add-runtime-api.png)

   3. 点击&#x200B;**下一个**
   4. 选择&#x200B;**OAuth服务器到服务器**&#x200B;身份验证方法。
      ![选择身份验证方法](/help/forms/assets/adc-add-authentication-method.png)

>[!ENDTABS]

您还可以通过单击&#x200B;**添加到项目** > **API**，将API和身份验证方法添加到现有项目\
![将API添加到现有项目](/help/forms/assets/add-api-existing-project.png)

### 3.添加产品配置文件

产品配置文件为访问AEM资源的凭据提供权限（或授权）。

1. 选择与您的AEM实例URL (**)匹配的**&#x200B;产品配置文件`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`。

   * **服务类型** — 指定与AEM实例关联的服务或权限

   * **环境类型** — 指定环境是用于Author还是Publish服务

   * **项目XXX** — 标识Cloud Manager项目ID

   * **环境XXX** — 标识该项目中的特定环境ID

   >[!NOTE]
   >
   > 产品配置文件与特定AEM实例（项目+环境）关联。 始终选择与实例URL匹配的配置文件。

2. 单击&#x200B;**保存配置的 API**。API和产品配置文件已添加到您的项目中

   ![选择项目配置](/help/forms/assets/adc-add-product-profile.png)

### 4.生成并保存凭据

1. 在Adobe Developer Console中导航到项目
2. 单击&#x200B;**OAuth服务器到服务器**&#x200B;凭据
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

### 5.访问令牌生成

手动或以编程方式生成访问令牌：

>[!BEGINTABS]

>[!TAB 用于测试的] 

在Adobe Developer Console中手动生成访问令牌：

1. **导航到您的项目**
   1. 在Adobe Developer Console中，打开您的项目
   2. 单击&#x200B;**OAuth服务器到服务器**

2. **生成访问令牌**
   1. 单击项目API部分中的&#x200B;**“生成访问令牌”**&#x200B;按钮
   2. 复制生成的访问令牌

   ![生成访问令牌](/help/forms/assets/adc-access-token.png)

   >[!NOTE]
   >
   > 访问令牌仅在&#x200B;**24小时**&#x200B;内有效
   >用于生产[!TAB 的]

使用[Adobe IMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service) API以编程方式生成令牌：

**必需的凭据：**

* 客户端 ID
* 客户端密码
* 范围（通常： `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`）

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

>
>
> 要了解有关OAuth服务器到服务器实施以生成访问令牌和进行API调用的更多信息，请[单击此处](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)。

## 最佳实践：管理开发、暂存和生产凭据

* 始终使用单独的凭据进行“开发”、“暂存”和“生产”。

* 将每个凭据映射到正确的AEM环境URL。

* 安全地存储密钥，绝不会将其提交到源代码管理。

* 跟踪访问令牌的有效性，因为令牌仅在24小时内有效。

## 后续步骤

要了解如何设置同步Forms通信API的环境，请参阅[AEM Forms as a Cloud Service通信同步处理](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)。


## 相关文章

了解如何为同步（按需）和异步（批处理） Forms Communications API设置环境：

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="同步API" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="同步API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms Communications API — 同步">AEM Forms Communications API — 同步</a>
                    </p>
                    <p class="is-size-6">了解如何为同步（按需）Forms Communications API设置环境，以即时生成或处理文档。 </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms Communications API — 异步" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="异步API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="异步API">AEM Forms Communications API — 异步（批次）</a>
                    </p>
                    <p class="is-size-6">了解如何为异步（批处理）Forms Communications API设置环境，以计划方式生成或处理多个文档。</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


