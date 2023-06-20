---
title: 体验片段概述
description: 扩展Adobe Experience Manager as a Cloud Service体验片段。
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 1%

---

# 体验片段{#experience-fragments}

## 基础知识 {#the-basics}

An [体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) 由一个或多个组件组成，包括可在页面中引用的内容和布局。

体验片段主控和/或变体使用：

* `sling:resourceType` ： `/libs/cq/experience-fragments/components/xfpage`

因为没有 `/libs/cq/experience-fragments/components/xfpage/xfpage.html` 它还原为

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## 纯 HTML 演绎版 {#the-plain-html-rendition}

使用 `.plain.` 选择器时，您可以访问纯HTML演绎版。

这可以从浏览器中获得，但其主要目的是允许其他应用程序（例如，第三方Web应用程序、自定义移动实施）仅使用URL直接访问体验片段的内容。

纯HTML演绎版将协议、主机和上下文路径添加到路径中，这些路径为：

* 类型： `src`， `href`，或 `action`

* 或结尾为： `-src`，或 `-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>链接始终引用发布实例。 这些链接旨在由第三方使用，因此将始终从发布实例而不是作者中调用链接。

![普通HTML演绎版](assets/xf-14.png)

纯格式副本选择器使用转换器，而不是其他脚本； [Sling重写器](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 用作转换器。 此配置于

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### 配置HTML演绎版生成 {#configuring-html-rendition-generation}

HTML演绎版是使用Sling重写器管道生成的。 管道定义于 `/libs/experience-fragments/config/rewriter/experiencefragments`. HTML转换器支持以下选项：

* `allowedCssClasses`
   * 匹配应保留在最终演绎版中的CSS类的RegEx表达式。
   * 如果客户想要删除某些特定的CSS类，这将很有用
* `allowedTags`
   * 最终演绎版中允许的HTML标签列表。
   * 默认情况下，允许使用以下标记（无需配置）：html、head、title、body、img、p、span、ul、li、a、b、i、em、strong、h1、h2、h3、h4、h5、h6、br、noscript、div、link和script

建议使用叠加配置重写器。 参见 [AEMas a Cloud Service中的叠加](/help/implementing/developing/introduction/overlays.md)

## 体验片段的模板 {#templates-for-experience-fragments}

>[!CAUTION]
>
>***仅*** 体验片段支持可编辑的模板。

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

在开发体验片段的新模板时，您可以遵循可编辑模板的标准实践。

<!-- When developing a new template for Experience Fragments you can follow follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

创建由检测到的体验片段模板 **创建体验片段** 向导中，必须遵循以下规则集之一：

1. 两者：

   1. 模板的资源类型（初始节点）必须继承自：
      `cq/experience-fragments/components/xfpage`

   1. 模板名称必须以下列内容开头：
      `experience-fragments`
这允许用户在/content/experience-fragments中创建体验片段作为 `cq:allowedTemplates` 此文件夹的属性包括名称以开头的所有模板 `experience-fragment`. 客户可以更新此属性以包含他们自己的命名方案或模板位置。

1. [允许的模板](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) 可以在体验片段控制台中配置。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 体验片段的组件 {#components-for-experience-fragments}

开发要与/在体验片段中使用的组件时，应遵循标准实践。

唯一额外的配置是确保模板上允许组件，这是通过内容策略实现的。

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## 体验片段链接重写器提供程序 — HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以创建体验片段。 体验片段：

* 由一组组件和一个布局组成，
* 可以独立于AEM页面存在。

此类组的用例之一是将内容嵌入第三方接触点，例如Adobe Target。

### 默认链接重写 {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

使用“导出到目标”功能，您可以：

* 创建体验片段，
* 向其中添加组件，
* 然后以HTML格式或JSON格式将其导出为Adobe Target选件。

可以在AEM的创作实例上启用此功能。 它需要有效的Adobe Target配置以及Link Externalizer配置。

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

链接外部化器用于确定在创建Target选件的HTML版本(随后将发送到Adobe Target)时所需的正确URL。 这是必需的，因为Adobe Target要求可以公开访问TargetHTML选件中的所有链接；这意味着链接引用的任何资源以及体验片段本身必须在使用之前发布。

默认情况下，当您构建TargetHTML选件时，会向AEM中的自定义Sling选择器发送请求。 此选择器名为 `.nocloudconfigs.html`. 顾名思义，它创建了体验片段的纯HTML渲染，但不包括云配置（这会是多余的信息）。

生成HTML页后，Sling重写器管道对输出进行修改：

1. 此 `html`， `head`、和 `body` 元素将被替换为 `div` 元素。 此 `meta`， `noscript` 和 `title` 元素会被删除（它们是原始元素的子元素） `head` 元素取代，则由元素取代时不予以考虑 `div` 元素)。

   这样做是为了确保可将HTMLTarget选件包含在Target活动中。

2. AEM修改HTML中存在的任何内部链接，以便这些链接指向已发布的资源。

   要确定要修改的链接，AEM对HTML元素的属性遵循以下模式：

   1. `src` 属性
   2. `href` 属性
   3. `*-src` 属性（如data-src、custom-src等）
   4. `*-href` 属性(如 `data-href`， `custom-href`， `img-href`、等)

   >[!NOTE]
   >
   >在大多数情况下，HTML中的内部链接是相对链接，但在某些情况下，自定义组件可能会在HTML中提供完整的URL。 默认情况下，AEM会忽略这些完全成熟的URL并且不会进行任何修改。

   这些属性中的链接通过AEM链接外部化器运行 `publishLink()` 以重新创建URL，就像在已发布的实例上一样，并且该URL已公开可用。

使用现成实施时，上述流程应足以从体验片段生成Target选件，然后将其导出到Adobe Target。 但是，有一些用例未在此流程中说明；这些用例包括：

* Sling映射仅在发布实例上可用
* Dispatcher重定向

对于这些用例，AEM提供了链接重写器提供程序接口。

### 链接重写器提供程序接口 {#link-rewriter-provider-interface}

对于更复杂的案例，不属于 [默认](#default-link-rewriting)，AEM提供链接重写器提供程序接口。 这是 `ConsumerType` 接口，您可以在捆绑包中实施该接口作为服务。 它绕过AEM对HTML选件的内部链接执行的修改（从体验片段渲染）。 此界面允许您自定义重写内部HTML链接的流程，以符合您的业务需求。

实施此接口作为服务的用例示例包括：

* Sling映射在发布实例上启用，但在创作实例上未启用
* 调度程序或类似技术用于在内部重定向URL
* 有 `sling:alias mechanisms` 资源就位

>[!NOTE]
>
>此界面仅处理来自所生成Target选件的内部HTML链接。

链接重写器提供程序接口( `ExperienceFragmentLinkRewriterProvider`)如下所示：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用链接重写器提供程序界面 {#how-to-use-the-link-rewriter-provider-interface}

要使用接口，您首先需要创建一个包，其中包含用于实现链接重写器提供程序接口的新服务组件。

此服务用于插入Experience Fragment Export to Target重写，以便能够访问各种链接。

例如， `ComponentService`：

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

要使服务正常工作，现在需要在服务中实施三种方法：

* `[shouldRewrite](#shouldrewrite)`
* `[rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* `[getPriority](#priorities-getpriority)`

#### 应重写 {#shouldrewrite}

您需要向系统指示在对特定体验片段变量调用“导出到Target”时是否需要重写链接。 要执行此操作，请实施以下方法：

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例如：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

此方法接收导出到Target系统当前正在重写的体验片段变体作为参数。

在上面的示例中，我们要重写：

* 链接存在于 `src`

* `href` 仅限属性

* 对于特定体验片段：
  `/content/experience-fragment/master`

任何通过“导出到Target”系统的其他体验片段将被忽略，并且不受此服务中实施的更改的影响。

#### rewritelink {#rewritelink}

对于受重写过程影响的体验片段变体，它会继续让服务处理链接重写。 每当在内部HTML中遇到链接时，都会调用以下方法：

`rewriteLink(String link, String tag, String attribute)`

作为输入，方法接收参数：

* `link`
此 `String` 表示当前正在处理的链接。 这通常是指向创作实例上资源的相对URL。

* `tag`
当前正在处理的HTML元素的名称。

* `attribute`
确切的属性名称。

例如，如果“导出到目标”系统当前正在处理此元素，则可以定义 `CSSInclude` 作为：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

对的调用 `rewriteLink()` 方法可使用以下参数完成：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

在创建服务时，您可以根据给定的输入做出决策，然后相应地重写链接。

例如，我们想要删除 `/etc.clientlibs` URL的一部分并添加相应的外部域。 为了简单起见，我们将考虑我们有权访问用于您服务的资源解析程序，例如 `rewriteLinkExample2`：

>[!NOTE]
>
>有关如何通过服务用户获取资源解析器的更多信息，请参阅AEM中的服务用户。

<!--
>For more information on how to get a resource resolver through a service user see [Service Users in AEM](/help/sites-administering/security-service-users.md).
-->

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>如果上述方法返回 `null`，则Export to Target系统将保持链接不变，即指向资源的相对链接。

#### 优先级 — getPriority {#priorities-getpriority}

需要多个服务来满足不同类型的体验片段的情况并不少见，甚至需要拥有通用服务来处理所有体验片段的外部化和映射也很常见。 在这些情况下，可能会发生与使用哪个服务有关的冲突，因此AEM提供了定义 **优先级** 用于不同的服务。 使用下列方法指定优先级：

* `getPriority()`

此方法允许使用多种服务，其中 `shouldRewrite()` 对于同一体验片段，方法会返回true。 从中返回最高编号的服务 `getPriority()`方法是处理体验片段变量的服务。

例如，您可以使用 `GenericLinkRewriterProvider` 用于处理所有体验片段的基本映射以及当 `shouldRewrite()` 方法返回 `true` 适用于所有体验片段变量。 对于多个特定的体验片段，您可能需要特殊处理，因此在这种情况下，您可以提供 `SpecificLinkRewriterProvider` 对于 `shouldRewrite()` 仅对于某些体验片段变量，方法会返回true。 为了确保 `SpecificLinkRewriterProvider` 被选择用于处理这些体验片段变量，它必须返回其 `getPriority()` 方法数字大于 `GenericLinkRewriterProvider.`
