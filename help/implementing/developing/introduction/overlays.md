---
title: Adobe Experience Manager as a Cloud Service的叠加图
description: AEMas a Cloud Service使用叠加原理来允许您扩展和自定义控制台和其他功能
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# AEM as a Cloud Service 中的叠加 {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service使用叠加原理来允许您扩展和自定义控制台和其他功能（例如，页面创作）。

“叠加”是一个可在许多上下文中使用的术语。 在此上下文中(扩展AEMas a Cloud Service)，叠加意味着采用预定义功能并将您自己的定义强加于此功能（以自定义标准功能）。

在标准实例中，预定义功能保存在 `/libs` 推荐做法是在下定义您的叠加（自定义） `/apps` 分支(使用 [搜索路径](#search-paths) 以解决资源问题)。

* 触屏优化UI使用 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)相关叠加图：

   * 方法

      * 重构适当的 `/libs` 下结构 `/apps`.

         这不需要一对一的拷贝，因为 [Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md) 用于交叉引用所需的原始定义。 Sling资源合并器提供通过差异（差异）机制访问和合并资源的服务。

      * 进行以下任何更改 `/apps`.
   * 优点

      * 对下的更改更强健 `/libs`.
      * 仅重新定义实际需要的内容。


>[!CAUTION]
>
>此 [Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md) 并且相关方法只能用于 [Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). 这意味着创建具有框架结构的叠加仅适用于支持触摸的标准用户界面。

叠加是进行许多更改的推荐方法，例如配置控制台或向侧面板中的资产浏览器创建选择类别（在创作页面时使用）。 要求它们是：

* 您 ***不得* 在 `/libs` 分支&#x200B;**您所做的任何更改都可能会丢失，因为每当升级应用于您的实例时，此分支都很容易发生更改。

* 它们将您的更改集中在一个位置；使您更轻松地跟踪、迁移、备份和/或调试更改（如有必要）。

## 搜索路径 {#search-paths}

AEM使用搜索路径查找资源，首先搜索（默认情况下） `/apps` 分支，然后 `/libs` 分支。 此机制表示您的叠加 `/apps` （以及其中定义的自定义项）将具有优先级。

对于叠加图，交付的资源是检索到的资源和属性的汇总，具体取决于OSGi配置中定义的搜索路径。
