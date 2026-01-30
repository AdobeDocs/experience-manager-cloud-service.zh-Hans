---
title: 将MCP与AEM as a Cloud Service结合使用
description: 了解如何将模型上下文协议与AEM as a Cloud Service一起使用
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 3ff5ef0be78f5f5a61c81c8ab0388b56fa134047
workflow-type: tm+mt
source-wordcount: '2016'
ht-degree: 0%

---


# 将MCP与AEM as a Cloud Service结合使用 {#using-mcp-with-aem-as-a-cloud-service}

## 简介 {#introduction}

许多AEM团队现在都在IDE和基于聊天的应用程序中工作，例如Cursor、ChatGPT、Anthropic Claude和Microsoft Copilot Studio。 这些应用程序支持模型上下文协议(MCP)，它允许应用程序以标准化方式向大型语言模型(LLM)公开后端工具。

通过AEM的MCP集成，不同的角色可以围绕相同的内容进行协作：

* **开发人员**&#x200B;可以从其IDE或聊天应用程序编排内容操作和工作流
* **从业者**&#x200B;和内容架构师可以在AI帮助下管理站点、内容片段和资源，同时保留AEM的现有权限模型。

>[!IMPORTANT]
>
> 对于修改或删除内容的场景，从业人员应使用AI Assistant界面，而不是直接调用MCP工具，因为AI Assistant运行的AEM Agent包含内置安全保护。
>

本文介绍了AEM的MCP功能提供了哪些功能，支持哪些MCP应用程序，如何配置这些功能，以及如何在实践中使用该功能。

## 为什么MCP对AEM客户有用 {#why-mcp-is-useful-for-aem-customers}

现代IDE和聊天应用程序使用MCP作为LLM调用MCP服务器后面公开的工具的一种方式。 客户可以使用自然语言描述其意图，而不是根据低级API规范编写代码（*“在所有页面上更新此促销活动的主页横幅”*），并允许LLM调用相应的MCP工具，这些工具反过来将与AEM的API进行交互。

主要优势包括：

* **自然语言交互而不是API管道**
MCP工具描述了哪些操作可用以及如何调用它们。 LLM使用这些模式来确定要调用哪些工具以及使用哪些参数。
* **跨应用程序的一致体验**
相同的AEM MCP工具可用于多个MCP兼容应用程序，使团队能够在调用相同的底层AEM功能时，在最高效的地方工作。
* **已保留安全和治理**
对AEM MCP工具的请求在经过身份验证的用户身份下运行，每个工具都强制实施用户的现有AEM权限。 人工智能辅助的操作遵循与AEM中的手动工作相同的访问规则。

## AEM提供的MCP服务器 {#mcp-servers-provided-by-aem}

AEM将MCP服务器公开为HTTP端点。 下面列出的端点与以下对象相关：

`https://mcp.adobeaemcloud.com/adobe/mcp/`

### MCP服务器 {#mcp-servers}

| **MCP服务器** | **终结点** | **描述** |
|---|---|----------------------------------------------------------------------------------------------------------------------|
| **内容** | `/content` | 所有低级内容操作，包括创建、读取、更新和删除(CRUD)页面、片段和资产。 |
| **内容（只读）** | `/content-readonly` | 页面、片段和资产的只读内容操作（获取、列表/搜索）。 |

每个MCP服务器公开的特定工具可能会随着时间的推移而不断演变。 在实践中，您可以要求启用了MCP的应用程序通过提示来发现工具，例如：

*“列出此服务器上可用的所有AEM MCP工具，并描述它们执行的操作。”*

MCP客户端将使用MCP协议来检索工具列表和模式，然后LLM可以使用这些工具。

## 支持的MCP应用程序 {#supported-mcp-applications}

AEM的MCP服务器设计为可与定义的一组兼容MCP的应用程序配合使用。 支持以下应用程序：

* 克洛德
* 光标
* OpenAI ChatGPT
* Microsoft Copilot Studio

每个应用程序都提供自己的配置体验，但高级步骤类似。

## 设置概述 {#setup-overview}

为AEM配置MCP涉及两个主要部分：

1. **每个MCP客户端应用程序中的配置**，以便应用程序知道如何连接到AEM MCP服务器并执行OAuth登录
1. **在开始提示之前选择MCP服务器**，以便MCP客户端知道要使用它。

### AEM配置 {#aem-configuration}

默认情况下，对AEM MCP服务器的访问受各个用户在AEM中拥有的权限控制。 当用户通过MCP客户端应用程序进行身份验证时，MCP工具会强制实施与AEM中的手动操作相同的访问规则。 用户只能执行已授权他们执行的操作。

#### 允许的MCP客户端应用程序 {#permitted-mcp-client-applications}

默认情况下，允许使用以下MCP客户端应用程序：

* ChatGPT
* 克劳德
* MS Copilot Studio
* 光标

