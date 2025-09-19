---
title: Forms Experience Builder — 常见问题
description: 查找有关Forms Experience Builder的常见问题解答，包括设置、使用、故障排除和最佳实践。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# Forms Experience Builder — 常见问题

>[!NOTE]
>
> Forms Experience Builder可通过提前访问计划获得。 在开始之前，请确保您已请求并获得访问权限。

此常见问题解答介绍了Forms Experience Builder的最常见问题，从基本设置到高级功能和疑难解答。

## 一般问题

### 什么是Forms Experience Builder？

Forms Experience Builder是一款AI支持的表单创建工具，可让您使用对话语言构建复杂的数字表单。 您无需使用传统的拖放界面或复杂的编码，而只需描述您需要的内容，AI将为您创建表单。

### 谁可以使用Forms Experience Builder？

Forms Experience Builder专门用于：

- 希望快速高效地构建表单的&#x200B;**表单创建者**
- **需要创建表单而没有技术专业知识的业务用户**
- **希望利用AI建立快速表单原型的**&#x200B;开发人员
- 需要配置和管理表单创建工作流的&#x200B;**管理员**

### Forms Experience Builder是否适用于所有AEM Forms客户？

Forms Experience Builder当前可通过提前访问计划获得。 请联系您的Adobe代表，请求获取访问权限并了解贵组织的可用性。

## 设置和配置

### 使用Forms Experience Builder的先决条件是什么？

在使用Forms Experience Builder之前，请确保您已：

- 通过提前访问程序访问Forms Experience Builder
- 带有自适应AEM Forms核心组件的Forms as a Cloud Service
- 基本了解表单概念和业务要求

有关详细的技术设置要求，请参阅[部署和配置Forms Experience Builder](deploy-forms-experience-builder.md)。

### 如何在我的环境中启用Forms Experience Builder？

Forms Experience Builder的设置取决于您的AEM Forms实施：

Edge Delivery Services的&#x200B;**：**

- 为Edge Delivery Services Forms准备项目
- 在通用编辑器中启用Forms Experience Builder

对于基于核心组件的表单&#x200B;**：**

- 确保启用了自适应Forms核心组件
- 在自适应Forms编辑器中配置Forms Experience Builder

### 我能否将Forms Experience Builder与现有表单结合使用？

是，Forms Experience Builder可以通过多种方式处理现有表单：

- 导入和转换现有PDF forms
- 利用AI支持的功能增强现有自适应表单
- 将智能字段添加到当前表单结构

## 创建表单

### 如何创建我的第一个表单？

首先，简单描述您想要的内容：

    创建包含姓名、电子邮件和消息字段的联系人表单

AI将生成基本表单结构，然后您可以通过附加功能、验证和样式来增强该结构。

### 我可以创建哪些类型的表单？

Forms Experience Builder支持各种表单类型：

- 联系和反馈表单
- 注册和载入表单
- 调查和评估表
- 具有条件逻辑的多步表单
- Forms具有文件上传和复杂验证功能

### 我可以创建多步表单吗？

可以，您可以使用自然语言创建多步表单：

    创建包含3个步骤的渐进式表单：个人信息、首选项、确认

AI将自动设置包含步骤间导航的表单结构。

### 如何将验证添加到表单字段？

使用自然语言命令添加验证：

    使@email为具有电子邮件格式验证的必填字段
    将美国电话号码格式验证添加到@phoneNumber
    设置年龄验证：对于@dateOfBirth
，年龄必须为18岁或更早
## 高级功能

### 什么是LLM增强型智能字段？

LLM增强的智能字段是智能表单字段，其中预先填充了AI知识库中的相关选项。 例如：

- 世界各国的国家/地区下拉菜单
- 使用标准代码的行业分类
- 包含州、城市和邮政编码的地理数据

### 如何将现有文档导入表单？

您可以导入各种文档类型：

- **PDF forms**：上传静态或交互式PDF
- **图像**：上传纸质表单或屏幕截图的照片
- **设计文件**：导入Figma设计或其他设计格式

使用Forms Experience Builder中的附件图标上传您的文档并描述您的转化要求。

### 是否可以将表单与外部系统集成？

是，Forms Experience Builder支持各种集成选项：

- 使用自定义模板提交电子邮件
- REST API与外部服务集成
- 云存储集成(Azure、AWS、Google Cloud)
- 工作流集成(Power Automate、AEM Workflow)

## 疑难解答

### AI不理解我的请求。 我该怎么办？

尝试以下方法：

- 在描述中更加具体
- 将复杂的请求分解成多个小步骤
- 使用字段引用(@fieldName)进行目标更改
- 提供您想要的明确示例

### 我的表单验证不起作用。 如何修复它？

检查这些常见问题：

- 验证字段名称是否完全匹配（区分大小写）
- 确保验证语法正确
- 单独测试验证规则
- 查看特定问题的错误消息

### 条件逻辑未正确触发。 有什么问题吗？

条件逻辑疑难解答方式：

- 确保字段名称被正确引用
- 检查规则语法和条件
- 使用不同的输入组合进行测试
- 验证字段类型是否与规则要求匹配

### 接口未加载。 我该怎么办？

尝试以下解决方案：

- 刷新浏览器并清除缓存
- 检查您的互联网连接
- 验证您是否具有适当的访问权限
- 如果问题仍然存在，请联系您的系统管理员

## 最佳实践

### 如何使用Forms Experience Builder创建更好的表单？

请遵循以下最佳实践：

- **具体**：提供所需内容的详细说明
- **从简单开始**：从基本结构开始，逐步增加复杂性
- **彻底测试**：在部署之前验证所有表单功能
- **使用增量开发**：逐步生成表单

### 创建表单时应避免什么？

请避免以下常见错误：

- 在描述中过于模糊
- 尝试同时创建所有内容
- 跳过测试和验证
- 未考虑移动响应能力

### 如何确保我的表单可访问？

Forms Experience Builder包括辅助功能：

- 自动WCAG符合性检查
- 屏幕阅读器兼容性
- 键盘导航支持
- 高对比度模式选项

## 集成和部署

### 如何部署使用Forms Experience Builder创建的表单？

使用Forms Experience Builder创建的Forms遵循标准AEM Forms部署流程：

- 通过AEM创作环境发布表单
- 配置表单提交端点
- 设置表单处理工作流
- 生产环境中的测试表单

### 我可以自定义AI响应和行为吗？

可以，您可以配置各个方面：

- 响应样式（简明、详细、均衡）
- 语言偏好设置和术语
- 界面自定义选项
- 辅助功能设置

### 如何获取Forms Experience Builder的帮助？

要获得其他支持，请执行以下操作：

- 查看[入门指南](forms-experience-builder-getting-started.md)
- 查看[部署和配置指南](deploy-forms-experience-builder.md)
- 联系您的系统管理员
- 如有技术问题，请联系Adobe支持部门

## 相关文章

- [Forms Experience Builder概述](product-overview.md)
- [Forms Experience Builder快速入门](forms-experience-builder-getting-started.md)
- [部署和配置Forms Experience Builder](deploy-forms-experience-builder.md)
- [LLM增强的智能字段](forms-experience-builder-llm-smart-fields.md)
- [智能导入和转换](intelligent-import-conversion.md)
- [表单提交和集成](form-submission-integration.md)
