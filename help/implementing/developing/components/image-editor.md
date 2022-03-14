---
title: 图像编辑器
description: 图像编辑器是AEM的核心部分，可由组件使用，以便于内容作者处理图像。
exl-id: c8ae4f59-75b1-49b4-8dd4-957d2e33000b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---

# 图像编辑器 {#image-editor}

图像编辑器是AEM的核心部分，可由组件使用，以便于内容作者处理图像。

## 图像映射的相对单位 {#relative-units-for-image-map}

图像编辑器将图像映射区域保留为绝对和相对单位。 当提供相对单位作为数据属性时，用于在响应式图像组件的客户端上动态地调整图像映射（相对于图像大小）的大小。

### imageMap属性 {#imagemap-property}

图像映射坐标将作为 `imageMap` 属性。 其格式如下。

资产会按如下方式存储地图区域：

`[area1][area2][...]`

区域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

示例:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支持SVG图像 {#support-for-svg-images}

图像编辑器支持可缩放矢量图形(SVG)。

* 从 DAM 拖放上传 SVG 资源以及从本地文件系统上传 SVG 文件均受支持。

## 按MIME类型启用插件 {#enabling-plugins-by-mime-type}

在某些情况下，由于服务器端处理中不支持，因此必须限制某些MIME类型的创作操作。 例如，可能不允许编辑SVG图像。

可以通过设置 `supportedMimeTypes` 属性。

### 示例 {#example}

例如，应当仅允许对GIF、JPEG、PNG、WEBP和TIFF图像进行裁剪。

的 `supportedMimeTypes` 属性后，必须在 `cq:editConfig` 图像组件的节点。

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
