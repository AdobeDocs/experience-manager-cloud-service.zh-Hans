---
title: 在Forms上的自适应Forms中HTML电子邮件模板as a Cloud Service
description: 了解如何将电子邮件模板用于自适应表单。
feature: Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: b9364394f683fa8af5d28723e5f10b20b001ea37
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---

# 自适应Forms中的电子邮件模板

自适应Forms允许您使用HTML和纯文本电子邮件模板。 通过HTML电子邮件模板，您可以在提交表单时发送丰富、个性化且具有视觉吸引力的电子邮件。 这些电子邮件可使用表单数据自定义，并使用各种电子邮件标记（如图像和链接）进行增强。 通过自适应Forms，您可以上传包含HTML模板的文件或使用纯文本编辑器创建这些模板。

![HTML电子邮件模板](/help/forms/assets/html-email.png)

本文可帮助您在Adaptive Forms中配置和使用电子邮件模板。 到最后，您将能够：

* [为自适应表单配置HTML模板](#configure-an-html-template-for-an-adaptive-form)
* [为自适应表单配置纯文本电子邮件模板](#configure-a-plain-text-template-for-an-adaptive-form)
* [在电子邮件模板中使用表单数据](#use-form-data-in-your-email-templates)


下面是相关步骤的快速概述：

1. 打开自适应表单进行编辑。
1. 配置[发送电子邮件](/help/forms/configure-submit-action-send-email.md)提交操作。
1. 选择或上载HTML模板，或手动输入电子邮件模板。
1. 测试您的电子邮件配置。

## 为自适应表单配置HTML模板

您可以设置自适应表单，以使用&#x200B;[**发送电子邮件**&#x200B;提交操作](/help/forms/configure-submit-action-send-email.md)在提交时发送电子邮件。 操作提供了两种配置HTML模板的方法：

### 选项1：选择包含HTML模板的文件

在继续之前，请确保已将HTML模板上传到AEM Forms环境。

1. 打开自适应表单进行编辑。
1. 转到&#x200B;**内容浏览器**，选择&#x200B;**指南容器**，然后点按属性图标。 出现标题为`Adaptive Form Container`的对话框。
1. 转到&#x200B;**提交**&#x200B;选项卡并选择&#x200B;**发送电子邮件**&#x200B;提交操作。
1. 启用&#x200B;**使用外部模板**&#x200B;选项。
1. 启用&#x200B;**使用HTML模板**&#x200B;选项。
1. 单击“外部模板路径”选项的文件夹图标，然后浏览以选择您的HTML模板。
1. 单击完成以保存配置。

现在已为自适应表单配置了HTML模板。

### 选项2：手动输入或粘贴HTML模板

1. 打开自适应表单进行编辑。
1. 转到&#x200B;**内容浏览器**，选择&#x200B;**指南容器**，然后点按属性图标。 出现标题为`Adaptive Form Container`的对话框。
1. 转到&#x200B;**提交**&#x200B;选项卡并选择&#x200B;**发送电子邮件**&#x200B;提交操作。
1. 启用&#x200B;**使用外部模板**&#x200B;选项。
1. 启用&#x200B;**使用HTML模板**&#x200B;选项。
1. 在提供的&#x200B;**电子邮件HTML**&#x200B;框中直接键入或粘贴模板代码。


## 为自适应表单配置纯文本模板

您可以设置自适应表单，以使用&#x200B;[**发送电子邮件**&#x200B;提交操作](/help/forms/configure-submit-action-send-email.md)在提交时发送电子邮件。 该操作提供了两种配置纯文本模板的方法：

### 选项1：选择包含模板的文件

在继续之前，请确保已将HTML模板上传到AEM Forms环境。

1. 打开自适应表单进行编辑。
1. 转到&#x200B;**内容浏览器**，选择&#x200B;**指南容器**，然后点按属性图标。 出现标题为`Adaptive Form Container`的对话框。
1. 转到&#x200B;**提交**&#x200B;选项卡并选择&#x200B;**发送电子邮件**&#x200B;提交操作。
1. 启用&#x200B;**使用外部模板**&#x200B;选项。
1. 单击&#x200B;**外部模板路径**&#x200B;选项的文件夹图标，然后浏览以选择纯文本模板。
1. 单击完成以保存配置。

您的模板现在已为自适应表单配置了。

### 选项2：手动输入或粘贴HTML模板

1. 打开自适应表单进行编辑。
1. 转到&#x200B;**内容浏览器**，选择&#x200B;**指南容器**，然后点按属性图标。 出现标题为`Adaptive Form Container`的对话框。
1. 转到&#x200B;**提交**&#x200B;选项卡并选择&#x200B;**发送电子邮件**&#x200B;提交操作。
1. 将纯文本模板代码直接键入或粘贴到提供的&#x200B;**电子邮件模板**&#x200B;框中。

## 在电子邮件模板中使用表单数据

您可以使用占位符将表单数据包含在电子邮件模板中。 发送电子邮件时，这些占位符会动态替换为实际的表单字段值。 例如：

* ${name}：名为“name”的字段的值。
* ${email}：名为“email”的字段的值。
* ${message}：名为“message”的字段的值。

### 示例HTML电子邮件模板

以下是使用了表单数据占位符的HTML电子邮件模板的示例：

```HTML
    <!DOCTYPE html>
    <html>
    <head>
        <title>Form Submission</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                line-height: 1.6;
                color: #333;
            }
            h2 {
                color: #0056b3;
            }
        </style>
    </head>
    <body>
        <h2>Thank You for Your Submission</h2>
        <p>Dear ${name},</p>
        <p>We have received your submission with the following details:</p>
        <ul>
            <li><strong>Email:</strong> ${email}</li>
            <li><strong>Phone Number:</strong> ${phone_number}</li>
            <li><strong>Message:</strong> ${message}</li>
        </ul>
        <p>We will get back to you soon!</p>
        <p>Best regards,</p>
        <p>Your Team</p>
    </body>
    </html>
```

### 纯文本电子邮件模板示例

以下是纯文本电子邮件模板的示例：

```TXT
    
    Subject: Thank You for Your Submission
    
    Dear ${name},
    
    We have received your submission with the following details:
    
    - Email: ${email}
    - Phone Number: ${phone_number}
    - Message: ${message}
    
    We will get back to you soon!
    
    Best regards,
    Your Team
```

将占位符（${name}、${email}等）替换为自适应表单中的相应表单字段名称。

## HTML电子邮件模板的最佳实践

* 确保您的样式内联，以便更好地与电子邮件客户端兼容。
* 使您的模板可快速响应，以在移动设备上获得更好的体验。
* 使用Litmus或Email on Acid等工具预览跨各种电子邮件客户端的电子邮件。
* 确保占位符名称与表单字段名称完全匹配。
* 检查HTML模板中是否存在缺失或不正确的标记。
* 验证是否已正确配置[发送电子邮件](/help/forms/configure-submit-action-send-email.md)提交操作。
