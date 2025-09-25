---
title: 在通用编辑器中将 Google reCAPTCHA 添加到表单
description: 在 Edge Delivery Services 表单中实施防止垃圾邮件和自动攻击的 Google reCAPTCHA 保护指南
feature: Edge Delivery Services
keywords: 表单中的 reCAPTCHA，在通用编辑器中使用 reCAPTCHA，在表单中添加 reCAPTCHA，表单安全性，垃圾邮件防护
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '1281'
ht-degree: 100%

---


# 在通用编辑器中将 Google reCAPTCHA 添加到表单

Google reCAPTCHA 通过区分人类用户和自动机器人来帮助保护表单。本指南介绍了如何在通用编辑器中实施 reCAPTCHA Enterprise 和 Standard 两个版本。

**目标：**

- 选择合适的 reCAPTCHA 解决方案
- 配置 reCAPTCHA Enterprise 或 Standard
- 将 reCAPTCHA 添加到您的表单中
- 验证并测试实施
- 监控和优化性能

## 先决条件

开始之前，请确保您已：

### 满足访问权限要求

- AEM as a Cloud Service 创作访问权限
- 通用编辑器访问权限和表单编辑权限

### 技术要求

- 活跃的 Google 帐户
- 对于 Enterprise 版本：已启用计费的 Google 云平台项目
- 对于 Standard 版本：Google reCAPTCHA 帐户
- 已验证表单的域所有权

### 知识要求

- 具有 AEM Forms 和通用编辑器的基本知识
- 熟悉云服务配置
- 理解表单安全概念

## 为什么要在表单中使用 reCAPTCHA？

