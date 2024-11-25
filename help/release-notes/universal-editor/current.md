---
title: 通用编辑器 2024.11.13 发行说明
description: 这些是通用编辑器 2024.11.13 版本的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 98795cab471470442cf5c424a67ce2846cfe85dc
workflow-type: ht
source-wordcount: '370'
ht-degree: 100%

---


# 通用编辑器 2024.11.13 发行说明 {#release-notes}

这些是通用编辑器 2024 年 11 月 13 号版本的发行说明。

>[!TIP]
>
>关于 Adob&#x200B;&#x200B;e Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **CORS 超时重试选项：**&#x200B;在[版本 2024.09.26 中，](/help/release-notes/universal-editor/2024/2024-09-26.md)当编辑器无法建立与加载页面的连接时，会引入一个错误面板，以防止出现无休止的加载状态。
   * 在此版本中，编辑器会自动不断重试，一旦建立连接，即可恢复编辑。
   * 这对于初始化时间可能超时超过一分钟的页面尤其有用。
* **面向开发人员的可扩展性增强：**&#x200B;通用编辑器现在支持向扩展广播事件，从而允许扩展开发人员订阅[事件。](/help/implementing/universal-editor/events.md)
   * 这使开发人员能够[在其自定义扩展中对编辑器事件做出反应。](/help/implementing/universal-editor/customizing.md#extending)
* **持久组件选择：**&#x200B;即使刷新浏览器后，编辑器中选定的组件仍将保留。
   * 这确保了用户在重新加载页面时可以继续工作而不会丢失其上下文。
* **本地化快速链接：**&#x200B;主屏幕上的&#x200B;**快速链接**&#x200B;部分现在提供文档的本地化链接，帮助用户根据自己的语言偏好轻松访问相关指南。
* **高级调试的请求 ID：**&#x200B;错误通知现在在详细信息部分包含&#x200B;**请求 ID**，该 ID 与`x-request-id header`相关。
   * 通过将这些错误与内部日志进行匹配，Adobe 工程团队可以更轻松地追踪和诊断问题。

## 其他改进 {#other-improvements}

* **修复了长内容树标签：**&#x200B;解决了&#x200B;**内容树**&#x200B;面板中的长标签被截断的问题
   * 这确保了拖放手柄始终可见，以便对内容进行重新排序。
* **修复了长属性标签：**&#x200B;解决了&#x200B;**属性**&#x200B;面板中的长字段标签与字段验证信息重叠的错误
* **属性面板中的水平滚动：**&#x200B;修复了&#x200B;**属性**&#x200B;面板中的宽元素导致水平滚动的问题
* **修复了通知期间工具栏不活动的问题：**&#x200B;显示 **toast** 通知时，顶部 [Adobe Experience Cloud](https://spectrum.adobe.com/page/toast/) 工具栏现在可完全正常运行。
* **提高稳定性：**&#x200B;添加了错误边界来处理意外值，防止单个渲染程序或验证器失败时整个用户界面崩溃，从而提高稳健性
