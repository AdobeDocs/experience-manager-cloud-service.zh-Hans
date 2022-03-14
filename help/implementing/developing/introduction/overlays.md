---
title: 覆盖Adobe Experience Manager as a Cloud Service
description: AEM as a Cloud Service使用叠加原理来扩展和自定义控制台及其他功能
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# AEM as a Cloud Service 中的叠加 {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service使用叠加原理来允许您扩展和自定义控制台及其他功能（例如，页面创作）。

叠加图是一个可在许多上下文中使用的术语。 在此上下文中(扩展AEMas a Cloud Service)，叠加意味着采用预定义的功能，并将您自己的定义强加在该功能之上（以自定义标准功能）。

在标准实例中，预定义功能保留在 `/libs` 推荐在 `/apps` 分支(使用 [搜索路径](#search-paths) 以解析资源)。

* 触屏UI使用 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) — 相关叠加：

   * 方法

      * 重建适当的 `/libs` 结构 `/apps`.

         这不需要1:1的副本，因为 [Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md) 用于交叉引用所需的原始定义。 Sling资源合并器通过差异（差异）机制提供访问和合并资源的服务。

      * 在下进行任何更改 `/apps`.
   * 优点

      * 更强大地处理 `/libs`.
      * 只重新定义实际需要的内容。


>[!CAUTION]
>
>的 [Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md) 相关方法只能与 [Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). 这意味着创建具有骨架结构的叠加图仅适用于标准触屏UI。

叠加是进行许多更改的推荐方法，例如配置控制台或在侧面板中为资产浏览器创建选择类别（在创作页面时使用）。 它们要求为：

* 您 ***必须* 在 `/libs` 分支&#x200B;**您所做的任何更改都可能丢失，因为每当对实例应用升级时，此分支都会发生更改。

* 他们将您所做的更改集中在一个位置；更便于您根据需要跟踪、迁移、备份和/或调试更改。

## 搜索路径 {#search-paths}

AEM使用搜索路径查找资源，首先搜索（默认情况下） `/apps` 分支，然后 `/libs` 分支。 此机制表示您的叠加在 `/apps` （和在此处定义的自定义项）将具有优先级。

对于叠加图，交付的资源是检索到的资源和属性的聚合，具体取决于OSGi配置中定义的搜索路径。
