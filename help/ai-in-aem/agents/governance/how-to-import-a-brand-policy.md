---
title: 如何导入品牌策略
description: 使用Adobe Governance Agent导入品牌策略
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 94d671ebbd5aeb5992fdbc9d779ffbca51f82585
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---


# 如何导入品牌策略 {#how-to-import-a-brand-policy}

## 概述 {#overview}

品牌策略定义了规则、标准和约束，以确保Adobe Experience Manager生成或更新的所有内容均与公司的品牌标识保持一致。 这通常包括语调、术语、视觉准则和编辑规则。

治理代理使用品牌策略作为事实来源，来分析现有页面并指导内容生成。 客户可以提供其自己的原始品牌策略，治理代理会自动将其转换为人工智能可读的策略检查。 这些检查随后用于验证内容并为生产代理提供可靠、可执行的框架，以生成或更新与品牌保持一致的页面。

## 什么是治理代理中的品牌策略 {#what-is-a-brand-policy-in-the-governance-agent}

在治理代理的上下文中，品牌策略是品牌规则的结构化表示形式，可由AI理解和实施。 治理代理不要求客户以技术格式重写其准则，而是接受原始形式的品牌策略（例如文档、准则或规则描述）。

导入策略后，该策略将转换为一组AI策略检查，这些检查可以：

* 分析现有页面以检测品牌不一致
* 标记与语气、术语或强制规则的偏差
* 为下游代理提供明确指导
* 通过设计确保生成或更新内容符合品牌规范

这种方法允许团队重复使用其现有的品牌文档，同时受益于自动化治理和可扩展的内容生产。

## 如何使用品牌策略 {#how-brand-policies-are-used}

导入品牌策略后：

* 治理代理将策略解释并标准化为可强制执行的AI检查
* 可以根据策略分析页面以确定差距或违规
* 在生成或更新内容时，生产代理会将这些检查用作约束
* 跨网站和团队实现一致、可重复和可审核的品牌合规性


## 导入品牌策略 {#import-a-brand-policy}

要将品牌导入治理代理，请执行以下操作：

1. 通过指定名称和主域创建品牌。 为此，您可以单击Experience Manager主页左侧导航栏中的&#x200B;**治理上下文**&#x200B;按钮，然后按&#x200B;**+添加Brand**&#x200B;按钮，如下所示：

   ![添加新品牌](/help/ai-in-aem/agents/governance/assets/add_brand.png){width="70%"}

1. 在以下窗口中设置品牌名称和描述

   ![命名品牌](/help/ai-in-aem/agents/governance/assets/add_brand_dialogue.png){width="60%"}

1. 新品牌将以草稿状态创建。 确保将新创建的品牌更改为“活动”状态，方法是：单击品牌的卡片，按屏幕右上角的编辑（铅笔），在以下窗口中将&#x200B;**状态**&#x200B;设置为&#x200B;**活动**，然后单击&#x200B;**保存更改**。 您需要先将品牌设置为“活动”以启用品牌，然后才能使用它们。

   ![将品牌的状态设置为“活动”](/help/ai-in-aem/agents/governance/assets/set_brand_active.png){width="60%"}

1. 创建品牌后，请按左侧的&#x200B;**域**&#x200B;链接在下列窗口中创建一个主域：

   ![为品牌配置域](/help/ai-in-aem/agents/governance/assets/add_domain.png)

   >[!IMPORTANT]
   >
   >就像新品牌一样，新域也是以默认草稿状态创建的。 若要更改此设置，请转到您的品牌，单击&#x200B;**域**，然后使用铅笔图标编辑您的域并将其状态设置为&#x200B;**活动**。

1. 配置主域后，您可以上载品牌策略文档，方法是：登录到窗口左上角的&#x200B;**策略**，然后按&#x200B;**+添加策略**&#x200B;按钮。

   ![从品牌卡添加策略](/help/ai-in-aem/agents/governance/assets/add_policy_treeview.png)

   >[!NOTE]
   >
   >或者，您也可以通过切换到&#x200B;**策略**&#x200B;选项卡并按&#x200B;**+添加策略**&#x200B;链接来添加策略。

1. 在下一个窗口中，按&#x200B;**上传PDF**&#x200B;并选择PDF格式的品牌策略文档

   ![上载您的品牌策略文档](/help/ai-in-aem/agents/governance/assets/upload_brand_policy_document.png){width="70%"}

   治理代理将使用自然语言解析您的品牌策略指南，并将提取从文档获得的检查并将其转换为实际任务。 处理文档后，您可以查看导入的摘要，包括检查数量和策略状态，如下所示：

   ![品牌策略状态的概述窗口](/help/ai-in-aem/agents/governance/assets/policy_status.png)

1. 创建品牌并上传策略文档后，您可以通过转到&#x200B;**品牌**&#x200B;选项卡，然后单击品牌的卡片来获取详细的按品牌显示的视图。 通过按现有类别旁边的三个圆点，然后选择&#x200B;**+添加类别**，您将使用此视图来创建检查的类别，如下面的屏幕快照所示：

   ![添加类别](/help/ai-in-aem/agents/governance/assets/add_category.png)

   您也可以使用此视图来创建、编辑和删除检查，我们将在以下步骤中详细介绍这些检查。

1. 若要更详细地查看每张支票，可以切换到&#x200B;**支票**&#x200B;选项卡，并查看从准则文档提取的每张支票的列表。 您可以根据品牌或状态筛选检查：

   ![查看各个品牌检查](/help/ai-in-aem/agents/governance/assets/see_brand_checks.png)

   此外，您还可以通过单击支票左侧的三个圆点(**...**)并按&#x200B;**查看详细信息**&#x200B;来查看每个支票的其他详细信息。 这将打开一个新窗口，其中包含有关检查的详细信息：

   ![查看单个支票详细信息](/help/ai-in-aem/agents/governance/assets/view_check_details.png)

   您还可以在同一菜单位置按&#x200B;**删除**&#x200B;来删除检查，或者按&#x200B;**编辑**&#x200B;来编辑它们：

   ![编辑支票](/help/ai-in-aem/agents/governance/assets/edit_check.png)

1. 您可以通过按“支票”窗口左上角的&#x200B;**添加支票**&#x200B;来手动添加支票：

   ![添加支票](/help/ai-in-aem/agents/governance/assets/add_check.png)

   在以下屏幕中，您可以配置详细信息，例如：

   * 支票的名称
   * 用自然语言描述的规则
   * 类别
   * 它适用的范围

   ![配置检查详细信息](/help/ai-in-aem/agents/governance/assets/add_check_window.png)

1. 最后，要获取域及其关联的品牌的列表，您可以按&#x200B;**域**&#x200B;选项卡。 此部分允许您添加、删除或修改列表中的域。

