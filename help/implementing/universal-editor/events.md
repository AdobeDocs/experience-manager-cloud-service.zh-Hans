---
title: 通用编辑器事件
description: 了解通用编辑器发送的不同事件，您可以使用这些事件来响应远程应用程序中的内容或 UI 更改。
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Developer
source-git-commit: ac361c31b116466cc9a718640c1de4e4ef396fba
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 94%

---

# 通用编辑器事件 {#events}

了解通用编辑器发送的不同事件，您可以使用这些事件来响应远程应用程序中的内容或 UI 更改。

## 简介 {#introduction}

应用程序可能对页面或组件更新会有不同的要求。因此，通用编辑器将已定义的事件发送到远程应用程序。如果远程应用程序没有针对所发送事件的自定义事件侦听器，就会执行 `universal-editor-cors` 包提供的[后备事件侦听器](#fallback-listeners)。

所有事件都在远程页面的相关 DOM 元素上调用。事件冒泡到 `BODY` 元素，这个元素上注册了由 `universal-editor-cors` 包提供的默认事件侦听器。有针对内容的事件和针对 UI 的事件。

所有事件都遵循一个命名惯例。

* `aue:<content-or-ui>-<event-name>`

例如，`aue:content-update` 和 `aue:ui-select`。

事件包括请求和响应的负载，在相应调用成功后被触发。有关调用及其负载的示例的更多详细信息，请参阅文档[通用编辑器调用](/help/implementing/universal-editor/calls.md)。

## 内容更新事件 {#content-events}

### aue&amp;amp；冒号；content-add {#content-add}

当容器中添加了新组件时，会触发 `aue:content-add` 事件。

这个负载是来自通用编辑器服务的内容，后备内容来自组件定义。

```json
{
    details: {
        request: request payload;   // what is sent to the service
        response: {                 // what is returned by the service
            resource: string;       // newly created content resource
            updates: [{
                resource: string;   // resource to update
                type: string;       // type of instrumentation
                content?: string;   // content to replace
            }]
        }
    }
}
```

### aue&amp;amp；冒号；content-details {#content-details}

当属性面板中加载了组件时，会触发 `aue:content-details` 事件。

这个负载是组件的内容，也可以选择是组件的架构。

```json
{
    details: {
        content: object             // content object
        model: [object]             // model object
        request: request payload;   // what is sent to the service
        response: response payload; // what is returned by the service
    }
}
```

### aue&amp;amp；冒号；content-move {#content-move}

当组件被移动时，会触发 `aue:content-move` 事件。

这个负载是组件、源容器和目标容器。

```json
{
    details: {
        from: string;                   // container we move the component from
        component: string;              // component we move
        to: string;                     // container we move the component to
        before: string;                    // before which component shall we place the component
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue&amp;amp；冒号；content-patch {#content-patch}

当属性面板中的某个组件数据更新时，会触发 `aue:content-patch` 事件。

这个负载是被更新属性的 JSON 补丁。

```json
{
    details: {
        patch: {
            name: string;               // attribute which is updated
            value: string;              // new value which is stored to the attribute
        },
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue&amp;amp；冒号；content-remove {#content-remove}

当组件从容器中移除时，会触发 `aue:content-remove` 事件。

这个负载是被移除组件的项 ID。

```json
{
    details: {
        resource: string;               // the resource which got removed
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue&amp;amp；冒号；内容更新 {#content-update}

当组件的属性在上下文中更新时，会触发 `aue:content-update` 事件。

这个负载是更新后的值。

```json
{
    details: {
        value: string;                  // updated value
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service 
    }
}
```

### 传递负载 {#passing-payloads}

对于所有内容更新事件，请求的负载以及响应负载都会被传递到事件中。例如，对于更新调用：

请求负载：

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-p7452-e12433.adobeaemcloud.com"
    }
  ],
  "target": {
    "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "type": "text",
    "prop": "title"
  },
  "value": "Alhoa Spirit Northern Norway!"
}
```

响应负载

```json
{
    "updates": [
        {
            "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
            "prop": "title",
            "type": "text"
        }
    ]
}
```

## UI 事件 {#ui-events}

### aue&amp;amp；冒号；ui-preview {#ui-preview}

当页面的编辑模式被改为&#x200B;**预览**&#x200B;时，会触发 `aue:ui-preview` 事件。

此事件的负载为空。

```json
{
    details: {}
}
```

### aue&amp;amp；冒号；ui-edit {#ui-edit}

当页面的编辑模式被改为&#x200B;**编辑**&#x200B;时，会触发 `aue:ui-edit` 事件。

此事件的负载为空。

```json
{
    details: {}
}
```

### aue&amp;amp；冒号；ui-viewport-change {#ui-viewport-change}

当视口大小改变时，会触发 `aue:ui-viewport-change` 事件。

这个负载是视口的大小。

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue&amp;amp；冒号；已初始化 {#initialized}

触发 `aue:initialized` 事件以告知远程页面已在通用编辑器中成功加载。

此事件的负载为空。

```json
{
    details: {}
}
```

## 后备事件侦听器 {#fallback-listeners}

### 内容更新 {#content-update-fallbacks}

| 事件 | 行为 |
|---|---|
| `aue:content-add` | 页面重新加载 |
| `aue:content-details` | 无任何操作 |
| `aue:content-move` | 将组件的内容/结构移到目标区域 |
| `aue:content-patch` | 页面重新加载 |
| `aue:content-remove` | 移除 DOM 元素 |
| `aue:content-update` | 通过负载更新 `innerHTML` |

### UI 事件 {#ui-event-fallbacks}

| 事件 | 行为 |
|---|---|
| `aue:ui-select` | 滚动到选定元素 |
| `aue:ui-preview` | 将 `class="adobe-ue-preview"` 添加到 HTML 标记 |
| `aue:ui-edit` | 将 `class=adobe-ue-edit"` 添加到 HTML 标记 |
| `aue:ui-viewport-change` | 无任何操作 |
| `aue:initialized` | 无任何操作 |

## 其他资源 {#additional-resources}

* [通用编辑器调用](/help/implementing/universal-editor/calls.md)