#### 限制MCP服务器 {#restricting-mcp-servers}

默认情况下，所有MCP服务器都会被列入允许列表。 作为管理员，您可以选择在组织、项目或环境级别限制对特定MCP服务器的访问。 这使您能够精细地控制贵组织内的用户可以使用哪些MCP功能。

#### 管理MCP客户端访问 {#managing-mcp-client-access}

如果贵组织的策略需要，管理员还可以禁用对特定MCP客户端应用程序的访问。 如果您希望Adobe启用对其他MCP客户端产品的支持，请发送指向产品网站的链接。 如果您需要允许列表自定义MCP客户端，请联系。

对于所有MCP服务器相关请求，请随时通过&#x200B;**aemcs-mcp-feedback@adobe.com**&#x200B;联系我们

### MCP客户端应用程序配置 {#mcp-client-application-configuration}

此步骤由每个用户（或在支持的地方由MCP客户端应用程序的管理员执行）执行。 不同应用程序的配置详细信息略有不同。 MCP客户端发展迅速，并且正在积极开发对远程MCP服务器的支持。 您可能需要启用开发人员模式才能访问添加远程服务器的功能，但常规过程是：

1. 添加AEM MCP服务器URL
   * 从上表中配置MCP端点。 例如：`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. 触发连接
   * 保存或激活配置，以便MCP客户端应用程序尝试连接到AEM MCP服务器
1. 使用Adobe ID登录
   * 出现提示时，请完成Adobe登录流程，以便应用程序能够获得与您的Adobe ID关联的OAuth令牌
1. 验证发现的工具
   * 经过身份验证后，应用程序将从服务器发现MCP工具。 然后，您可以开始提示LLM执行AEM操作。

下面是每个受支持的应用程序在高级别上的外观示例。

**ChatGPT**

![配置ChatGPT步骤1](assets/chatgpt-1.png)

![配置ChatGPT步骤2](assets/chatgpt-2.png)

![配置ChatGPT步骤3](assets/chatgpt-3.png)

![配置ChatGPT步骤4](assets/chatgpt-4.png)

![配置ChatGPT步骤5](assets/chatgpt-5.png)

![配置ChatGPT步骤6](assets/chatgpt-6.png)

![配置ChatGPT步骤7](assets/chatgpt-7.png)

* 在配置了MCP连接或工具的区域添加AEM MCP服务器URL
* 在重定向时触发连接并使用Adobe ID登录
* 在聊天中，在提示中引用配置的AEM工具，例如：

  *“使用配置的AEM MCP工具，列出创作环境中的所有站点。”*

**克劳德**

![配置克劳德步骤1](assets/claude-1.png)

![配置克劳德步骤2](assets/claude-2.png)

![配置克劳德步骤3](assets/claude-3.png)

![配置克劳德步骤4](assets/claude-4.png)

![配置克劳德步骤5](assets/claude-5.png)

![配置克劳德步骤6](assets/claude-6.png)

![配置克劳德步骤7](assets/claude-7.png)

* 在Claude的MCP配置中，注册AEM MCP服务器URL
* 完成Adobe登录流程
* （可选）在配置区域为某些工具启用自动确认。 建议将此用于搜索或只读操作。
* 在开始对话之前，请确保已选择MCP服务器
* 要求Claude执行与AEM相关的任务；Claude将根据您的提示选择MCP服务器公开的AEM工具。

**游标**

![配置游标步骤1](assets/cursor-1.png)

![配置游标步骤2](assets/cursor-2.png)

![配置游标步骤3](assets/cursor-3.png)

![配置游标步骤4](assets/cursor-4.png)

![配置游标步骤5](assets/cursor-5.png)

* 在Cursor的MCP设置中，使用AEM MCP URL创建一个新的MCP服务器条目
* 出现提示时，使用您的Adobe ID进行身份验证
* （可选）通过单击工具名称启用或禁用单个工具。 默认情况下，所有工具都处于启用状态。
* 使用光标的编辑器或聊天工具在开发或内容工作流中调用AEM工具。

**Microsoft Copilot Studio**

![配置Copilot步骤1](assets/copilot-1.png)

![配置Copilot步骤2](assets/copilot-2.png)

![配置Copilot步骤3](assets/copilot-3.png)

![配置Copilot步骤4](assets/copilot-4.png)

![配置Copilot步骤5](assets/copilot-5.png)

![配置Copilot步骤6](assets/copilot-6.png)

![配置Copilot步骤7](assets/copilot-7.png)

![配置Copilot步骤8](assets/copilot-8.png)

![配置Copilot步骤9](assets/copilot-9.png)

![配置Copilot步骤10](assets/copilot-10.png)

* 创建新代理
* 导航到工具部分，然后单击&#x200B;**添加工具**
* 选择现有工具或创建新工具
* 配置指向AEM MCP服务器URL的新MCP工具
* 建立可在代理之间共享或专用的连接
* 重定向后使用您的Adobe ID登录
* （可选）启用自动确认模式或要求最终用户确认所有工具交互
* 测试代理时，请先打开连接管理器以向会话分配连接，然后按&#x200B;**重试**。

## 身份验证 {#authentication}

Adobe托管的MCP服务器实施OAuth，并与Adobe的Identity System集成。

* 当MCP客户端应用程序连接到AEM MCP服务器时，用户会看到Adobe登录对话框并使用其&#x200B;**Adobe ID**&#x200B;进行身份验证
* 成功登录后，系统会验证您的组织是否允许MCP客户端应用程序，以及是否允许请求的MCP服务器。 如果任一检查失败，则会显示错误消息。

![MCP客户端不允许错误](assets/MCP-Client-not-permitted.png)

* 验证后，MCP服务器会颁发应用程序用于后续工具调用的令牌
* MCP工具会尊重用户的AEM权限。 无权在AEM中修改内容片段的用户也无法通过MCP修改它。

这可确保AI辅助的操作符合您现有的AEM安全和治理模型。

## 将MCP与AEM结合使用 {#using-mcp-with-aem}

配置AEM和MCP客户端应用程序后，您可以在选择的应用程序中工作，并提示LLM执行AEM操作。 LLM读取MCP工具架构，选择要调用的工具，并根据需要对这些工具进行排序，以满足您的请求。

>[!IMPORTANT]
>
>为了获得最佳结果，尤其是对于包含多个步骤或针对不同内容类型（如图像和文本）的提示，请在MCP客户端中启用思考模型或选择“思考”选项，而不是依赖于“自动”模式。

### 示例用例 {#example-usecases}

一些典型的情况包括：

* **环境发现**
   * 列出环境和许可证以决定运行工作流的位置。

* **站点管理**
   * 列出站点
   * 创建、读取、更新和删除页面和页面内容。

* **内容片段管理**
   * 搜索内容片段
   * 创建新片段
   * 当营销活动消息更改时，更新现有片段。

* **Assets管理**
   * 导入资源
   * 查找现有资源
   * 发布资源。

### 示例工作流 {#example-workflows}

以下示例说明了LLM如何将MCP工具链接在一起。

1. **使用页面引用的内容片段**
   * **获取页面内容** — 调用诸如`get-aem-page-content`之类的工具以检索页面并找到`fragmentPath`属性。
   * **解析片段路径** — 使用`resolve_fragment_path`将路径转换为UUID。
   * **获取片段数据** — 调用`get_fragment`以检索当前字段。
   * **更新片段** — 调用`patch_fragment`以将更改应用于片段内容。
1. **基于模型创建新内容**
   * **发现模型** — 使用`list_models`查看哪些内容片段模型可用。
   * **检查模型** — 使用`get_model`了解模型的字段架构。
   * **创建内容** — 使用`create_fragment`创建一个新片段，其值派生自您的提示。
1. **安全更新现有内容**
   * **读取当前数据** — 使用`get_fragment`检索现有数据和ETag。
   * **应用JSON修补程序** — 将`patch_fragment`与ETag和JSON修补程序文档一起使用以更新片段，支持开放式并发。

从用户的角度来看，这些工作流可以通过提示来启动，例如：

*“根据主页横幅模型为春季促销活动创建新的内容片段，并从此简介填写其字段。”*

LLM自动选择并协调必要的MCP工具。

## 期望管理 {#expectation-management}

在通过MCP使用LLM时，请牢记以下几点：

* **功能强大，但不是万无一失**
LLM可以完成复杂的任务，但容易偶尔出错。 相同的提示可能会产生稍微不同的结果或演示，但没有明显的原因。 始终在将更改应用于生产内容之前审查输出。

* **不断发展的功能**
LLM模型正在不断改进。 随着时间的推移，他们在发现组合MCP工具以实现目标的新方法方面变得更加智能。 今天需要多个提示的任务明天可以无缝地处理单个提示。

* **人的监督是必不可少的**
把LLM想成需要监督的知识渊博的助手。 它拥有广泛的知识，可以设计创造性的解决方案，但它受益于您的指导和审查。 验证结果（尤其是关键操作的结果），并在输出与预期不符时提供反馈。

* **对于自动确认工具执行要小心**
某些MCP客户端应用程序（如Claude）提供了自动确认LLM请求的工具执行的选项。 虽然这对于只读操作（如搜索或检索内容）很方便，但请谨慎使用更新或删除内容的工具。 在确认修改AEM环境的操作之前，请查看每个工具执行请求。

## 限制 {#limitations}

AEM的MCP服务器目前打算在ChatGPT、Claude、Cursor和Microsoft Copilot Studio中进行配置。

如果要使用其他MCP客户端应用程序，请随时联系&#x200B;**aemcs-mcp-feedback@adobe.com**，请求支持其他客户端或列入允许列表自定义客户端。
