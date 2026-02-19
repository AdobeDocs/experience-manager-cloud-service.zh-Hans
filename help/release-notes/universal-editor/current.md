---
title: 通用编辑器2026.02.19发行说明
description: 这些是通用编辑器2026.02.19版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 39137052e9fa409f7f5494be53fa7693aaa60b17
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 23%

---


# 通用编辑器2026.02.19发行说明 {#release-notes}

这些是通用编辑器 2026 年 2 月 19 日版本的发行说明。

>[!TIP]
>
>如果您想在&#x200B;**即将推出的**&#x200B;通用编辑器发布之前对其功能进行测试，请参阅[通用编辑器预览发行说明。](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* 已对RTE进行改进。
   * [现在支持在上下文RTE](/help/implementing/universal-editor/configure-rte.md#common-action-options)中隐藏工具栏项。
   * [现在支持在带有段落](/help/implementing/universal-editor/configure-rte.md#table-actions)的表内环绕文本。
   * [不支持的HTML标记](/help/implementing/universal-editor/configure-rte.md#unsupported-html)现在可以由RTE保留。
   * 现在，可从单独的文件提供RTE逻辑。
   * 现在可以使用RTE创建[表](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)并进行良好编辑。
* 如果未设置标签，则现在使用组件定义中的组件标题。
* `setEditorMode`现在可通过扩展使用。

## 早期采用的功能 {#early-adopter}

如果您有兴趣测试下面列出的即将推出的功能并分享您的反馈，请从与您的Adobe关联的电子邮件地址向您的Adobe ID客户成功经理发送电子邮件。

* 已为内容片段实施浅层复制。

## 其他改进 {#other-improvements}

* RTE端点现在可用于就地编辑器。
* 编辑嵌套字段不再导致从这些结构覆盖对等条目。
* 必填RTE字段无法再保存为空。
* 在设置格式后添加链接时，不再错误地应用就地格式。
