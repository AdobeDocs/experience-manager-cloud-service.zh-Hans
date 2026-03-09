---
title: AEM创作项目的Experience现代化代理快速入门
description: 了解在使用Experience Modernization Console开始使用Experience Modernization Agent时，AEM创作项目所需的具体设置步骤。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: a1b2c3d4-e5f6-4789-a012-3456789abcde
source-git-commit: df23c3a4c497943135f8719425225526ae14aa92
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---


# AEM创作项目的Experience现代化代理快速入门 {#getting-started-aem-authoring}

对于使用通用编辑器的AEM创作项目，Experience现代化代理的准备工作与标准Edge Delivery流程不同。 本文档介绍了这些设置差异。 完成以下步骤后，请按照主[Experience现代化代理快速入门](getting-started.md)指南操作。

## 创建您的Edge Delivery Services项目存储库 {#create-repo}

1. 使用[`aem-block-collection-xwalk`](https://github.com/adobe-rnd/aem-block-collection-xwalk)存储库作为您的模板(不是标准Edge Delivery Services样板)。
1. 按照[Universal Editor教程](https://www.aem.live/developer/ue-tutorial)设置存储库。
   * 当要求您在AEM中创建站点时停止。
1. 删除`paths.json`并将此更改提交到`main`。
1. 将[AEM Code Connector](https://github.com/apps/aem-code-connector/installations/select_target)应用程序添加到存储库。
   * 这将允许控制台检查您的代码。

## 在AEM中创建新站点 {#create-site}

1. 在AEM Sites控制台中，选择&#x200B;**创建** > **从模板创建站点**。
1. 选择&#x200B;**包含Edge Delivery Services模板的AEM网站**。
   * 没看到它列在清单上吗？ [安装模板。](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)
1. 保留提供的&#x200B;**名称**&#x200B;网站（不是标题）。
   * 站点名称用作唯一标识符。
   * 可以更改标题以进行显示。
1. 单击&#x200B;**创建**。
   * 您将被重定向到“站点”页面。
   * 如果新站点未立即显示，请刷新页面。
1. 如果您在[设置存储库时尚未执行该操作，](#create-repo)将更新`fstab.yaml`，使其指向您的AEM主机、Git所有者和Git存储库，并将这些更改提交到`main`。
   * 有关说明，请参阅[配置内容源](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md)。

## 继续执行标准入门步骤 {#continue}

完成上述步骤后，您可以继续使用标准入门指南来开始迁移您的内容。

![内容导入](assets/content-import.png)

按照标准指南中的步骤操作。

1. [准备Edge Delivery GitHub存储库](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#prepare-repo)
1. [打开“体验现代化”控制台](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#open-console)
1. [连接您的GitHub存储库](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#connect-repo)
1. [开始提示](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#start-prompting)

![内容已导入](assets/content-imported-aem-authoring.png)

完成这些步骤以迁移内容后，请继续执行以下步骤。

## 验证内容 {#validate-content}

在预览面板中验证所选页面的内容。 单击&#x200B;**错误**按钮将显示任何错误。
继续与座席进行聊天对话以修复错误。 使用**添加到聊天**&#x200B;功能，将修复定位到页面、解析器文件或转换器文件的特定元素。

![上下文聊天](assets/contextual-chat.png)

## 上传内容 {#upload-content}

要将您的内容上传到AEM，请执行以下操作：

1. 确保您处于&#x200B;**Content**&#x200B;视图中，然后单击右上方的&#x200B;**Upload content**&#x200B;按钮。
1. 在&#x200B;**创建内容包**&#x200B;对话框中，选择要包含在包中的页面。
   * （可选）输入&#x200B;**包名称** （如果留空，则默认为站点名称）。
   * 使用&#x200B;**全选**、**清除选择**、**全部展开**&#x200B;或&#x200B;**全部折叠**&#x200B;来管理列表。
1. 单击&#x200B;**创建包**。

   ![创建内容包 — 选择页面并创建](assets/content-package.png)

1. 创建包后，**上传内容包**&#x200B;对话框显示包已就绪。
   1. 您可以&#x200B;**下载包**&#x200B;以将其保存在本地，或继续上传。
   1. 在&#x200B;**上传至AEM**&#x200B;下，确认&#x200B;**AEM站点**&#x200B;和&#x200B;**AEM主机**（从您的项目设置预填充）。
      * （可选）保留&#x200B;**上载图像**&#x200B;的选中以包含图像。
   1. 单击&#x200B;**上传至AEM**。

   ![已准备好上传到AEM或下载的包](assets/upload-package-start.png)

1. 该对话框在页面和资源发送到AEM时显示上传进度。 上传完成后，将显示成功消息和上传日志。 单击&#x200B;**关闭**&#x200B;以关闭对话框。

   ![在AEM中上传进度和完成度](assets/upload-package-complete.png)

您导入的内容现在位于AEM中。 继续主入门指南中的[推送代码更改](getting-started.md#push-code-changes)。

## 其他资源 {#additional-resources}

* [体验现代化代理入门](getting-started.md) — 完整的工作流，包括控制台、提示、上传和预览
* [体验现代化控制台](console.md) — 控制台引用
* [通用编辑器教程](https://www.aem.live/developer/ue-tutorial) — 设置AEM创作和通用编辑器项目
* [`aem-block-collection-xwalk`](https://github.com/adobe-rnd/aem-block-collection-xwalk) - AEM创作和通用编辑器项目的模板存储库
