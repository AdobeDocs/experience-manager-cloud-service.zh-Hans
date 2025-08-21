---
title: 为集成 Edge Delivery Services 的 AEM Forms 配置提交操作
description: 了解如何在使用 Edge Delivery Services 的 AEM Forms 中配置提交操作。在 Forms Submission Service 与 AEM Publish Submit Action 之间进行选择，以安全高效地处理表单数据。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '855'
ht-degree: 100%

---

# 配置 AEM Forms 的提交操作

配置表单提交处理方法，通过带 Edge Delivery Services 的 AEM Forms 将数据路由到电子表格、电子邮件或后端系统。

## 快速决策指南

选择您的提交方法：

| 方法 | 最适合 | 设置复杂性 | 用例 |
|--------|----------|------------------|-----------|
| **表单提交服务** | 简单数据捕获 | 低 | 联系表单、意见调查、基本数据收集 |
| **AEM 发布提交** | 复杂的工作流程 | 高 | 企业集成、自定义处理、工作流程 |

## 先决条件

在配置提交操作之前，请确保您具有：

- AEM Forms as a Cloud Service 实例
- 已配置的 Edge Delivery Services 项目
- 使用文档创作或通用编辑器创建的表单
- 目标目的地（电子表格、电子邮件系统或 AEM）所需的权限

+++ 方法 1：表单提交服务

表单提交服务是 Adobe 托管的端点，非常适合用于简单数据捕获场景。

### 受支持的目标

- **电子表格**：Google 表格，Microsoft Excel (OneDrive/SharePoint)
- **电子邮件**：将表单数据发送到特定的电子邮件地址

### 配置步骤

1. **设置目标访问权限**
   - 对于电子表格：授予目标电子表格上 `forms@adobe.com` 的编辑权限
   - 对于电子邮件：验证收件人的电子邮件地址是否可访问

2. **配置表单提交**
   - 在创作环境中打开表单
   - 将提交操作设置为“表单提交服务”
   - 指定目标电子表格的 URL 或电子邮件地址
   - 保存并发布表单

3. **测试提交**
   - 通过表单提交测试数据
   - 验证数据是否显示在目标目的地
   - 如果提交失败，请检查错误日志

### 重要说明

- 服务帐户 `forms@adobe.com` 需要目标电子表格的编辑权限
- 表单提交后会立即发送电子邮件通知
- 在服务级别上进行数据验证

![表单提交服务流](/help/forms/assets/eds-fss.png)

+++

+++ 方法 2：AEM 发布提交

将表单数据直接提交到您的 AEM as a Cloud Service 发布实例，以进行复杂的处理。

### 何时使用 AEM 发布

- 提交后需要自定义 AEM 工作流
- 表单数据模型 (FDM) 与数据库集成
- 第三方服务集成（Marketo、Power Automate、Workfront Fusion）
- Azure Blob 存储或 SharePoint 文档库
- 复杂的服务器端验证或处理逻辑

### 可用的提交操作

