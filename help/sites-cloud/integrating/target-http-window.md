---
title: AdobeAEM Target HTTP窗口
description: 'AdobeAEM Target HTTP窗口 '
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---


# 简介 {#introduction}

本页介绍AdobeAEM Target HTTP窗口中存在的可配置参数。

## 参数 {#parameters}

![目标HTTP窗口](assets/httpwindow.png "目标HTTP窗口")

窗口包含以下可配置参数：

| 参数 | 描述 |
|---|---|
| Adobe Target API URL | Adobe Target API的URL。 |
| 启用绝对URL | 确定是使用URL的主机部分还是使用完整URL。 如果要使用完整（无删节）URL，请启用此复选框。 默认情况下，复选框处于禁用状态。 |
| 连接超时 | 在建立连接之前的超时时间（以毫秒为单位）。 默认值为60000毫秒。 值0被解释为无限超时。 |
| 套接字超时 | 等待数据的超时时间（以毫秒为单位），或两个连续数据包之间的最长不活动时间段。 默认值为30000毫秒。 |
| Adobe Target Recommendations URL替换正则表达式令牌 | 控制Adobe Target端点URL中需要替换以指向Target Recommandations API URL的令牌。 |
| Adobe Target Recommendations URL替换为令牌 | 替换了上述参数中描述的正则表达式，因此生成的URL将指向Target Recommandations API。 |
