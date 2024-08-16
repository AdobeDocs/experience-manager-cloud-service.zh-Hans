---
title: 通用编辑器2024.08.13发行说明
description: 这些是通用编辑器2024.08.13版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: aad4d0353fb5e2eacb518b72e935def931d0798a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# 通用编辑器2024.08.13发行说明 {#release-notes}

这些是通用编辑器2024年8月13日版本的发行说明。

>[!TIP]
>
>有关Adobe Experience Manager as a Cloud Service的最新发行说明，请参阅[此页面。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **自定义数据类型**：根据您的独特数据需求定制编辑器，以便在属性面板中创建自定义字段。
   * 无论您是开发用于商业用例的自定义产品选取器，还是使用来自后端的值填充下拉列表，此功能均可为您提供对作者用于撰写内容的数据所需的控制。
* **跨容器拖放**：布局构成更加灵活，能够在[内容树面板中[通过拖放](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components)在不同容器之间移动组件。](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)
* **优化的GitHub集成**：引入了GitHub响应的缓存，显着加快了标记和`universal-editor-cors-library`的检索，从而提供了更快、更流畅的用户体验。
* **Managed Services RPM包**：Adobe现在提供RPM包，以简化Universal Editor服务的部署和管理，从而简化维护并降低托管服务的操作开销。
* **可配置的IMS令牌验证**：为了提高令牌管理的灵活性，IMS令牌验证现在为可选。
   * 此配置选项允许您根据需要禁用验证，从而简化云网关设置。
* **Splunk集成**： Splunk日志记录已集成到[Universal Editor服务以进行本地开发，](/help/implementing/universal-editor/local-dev.md)增强了监控和诊断。
   * 此集成可确保高效的日志跟踪、更顺畅的操作和更快的故障排除。

## 错误修复 {#bug-fixes}

* **增强的发布反馈**：如果发布由于权限不足而失败，则发布期间向用户提供的反馈将得到改进，以显示明确的警告，而不是简单地指示失败。
* **已改进URL处理**：修复了导致发布失败的URL编码/解码错误问题。
* **准确的数据处理**：解决了浮点数错误地存储为整数的问题，从而确保在整个内容中精确处理数据。
* **安全性和稳定性**：修复了Docker映像中的安全漏洞，并实施了关键组件（如组件选取器和痕迹导航）的测试覆盖率，从而提供了更安全、稳定且可靠的编辑器体验。
