---
title: 配置用于呈现的组件的内容片段
description: 配置用于呈现的组件的内容片段
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 6%

---

# 配置用于呈现的组件的内容片段{#content-fragments-configuring-components-for-rendering}

有几个 [高级服务](#definition-of-advanced-services-that-need-configuration) 与内容片段的呈现相关。 要使用这些服务，此类组件的资源类型必须在内容片段框架中知晓自己。

这是通过配置 [OSGi服务 — 内容片段组件配置](#osgi-service-content-fragment-component-configuration).

以下情况需要提供此信息：

* 您需要实施您自己的基于内容片段的组件，
* 需要利用先进的服务。

建议使用核心组件。

>[!CAUTION]
>
>* **如果您不需要 [高级服务](#definition-of-advanced-services-that-need-configuration)** 下面所述，您可以忽略此配置。
>
>* **扩展或使用现成的组件时**，则不建议更改OSGi配置。
>
>* **您可以从头开始编写仅使用内容片段API的组件，而无需任何高级服务**. 但是，在这种情况下，您必须开发组件，以便它处理相应的处理。
>
>因此，建议使用核心组件。

## 需要配置的高级服务的定义 {#definition-of-advanced-services-that-need-configuration}

需要注册组件的服务包括：

* 在发布期间正确确定依赖项（即，如果片段和模型自上次发布后发生更改，则可以随页面自动发布它们）。
* 支持全文搜索中的内容片段。
* 管理/处理 *中间内容。*
* 管理/处理 *混合媒体资产。*
* 引用片段的调度程序刷新（如果包含片段的页面被重新发布）。
* 使用基于段落的渲染。

如果您需要其中一个或多个功能，则（通常）使用现成的高级服务会比较容易，而不是从头开始开发。

## OSGi服务 — 内容片段组件配置 {#osgi-service-content-fragment-component-configuration}

配置需要绑定到OSGi服务 **内容片段组件配置**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>请参阅 [OSGi配置](/help/implementing/deploying/overview.md#osgi-configuration) 以了解更多详细信息。

例如：

![OSGi配置内容片段组件配置](assets/cf-component-configuration-osgi.png)

OSGi配置为：

<table>
 <thead>
  <tr>
   <td>标签</td>
   <td>OSGi配置<br /> </td>
   <td>描述</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>资源类型</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>要注册的资源类型；例如 <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>引用属性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含对片段的引用的属性的名称；例如 <code>fragmentPath</code> 或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Element(s)属性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要呈现的元素名称的属性名称；例如<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>变量属性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈现的变体名称的属性名称；例如<code>variationName</code></td>
  </tr>
 </tbody>
</table>

对于某些功能，您的组件必须遵守预定义的约定。 下表详细列出了组件需要为每个段落(即 `jcr:paragraph` （适用于每个组件实例），以便服务能够正确检测和处理它们。

<table>
 <thead>
  <tr>
   <td>属性名称</td>
   <td>描述</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>一个字符串属性，用于定义在 <em>单元渲染模式</em>.</p> <p>值:</p>
    <ul>
     <li><code>all</code> :渲染所有段落</li>
     <li><code>range</code> :呈现提供的段落范围 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>字符串属性，用于定义要输出的段落范围(如果在 <em>单元渲染模式</em>.</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 或 <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> 范围指示器</li>
       <li><code>;</code> 列表分隔符</li>
       <li><code>*</code> 通配符</li>
     </ul>
     </li>
     <li>仅评估 <code>paragraphScope</code> 设置为 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>一个布尔属性，用于定义标题是否为 <code>h1</code>, <code>h2</code>, <code>h3</code>)计为段落(<code>true</code>)或否(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## 示例 {#example}

例如，请参阅以下内容(在现成的AEM实例上):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

其中包含：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
