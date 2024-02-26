---
title: 通用编辑器事件
description: 了解通用编辑器发送的不同事件，您可以使用这些事件对远程应用程序中的内容或UI更改做出反应。
source-git-commit: e92a0be2213e3d5793fd077bd1968852336cc98b
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---


# 通用编辑器事件 {#events}

了解通用编辑器发送的不同事件，您可以使用这些事件对远程应用程序中的内容或UI更改做出反应。

## 简介 {#introduction}

应用程序对页面或组件更新可能有不同的要求。 因此，Universal Editor会将定义的事件发送到远程应用程序。 如果远程应用程序没有已发送事件的自定义事件侦听器， [回退事件侦听器](#fallback-listeners) 由 `universal-editor-cors` 包被执行。

所有事件均会在远程页面中受影响的DOM元素上调用。 事件冒泡上升到 `BODY` 元素，其中提供的默认事件侦听器 `universal-editor-cors` 包已注册。 UI包含内容和事件。

所有事件都遵循命名约定。

* `aue:<content-or-ui>-<event-name>`

例如， `aue:content-update` 和 `aue:ui-select`

事件包括请求和响应的有效负载，并在相应的调用成功后触发。 有关调用及其负载示例的更多详细信息，请参阅文档 [通用编辑器调用。](/help/implementing/universal-editor/calls.md)

## 内容更新事件 {#content-events}

### aue：content-add {#content-add}

此 `aue:content-add` 将新组件添加到容器时会触发事件。

有效负载是通用编辑器服务中的内容，其中包含组件定义中的回退内容。

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

### aue：content-details {#content-details}

此 `aue:content-details` 当组件加载到属性边栏中时，将触发事件。

有效负载是组件的内容，并可以选择是组件的架构。

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

### aue：content-move {#content-move}

此 `aue:content-move` 移动组件时会触发事件。

有效负载包括组件、源容器和目标容器。

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

### aue：content-patch {#content-patch}

此 `aue:content-patch` 当组件数据在属性边栏中更新时，会触发事件。

有效负载是已更新属性的JSON修补程序。

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

### aue：content-remove {#content-remove}

此 `aue:content-remove` 从容器中删除组件时会触发事件。

有效负载是已删除组件的项目ID。

```json
{
    details: {
        resource: string;               // the resource which got removed
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue：content-update {#content-update}

此 `aue:content-update` 在上下文中更新组件的属性时，将触发事件。

有效负载是更新的值。

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

对于所有内容更新事件，请求的有效负载以及响应有效负载会传递到事件中。 例如，对于更新调用：

请求有效负载：

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

响应有效负载

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

## UI事件 {#ui-events}

### aue：ui-publish {#ui-publish}

此 `aue:ui-publish` 事件在发布内容时触发(调用 `BODY` 级别)。

有效负载是项目ID及其发布状态的列表。

### aue：ui-select {#ui-select}

此 `aue:ui-select` 选择组件时会触发事件。

有效负载是所选组件的项目ID、项目属性和项目类型。

```json
{
    details: {
        resource: string;       // resource of the selected
        prop: string;           // prop of the selected
        type: string;           // type of the selected
        selected: boolean;      // was selected or unselected
    }
}
```

### aue：ui-preview {#ui-preview}

此 `aue:ui-preview` 当页面的编辑模式更改为时，将触发事件 **预览**.

此事件的有效负载为空。

```json
{
    details: {}
}
```

### aue：ui-edit {#ui-edit}

此 `aue:ui-edit` 当页面的编辑模式更改为时，将触发事件 **编辑**.

此事件的有效负载为空。

```json
{
    details: {}
}
```

### aue：ui-viewport-change {#ui-viewport-change}

此 `aue:ui-viewport-change` 事件在视区大小更改时触发。

有效负载是视区的尺寸。

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue：initialized {#initialized}

此 `aue:initialized` 触发事件以告知远程页面已成功将其加载到通用编辑器中。

此事件的有效负载为空。

```json
{
    details: {}
}
```

## 回退事件侦听器 {#fallback-listeners}

### 内容更新 {#content-update-fallbacks}

| 事件 | 行为 |
|---|---|
| `aue:content-add` | 页面重新加载 |
| `aue:content-details` | 不执行任何操作 |
| `aue:content-move` | 将组件的内容/结构移动到目标区域 |
| `aue:content-patch` | 页面重新加载 |
| `aue:content-remove` | 删除DOM元素 |
| `aue:content-update` | 更新 `innerHTML` 包含有效负荷 |

### UI事件 {#ui-event-fallbacks}

| 事件 | 行为 |
|---|---|
| `aue:ui-publish` | 不执行任何操作 |
| `aue:ui-select` | 滚动到选定的元素 |
| `aue:ui-preview` | 添加 `class="adobe-ue-preview"` HTML标记 |
| `aue:ui-edit` | 添加 `class=adobe-ue-edit"` HTML标记 |
| `aue:ui-viewport-change` | 不执行任何操作 |
| `aue:initialized` | 不执行任何操作 |

## 其他资源 {#additional-resources}

* [Universal Editor 调用](/help/implementing/universal-editor/calls.md)
