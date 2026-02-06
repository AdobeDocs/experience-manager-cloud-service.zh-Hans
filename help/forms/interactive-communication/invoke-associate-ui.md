---
title: 集成运行时交互式通信的关联UI
description: 了解如何将AEM Forms关联UI与您的应用程序集成，以使面向客户的专业人士能够在Publish实例上实时生成个性化的交互式通信。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
hidefromtoc: true
source-git-commit: b76f6dfe2462cec187d549234e9050f8ca9a8cdf
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 2%

---


# 在应用程序中集成关联UI

<span>交互式通信功能在早期采用者计划下可用。 将工作地址中的电子邮件发送至`aem-forms-ea@adobe.com`以请求访问权限。</span>

本文说明如何将关联UI与您的应用程序集成，从而使面向客户的专业人员（如现场助理和服务代理）能够在Publish实例上实时生成个性化的交互式通信。

## 先决条件

在将关联UI与您的应用程序集成之前，请确保您已：

- 交互式通信已创建和发布
- 已启用弹出窗口支持的浏览器
- 关联[用户必须属于Forms-associates组](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups)
- 使用AEM[支持的任何](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/authentication)身份验证机制（例如SAML 2.0、OAuth或自定义身份验证处理程序）配置的身份验证

>[!NOTE]
>
>- 本文演示了将SAML 2.0和[Microsoft Entra ID (Azure AD)用作身份提供程序](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings)的身份验证配置。
>- 对于关联UI，需要除[SAML 2.0身份验证](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)文章中说明的标准设置之外的其他SAML配置。 有关详细信息，请参阅[关联UI的其他SAML配置](#additional-saml-configurations-for-associate-ui)部分。

### 关联UI的其他SAML配置

为关联UI配置SAML 2.0身份验证时，必须在OSGi配置文件中应用以下特定设置。

#### SAML身份验证处理程序

SAML身份验证处理程序是一个OSGi工厂配置，它允许为不同的资源树使用多个SAML配置。 这支持多站点AEM部署，并允许您向现有SAML设置添加关联UI资源。

在`com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json`中创建文件`ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`：

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login"
    "idpUrl": "https://login.microsoftonline.com/{azure-tenant-id}/saml2",
    "idpCertAlias": "{your-certificate-alias}",
    "idpIdentifier": "https://sts.windows.net/{azure-tenant-id}/",
    "userIDAttribute": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
    "createUser": true,
    "userIntermediatePath": "saml",
    "synchronizeAttributes": [
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname=profile/givenName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname=profile/familyName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress=profile/email"
      ],
      "addGroupMemberships": true,
      "defaultGroups": ["forms-associates"],
      "defaultRedirectUrl": "/libs/fd/associate/ui.html",
      "idpHttpRedirect": false,
      "service.ranking": 5002
  }
