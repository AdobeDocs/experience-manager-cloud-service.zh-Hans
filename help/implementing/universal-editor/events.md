---
title: 通用编辑器事件
description: 了解通用编辑器发送的不同事件，您可以使用这些事件对远程应用程序中的内容或UI更改做出反应。
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Architect, Developer
source-git-commit: a7b48559e5bf60c86fecd73a8bcef6c9aaa03b80
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# 通用编辑器事件 {#events}

了解通用编辑器发送的不同事件，您可以使用这些事件对远程应用程序中的内容或UI更改做出反应。

## 简介 {#introduction}

应用程序对页面或组件更新可能有不同的要求。 因此，Universal Editor会将定义的事件发送到远程应用程序。 如果远程应用程序没有已发送事件的自定义事件侦听器，则会执行`universal-editor-cors`包提供的[回退事件侦听器](#fallback-listeners)。

所有事件均会在远程页面中受影响的DOM元素上调用。 事件向上冒泡到`BODY`元素，其中注册了`universal-editor-cors`包提供的默认事件侦听器。 UI包含内容和事件。

所有事件都遵循命名约定。

* `aue:<content-or-ui>-<event-name>`

例如，`aue:content-update`和`aue:ui-select`

事件包括请求和响应的有效负载，并在相应的调用成功后触发。 有关调用及其负载示例的更多详细信息，请参阅文档[通用编辑器调用。](/help/implementing/universal-editor/calls.md)

## 内容更新事件 {#content-events}

### aue：content-add {#content-add}

向容器添加新组件时触发`aue:content-add`事件。

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

在属性面板中加载组件时触发`aue:content-details`事件。

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

移动组件时会触发`aue:content-move`事件。

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

当在属性面板中更新组件的数据时，会触发`aue:content-patch`事件。

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

从容器中删除组件时触发`aue:content-remove`事件。

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

在上下文中更新组件的属性时，会触发`aue:content-update`事件。

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

发布内容时触发`aue:ui-publish`事件（在`BODY`级别调用）。

有效负载是项目ID及其发布状态的列表。

### aue：ui-select {#ui-select}

选择某个组件时会触发`aue:ui-select`事件。

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

当页面的编辑模式更改为&#x200B;**预览**&#x200B;时，将触发`aue:ui-preview`事件。

此事件的有效负载为空。

```json
{
    details: {}
}
```

### aue：ui-edit {#ui-edit}

当页面的编辑模式更改为&#x200B;**编辑**&#x200B;时，将触发`aue:ui-edit`事件。

此事件的有效负载为空。

```json
{
    details: {}
}
```

### aue：ui-viewport-change {#ui-viewport-change}

更改视区大小时会触发`aue:ui-viewport-change`事件。

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

触发`aue:initialized`事件是为了让远程页面知道它已成功加载到通用编辑器中。

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
| `aue:content-update` | 使用有效负载更新`innerHTML` |

### UI事件 {#ui-event-fallbacks}

| 事件 | 行为 |
|---|---|
| `aue:ui-publish` | 不执行任何操作 |
| `aue:ui-select` | 滚动到选定的元素 |
| `aue:ui-preview` | 将`class="adobe-ue-preview"`添加到HTML标记 |
| `aue:ui-edit` | 将`class=adobe-ue-edit"`添加到HTML标记 |
| `aue:ui-viewport-change` | 不执行任何操作 |
| `aue:initialized` | 不执行任何操作 |

## 其他资源 {#additional-resources}

* [Universal Editor 调用](/help/implementing/universal-editor/calls.md)

