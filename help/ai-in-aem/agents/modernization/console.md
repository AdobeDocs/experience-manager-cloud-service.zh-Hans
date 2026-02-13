---
title: 体验现代化控制台
description: Experience Modernization Console界面和功能的参考指南
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 43d8c124-fc87-4cec-a91d-ab12255ae321
source-git-commit: 76c0f41acb5c2e4e0f0a292f8205b0b9de5cda81
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---


# 体验现代化控制台 {#console-reference}

Experience Modernization Console界面和功能的参考指南

>[!NOTE]
>
>如果您有兴趣使用Experience Modernization Console，可以请求访问权限以确保顺利入门体验。

## 概述 {#overview}

Experience Modernization Console是Edge Delivery Services的托管、AI辅助的开发环境，在[`aemcoder.adobe.io`公开为Web界面。](https://aemcoder.adobe.io)连接到他们的GitHub项目后，您可以立即开始以自然语言提示更改，而无需进一步设置或本地环境配置。

>[!TIP]
>
>如果您有兴趣立即开始使用控制台，请查看文档[Experience现代化代理快速入门。](/help/ai-in-aem/agents/modernization/getting-started.md)

## 功能 {#capabilities}

控制台的核心功能：

* 与代理的交互式聊天面板及其技能
* 实时AEM预览，可即时提供更改的可视反馈
* 内容文件浏览器和Markdown查看器
* 与[文档创作](https://da.live)的内容同步
* 用于审阅所做更改的代码浏览器和比较查看器
* GitHub集成，能够根据更改创建拉取请求

开发人员可以完全控制哪些产品要发货。 通过控制台进行的所有更改都需要在部署之前进行审查和批准，以确保治理、品牌一致性和安全性。

## 导航 {#navigation}

在[`aemcoder.adobe.io`，](https://aemcoder.adobe.io)登录到控制台后，您将进入控制台的主屏幕。

![控制台的主屏幕](assets/console-home.png)

### 菜单栏 {#menu-bar}

顶部菜单栏提供：

* 左侧有一个&#x200B;**打开菜单**&#x200B;按钮，用于展开和折叠左侧面板的详细信息
* 右侧的&#x200B;**帐户**&#x200B;按钮，用于切换到深色模式并注销控制台

### 左侧栏 {#sidebar}

左侧边栏允许快速访问控制台的重要视图。

* **[主页视图](#home-view)**（住宅图标） — 您使用该控制台的起点
* **[内容视图](#content-view)**（文件图标） — 您已导入的内容
* **[代码视图](#code-view)** （`</>`图标） — 您正在处理的网站的代码
* **[设置视图](#settings-view)**（齿轮图标） — 控制台的设置

## 主视图 {#home-view}

**Home**&#x200B;视图是您使用该控制台的起点。

* 顶部是一个用于发出控制台请求的[提示面板](#prompt-panel)。
* 提示面板下面是用来启动项目的建议提示。

### 提示面板 {#prompt-panel}

提示面板提供用于与AI交互的控件。

* **计划/执行模式**（灯泡和魔棒图标）：分别在计划模式和执行模式之间切换
   * **规划模式**：人工智能分析请求并概述不做更改的方法，这有助于在提交之前了解策略。
   * **执行模式**： AI执行计划并进行实际文件更改。
* **附加文件**（回形针图标）：将文件上载并附加到提示以查找其他上下文（例如，参考设计、屏幕快照、规范）
* **设置**（齿轮图标）：选择以跳过人工智能中的确认问题
* **清除聊天**：这将重置对话并清除AI的上下文窗口。 在启动与上一个对话无关的新任务时，使用此选项。

## 内容视图 {#content-view}

**内容视图**&#x200B;提供了浏览和预览内容的工具。 默认情况下，视图将拆分为三个面板，从左至右：

* 用于与控制台和项目交互的提示面板
* 用于查看内容文件概览的文件浏览器（切换是否显示带有V形图标的此面板）
* 用于可视化在文件浏览器中选择的内容的“预览”面板

![内容视图](assets/content-imported.png)

“预览”面板提供三种模式：

* **预览**（带放大镜图标的文档）以查看渲染的HTML内容
* **HTML视图**（文档图标）分别用于查看基础文档创作内容结构
* **设计模式** （画笔图标）为提示选择页面的上下文元素

您始终可以单击&#x200B;**刷新预览**&#x200B;图标来更新预览面板。

使用&#x200B;**Upload content**&#x200B;按钮可打开一个模式窗口，以将文件上传到AEM Document Authoring。

* 如果您的项目具有&#x200B;**文件，则将预填充**&#x200B;组织&#x200B;**和**&#x200B;存储库`fstab.yaml`字段
* 文件选择提供了可编辑的目标路径
* 不支持上载到JCR（对于通用编辑器）

![上传内容](assets/upload-content.png)

## 代码视图 {#code-view}

**代码视图**&#x200B;提供了用于浏览代码和管理代码更改的工具。 视图由左至右分为三个面板：

* 用于与控制台和项目交互的提示面板
* 文件浏览器，用于获取代码文件的概述或差异更改
* 用于查看在文件浏览器中选择的代码文件或差异的“预览”面板

![代码视图](assets/code-view.png)

“预览”面板提供两种不同的模式：

* **Workspace文件**&#x200B;以浏览当前工作区中的代码文件
* **Git更改**&#x200B;以查看您项目工作所创建的文件更改的差异
   * 单击`+`图标存放更改的文件
   * 单击箭头图标可放弃更改的文件

**信息**&#x200B;图标列出了您当前连接的GitHub帐户和项目。

**GitHub操作**&#x200B;菜单（右上方）提供存储库操作。

* **连接/重新连接**：启动GitHub OAuth
* **切换存储库**：将工作区替换为其他存储库。 任何未提交的工作都将丢失。
* **切换分支**：在同一存储库中切换分支
* **同步**：从远程源提取最新更改
* **推送**：打开一个模式以将工作区更改推送到GitHub
* **注销**：断开与GitHub的连接

推送更改时，您必须先将更改暂存，才能将其包含在推送中。 推送时，您可以选择创建新PR或直接推送至当前分支

![推送更改](assets/push-changes.png)

## 设置视图 {#settings-view}

设置视图允许您管理控制台的基本设置。

![设置视图](assets/settings-view.png)

* **凭据**&#x200B;允许您为Figma指定个人访问令牌，以便控制台可以访问项目的设计块。
* **重置工作区**&#x200B;将控制台还原为开始状态，所有未推送或未上传的更改都将丢失。
