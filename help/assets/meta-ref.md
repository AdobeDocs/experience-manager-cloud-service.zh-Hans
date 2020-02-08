---
title: 元数据架构参考
description: '了解用于描述资产元数据的标准惯例，包括都柏林核心、IPTC和其他元数据架构。 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 元数据架构参考 {#metadata-schemata-reference}

以下参考内容介绍了关于特定元数据架构（按字母顺序排列）的信息并列出了各个属性及其定义。

## 都柏林核心 {#dublin-core}

都柏林核心元数据提供了一个用于描述资产的标准化惯例集，可使资产更易于查找。在AEM资产中，都柏林核心描述数字资产，包括视频、声音、图像和文档。

都柏林核心元数据元素集 (DCMES) 很简单，共包含 15 个元数据元素，如下表所示。每个都柏林核心元素都是可选元素，并且可以重复。您可以视需要为特定于媒体类型的元数据添加或删除都柏林核心元数据信息。

除了 DCMES 之外，都柏林核心计划还创建了其他一些元数据元素。有关详细信息，请查看[都柏林核心计划](https://dublincore.org/)。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td> 
   <td><strong>描述</strong></td> 
  </tr>
  <tr>
   <td>contributor</td> 
   <td>负责贡献内容的个人或公司。</td> 
  </tr>
  <tr>
   <td>coverage</td> 
   <td>资产覆盖的地理位置或时间段。<br /> </td> 
  </tr>
  <tr>
   <td>creator</td> 
   <td>负责创建内容的个人或公司。</td> 
  </tr>
  <tr>
   <td>date</td> 
   <td>与资产关联的日期或时间段。<br /> </td> 
  </tr>
  <tr>
   <td>描述</td> 
   <td>关于资产的详细信息。</td> 
  </tr>
  <tr>
   <td>format</td> 
   <td>资产的文件格式、物理介质或尺寸。AEM uses <code>dc:format</code> to denote the mime-type of the asset.<br /> </td> 
  </tr>
  <tr>
   <td>标识符</td> 
   <td>资产的唯一参考。</td> 
  </tr>
  <tr>
   <td>语言</td> 
   <td>资产的语言（例如，en 表示英语）。</td> 
  </tr>
  <tr>
   <td>publisher</td> 
   <td>负责使资产进入可用状态的个人或公司。</td> 
  </tr>
  <tr>
   <td>relation</td> 
   <td>相关的资产。</td> 
  </tr>
  <tr>
   <td>rights</td> 
   <td>关于谁有权使用此资产的信息。</td> 
  </tr>
  <tr>
   <td>source</td> 
   <td>作为资产派生来源的相关资产。</td> 
  </tr>
  <tr>
   <td>subject</td> 
   <td>资产的主题。<br /> </td> 
  </tr>
  <tr>
   <td>职位</td> 
   <td>资产的名称。</td> 
  </tr>
  <tr>
   <td>类型</td> 
   <td>资产的性质或类型。</td> 
  </tr>
 </tbody>
</table>

## IPTC {#iptc}

国际出版电讯委员会 (IPTC) 是全世界新闻机构的联盟，其宗旨之一是制定并维护技术标准。IPTC 定义了针对图像的一套照片元数据标准，几乎所有摄影人士都普遍接受这套标准。这些元数据标准从属于一个更广泛的标准，即 20 世纪 90 年代创建的 IPTC 信息交换模型 (IIM)。

尽管 IPTC 标题信息基本上已经被 XMP 所取代，但仍有 IPTC 核心架构和扩展架构可供 XMP 使用。在图像程序中，会同时同步 XMP 属性和 IPTC 属性。
