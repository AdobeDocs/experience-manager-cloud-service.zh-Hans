---
title: 内容片段配置要渲染的组件
description: 内容片段配置要渲染的组件
translation-type: tm+mt
source-git-commit: a5d6a072dfd8df887309f56ad4a61b6b38b32fa7

---


# 内容片段配置要渲染的组件{#content-fragments-configuring-components-for-rendering}

有几个与 [内容片段的呈现](#definition-of-advanced-services-that-need-configuration) 相关的高级服务。 要使用这些服务，此类组件的资源类型必须使内容片段框架知道自己。

这是通过配置 [OSGi服务——内容片段组件配置来完成的](#osgi-service-content-fragment-component-configuration)。

以下情况下需要此信息：

* 您需要实现您自己的基于内容片段的组件，
* 需要利用先进的服务。

建议使用核心组件。

>[!CAUTION]
>
>* **如果您不需要下面介绍[的高级服务](#definition-of-advanced-services-that-need-configuration)**，则可以忽略此配置。
   >
   >
* **当您扩展或使用现成组件时**，不建议更改OSGi配置。
   >
   >
* **您可以从头开始编写一个仅使用内容片段API的组件，而无需高级服务**。 但是，在这种情况下，您必须开发组件，以便它处理相应的处理。
>
>
因此，建议使用核心组件。

## 需要配置的高级服务的定义 {#definition-of-advanced-services-that-need-configuration}

需要注册组件的服务包括：

* 在发布过程中正确确定依赖关系（即，如果片段和模型自上次发布后发生更改，则可以自动与页面一起发布）。
* 全文搜索中支持内容片段。
* 中间内容的 *管理／处理。*
* 管理／处理混 *合媒体资产。*
* 针对引用片段的调度程序刷新（如果包含片段的页面被重新发布）。
* 使用基于段落的渲染。

如果您需要这些功能中的一个或多个，那么（通常）使用现成的高级服务会更简单，而不是从头开始开发。

## OSGi服务——内容片段组件配置 {#osgi-service-content-fragment-component-configuration}

配置需要绑定到OSGi服务内容片段 **组件配置**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>有关更 [多详细信息](/help/implementing/deploying/overview.md#osgi-configuration) ，请参阅OSGi配置。

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
   <td>要注册的资源类型；例如， <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>引用属性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含对片段的引用的属性的名称；例如 <code>fragmentPath</code> , <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>元素属性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要渲染的元素名称的属性名称；例如，<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>变量属性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要渲染的变体的名称的属性的名称；例如，<code>variationName</code></td>
  </tr>
 </tbody>
</table>

对于某些功能，您的组件必须遵守预定义的惯例。 下表详细列出了组件需要为每个段落（即每个组件实例）定义的属性，以便服务能够正确检测和处理这些属性。 `jcr:paragraph`

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
   <td><p>一个字符串属性，它定义在单个元素渲染模式下如何输 <em>出段落</em>。</p> <p>值:</p>
    <ul>
     <li><code>all</code> :渲染所有段落</li>
     <li><code>range</code> :渲染提供的段落范围 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>一个字符串属性，它定义在单元素渲染模式下要输出的段 <em>落范围</em>。</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 者 <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> 范围指示符</li>
       <li><code>;</code> 列表分离器</li>
       <li><code>*</code> 通配符</li>
     </ul>
     </li>
     <li>仅在设置为 <code>paragraphScope</code> 时计算 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>一个布尔属性，它定义标题( <code>h1</code>例如， <code>h2</code>, <code>h3</code>)是否被计为段落(<code>true</code>)或(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## 示例 {#example}

例如，请参阅以下内容（在现成的AEM实例上）:

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

