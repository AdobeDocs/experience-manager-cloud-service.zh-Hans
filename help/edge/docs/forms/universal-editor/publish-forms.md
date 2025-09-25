---
title: 通过 Edge Delivery Services 发布自适应表单
description: 了解如何使用 Edge Delivery Services 发布、配置和访问自适应表单，以用于生产。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
keywords: 发布表单，Edge Delivery Services，表单配置，CORS，引荐来源过滤器
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '746'
ht-degree: 100%

---

# 通过 Edge Delivery Services 发布自适应表单

发布自适应表单可使其在 Edge Delivery Services 上供最终用户访问和提交。此过程包括三个主要阶段：发布表单、配置安全设置、访问上线表单。

**您将了解：**

- 将表单发布到 Edge Delivery Services
- 为表单提交配置安全设置
- 访问并验证您发布的表单
- 设置适当的 URL 路由和 CORS 策略

## 先决条件

- 已使用 Edge Delivery Services 模板创建了自适应表单
- 表单已经过测试，并准备好用于生产
- AEM Forms 作者权限
- Cloud Manager 访问权限（用于生产配置）
- 开发人员对表单块代码的访问权限（用于提交设置）

## 发布流程概述

将表单发布到 Edge Delivery Services 采用一个三阶段方法：

- **第一阶段：表单发布** - 将您的表单发布到内容传递网络并验证发布状态
- **第二阶段：安全配置** - 设置 CORS 策略和引荐来源过滤器以确保安全提交
- **第三阶段：访问和验证** - 测试表单功能并验证完整的工作流

每个阶段都以前一个阶段为基础，以确保安全、正确地部署。

### 阶段 1：发布表单

+++ 步骤 1：开始发布

1. **访问您的表单**：在通用编辑器中打开自适应表单
2. **开始发布**：点击工具栏中的&#x200B;**发布**&#x200B;图标

   ![单击发布](/help/edge/docs/forms/universal-editor/assets/publish-form-ue.png)

+++


+++ 步骤 2：审阅后确认

1. **审阅发布资产**：系统显示所有正在发布的资产，包括您的表单

   ![在单击发布上](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-review.png)

2. **确认发布**：点击&#x200B;**发布**&#x200B;以继续
3. **验证成功**：查看确认消息

   ![发布成功](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-success.png)

+++


+++ 步骤 3：验证发布状态

**检查状态**：再次点击&#x200B;**发布**&#x200B;图标，查看当前状态

![发布状态](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-validate.png)

**验证检查点：**

- 在编辑器中，表单显示“已发布”状态
- 发布过程中没有出现任何错误消息
- 表单出现在已发布资产列表中

+++


+++ 管理已发布的表单

**要取消发布表单：**

1. 在编辑器中打开表单
2. 点击右上角的三圆点菜单（⋯）
3. 选择&#x200B;**取消发布**

![取消发布表单](/help/edge/docs/forms/universal-editor/assets/unpublish-ue.png)

+++


### 阶段 2：配置安全设置

+++ 为什么一定需要安全配置

要启用安全表单提交，您必须配置以下安全设置：

- 允许 Edge Delivery Services 将数据提交给 AEM
- 防止您的 AEM 实例在未经授权的情况下被访问
- 为表单提交启用 CORS（跨来源资源共享）
- 过滤请求，仅允许合法的 Edge Delivery 域

>[!IMPORTANT]
>
>**生产环境中需要**：这些配置对于在生产环境中的表单提交是必需的。

+++



+++ 步骤 1：配置表单提交 URL

**目的**：将表单直接提交到您的 AEM 实例

**文件位置**：`blocks/form/constant.js` 在您的 Edge Delivery Services 项目中

**配置示例：**

```javascript
// Production Environment
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';

// Local Development Environment  
export const submitBaseUrl = 'http://localhost:4503';

// Staging Environment
export const submitBaseUrl = 'https://publish-staging-p120-e12.adobeaemcloud.com';
```

**验证检查点：**

- 通过正确的 AEM 发布 URL 更新了 `constant.js` 文件
- URL 与您的（生产、暂存或本地）环境匹配
- URL 中没有结尾斜杠

+++



+++ 步骤 2：配置 CORS 设置

**目的**：允许来自 Edge Delivery Services 域的表单提交请求

**实施**：将 CORS 配置添加到您的 AEM dispatcher 或 Apache 配置

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**验证检查点：**

- dispatcher 配置已应用 CORS 规则
- 包含所有必需的域（localhost、hlx.page、hlx.live）
- 配置已部署到目标环境

**参考文档：**

- [CORS 配置指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [引荐来源过滤器文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ 步骤 3：配置引荐来源过滤器

**目的**：将写入操作限制在已授权的 Edge Delivery Services 域中

**实施方法**：通过 AEM as a Cloud Service 中的 Cloud Manager 配置

**配置文件**：添加到项目的 OSGi 配置

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

**配置细分：**

- **`allow.empty`**：拒绝没有引荐来源标头的请求
- **`allow.hosts.regexp`**：允许来自 Edge Delivery Services 域的请求
- **`filter.methods`**：在这些 HTTP 方法中进行筛选
- **`exclude.agents.regexp`**：筛选时排除在外的用户代理

**验证检查点：**

- 通过 Cloud Manager 部署了引荐来源过滤器配置
- AEM 发布实例上的配置已激活
- 测试从 Edge Delivery Services 域提交表单是否正常运作
- 未经授权的域被禁止提交表单

**参考文档：**

- [通过 Cloud Manager 配置引荐来源过滤器](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### 阶段 3：访问您已发布的表单



+++ Edge Delivery Services 的 URL 结构

**标准 URL 格式：**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**URL 组成：**

- **`<branch>`**：Git 分支名称（通常是 `main`）
- **`<repo>`**：存储库名称
- **`<owner>`**：GitHub 组织或用户名
- **`<form_name>`**：您的表单名称（小写，使用连字符）

**环境特有的 URL：**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ 最终验证步骤

**验证表单的无障碍可访问性：**

1. **测试表单加载**：访问您的表单 URL，确认其正确加载
2. **测试表单提交**：填写并提交表单，验证数据处理
3. **检查响应式设计**：在不同的设备和屏幕尺寸上测试表单
4. **验证安全性**：确保 CORS 和引荐来源过滤器正常工作

**预期结果：**

- 表单加载无误
- 所有表单字段均正确显现
- 成功处理了表单提交
- 数据出现在所配置的目标中（电子表格、电子邮件等）
- 没有与 CORS 或安全策略相关的控制台错误

+++


## 后续步骤


- [配置表单提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)
- [表单的样式和主题](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [创建响应式表单布局](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [添加 reCAPTCHA 保护](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



