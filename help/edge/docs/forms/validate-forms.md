---
title: 从电子表格到Forms — 掌握自适应Forms块字段验证
description: 使用电子表格和自适应Forms块字段更快地制作功能强大的表单！ 本指南可帮助您为 EDS Forms 区块字段构建自定义验证。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 16e1d42a-42d0-4335-ba81-feedea7ed7d7
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 80%

---

# 向表单字段添加验证

自适应Forms Block具有内置验证功能。 这些验证会根据所选字段类型和您提供的附加属性自动应用于现代浏览器中。

## 了解字段类型和验证

自适应Forms块支持各种 [HTML5输入类型](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)，包括文本、电子邮件、数字、日期等。 它还容纳 [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)、select 和 fieldset，以及 HTML-5 固有的全面输入验证功能。

使用 HTML 字段类型定义用户可输入的数据类型。不同的字段类型有不同的内置验证规则：

电子邮件：此字段类型自动根据常见电子邮件地址格式验证用户输入。输入无效电子邮件的用户将看到一条错误消息。
数字：此字段类型仅允许输入数字。输入非数字字符的用户将收到错误。
日期：此字段类型根据标准日期格式验证用户输入。超出合理范围的日期也可能被标记为无效。
URL：此字段类型根据有效的 URL 格式验证用户输入。输入无效 URL 的用户将看到一条错误消息。
电话：此字段类型专为电话号码而设计，可能会触发基于特定国家/地区格式的验证（并非普遍支持）。



