---
title: 沟通创建技能
description: 了解Experience Production Agent的通信创建技能以及如何使用自然语言创建交互式通信。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 701c35341ead684cdf306cadcacd8c638004facd
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# 沟通创建技能 {#ic-creation-skill}

交互式通信是专为业务通信而设计的个性化数据驱动文档，如帐户报表、策略文档、帐单、欢迎套件和福利通知。 与收集用户输入的表单不同，交互式通信会生成具有动态、特定于收件人的内容的输出文档。

通信创建技能是Experience Production Agent的一项功能，旨在使用自然语言提示开发交互式通信。 此技能可自动为打印生成数据驱动的个性化通信(PDF格式)。 该技能通过AI助手显现出来。

通信创建技能的一些主要优势包括：

* **加速通信开发**：使用简单的自然语言命令快速创建通信，无需学习传统的产品界面。
* **一致的品牌通信**：使用批准的模板和样式创建遵循您组织的品牌、模板和样式准则的通信。
* **技术壁垒更低**：允许业务用户轻松创建通信，而无需高级技术或深厚的产品专业知识。

## 功能 {#capabilities}

<!-- * **Create personalized communications with plain text prompt**: You can create communication documents for print (in PDF format) by submitting your requirements in plain language. The agent automatically generates appropriate document structures, layouts, and data bindings based on your natural language description. -->

* **从模板创建**：您可以使用已批准的组织模板来确保品牌一致性和合规性标准。 该代理利用您现有的模板和风格指南来创建符合法规要求的品牌通信。

* **将现有图像和文档导入并转换为交互式通信**：您可以将现有文档导入并转换为交互式通信。 代理可分析上传的内容以检测字段、保留布局并创建与动态内容功能的数据驱动通信。 支持的格式包括PDF、图像(JPG、PNG)和手绘模板。


## 示例提示 {#sample-prompts}

* *使用位于https://[aem-author-url]/path/to/pdf/file*&#x200B;的模板为贷款对帐单创建通信
* *从PDF创建通信，网址为https://[aem-author-url]/path/to/pdf/file*
* *从位于https://[aem-author-url]/path/to/image/file*&#x200B;的图像文件创建通信
* 使用PDF文件(位于https://[aem-author-url]/path/to/pdf/file)创建书信

## 优化您的通信 {#refine-with-ic-editor}

使用AI助手创建初始通信结构后，可以使用交互式通信编辑器来优化和增强文档。 在交互式通信编辑器中，您可以使用自然语言提供提示，以便：

* **添加字段和内容**：使用自然语言提示向通信文档中添加新字段、文本块、图像、图表、表及其他组件。 代理将解释您的说明并插入具有正确结构和格式的相应元素。

* **编辑字段和内容**：通过对话式命令修改通信文档中的现有字段和内容。 更新字段属性、更改文本内容、调整数据绑定以及优化组件配置。

* **删除字段和内容**：使用自然语言说明从通信文档中删除不需要的字段、组件或部分。 代理删除指定的元素，同时保持文档结构和布局完整性。

* **样式字段和内容**：通过自然语言提示将格式设置和样式应用于字段和内容。 根据品牌准则和设计要求调整字体、颜色、对齐方式、间距和其他可视属性。

### 优化通信的示例提示 {#sample-prompts-refining}

* *生成车辆保险理赔结算函*
* *将免责声明文本变为斜体*
* *将免责声明文本的字体大小更改为12*
* *将免责声明文本的字体颜色更新为红色*
* *将页眉和页脚文本框的背景颜色更新为浅灰色*
* *添加具有签名和确认字段的新免责声明面板*
* *删除确认文本字段*
* *添加具有三列的付款详细信息表*
* *更新策略编号字段与中心*&#x200B;的对齐方式
* *将条款和条件部分的行距更改为1.5*

有关交互式通信编辑器功能的详细信息，请参阅[交互式通信文档](/help/forms/introduction-to-interactive-communication.md)。

