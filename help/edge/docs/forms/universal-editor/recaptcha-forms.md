---
title: 在通用编辑器中将Google reCAPTCHA添加到Forms
description: 在Edge Delivery Services表单中实施Google reCAPTCHA保护以阻止垃圾邮件和自动攻击的指南
feature: Edge Delivery Services
keywords: 表单中的 reCAPTCHA，在通用编辑器中使用 reCAPTCHA，在表单中添加 reCAPTCHA，表单安全性，垃圾邮件防护
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 4%

---


# 在通用编辑器中将Google reCAPTCHA添加到Forms

Google reCAPTCHA通过区分人类用户和自动机器人，帮助保护表单。 本指南介绍如何在通用编辑器中实施reCAPTCHA Enterprise和Standard版本。

**目标：**

- 选择适当的reCAPTCHA解决方案
- 配置reCAPTCHA Enterprise或Standard
- 将reCAPTCHA添加到表单
- 验证和测试实施
- 监控和优化性能

## 先决条件

开始之前，请确保您满足以下条件：

### 访问要求

- AEM as a Cloud Service创作访问权限
- 具有表单编辑权限的通用编辑器访问
- 注册抢先访问计划以获得reCAPTCHA功能

### 技术要求

- 有效的Google帐户
- 企业：启用了计费的Google Cloud Platform项目
- 对于Standard：Google reCAPTCHA帐户
- 已验证表单的域所有权

### 知识要求

- 对AEM Forms和通用编辑器的基本了解
- 熟悉云服务配置
- 了解表单安全概念

## 为何在Forms中使用reCAPTCHA？

