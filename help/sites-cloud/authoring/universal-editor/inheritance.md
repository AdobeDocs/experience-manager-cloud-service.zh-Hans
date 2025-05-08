---
title: 通用编辑器中的内容继承
description: 了解通用编辑器如何支持多站点管理和启动的内容继承，以支持内容重用和本地化。
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 2a1b87c2-29b9-4689-9a15-e17942439160
source-git-commit: 9941c652a1509934662cdaae6d187d1a28a1cc31
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 3%

---

# 通用编辑器中的内容继承 {#inheritance}

了解通用编辑器如何支持多站点管理和启动的内容继承，以支持内容重用和本地化。

>[!NOTE]
>
>此功能仅适用于存储在AEM存储库中的内容。

## 用例 {#use-case}

对于AEM的许多用户，创建页面只是开始。 为了有效地扩展内容，通常在创建页面后需要完成以下步骤：

1. **使用语言副本和翻译工作流翻译页面**。
1. **使用多站点管理对页面**&#x200B;进行本地化，以将翻译后的页面推出到不同的市场。
1. **使用启动项创建新版本**&#x200B;以准备页面的未来小版本并将这些更改上线。

这些步骤可以加快内容速度并确保内容一致性。 通用编辑器支持内容继承，这是语言副本、多站点管理和启动项所依赖的机制。

## 继承 {#what-is-inheritance}

继承是一种机制，通过该机制，可以链接内容，以便更改一个内容会自动更改另一个内容。

MSM和启动项是功能强大的工具，可帮助您使用继承重用内容。 页面可以从中央源(Blueprint)复制，以使作者能够对这些副本的上下文进行特定更改，而其余内容仍会从Blueprint继承。 这在本地化站点时非常有用。

要修改副本的某些内容，作者会中断受影响组件的继承，以确保在副本与Blueprint同步时，不会覆盖其本地更改。

## 内容继承和通用编辑器 {#universal-editor}

当页面是MSM或Launch的一部分并且内容使用通用编辑器进行编辑时，编辑器会自动禁用作者在该页面上所做所有更改的继承，确保在从Blueprint同步更新时保留修改的内容。

在进行本地编辑之前，作者不需要单击按钮或执行任何其他步骤来禁用继承。 进行更改后，将立即隐式取消继承。 此工作流与[页面编辑器](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components)形成对比。

可以通过以下方式还原整个页面的继承：

* [Live Copy概述控制台](/help/sites-cloud/administering/msm/live-copy-overview.md)
* [启动项控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
* 使用[页面属性窗口](/help/sites-cloud/authoring/sites-console/page-properties.md)的&#x200B;**Live Copy**&#x200B;选项卡上的&#x200B;**重置**&#x200B;按钮。

通用编辑器不会影响继承的底层机制。 有关继承如何工作的更多详细信息，请参阅以下文档。

* [多站点管理(MSM)](/help/sites-cloud/administering/msm/overview.md)
* [启动项](/help/sites-cloud/authoring/launches/overview.md)

### AEM多站点管理(MSM)扩展 {#msm-extension}

如果已安装，**AEM多站点管理(MSM)扩展**&#x200B;将显示选定组件的当前继承状态，并允许您在组件级别中断或恢复继承。

有关如何使用此扩展的更多信息，请参阅[创作文档。](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)

有关如何启用此扩展的信息，[请参阅Extension Manager文档。](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)

## 限制 {#limitations}

* 要还原单个组件的继承，必须启用&#x200B;**AEM多站点管理(MSM)扩展**。
* 若要获得可视反馈，以查看哪些组件的继承已禁用，哪些组件仍保留其继承，则必须启用&#x200B;**AEM多站点管理(MSM)扩展**。
* 这些功能当前仅限于页面中的组件，尚不适用于[内容片段](/help/sites-cloud/administering/content-fragments/overview.md)，尽管这些片段也具有MSM和Launch功能。
