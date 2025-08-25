---
title: 对Edge Delivery Services表单提交中的403禁止错误进行故障诊断
description: 了解如何诊断和解决在从Edge Delivery Services提交表单到AEM Publish时出现403禁止显示的错误。 本指南涵盖的常见原因包括CORS、Dispatcher规则和反向链接筛选条件问题。
feature: Edge Delivery Services
role: Admin, Developer
exl-id: f397e059-f1b3-4afa-bd38-8f5fc591bb22
source-git-commit: d457bf9af377176222c2b96816fbbc4265e6b167
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 3%

---

# 对Edge Delivery Services表单提交中的403禁止错误进行故障诊断 {#troubleshooting-403-forbidden-edge-delivery}

将表单从Edge Delivery Services提交到AEM Publish时，您可能会遇到&#x200B;**403 Forbidden**&#x200B;错误。 此错误表示服务器拒绝处理请求，通常是因为安全配置。 本文可帮助您识别并解决此问题的最常见原因。

## 问题描述

用户将表单从Edge Delivery Services提交到AEM Publish时遇到&#x200B;**403 Forbidden**&#x200B;错误。 错误显示为：

- HTTP状态代码： 403
- 错误消息：“禁止访问”或“访问被拒绝”
- 表单提交失败，无法访问AEM提交servlet

在Edge Delivery Services集成中，当托管在Edge域(`.aem.live`、`.aem.page`、`.hlx.page`、`.hlx.live`)上的表单尝试将数据提交到AEM发布实例时，经常会发生此问题。

>[!IMPORTANT]
>
>通过重新设置，可以使用同一存储库来托管多个站点。 每个站点域必须单独添加到允许列表中，表单提交才能正常工作。
>
>**示例：**
>
>- 存储库： `https://github.com/adobe/abc`
>- 站点1： `main--abc--adobe.aem.live`
>- 站点2： `main--abc1--adobe.aem.live`
>
>两个域都需要单独的允许列表条目才能从两个站点提交表单。

## 常见原因和解决方法

Edge Delivery Services表单提交中出现403禁止的错误可能有多个原因。 请按照以下顺序执行以下故障诊断步骤：

### &#x200B;1. CORS（跨源资源共享）问题

**症状：**

- 浏览器控制台显示与CORS相关的错误消息
- “网络”选项卡显示请求在到达服务器之前被阻止
- 提及“跨源请求已阻止”的错误消息

**诊断：**

1. 打开浏览器开发人员工具(F12)
2. 检查Console选项卡以查看CORS错误消息
3. 查找如下消息： `Access to fetch at 'https://publish-xxx.adobeaemcloud.com' from origin 'https://main--repo--owner.aem.live' has been blocked by CORS policy`

**解决方案：**
在AEM中配置CORS设置，以允许来自您的特定Edge Delivery站点域的请求：

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Sites - Add each site domain individually
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true

# Legacy Franklin domains (if still in use)
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>将`main--abc--adobe.aem.live`和`main--abc1--adobe.aem.live`替换为您的实际网站域。 从同一存储库托管的每个站点都需要一个单独的CORS配置条目。

有关详细的CORS配置，请参阅[CORS配置指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)。

### &#x200B;2. 《Dispatcher规则》

**症状：**

- 浏览器控制台中不显示CORS消息时出现403错误
- 请求到达服务器，但被Dispatcher阻止
- 在到达AEM应用层之前发生错误

**诊断：**

1. 检查请求URL是否与任何Dispatcher过滤器规则匹配
2. 查看可能阻止POST请求的`/filter`规则的Dispatcher配置
3. 验证Dispatcher配置中是否允许表单提交端点

**解决方案：**
更新Dispatcher配置以允许表单提交请求：

1. 确保允许向表单提交端点发送POST请求
2. 为Edge Delivery域添加适当的过滤器规则
3. 验证是否未阻止提交servlet路径

Dispatcher过滤器配置示例：

```apache
/filter {
  # Allow POST requests to form submission servlet
  /0100 { /type "allow" /method "POST" /url "/content/forms/af/*" }
  /0101 { /type "allow" /method "POST" /url "/adobe/forms/af/submit/*" }
  /0102 { /type "allow" /method "POST" /url "/content/forms/portal/submit/adaptiveform" }
}
```

### 3.反向链接筛选问题

**症状：**

- 403错误，浏览器控制台中没有CORS问题
- 请求到达AEM但被Sling引用过滤器拒绝
- AEM应用层出错

**诊断：**
查看AEM错误日志中的反向链接筛选条件拒绝消息：

1. [通过Cloud Manager访问AEM云服务日志](/help/implementing/cloud-manager/manage-logs.md)
2. 在`aemerror.log`中查找包含以下内容的条目：
   - “反向链接筛选条件被拒绝”
   - &quot;org.apache.sling.security.impl.ReferrerFilter&quot;
   - 指示反向链接验证失败的消息

**示例日志条目：**

```
[ERROR] org.apache.sling.security.impl.ReferrerFilter Referrer filter rejected request with referrer 'https://main--abc--adobe.aem.live' for POST /content/forms/af/submit
```

