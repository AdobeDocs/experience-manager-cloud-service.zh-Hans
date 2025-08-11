---
title: 使用Edge Delivery Services发布自适应Forms
description: 了解如何使用Edge Delivery Services发布、配置和访问自适应Forms以用于生产。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
keywords: [发布表单、Edge Delivery Services、表单配置、CORS、反向链接筛选条件]
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: 746
ht-degree: 2%

---

# 使用Edge Delivery Services发布自适应Forms

发布自适应表单后，该表单便可在Edge Delivery Services上供最终用户访问和提交。 此过程包括三个主要阶段：发布表单、配置安全设置和访问实时表单。

**您将完成的内容：**

- 将表单发布到Edge Delivery Services
- 配置表单提交的安全设置
- 访问并验证已发布的表单
- 设置正确的URL路由和CORS策略

## 先决条件

- 使用Edge Delivery Services模板创建的自适应表单
- 表单已测试并可供生产使用
- AEM Forms作者权限
- Cloud Manager访问权限（用于生产配置）
- 开发人员对表单块代码的访问权限（用于提交设置）

## 发布流程概述

将表单发布到Edge Delivery Services的过程分为三个阶段：

- **阶段1：表单发布** — 将表单发布到CDN并验证发布状态
- **第2阶段：安全配置** — 设置CORS策略和反向链接筛选器以便安全提交
- **阶段3：访问和验证** — 测试表单功能并验证完整的工作流

每个阶段都以上一个阶段为基础，以确保安全且功能正常的部署。

### 第1阶段：发布表单

+++ 步骤1：启动发布

1. **访问您的表单**：在通用编辑器中打开您的自适应表单
2. **开始发布**：单击工具栏中的&#x200B;**发布**&#x200B;图标

   ![单击发布](/help/forms/assets/publish-icon-eds-form.png)

+++


+++ 第2步：查看和确认

1. **审阅发布资产**：系统将显示所有正在发布的资产，包括您的表单

   ![在单击发布上](/help/forms/assets/on-click-publish.png)

2. **确认发布**：单击&#x200B;**发布**&#x200B;以继续
3. **验证是否成功**：查找确认消息

   ![发布成功](/help/forms/assets/publish-success.png)

+++


+++ 步骤3：验证发布状态

**检查状态**：再次单击&#x200B;**发布**&#x200B;图标以查看当前状态

![发布状态](/help/forms/assets/publish-status.png)

**验证检查点：**

- 表单在编辑器中显示“已发布”状态
- 发布过程中无错误消息
- 表单显示在已发布的资源列表中

+++


+++ 管理已发布的Forms

**要取消发布表单：**

1. 在编辑器中打开表单
2. 单击右上角的三个圆点菜单(⋯)
3. 选择&#x200B;**取消发布**

![取消发布表单](/help/forms/assets/unpublish--form.png)

+++


### 阶段2：配置安全设置

+++ 为什么需要安全配置

要启用安全表单提交，您必须配置安全设置，以便：

- 允许Edge Delivery Services向AEM提交数据
- 防止对您的AEM实例的未授权访问
- 为表单提交启用CORS（跨源资源共享）
- 筛选请求以仅允许合法的Edge Delivery域

>[!IMPORTANT]
>
>生产环境需要&#x200B;****：这些配置是表单提交在生产环境中工作的必备配置。

+++



+++ 步骤1：配置表单提交URL

**用途**：直接向AEM实例提交表单

您的Edge Delivery Services项目中的&#x200B;**文件位置**： `blocks/form/constant.js`

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

- 使用正确的AEM发布URL更新了`constant.js`文件
- URL与您的环境（生产、暂存或本地）匹配
- URL中没有尾随斜杠

+++



+++ 步骤2：配置CORS设置

**目的**：允许来自Edge Delivery Services域的表单提交请求

**实施**：将CORS配置添加到您的AEM Dispatcher或Apache配置

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**验证检查点：**

- 应用于Dispatcher配置的CORS规则
- 包括所有必需域(localhost、hlx.page、hlx.live)
- 部署到目标环境的配置

**参考文档：**

- [CORS配置指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [反向链接筛选条件文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ 步骤3：配置反向链接过滤器

**目的**：将写入操作限制为授权的Edge Delivery Services域

**实施方法**：通过AEM as a Cloud Service中的Cloud Manager进行配置

**配置文件**：添加到项目的OSGi配置

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

**配置划分：**

- **`allow.empty`**：拒绝没有反向链接标头的请求
- **`allow.hosts.regexp`**：允许来自Edge Delivery Services域的请求
- **`filter.methods`**：将筛选应用于这些HTTP方法
- **`exclude.agents.regexp`**：从筛选中排除的用户代理

**验证检查点：**

- 通过Cloud Manager部署的反向链接筛选条件配置
- 在AEM发布实例上处于活动状态的配置
- 测试表单提交工作来自Edge Delivery Services域
- 阻止未授权的域提交表单

**参考文档：**

- [通过Cloud Manager配置反向链接筛选器](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### 第3阶段：访问已发布的表单



+++ Edge Delivery Services的URL结构

**标准URL格式：**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**URL组件：**

- **`<branch>`**： Git分支名称（通常为`main`）
- **`<repo>`**：存储库名称
- **`<owner>`**： GitHub组织或用户名
- **`<form_name>`**：您的表单名称（小写，带连字符）

**特定于环境的URL：**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ 最终验证步骤

**验证表单可访问性：**

1. **正在加载测试表单**：请访问您的表单URL并确认其正确加载
2. **测试表单提交**：填写并提交表单以验证数据处理
3. **检查响应式设计**：测试不同设备和屏幕大小上的表单
4. **验证安全性**：确保CORS和反向链接筛选器正常工作

**预期结果：**

- 表单加载无错误
- 所有表单字段均正确呈现
- 表单提交流程成功
- 数据会显示在配置的目标中（电子表格、电子邮件等）
- 没有与CORS或安全策略相关的控制台错误

+++


## 后续步骤


- [配置表单提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)
- [表单的样式和主题](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [创建响应式表单布局](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [添加reCAPTCHA保护](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



