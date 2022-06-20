---
title: Adobe AEM Target HTTP 窗口
description: 'Adobe AEM Target HTTP 窗口 '
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: ht
source-wordcount: '195'
ht-degree: 100%

---


# 简介 {#introduction}

此页面描述了 Adobe AEM Target HTTP 窗口中提供的可配置参数。

## 参数 {#parameters}

![Target HTTP 窗口](assets/httpwindow.png "Target HTTP 窗口")

此窗口包含以下可配置的参数：

| 参数 | 描述 |
|---|---|
| Adobe Target API URL | Adobe Target API 的 URL。 |
| 启用绝对 URL | 确定是使用 URL 的主机部分还是使用完整 URL。如果要使用完整的（未删节的）URL，请启用该复选框。默认情况下，该复选框处于禁用状态。 |
| 连接超时 | 在建立连接之前的超时时间（以毫秒为单位）。默认值为 60000 毫秒。值为 0 被解释为无限超时。 |
| 套接字超时 | 等待数据的超时时间，或两个连续数据包之间的最长不活动时间段（以毫秒为单位）。默认值为 30000 毫秒。 |
| Adobe Target Recommendations URL 替换正则表达式令牌 | 控制 Adobe Target 端点 URL 中需要替换以指向 Target Recommandations API URL 的令牌。 |
| Adobe Target Recommendations URL 替换令牌 | 替换上述参数中描述的正则表达式，使生成的 URL 指向 Target Recommandations API。 |
