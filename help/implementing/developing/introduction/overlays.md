---
title: Adobe Experience Manager为Cloud Service的叠加
description: AEM作为Cloud Service使用叠加原则允许您扩展和自定义控制台和其他功能
translation-type: tm+mt
source-git-commit: 8028682f19ba6ba7db6b60a2e5e5f5843f7ac11f
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# AEM中的叠加作为Cloud Service {#overlays-in-aem}

Adobe Experience Manager作为Cloud Service，使用叠加原则允许您扩展和自定义控制台和其他功能（例如，页面创作）。

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

叠加是可用于许多上下文的术语。 在此上下文(将AEM扩展为Cloud Service)中，叠加意味着采用预定义的功能并将您自己的定义强加到该之上（以自定义标准功能）。

在标准实例中，预定义的功 `/libs` 能保留在下面，建议在分支下定义叠加(自定义 `/apps` )(使用 [搜索路径解析资](#search-paths) 源)。

* 触屏优化UI使用与 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)相关的叠加：

   * 方法

      * 在下重建相 `/libs` 应的结 `/apps`构。

         这不需要1:1副本，因为Sling Resource Mergare [用于交叉引用](/help/implementing/developing/introduction/sling-resource-merger.md) 所需的原始定义。 Sling Resource Merager通过差异（差异）机制提供访问和合并资源的服务。

      * 在下进行任何更改 `/apps`。
   * 优势

      * 对下面的更改更可靠 `/libs`。
      * 只重新定义实际需要的内容。


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>Sling [Resource Merage](/help/implementing/developing/introduction/sling-resource-merger.md) (Sling Resource Merabire)及相关方法只能与Granite一 [起使用](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。 这意味着创建具有骨架结构的叠加仅适用于标准的触屏优化UI。

对于许多更改，建议使用叠加方法，例如配置控制台或在侧面板中创建资产浏览器的选择类别（在创作页面时使用）。 它们的要求是：

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* 您不 ***得在分支&#x200B;*中进行更改。您`/libs`**所做的任何更改都可能丢失，因为只要对实例应用升级，该分支就会承担更改的责任。

* 他们将您所做的更改集中在一个位置； 使您能根据需要更轻松地跟踪、迁移、备份和／或调试更改。

## 搜索路径 {#search-paths}

AEM使用搜索路径来查找资源，首先搜索（默认情况下）分支， `/apps` 然后搜索分 `/libs` 支。 此机制意味着您的叠加(以 `/apps` 及在其中定义的自定义)将具有优先级。

对于叠加，交付的资源是检索到的资源和属性的聚合，具体取决于OSGi配置中定义的搜索路径。

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->