---
title: 图像编辑器
description: 图像编辑器是AEM的核心部分，组件可利用它来方便内容作者处理图像。
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---


# 图像编辑器 {#image-editor}

图像编辑器是AEM的核心部分，组件可利用它来方便内容作者处理图像。

## 图像映射的相对单位 {#relative-units-for-image-map}

图像编辑器将图像映射区域保留为绝对和相对单位。 当在响应式图像组件中以数据属性的形式提供相对单位，用于在客户端动态地调整图像映射（相对于图像大小）的大小时。

### imageMap属性 {#imagemap-property}

图像编辑器将图像映射坐标作为属 `imageMap` 性保留到JCR。 它有以下格式。

属性按如下方式存储地图区域：

`[area1][area2][...]`

区域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

示例:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支持SVG图像 {#support-for-svg-images}

图像编辑器支持可缩放矢量图形(SVG)。

* 支持从DAM拖放SVG资产和从本地文件系统上传SVG文件。

## 按MIME类型启用插件 {#enabling-plugins-by-mime-type}

在某些情况下，创作操作必须限制用于某些MIME类型，因为在服务器端处理中缺乏支持。 例如，可能不允许编辑SVG图像。

通过在单个插件的配置节点上设置属性，可以通过MIME类 `supportedMimeTypes` 型选择性地启用图像编辑器中的插件。

### 示例 {#example}

例如，我们假设仅允许对GIF、JPEG、PNG、WEBP和TIFF图像进行裁剪。

然 `supportedMimeTypes` 后，必须在图像组件节点上插件的配置节点上将属性设置为允许 `cq:editConfig` 的MIME类型的字符串。

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
