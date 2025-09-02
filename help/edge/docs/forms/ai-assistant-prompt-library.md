---
title: Forms Experience Builder — 提示库
description: 收集经过验证的提示词模式和示例，用于在表单管理用户界面、自适应表单编辑器和通用编辑器中使用 AI 辅助构建表单。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 13%

---


# Forms Experience Builder — 提示库

可重用提示模式的收藏集和针对Forms Experience Builder优化的示例。 这个简化的库重点关注两种核心创建方法：从头开始创建以及导入和转换，并增强对LLM支持的智能字段和品牌一致性的支持。

>[!NOTE]
>
> Forms Experience Builder在率先采用者计划下提供。 将工作地址中的电子邮件发送至`aem-forms-ea@adobe.com`以请求访问权限。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此提示词库目前正在针对产品进行测试，因此可能会进行更新和修订。随着Forms Experience Builder在率先采用者计划中的不断演变，提示、示例和最佳实践可能会发生变化。

## 使用此提示库

此库为常见的表单构建方案提供了可重用的提示模式。 有关全面的最佳实践，请参阅[Forms Experience Builder快速入门指南](forms-ai-assistant-getting-started.md#best-practices)。

### 此库的快速提示

- **以示例开始** — 将提供的提示用作模板并适应您的需求
- **两种创建方法** — 选择“从头开始创建”或“导入并转换”方法
- **具体说明** — 将您自己的详细信息添加到常规示例
- **彻底测试** — 始终验证您特定环境中的结果

### 品牌模板和样式

**提前准备品牌资产以创建一致的表单：**

- **品牌模板** — 使用您组织的颜色、字体和布局模式准备标准化表单模板
- **样式准则** — 定义Forms Experience Builder可以应用的一致字段样式、按钮设计和间距标准
- **组件库** — 与开发团队合作，准备与您的品牌标识相匹配的可重用表单组件
- **可视化Assets** — 为表单集成准备徽标、图标和背景元素

<!-- **Example Brand Application Prompt:**

    Apply our financial services brand template with:
    - Corporate blue (#003366) and silver (#C0C0C0) color scheme
    - Open Sans font family for all text
    - 16px minimum font size for accessibility
    - Consistent 24px spacing between sections
    - Corporate logo in header with proper sizing
    - Professional button styling with hover effects

>[!NOTE]
>
>**Custom Components**: Check with your development team about using organization-specific components and their compatibility with Forms Experience Builder before implementing custom brand elements.

>[!NOTE]
>
> This prompt library has been updated to reflect the streamlined Forms Experience Builder capabilities. Some advanced integration and testing features shown in examples may require additional configuration.

-->


## 逐步开发示例

这些示例展示了如何逐步构建表单，从简单开始，逐渐增加复杂性：

### 示例 1：逐步构建一个联系表单

**步骤 1 - 从简单开始：**

    创建包含姓名、电子邮件和消息字段的基本联系人表单

**步骤 2 - 添加验证：**

    使@name和@email必填字段具有适当的验证

**步骤 3 - 增强用户体验**

    添加占位符文本： @name “您的全名”、“your.email@company.com”@email以@message“告诉我们如何提供帮助”

**步骤 4 - 添加高级功能：**

    添加包含下列选项的下拉列表inquiryType：“General Question”、“Support Request”、“Sales Inquiry”、“Partnership”

**步骤 5 - 实施条件逻辑：**

仅当@inquiryType等于“支持请求”    时，
/create-rule才会显示@urgencyLevel下拉列表(下限、Medium、上限)

### 示例 2：逐步构建一个注册表单

**步骤 1- 基本结构：**

    创建包含个人信息面板的用户注册表

**第2步 — 添加必填字段：**

    添加@firstName、@lastName、@email、@phoneNumber的字段并进行适当的验证

**步骤3 — 添加业务逻辑：**

    创建规则：如果@age低于18，则显示父/监护人信息部分

**步骤4 — 使用首选项进行增强：**

    添加包含@newsletterSubscription、@marketingConsent、@termsAccepted
的首选项面板
**步骤5 — 添加文件上传：**

    包含大小限制为5MB的@profilePicture的文件上载字段

## 表单创建和管理

**何时使用：**&#x200B;需要创建新表单或修改现有表单时。

**使用方法：**&#x200B;从头开始创建或导入并转换（请参阅[入门指南](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)）。

**示例提示 — 简单表单创建：**

    创建客户反馈表，其内容为：
     — 产品评分（1-5星）
     — 详细反馈的评论字段
     — 客户电子邮件（可选）
     — 提交至电子邮件通知

**示例提示 — 复杂表单创建：**

    使用以下内容创建全面的员工入职表单：
    
    **个人信息部分：**
     — 全名（名字、中间名、姓氏）
     — 出生日期及年龄验证
     — 联系信息（电子邮件、电话、地址）
     — 紧急联系详细信息
    
    **雇佣详细信息：**
     — 职位和部门选择
     — 开始日期及工作日期验证
     — 带有保密通知的薪金信息
     — 报告结构
    
    **文档上传：**
     — 简历/简历上传(PDF、DOC、DOCX) ID验证文件
    - ID验证文件
     — 纳税表单和银行信息
     — 已签署的雇佣协议
    
    **首选项：**
     — 使用成本计算器的福利选择
     — 工作计划首选项
     — 培训要求
     — 设备需求
    
    **验证规则：**
     — 电子邮件格式验证
     — 电话号码格式验证
     — 年龄必须为18岁或以上
     — 必须上载所有必需的文件
     — 条款和条件被接受
    
    **提交操作：**
     — 向新员工发送确认电子邮件
     — 通知HR部门
     — 在HR系统中创建员工记录
     — 安排指导会议

**表单管理提示：**

    导入此PDF应用程序表单，并将其转换为具有增强型验证的自适应表单
    
    更新现有联系人表单以包含社交媒体句柄和首选联系方式
    
    将注册表单重新组织为三步向导：个人信息、首选项、确认

## 字段管理和配置

**何时使用：**&#x200B;需要添加、修改或配置表单字段时。

**使用方法：**&#x200B;具体说明字段类型、验证规则和用户体验要求。

**示例提示 — 基本字段添加：**

    为“公司名称”添加一个文本输入字段，其占位符为“输入您的公司名称”

**示例提示 — 高级字段配置：**

    添加综合地址部分，地址为：
    
    **街道地址：**
     — 地址行1（必需，最多100个字符）
     — 地址行2（可选，最多100个字符）
     — 城市（必需，包含常用城市的下拉列表）
     — 州/省（必需，下拉列表）
     — 邮政编码（必需，格式验证）
     — 国家/地区（必需，默认为“美国”）
    
    **验证规则：**
     — 邮政编码必须与州选择匹配
     — 地址行1 empty
     — 城市必须是选定州
    
    **用户体验：**
     — 自动完成地址字段
     — 清除标签和帮助文本
     — 移动友好的输入字段
     — 辅助功能合规性

**字段配置提示：**

    使@email字段为实时验证和自定义错误消息所必需
    
    添加一个下拉列表，以便@country表具有USA、Canada、UK、Germany、France和“Other”选项
    
    使用(XXX) XXX-XXXX和验证格式配置@phoneNumber字段
    
    添加一个文件上传字段，以便@resume用PDF和DOC限制，最大为5MB

## LLM增强型智能字段

**何时使用：**&#x200B;您需要具有预填充选项的字段时，这些选项将利用AI知识库。

**如何使用：**&#x200B;请求需要全面数据集的字段 — AI可以使用其内置知识自动填充选项。

### 地理和位置字段

**机场和运输：**

    添加包含所有主要国际机场的出发机场的下拉菜单
    添加包含IATA代码和全名的到达机场字段
    创建与用户位置最接近的机场的字段
    添加欧洲城市的火车站选择

**管理区域：**

    添加包含缩写的美国州的完整列表
    创建包含ISO代码和全名的国家/地区下拉列表
    添加包含时区的世界主要城市的字段
    包含加拿大省和地区的下拉列表
    添加英国县和邮政区域的字段

### 商业和行业数据

**公司分类：**

    添加具有NAICS代码的行业分类字段
    创建业务实体类型（LLC、公司、合作伙伴等）的下拉列表
    为公司规模类别（启动、SME、企业）添加字段
    包括大型组织的部门选择
    为专业服务类型添加字段

**专业分类：**

    为具有常见行业角色的职称添加字段
    按字段创建专业认证下拉列表
    包含学位类型的教育级别
    添加具有多年经验范围的字段
    为编程语言和框架创建选择

### 标准和法规

**财务和法律信息：**

    为具有符号和汇率的货币代码添加字段
    按国家/地区创建税务ID类型的下拉列表
    包括合法文档类型的字段
    添加具有安全功能的付款方法选项
    按国家/地区为银行机构创建选择项

**技术标准：**

    添加具有扩展名的文件格式类型的下拉列表
    包含网络协议选项
    添加数据库类型和版本的字段
    为API身份验证方法创建选择

### 医疗保健业

**医疗分类：**

    添加医疗专长字段
    创建具有通用名称的常用药物下拉列表
    包含保险公司类型的字段
    添加医疗紧急联系关系的选择项
    创建饮食限制和过敏字段

### 时间和日历智能

**日期和时间字段：**

    添加包含时区处理的营业时间字段
    按国家/地区创建公共假日的下拉列表
    包含日期范围的季节性选项
    添加包含可用性的会议室预订字段
    为定期会议模式创建选择

### 产品和服务类别

**电子商务分类：**

    为包含子类别的产品类别添加字段
    创建包含交货估计值的配送方式下拉列表
    包含退货政策选项字段
    添加客户优先级别选项
    创建订阅计费周期字段

**智能字段提示示例：**

    “添加一个出发机场字段，其中包含全球所有主要机场，包括IATA代码和城市名称”
    
    “使用具有技术子类别的标准NAICS分类创建一个全面的行业字段”
    
    “包含一个根据所选工作字段进行调整的专业认证下拉列表”
    
    “添加一个根据所选国家/地区设置格式的国际电话号码字段”
    
    “创建一个包含按国家/地区和排名进行组织的主要机构的大学选择字段”

## 规则创建和业务逻辑

**何时使用：**&#x200B;需要实施条件逻辑、验证规则或业务流程时。

**使用方式：**&#x200B;明确描述业务逻辑，指定条件和操作。

**示例提示 — 简单条件逻辑：**

    创建一个规则，该规则仅在@maritalStatus等于“已婚”时显示@spouseInformation面板

**示例提示 — 复杂业务规则：**

    实施全面的贷款申请验证：
    
    **收入验证：**
     — 如果@annualIncome小于30000：
     — 显示警告消息：“收入可能不足以偿还请求的贷款金额”
     — 需要其他收入文档
     — 显示消息：“可能需要其他文档”
     — 如果@annualIncome大于100000：
     — 显示高级服务选项
     — 启用优先级处理复选框
    
    **基于年龄的验证：**
     — 如果@age低于18：
     — 显示父/监护人信息部分
     — 制作强制签名上传
     — 将提交按钮文本更改为“提交以供审核”
     — 如果@age的年龄为65岁或以上：
     — 显示高级折扣选项
     — 添加辅助功能首选项部分

**规则特定的提示词：**

    创建一个&#x200B;**可见性规则**，该规则仅在@maritalStatus等于“已婚”或“家庭伙伴关系”时显示@spouseInformation面板
    
    添加&#x200B;**渐进式披露**，其中根据先前的回答显示其他问题。 从基本信息开始，然后显示相关跟进
    
    实施&#x200B;**智能默认值**，@country选择会自动设置相关字段。 允许手动覆盖

## 数据集成与提交

**何时使用：**&#x200B;当您需要将表单连接到后端系统、数据库或外部服务时。

**如何使用：**&#x200B;从基本的提交设置开始，然后逐步添加其他集成。指定集成类型、数据格式要求和错误处理偏好。

**提示词示例 - 从基本提交开始：**

    配置@applicationForm的基本表单提交：
    
    **主要提交：**
     — 将表单数据发送到REST终结点：“/api/v1/applications”
     — 将数据格式化为JSON
     — 显示成功消息：“已成功提交应用程序”
     — 如果提交失败，则显示错误消息：“提交失败，请重试”

**然后逐步添加次要操作：**

    向@applicationForm添加电子邮件通知：向@email地址发送确认电子邮件，该地址具有应用程序参考编号
    
    向@applicationForm添加CRM集成：创建具有@firstName、@lastName、@email的新潜在客户记录，并将Status设置为“New Application”

**示例提示 — 标准多渠道提交：**

    配置具有多个数据目标的表单提交：
    
    **主提交：**
     — 将表单数据发送到REST终结点：“/api/v1/applications”
     — 包含带有API密钥的身份验证标头
     — 将数据格式化为带有嵌套对象的JSON用于地址和雇佣
     — 通过显示感谢消息处理成功响应(201)
    
    **辅助操作：**
     — 将通知电子邮件发送到@email地址上的申请人
     — 将应用程序数据复制到跟踪系统
     — 触发审批流程工作流
     — 在带有潜在客户的CRM状态中创建记录“新应用程序”
    
    **错误处理：**
     — 如果主提交失败，请将数据保存在本地并重试
     — 显示用户友好的错误消息：“提交暂时不可用”
     — 提供将表单数据下载为备份的选项
     — 向管理员团队发送有关提交失败的警报电子邮件
    
    **成功流程：**
     — 重定向到具有应用程序参考编号的确认页面
     — 发送包含后续步骤的确认电子邮件
     — 显示估计的处理时间线

**集成特定的提示词：**

    将此表单连接到&#x200B;**CRM系统**&#x200B;以创建新潜在客户。 将@firstName映射到FirstName，@email映射到Email，将LeadSource设置为“Web表单”，将Status设置为“新建”
    
    在提交表单时设置&#x200B;**工作流触发器**。 通过经理通知
    
    配置&#x200B;**数据库集成**&#x200B;传递所有表单数据并触发审批工作流，以将表单提交另存为记录。 为上载文档的每个提交创建新文件夹

<!-- ## Import & Convert Existing Forms

**When to use:** When you have existing forms, documents, or designs to transform into modern AEM forms.

**How to use:** Upload your source file and describe the conversion requirements (see [Import Guide](forms-ai-assistant-getting-started.md#2-import-and-convert)).


**Design Import Prompts:**

    Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness

    Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields

    Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes

## Mobile Optimization & Responsiveness

**When to use:** When forms need to work seamlessly across all device types and screen sizes.

**How to use:** Start with basic mobile optimization, then enhance with advanced features. Emphasize mobile-first approach and specify breakpoint behaviors incrementally.

**Example Prompt - Start with Basic Mobile Optimization:**

    Make @contactForm mobile-friendly with:
    
    **Basic Mobile Layout:**
    - Single column layout for all form sections
    - Larger touch targets for buttons and inputs
    - Responsive design that works on phones and tablets

**Then Add Advanced Mobile Features:**

    Enhance @contactForm mobile experience with:
    - Sticky submit button at bottom of screen
    - Touch-friendly date pickers
    - Swipe gestures for multi-step navigation

**Example Prompt - Comprehensive Mobile-First Optimization:**

    Optimize this form for **mobile-first responsive design**:
    
    **Mobile Layout (320px - 768px):**
    - Single column layout for all form sections
    - Larger touch targets (minimum 44px height)
    - Simplified navigation with collapsible sections
    - Sticky submit button at bottom of screen
    - Auto-zoom disabled on input focus
    
    **Tablet Layout (768px - 1024px):**
    - Two-column layout for shorter fields (name, email)
    - Single column for complex fields (address, comments)
    - Side navigation for multi-step forms
    - Optimized for both portrait and landscape
    
    **Desktop Layout (1024px+):**
    - Multi-column layouts where appropriate
    - Horizontal form sections for related fields
    - Sidebar navigation for long forms
    - Hover states and advanced interactions

**Mobile-Specific Prompts:**

    Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users

    Optimize form for **tablet users** with appropriate field sizes and navigation patterns

    Add **swipe gestures** for multi-step form navigation on mobile devices

## Accessibility & Compliance

**When to use:** When forms need to meet accessibility standards (WCAG) or compliance requirements.

**How to use:** Specify the required compliance level and any specific accessibility features needed.

**Example Prompt - Basic Accessibility:**

    Make @contactForm accessible with:
    
    **Basic Accessibility:**
    - Proper ARIA labels for all form fields
    - Keyboard navigation support
    - High contrast color scheme
    - Screen reader compatibility
    - Focus indicators for all interactive elements

**Example Prompt - Advanced Accessibility:**

    Implement comprehensive accessibility for @applicationForm:
    
    **WCAG 2.1 AA Compliance:**
    
    - Semantic HTML structure with proper headings
    - ARIA landmarks and roles for navigation
    - Color contrast ratio of at least 4.5:1
    - Keyboard-only navigation support
    - Screen reader announcements for dynamic content
    
    **Form-Specific Accessibility:**
    
    - Error messages announced to screen readers
    - Field validation with clear error descriptions
    - Progress indicators for multi-step forms
    - Skip navigation links for keyboard users
    - Alternative text for all images and icons
    
    **User Experience:**
    
    - Clear focus indicators on all interactive elements
    - Logical tab order through form fields
    - Descriptive link text and button labels
    - Help text available for complex fields
    - Timeout warnings for session expiration

**Accessibility-Specific Prompts:**

    Add **screen reader support** to this form with proper ARIA labels and announcements

    Implement **keyboard navigation** for all form interactions and navigation elements

    Ensure **color contrast** meets WCAG AA standards for all text and interactive elements  

## Performance Optimization

**When to use:** When forms need to load quickly and perform well under various conditions.

**How to use:** Specify performance requirements and optimization strategies.

**Example Prompt - Basic Performance:**

    
Optimize @contactForm for performance:

**Loading Optimization:**

- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
    

**Example Prompt - Advanced Performance:**

    
Implement comprehensive performance optimization for @applicationForm:

**Loading Performance:**

- Progressive loading of form sections
- Optimize images with WebP format
- Minimize JavaScript bundle size
- Enable gzip compression for all assets

**Runtime Performance:**

- Debounce validation calls to reduce API requests
- Optimize conditional logic execution
- Cache frequently used data
- Implement virtual scrolling for long lists

**User Experience:**

- Show loading indicators for async operations
- Provide offline capability for form data
- Auto-save form progress every 30 seconds
- Optimize form submission with retry logic

**Monitoring:**

- Track form load times and user interactions
- Monitor validation performance
- Measure submission success rates
- Alert on performance degradation
    

**Performance-Specific Prompts:**

    
Optimize form **loading speed** by implementing progressive loading and asset optimization
    

    
Add **auto-save functionality** to prevent data loss during form completion
    

    
Implement **offline support** so users can complete forms without internet connection
    

## Testing & Quality Assurance

**When to use:** When forms need comprehensive testing to ensure reliability and user satisfaction.

**How to use:** Specify testing scenarios, validation requirements, and quality metrics.

**Example Prompt - Basic Testing:**

    
Add comprehensive testing for @contactForm:

**Functional Testing:**

- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
    

**Example Prompt - Advanced Testing:**

    
Implement comprehensive testing strategy for @applicationForm:

**Functional Testing:**

- Unit tests for all validation rules
- Integration tests for submit actions
- End-to-end testing for complete user flows
- Cross-browser compatibility testing

**User Experience Testing:**

- Usability testing with target user groups
- Accessibility testing with screen readers
- Mobile device testing on various screen sizes
- Performance testing under load conditions

**Quality Assurance:**

- Automated testing for regression prevention
- Manual testing for edge cases and scenarios
- Security testing for data protection
- Compliance testing for regulatory requirements

**Monitoring:**

- Track form completion rates and abandonment
- Monitor error rates and user feedback
- Measure performance metrics and load times
- Analyze user behavior and interaction patterns
    

**Testing-Specific Prompts:**

    
Add **automated testing** for all form validations and submit functionality
    

    
Implement **user acceptance testing** scenarios for complete form workflows
    

    
Set up **performance monitoring** to track form load times and user interactions
    
-->

## 命令引用

### 基本命令

| 命令 | 最佳用例 | 示例 |
|---------|---------------|---------|
| `/create-form` | 开始构建新表单 | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | 将表单添加到页面 | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | 改变表单结构 | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | 更改字段属性 | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | 添加动态行为 | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | 组织表单部分 | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | 转换设计 | `/add-panel from uploaded form image with field recognition` |
| `/help` | 获取帮助 | `/help how to implement multi-step validation?` |

### 字段引用

使用`@fieldName`语法引用提示中的现有字段：

- `@email` — 引用电子邮件字段
- `@firstName` — 引用名字字段
- `@maritalStatus` — 参考婚姻状况字段

### 组件类型

**输入组件：**

- `text`，`email`，`number`，`tel`，`date`，`checkbox`，`radio`，`dropdown`，`file`，`textarea`

**容器组件：**

- `fieldset`，`panel`，`repeatable`，`wizard`

### 组件属性

**通用属性（所有组件）：**

- **类型**：组件类型
- **名称**：表单提交的字段标识符
- **标签**：显示字段的文本
- **描述**：字段的帮助文本
- **可视**：表示初始可见性的布尔值
- **必填**：表示必填字段的布尔值

**输入字段属性：**

- **值**：默认/初始值
- **占位符**：输入字段的提示文本
- **Min**：最小值（数字/日期）
- **Max**：最大值（数字/日期）

**文件上载属性：**

- **接受**：文件类型（.pdf、.doc、.docx、.jpg、.png 等）
- **Multiple**：用于选择多个文件的布尔值

**选择控件属性：**

- **选项**：下拉菜单的选项（逗号分隔的列表）
- **已选中**：复选框/单选框的默认选择

**容器属性：**

- **Fieldset**：对相关字段进行分组
- **可重复**：可重复部分的布尔值

**高级属性：**

- **可见表达式**：条件可见性的公式（=公式）
- **值表达式**：计算值的公式（=公式）

### 集成命令

**提交操作：**

- 电子邮件通知
- REST API提交
- 云存储(Azure、SharePoint)
- 工作流自动化(Power Automate、Workfront Fusion)
- 营销平台(Marketo)
- CRM集成

### 提示语法准则

- **字段引用**：将`@fieldName`用于现有字段
- **命令**：将`/command`用于特定操作
- **自然语言**：清晰明确地描述要求

### 验证核对清单

有关全面的最佳实践和验证准则，请参阅[Forms Experience Builder快速入门指南](forms-ai-assistant-getting-started.md#best-practices)。

*此提示库会根据用户反馈和新的Forms Experience Builder功能不断更新。 如需了解最新功能和示例，请查看 [AEM Forms 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=zh-Hans)。*
