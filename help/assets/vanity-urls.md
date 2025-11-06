---
title: 使用具有OpenAPI功能的Dynamic Media创建虚名URL
description: 使用Dynamic Media OpenAPI功能将您的长资源投放URL转换为简短且带品牌的虚名URL。 虚URL是复杂投放URL的简短、干净、易于记忆和可读的版本。 您可以在虚URL中包含品牌名称、产品名称和相关的关键词，以提高品牌知名度和用户参与度
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
exl-id: 596136e9-7c2a-43a1-8091-2d8b6226b695
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---

# 使用虚URL{#vanity-urls}

使用[!DNL Dynamic Media with OpenAPI capabilities]将您的长资源投放URL转换为短的、品牌化的虚URL。 标准资产交付URL包括系统生成的资产UUID，这些UUID使交付URL复杂、难以记忆和共享。 将这些资产UUID替换为简单标识符（虚ID）以生成虚URL。 虚URL是复杂投放URL的简短、干净和可读版本。

请参阅以下URL格式以了解其差异：

* [标准投放URL](#standard-urls)
* [虚名 URL](#vanity-url)

标准投放URL使用`aaid`后跟UUID，而虚URL使用`avid`后跟自定义标识符（虚标识符）。

使用简短而简单的虚标识符，使您的虚URL短、干净、可读、易于记忆和共享。 将您的品牌名称、产品名称和相关的关键字用作虚ID，以提高品牌知名度和用户参与度。

当用户单击虚URL时，[!DNL Dynamic Media with OpenAPI]会在摄取时自动映射到原始资源位置，并在交付时正确解析这些位置，以将资源服务器提供给用户。

了解[创建虚URL](#create-vanity-urls)。

## 标准交付URL{#standard-urls}

标准[!DNL Dynamic Media with OpenAPI]资产投放URL包含系统生成的唯一标识符，并遵循以下格式。

***格式：*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:aaid:aem:<asset-uuid>/as/<seoname>.<format>`

标准投放URL包含`aaid`之后的&#x200B;*（*&#x200B;实际资产标识符`urn:`）以及介于`urn:aaid:aem:`和`/as/<seoname>.<format>`之间的UUID。

***示例：*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:aaid:aem:43341ab1-4086-44d2-b7ce-ee546c35613b/as/check.jpeg`

在上述示例中，`43341ab1-4086-44d2-b7ce-ee546c35613b`是UUID。

## 虚名 URL{#vanity-url}

虚URL包含虚标识符来代替资产UUID，并遵循以下格式。

***格式：*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/as/<seoname>.<format>`

虚URL包含`avid`之后的&#x200B;*（*&#x200B;实际虚标识符`urn:`）以及介于`urn:avid:aem:`和`/<seoname>.<format>`之间的虚ID。

***示例：*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:avid:aem:VanityCheck/as/check.jpeg`

在上述示例中，`VanityCheck`是替代UUID的虚ID。

## 探索主要功能和优势{#capabilities-and-benefits-of-vanity-urls}

使用有意义的虚ID来自定义标准资产交付URL，这具备多项优势并可产生可衡量的影响。 虚URL的一些主要功能和优势包括。

### 主要功能{#key-capabilities}

* **URL自定义：**&#x200B;将投放URL中的长标识符（资产UUID）替换为较短、与品牌一致的替代项，以生成更干净的投放URL。
* **实时重定向：**&#x200B;虚URL在运行时重定向到原始资源UUID，而不会中断工作流。 当系统处理技术路由时，用户在地址栏中看到干净的URL。
* **轻松的链接管理：**&#x200B;随时自定义您的虚URL而不影响资产交付性能。

### 主要优势{#key-benefits}

* **增强用户体验：**&#x200B;简洁而短的虚URL可读、用户友好、易于记忆和共享。

* **提高用户参与度：**&#x200B;品牌化URL可建立用户信任和信任。 用户更有可能点击专业品牌链接，从而提高点进率。

* **SEO优化：**&#x200B;包含相关关键字的URL提高了搜索引擎排名和可发现性。

* **增强的品牌可见性：**&#x200B;品牌特定的URL增强了所有营销渠道（包括电子邮件、社交媒体和广告营销活动）中的品牌影响力。
此外，在所有通信中始终如一地使用品牌URL可加强品牌标识和知名度。

* **促销活动跟踪和分析：**&#x200B;为不同的促销活动和渠道使用唯一的虚URL，以详细了解流量源和转化效果。

## 先决条件{#prerequisites-for-creating-vanity-id}

要创建虚URL，请确保您已[批准用于公共投放的资产](/help/assets/manage-organize-assets-view.md#manage-asset-status)。

## 创建虚URL{#create-vanity-urls}

执行以下步骤以创建虚URL：

1. [设置资源元数据](#set-up-asset-metadata)
1. [创建和映射Cloud Manager环境变量](#map-cloud-manager-environment-variable)
1. [批准需要虚URL才能交付的资产](/help/assets/manage-organize-assets-view.md#manage-asset-status)
1. [生成虚URL](#generate-vanity-urls)

### 设置资源元数据{#set-up-asset-metadata}

执行以下操作以在资源的元数据表单中设置虚ID：

1. 导航到包含[!DNL Dynamic Media with OpenAPI]投放的资产的文件夹的详细信息页面。
1. [通过执行以下操作之一来编辑该元数据表单](/help/assets/metadata-assets-view.md#edit-metadata-forms)：

   * 添加新元数据字段，并将所需的虚ID指定为该字段的值。
   * 通过将现有元数据属性的值替换为所需的虚ID来更新现有字段。 了解创建虚ID的[最佳实践](#best-practices)。

   ![虚ID](/help/assets/assets/vanity-id-metadata.png)

   了解有关[元数据架构](/help/assets/metadata-schemas.md)的更多信息。

   >[!NOTE]
   >
   > * 为每个资源使用唯一的虚ID。 始终验证共享同一元数据表单的资产是否具有唯一的虚ID，以用于通过虚URL进行OpenAPI投放的DM。 如果两个资产共享同一个虚ID，则带OpenAPI的DM将交付最近收到该ID的资产，覆盖该ID先前对另一个资产的授权。
   >
   > * 单个资产可以具有多个虚ID。 [联系Adobe支持](https://helpx.adobe.com/in/contact.html)并提出生成所需虚ID的请求。

在资源元数据表单中设置虚ID后，[将此元数据字段映射到系统的投放机制](#map-cloud-manager-environment-variable)。

### 创建和映射Cloud Manager环境变量{#map-cloud-manager-environment-variable}

执行以下步骤可创建环境变量，并将其映射到包含虚ID的元数据字段：

1. [导航到Cloud Manager环境的配置页面](/help/implementing/cloud-manager/environment-variables.md)，并执行以下操作：
   1. 添加`ASSET_DELIVERY_VANITY_ID`变量。 这是钥匙。
   1. 使用值字段映射到包含虚ID的资源元数据属性。 映射遵循`dc:<your-metadata-property>`格式，其中元数据映射前缀（如dc：）因资源元数据配置属性而异。
      ![ASSET_DELIVERY_VANITY_ID变量](/help/assets/assets/environment-config.png)
1. 保存更改以重新启动环境中的pod。

### 审批要交付的资产{#approve-assets-for-delivery}

将Cloud Manager环境中的`ASSET_DELIVERY_VANITY_ID`变量映射到包含虚ID的资源元数据属性后，[批准需要虚URL才能交付的资源](/help/assets/manage-organize-assets-view.md#manage-asset-status)。

### 生成虚URL{#generate-vanity-urls}

在您的标准交付URL中进行以下替换以将其转换为虚URL：

* 将&#x200B;**UUID**&#x200B;替换为您的&#x200B;**虚ID**。
* 将`aaid`替换为`avid`。

请参阅上述[URL从标准到虚名URL的转换](#standard-urls)。
了解如何[复制具有OpenAPI投放URL的Dynamic Media](/help/assets/approve-assets.md#copy-delivery-url-for-approved-assets)以用于您的资产。

当用户单击虚URL时，[!DNL Dynamic Media with OpenAPI]会在提取时自动将虚ID映射到原始资产UUID，并在交付时正确解析它们，以便毫不延迟地将该资产提供给用户。 您可以在不影响资产交付性能的情况下实时自定义虚名URL。

[将AEM Cloud Service的高级自定义功能与您的虚URL结合使用以增强其影响](#scale-using-vanity-url)。

## 使用虚URL进行扩展{#scale-using-vanity-url}

AEM as a Cloud Service允许您[自定义网址中的DNS和CDN名称](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/introduction)。 将这些AEMCS功能与您的虚URL结合使用，将它们转换为清洁、描述性、品牌化、直观的唯一Web地址，并提供上述[好处](#key-benefits)。

请参阅以下虚URL及其可自定义的组件：

**虚URL格式：**

`https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/as/<seoname>.<format>`

<table style="border-collapse:collapse; table-layout:auto; width:auto;">
<tr valign="top">
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>https://delivery&#8209;&lt;tenant&gt;.adobeaemcloud.com</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#customize-dns">自定义此DNS</a></div>
</td>
<td style="padding:0 6px; white-space:nowrap; text-align:center;">/</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>adobe/assets/urn:avid:aem:</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#rewrite-cdn-rules">使用重写规则自定义URL</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>&lt;vanity-id&gt;</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#create-vanity-urls">创建虚ID</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:left; width:1%;">
<code>/as/&lt;seoname&gt;.&lt;format&gt;</code>
</td>
</tr>
</table>

**具有自定义DNS和CDN名称的虚名URL格式：**

`https://<custom-dns>` `/` `dam/assets/` `<vanity-id>` `/as/<seoname>.<format>`

**可自定义的URL组件**

* ***[DNS名称（主机名）：](#customize-DNS)*** `https://delivery-<tenant>.adobeaemcloud.com`是托管资产的服务器域。 [自定义DNS以更改主机名](#customize-DNS)。
* ***[CDN重写规则：](#rewrite-cdn-rules)*** `adobe/assets/urn:avid:aem:`是标识资源类型和交付方法的路径结构。 [重写CDN规则](#rewrite-cdn-rules)以修改域路径。

### 自定义DNS{#customize-dns}

[向Adobe支持部门提出请求](https://helpx.adobe.com/in/contact.html)，以便为您的传递层生成所需的自定义DNS。 按照以下[最佳实践](#best-practices)创建自定义DNS名称。

### 重写CDN规则{#rewrite-cdn-rules}

执行以下步骤可重写用于投放的CDN规则：

1. 导航到您的AEM存储库以创建YAML配置文件。
2. 执行[设置](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-error-pages#setup)部分中的步骤以配置CDN规则并通过Cloud Manager配置管道部署配置。
按照这些[最佳实践](#best-practices)创建域路径。
   [了解有关CDN重写规则的更多信息](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations)。

以下是重写规则的示例，这些规则用于在虚名URL中附加具有扩展名的文件名。 根据特定要求自定义这些重写规则。 [联系Adobe支持](https://helpx.adobe.com/in/contact.html)以获取更多帮助：

```- name: cdn-rewrite-rule
  when:
    allOf:
      - reqProperty: tier
        equals: delivery
```

#### 对于SVG、GIF和PDF {#svg-gif-pdf}

```
    type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:svg|gif|pdf|docx|xlsx))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/original/as/\1\2
```

#### 对于视频{#video}

用于视频，包括MP4、MOV、AVI和MKV

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:mp4|mov|avi|mkv))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/play\2
```

#### 图像{#image}

适用于所有图像类型，不包括SVG。

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.[^/]+)(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/as/\1\2
```

## 遵循创建干净的虚URL的最佳实践{#best-practices}

按照以下最佳实践创建[虚ID](#create-vanity-urls)、[自定义DNS](#customize-dns)和[CDN名称](#rewrite-cdn-rules)：

1. 请勿在虚ID中使用特殊字符，例如空格、斜杠、连字符等。 系统使用预定义映射替换虚名ID中的特殊字符。
1. 在[虚ID](#create-vanity-urls)、[自定义DNS](#customize-dns)和[CDN名称](#rewrite-cdn-rules)中使用您的品牌名称、产品名称和相关的关键字，以提高您的品牌知名度和用户参与度。
1. 使用简短的描述性词语或可传达意义的字符串。
1. 使用文本邀请用户进行点击。
