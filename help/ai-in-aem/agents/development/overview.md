---
title: 开发代理概述
description: 了解AEM中的开发代理如何分析Cloud Manager中的失败管道并构建日志以建议代码修复和加快调试。
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Architect, Developer
exl-id: 2194556f-aac2-4cdd-8f7f-00c92c8c4424
source-git-commit: eeaa119711b480197b5807b85eb9c566a735f270
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# 开发代理概述 {#development-agent-overview}

开发代理可帮助AEM开发人员和管理员更高效地创建、调试、部署和优化代码。

目前，代理可以检索管道状态，并通过建议修复来帮助您排除失败的构建步骤，从而节省在开发、暂存和生产环境中调试AEM as a Cloud Service部署的时间。 它会检查构建日志和相关代码，以推荐您可以手动应用的修复。

>[!VIDEO](https://video.tv.adobe.com/v/3478017?captions=chi_hans&quality=12&learn=on)

>[!IMPORTANT]
>
>AI生成的响应可能不准确或具有误导性。 请务必仔细检查建议的修复和响应。
>
>另请参阅[Adobe Experience Cloud Generative AI用户指南](https://www.adobe.com/cn/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

要访问此代理，请参阅[发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)以了解如何注册测试版计划的说明，并确保表明您对开发代理感兴趣。 您还可以通过电子邮件将特定于开发代理的反馈发送至[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)。

[观看教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/ai/development-agent-troubleshoot-ci-cd-pipeline)，了解如何使用开发代理解决管道故障问题。

## 通过Cloud Manager访问开发代理 {#how-to-access-the-agent}

您可以通过用户界面中的AI助手访问开发代理，包括Cloud Manager或Experience Hub。

**要通过Cloud Manager访问开发代理，请执行以下操作：**

1. 若要开始，请单击[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)打开其主页。

   ![Adobe Experience Cloud主页](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. 在左边栏中的&#x200B;**服务**&#x200B;标题下，单击&#x200B;**Cloud Manager**。

   ![已选定显示内容作者预设的下拉列表](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >显示的构件、工具和工件取决于用户角色、权限和AEM部署类型(AEM as a Cloud Service或Managed Services 6.5/6.5 LTS)。

1. 在左边栏中的&#x200B;**项目**&#x200B;下，单击&#x200B;**![概述图标](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg)概述**。

1. 在&#x200B;**项目概述**&#x200B;页面的&#x200B;**管道**&#x200B;信息卡中，单击管道。

   ![所选的管道](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-select.png)

1. 在&#x200B;**内部版本和代码扫描**&#x200B;页面中，请注意失败的管道。

   ![管道故障，在“生成和代码扫描”页面中看到](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-failure.png)

1. 在AEM用户界面的右上角(从Cloud Manager页面或AEM环境的创作实例)附近，单击&#x200B;**AI助手**&#x200B;图标。

   工具栏上的![AI助手图标](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   另请参阅AEM中的[AI助手](/help/implementing/cloud-manager/ai-assistant-in-aem.md)。

1. 在底部附近的&#x200B;**AI助手**&#x200B;面板文本框中，键入您的问题或提示，然后按`Enter`或单击![发送图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)。

   例如：
   *在“eda-org-01-no-access”程序中，分析“no-access”管道的故障并进行故障排除。*

   此提示将导致以下响应。

   ![AI助手提示和生成的响应](/help/ai-in-aem/agents/development/assets/dev-agent-prompt-response.png)


## 权限 {#permissions}

开发代理的管道故障排除工作需要Cloud Manager — 开发人员角色或Cloud Manager — 项目经理角色。

## 示例提示 {#sample-prompts}

| 提示 | 结果 |
| --- | --- |
| *对失败的管道进行故障排除* | 执行管道失败原因分析；如果不清楚引用了哪个管道，将向用户询问其他问题。 |
| *为项目主项目列出我的失败管道。* | 虽然结果可能有所不同，但此提示会输出一个失败管道表，并提供一个后续建议，以引用要分析的特定管道。 |
| *分析我失败的、名为“开发管道”的管道。* | 此提示将导致分析失败的管道，并提供修复建议。 如果多次失败，则会询问用户其他问题。 |
| *管道执行疑难解答1234567* | 通过提供准确的管道执行ID，执行管道分析。 |

## 超出范围的功能 {#out-of-scope-features}

管道故障排除在全栈管道的构建步骤中进行。 对于其他管道类型和步骤，通过下载并检查日志来调试故障。

查看[访问和下载日志](/help/implementing/cloud-manager/manage-logs.md)。