- [提交到 REST 端点](/help/forms/configure-submit-action-restpoint.md)
- [通过 AEM 邮件服务发送电子邮件](/help/forms/configure-submit-action-send-email.md)
- [使用表单数据模型提交](/help/forms/configure-data-sources.md)
- [调用 AEM 工作流](/help/forms/aem-forms-workflow-step-reference.md)
- [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [提交至 Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [提交至 Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [提交至 Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [提交至 Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![AEM 发布提交流](/help/forms/assets/eds-aem-publish.png)

### 配置要求

#### &#x200B;1. AEM Dispatcher 配置

在 AEM 发布实例上配置 Dispatcher：

- **允许提交路径**：更改 `filters.any` 以允许对 `/adobe/forms/af/submit/...` 的 POST 请求
- **不重定向**：确保 Dispatcher 规则不会将表单提交路径重定向

#### &#x200B;2. OSGi 引荐来源过滤器

在 AEM OSGi 控制台 (`/system/console/configMgr`) 中：

1. 查找“Apache Sling 引荐来源过滤器”
2. 将您的 Edge Delivery 域添加到“允许主机”列表
3. 包括以下域 `https://your-eds-domain.hlx.page`

#### &#x200B;3. CDN 重定向规则

将 Edge Delivery CDN 配置为路由提交：

- 将请求从 `/adobe/forms/af/submit/...` 路由到 AEM 发布实例
- 实施因 CDN 提供商（Fastly、Akamai、Cloudflare）而异

#### &#x200B;4. 表单配置

1. 在通用编辑器中创建表单
2. 将提交操作配置为目标 AEM Forms 操作
3. 指定提交端点路径
4. 将表单发布到 Edge Delivery 网站

+++

+++ 表单嵌入（可选）

将在一个位置创建的表单嵌入到不同的网页或网站中。

### 用例

- 在多个登陆页面上重复使用标准表单
- 在文档创作的内容中包含专门的表单
- 在多个 EDS 项目中维护一个表单

### CORS 配置

配置表单源上的跨来源资源共享：

1. **将 CORS 标头添加**&#x200B;到表单源响应：
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`
   - `Access-Control-Allow-Headers: Content-Type`

2. **配置示例**：

       # 托管表单的网站的配置
       标头：
       - 路径：/forms/**
       自定义：
       Access-Control-Allow-Origin: https://host-domain.com
       Access-Control-Allow-Methods: GET, OPTIONS
   
### 嵌入步骤

1. **创建并发布表单**
   - 使用文档创作或通用编辑器构建表单
   - 配置提交方法（FSS 或 AEM 发布）
   - 发布到独立 URL

2. **配置 CORS**
   - 设置表单源网站上的 CORS 标头
   - 允许主机页面的域获取表单

3. **嵌入到主机页面**
   - 将表单嵌入块添加到主机页面
   - 将嵌入块指向已发布的表单 URL
   - 发布主机页面

![嵌入式表单架构](/help/forms/assets/eds-embedded-form.png)

+++

+++ 常见问题

| 问题 | 解决办法 |
|-------|----------|
| **表单提交失败** | 检查控制台错误，验证端点 URL，确认权限 |
| **嵌入的表单不显示** | 配置表单源上的 CORS 标头，验证表单 URL |
| **AEM 发生 403/401 错误** | 更新 Sling 引荐来源过滤器，检查身份验证设置 |
| **数据未到达电子表格** | 验证 `forms@adobe.com` 是否具有编辑权限，检查电子表格的 URL |
| **CORS 错误** | 将适当的 `Access-Control-Allow-Origin` 标头添加到表单源 |

+++

## 配置示例

+++ 基于文档的表单与电子表格提交

1. 在 Google Docs/Sheets 中创建表单结构
2. 配置表单提交服务端点
3. 授予对目标电子表格的 `forms@adobe.com` 编辑权限
4. 将文档发布到 Edge Delivery 网站
5. 测试表单提交和数据流

+++

+++ 通用编辑器表单与 AEM 工作流

1. 在通用编辑器中构建表单
2. 将提交操作配置为“调用 AEM 工作流”
3. 在 AEM 发布上设置 Dispatcher 和引荐来源过滤器
4. 配置 CDN 路由规则
5. 发布表单并测试工作流的执行

+++

## 最佳实践

- 为简单数据捕获场景&#x200B;**使用表单提交服务**
- 在需要复杂的处理或集成的情况下，**选择 AEM 发布** 
- 在部署生产之前，在暂存环境中进行&#x200B;**彻底测试**
- 通过 AEM 日志和控制台错误&#x200B;**监控提交**
- 对失败的提交&#x200B;**实施恰当的错误处理方法**
- 在客户端和服务器两个层面上&#x200B;**验证数据**
- 所有表单提交和数据传输都&#x200B;**使用 HTTPS**

## 相关主题

- [使用 EDS Forms 进行基于文档的创作](/help/edge/docs/forms/tutorial.md)
- [通用编辑器与 EDS Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [AEM Forms 提交服务](/help/forms/forms-submission-service.md)
- [配置数据源](/help/forms/configure-data-sources.md)
- [AEM Forms 工作流参考](/help/forms/aem-forms-workflow-step-reference.md)
