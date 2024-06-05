---
title: Adobe Experience Manager as a Cloud Service的叠加
description: AEMas a Cloud Service使用叠加原理来允许您扩展和自定义控制台和其他功能
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# AEM as a Cloud Service 中的叠加 {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service使用叠加原理来允许您扩展和自定义控制台和其他功能（例如，页面创作）。

“叠加”是一个可在许多上下文中使用的术语。 在此上下文中，扩展AEMas a Cloud Service，叠加意味着采用预定义功能并将您自己的定义施加到它上以自定义标准功能。

在标准实例中，预定义功能保存在 `/libs` 推荐做法是在下定义您的叠加（自定义） `/apps` 分支(使用 [搜索路径](#search-paths) 以解决资源问题)。

* 触屏式用户界面使用 [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)相关叠加：

   * 方法

      * 重建适当的 `/libs` 结构 `/apps`.

        此重构不需要1:1复制，因为 [Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md) 用于交叉引用所需的原始定义。 Sling资源合并器提供访问资源并将其与差异（差异）机制合并的服务。

      * 下 `/apps`，进行更改。

   * 优点

      * 对下的更改更加强健 `/libs`.
      * 仅重新定义所需的内容。

>[!CAUTION]
>
>此 [Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md) 并且相关方法只能用于 [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). 此规则意味着创建具有框架结构的叠加仅适用于已启用触摸的标准用户界面。

叠加是适用于许多更改的推荐方法。 例如，配置控制台，或在侧面板中为资源浏览器创建选择类别（在创作页面时使用）。 它们必须是：

* **在 `/libs` 分支， *不要* 进行更改**
您所做的任何更改都可能会丢失，因为每当将升级应用于实例时，此分支都可能会发生更改。

* 它们将您的更改集中在一个位置，使您能够更轻松地跟踪、迁移、备份或调试所需的更改。

## 搜索路径 {#search-paths}

AEM使用搜索路径来查找资源，首先搜索 — 默认情况下 —  `/apps` 分支，然后 `/libs` 分支。 此机制表示您的叠加 `/apps` （以及其中定义的自定义项）具有优先级。

对于叠加，交付的资源是检索到的资源和属性的汇总，具体取决于OSGi配置中定义的搜索路径。
