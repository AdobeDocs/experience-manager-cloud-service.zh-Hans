---
title: 配置用于呈现的组件的内容片段
description: 配置用于呈现的组件的内容片段
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 6%

---

# 配置用于呈现的组件的内容片段{#content-fragments-configuring-components-for-rendering}

有數種 [進階服務](#definition-of-advanced-services-that-need-configuration) 和內容片段的演算相關。 若要使用這些服務，內容片段架構必須瞭解這些元件的資源型別。

這是透過設定 [OSGi服務 — 內容片段元件設定](#osgi-service-content-fragment-component-configuration).

下列情況需要此資訊：

* 您需要實作自己的內容片段型元件，
* 而且需要使用進階服務。

建議使用核心元件。

>[!CAUTION]
>
>* **如果您不需要 [進階服務](#definition-of-advanced-services-that-need-configuration)** 如下所述，您可以忽略此設定。
>
>* **當您延伸或使用現成元件時**，不建議變更OSGi設定。
>
>* **您可以從頭開始撰寫只使用內容片段API （沒有進階服務）的元件**. 但是，在這種情況下，您必須開發元件，以便處理適當的處理。
>
>因此，建議使用核心元件。

## 需要設定的進階服務定義 {#definition-of-advanced-services-that-need-configuration}

需要註冊元件的服務包括：

* 在發佈期間正確判斷相依性（亦即，如果片段和模型自上次發佈以來已變更，請確保片段和模型可隨頁面自動發佈）。
* 支援全文檢索搜尋中的內容片段。
* 管理/處理 *中間內容。*
* 管理/處理 *混合媒體資產。*
* 參考片段的Dispatcher排清（如果重新發佈包含片段的頁面）。
* 使用段落式轉譯。

如果您需要這些功能中的一或多個，那麼使用現成可用的進階服務通常會比較容易，而不是從頭開始開發。

## OSGi服務 — 內容片段元件設定 {#osgi-service-content-fragment-component-configuration}

設定需要繫結到OSGi服務 **內容片段元件設定**：

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>另請參閱 [OSGi設定](/help/implementing/deploying/overview.md#osgi-configuration) 以取得更多詳細資料。

例如：

![OSGi設定內容片段元件設定](assets/cf-component-configuration-osgi.png)

OSGi設定為：

<table>
 <thead>
  <tr>
   <td>标签</td>
   <td>OSGi 配置<br /> </td>
   <td>描述</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>资源类型</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>要註冊的資源型別；例如， <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>參考屬性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含片段參照的屬性名稱；例如， <code>fragmentPath</code> 或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>元素屬性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要呈現之元素名稱的屬性名稱；例如，<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>变量属性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈現之變數名稱的屬性名稱；例如，<code>variationName</code></td>
  </tr>
 </tbody>
</table>

對於某些功能，您的元件必須遵循預先定義的慣例。 下表詳細說明每個段落(亦即 `jcr:paragraph` （每個元件例項），讓服務可以正確偵測及處理它們。

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
   <td><p>字串屬性，定義段落在中的輸出方式 <em>單一元素轉譯模式</em>.</p> <p>值:</p>
    <ul>
     <li><code>all</code> ：呈現所有段落</li>
     <li><code>range</code> ：呈現以下專案提供的段落範圍： <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>字串屬性，定義要在下列情況下輸出的段落範圍： <em>單一元素轉譯模式</em>.</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 或 <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> 範圍指示器</li>
       <li><code>;</code> 清單分隔符號</li>
       <li><code>*</code> 萬用字元</li>
     </ul>
     </li>
     <li>只有在 <code>paragraphScope</code> 設為 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>布林值屬性，定義標題(例如， <code>h1</code>， <code>h2</code>， <code>h3</code>)計算為段落(<code>true</code>)或不是(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## 示例 {#example}

如需範例，請參閱以下內容(在現成可用的AEM例項上)：

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

這包含：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
