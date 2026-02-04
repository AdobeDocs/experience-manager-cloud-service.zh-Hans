---
title: 在发布实例上调用关联UI
description: 了解如何在发布实例上集成和调用AEM Forms关联UI，以使面向客户的专业人员能够实时生成个性化的交互式通信。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
hidefromtoc: true
source-git-commit: 2f3badafddfdfe1dd21eb74be7189102aa0474bc
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 2%

---


# 使用关联UI生成个性化通信

<span>交互式通信功能在早期采用者计划下可用。 将工作地址中的电子邮件发送至`aem-forms-ea@adobe.com`以请求访问权限。</span>

关联UI可直接在发布实例上调用，从而使面向客户的专业人员（如现场助理和服务代理）能够在客户交互期间实时生成个性化通信。

下表描述了各种真实情景，其中关联UI可用于向客户发送个性化消息：

| 行业 | 用例 |
|----------|----------|
| **金融服务** | 在客户会议期间生成实时贷款确认函、账户报表和风险状况摘要 |
| **保险** | 在服务柜台制作即时保险证明卡和索赔处理摘要 |
| **医疗保健** | 使用计算出的copay金额和时间表创建患者治疗计划汇总 |
| **政府** | 当场生成警方核查报告、公民服务收据和案件更新摘要 |

## 先决条件

在将关联UI与您的应用程序集成之前，请确保您已：

- 交互式通信已创建和发布
- 已启用弹出窗口支持的浏览器
- 关联[用户必须属于Forms-associates组](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups)
- 已配置身份验证 — [SAML 2.0](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)

>[!NOTE]
>
> 对于关联UI，需要除[SAML 2.0身份验证](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)文章中说明的标准设置之外的其他SAML配置。 有关详细信息，请参阅[关联UI的其他SAML配置](#additional-saml-configurations-for-associate-ui)部分。

### 关联UI的其他SAML配置

为关联UI配置SAML 2.0身份验证时，必须在OSGi配置文件中应用以下特定设置。

#### SAML身份验证处理程序

在`com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json`中创建文件`ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`：

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login",
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

更新`org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json`中的文件`ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`：

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Dispatcher筛选器

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

要从应用程序调用关联UI，请配置发布实例URL，准备数据有效负载，然后使用集成函数在新的浏览器窗口中启动关联UI。

### 步骤1：配置发布实例URL

可通过您的AEM Forms Cloud Service发布实例上的特定端点访问关联UI：

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

将`{program-id}`和`{env-id}`替换为您的实际环境值。

### 步骤2：准备数据有效负载

使用以下格式构建数据有效负载：

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
| `prefill` | 可选 | 包含用于数据预填充的服务配置。 |
| `prefill.serviceName` | 可选 | 要调用以预填充数据的表单数据模型服务的名称 |
| `prefill.serviceParams` | 可选 | 传递到预填充服务的键值对 |
| `options` | 可选 | PDF渲染支持的其他属性 — 区域设置、includeAttachments、embedFonts、makeAccessible |

### 步骤3：实施集成功能

创建JavaScript函数以启动关联UI并处理消息通信：

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

### 步骤4：调用函数

使用适当的参数调用函数：

```javascript
// Basic invocation with IC ID only
launchAssociateUI('12345', '', {}, {});

// With prefill service
launchAssociateUI('12345', 'FdmTestData', 
  { customerId: '101'}, {});

// With all parameters
launchAssociateUI('12345', 'FdmTestData', 
  { policyNumber: 'POL-123' }, 
  { locale: 'en', acrobatVersion: 'Acrobat_11' });
```

## 测试与示例HTML页面的集成

为了观察关联UI如何出现在前端并测试您的集成，以下是一个简单的HTML示例。 此示例页面允许您输入IC ID、配置预填充服务参数、设置PDF选项并在发布实例上启动关联UI。

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

### 示例的工作原理

1. **IC ID字段**：输入交互式通信标识符（必需）
2. **预填充服务**：指定用于预填充数据的表单数据模型服务名称
3. **服务参数**：输入要传递给预填充服务的JSON对象
4. **选项**：输入PDF的配置选项，例如，区域设置、includeAttachments、embedFonts、makeAccessible
5. **启动按钮**：在新窗口中打开关联UI并发送初始化数据

## 数据有效负载示例

### 最小有效负载（仅限IC）

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

### 包含预填充数据

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

### 带选项配置

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
      locale: "en_US",
      includeAttachments: "true",
      webOptimized: "false",
      embedFonts: "false",
      makeAccessible: "false"
  }
}
```

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