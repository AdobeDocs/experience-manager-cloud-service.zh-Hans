---
title: 通用编辑器2024.11.13发行说明
description: 这些是通用编辑器2024.11.13版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 98795cab471470442cf5c424a67ce2846cfe85dc
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 5%

---


# 通用编辑器2024.11.13发行说明 {#release-notes}

这些是通用编辑器2024年11月13日版本的发行说明。

>[!TIP]
>
>关于 Adob&#x200B;&#x200B;e Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **CORS上的重试选项：**&#x200B;对于[版本2024.09.26，](/help/release-notes/universal-editor/2024/2024-09-26.md)，当编辑器无法与加载的页面建立连接时引入了错误面板，从而阻止了无休止的加载状态。
   * 在此版本中，编辑器会自动不断重试，在建立连接后，可以继续编辑。
   * 这对于初始化时间可能超过一分钟超时的页面特别有用。
* **面向开发人员的扩展性增强功能：**&#x200B;通用编辑器现在支持将事件广播到扩展，从而允许扩展开发人员订阅[事件。](/help/implementing/universal-editor/events.md)
   * 这使开发人员能够[对其自定义扩展中的编辑器事件做出反应。](/help/implementing/universal-editor/customizing.md#extending)
* **持久组件选择：**&#x200B;编辑器中选定的组件现在将持续存在，即使在刷新浏览器之后也是如此。
   * 这可确保用户在重新加载页面时可以继续工作，而不会丢失上下文。
* **本地化的快速链接：**&#x200B;主页屏幕上的&#x200B;**快速链接**&#x200B;部分现在提供指向文档的本地化链接，帮助用户根据其语言首选项轻松访问相关指南。
* 高级调试的&#x200B;**请求ID：**&#x200B;错误通知现在在详细信息部分中包含与`x-request-id header`相关的&#x200B;**请求ID**。
   * 这使Adobe工程团队更容易通过将这些错误与内部日志匹配来跟踪和诊断问题。

## 其他改进 {#other-improvements}

* **修复了长内容树标签：**&#x200B;解决了&#x200B;**内容树**&#x200B;面板中的长标签被截断的问题
   * 这可确保对于内容重新排序始终显示拖放手柄。
* **修复了长属性标签：**&#x200B;解决&#x200B;**属性**&#x200B;面板中的长字段标签与字段验证信息重叠的错误
* **属性面板中的水平滚动：**&#x200B;修复了&#x200B;**属性**&#x200B;面板中的宽元素导致水平滚动的问题
* **修复了在通知期间不活动的工具栏：**&#x200B;显示[快显通知](https://spectrum.adobe.com/page/toast/)时，顶部&#x200B;**Adobe Experience Cloud**&#x200B;工具栏现在可以完全正常工作。
* **改进的稳定性：**&#x200B;添加了用于处理意外值的错误边界，以防止单个渲染器或验证器失败时整个UI崩溃，从而提高稳健性
