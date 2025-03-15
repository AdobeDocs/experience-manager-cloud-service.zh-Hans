---
title: AEM Forms as a Cloud Service通信API
description: 在云中使用AEM Forms Communication API生成、操作和保护文档
Keywords: document generation, PDF manipulation, document security, batch processing, document conversion, PDF/A compliance
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: a9eed5b6219163e721d81c9d77a31604666a2ac5
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 3%

---


# AEM Forms as a Cloud Service通信API {#communications-apis-overview}

> **版本可用性**
>
> * **AEM 6.5**： [AEM文档服务概述](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html)
> * **AEM as a Cloud Service**：本文

## 简介

AEM Forms as a Cloud Service中的通信API可帮助您创建品牌批准、个性化和标准化的文档，以满足您的业务需求。 这些功能强大的API使您能够以编程方式生成、操作和保护文档，无论是在按需还是高容量批处理中。


### 主要优点

* **简化文档生成** — 通过将模板与客户数据合并来创建个性化文档
* **强大的文档操作** — 以编程方式组合、重新排列和验证PDF文档
* **灵活的部署选项** — 使用按需API满足低延迟需求，或使用批量API进行高吞吐量操作
* **增强的安全性** — 应用数字签名、认证和加密来保护敏感文档
* **云原生架构** — 利用可扩展的安全云基础架构，无维护开销

## 主要功能

Communications API提供了一组全面的文档处理功能，可划分为以下功能区域：


| 文档生成 | 文档操作 | 文档提取 | 文档转换 | 记录Assurance |
|---------------------|----------------------|---------------------|---------------------|-------------------|
| 通过将模板与各种格式(包括PDF和打印格式)的数据合并来生成个性化文档。 | 以编程方式组合、重新排列和验证PDF文档以创建新文档包。 | 从PDF文档中提取属性、元数据和内容以供进一步处理。 | 在多种格式之间转换文档，包括PDF/A合规性验证以满足存档需求。 | 应用数字签名、认证和加密来保护文档。 |

## 文档生成

通信文档生成API将模板(XFA或PDF)与客户数据(XML)相结合，在PDF中创建个性化文档以及各种打印格式(PS、PCL、DPL、IPL、ZPL)。

### 文档生成的工作方式

典型的工作流包括：

1. 使用[Designer](use-forms-designer.md)创建模板
2. 正在准备XML数据以填充模板
3. 使用通信API将模板与数据合并
4. 以所需格式生成输出文档

![通信文档生成工作流](assets/communicaions-workflow.png)

### 创建PDF文档

文档生成API允许您通过将XML数据与表单模板合并来创建非交互式PDF文档：

![创建PDF文档](assets/outPutPDF_popup.png)

您可以通过下载将生成的PDF交付给用户，将它们存储在存储库中，或者选择将它们上传到Azure Blob Storage。

<span class="preview">可以通过[早期采用者计划](/help/forms/early-access-ea-features.md)将生成的PDF上载到Azure Blob Storage。 通过正式电子邮件联系aem-forms-ea@adobe.com以加入。</span>

### 创建打印格式文档

生成打印格式的文档，包括：
* PostScript (PS)
* 打印机命令语言(PCL)
* 斑马打印语言(ZPL)

这些格式非常适合于大容量打印操作和专业化打印需求。

### 多个文档的批处理

使用批处理API高效地处理大量文档：

![批处理工作流](assets/ou_OutputBatchMany_popup.png)

批量处理允许您：

* 为XML数据源中的每个记录生成单独的文档
* 异步处理文档以提高性能
* 为批处理配置各种转化参数

## 文档操作

文档操作API可帮助您以编程方式组合、重新排列和转换PDF文档。

### 文档程序集

将多个PDF或XDP文档合并到一个有凝聚力的文档中：

![从多个PDF文档汇编一个简单的PDF文档](assets/as_document_assembly.png)

