---
title: 配置AI翻译集成
description: 了解如何使用翻译云服务和翻译集成框架将Adobe Experience Manager连接到Azure OpenAI以进行代理翻译。
feature: Language Copy
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="适用于AEM Sites)。"
solution: Experience Manager Sites
source-git-commit: cb7dcc07a5913d6c7e88e0eec03f0003f1e3997a
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# 配置AI翻译集成 {#ai-translation-integration}

人工智能翻译集成允许您使用&#x200B;**大型语言模型(LLM)**&#x200B;作为您在Adobe Experience Manager中创作的内容的翻译服务。 您可以将AEM连接到LLM提供商（从Microsoft Azure OpenAI开始），重复使用与其他连接器相同的[翻译工作流](/help/sites-cloud/administering/translation/overview.md)，还可以选择上传&#x200B;**翻译样式指南**，以便AEM可以生成在不同区域设置之间保持语气、术语和品牌语言一致的规则。

有关翻译项目、云配置和翻译集成框架的背景，请参阅[翻译多语言站点的内容](overview.md)和[配置翻译集成框架](integration-framework.md)。

## 人工智能翻译如何适应AEM {#how-ai-translation-fits-in-aem}

大型语言模型可以翻译全段，关注上下文、语调和习语，而不是字面逐字替换。 在配置AI翻译集成时，LLM作为&#x200B;**第三方翻译服务**&#x200B;的方式与您通过AEM连接的其他提供商相同。 您为LLM服务提供&#x200B;**自己的许可证和凭据**。

初始支持将AEM连接到&#x200B;**Azure OpenAI**。 Adobe计划在以后的版本中添加对其他提供商的支持。

在&#x200B;**翻译云服务**&#x200B;中配置LLM连接和可选样式指南以及其他翻译配置。 您可以为不同的[云配置](/help/sites-cloud/administering/translation/integration-framework.md#creating-a-translation-integration-configuration)使用不同的翻译服务；例如，一个配置可以使用人工智能翻译，而另一个配置使用传统的机器翻译连接器。

## 配置翻译云服务 {#configure-translation-cloud-services}

在管理其他翻译云配置的同一区域设置AI翻译。

1. 在[全局导航菜单](/help/sites-cloud/authoring/basic-handling.md#global-navigation)中，选择&#x200B;**工具** > **云服务** > **翻译云服务**。
1. 打开或创建要在其中启用AI翻译的配置（如果该功能应广泛应用，则包括`/conf/global`）。

![翻译云服务控制台显示管理翻译配置的位置。](assets/ai-translation-integration/aem_ai-translation_translation-cloud-services.png)

## 配置LLM连接 {#configure-the-llm-connection}

**代理翻译配置**&#x200B;体验包含用于连接提供商的&#x200B;**LLM配置**&#x200B;部分。

1. 打开翻译云服务条目的AI翻译配置。
1. 选择&#x200B;**[!UICONTROL LLM配置]**。
1. 选择您的提供商（例如，**Azure OpenAI**）。
1. 输入订阅所需的凭据和终结点详细信息（**API密钥**、**API版本**、**基本路径**、**部署名称**&#x200B;以及您的提供商所需的任何其他字段）。
1. 保存配置。

![带有LLM配置选项卡和Azure OpenAI字段的代理翻译配置屏幕。](assets/ai-translation-integration/aem_ai-translation_agentic-translation-llm-config.png)

## 添加翻译样式指南和生成的规则 {#add-translation-style-guides-and-generated-rules}

您可以上传&#x200B;**翻译样式指南**&#x200B;文档（通常每个目标语言一个）。 AEM分析每个指南并生成&#x200B;**翻译规则**，以使输出符合您的品牌和语言预期。

1. 在&#x200B;**代理翻译配置**&#x200B;中，选择&#x200B;**[!UICONTROL LLM准则]**。
1. 选择区域设置并使用&#x200B;**[!UICONTROL 上传]**&#x200B;添加该语言的样式指南文档。
1. AEM处理指南时，状态指示器显示进度（**处理**、**已完成**&#x200B;或&#x200B;**已中止**）。
1. 在编辑器中查看或编辑生成的规则（例如，捕获提示音、术语和示例的JSON）。

![LLM Guidelines选项卡显示选定语言的区域设置列表和生成的翻译规则。](assets/ai-translation-integration/aem_ai-translation_agentic-translation-llm-guidelines.png)

## 在框架中设置默认翻译方法 {#set-the-default-translation-method-in-the-framework}

保存云配置后，在创建翻译项目时，将&#x200B;**代理翻译**&#x200B;注册为[翻译集成框架](integration-framework.md)配置中的默认行为。 如果需要，您可以为每个项目更改方法。

![显示包括代理翻译的翻译方法选项的“翻译集成框架站点”选项卡。](assets/ai-translation-integration/aem_ai-translation_translation-integration-framework-default.png)

## 运行翻译项目 {#run-translation-projects}

配置AI翻译并将其与页面关联后，您可以[像创建其他翻译提供商一样创建并运行翻译项目](managing-projects.md)。 页面、内容片段和资产中的内容遵循翻译规则和框架设置。

>[!NOTE]
>
>AI翻译集成是&#x200B;**非**&#x200B;可用的，可在Adobe Experience Manager](/help/implementing/cloud-manager/ai-assistant-in-aem.md)聊天UI中的[AI助手或Experience Production Agent界面中使用。 使用本文中所述的翻译工作流和控制台。

