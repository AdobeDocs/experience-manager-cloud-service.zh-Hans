---
title: '通用编辑器预览发行说明 '
description: 这些是通用编辑器预览版的发行说明。
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: 374c8045043f67f06d4ae68aef499bb594f1c08c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 29%

---

# 通用编辑器预览发行说明  {#preview}

这些是通用编辑器&#x200B;**预览版**&#x200B;的发行说明。这些功能当前在通用编辑器的&#x200B;**预览环境**&#x200B;中可用。这些功能计划于2026年2月19日正式发布。

这些&#x200B;**预览**&#x200B;发行说明是为了方便您了解即将对通用编辑器进行哪些更改，并且您可以通过[切换到预览版本来测试这些更改。](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>有关通用编辑器的&#x200B;**当前发行说明**，请参阅文档[通用编辑器发行说明。](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>实际发布的内容和发布日期可能会发生变化。

## 即将推出的新功能 {#what-is-new}

* 已对RTE进行改进。
   * 现在支持在上下文RTE中隐藏工具栏项。
   * 现在支持在具有段落的表内环绕文本。
   * 现在会保留不支持的RTE标记。
   * 现在，可从单独的文件提供RTE逻辑。
   * 现在可以使用RTE创建或编辑表。
* 如果未设置标签，则现在使用组件定义中的组件标题。
* `setEditorMode`现在可通过扩展使用。

## 即将推出的改进 {#other-improvements}

* 修复了页面之间的复制和粘贴功能。
* `universal-editor-extensibility`已移至`universal-editor`。
* 对扩展端点的请求数已减少。
* RemoteApp卸载次数已从三次减少到一次。
* RTE端点现在可用于就地编辑器。
* 编辑嵌套字段不再导致从这些结构覆盖对等条目。
* 必填RTE字段无法再保存为空。
* 在设置格式后添加链接时，不再错误地应用就地格式。
