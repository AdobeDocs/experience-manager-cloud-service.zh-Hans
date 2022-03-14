---
title: 体验片段
description: 扩展Adobe Experience Manager as a Cloud Service体验片段。
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
source-git-commit: 975bbe809da1b34af8b8cab3b10ae2594133cf6d
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 2%

---

# 体验片段{#experience-fragments}

## 基本信息 {#the-basics}

[体验片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)是由一个或多个组件构成的组件组，包括可在页面内引用的内容和布局。

体验片段主控和/或变体使用：

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

因为没有 `/libs/cq/experience-fragments/components/xfpage/xfpage.html` 它会还原为

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## 纯 HTML 演绎版 {#the-plain-html-rendition}

使用 `.plain.` 选择器中，您可以访问纯HTML呈现版本。

可以从浏览器获取该功能，但其主要用途是允许其他应用程序（例如，第三方Web应用程序、自定义移动设备实施）仅使用URL直接访问体验片段的内容。

纯HTML呈现将协议、主机和上下文路径添加到以下路径：

* 类型： `src`, `href`或 `action`

* 或结束于： `-src`或 `-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>链接始终引用发布实例。 这些链接将由第三方使用，因此链接将始终从发布实例中调用，而不是从作者调用。

![纯HTML呈现](assets/xf-14.png)

纯格式副本选择器使用变压器，而不是其他脚本；the [Sling重写程序](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 用作变压器。 此配置位于

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## 体验片段的模板 {#templates-for-experience-fragments}

>[!CAUTION]
>
>***仅*** 体验片段支持可编辑的模板。

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

在为体验片段开发新模板时，您可以按照可编辑模板的标准实践操作。

<!-- When developing a new template for Experience Fragments you can follow follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

创建由 **创建体验片段** 向导中，您必须遵循以下规则集之一：

1. 两者:

   1. 模板的资源类型（初始节点）必须继承自：
      `cq/experience-fragments/components/xfpage`

   1. 并且模板的名称必须以下面的开头：
      `experience-fragments`
这允许用户在/content/experience-fragments中创建体验片段，作为 
`cq:allowedTemplates` 该文件夹的属性包含名称以开头的所有模板 `experience-fragment`. 客户可以更新此属性以包含他们自己的命名方案或模板位置。

1. [允许的模板](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) 可以在体验片段控制台中进行配置。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 体验片段的组件 {#components-for-experience-fragments}

开发与体验片段一起使用的组件/在中，遵循标准实践。

唯一的额外配置是确保模板上允许使用组件，这是通过内容策略实现的。

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## 体验片段链接重写程序提供程序 — HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以创建体验片段。 体验片段：

* 包含一组组件和一个布局，
* 可以独立于AEM页面存在。

此类组的一个用例用于将内容嵌入第三方接触点，如Adobe Target。

### 默认链接重写 {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

使用导出到Target功能，您可以：

* 创建体验片段，
* 添加组件，
* 然后，将其导出为Adobe Target选件(以HTML格式或JSON格式)。

此功能可以在AEM的创作实例上启用。 它需要有效的Adobe Target配置和链接外部器的配置。

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

链接外部器用于确定创建Target选件的HTML版本时所需的正确URL，该版本随后会发送到Adobe Target。 这是必需的，因为Adobe Target要求可以公开访问TargetHTML选件内的所有链接；这意味着必须先发布链接引用的任何资源以及体验片段本身，然后才能使用这些资源。

默认情况下，当您构建TargetHTML选件时，会向AEM中的自定义Sling选择器发送请求。 此选择器名为 `.nocloudconfigs.html`. 正如其名称所暗示的，它会创建体验片段的纯HTML渲染，但不包括云配置（这将是多余的信息）。

生成HTML页面后，Sling重写器管道会对输出进行修改：

1. 的 `html`, `head`和 `body` 元素替换为 `div` 元素。 的 `meta`, `noscript` 和 `title` 元素会被删除（它们是原始元素的子元素） `head` 元素，且在被替换为 `div` 元素)。

   这样做是为了确保将HTML目标选件包含在Target活动中。

2. AEM会修改HTML中存在的任何内部链接，以便它们指向已发布的资源。

   要确定要修改的链接， AEM对于HTML元素的属性遵循以下模式：

   1. `src` 属性
   2. `href` 属性
   3. `*-src` 属性（如data-src、custom-src等）
   4. `*-href` 属性(如 `data-href`, `custom-href`, `img-href`)

   >[!NOTE]
   >
   >在大多数情况下，HTML中的内部链接是相对链接，但在某些情况下，自定义组件会在HTML中提供完整的URL。 默认情况下，AEM会忽略这些完整的URL，且不会进行任何修改。

   这些属性中的链接通过AEM Link Externalizer运行 `publishLink()` 以便重新创建URL，使其像在已发布的实例上一样公开可用。

使用现成的实施时，上述流程应该足以从体验片段中生成Target选件，然后将其导出到Adobe Target。 但是，有些用例在此过程中没有说明；这包括：

* Sling映射仅在发布实例上可用
* 调度程序重定向

对于这些用例，AEM提供了链接重写程序提供程序界面。

### 链接重写程序提供程序界面 {#link-rewriter-provider-interface}

对于更复杂的情况，未涵盖 [默认](#default-link-rewriting), AEM提供链接重写器提供程序界面。 这是 `ConsumerType` 界面（作为服务）。 它会绕过AEM对从体验片段呈现的HTML选件的内部链接所执行的修改。 此界面允许您自定义重写内部HTML链接的过程，以符合您的业务需求。

将此接口作为服务实施的用例示例包括：

* Sling映射在发布实例上启用，但在创作实例上未启用
* 调度程序或类似技术用于在内部重定向URL
* 有 `sling:alias mechanisms` 资源就地

>[!NOTE]
>
>此界面仅处理生成的Target选件中的内部HTML链接。

链接重写器提供程序界面( `ExperienceFragmentLinkRewriterProvider`)如下所示：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用链接重写器提供程序界面 {#how-to-use-the-link-rewriter-provider-interface}

要使用接口，您首先需要创建一个包，其中包含一个实施链接重写程序提供程序接口的新服务组件。

此服务将用于插入体验片段导出到Target的重写，以便能够访问各种链接。

例如， `ComponentService`:

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

为了使服务正常工作，现在需要在服务中实施以下三种方法：

* `[shouldRewrite](#shouldrewrite)`
* `[rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* `[getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

您需要向系统指示在对特定体验片段变量中的“导出到Target”调用时，系统是否需要重写链接。 为此，请实施以下方法：

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例如：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

此方法将作为参数接收导出到Target系统当前正在重写的体验片段变量。

在以上示例中，我们希望重写：

* 存在的链接 `src`

* `href` 仅属性

* 对于特定体验片段：
   `/content/experience-fragment/master`

通过导出到Target系统的任何其他体验片段都将被忽略，并且不会受此服务中实施的更改的影响。

#### rewriteLink {#rewritelink}

对于受重写过程影响的体验片段变体，它将继续让服务处理链接重写。 每当在内部HTML中遇到链接时，都会调用以下方法：

`rewriteLink(String link, String tag, String attribute)`

作为输入，方法接收参数：

* `link`不为目标组件考虑  
`String` 当前正在处理的链接的表示形式。 这通常是指向创作实例上资源的相对URL。

* `tag`
当前正在处理的HTML元素的名称。

* `attribute`
确切的属性名称。

例如，如果导出到目标系统当前正在处理此元素，则可以定义 `CSSInclude` 为：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

对 `rewriteLink()` 方法可使用以下参数完成：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

创建服务时，您可以根据给定的输入做出决策，然后相应地重写链接。

例如，我们要删除 `/etc.clientlibs` 作为URL的一部分，并添加相应的外部域。 为了简单起见，我们将考虑我们有权访问您服务的资源解析程序，如 `rewriteLinkExample2`:

>[!NOTE]
>
>有关如何通过服务用户获取资源解析程序的更多信息，请参阅AEM中的服务用户。

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
>如果上述方法返回 `null`，则导出到Target系统将保留原样的链接，该链接是指向资源的相对链接。

#### 优先级 — getPriority {#priorities-getpriority}

需要多项服务以满足不同类型的体验片段的需求，甚至需要通用服务来处理所有体验片段的外部化和映射，这种情况并不罕见。 在这些情况下，可能会发生与使用哪项服务有关的冲突，因此AEM提供了定义 **优先事项** 不同服务。 使用以下方法指定优先级：

* `getPriority()`

此方法允许使用以下几项服务： `shouldRewrite()` 方法会为同一体验片段返回true。 返回其 `getPriority()`方法是用于处理体验片段变量的服务。

例如，您可以 `GenericLinkRewriterProvider` 可处理所有体验片段的基本映射，以及 `shouldRewrite()` 方法返回 `true` ，以用于所有体验片段变量。 对于多个特定的体验片段，您可能需要特殊处理，因此在这种情况下，您可以提供 `SpecificLinkRewriterProvider` 其中 `shouldRewrite()` 方法仅对某些体验片段变量返回true。 确保 `SpecificLinkRewriterProvider` 被选择用于处理这些体验片段变量，则必须在 `getPriority()` 方法大于 `GenericLinkRewriterProvider.`
