---
title: 在交互式通信编辑器中关联UI
description: 通过使面向客户的代理生成个性化、合规的通信，在交互式通信编辑器中发现关联UI。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="适用于AEM Forms)。"
exl-id: 9ba58659-b14c-4ebc-a6d9-e56a4b6aa48b
source-git-commit: f889498f9ee5e71a4d3695dbfbe194d1bbb11488
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 3%

---

# 在交互式通信编辑器中关联UI

>[!NOTE]
>
> 交互式通信功能在早期采用者计划下提供。 请从您的工作地址发送电子邮件至 `aem-forms-ea@adobe.com`，以申请访问权限。

**关联UI**&#x200B;是一个基于交互式通信(IC)编辑器构建的专用简化界面。 它面向面向面向客户的专业人员（如现场助理和服务代理），旨在于实时交互期间实时生成个性化、合规且准确的通信。

![查找IC文档](/help/forms/interactive-communication/assets/associate-ui-preview.png)

## 关联UI界面

关联UI提供了一个干净的双面板工作区，该工作区支持快速且安全的通信生成：

### 左面板：数据输入

- 联系人输入或确认特定于客户的信息。
- 验证、帮助程序文本和必填字段用于指导准确输入。

### 右侧面板：实时预览

- 显示最终文档的即时预览。
- 在关联填写数据时自动更新。

### 即时文档生成

- 生成或下载最终完成的通信。

## 用户角色和职责

关联UI由三个核心角色驱动，每个角色具有不同的职责：

### 1.管理员

负责系统设置、管理、后端集成和用户访问。

| 责任 | 焦点 |
|---------------|-------|
| 系统配置 | 设置核心基础架构、用户组、表单数据模型(FDM)、输出。 |
| 治理和安全 | 管理用户权限并确保系统合规性。 |
| 集成管理 | 维护后端集成和实时客户数据连接。 |

### 2.作者

设计和管理交互式通信，并将其配置为关联UI（包括启用关联视图和可选工作流）。

| 责任 | 焦点 |
|---------------|-------|
| IC创作和设计 | 创建布局、品牌和兼容的文档结构。 |
| 字段配置 | 映射数据字段，定义可编辑、必需和只读字段。 |
| 发布与启用 | 发布IC并共享链接以进行关联访问。 |

### 3.联营公司

使用关联UI帮助客户、更新信息和生成合规通信。


| 责任 | 焦点 |
|---------------|-------|
| 数据确认 | 通过左侧输入面板填写或验证客户数据。 |
| 预览和验证 | 使用实时预览面板确保准确性。 |
| 交付 | 生成PDF/电子邮件并通过批准的渠道发送。 |

>[!NOTE]
>
> 关联必须是&#x200B;**forms-associates**&#x200B;组的一部分。 对于也从创作实例上的关联UI提交的作者，也将其添加到&#x200B;**workflow-users**。

## 动态用例

关联UI支持即时、个性化的文档生成，这对于具有实时服务需求的行业至关重要。

| 行业 | 示例用例 |
|----------|-------------------|
| **金融服务** | 生成实时贷款确认函、风险状况摘要和账户创建。 |
| **保险** | 生成即时保险证明卡或索赔处理摘要。 |
| **医疗保健** | 使用计算的copay和时间表创建患者治疗计划摘要。 |
| **公共部门** | 当场生成警方核查报告、公民服务收据、申诉确认信和案件更新摘要。 |
| **政府** | 为福利计划注册创建申请状态摘要、服务批准书和实时通信。 |

## 启用关联UI

作者启用关联UI，并可以选择配置工作流以在&#x200B;**交互式通信设置**&#x200B;中提交：

1. **启用关联视图** — 在&#x200B;**关联属性**&#x200B;中，选中&#x200B;**启用关联视图编辑**，然后单击&#x200B;**应用更改**&#x200B;并保存文档。
2. **配置工作流（可选）** — 在&#x200B;**工作流**&#x200B;中，打开&#x200B;**配置更新工作流**，选择工作流模型，并可以选择设置成功消息和重定向URL。
3. **配置可编辑的字段** — 启用关联可以编辑和设置验证的字段。
4. **发布并共享** — 发布IC并与关联共享链接。

有关屏幕截图和提交/工作流行为（作者与发布关联）的分步说明，请参阅[为交互式通信启用并配置关联UI](/help/forms/interactive-communication/enable-configure-associate-ui.md)。 要构建通过IC提交生成PDF的工作流，请参阅[关联UI的提交工作流 — IC生成PDF输出](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md)。

**关联UI**&#x200B;弥合了结构化内容创作与实时客户参与之间的差距。\
通过结合直观的设计、强大的后端配置和严格的法规遵从性控制，组织可以大规模提供&#x200B;**快速、准确和个性化的通信**。

## 另请参阅

- [为交互式通信启用并配置关联UI](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [在应用程序中集成关联UI](/help/forms/interactive-communication/invoke-associate-ui.md)
- [关联UI的提交工作流 — IC生成PDF输出](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md)
