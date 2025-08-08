---
title: 适用于Edge Delivery Services的Forms提交服务
description: 使用Adobe托管的Forms提交服务将表单提交直接存储在电子表格中。 了解Google Sheets、OneDrive和SharePoint集成的设置、配置和API用法。
keywords: Forms提交服务， Edge Delivery Services forms，电子表格集成， Google Sheets forms， OneDrive forms， SharePoint forms，表单数据收集
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: b8b5937919dceb83a11b2fe359a9accec7012f81
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 1%

---

# 适用于Edge Delivery Services的Forms提交服务

Forms提交服务是Adobe的托管解决方案，它自动将表单提交数据直接存储在首选电子表格(Google工作表、Microsoft OneDrive或SharePoint)中。 这消除了对复杂后端基础架构的需求，同时提供了实时数据收集和管理。

>[!NOTE]
>
>**提前访问计划：**&#x200B;此功能当前可通过提前访问获得。 若要请求访问，请通过您的官方地址发送电子邮件[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，其中包含GitHub组织和存储库名称。
>
>**示例：**&#x200B;对于存储库`https://github.com/adobe/abc`，发送：组织= `adobe`，存储库= `abc`

## 概述

![Forms提交服务](/help/forms/assets/form-submission-service.png)
*图：Forms提交服务工作流程 — 从表单提交到电子表格存储*

### 谁应使用此服务？

**最适合：**

- **内容创建者**&#x200B;正在构建简单的数据收集表单
- **小型企业**&#x200B;需要快速的表单到电子表格工作流
- **营销团队**&#x200B;正在收集潜在客户信息
- **活动组织者**&#x200B;管理注册

**考虑以下项的替代项：**

- 需要自定义逻辑的复杂工作流
- 企业与数据库的集成
- 需要高级验证或处理的Forms

### 常见用例

| 用例 | 示例 | 电子表格优势 |
|----------|---------|-------------------|
| **联系Forms** | 网站查询→ Google工作表 | 轻松跟进和CRM导入 |
| **事件注册** | 会议注册→ Excel Online | 实时与会者跟踪 |
| **潜在客户生成** | SharePoint→的新闻稿注册 | 营销活动分析 |
| **反馈集合** | Google工作表→的调查回复 | 快速数据可视化 |

## 主要优点

Forms提交服务具备多项优势可简化数据收集：

### **简化的设置**

- **不需要后端基础结构** - Adobe托管提交终结点
- **与常用电子表格平台的直接集成**
- **自动将数据从表单字段映射到电子表格列**

### **实时数据管理**

- **即时数据捕获** — 提交内容会立即显示在电子表格中
- **结构化存储** — 用于轻松分析的组织列
- **实时协作** — 多个团队成员可以访问和分析数据

### **内置安全和访问控制**

- **利用现有权限** — 使用电子表格平台的共享控件
- **Adobe管理的安全性** — 具有企业级保护的安全提交终结点
- **数据所有权** — 您的数据保留在您选择的电子表格平台中

## 先决条件

在设置Forms提交服务之前，请确保您已：

### **技术要求**

- 为安装了最新自适应Forms块的Edge Delivery Services项目设置了&#x200B;**GitHub存储库**
- 列入允许列表 **访问审批** — 已将存储库添加到

### **电子表格平台设置**

选择一种受支持的平台：

- **Google工作表** — 具有工作表创建权限的Google帐户
- **Microsoft OneDrive** — 具有Excel Online访问权限的Microsoft 365帐户
- **SharePoint** — 具有列表/库权限的SharePoint访问权限

### **权限和访问**

- **编辑目标电子表格的权限**
- **共享功能**&#x200B;以授予对`forms@adobe.com`的访问权限
- 针对您选择的平台的&#x200B;**链接生成**&#x200B;权限

>[!TIP]
>
>**是Edge Delivery Services的新用户？**&#x200B;从[入门教程](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial)开始，设置您的项目基础。

## 配置方法

Forms提交服务提供了两种配置方法。 选择最适合您的工作流的方法：

### 选择配置方法

