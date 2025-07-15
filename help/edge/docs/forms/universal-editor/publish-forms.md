---
title: 发布适用于 Edge Delivery Services 的 AEM Forms。
description: 快速无缝地发布您的 Edge Delivery Services Forms。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 97%

---

# 将自适应表单发布到 Edge Delivery Services

<span class="preview">这是通过我们的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-hans#new-features">预发行渠道</a>提供的预发行功能。</span>


当表单最终完成并可供使用时，您就可以发布表单，使客户可以访问表单，进行数据收集和提交。发布后可确保表单在 Edge Delivery 上可用，使用户能够与之无缝交互。在此过程中，客户可以实时填写和提交表单，确保高效的数据捕获和简化的处理过程。

## 先决条件

* 使用 **Edge Delivery Services 模板**&#x200B;创建表单。[详细了解](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)有关创建基于 EDS 表单的信息。

## 发布表单

您可以按照以下步骤将任何&#x200B;**基于 EDS 的自适应表单**&#x200B;发布到 Edge Delivery：

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. 在编辑器中打开自适应表单，然后单击上方边栏上的&#x200B;**发布**图标。
   ![单击发布](/help/forms/assets/publish-icon-eds-form.png)

1. 单击&#x200B;**发布**&#x200B;后，会出现一个屏幕或弹出窗口，显示发布资产，包括表单标题。本例中使用了 **Wknd_Form** 模板。
   ![在单击发布上](/help/forms/assets/on-click-publish.png)

1. 再次单击&#x200B;**发布**，将出现一个确认弹出窗口，表明您的表单现已发布。
   ![发布成功](/help/forms/assets/publish-success.png)

1. 要检查表单发布状态，请再次单击&#x200B;**发布**。
   ![发布状态](/help/forms/assets/publish-status.png)

1. 要&#x200B;**取消发布**&#x200B;表单，请在编辑器中打开表单，单击右上角的三圆点菜单，然后单击&#x200B;**取消发布**。
   ![取消发布](/help/forms/assets/unpublish--form.png)

## 通过在 AEM 发布者中配置推荐人过滤器来启用 Edge Delivery 上的表单提交

要确保表单安全提交，您需要在 AEM 发布者中配置&#x200B;**推荐人过滤器**。该过滤器可确保只有来自 Edge Delivery 的被授权请求才能执行写入操作（POST、PUT、DELETE、COPY、MOVE），从而防止未经授权的修改。以下是在 AEM 发布者中配置推荐人过滤器的步骤：

### 在 Edge Delivery 中更新 AEM 实例 URL

修改表单块内 **constant.js** 文件中的 `submitBaseUrl`，指定 AEM 实例 URL：

**对于 Cloud 设置：**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```
**对于本地开发：**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### 更改 CORS 配置

调整 **CORS 设置**，允许来自 Edge Delivery 域的表单提交请求。详情请参阅 [CORS 配置指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)。

**CORS 配置示例：**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```
对于本地开发，请参阅[文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)，从&#x200B;**开发 UI 主机 URL** 中启用 CORS。

### 配置推荐人过滤器

通过 Cloud Manager 在 AEM Cloud Service 中设置&#x200B;**推荐人过滤器**。[了解](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)有关使用 Cloud Manager 在 AEM Cloud Service 实例上配置推荐人过滤器的更多信息。

**推荐人过滤器的 JSON 配置：**

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

此配置指定过滤哪些 HTTP 方法、允许哪些推荐人以及哪些用户代理被排除在过滤器之外。实施这些配置后，**通过 Edge Delivery 提交的表单**&#x200B;将受到保护，且仅限于授权来源。

### 访问您发布的自适应表单

现在，您可以通过 **Edge Delivery** 使用以下 URL 格式访问自适应表单：

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

例如，**Wknd-Form** 的 URL 为：

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


## 另请参阅

{{universal-editor-see-also}}

