---
title: 为集成 Edge Delivery Services 的 AEM Forms 配置提交操作
description: 了解如何在使用 Edge Delivery Services 的 AEM Forms 中配置提交操作。在 Forms Submission Service 与 AEM Publish Submit Action 之间进行选择，以安全高效地处理表单数据。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 12%

---

# 为AEM Forms配置提交操作

使用带有Edge Delivery Services的AEM Forms配置表单提交处理，将数据路由到电子表格、电子邮件或后端系统。

## 快速决策指南

选择提交方法：

| 方法 | 最适合 | 设置复杂性 | 用例 |
|--------|----------|------------------|-----------|
| **Forms提交服务** | 简单的数据捕获 | 低 | 联系表单、调查、基本数据收集 |
| **AEM发布提交** | 复杂的工作流 | 高 | 企业集成、自定义处理、工作流 |

## 先决条件

在配置提交操作之前，请确保您具有：

- AEM Forms as a Cloud Service实例
- 已配置Edge Delivery Services项目
- 使用文档创作或通用编辑器创建的表单
- 目标目标所需的权限(电子表格、电子邮件系统或AEM)

+++ 方法1：Forms提交服务

Forms提交服务是Adobe托管的端点，非常适用于简单的数据捕获场景。

### 支持的目标

- **电子表格**：Google工作表、Microsoft Excel (OneDrive/SharePoint)
- **电子邮件**：将表单数据发送到指定的电子邮件地址

### 配置步骤

1. **设置目标访问**
   - 对于电子表格：授予对`forms@adobe.com`在目标电子表格上的编辑权限
   - 对于电子邮件：验证收件人电子邮件地址是否可访问

2. **配置表单提交**
   - 在创作环境中打开表单
   - 将提交操作设置为“Forms提交服务”
   - 指定目标电子表格URL或电子邮件地址
   - 保存并发布表单

3. **测试提交**
   - 通过表单提交测试数据
   - 验证数据是否显示在目标目标中
   - 提交失败时检查错误日志

### 重要说明

- 服务帐户`forms@adobe.com`需要目标电子表格的编辑权限
- 在提交表单后立即发送电子邮件通知
- 数据验证在服务级别进行

![Forms提交服务流程](/help/forms/assets/eds-fss.png)

+++

+++ 方法2：AEM发布提交

将表单数据直接提交到AEM as a Cloud Service发布实例，以进行复杂处理。

### 何时使用AEM Publish

- 提交后需要自定义AEM工作流
- 表单数据模型(FDM)与数据库的集成
- 第三方服务集成(Marketo、Power Automate、Workfront Fusion)
- Azure Blob Storage或SharePoint文档库
- 复杂的服务器端验证或处理逻辑

### 可用的提交操作

- [提交到 REST 端点](/help/forms/configure-submit-action-restpoint.md)
- [通过AEM邮件服务发送电子邮件](/help/forms/configure-submit-action-send-email.md)
- [使用表单数据模型提交](/help/forms/configure-data-sources.md)
- [调用 AEM 工作流](/help/forms/aem-forms-workflow-step-reference.md)
- [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [提交至 Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [提交至 Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [提交至 Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [提交至 Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![AEM发布提交流程](/help/forms/assets/eds-aem-publish.png)

### 配置要求

#### &#x200B;1. AEM Dispatcher配置

在AEM发布实例上配置Dispatcher：

- **允许提交路径**：修改`filters.any`以允许`/adobe/forms/af/submit/...`的POST请求
- **无重定向**：确保Dispatcher规则不会重定向表单提交路径

#### &#x200B;2. OSGi引用过滤器

在AEM OSGi控制台(`/system/console/configMgr`)中：

1. 查找“Apache Sling引用过滤器”
2. 将您的Edge Delivery域添加到“允许主机”列表
3. 包括`https://your-eds-domain.hlx.page`等域

#### &#x200B;3. CDN重定向规则

配置您的Edge Delivery CDN以路由提交内容：

- 将请求从`/adobe/forms/af/submit/...`路由到您的AEM发布实例
- 实施因CDN提供商(Fastly、Akamai、Cloudflare)而异

#### 4.表单配置

1. 在通用编辑器中创建表单
2. 配置提交操作以定位AEM Forms操作
3. 指定提交端点路径
4. 将表单发布到Edge Delivery站点

+++

+++ 表单嵌入（可选）

将在一个位置创建的表单嵌入到不同的网页或站点中。

### 用例

- 在多个登陆页面中重用标准表单
- 在文档创作内容中包含专业表单
- 跨多个EDS项目维护单个表单

### CORS 配置

在表单源上配置跨源资源共享：

1. **将CORS标头**&#x200B;添加到表单源响应：
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`
   - `Access-Control-Allow-Headers: Content-Type`

2. **示例配置**：

   承载表单    的站点的
&#x200B;#配置 标头：
        — 路径： /forms/**
       自定义：
       Access-Control-Allow-Origin： https://host-domain.com
       Access-Control-Allow-Methods： GET， OPTIONS
   

### 嵌入步骤

1. **创建和发布表单**
   - 使用文档创作或通用编辑器构建表单
   - 配置提交方法(FSS或AEM Publish)
   - 发布到独立URL

2. **配置CORS**
   - 在表单源网站上设置CORS标头
   - 允许主机页域提取表单

3. **嵌入到主机页面**
   - 将表单嵌入块添加到主机页面
   - 将块指向已发布的表单URL
   - “发布主机”页

![嵌入式表单架构](/help/forms/assets/eds-embedded-form.png)

+++

+++ 常见问题

| 问题 | 解决方案 |
|-------|----------|
| **表单提交失败** | 检查控制台错误，验证端点URL，确认权限 |
| **未显示嵌入表单** | 在表单源上配置CORS标头，验证表单URL |
| AEM出现&#x200B;**403/401错误** | 更新Sling引用过滤器，检查身份验证设置 |
| **数据无法访问电子表格** | 验证`forms@adobe.com`是否具有编辑权限，检查电子表格URL |
| **个CORS错误** | 将适当的`Access-Control-Allow-Origin`标头添加到表单源 |

+++

## 配置示例

+++ 提交电子表格的基于文档的表单

1. 在Google Docs/Sheets中创建窗体结构
2. 配置Forms提交服务端点
3. 授予目标电子表格的`forms@adobe.com`编辑访问权限
4. 将文档发布到Edge Delivery站点
5. 测试表单提交和数据流

+++

+++ 带AEM Workflow的通用编辑器表单

1. 在通用编辑器中构建表单
2. 配置提交操作以“调用AEM工作流”
3. 在AEM Publish上设置Dispatcher和反向链接筛选器
4. 配置CDN路由规则
5. 发布表单并测试工作流执行

+++

## 最佳实践

- **将Forms提交服务**&#x200B;用于简单的数据捕获方案
- **当需要复杂的处理或集成时，请选择AEM发布**
- 在生产部署之前，在暂存环境中彻底测试&#x200B;**&#x200B;**
- **使用AEM日志和控制台错误监视提交**
- **为失败的提交实施正确的错误处理**
- **在客户端和服务器级别验证数据**
- **对所有表单提交和数据传输使用HTTPS**

## 相关主题

- [使用EDS Forms进行基于文档的创作](/help/edge/docs/forms/tutorial.md)
- [带有EDS Forms的通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [AEM Forms Submission Service](/help/forms/forms-submission-service.md)
- [配置数据源](/help/forms/configure-data-sources.md)
- [AEM Forms工作流参考](/help/forms/aem-forms-workflow-step-reference.md)