| ![安全性](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![机器人防护](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![用户体验](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **增强安全性** | **机器人和垃圾邮件防范** | **无缝的用户体验** |
| 保护表单免受欺诈活动的侵扰和攻击 | 防止自动机器人提交表单 | 不可见的 reCAPTCHA 不会干扰合法用户 |

**关键概念：** reCAPTCHA 使用机器学习来分析用户行为，并为人机交互的可能性分配一个分数（0.0 到 1.0）。分数越高表明是人类用户，分数越低表明是机器人。

**举例：**&#x200B;处理敏感数据的税费计算表需要防范自动攻击。reCAPTCHA 会验证提交是来自真人用户，而不是机器人。

## 选择您的 reCAPTCHA 解决方案

Edge Delivery Services Forms 支持两个 Google reCAPTCHA 选项。使用以下标准选择正确的解决方案：

### 快速决策指南

**在以下情况下使用 reCAPTCHA Enterprise：**

- 高流量表单（每月 >10,000 个请求）
- 要满足严格的合规要求（GDPR、SOX、HIPAA）
- 需要高级分析和报告
- 有高级安全功能的预算
- 进行复杂的多域部署

**在以下情况下使用 reCAPTCHA Standard：**

- 低到中等流量（每月 &lt;10,000 个请求）
- 有基本安全需求
- 预算有限（免费层）
- 简单的单域设置
- reCAPTCHA 新手

### 详细比较

| **功能** | **reCAPTCHA Enterprise** | **reCAPTCHA Standard** |
|-------------|--------------------------|------------------------|
| **成本** | 付费（基于使用情况定价） | 免费 |
| **请求限制** | 无限制 | 每月 100 万个请求 |
| **高级分析** | 详细报告 | 仅基本统计数据 |
| **自定义规则** | 帐户特有的规则 | 仅限全局规则 |
| **多域支持** | 高级管理 | 基本支持 |
| **SLA** | 99.9% 正常运行时间保证 | 尽力 |
| **支持** | 企业支持 | 社区支持 |
| **合规性** | 企业级 | 标准合规性 |

**两种解决方案均提供：**

- 基于分数的检测（0.0 到 1.0 分度）
- 不可见操作（无需用户交互）
- 机器学习驱动的机器人检测
- 实时风险评估

## 设置 reCAPTCHA Enterprise


+++ 步骤 1：准备 Google 云环境

**要求：**

1. 已启用计费的 Google 云项目
2. 项目 ID（来自 GCP 仪表板）
3. 表单的域验证
4. GCP 和 AEM 的管理员访问权限

**设置：** 

1. 创建或选择 Google 云项目
   - 前往 [Google 云控制台](https://console.cloud.google.com/)
   - 创建新项目或选择一个现有项目
   - 记下您的项目 ID

2. 启用 reCAPTCHA Enterprise API
   - 前往 API 和服务 > 库
   - 搜索“reCAPTCHA Enterprise API”
   - 点击“启用”

3. 创建 API 凭据
   - 前往 API 和服务 > 凭据
   - 点击创建凭据 > API 密钥
   - 复制并存储您的 API 密钥

4. 创建网站密钥
   - 前往“安全” > reCAPTCHA Enterprise
   - 点击创建密钥
   - 选择基于分数的密钥类型
   - 添加您的域
   - 设置阈值分数（建议：0.5）

**验证检查点：**&#x200B;确保您有：

- 项目 ID
- API 密钥
- 网站密钥
- 已验证 Google 云中的域

+++

+++ 步骤 2：创建 AEM 云配置容器

![逐步的云配置设置](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*图：为表单容器启用云配置*

**设置：** 

1. 访问配置浏览器
   - 登录到 AEM 作者实例
   - 前往工具 > 常规 > 配置浏览器

2. 启用云配置
   - 找到表单的配置容器
   - 选择属性
   - 检查云配置
   - 点击“保存并关闭”

3. 验证配置
   - 确认“云配置”出现在容器属性中

**验证检查点：**

- 为您的容器启用云配置
- 容器出现在配置浏览器中
- 属性显示“云配置”已启用

+++

+++ 步骤 3：在 AEM 中配置 reCAPTCHA Enterprise 服务

![reCAPTCHA Enterprise 配置屏幕](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*图：AEM 中的 reCAPTCHA Enterprise 配置界面*

**配置：**

1. 访问 reCAPTCHA 配置
   - 前往工具 > 云服务 > reCAPTCHA
   - 选择表单的配置容器
   - 点击创建

2. 配置 Enterprise 设置
   - 标题：描述性名称（例如“Production reCAPTCHA”）
   - 名称：系统名称（自动生成或自定义）
   - 版本：选择 ReCAPTCHA Enterprise
   - 项目 ID：输入您的 Google 云项目 ID
   - 网站密钥：输入来自 Google 云的网站密钥
   - API 密钥：输入您的 Google 云 API 密钥
   - 密钥类型：选择基于分数的网站密钥

3. 设置安全性阈值
   - 阈值分数：设置在 0.0 到 1.0 之间
   - 建议值：
      - 0.7-0.9：高安全性（可能会阻止一些合法用户）
      - 0.5-0.7：平衡安全性（推荐）
      - 0.1-0.5：低安全性（允许更多用户）

4. 保存并发布
   - 点击创建，以保存配置
   - 点击发布即可用

**验证检查点：**

- 已成功保存配置
- 已完成所有必填字段
- 已发布配置且可见
- 无错误消息

+++

## 设置 reCAPTCHA Standard

+++步骤 1：获取 reCAPTCHA API 密钥（参见详细信息）

>[!IMPORTANT]
>
> Edge Delivery Services Forms 仅支持 reCAPTCHA 服务 v2（基于分数）。不要使用复选框版本。

**密钥生成：**

1. 访问 Google reCAPTCHA 控制台

   - 前往 [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin)
   - 使用您的 Google 帐户登录

2. 创建新网站

   - 点击“+”添加新网站
   - 标签：输入一个描述性名称
   - reCAPTCHA 类型：选择 reCAPTCHA v2 > “我不是机器人”不可见
   - 域：添加您的表单域
   - 接受条款后点击提交

3. 收集您的密钥

   - 网站密钥：复制网站密钥（公钥）
   - 密钥：复制密钥（私钥）

**验证检查点：**

- 已在 reCAPTCHA 控制台中创建了网站

- 已获取网站密钥

- 已获取密钥

- 已添加并验证域

+++

+++步骤 2：配置 AEM 云配置容器（参见详细信息）

遵循与 Enterprise 设置中相同的流程：

1. 在配置浏览器中启用云配置

2. 验证容器配置

3. 确认设置已保存

+++

+++步骤 3：在 AEM 中配置 reCAPTCHA 标准服务（参见详细信息）

![reCAPTCHA Standard 配置屏幕](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*图：AEM 中的 reCAPTCHA Standard 配置界面*

**配置：**

1. 访问 reCAPTCHA 配置

   - 前往工具 > 云服务 > reCAPTCHA
   - 选择表单的配置容器
   - 点击创建

2. 配置 Standard 设置

   - 标题：描述性名称（例如“Standard reCAPTCHA”）
   - 名称：系统名称（自动生成或自定义）
   - 版本：选择 ReCAPTCHA v2
   - 网站密钥：输入您的 Google reCAPTCHA 网站密钥
   - 密钥：输入您的 Google reCAPTCHA 密钥

3. 保存并发布

   - 点击创建，以保存配置
   - 点击发布即可用

**验证检查点：**

- 配置已创建，未发生任何错误

- 两个密钥均输入正确

- 配置已成功发布

- 配置出现在列表中

+++

## 将 reCAPTCHA 添加到您的表单中

配置 reCAPTCHA 服务后，按如下方式在您的表单中添加保护：

![将 reCAPTCHA 组件添加到表单](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*图：将不可见的验证码组件添加到表单*

+++&#x200B;1. 在通用编辑器中打开表单
前往 AEM Sites 中的表单，然后点击“编辑”，在通用编辑器中将其打开。等待编辑器加载。

- 前往 AEM Sites 中的表单
- 点击编辑，在通用编辑器中打开
- 等待编辑器加载
+++

+++&#x200B;2. 找到表单结构
在内容树（左侧面板）中，找到自适应表单分区，展开表单结构以查看插入点。

- 在内容树（左侧面板）中，找到您的自适应表单分区
- 展开表单结构，查看插入点
+++

+++&#x200B;3. 添加 reCAPTCHA 组件
将验证码（不可见）组件添加到您的表单。

- 点击表单分区中的添加 (+) 图标
- 从组件列表中选择验证码（不可见）
- 也可以从组件面板中拖放组件
+++

+++&#x200B;4. 配置组件（可选）
选择新添加的验证码组件，验证它是否使用您的 reCAPTCHA 配置。

- 选择新添加的验证码组件
- 在“属性”面板中，验证它是否使用您的 reCAPTCHA 配置
- 基本设置不需要额外配置
+++

+++&#x200B;5. 发布更改
发布您的更改并验证未发生任何错误。

- 点击通用编辑器中的发布
- 等待确认
- 确认没有出现错误
+++

### 验证实施

现在，受到保护的表单位于：

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/
<form-name>
```

**URL 示例：**

```
https://main--my-forms--company.aem.live/content/forms/af/
contact-us-form
```
