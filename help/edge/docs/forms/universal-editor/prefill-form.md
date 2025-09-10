---
title: 如何预填充自适应表单字段
description: 使用现有数据预填充自适应表单的字段。用户可以使用社交媒体账号登录，预填充表单中的基本信息。
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: 预填充自适应表单、自适应表单 edge delivery services、自适应表单自动填充
exl-id: 7b6224e2-a19c-4146-8545-0ce9d1da9b29
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 99%

---

# 配置使用 Edge Delivery Services 的自适应表单预填充服务

表单预填充是指用户打开表单时立即自动使用外部来源的相关数据填充表单字段的过程。预填充方法使用来自用户账号、数据库、已保存的草稿或其他后端系统的信息，简化了表单填写体验，减少手动输入，最大限度减少错误，并能加快完成速度。这不仅提高了用户满意度，而且增加了表单提交成功的可能性。

## 表单预填充的优势

| 优势 | 描述 |
|---------|-------------|
| **更快完成表单** | 减少手动输入数据，帮助用户快速完成表单 |
| **改善用户体验** | 表单让人感觉更加个性化、更方便，特别是对于回访用户来说 |
| **提高转化率** | 最大限度减少用户的工作量，减少表单放弃的发生 |
| **减少输入错误** | 来自可靠来源的数据有助于减少拼写错误和错误输入 |
| **提高数据质量** | 确保为后端系统提供结构化、准确且一致的数据 |

## 如何进行预填充

下图说明了当用户打开自适应表单时发生的自动预填充过程：

