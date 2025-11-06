---
title: 通用编辑器2025.11.06发行说明
description: 这些是通用编辑器2025.11.06版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5c762da645ee26164d39af3936fc6b3fcbd43f0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 45%

---


# 通用编辑器2025.11.06发行说明 {#release-notes}

这些是通用编辑器 2025 年 11 月 6 号版本的发行说明。

>[!TIP]
>
>如果您想在&#x200B;**即将推出的**&#x200B;通用编辑器发布之前对其功能进行测试，请参阅[通用编辑器预览发行说明。](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 早期采用的功能 {#early-adopter}

如果您有兴趣测试这些即将推出的功能并分享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址发送邮件至您的 Adobe 客户成功经理。

### 新 RTE {#new-rte}

现在，右侧面板中提供新的 ProseMirror RTE，在链接对话框中引入了页面选取器功能。[此 RTE 提供灵活的配置选项。](/help/implementing/universal-editor/configure-rte.md)

## 其他改进 {#other-improvements}

* 现在可以正确删除`og:title`元数据字段。
* 修复了用户在浏览器中编辑位置栏以正确反映这些更改并且编辑器和/或应用程序现在导航到请求的URL时的导航问题。
* 字段模型分辨率已更正，并且编辑器使用来自组件的模型（如果存在）。
* componentId现在包含在/add操作中。
* 修复了删除某些以前无法删除的元数据属性的功能。
* 当AEM插件未设置时，现在会有条件地为xwalk完成原始获取。
* 已更正使用RTE处理内容片段MSM。
* 现在支持图片中的图像突出显示。