文档组件功能包括：
* 从多个来源创建简单的PDF文档
* 构建PDF项目组合
* 汇编加密文档
* 为法律文档添加Bates编号
* 拼合和组合交互式表单

### 文档反汇编

将大型PDF文档划分为更小、更易于管理的组件：

![根据书签将源文档划分为多个文档](assets/as_intro_pdfsfrombookmarks.png)

文档反汇编允许您：
* 从源文档提取特定页面
* 根据书签划分文档
* 从大型编译创建逻辑文档集

>[!NOTE]
>
> AEM Forms包含许多内置字体，可与PDF文件无缝集成。 有关支持的字体的完整列表，[单击此处](/help/forms/supported-out-of-the-box-fonts.md)。

## 文档提取

<span class="preview">文档提取可通过[早期采用者计划](/help/forms/early-access-ea-features.md)获得。 通过正式电子邮件联系aem-forms-ea@adobe.com以加入。</span>

文档提取API允许您从PDF文档检索信息，包括：

* 文档属性（是否为可填写表单、是否具有附件等）
* 使用权限和权限
* 使用Adobe可扩展元数据平台(XMP)的元数据信息

此功能对于文档管理系统、归档解决方案和工作流自动化特别有用。

## 文档转换

### PDF/A转换和验证

将标准PDF文档转换为PDF/A格式以进行长期存档：

* 支持PDF/A-1a、1b、2a、2b、3a和3b合规标准
* 验证PDF/A合规性
* 使用嵌入的字体和未压缩的内容保持文档完整性

### PDF到XDP的转换

<span class="preview">PDF到XDP的转换可通过[早期采用者计划](/help/forms/early-access-ea-features.md)获得。 通过正式电子邮件联系aem-forms-ea@adobe.com以加入。</span>

将包含XFA流的PDF文档转换为XDP格式，以供模板编辑和重用。

## 记录Assurance {#doc-assurance}

Document Assurance包括签名和加密API ，可在文档的整个生命周期中保护您的文档。

### 签名API

使用数字签名和认证保护PDF文档：

* 添加可见或不可见的签名字段
* 对签名字段进行数字签名
* 验证文档的完整性
* 从文档中删除签名
* 从文档中删除签名字段

<span class="preview">可通过[早期采用者计划](/help/forms/early-access-ea-features.md)删除签名和签名字段。 通过正式电子邮件联系aem-forms-ea@adobe.com以加入。</span>

### 加密API

使用加密保护文档内容：

* 使用密码加密PDF文档
* 删除基于密码的加密
* 确定应用于文档的安全类型
* 从受保护文档检索安全信息

### 文档实用工具 {#doc-utility}

文档实用程序提供了用于处理PDF文档的附加功能：

#### 使用权限API(Reader扩展)

<span class="preview">使用权限(Reader扩展)可通过[早期采用者计划](/help/forms/early-access-ea-features.md)获得。 通过正式电子邮件联系aem-forms-ea@adobe.com以加入。</span>

通过向Adobe Reader文档添加使用权限，启用PDF文档等功能来扩展Adobe Reader的功能：

* 表单填写和保存
* 添加注释和批注
* 数字签名
* 文件附件
* 表单数据导入/导出
* 访问Web服务和数据库

可用的使用权限包括：

* **表单交互**：表单填写、表单数据导入/导出、动态表单字段/页面
* **注释**：注释（在线和离线）、数字签名
* **文档处理**：嵌入文件，提交独立，条形码解码
* **联机服务**：联机Forms，访问Web服务

## 通信API的类型 {#types}

通信提供了两种类型的API以适应不同的用例：

### 同步API

