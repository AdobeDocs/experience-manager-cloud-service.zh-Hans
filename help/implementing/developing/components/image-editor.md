---
title: 图像编辑器
description: 图像编辑器是AEM的一个核心部分，组件可以使用它来促进内容作者对图像的操作。
exl-id: c8ae4f59-75b1-49b4-8dd4-957d2e33000b
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---

# 图像编辑器 {#image-editor}

图像编辑器是AEM的一个核心部分，组件可以使用它来促进内容作者对图像的操作。

## 图像映射的相对单位 {#relative-units-for-image-map}

图像编辑器将图像映射区域保留为绝对和相对单位。 当提供相对单位作为数据属性用于动态地调整响应式图像组件中客户端上的图像映射（相对于图像大小）的大小时，相对单位很有用。

### imageMap属性 {#imagemap-property}

图像映射坐标作为 `imageMap` 属性。 其格式如下。

物业按下列方式储存地图区域：

`[area1][area2][...]`

区域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

示例：

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支持SVG图像 {#support-for-svg-images}

图像编辑器支持可缩放矢量图形(SVG)。

* 从 DAM 拖放上传 SVG 资源以及从本地文件系统上传 SVG 文件均受支持。

## 按MIME类型启用插件 {#enabling-plugins-by-mime-type}

在某些情况下，由于缺少服务器端处理支持，必须限制某些MIME类型的创作操作。 例如，可能不允许编辑SVG图像。

MIME类型可以通过设置 `supportedMimeTypes` 属性。

### 示例 {#example}

例如，我们假设仅允许对GIF、JPEG、PNG、WEBP和TIFF图像进行裁切的功能。

此 `supportedMimeTypes` 然后，必须在上的插件的配置节点上将属性设置为允许的MIME类型的字符串。 `cq:editConfig` 图像组件的节点。

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