| ![安全性](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![机器人防护](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![用户体验](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **增强安全性** | **机器人和垃圾邮件防范** | **无缝的用户体验** |
| 保护表单免受欺诈活动和攻击 | 阻止自动机器人提交表单 | 不可见reCAPTCHA不会中断合法用户 |

**密钥概念：** reCAPTCHA使用机器学习分析用户行为并分配一个分数（0.0到1.0），该分数用于指示人机交互的可能性。 得分越高表示人类用户；得分越低表示机器人。

**示例：**&#x200B;处理敏感数据的税务计算表单需要针对自动攻击的保护。 reCAPTCHA验证提交的是真实用户而不是机器人。

## 选择您的 reCAPTCHA 解决方案

Edge Delivery Services Forms支持两个Google reCAPTCHA选项。 使用以下标准选择正确的解决方案：

### 快速决策指南

**在以下情况下使用reCAPTCHA Enterprise：**

- 高流量表单（每月超过10,000个请求）
- 严格的合规要求(GDPR、SOX、HIPAA)
- 需要高级分析和报告
- 高级安全功能的预算
- 复杂的多域部署

**如果您具有以下特征，请使用reCAPTCHA Standard：**

- 低到中等流量（每月少于10,000个请求）
- 基本安全需求
- 预算有限（免费套餐）
- 简单的单域设置
- 初次使用reCAPTCHA

### 详细比较

| **功能** | **reCAPTCHA Enterprise** | **reCAPTCHA Standard** |
|-------------|--------------------------|------------------------|
| **成本** | 付费（基于使用率的定价） | 免费 |
| **请求限制** | 无限制 | 每月100万项请求 |
| **高级分析** | 详细报告 | 仅基本统计信息 |
| **自定义规则** | 特定于帐户的规则 | 仅限全局规则 |
| **多域支持** | 高级管理 | 基本支持 |
| **SLA** | 99.9%的正常运行时间保证 | 尽力 |
| **支持** | 企业支持 | 社区支持 |
| **合规性** | 企业级 | 标准合规性 |

**两个解决方案都提供：**

- 基于分数的检测（0.0到1.0分制）
- 不可见的操作（无需用户交互）
- 机器学习驱动的机器人检测
- 实时风险评估

## 设置 reCAPTCHA Enterprise


+++ 步骤1：准备Google Cloud环境

**要求：**

1. 已启用计费的Google云项目
2. 项目ID（从GCP功能板）
3. 表单的域验证
4. 管理员对GCP和AEM的访问权限

**设置：**

1. 创建或选择Google Cloud项目
   - 转到[Google Cloud Console](https://console.cloud.google.com/)
   - 创建新项目或选择现有项目
   - 记下您的项目ID

2. 启用reCAPTCHA Enterprise API
   - 转到API和服务>库
   - 搜索“reCAPTCHA Enterprise API”
   - 单击启用

3. 创建API凭据
   - 转到“API和服务”>“凭据”
   - 单击创建凭据> API密钥
   - 复制并存储您的API密钥

4. 创建站点密钥
   - 转到“安全”>“reCAPTCHA Enterprise”
   - 单击“创建密钥”
   - 选择基于得分的键类型
   - 添加域
   - 设置阈值分数（推荐： 0.5）

**验证检查点：**&#x200B;确保您具有：

- 项目 ID
- API 键
- 站点密钥
- Google Cloud中已验证的域

+++

+++ 步骤2：配置AEM Cloud配置容器

![逐步云配置设置](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*图：正在为表单容器启用云配置*

**设置：**

1. 访问配置浏览器
   - 登录到 AEM 作者实例
   - 转到“工具”>“常规”>“配置浏览器”

2. 启用云配置
   - 找到表单的配置容器
   - 选择属性
   - 检查云配置
   - 单击保存并关闭

3. 验证配置
   - 确认容器属性中显示“云配置”

**验证检查点：**

- 为您的容器启用的云配置
- 容器显示在配置浏览器中
- 属性将“云配置”显示为已启用

+++

+++ 步骤3：在AEM中配置reCAPTCHA企业服务

![reCAPTCHA Enterprise配置屏幕](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*图： AEM中的reCAPTCHA企业配置接口*

**配置：**

1. 访问recaptcha配置
   - 转到“工具”>“云服务”>“reCAPTCHA”
   - 选择表单的配置容器
   - 单击创建

2. 配置企业设置
   - 标题：描述性名称（例如“Production reCAPTCHA”）
   - 名称：系统名称（自动生成或自定义）
   - 版本：选择ReCAPTCHA Enterprise
   - 项目ID：输入您的Google Cloud项目ID
   - 站点密钥：输入Google Cloud中的站点密钥
   - API密钥：输入您的Google Cloud API密钥
   - 密钥类型：选择基于得分的网站密钥

3. 设置安全阈值
   - 阈值分数：设置为0.0到1.0之间
   - 建议值：
      - 0.7-0.9：高安全性（可能会阻止某些合法用户）
      - 0.5-0.7：均衡安全性（推荐）
      - 0.1-0.5：较低的安全性（允许更多用户）

4. 保存并发布
   - 单击创建以保存配置
   - 单击“发布”使其可用

**验证检查点：**

- 配置保存成功
- 所有必填字段已完成
- 配置已发布并可见
- 无错误消息

+++

## 设置 reCAPTCHA Standard

+++步骤1：获取reCAPTCHA API密钥（请参阅详细信息）

>[!IMPORTANT]
>
> Edge Delivery Services Forms仅支持reCAPTCHA v2（基于得分）。 请勿使用复选框版本。

**密钥生成：**

1. 访问Google reCAPTCHA控制台

   - 转到[Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin)
   - 使用您的Google帐户登录

2. 创建新站点

   - 单击+以添加新站点
   - 标签：输入描述性名称
   - reCAPTCHA类型：选择reCAPTCHA v2 >“我不是机器人”不可见
   - 域：添加您的表单域
   - 接受条款并单击“提交”

3. 收集您的密钥

   - 站点密钥：复制站点密钥（公共密钥）
   - 密钥：复制密钥（私钥）

**验证检查点：**

- 在reCAPTCHA控制台中创建的站点

- 站点密钥已获取

- 已获取密钥

- 已添加和验证的域

+++

+++步骤2：配置AEM云配置容器（请参阅详细信息）

遵循与企业设置中相同的过程：

1. 在配置浏览器中启用云配置

2. 验证容器配置

3. 确认设置已保存

+++

+++步骤3：在AEM中配置reCAPTCHA标准服务（请参阅详细信息）

![reCAPTCHA标准配置屏幕](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*图： AEM中的reCAPTCHA标准配置接口*

**配置：**

1. 访问recaptcha配置

   - 转到“工具”>“云服务”>“reCAPTCHA”
   - 选择表单的配置容器
   - 单击创建

2. 配置标准设置

   - 标题：描述性名称（例如“标准reCAPTCHA”）
   - 名称：系统名称（自动生成或自定义）
   - 版本：选择ReCAPTCHA v2
   - 站点密钥：输入您的Google reCAPTCHA站点密钥
   - 密钥：输入您的Google reCAPTCHA密钥

3. 保存并发布

   - 单击创建以保存配置
   - 单击“发布”使其可用

**验证检查点：**

- 创建配置时没有出现错误

- 两个键都输入正确

- 配置发布成功

- 配置显示在列表中

+++

## 将reCAPTCHA添加到表单

配置reCAPTCHA服务后，按如下方式向表单添加保护：

![正在将reCAPTCHA组件添加到表单](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*图：正在将不可见的Captcha组件添加到表单*

+++1. 在通用编辑器中打开表单
转到AEM Sites中的表单，然后单击“编辑”以在通用编辑器中打开该表单。 等待加载编辑器。

- 转到AEM Sites中的表单
- 单击编辑以在通用编辑器中打开
- 等待编辑器加载
+++

+++2. 查找表单结构
在内容树（左面板）中，找到您的自适应表单部分，并展开表单结构以查看插入点。

- 在内容树（左面板）中，找到您的自适应表单部分
- 展开窗体结构以查看插入点
+++

+++3. 添加reCAPTCHA组件
将Captcha（不可见）组件添加到表单。

- 单击表单部分中的添加(+)图标
- 从组件列表中，选择Captcha （不可见）
- 或者，从组件面板中拖放组件
+++

+++4. 配置组件（可选）
选择新添加的captcha组件并验证它是否使用您的reCAPTCHA配置。

- 选择新添加的验证码组件
- 在“属性”面板中，验证它是否使用您的reCAPTCHA配置
- 基本设置无需其他配置
+++

+++5. 发布更改
发布更改并验证没有错误。

- 单击在通用编辑器中发布
- 等待确认
- 验证未显示任何错误
+++

### 验证实施

您的受保护表单现在在以下位置提供：

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/
<form-name>
```

**示例URL：**

```
https://main--my-forms--company.aem.live/content/forms/af/
contact-form
```