![表单预填充流程](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

预填充过程包括四个关键步骤：

1. **用户打开表单**：用户通过 URL 或导航访问一个自适应表单
1. **识别数据源**：预填充服务会确定所配置的数据源（表单数据模型或草稿服务）
1. **检索数据**：系统根据上下文、参数或用户身份获取相关的用户数据
1. **映射与显示**：数据通过 `bindRef` 属性映射到表单字段，填充好的表单显示给用户

此自动化过程可确保用户看到预先填充了自己相关信息的表单，从而显著提高用户体验和表单完成率。

## 预填充的数据结构

自适应表单支持两种类型的字段：

- **绑定字段**：与某个 `bindRef` 属性非空的数据源连接的字段
- **未绑定字段**：`bindRef` 为空值的独立字段

预填充数据结构包括：

- **afBoundData**：包含用于被绑定字段和面板的数据
- **afUnBoundData**：包含用于未绑定字段的数据

数据格式必须符合您的表单模型：

- **XFA 表单**：符合 XFA 模板架构的 XML
- **XML 架构表单**：符合架构结构的 XML
- **JSON 架构表单**：符合架构的 JSON
- **表单数据模型 (FDM) 表单**：符合 FDM 结构的 JSON
- **无架构表单**：所有字段均未绑定，并使用未绑定的 XML

## 先决条件

在配置预填充服务之前，请确保您已：

### 进行了必需的设置

- [为 Edge Delivery Services 配置了 GitHub 存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [将自适应表单块添加到您的项目](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [配置了数据源](/help/forms/configure-data-sources.md)
- [创建了表单数据模型 (FDM)](/help/forms/create-form-data-models.md)

### 满足访问权限要求

- 具有 AEM Forms as a Cloud Service 的访问权限
- 具有创建和编辑表单的权限
- 有权访问通用编辑器，并启用了所需的扩展

>[!TIP]
>
> 您还可以在通用编辑器中编辑表单，集成表单数据模型 (FDM)，从各种后端来源获取数据。有关详细信息，请参阅[在通用编辑器中将表单与表单数据模型集成](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)文章。

## 预填充服务选项

通用编辑器提供两种预填充服务选项：

| 服务类型 | 用途 | 数据源 | 最适合 |
|--------------|---------|-------------|----------|
| **表单门户草稿预填充** | 恢复已部分完成的表单 | 表单门户中保存的草稿 | 继续填写未完成的申请 |
| **表单数据模型预填充** | 从外部系统填充字段 | 通过 FDM 的后端数据库 | 自动填充用户个人资料数据 |

### 详细比较

| 功能 | 草稿预填充服务 | FDM 预填充服务 |
|---------|----------------------|---------------------|
| **身份验证** | 需要用户登录才能访问草稿 | 可根据数据源配置 |
| **设置复杂性** | 最低配置 | 需要 FDM 设置和映射 |
| **数据类型** | 静态保存的数据 | 实时动态数据 |
| **用例** | 恢复已保存的申请 | 从用户个人资料或数据库预填充 |


## 为表单配置预填充服务

+++阶段 1：设置表单数据模型

### 步骤 1：创建表单数据模型

1. 登录您的 AEM Forms as a Cloud Service 实例
1. 导航至 **Adobe Experience Manager** > **表单** > **数据集成**
1. 选择&#x200B;**创建** > **表单数据模型**
1. 选择您的&#x200B;**数据源配置**，然后选择已配置的&#x200B;**数据源**

   ![已创建的表单数据模型](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   >有关创建表单数据模型的详细说明，请参阅[创建表单数据模型](/help/forms/create-form-data-models.md)。

### 步骤 2：配置 FDM 服务

1. 前往 **Adobe Experience Manager** > **表单** > **数据集成**
1. 在编辑模式中打开您的表单数据模型
1. 选择一个数据模型对象，然后点击&#x200B;**编辑属性**
1. 为选定的数据模型对象配置&#x200B;**读取**&#x200B;和&#x200B;**写入**&#x200B;服务

   ![配置读取和写入服务](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

1. 配置服务参数：

   - 点击读取服务参数的编辑图标
   - 将参数绑定到&#x200B;**用户个人资料属性**、**请求属性**&#x200B;或&#x200B;**文字值**
   - 指定绑定值（例如为宠物登记表单指定 `petid`）

   ![配置宠物 ID 参数](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

1. 点击&#x200B;**完成**&#x200B;保存参数，然后点击&#x200B;**保存**&#x200B;保存 FDM

   >[!NOTE]
   >
   > 要了解有关配置 FDM 服务的更多信息，请参阅[使用表单数据模型 (FDM)](/help/forms/work-with-form-data-model.md)。

+++

+++阶段 2：创建和配置自适应表单

### 步骤 3：创建自适应表单

1. 导航至 **Adobe Experience Manager** > **表单** > **表单和文档**
1. 选择&#x200B;**创建** > **自适应表单**
1. 在&#x200B;**源**&#x200B;选项卡中选择一个 Edge Delivery Services 模板：

   ![Edge Delivery Services 模板](/help/edge/assets/create-eds-forms.png)

1. 点击&#x200B;**创建**，打开&#x200B;**创建表单**&#x200B;向导

   >
   >
   > 您可以通过编辑表单属性，从&#x200B;**数据**&#x200B;选项卡或更高版本配置数据源。

1. 指定表单详细信息：

   - **名称**：输入表单的描述性名称
   - **标题**：提供一个用户友好的标题
   - **GitHub URL**：输入您的存储库 URL（例如 `https://github.com/wkndforms/edsforms`）

1. 单击&#x200B;**创建**

   ![创建基于架构的表单](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)

表单在通用编辑器中打开以进行创作。

### 步骤 4：配置表单数据源

1. 选择表单，然后点击&#x200B;**属性**

   ![选择表单属性](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)

2. 打开&#x200B;**表单模型**&#x200B;选项卡
3. 从&#x200B;**从这里选择**&#x200B;下拉菜单中选择&#x200B;**表单数据模型 (FDM)**
4. 从下拉菜单中选择您创建的表单数据模型（例如 PetFDM）

   ![选择表单模型选项卡](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)

5. 点击&#x200B;**保存并关闭**
6. 在通用编辑器中打开表单进行编辑

FDM 中的表单元素将显示在&#x200B;**内容浏览器**&#x200B;的&#x200B;**数据源**&#x200B;选项卡中。

### 步骤 5：将数据绑定添加到表单字段

1. 从&#x200B;**数据源**&#x200B;选项卡中选择数据元素
2. 点击&#x200B;**添加**&#x200B;或拖放元素，构建表单

   ![通用编辑器的屏幕快照，显示一个基于架构的表单](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. 将数据绑定添加到表单字段：

   - 选择一个表单字段
   - 在&#x200B;**属性**&#x200B;面板中找到&#x200B;**绑定引用**&#x200B;属性
   - 选择适当的数据绑定引用

     ![数据绑定](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++阶段 3：配置预填充服务

### 步骤 6：启用必需的扩展

确保在通用编辑器中启用了这些扩展：

1. **AEM 表单属性扩展**

   - 在通用编辑器中打开&#x200B;**扩展管理器**
   - 启用 **AEM 表单属性**&#x200B;扩展

   ![表单属性图标](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

1. **数据源扩展**

   - 如果您看不到&#x200B;**数据源**&#x200B;图标，请启用&#x200B;**数据源**&#x200B;扩展

   ![通用编辑器扩展管理器的屏幕快照](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > 有关管理扩展的详细说明，请参阅[扩展管理器功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)。

### 步骤 7：配置预填充服务

1. 在通用编辑器中打开您的自适应表单
2. 点击 **AEM 表单属性**&#x200B;扩展图标

   ![选择表单属性图标](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. 点击&#x200B;**预填充**&#x200B;选项卡
4. 选择&#x200B;**表单数据模型预填充服务**

   ![选择预填充服务](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)

5. 点击&#x200B;**保存并关闭**

+++

+++阶段 4：测试您的预填充配置

### 步骤 8：预览和测试

1. 前往&#x200B;**表单** > **表单和文档**
2. 选择您的自适应表单
3. 选择&#x200B;**作为 HTML 预览**
4. 通过将参数附加到 URL 来测试预填充：

   `https://your-preview-url.com?<bindreferencefield>=<value>`

   **示例：**

   https://your-preview-url.com?petid=12345

   ![预填充表单](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)

表单应根据所提供的参数自动填充数据。

+++

## 示例

### 预填充数据结构示例

**基于 FDM 的表单的 JSON 示例：**

```
  {
    "afBoundData": {
      "user": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@example.com",
        "phone": "+1-555-0123"
      }
    },
    "afUnBoundData": {
      "additionalInfo": "User preferences loaded"
    }
  }
```

**基于 XFA 的表单的 XML 示例：**

```
  <?xml version="1.0" encoding="UTF-8"?>
  <afData>
    <afBoundData>
      <user>
        <firstName>John</firstName>
        <lastName>Doe</lastName>
        <email>john.doe@example.com</email>
      </user>
    </afBoundData>
  </afData>
```

### 预填充 URL 示例

以下 URL 仅用于说明目的，实际中不能按原样使用。测试预填充功能时，将主机和参数替换为与您自己的环境相关的数据。

**预填充基本测试：**

`https://preview.example.com/form.html?userId=12345`

**多参数测试：**

`https://preview.example.com/form.html?userId=12345&category=premium`


## 疑难解答

+++常见问题和解决方案

| 问题 | 可能的原因 | 解决方案 |
|-------|----------------|----------|
| **表单字段未进行预填充** | `bindRef` 值错误 | 验证 `bindRef` 准确符合 FDM 字段名称 |
| **数据格式错误** | 数据结构不匹配 | 确保预填充数据符合表单模型架构 |
| **未找到服务** | FDM 配置问题 | 检查 FDM 服务是否已正确配置并保存 |
| **身份验证错误** | 数据源连接 | 验证数据源凭据和连接情况 |
| **部分数据加载** | 缺少字段映射 | 确保所有必需字段都已正确绑定数据 |

+++

+++调试步骤

1. **验证 FDM 配置：**

   - 检查服务是否正确配置
   - 独立测试 FDM 服务
   - 验证数据源连接

2. **检查表单配置：**

   - 确认表单与正确的 FDM 关联
   - 验证字段 `bindRef` 的值
   - 预填充之前先测试表单

3. **测试数据流：**

   - 使用浏览器开发者工具检查网络请求
   - 检查控制台是否有 JavaScript 错误
   - 验证响应数据格式

4. **常见错误消息：**

   - “未找到预填充服务”：检查服务配置
   - “数据绑定失败”：验证 `bindRef` 准确性
   - “数据格式无效”：确保数据符合架构

+++

## 最佳实践

+++配置的最佳实践

- **使用描述性名称**：清晰命名您的 FDM 和服务
- **验证数据架构**：确保数据结构符合表单要求
- **逐步测试**：一次配置并测试一个字段
- **文档映射**：跟踪字段到数据的映射

+++

+++性能优化

- **最小数据量**：仅预填必要的字段
- **使用缓存**：为频繁被访问的数据配置适当的缓存
- **优化查询**：确保高效的数据库查询
- **监控性能**：启用预填充功能后，跟踪表单加载时间

+++

+++安全考虑事项

- **验证输入参数**：始终验证 URL 参数
- **清理数据**：在预填表单之前清理数据
- **实施访问控制**：确保用户只能访问自己的数据
- **使用 HTTPS**：数据传输始终使用安全连接

+++

+++用户体验指南

- **提供反馈**：获取数据的过程中显示加载指示器
- **妥善处理错误**：显示有用的错误消息
- **允许覆盖**：允许用户更改已预填充的数据
- **保持一致性**：在所有表单中使用一致的预填充行为

+++

## 常见问题解答

+++如何测试预填充是否正常工作？

预览您的表单，使用以下格式将预填参数附加到 URL：`?<bindreferencefield>=<value>`。确保该字段具有符合您的数据结构的有效 `bindRef`。使用浏览器开发者工具检查网络请求，验证是否正确获取数据。

+++

+++自适应表单预填充支持哪些数据格式？

自适应表单支持多种格式，具体取决于您的表单模型：

- **XFA 表单**：符合 XFA 架构的 XML
- **JSON 架构表单**：符合架构的 JSON 数据
- **FDM 表单**：映射到数据模型结构的 JSON
- **XML 架构表单**：符合架构结构的 XML

+++

+++被绑定和未绑定的字段都可以预填充吗？

是的，您可以预填这两种类型的字段。绑定字段使用 `afBoundData` 部分，并且必须符合您的表单模型架构。未绑定字段使用 `afUnBoundData` 部分，可以包含任何其他数据。

+++

+++如果只预填了部分字段该怎么办？

检查所有字段是否具有准确符合您的 FDM 的正确 `bindRef` 值。验证您的数据源是否包含所有必需字段，以及数据结构是否符合您的表单模型架构。

+++

+++我可以在一个表单中使用多个预填充服务吗？

您可以为每个表单配置一个主要预填充服务。但是，您可以在一个表单数据模型中组合使用不同的数据源来实现类似的功能。

+++

+++应如何执行预填充服务的身份验证？

身份验证取决于您的数据源配置。对于基于 FDM 的预填充，应在数据源设置中配置身份验证。对于草稿预填充，用户通常需要登录后才能访问他们保存的草稿。

+++



## 相关主题

- [在通用编辑器中将表单与表单数据模型集成](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [创建表单数据模型](/help/forms/create-form-data-models.md)
- [使用表单数据模型 (FDM)](/help/forms/work-with-form-data-model.md)
- [配置数据源](/help/forms/configure-data-sources.md)
- [适用于 AEM Forms 的 Edge Delivery Services 快速入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
