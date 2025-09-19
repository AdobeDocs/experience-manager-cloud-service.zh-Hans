---
title: 表单提交和集成
description: 了解如何配置表单提交并将Forms Experience Builder表单与外部系统、API和业务工作流集成。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 0%

---


# 表单提交和集成

>[!NOTE]
>
> Forms Experience Builder可通过提前访问计划获得。 在开始之前，请确保您已请求并获得访问权限。

Forms Experience Builder提供强大的集成功能，将您的表单与外部系统、API和业务工作流连接起来。 本指南介绍如何配置表单提交和设置各种集成方案。

## 提交配置选项

### 电子邮件提交

配置表单以通过电子邮件发送提交内容：

**基本电子邮件设置：**

- 设置收件人电子邮件地址
- 配置电子邮件模板
- 添加抄送和密送收件人
- 设置电子邮件通知

**高级电子邮件功能：**

- 动态收件人选择
- 包含表单数据的电子邮件模板
- 附件处理
- 电子邮件投放确认

### REST API集成

将表单连接到外部API和服务：

**API终结点配置：**

- 设置REST API URL
- 配置身份验证方法
- 设置请求标头和参数
- 处理响应数据

**数据映射：**

- 将表单字段映射到API参数
- 转换数据格式
- 处理嵌套JSON结构
- 管理错误响应

### 云存储集成

在云存储服务中存储表单提交：

**支持的平台：**

- Microsoft Azure Blob存储
- Amazon S3
- Google云存储
- SharePoint Online

**配置选项：**

- 设置存储凭据
- 配置文件夹结构
- 设置文件命名约定
- 管理访问权限

### 工作流集成

将表单连接到业务流程工作流：

**Microsoft Power Automate：**

- 在表单提交时触发工作流
- 将表单数据传递到工作流步骤
- 处理工作流响应
- 管理审批流程

**Adobe工作流：**

- 与AEM工作流集成
- 设置审批链
- 配置通知步骤
- 管理文档处理

## 设置表单提交

### 步骤1：访问提交配置

1. 在Forms Experience Builder中打开表单
2. 导航到提交设置
3. 选择“配置表单提交”
4. 选择您的集成类型

### 步骤2：配置电子邮件提交

**基本电子邮件设置：**

    配置电子邮件提交至hr@company.com的内容：
     — 主题：“新员工申请”
     — 在电子邮件正文中包含表单数据
     — 向申请人发送确认函

**高级电子邮件配置：**

    设置动态电子邮件路由：
     — 如果部门等于“IT”，请发送到it-hr@company.com
     — 如果部门等于“销售”，请发送到sales-hr@company.com
     — 默认为hr@company.com

### 步骤3：设置API集成

**REST API配置：**

    将表单数据提交到REST终结点：
    - URL： https://api.company.com/forms/submit
     — 方法： POST
     — 身份验证： Bearer令牌
    - Content-Type： application/json

**数据映射示例：**

    将表单字段映射到API：
    - firstName -> user.first_name
    - lastName -> user.last_name
    - email -> user.email_address
    - department -> user.department_id

### 步骤4：配置云存储

**Azure Blob存储设置：**

    在Azure中存储表单提交：
     — 容器：表单提交
     — 文件夹：/{year}/{month}/{day}/
     — 文件格式：带有附件的JSON
     — 访问级别：私人

## 集成示例

### 客户反馈表

**提交配置：**

- 向支持团队发送电子邮件通知
- 通过API在CRM系统中存储数据
- 自动创建支持票证
- 向客户发送确认电子邮件

**实现：**
将客户反馈表提交到：
1.发送包含表单详细信息的电子邮件<support@company.com>
2.发布到CRM API以创建客户记录
3.触发支持票证创建工作流
4.向客户发送感谢电子邮件

### 员工入门培训表

**提交配置：**

- 向人力资源团队发送电子邮件，其中包含新员工信息
- 在SharePoint中存储文档
- 触发载入工作流
- 在各种系统中创建用户帐户

**实现：**
处理员工入职流程：
1.发送包含员工详细信息的电子邮件<hr@company.com>
2.将文档上传到SharePoint员工文件夹
3.在Power Automate中开始载入工作流
4.在HR系统、电子邮件和其他工具中创建帐户

### 商机开发表单

**提交配置：**

- 在营销自动化平台中存储潜在客户数据
- 向销售团队发送通知
- 将潜在客户添加到CRM系统
- 触发跟进电子邮件序列

**实现：**
流程商机开发：
1.将潜在客户数据发布到Marketo API
2.在Salesforce中创建潜在客户记录
3.向销售团队发送电子邮件，其中包含潜在客户详细信息
4.启动自动化电子邮件培养序列

## 高级集成方案

### 多步骤表单处理

**复杂的工作流集成：**

- 针对外部系统验证表单数据
- 通过付款网关处理付款
- 生成文档和合同
- 向多个利益相关者发送通知

### 实时数据验证

**基于API的验证：**

- 根据公司目录验证电子邮件地址
- 检查库存系统中的产品可用性
- 验证CRM中的客户信息
- 验证付款信息

### 条件提交路由

**基于表单数据的动态路由：**

- 基于查询类型到不同部门的路由
- 根据客户层发送到不同的系统
- 根据表单完成状态进行不同处理
- 按地区处理不同的业务规则

## 安全性和合规性

### 数据保护

**加密和安全性：**

- 加密传输中的敏感数据
- 安全API凭据和令牌
- 实施适当的访问控制
- 遵循数据保留策略

### 合规性要求

**GDPR和隐私：**

- 实施同意管理
- 提供数据导出功能
- 启用数据删除请求
- 维护审核跟踪

**行业标准：**

- 针对医疗保健表单的HIPAA合规性
- 用于支付处理的PCI DSS
- 针对金融表单的SOX合规性
- 行业特定法规

## 测试和验证

### 提交测试

**测试方案：**

- 验证电子邮件投放和格式
- 测试API连接和数据映射
- 验证云存储上传
- 检查工作流触发器功能

**错误处理：**

- 测试网络故障方案
- 验证错误消息显示
- 检查重试机制
- 验证回退选项

### 性能优化

**优化策略：**

- 实施异步处理
- 对批量数据使用批处理操作
- 优化API调用频率
- 缓存经常访问的数据

## 集成问题疑难解答

### 常见问题

**电子邮件传递问题：**

- 检查SMTP服务器配置
- 验证收件人电子邮件地址
- 审查垃圾邮件过滤器设置
- 测试电子邮件模板格式

**API集成问题：**

- 验证API端点URL
- 检查身份验证凭据
- 验证请求格式和标头
- 审查API响应处理

**存储集成问题：**

- 确认存储凭据
- 检查文件夹权限
- 验证文件上传限制
- 测试网络连接

### 获取帮助

对于集成问题：

- 查看[Forms Experience Builder常见问题解答](forms-experience-builder-frequently-asked-questions.md)
- 查看[入门指南](forms-experience-builder-getting-started.md)
- 请与系统管理员联系以获得技术帮助
- 请参阅外部服务的API文档

## 相关文章

- [Forms Experience Builder概述](product-overview.md)
- [Forms Experience Builder快速入门](forms-experience-builder-getting-started.md)
- [部署和配置Forms Experience Builder](deploy-forms-experience-builder.md)
- [智能导入和转换](intelligent-import-conversion.md)
- [常见问题解答](forms-experience-builder-frequently-asked-questions.md)
