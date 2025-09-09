---
title: 如何使用AFP输出同步API？
description: 了解如何使用AFP输出同步API检索和同步输出呈现版本。
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, User
exl-id: 5602fc63-ef74-44eb-b3be-61b8f8a2795a
source-git-commit: 33dcc771c8c2deb2e5fcb582de001ce5cfaa9ce4
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 14%

---

# 使用 AEM Forms API 生成 AFP 输出

<span class="preview">这是一项预发行功能，可通过我们的[预发行渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features)访问。</span>

高级功能演示(AFP)是一种高性能文档格式，主要用于打印目的。\
本指南概述了使用AEM Forms生成AFP输出所需的所有步骤和配置。

<!--
## Prerequisites

To support AFP output generation, the following OSGi bundles must be present and in an **active** state:

* **AFP Core Bundle** – Available in the AFP repository
* **Forms Output Core** – Found in the Forms Output comments package
* **Bedrock Connector** – Provided by the Forms Output API
* **Cloud Ready Implementation** – Available through the Forms installer

>[!NOTE]
>
> * If any bundle is inactive, resolve dependency issues or reinstall manually.
> * To enable AFP generation, the `FT_FORMS-17887` toggle configurations must be set in AEM configuration manager.-->

## AFP生成API

使用XDP模板和输入数据生成AFP（高级函数演示）文件。

### 授权

您可以对本地环境使用&#x200B;**BasicAuth**（管理员凭据），或对AEM Cloud实例使用&#x200B;**BearerAuth**&#x200B;授权。

### 请求

**终结点：**
`POST http://<server>:<port>/adobe/forms/document/generate/afp`

### 标头

| 键 | 值 |
| --------------- | ------------------------------------------------------ |
| `Content-Type` | `application/pdf` |
| `Authorization` | `(Bearer Access token)` |

### 请求正文

**Content-Type： multipart/form-data**

| 键 | 类型 | 必需 | 描述 |
| ---------- | ---- | -------- | ------------------------------------------------------------------------- |
| `template` | 文件/文本 | 是 | 用作AFP生成模板的XDP文件（例如，`demo.xdp`） |
| `data` | 文件/文本 | 否 | 要与模板合并的数据文件（XML或JSON）（例如，`data.xml`） |
| `options` | 文本 | 否 | 包含用于控制AFP输出的选项（例如，分辨率、区域设置）的JSON字符串 |

**示例`options` JSON（文本字段）：**

```json
{
  "pdfVersion": "1.7",
  "resolution": 300,
  "locale": "en-US",
  "embedFonts": true,
  "contentRoot": "/usr/tmp"
}
```

### 响应

| 代码 | 描述 |
| ----- | ------------------------------------------------------------------------- |
| `200` | 操作成功。 返回AFP文档流。 |
| `400` | 错误请求。 请求有效负载格式不正确或缺少必填字段。 |
| `500` | 内部服务器错误。 请稍后重试。 |

### Curl命令

```
curl --location 'http://<server>:<port>/adobe/forms/document/generate/afp' \
--header 'Authorization: Bearertoken <base64-encoded-credentials>' \
--form 'template=@"<path-to-template>.xdp"' \
--form 'data=@"<path-to-data-file>.xml"' \
--form 'options=<JSON-options-string>'
```

### 测试API

您可以下载.yaml文件并将其上传到Postman以检查API的功能。

![AFP Postman图像](/help/forms/assets/afp-postman.png)

您可以保存响应并在AFP阅读器中打开保存的文件进行查看。

![查找IC文档](/help/forms/interactive-communication/assets/introimg.png)