**解决方案：**
配置反向链接筛选条件，以允许您的特定Edge Delivery站点域：

1. 创建或更新OSGi配置文件： `org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. 为您的特定站点域添加以下配置：

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "main--abc--adobe.aem.live",
       "main--abc1--adobe.aem.live"
     ],
     "allow.hosts.regexp": [
       "https://.*\\.aem\\.live:443",
       "https://.*\\.aem\\.page:443",
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

3. 通过Cloud Manager部署配置

>[!IMPORTANT]
>
>**对于重写设置：**&#x200B;必须将每个站点域单独添加到`allow.hosts`数组。 仅使用正则表达式模式可能并不足以满足所有场景。 包括特定域和正则表达式模式以实现全面覆盖。

>[!WARNING]
>
>AEM 的反向链接筛选条件不是 OSGi 配置工厂，这意味着一次只有一个配置在 AEM 服务上处于活动状态。如果可能，请避免添加自定义反向链接筛选条件配置，因为这会覆盖AEM的本机配置，并可能破坏产品功能。

## 诊断步骤

按照以下步骤确定403错误的特定原因：

### 步骤1：检查浏览器控制台

1. 打开浏览器开发人员工具(F12)
2. 导航到控制台选项卡
3. 尝试提交表单
4. 查找与CORS相关的错误消息

**如果存在CORS错误：**&#x200B;请按照上述CORS解决方案操作。
**如果没有CORS错误：**&#x200B;请继续执行步骤2。

### 步骤2：检查网络选项卡

1. 打开浏览器开发人员工具(F12)
2. 导航到“网络”选项卡
3. 尝试提交表单
4. 检查失败的请求详细信息
5. 查看响应标头和状态

**如果请求未到达服务器：**&#x200B;可能是Dispatcher问题。
**如果请求到达服务器但失败：**&#x200B;可能是反向链接筛选条件问题。

### 步骤3：检查AEM日志

1. 访问 Cloud Manager
2. 在日志→导航到环境→环境
3. 下载或查看`aemerror.log`
4. 在提交表单前后搜索条目
5. 查找反向链接筛选条件或与安全相关的消息

## 预防和最佳实践

### 1.安装过程中正确的配置

- 在初始Edge Delivery Services设置期间配置CORS、Dispatcher和反向链接筛选条件设置
- 列入允许列表 **对于每个新站点：**&#x200B;将特定域添加到所有（CORS，反向链接筛选器）
- 在开发环境中测试表单提交内容后上线

### 2.特定于环境的配置

- 使用不同的配置进行开发、暂存和生产环境
- 包含本地主机域以进行本地开发测试
- **记录您的存储库需要允许列表访问权限的所有网站域**

### 3.监测和记录

- 为反向链接筛选条件拒绝设置日志监测
- 在表单提交代码中实施正确的错误处理
- 在测试期间使用浏览器开发人员工具

### 4.文档和团队知识

- **维护使用相同存储库的所有站点域的注册表**
- 对开发团队进行故障排除步骤的培训
- 维护Edge Delivery Services表单设置的核对清单
- 每当从现有允许列表库创建新站点时，**更新存储库**

## 用于重写设置的站点域管理

使用Helix-5和无层体系结构，请遵循以下准则：

### 创建新站点时

1. **标识站点域** （例如，`main--newsite--adobe.aem.live`）
2. **更新CORS配置**&#x200B;以包含新域
3. **更新反向链接筛选条件**&#x200B;以在`allow.hosts`中包含新域
4. 从新站点提交&#x200B;**测试表单**
5. **在站点注册表中记录新域**

### 域命名模式

- 标准模式： `{branch}--{site}--{owner}.aem.live`
- 即使共享同一存储库，每个网站也会获得一个唯一的域
- `.aem.live`和`.aem.page`域都可以使用

### 配置管理

- 在`allow.hosts`中使用特定域条目以获得更好的安全性
- 使用正则表达式模式进行补充，以扩大覆盖范围
- 在添加或删除站点时定期审核和更新允许列表

## 其他资源

- [AEM Headless的反向链接筛选条件配置](/help/headless/deployment/referrer-filter.md)
- [CORS 配置指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [了解跨源资源共享](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)
- [Edge Delivery Services Forms文档](/help/edge/docs/forms/universal-editor/publish-forms.md)

## 相关主题

- [配置提交操作](/help/forms/configuring-submit-actions.md)
- [Forms Submission Service](/help/forms/forms-submission-service.md)
- [Edge Delivery Services 概述](/help/edge/overview.md)


**是否需要其他帮助？**&#x200B;如果您在执行以下疑难解答步骤后继续遇到问题，请通过以下方式联系Adobe客户支持：

- 您的特定错误消息
- AEM Cloud Service环境详细信息
- **需要表单提交访问权限的所有Edge Delivery Services站点域**
- 自错误发生时起的相关日志条目

**是否需要其他帮助？**&#x200B;如果您在执行以下疑难解答步骤后继续遇到问题，请通过以下方式联系Adobe客户支持：

- 您的特定错误消息
- AEM Cloud Service环境详细信息
- Edge Delivery Services域信息
- 自错误发生时起的相关日志条目
