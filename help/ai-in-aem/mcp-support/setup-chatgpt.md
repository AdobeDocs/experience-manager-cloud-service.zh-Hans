---
title: 使用AEM MCP设置OpenAI ChatGPT
description: 了解如何配置OpenAI ChatGPT以连接到AEM MCP服务器
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 1f116225-168b-483c-9df6-c752a573b57b
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 使用AEM MCP设置OpenAI ChatGPT {#setup-chatgpt}

按照以下步骤将OpenAI ChatGPT连接到AEM的MCP服务器。

* 在配置了MCP连接或工具的区域中添加一个或多个AEM MCP服务器URL。
* 在重定向时触发连接并使用Adobe ID登录。
* 在聊天中，在提示中引用配置的AEM工具，例如：

  ```
  "Using the configured AEM MCP tools, list all sites in the author environment."
  ```

![ChatGPT设置对话框。](assets/chatgpt-1.png)

![ChatGPT中的“应用和连接器”高级设置面板。](assets/chatgpt-2.png)

![在“应用程序和连接器”部分启用开发人员模式。](assets/chatgpt-3.png)

![用于在ChatGPT中创建新应用的对话框。](assets/chatgpt-4.png)

![ChatGPT中的新应用配置表单。](assets/chatgpt-5.png)

![应用程序和连接器中列出了AEM内容MCP服务。](assets/chatgpt-6.png)

![提示ChatGPT使用AEM内容MCP服务。](assets/chatgpt-7.png)
