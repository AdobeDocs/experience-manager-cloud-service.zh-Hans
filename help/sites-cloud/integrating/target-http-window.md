---
title: AdobeAEM目标HTTP窗口
description: 'AdobeAEM目标HTTP窗口 '
translation-type: tm+mt
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 3%

---


# 简介 {#introduction}

本页介绍了AdobeAEM目标HTTP窗口中存在的可配置参数。

## 参数 {#parameters}

![目标HTTP](assets/httpwindow.png "WindowTarget HTTP窗口")

该窗口包含以下可配置参数：

| 参数 | 描述 |
|---|---|
| Adobe TargetAPI URL | Adobe TargetAPI的URL。 |
| 启用绝对URL | 确定是使用URL的主机部分还是使用完整URL。 如果要使用完整（未加删节的）URL，请启用此复选框。 默认情况下，此复选框处于禁用状态。 |
| 连接超时 | 建立连接之前的超时（以毫秒为单位）。 默认值为60000毫秒。 值0被解释为无限超时。 |
| 套接字超时 | 等待数据或两个连续数据包之间最长非活动时间的超时（以毫秒为单位）。 默认值为30000毫秒。 |
| Adobe TargetRecommendationsURL替换正则表达式令牌 | 控制需要替换的Adobe Target端点URL中的令牌，以指向目标重定义API URL。 |
| Adobe TargetRecommendationsURL替换为令牌 | 替换上述参数中描述的正则表达式，因此生成的URL将指向目标重新命令API。 |