**最适合**：按需、低延迟、单个文档生成
**用例**：用户触发的文档生成，交互式应用程序
**文档**： [同步API引用](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

### 批处理API（异步）

**最适合**：已计划、高吞吐量、多文档生成
**用例**：月报表、帐单、通知、计划报表
**文档**：[批次API引用](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

## 通信API快速入门

### 载入流程

通信可作为独立模块或加载项供Forms as a Cloud Service用户使用：

1. 联系Adobe销售人员或您的Adobe代表以请求获取访问权限
2. Adobe将为您的组织启用访问权限并授予管理员权限
3. 然后，管理员可以向组织中的开发人员授予访问权限

### 在您的环境中启用通信

请按照以下步骤为Forms as a Cloud Service环境启用通信：

1. 登录Cloud Manager并打开AEM Forms as a Cloud Service实例
2. 打开编辑程序选项，然后转到解决方案和加载项选项卡
3. 选择&#x200B;**[!UICONTROL Forms — 通信]**&#x200B;选项

   ![通信](assets/communications.png)

   如果您已启用&#x200B;**[!UICONTROL Forms — 数字注册]**，请改为选择&#x200B;**[!UICONTROL Forms — 通信加载项]**&#x200B;选项。

   ![加载项](assets/add-on.png)

4. 单击&#x200B;**[!UICONTROL 更新]**
5. 运行构建管道 — 通信API将在成功完成后启用

>[!NOTE]
>
> 要启用文档操作API，请将以下规则添加到[Dispatcher配置](setup-local-development-environment.md#forms-specific-rules-to-dispatcher)：
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## API参考文档 {#api-reference}

Communications API可划分为若干个功能类别，每个类别都有详细的参考文档。 这些API参考可提供关于端点、参数、请求/响应格式和身份验证要求的全面信息。

### 文档生成API

| API | 描述 | 引用链接 |
|-----|-------------|----------------|
| 文档生成 — 同步 | 为交互式方案按需生成低延迟的文档 | [API引用](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/) |
| 文档生成 — 批次 | 为计划的操作异步处理大量文档 | [API引用](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/) |

### 文档操作API

| API | 描述 | 引用链接 |
|-----|-------------|----------------|
| 文档操作 — 同步 | 使用DDX说明组合、拆分和转换PDF文档 | [API引用](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/) |

### 文档Assurance API

| API | 描述 | 引用链接 |
|-----|-------------|----------------|
| DocAssurance — 同步 | 应用数字签名、认证、加密和Reader扩展 | [API引用](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/docassurance/) |

### 常见API参数

每个API类别都有特定的参数，但一些常见的参数包括：

#### 文档生成参数

| 参数 | 类型 | 必需 | 描述 |
|-----------|------|----------|-------------|
| `template` | 字符串 | 是 | XDP或PDF模板文件的路径 |
| `data` | 字符串 | 否 | 要与模板合并的XML数据 |
| `outputOptions` | 对象 | 否 | 输出文档的配置选项 |

#### 文档操作参数

| 参数 | 类型 | 必需 | 描述 |
|-----------|------|----------|-------------|
| `ddx` | 字符串 | 是 | 文档汇编或反汇编的DDX说明 |
| `inputDocuments` | 对象 | 是 | 要处理的输入文档的地图 |
| `outputOptions` | 对象 | 否 | 输出文档的配置选项 |

#### 记录Assurance参数

| 参数 | 类型 | 必需 | 描述 |
|-----------|------|----------|-------------|
| `inputPDF` | 字符串 | 是 | 输入要受保护或签名的PDF文档 |
| `certificateAlias` | 字符串 | 条件 | 用于签名操作的证书的别名 |
| `credentialPassword` | 字符串 | 条件 | 签名中使用的凭据的密码 |

有关完整的参数详细信息、身份验证要求以及请求/响应示例，请参阅上表中链接的特定API参考文档。

## 其他资源 {#see-also}

* [通信处理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
* [通信处理 — 批处理API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [AEM Forms as a Cloud Service架构](/help/forms/aem-forms-cloud-service-architecture.md)
* [API参考文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)
* [早期采用者计划功能](/help/forms/early-access-ea-features.md)
