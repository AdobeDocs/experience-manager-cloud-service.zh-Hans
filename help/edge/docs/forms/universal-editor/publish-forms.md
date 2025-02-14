---
title: 发布适用于Edge Delivery Services的AEM Forms。
description: 快速无缝地发布Edge Delivery Services表单。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ac005e5bc143c35eb29ba177a26aa6cc33897db4
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# 将自适应表单发布到Edge Delivery Services

当您的表单最终完成并可供使用时，您可以发布该表单，以便客户能够访问它来收集和提交数据。 发布功能可确保表单在Edge Delivery上可用，从而使用户能够无缝地与之交互。 此流程允许客户实时填写并提交表单，以确保高效的数据捕获和简化的处理。

## 先决条件

* 使用&#x200B;**Edge Delivery Services (EDS)模板**&#x200B;创建的表单。 [了解更多](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)有关创建基于EDS的表单的信息。

## 发布您的表单

您可以按照以下步骤将任何基于&#x200B;**EDS的自适应表单**&#x200B;发布到Edge Delivery：

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. 在编辑器中打开自适应表单，然后单击上边栏上的&#x200B;**发布**图标。
   ![单击“发布”](/help/forms/assets/publish-icon-eds-form.png)

1. 单击&#x200B;**发布**&#x200B;后，将显示一个屏幕或弹出窗口，其中显示发布资产，包括表单标题。 在此示例中，使用了&#x200B;**Wknd_Form**模板。
   ![单击“发布”](/help/forms/assets/on-click-publish.png)

1. 再次单击&#x200B;**发布**，将显示一个确认弹出窗口，指示您的表单现已发布。
   ![发布成功](/help/forms/assets/publish-success.png)

1. 要检查表单的发布状态，请再次单击&#x200B;**发布**。
   ![发布状态](/help/forms/assets/publish-status.png)

1. 要&#x200B;**取消发布**&#x200B;表单，请在编辑器中打开您的表单，单击右上角的三个圆点菜单，然后单击&#x200B;**取消发布**。
   ![取消发布](/help/forms/assets/unpublish--form.png)

## 通过为Edge Delivery Publisher配置反向链接筛选条件，在AEM上启用表单提交

为确保表单提交安全，您需要在AEM Publisher中配置&#x200B;**反向链接筛选条件**。 此过滤器可确保只有来自Edge Delivery的授权请求才能执行写入操作(POST、PUT、DELETE、COPY、MOVE)，从而防止未经授权的修改。 以下是为AEM Publisher配置反向链接筛选条件的给定步骤：

### 在Edge Delivery中更新AEM实例URL

修改表单块中&#x200B;**constant.js**&#x200B;文件中的`submitBaseUrl`以指定AEM实例URL：

云设置的&#x200B;**：**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```
用于本地开发的&#x200B;**：**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### 修改CORS配置

调整&#x200B;**CORS设置**&#x200B;以允许来自Edge Delivery域的表单提交请求。 有关详细信息，请参阅[CORS配置指南](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)。

**示例CORS配置：**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```
对于本地开发，请参阅[文档](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)以启用&#x200B;**开发UI主机URL**&#x200B;中的CORS。

### 配置反向链接过滤器

通过Cloud Manager在AEM云服务中设置&#x200B;**反向链接筛选条件**。 [了解更多](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)关于使用Cloud Manager在AEM Cloud Service实例上配置反向链接筛选器的信息。

反向链接筛选条件的&#x200B;**JSON配置：**

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
    "https://.*\\.hlx\\.page:443",
    "https://.*\\.hlx\\.live:443"
  ],
  "filter.methods": [
    "POST",
    "PUT",
    "DELETE",
    "COPY",
    "MOVE"
  ],
  "exclude.agents.regexp": [
    ""
  ]
}
```

此配置指定过滤哪些HTTP方法、允许哪些反向链接以及要从过滤器中排除哪些用户代理。 通过实施这些配置，将保护通过Edge Delivery提交的&#x200B;**表单**&#x200B;并限制仅向授权源提交。

### 访问您发布的自适应表单

自适应表单现在可通过以下URL格式通过&#x200B;**Edge Delivery**&#x200B;访问：

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

例如，**Wknd-Form**&#x200B;的URL是：

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


















