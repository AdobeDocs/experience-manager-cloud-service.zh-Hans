---
title: 本文介绍了基于核心组件的自适应表单中规则编辑器的各种用例。
description: 本文探讨了基于核心组件的自适应表单中规则编辑器的各种用例。 它还重点说明了如何使用自定义函数为表单创建定制规则。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 062ed441-6e1f-4279-9542-7c0fedc9b200
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 0%

---

# 规则编辑器增强功能和用例

<span class="preview">这些是通过我们的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features">预发布渠道</a>提供的预发布功能。 这些增强功能还适用于Edge Delivery Services Forms。

本文介绍了自适应Forms中规则编辑器的最新增强功能。 这些更新旨在帮助您更轻松地定义表单行为，而无需编写自定义代码，并创建更动态、响应更快且个性化的表单体验。

下表列出了自适应Forms中规则编辑器的最近增强功能，简要说明以及每项功能的主要优势：

| 增强功能 | 描述 | 优点 |
|---|----|---|
| [使用validate()方法进行验证](#validate-method-in-function-list) | 在函数列表中可用，用于验证单个字段、面板或整个表单。 |  — 在面板、字段或表单级别<br>进行粒度验证 — 通过目标错误消息传递<br>获得更好的用户体验 — 防止因数据不完整而进步<br> — 减少表单提交错误 |
| [下载记录文档](#download-document-of-record) | 在规则编辑器中提供的现成函数可用于下载记录文档(DoR)。 |  — 下载DoR <br>无需自定义开发 — 各表单的下载体验一致 |
| [动态变量](#support-for-dynamic-variables-in-rules) | 使用根据用户输入或其他条件而更改的变量创建规则。 |  — 启用灵活的规则条件<br> — 减少对重复逻辑<br>的需求 — 消除创建隐藏字段的要求 |
| [自定义基于事件的规则](#custom-event-based-rules-support) | 定义对标准触发器以外的自定义事件做出响应的规则。 |  — 支持高级用例<br> — 更好地控制执行规则的时间和方式<br> — 增强了交互性 |
| [上下文感知的可重复面板执行](#context-based-rule-execution-for-repeatable-panels) | 现在，规则会在每个重复面板的正确上下文中执行，而不是仅在最后一个实例中执行。 |  — 每个重复实例<br>的精确规则应用 — 减少动态部分<br>中的错误 — 改进用户使用重复内容的体验 |
| [支持查询字符串、UTM和浏览器参数](#url-and-browser-parameter-based-rules-in-adaptive-forms) | 创建根据URL参数或浏览器特定的值调整表单行为的规则。 |  — 基于源或环境<br>启用个性化 — 对营销或跟踪特定的流<br>很有用 — 无需额外的脚本编写或自定义 |

>[!NOTE]
>
> 增强功能还适用于Edge Delivery Services Forms[的](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)规则编辑器。

现在，让我们通过特定用例详细探索每种方法，以帮助您了解如何使用这些功能为用户提供个性化体验

## 函数列表中的验证方法

增强的验证功能，允许在函数列表中使用&#x200B;**validate()**&#x200B;方法来验证面板、字段或整个表单。 例如，在多步骤贷款申请表单中，您需要先验证不同的部分，然后才能允许用户继续执行下一步。

**方案：**&#x200B;金融机构提供多步骤贷款申请表，用户必须填写不同的部分，例如：

* 个人详细信息
* 雇用详细信息
* 贷款详细信息
* 审核并提交

在用户从一个步骤移动到下一个步骤之前，表单必须仅验证当前部分中的字段。 例如，除非正确填写“个人详细信息”中的所有必填字段，否则不应允许用户继续访问“雇用详细信息”。

在规则编辑器中使用validate()的&#x200B;**实现**

每个面板中的&#x200B;**Next**&#x200B;按钮使用&#x200B;**validate()**&#x200B;方法触发规则。 该规则检查当前面板中的所有字段是否有效。 如果验证通过，表单将导航到下一个面板。 如果没有，则显示错误消息，引导用户更正输入。

下面的屏幕截图显示了应用于&#x200B;**下一步**&#x200B;按钮的规则：

![验证“下一步”按钮](/help/forms/assets/validate-next.png)

在上述规则中，**下一步**&#x200B;按钮检查&#x200B;**个人详细信息**&#x200B;部分中的字段是否有效。 如果详细信息无效，焦点将移至&#x200B;**个人详细信息**&#x200B;面板中的&#x200B;**姓名**&#x200B;字段。

![输出](/help/forms/assets/valid-output.png)

>[!NOTE]
>
>您可以对表单、片段或单个字段使用&#x200B;**validate()**&#x200B;方法。 当片段包含在表单中时，表单和片段将作为选项显示在验证上下文中。 在这种情况下，片段是指其中的字段，而表单是指嵌入片段的父表单。

## 下载记录文档

使用规则编辑器中的&#x200B;**DownloadDor()**&#x200B;现成(OOTB)函数，允许用户下载记录文档（如果表单配置为生成记录文档）。

>[!NOTE]
>
>如果表单未针对记录文档进行配置，则在使用&#x200B;**downloadDoR()**&#x200B;函数的规则应用于按钮时显示错误消息。

**方案**：政府机构提供了用于颁发证书的数字申请表。 在提交表单后，申请人通常需要填写完毕的表单副本以作记录或与另一个部门共享。 为了改善用户体验，FDA希望让申请者可以选择在提交后立即下载记录文档(DoR)，或选择在最终提交前的任何阶段下载。

在规则编辑器中使用DownloadDor()的&#x200B;**实现**

使用规则编辑器将&#x200B;**Download**&#x200B;按钮添加到表单，并配置了一个规则以在单击该按钮时触发&#x200B;**DownloadDor()**&#x200B;函数。

下面的屏幕截图显示了应用于&#x200B;**下载**&#x200B;按钮的规则：

![下载按钮规则](/help/forms/assets/download-button-rule.png)

>[!NOTE]
>
> **输入**&#x200B;字段允许用户为可下载文档指定文件名。 这是一个可选参数。

如果表单配置为生成DoR，则此函数会立即生成和下载PDF，而无需任何自定义函数。

![记录文档](/help/forms/assets/download-dor-output.png)

## 在规则中支持动态变量

增强型规则编辑器支持创建和使用动态（临时）变量。 可使用内置&#x200B;**设置变量值**&#x200B;和&#x200B;**获取变量值**&#x200B;函数在表单的整个生命周期内设置和检索这些变量。
这些变量包括：

* 未随表单数据一起提交。
* 可以保存中间值或计算值。
* 可用于条件逻辑和操作中。

**方案**：在线购物表单允许用户选择产品、输入数量以及选择送货国家/地区。 产品价格是通过表单字段捕获的固定值，而装运费用会因所选国家/地区而动态变化。

为避免表单与隐藏字段混乱，企业决定将运费存储在一个临时变量中，并将其用于实时计算。

**在规则编辑器中使用Set Variable Value和Get Variable Value函数实现**

>[!VIDEO](https://video.tv.adobe.com/v/3471607/get-set-variable-final-video/?quality=12&learn=on)

已使用&#x200B;**Set Variable Value**&#x200B;函数在&#x200B;**Address**&#x200B;片段上配置规则，以分配名为&#x200B;**extracharge**&#x200B;的临时变量。 此变量的值会根据所选国家/地区进行动态更改。 例如：

* 如果用户选择“美国”，则&#x200B;**extracharge**&#x200B;设置为500。
* 对于任何其他国家/地区，**extracharge**&#x200B;设置为100。

![设置变量值](/help/forms/assets/setvalue.png)

稍后，在计算&#x200B;**总装运成本**&#x200B;时，使用&#x200B;**获取变量值**&#x200B;函数检索&#x200B;**excharge**&#x200B;的值。 此值将添加到&#x200B;**产品价格×产品数量**&#x200B;中，以计算点击按钮时应付的最终金额。

![获取变量值](/help/forms/assets/getvalue.png)

随着用户更改国家/地区或数量，**总装运成本**&#x200B;字段会动态更新以反映产品成本和装运费用。
![输出](/help/forms/assets/getsetvalue-output.png)

>[!NOTE]
>
> 您还可以在When条件中添加&#x200B;**Get Variable value**&#x200B;函数。
> &#x200B;> ![当条件](/help/forms/assets/when-get-variable.png){width=50%，height=50%，align=center}时，在中获取变量值函数

这种方法可以实现动态的实时计算，而无需向表单中添加额外的字段，保持结构干净和用户友好。

## 基于自定义事件的规则支持

增强规则编辑器支持使用&#x200B;**调度事件**&#x200B;和&#x200B;**触发事件**&#x200B;函数进行自定义事件处理。 这些函数允许表单的不同部分通过发送和侦听自定义事件来通信，实现更干净的模块化逻辑，而无需将操作紧密耦合到特定字段。

**方案**：使用可重用的登录片段构建登录表单，该登录片段包含&#x200B;**输入用户名**&#x200B;和&#x200B;**输入密码**&#x200B;字段。 当用户提供有效凭据时，表单验证输入并启动&#x200B;**获取OTP**&#x200B;进程。 用户输入有效的OTP后，会被重定向到相应的页面。

该表单不使用直接绑定到字段的逻辑，而是使用基于事件的方法搭配&#x200B;**调度事件**&#x200B;和&#x200B;**触发事件**&#x200B;来提高模块性和可维护性。

**使用调度事件和触发器事件实施**


>[!VIDEO](https://video.tv.adobe.com/v/3471610/dispatch-trigger-final/?quality=12&learn=on)

登录片段将添加到表单中，其中包含用户名和密码的预定义字段。 在&#x200B;**获取OTP**&#x200B;按钮上配置了用于显示&#x200B;**验证面板**&#x200B;的规则，该面板包括用于输入和验证OTP的输入字段。

![获取OTP规则](/help/forms/assets/get-otp-rule.png)

在&#x200B;**验证面板**&#x200B;中，在“验证”按钮上配置了规则。 API集成用于验证在&#x200B;**输入OTP**&#x200B;字段中输入的OTP。 如果验证成功，则使用包含API响应的事件有效负载触发名为&#x200B;**LoggedIn**&#x200B;的&#x200B;**调度事件**。

![在触发器事件规则中](/help/forms/assets/trigger-event-rule.png)

在表单级别，规则配置为侦听&#x200B;**LoggedIn**&#x200B;事件。 触发此事件时，规则会显示重定向消息并将用户转到仪表板页面。

![调度事件规则](/help/forms/assets/dispatch-event-rule.png)

当用户提交具有正确凭据和有效OTP的表单时，登录成功，用户将被重定向到其仪表板。

支持自定义事件，允许开发人员创建和触发可用作规则编辑器中的条件的自定义事件。

## 针对可重复面板的基于上下文的规则执行

自适应Forms支持对可重复面板执行上下文感知规则。 这允许规则专门应用于用户进行交互的面板实例，而不是影响所有实例或默认为最后一个实例。

**方案**：产品订购单允许用户在单独的面板中添加多个产品。 每个面板都包含一个&#x200B;**Number of Product**&#x200B;字段和一个&#x200B;**总成本**&#x200B;字段。 当用户更新产品的数量时，表单应重新计算总价，但仅针对该特定面板，不针对所有其他面板。

**在规则编辑器中使用上下文感知规则的实施**

在可重复产品面板内的&#x200B;**Number of Product**&#x200B;字段中配置了规则。

以下屏幕快照显示可重复产品面板中&#x200B;**Number of Product**&#x200B;字段的规则：

![产品规则数](/help/forms/assets/number-of-product-rule.png)

更改数量时，规则将获取所选产品的单价，并仅计算该面板的总成本。

![上下文感知规则输出](/help/forms/assets/context-aware-rule-output.png)

## 自适应Forms中基于URL和浏览器参数的规则

自适应Forms支持使用外部参数执行动态规则，这些外部参数通过表单URL传递或派生自用户的浏览器环境。 这可根据访客来自何处或他们使用的设备来实现个性化的上下文感知表单体验。

## 允许的参数类型

| 参数类型 | 支持的选项 | 描述 | 示例值 |
| --- | --- | --- | ---|
| 查询参数 | `ref` （仅限字符串值） | URL中`?`之后的通用键值对 | `?ref=partner123` |
| UTM参数 | UTM Source<br>UTM Medium<br>UTM Campaign<br>UTM搜索词<br>UTM内容 | 用于营销活动跟踪的特殊查询参数 | `?utm_source=google&utm_medium=email` |
| URL 参数 | 主机名<br>路径 | 提取表单URL的结构组件 | `hostname=www.example.com`、`path=/signup` |
| 浏览器参数 | 浏览器代理<br>浏览器语言<br>浏览器平台 | 从用户的浏览器或设备派生的值 | `Browser Agent=Mozilla`、`Language=en-US` |

**方案**：潜在客户生成表单需要根据流量源定制其欢迎消息。 当用户通过Google广告促销活动登陆表单时（在URL中使用utm_source=google），表单应显示自定义问候语。

使用UTM参数&#x200B;**实现**

在向Google用户显示自定义消息的文本字段中配置了一个规则，该规则使用&#x200B;**utm_source**&#x200B;参数。

下面的屏幕截图显示了短信上配置的规则：

![短信规则](/help/forms/assets/utm-param-rule.png)

如果&#x200B;**utm_source**&#x200B;参数值等于“google”，则自定义消息为“Hello Google users， welcome to the Campaign Ad！” 显示了。

![utm-param-output](/help/forms/assets/utm-param-output.png)

这允许营销人员根据将他们带到表单的营销活动将相关内容交付给用户，而无需手动输入字段或自定义脚本。

这些增强功能显着扩展了自适应Forms规则编辑器的功能，为开发人员提供了创建更动态、交互式和智能表单的强大工具。 每项增强功能都可满足特定的业务需求，同时维护使规则编辑器可供技术和非技术用户访问的易用性。

## 其他资源

{{see-also-rule-editor}}
