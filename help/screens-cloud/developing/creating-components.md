---
title: 创建组件
description: AEM组件用于保存、格式化和渲染网页上提供的内容。 可查看本页以了解有关创作渠道和渲染组件的信息。
source-git-commit: 34a072bd8e936a7cdf6c37ad7b3eea704d644fd9
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 2%

---


# 创建组件 {#creating-components}

AEM组件用于保存、格式化和渲染网页上提供的内容。

## 创作渠道 {#authoring-channels}

渠道是交付到一组显示屏的内容的中心对象。 因此，内容作者通常会在编辑器中打开渠道以添加或修改内容。 由于渠道是 ***cq:Page*** 它将遵循相同的传统UX模式在渠道中添加和更改组件。

但是，由于渠道中的组件通常呈现全屏，因此在尝试编辑单个组件或撰写新订单时，创作体验将会受损。 因此，渠道将依赖选择器来呈现组件的不同视图。 创作环境将利用编辑选择器来激活自定义渠道渲染。

例如, `http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

在编辑时，用户不必负责将选择器添加到URL。 客户端逻辑正在侦听层交换事件，并在信道具有专用资源类型时添加选择器 *screens/core/components/channel.*

## 渲染组件 {#rendering-components}

要启用正确的创作功能，组件需要提供以下两种渲染：

| **Component** | **演绎版** |
|---|---|
| *my-component/my-component.html* | 生产渲染 |
| *my-component/edit.html* | 在较小的视图中编辑渲染 |

内置组件利用以下客户端库类别：

| **组件** | **客户端库** |
|---|---|
| *cq.screens.components.edit* | 必须在创作过程中加载的CSS和JS |
| *cq.screens.components.production* | 必须在渠道运行时加载的CSS和JS |
| *cq.screens.components* | 共享的CSS和JS |

>[!NOTE]
>
>要开发自定义组件，请使用***[AEM Screens示例组件模板](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***。
