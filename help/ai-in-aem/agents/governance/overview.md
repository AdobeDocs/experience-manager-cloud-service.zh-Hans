---
title: 治理代理概述
description: 了解AEM治理代理如何跨AEM保护品牌完整性和合规性
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 9b26cd1f30ad6fa23e28c9f36fe48091e069962e
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# 治理代理概述 {#governance-agent}

**治理代理**&#x200B;是一种旨在跨Adobe Experience Manager保护品牌完整性和合规性的解决方案。 它强制执行安全、法规和品牌政策，以确保每次交互和激活都遵守既定标准。 治理代理已完全集成在AI助手中，设计用于利用&#x200B;**A2A（代理到代理）**&#x200B;和&#x200B;**MCP（模型控制协议）**&#x200B;工具在企业环境中无缝运行。 这些集成使代理能够与高级AI协调器（如ChatGPT、Claude和其他外部AI系统）联系，确保跨平台的灵活和可伸缩的智能。

主要功能包括：

* **品牌治理：**&#x200B;通过自动跨内容和资产进行品牌检查，保持品牌一致性并减少手动审查
* **权限和Digital Rights Management (DRM)：**&#x200B;通过跨数字资源控制权限和使用权限，确保安全合规的协作。

通过结合这些功能，Governance Agent降低了风险，并实现快速、安全和大规模的品牌上交付。

>[!IMPORTANT]
>
>AI生成的响应可能不准确或具有误导性。 请务必仔细检查建议的修复和响应。
>
>另请参阅[Adobe Experience Cloud Generative AI用户指南](https://www.adobe.com/cn/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

## AEM Governance Agent技能 {#skills-in-aem-governance-agent}

### 品牌治理 {#brand-governance}

治理代理可以根据品牌准则验证内容，以确保所有数字体验的一致性。 它使用预先摄取的品牌规则，如语气、声明、徽标使用、排版和图像。 它在Experience Hub的聊天、编辑和批量模式下实时运行，因此非常适合于AI生成的内容、站点迁移和基于摘要的站点创建。

![品牌治理概述](/help/ai-in-aem/agents/governance/assets/brand-governance.png)

**提示示例：**

* *此页面是否符合我的品牌？`https://www.website/en.html`*
* *此`https://www.website/en.html`是否遵循品牌消息传递指南？*
* *检查`https://www.website/homepage`是否遵循品牌指南*
* *显示我的品牌指南*

### 权限和Digital Rights Management {#permission-and-digital-rights-management}

#### Content Hub中的权限管理 {#permission-management-in-content-hub}

在Content Hub中，治理代理可确保只有合适的人员在合适的时间访问合适的资产。 通过应用精细的、基于属性的控制和使用权限，它可以保护敏感内容，同时实现安全协作。 这意味着降低了合规性风险，增强了品牌完整性，并加快了工作流程，团队可以放心地共享和重复使用资产，而无需担心未经授权的访问或滥用。 安全性和灵活性之间的这种平衡转化为更高的运营效率和整个组织内的信任。

![权限管理概述](/help/ai-in-aem/agents/governance/assets/permission-management.png)

**提示示例：**

* *显示所有现有的Content Hub ABAC规则。*
* *创建一个允许“营销”组访问所有资产的规则。*
* *授予“销售组”对市场营销:segment等于EMEA的资产的访问权限。*
* *删除所有授予外部代理访问权限的规则*
* *什么是Content Hub中的ABAC，你能帮助我做什么？*

#### Assets Digital Rights Management {#assets-digital-rights-management}

使用该代理，您可以在内容生态系统中管理您的Assets数字权限。 它可以在精细的级别控制权限和使用权限，确保仅在定义的法规遵从性边界内访问和使用资产。 这可以让您高枕无忧，保护知识产权，降低管理风险，并维护品牌完整性。 通过自动化权限实施，团队可以安全而自信地协作，从而在不影响安全性或法规遵从性的情况下加快内容分发。

![DRM管理概述](/help/ai-in-aem/agents/governance/assets/drm-management.png)

**提示示例：**

* *我的任何资源是否即将过期？*
* *查找上个月过期的所有自行车资源。*
* *哪些资产最近过期？*
* *查找没有到期日期的资源*
* *显示/content/dam/products中将在未来14天内过期的所有资产*