| 方法 | 最适合 | 所需时间 | 技术级别 |
|--------|----------|---------------|-----------------|
| **[手动设置](#manual-configuration)** | 内容创建者，一次性设置 | 10-15 分钟 | 初学者 |
| **[API配置](#api-configuration)** | 开发人员，自动化工作流 | 5-10 分钟 | 中间 |

### 项目设置

在配置任一方法之前，请确保您的AEM项目基础已准备就绪：

1. **使用最新的自适应AEM块创建或更新您的Forms项目** （[入门教程](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial)）
1. **更新项目根目录中的`fstab.yaml`**：

   ```yaml
   # Replace with the path to your shared folder
   mountpoints:
     /: https://drive.google.com/drive/folders/your-shared-folder-id
   ```

1. **与**&#x200B;共享您的项目文件夹`forms@adobe.com`（需要编辑权限）

## 手动配置

表单提交服务的![工作流](/help/forms/assets/forms-submission-service-workflow.png)
*图：手动Forms提交服务设置的完整工作流*

按照以下分步说明设置带有电子表格提交的表单：

### 第1步：创建表单定义

使用Google Sheets或Microsoft Excel创建窗体结构。

**表单创建步骤：**

1. **打开您的电子表格平台**(Google Sheets或Microsoft Excel)
1. **为您的表单项目创建新电子表格**
1. **为您的工作表命名**（必须为`helix-default`或`shared-aem`）
1. **使用**&#x200B;表单创建指南[定义您的表单结构](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)

![表单定义](/help/forms/assets/form-submission-definition.png)
*示例：具有字段类型、标签和验证规则的表单定义*

>[!IMPORTANT]
>
>**工作表命名要求**
>
>您的表单定义工作表必须命名为：
>
>- `helix-default` （建议用于单个表单）
>- `shared-aem` （对于多表单项目）
>
>系统无法识别其他工作表名称。

**验证检查点：**

- 表单结构已完成，且包含所有必填字段
- 工作表已正确命名（`helix-default`或`shared-aem`）
- 字段类型和验证规则已正确配置

### 第2步：创建数据收集工作表

设置专用工作表以接收表单提交数据。

**数据表设置：**

1. **向现有电子表格中添加新工作表**
1. **将工作表完全命名为`incoming`**（区分大小写）
1. **设置与表单字段匹配的列标题**
1. **保存电子表格**&#x200B;以确保保留更改

![传入工作表](/help/forms/assets/form-submission-incoming-sheet.png)
*示例：带有与表单字段匹配的列标题的传入工作表*

>[!WARNING]
>
>**关键要求**
>
>工作表必须完全命名为`incoming`（小写）。 如果没有此工作表：
>
>- 表单提交将被拒绝
>- 不会存储任何数据
>- 用户将看到提交错误

**验证检查点：**

- 您的电子表格中存在`incoming`工作表
- 列标题与表单字段名称匹配
- 工作表已正确保存并可访问

>[!TIP]
>
>**专业提示：**&#x200B;从表单定义中复制准确的字段名称，以确保表单字段与电子表格列完全匹配。

### 步骤3：与Adobe服务共享电子表格

授予Adobe Forms提交服务访问电子表格的权限。

**共享进程：**

1. **单击电子表格右上角的共享按钮**
1. **添加Adobe服务帐户：**

   - 电子邮件： `forms@adobe.com`
   - 权限级别： **编辑者** （数据写入所需）

1. **发送共享邀请**
1. **复制电子表格链接**，以便进行下一步

   ![共享传入工作表](/help/forms/assets/form-submission-share-incoming.png)

*授予Adobe服务访问权限的分步共享流程*

**平台特定说明：**

**Google工作表：**

- 将`forms@adobe.com`添加为编辑器
- 确保启用了“具有此链接的任何人都可以查看”
- 复制可共享链接

**Microsoft Excel (OneDrive/SharePoint)：**

- 添加具有编辑权限的`forms@adobe.com`
- 将链接共享设置为“拥有链接的任何人都可以编辑”
- 复制共享URL

  ![复制传入工作表的链接](/help/forms/assets/form-submission-copy-link.png)
  *示例：正在复制表单配置的可共享链接*

**验证检查点：**

- `forms@adobe.com`拥有电子表格的编辑器访问权限
- 电子表格链接已复制并可供使用
- 共享权限允许外部访问

### 步骤4：将表单连接到电子表格

将表单定义链接到提交电子表格。

**表单电子表格连接：**

1. **打开您的表单定义电子表格**（带有`helix-default`或`shared-aem`张表格的表格）
1. **在表单定义中查找提交字段行**
1. **将复制的电子表格链接**&#x200B;粘贴到“提交”字段的&#x200B;**操作**&#x200B;列
1. **将更改保存到表单定义**

   ![链接电子表格](/help/forms/assets/form-submission-sheet-linking.png)

*示例：将提交操作连接到您的数据收集电子表格*

**正在发布您的表单：**

1. 在浏览器中&#x200B;**打开AEM Sidekick**
1. **预览表单**&#x200B;以测试配置
1. **发布表单**&#x200B;以使其上线

**最终验证：**

- 电子表格链接已正确添加到提交字段操作
- 表单定义已保存并发布
- 表单预览正确显示所有字段
- 提交按钮配置正确

>[!SUCCESS]
>
>**安装完成！**&#x200B;您的表单现已连接到Forms提交服务。 通过提交示例数据并检查您的`incoming`工作表对其进行测试。

**参考资料：**

- [使用正确的配置完成示例电子表格](/help/forms/assets/spreadsheet.xlsx)
- 发布指南的[AEM Sidekick文档](https://www.aem.live/docs/sidekick)

## API 配置

API方法允许开发人员以编程方式将数据提交到Forms提交服务，非常适合于自动化工作流和自定义集成。

### 何时使用API

**最适合：**

- 自动数据收集系统
- 自定义表单实施
- 与现有应用程序集成
- 批量数据提交工作流

### API先决条件

在使用API之前，请确保您已：

- 已完成&#x200B;**电子表格设置**（包括`incoming`表）
- 已向&#x200B;**授予** Adobe服务访问权限`forms@adobe.com`
- 您发布的表单中的&#x200B;**表单ID**
- **存储库信息**（组织和站点名称）

>[!IMPORTANT]
>
>**必需的设置步骤**
>
>API需要与手动配置相同的电子表格设置：
>
>- `incoming`工作表必须存在
>- `forms@adobe.com`必须具有编辑器访问权限
>- 工作表必须通过AEM Sidekick发布

### API端点和身份验证

**基本URL：** `https://forms.adobe.com/adobe/forms/af/submit/{id}`

**必需的标头：**

- `Content-Type: application/json`
- `x-adobe-routing: tier=live,bucket=main--[repository]--[organization]`

**API文档：**&#x200B;[完整API引用](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)

### 使用Postman

Postman为测试API提交提供了一个用户友好的界面。

**安装说明：**

1. **在Postman中创建新的POST请求**
1. **配置终结点：** `https://forms.adobe.com/adobe/forms/af/submit/{id}`
1. **替换占位符：**

   - `{id}`→您的实际表单ID
   - `[repository]`→您的GitHub存储库名称
   - `[organization]`→您的GitHub组织/用户名

**请求配置：**

```json
POST https://forms.adobe.com/adobe/forms/af/submit/your-form-id

Headers:
Content-Type: application/json
x-adobe-routing: tier=live,bucket=main--your-repo--your-org

Body (JSON):
{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Mary",
            "age": "35",
            "subscribe": null,
            "email": "mary@gmail.com"
                }
}
```

**预期响应：**

- **状态代码：** `201 Created`
- **数据立即出现在您的**&#x200B;电子表格中`incoming`

![Postman屏幕](/help/forms/assets/postman-api.png)
*示例：使用Postman接口成功提交API*

### 使用命令行(curl)

对于更喜欢终端/命令提示的开发人员，使用curl以编程方式提交数据。

**命令行设置：**

在下列命令中替换以下占位符：

- `{id}`→您的实际表单ID
- `[repository]`→您的GitHub存储库名称
- `[organization]`→您的GitHub组织/用户名

>[!BEGINTABS]

>[!TAB macOS/Linux]

```bash
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" \
    --header "Content-Type: application/json" \
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" \
    --data '{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Joe",
            "age": "35",
            "subscribe": null,
      "email": "joe@example.com"
                }
            }'
```

>[!TAB Windows命令提示符]

```cmd
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" ^
    --header "Content-Type: application/json" ^
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" ^
  --data "{\"data\": {\"startDate\": \"2025-01-10\", \"endDate\": \"2025-01-25\", \"destination\": \"Australia\", \"class\": \"First Class\", \"budget\": \"2000\", \"amount\": \"1000000\", \"name\": \"Joe\", \"age\": \"35\", \"subscribe\": null, \"email\": \"joe@example.com\"}}"
```

>[!TAB Windows PowerShell]

```powershell
$body = @{
  data = @{
    startDate = "2025-01-10"
    endDate = "2025-01-25"
    destination = "Australia"
    class = "First Class"
    budget = "2000"
    amount = "1000000"
    name = "Joe"
    age = "35"
    subscribe = $null
    email = "joe@example.com"
  }
} | ConvertTo-Json -Depth 3

Invoke-RestMethod -Uri "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" `
  -Method POST `
  -Headers @{"Content-Type"="application/json"; "x-adobe-routing"="tier=live,bucket=main--your-repo--your-org"} `
  -Body $body
```

>[!ENDTABS]

### API响应和验证

**成功的响应：**

```http
HTTP/1.1 201 Created
Connection: keep-alive
Content-Length: 0
X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
Date: Fri, 10 Jan 2025 13:06:10 GMT
Access-Control-Allow-Origin: *
```

**数据验证：**

成功提交后，请验证数据是否显示在电子表格中：

![已更新工作表](/help/forms/assets/updated-sheet.png)
*示例：数据已成功通过API写入传入工作表*

**响应验证：**

- **HTTP状态：** `201 Created`表示提交成功
- **X-Request-Id：**&#x200B;用于跟踪提交的唯一标识符
- **数据在几秒内显示在您的**&#x200B;工作表中`incoming`
- **所有表单字段**&#x200B;均正确映射到电子表格列

## 疑难解答

### 常见问题和解决方案

**问题： 403禁止出现错误**

```
Causes: Missing or incorrect access permissions
Solutions:
- Verify forms@adobe.com has Editor access to your spreadsheet
- Check that your repository is added to the allowlist
- Confirm the x-adobe-routing header format
```

**问题： 404 Not Found错误**

```
Causes: Incorrect Form ID or endpoint URL
Solutions:  
- Verify your Form ID is correct
- Check the API endpoint URL format
- Ensure your form is published and live
```


**问题：数据未出现在电子表格中**

```
Causes: Missing 'incoming' sheet or permission issues
Solutions:
- Confirm 'incoming' sheet exists (case-sensitive)
- Verify column headers match form field names exactly
- Check forms@adobe.com has edit permissions
- Ensure spreadsheet is shared properly
```


**问题： JSON格式无效错误**

```
Causes: Malformed request body
Solutions:
- Validate JSON syntax using online JSON validators
- Ensure proper escaping of special characters
- Check quote marks and brackets are balanced
```


### 获取帮助

**支持渠道：**

- **早期访问问题：**&#x200B;电子邮件[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)
- **API文档：** [开发人员参考](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)
- **社区支持：** [Adobe Experience League社区](https://experienceleaguecommunities.adobe.com/)

## 后续步骤

现在您已配置Forms提交服务，请探索以下相关主题：

### **增强您的Forms**

- **[创建高级Forms](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)** — 添加验证、条件逻辑和自定义样式
- **[表单组件指南](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-components)** — 浏览可用的表单字段类型

### **替代提交方法**

- **[AEM发布提交](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)** — 用于复杂的工作流和企业集成
- **[自定义提交操作](/help/forms/configure-submit-actions-core-components.md)** — 高级提交处理

### **数据管理**

- **[表单分析](/help/forms/view-understand-aem-forms-analytics-reports.md)** — 跟踪表单性能和使用情况
- **[数据集成](/help/forms/configure-data-sources.md)** — 将表单连接到数据库和CRM系统

## 摘要

Forms提交服务提供了一个功能强大的无代码解决方案，用于将表单数据直接收集到电子表格中。 主要优势包括：

- **快速设置** — 不需要后端基础结构
- **实时数据** — 立即提交捕获
- **灵活平台** - Google Sheets、OneDrive或SharePoint
- **API访问** — 程序化提交功能
- **企业安全性** — 具有访问控制的Adobe管理的端点

**准备好开始了吗？***遵循可视化设置的[手动配置](#manual-configuration)指南，或跳转到[API配置](#api-configuration)进行程序集成。
