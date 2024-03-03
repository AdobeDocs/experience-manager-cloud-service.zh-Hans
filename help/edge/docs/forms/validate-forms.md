---
title: 从电子表格到Forms — 掌握自适应表单块字段验证
description: 使用电子表格和自适应表单块字段更快地制作功能强大的表单！ 本指南可帮助您为 EDS Forms 区块字段构建自定义验证。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 17%

---


# 向表单字段添加验证

自适应表单块具有内置验证功能。 这些验证会根据所选字段类型和您提供的其他属性自动应用于现代浏览器。

## 了解字段类型和验证

自适应表单块支持各种 [HTML5输入类型](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)，包括文本、电子邮件、数字、日期等。 它还可适应 [文本区域](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)、 select和fieldset ，以及HTML-5固有的综合输入验证功能。

使用HTML字段类型定义用户可以输入的数据类型。 不同的字段类型具有不同的内置验证规则：

电子邮件：此字段类型根据通用电子邮件地址格式自动验证用户输入。 用户输入无效的电子邮件时，会看到一条错误消息。
数字：此字段类型仅允许数字输入。 输入非数字字符的用户将收到错误。
日期：此字段类型根据标准日期格式验证用户输入。 超出合理范围的日期也可能被标记为无效。
URL：此字段类型根据有效的URL格式验证用户输入。 输入无效URL的用户将看到错误消息。
电话：此字段类型专门针对电话号码而设计，并且可能会触发基于特定国家/地区格式（并非通用支持）的验证。


## 查看更多

* [创建并预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)