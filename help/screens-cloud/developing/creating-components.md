---
title: 创建组件
description: AEM组件用于保留、格式化和呈现网页上可用的内容。 请按照此页面了解如何创作渠道和渲染组件。
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
feature: Developing Screens
role: Admin, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# 创建组件 {#creating-components}

AEM组件用于保留、格式化和呈现网页上可用的内容。

## 创作渠道 {#authoring-channels}

渠道是交付给一组显示器的内容的中心对象。 因此，内容作者通常会在编辑器中打开一个渠道来添加或修改内容。 由于渠道是 ***cq：Page*** 它将遵循相同的传统UX模式，在渠道上添加和更改组件。

但是，由于渠道中的组件通常以全屏方式呈现，因此在尝试编辑单个组件或撰写新订单时，创作体验会受到影响。 因此，渠道将依赖选择器呈现组件的不同视图。 创作环境使用编辑选择器来激活自定义渠道渲染。

例如，`http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

编辑时，用户无需将选择器添加到URL。 客户端逻辑正在侦听层切换事件，如果通道具有专用资源类型，则添加选择器 *screens/core/components/channel.*

## 渲染组件 {#rendering-components}

要启用正确创作，组件需要提供以下两种渲染：

| **Component** | **演绎版** |
|---|---|
| *my-component/my-component.html* | 生产渲染 |
| *my-component/edit.html* | 在较小的视图中编辑渲染 |

内置组件使用以下客户端库类别：

| **Component** | **客户端库** |
|---|---|
| *cq.screens.components.edit* | 创作期间必须加载的CSS和JS |
| *cq.screens.components.production* | 渠道运行时必须加载的CSS和JS |
| *cq.screens.components* | 共享的CSS和JS |

>[!NOTE]
>
>要开发自定义组件，请使用***[AEM Screens示例组件模板](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***。