```

| 属性 | 描述 |
|----------|-------------|
| `path` | 必须为关联UI设置为`/libs/fd/associate` |
| `defaultGroups` | 设置为`forms-associates`以自动将用户分配给所需的组 |
| `defaultRedirectUrl` | 将经过身份验证的用户重定向到关联UI |
| `idpHttpRedirect` | 对于SP启动的流，必须为`false` |
| `idpCertAlias` | 必须完全匹配信任存储区中的证书别名（区分大小写） |

#### Sling身份验证程序

Sling Authenticator强制进行身份验证以访问发布上的关联UI资源。

更新`org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json`中的文件`ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`：

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Dispatcher筛选器

添加以下规则以确保Interactive Communications API和关联UI在发布实例上正确运行。

如果尚未存在，请将以下规则添加到您的`dispatcher/src/conf.dispatcher.d/filters/filters.any`文件：

```json
  # Allow Interactive Communications APIs and Associate UI
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/adobe/communications" }
  /XXXX { /type "allow" /method '(GET|POST|OPTIONS)' /url "/adobe/communications/*" }
  /XXXX { /type "allow" /method "GET" /url "/content/dam/fd:fonts/*" }
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/libs/fd/associate/*" }
```

>[!NOTE]
>
> 将`XXXX`替换为现有`filters.any`文件中使用的相应数字序列。

## 在发布实例上调用关联UI

本节将指导您从自己的应用程序中启动关联UI。 按照以下步骤快速入门 — 从现成的示例HTML页面开始，然后为您的环境配置它。

### 步骤1：开始创建示例HTML页面

要快速测试和了解关联UI集成的工作方式，请使用以下示例HTML页面。 将此代码复制到HTML文件中，并在浏览器中将其打开。

此示例提供了一个简单的表单界面，您可以在其中输入交互式通信详细信息，并通过一次单击启动关联UI。

```html
<!DOCTYPE html>
<html>
<head>
  <title>Associate UI Integration</title>
  <style>
    body {
      font-family: sans-serif;
      max-width: 600px;
      margin: 50px auto;
      padding: 20px;
    }
    .form-group {
      margin: 20px 0;
    }
    label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }
    input, textarea {
      width: 100%;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
      box-sizing: border-box;
    }
    textarea {
      height: 80px;
      font-family: monospace;
    }
    button {
      padding: 10px 20px;
      margin: 5px;
      cursor: pointer;
      border-radius: 4px;
    }
    .btn-primary {
      background: #007bff;
      color: white;
      border: none;
    }
    .btn-primary:hover {
      background: #0056b3;
    }
    .error {
      color: red;
      font-size: 12px;
      display: none;
    }
  </style>
</head>
<body>
  <h1>Launch Associate UI</h1>

  <form id="form">
    <div class="form-group">
      <label>IC ID *</label>
      <input type="text" id="icId" placeholder="Enter Interactive Communication ID" required>
    </div>

    <div class="form-group">
      <label>Prefill Service</label>
      <input type="text" id="serviceName" placeholder="e.g., CustomerDataService">
    </div>

    <div class="form-group">
      <label>Service Parameters (JSON)</label>
      <textarea id="serviceParams" placeholder='{"customerId": "12345"}'>{}</textarea>
      <span id="paramsError" class="error">Invalid JSON format</span>
    </div>

    <div class="form-group">
      <label>Options (JSON)</label>
      <textarea id="options" placeholder='{"mode": "edit", "locale": "en_US"}'>{}</textarea>
      <span id="optionsError" class="error">Invalid JSON format</span>
    </div>

    <button type="button" onclick="reset()">Reset</button>
    <button type="button" class="btn-primary" onclick="launch()">Launch Associate UI</button>
  </form>

  <script>
    // Replace with your AEM Publish instance URL
    const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';

    function validateJSON(str, errorId) {
      const err = document.getElementById(errorId);
      try {
        const obj = JSON.parse(str || '{}');
        err.style.display = 'none';
        return obj;
      } catch (e) {
        err.style.display = 'block';
        return null;
      }
    }

    function launch() {
      const icId = document.getElementById('icId').value.trim();
      if (!icId) {
        alert('IC ID is required');
        return;
      }

      const params = validateJSON(document.getElementById('serviceParams').value, 'paramsError');
      const opts = validateJSON(document.getElementById('options').value, 'optionsError');

      if (!params || !opts) {
        alert('Please fix JSON errors before launching');
        return;
      }

      const data = {
        id: icId,
        prefill: {
          serviceName: document.getElementById('serviceName').value.trim(),
          serviceParams: params
        },
        options: opts
      };

      const win = window.open(AEM_URL, '_blank');
      if (!win) {
        alert('Pop-up blocked. Please enable pop-ups for this site.');
        return;
      }

      const handler = (e) => {
        if (e.data && e.data.type === 'READY' && e.data.source === 'APP') {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      };

      window.addEventListener('message', handler);

      // Fallback timeout in case READY message is missed
      setTimeout(() => {
        if (win && !win.closed) {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      }, 1000);
    }

    function reset() {
      document.getElementById('form').reset();
      document.getElementById('serviceParams').value = '{}';
      document.getElementById('options').value = '{}';
      document.getElementById('paramsError').style.display = 'none';
      document.getElementById('optionsError').style.display = 'none';
    }
  </script>
</body>
</html>
```

### 步骤2：配置发布实例URL

在启动关联UI之前，您需要将示例指向AEM Forms Cloud Service发布实例。

在上面的HTML示例中，在`<script>`部分中找到以下行：

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

将占位符值替换为您的实际环境详细信息：
- `{program-id}`：您的AEM Cloud Service项目ID
- `{env-id}`：您的环境ID

例如，如果您的项目ID为`12345`，环境ID为`67890`，则URL将变为：

```javascript
const AEM_URL = 'https://publish-p12345`-e67890.adobeaemcloud.com/libs/fd/associate/ui.html';
```

>[!NOTE]
>
> 为安全起见，交互式通信ID、预填充服务和服务参数等参数不会通过URL进行传递。 相反，这些参数是使用JavaScript的`postMessage` API安全传递的。

### 步骤3：了解JavaScript集成功能

示例HTML使用以下JavaScript函数来启动关联UI。 此函数验证IC ID、构造数据有效负载、在新的浏览器窗口中打开关联UI，并使用浏览器的`postMessage` API发送数据。

```javascript
function launchAssociateUI(icId, prefillService, prefillParams, options) {
  if (!icId) {
    console.error('IC ID required');
    return;
  }

  const data = {
    id: icId,
    prefill: {
      serviceName: prefillService || '',
      serviceParams: prefillParams || {}
    },
    options: options || {}
  };

  const AEM_URL = 'https://your-aem.adobeaemcloud.com/libs/fd/associate/ui.html';
  const win = window.open(AEM_URL, '_blank');

  if (!win) {
    alert('Please enable pop-ups for this site');
    return;
  }

  const readyHandler = (event) => {
    if (event.data && event.data.type === 'READY' && event.data.source === 'APP') {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  };

  window.addEventListener('message', readyHandler);

  // Fallback timeout in case READY message is missed
  setTimeout(() => {
    if (win && !win.closed) {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  }, 1000);
}
```

该函数接受四个参数：IC ID（必需）、预填充服务名称、预填充服务参数和其他选项。 这些参数将结构化到数据有效负载中，如下所述。

### 步骤4：了解数据有效载荷结构

**有效负载格式：**

```javascript
const data = {
  id: "your-ic-id",              // Required: Interactive Communication ID
  prefill: {                      // Optional: Data to prefill the IC
    serviceName: "YourService",
    serviceParams: { key: "value" }
  },
  options: {}                     // Optional: Additional configuration options
};
```

**有效负载组件：**

| 组件 | 必需 | 描述 |
|-----------|----------|-------------|
| `id` | 是 | 要加载的交互式通信(IC)的标识符 |
| `prefill` | 可选 | 包含用于数据预填充的服务配置 |
| `prefill.serviceName` | 可选 | 要调用以预填充数据的表单数据模型服务的名称 |
| `prefill.serviceParams` | 可选 | 传递到预填充服务的键值对 |
| `options` | 可选 | PDF渲染支持的其他属性 — 区域设置、包括Attachments、embedFonts、makeAccessible |

#### 数据有效负载示例

**最小有效负载（仅限IC ID）**

当不需要预填充数据时，使用此项：

```json
{
  "id": "12345",
  "prefill": { 
    "serviceName": "", 
    "serviceParams": {} 
  },
  "options": {}
}
```

**包含预填充数据**

使用它动态地向IC填充客户数据：

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": {}
}
```

**具有PDF渲染选项**

使用此选项可指定其他渲染选项：

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": { 
      "locale": "en_US",
      "includeAttachments": "true",
      "webOptimized": "false",
      "embedFonts": "false",
      "makeAccessible": "false"
  }
}
```

### 步骤5：输入IC ID并启动关联UI

现在，您可以使用示例HTML页面启动关联UI：

1. **输入IC ID**：在&#x200B;**IC ID**&#x200B;字段中，输入已发布的交互式通信的标识符。 这是唯一的必填字段。

2. **配置预填充服务**（可选）：如果要使用动态数据预填充IC，请在&#x200B;**预填充服务**&#x200B;字段中输入表单数据模型服务名称。 例如，将`FdmTestData`用于示例数据，或将`IC-FDM`用于测试数据。

3. **添加服务参数**（可选）：在&#x200B;**服务参数(JSON)**&#x200B;字段中，输入带有预填充服务所需参数的JSON对象。 例如：

   ```json
   {"customerId": "101", "accountNumber": "ACC-98765"}
   ```

4. **设置PDF选项**（可选）：在&#x200B;**选项(JSON)**&#x200B;字段中，配置区域设置、附件或辅助功能设置等渲染选项。

5. **单击“启动关联UI”**：单击“启动关联UI”**&#x200B;**&#x200B;按钮。 此时将打开一个新浏览器窗口，其中显示与交互式通信预先加载的关联UI 。

>[!NOTE]
>
> 如果该窗口未打开，请检查浏览器是否允许显示此站点的弹出窗口。

## 疑难解答

### 已阻止弹出窗口

**问题**：“关联UI”窗口未打开。

**解决方案**：
- 在浏览器设置中为域启用弹出窗口
- 确保从用户操作（例如，按钮单击）中调用`window.open()`
- 使用不同的浏览器测试以识别阻止行为

### 数据未加载

**问题**：交互式通信打开，但数据未填充。

**解决方案**：
- 验证IC ID是否正确，以及IC是否已发布
- 检查浏览器控制台是否显示 JavaScript 错误
- 确保`postMessage`结构与规范完全匹配
- 验证表单数据模型服务是否已正确配置

### 身份验证错误

**问题**：打开关联UI时，用户收到身份验证错误。

**解决方案**：
- 在发布实例上配置SAML 2.0身份验证
- 验证用户是否属于&#x200B;**forms-associates**&#x200B;组
- 检查会话超时设置

### CORS错误

**问题**：控制台中存在跨源资源共享错误。

**解决方案**：
- 对于开发：在`'*'`中使用`postMessage`作为目标来源
- 用于生产：指定应用程序的确切起源URL
- 确保发布实例CORS设置允许您的应用程序域

<!--## Best Practices

When implementing the Associate UI integration, follow these best practices:

1. **Validation**: Always validate the IC ID and JSON payload before sending
2. **Error Handling**: Implement proper error handling for `window.open()` failures
3. **User Experience**: Display a loading indicator while the Associate UI initializes
4. **Memory Management**: Remove event listeners after initialization to prevent memory leaks
5. **Testing**: Test the integration with popup blockers enabled to ensure graceful handling
6. **User Permissions**: Verify users have appropriate access to the forms-associates group-->

## 另请参阅

- [在交互式通信编辑器中关联UI](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [云端交互式通信](/help/forms/early-access-ea-features.md#interactive-communications-on-cloud)
- [抢先体验功能](/help/forms/early-access-ea-features.md)