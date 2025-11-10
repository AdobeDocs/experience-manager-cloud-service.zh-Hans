---
title: 如何设置JWT（JSON Web令牌）身份验证？
description: 了解如何为Adobe Experience Manager Forms as a Cloud Service配置JWT（JSON Web令牌）身份验证
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromToC: true
index: false
source-git-commit: 69704ca8de41c655b59ce6652a4a43b788ba75ec
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 3%

---


# JWT（JSON Web令牌）身份验证 — 已弃用

AEM Forms中的JWT身份验证，特别是与AEM as a Cloud Service的服务器端集成，涉及与AEM服务安全交互的特定过程。

## 注意事项

JWT生成的访问令牌将在当前证书过期后或2026年3月1日（以较早者为准）失效。 因此，您必须迁移集成才能使用新的[OAuth服务器到服务器凭据](/help/forms/oauth-api-authetication.md)。

将您的项目迁移到OAuth服务器到服务器凭据是一个简单的两步过程，可为您的应用程序和集成实现零停机迁移。 请阅读[迁移指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration)以迁移到OAuth服务器到服务器凭据。


## 先决条件

在开始之前，请确保满足以下先决条件：

* 确保您有权访问特定于您使用环境的[Adobe Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html)。
* 分配系统管理员或开发人员角色以访问Adobe Cloud Manager。

## 如何使用JWT凭据生成访问令牌？

请按照以下步骤操作，其中显示了如何从JWT凭据生成访问令牌。

1. **Adobe Cloud Manager**

   1. 登录到您的[Cloud Manager帐户](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html)。
   2. 在您选择的计划上，单击&#x200B;**[!UICONTROL 计划概述]**。

      ![Cloud Manager帐户](/help/forms/assets/jwt-cloud-manager-landing.png)

   3. 在程序上，单击三个圆点菜单，然后选择&#x200B;**[!UICONTROL Developer Console]**。

      ![开发人员控制台](/help/forms/assets/jwt-developer-console.png)

2. **AEM Developer Console**
   1. 登录AEM Developer Console
   2. 单击位于上方菜单栏上的&#x200B;**[!UICONTROL 集成]**。

      ![集成](/help/forms/assets/jwt-integrations.png)

   3. 单击选项&#x200B;**[!UICONTROL 创建新的技术帐户]**。

      ![创建新的技术帐户](/help/forms/assets/jwt-creae-new-tech-account.png)

   单击创建新的技术帐户后，生成访问令牌（如客户端ID和客户端密钥）所需的信息以及其他技术帐户信息（包括私钥、公钥、过期日期）均会生成。

   ![JWT凭据](/help/forms/assets/jwt-credentials.png)


3. 生成并保存凭据

   1. 记录API凭据

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

4. 访问令牌生成

   使用Adobe IMS API以编程方式生成令牌：

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

您现在可以使用生成的访问令牌为开发、暂存或生产环境进行API调用。

## 后续步骤

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


