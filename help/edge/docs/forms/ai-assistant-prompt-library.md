---
title: AEM Forms AI 助手 - 提示词库
description: 收集经过验证的提示词模式和示例，用于在表单管理用户界面、自适应表单编辑器和通用编辑器中使用 AI 辅助构建表单。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 333d42e0-625f-432e-a61b-5d49bf08765a
source-git-commit: abcd5be06b0bf24ebe8737827fb4abdbf148b1b0
workflow-type: ht
source-wordcount: '1613'
ht-degree: 100%

---

# AEM Forms AI 助手 - 提示词库

收集可重复使用的提示词模式和常见表单构建场景的示例。将它们视为可以根据您的特定需求进行调整的模板。每个部分都涵盖了一个特定的用例，并提供了何时使用该用例的指导以及经过验证的示例。

>[!NOTE]
>
> AEM Forms 的 AI 助手可在早期采用者计划中使用。请使用您的工作邮箱发送邮件至 mailto:aem-forms-ea@adobe.com，以申请访问权限。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此提示词库目前正在针对产品进行测试，因此可能会进行更新和修订。随着 AEM Forms 的 AI 助手在早期采用者计划期间不断发展，提示词、示例和最佳实践可能会发生变化。

## 获得最佳结果的最佳实践

为了充分利用 AI 助手，请考虑以下建议：

### 从简单开始，逐步构建

一开始先从较小的具体的命令开始（例如，“添加一个‘名字’的文本输入框”），而不是一开始就提出过于复杂的多步骤请求。这种方法有助于确保准确性，并在出现异常情况时更便于修改错误。

**简单开始的示例：**

```
Add a text input field for "First Name" with placeholder "Enter your first name"
```

**然后逐步构建：**

```
Make @firstName mandatory and add validation message "First name is mandatory"
```

### 使用 AEM Forms 术语

使用“面板”、“文本输入字段”、“复选框组”、“提交操作”、“规则”等术语，以便助手更好地理解。这可确保 AI 在 AEM Forms 上下文中正确理解您的请求。

**首选术语：**

- “文本输入字段”而不是“文本框”
- “复选框组”而不是“多个复选框”
- “下拉列表”而不是“选择列表”
- “面板”而不是“部分”或“容器”
- “提交操作”而不是“表单提交”
- “规则”而不是“逻辑”或“条件”

### 明确引用字段

在配置现有字段时，请使用 @firstName 符号（例如，“将 @firstName 设为必填”）。这有助于 AI 准确识别您所指的字段，尤其是在包含许多字段的复杂表单中。

**示例：**

- `Make @email mandatory with real-time validation`
- `Show @spouseInfo panel when @maritalStatus equals "Married"`
- `Set @country default value to "United States"`

### 务必审阅计划

在点击“应用”之前，请务必仔细审阅通用编辑器中的助手提出的更改建议。AI 助手会显示它的更改计划——请花点时间确认这是否符合您的期望。

### 手动验证

助手完成更改后，请务必预览并测试表单，以确保其功能和外观均符合预期。人工智能是一个强大的工具，但最终验证是确保质量的关键。

**验证清单：**

- 在预览模式下测试表单功能
- 验证条件逻辑是否工作正常
- 检查移动端响应能力
- 测试表单提交
- 验证无障碍访问功能

### 迭代和优化

如果第一个提示词没有产生准确的结果，请尝试重新措辞或将请求分解为几个更小的步骤。人工智能会从上下文中学习，因此提供更具体的细节通常可以改善结果。

**迭代示例：**

1. 第一次尝试：“使表单适合在移动设备上使用”
2. 优化：“针对 768px 以下的移动设备屏幕优化表单布局，采用单栏布局和较大的触摸目标”

### 提供反馈

使用内置的反馈机制帮助助手学习和改进。您的反馈有助于让 AI 更好地为每个人服务。


## 逐步开发示例

这些示例展示了如何逐步构建表单，从简单开始，逐渐增加复杂性：

### 示例 1：逐步构建一个联系表单

**步骤 1 - 从简单开始：**

```
Create a basic contact form with name, email, and message fields
```

**步骤 2 - 添加验证：**

```
Make @name and @email mandatory fields with appropriate validation
```

**步骤 3 - 增强用户体验**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**步骤 4 - 添加高级功能：**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**步骤 5 - 实施条件逻辑：**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### 示例 2：逐步构建一个注册表单

**步骤 1- 基本结构：**

```
Create a user registration form with personal information panel
```

**步骤 2 - 添加核心字段：**

```
Add text input fields: @firstName, @lastName, @email, @phone to the personal information panel
```

**步骤 3 - 添加验证：**

```
Make @firstName, @lastName, and @email mandatory with real-time validation
```

**步骤 4 - 添加帐户信息：**

```
Create a new panel "Account Information" with @username and @password fields
```

**步骤 5 - 增强安全性：**

```
Add password confirmation field @confirmPassword with validation to match @password
```

**步骤 6 - 添加首选项：**

```
Create "Preferences" panel with @newsletter checkbox and @communicationMethod radio group (Email, SMS, Phone)
```

这种渐进式方法可以帮助您：

- 在问题变得严重之前及早发现并解决
- 对每个功能进行全面测试
- 根据用户反馈进行调整
- 更好地控制开发过程

## 开始构建新表单

**何时使用：**&#x200B;在任何表单项目开始时。该提示词可以帮助 AI 了解您的要求并构建基础结构。

**如何使用：**&#x200B;从基本结构和核心要求开始。指定表单类型、目标受众和主要目的。在后续提示词中增加复杂性。

**提示词示例 - 从简单开始：**

```
Create a **customer onboarding form** for new bank account applications with:

**Purpose:** Collect personal information for account setup
**Target Users:** New customers applying for checking/savings accounts
**Basic Structure:** Single panel with essential fields
**Core Fields:** Name, email, phone, account type selection

Start with a simple layout that we can enhance step by step.
```

**然后逐步构建：**

```
Add an address panel to @customerOnboardingForm with street address, city, state, and zip code fields
```

```
Add employment information panel with @employer, @jobTitle, and @annualIncome fields
```

```
Add file upload field @identityDocuments for identity verification (Accept: .pdf,.jpg,.png)
```

**其他简单的开始提示词：**

```
Create a basic **event registration form** with name, email, and event selection fields
```

```
Build a simple **contact form** with name, email, and message fields
```

```
Design a basic **feedback survey** with rating scale and comments field
```

## 表单结构和布局

**何时使用：**&#x200B;当您需要组织多个复杂的表单或通过更好的布局设计来提升用户体验时。

**如何使用：**&#x200B;关注用户历程和信息的逻辑分组。指定布局偏好和导航模式。

**提示词示例 - 多步骤表单结构：**

```
Convert this single-page form into a **3-step wizard** with:

**Step 1: Personal Information**
- Name, email, phone, address fields
- Progress indicator showing "Step 1 of 3"
- "Next" button (validate mandatory fields before proceeding)

**Step 2: Preferences & Requirements** 
- Service selection (checkbox group)
- Budget range (dropdown)
- Timeline preferences (radio group)
- Special requirements (text input field)

**Step 3: Review & Submit**
- Summary of all entered information
- Edit links to go back to specific steps
- Terms and conditions checkbox
- Submit button with confirmation

Include "Previous" and "Next" buttons, allow users to jump between completed steps, save progress automatically.
```

**布局优化提示词：**

```
Reorganize this form using a **wizard layout** for desktop and single column for mobile. 
```

```
Convert this long form into an **accordion layout** where users can expand/collapse sections.
```

```
Create a **vertical tabbed interface** for this form with tabs for: Basic Info, Contact Details, Preferences, and Review.
```

## 字段管理与验证

**何时使用：**&#x200B;当您需要添加、更改或增强具有特定验证规则和行为的表单字段时。

**如何使用：**&#x200B;明确说明字段类型、验证要求以及用户体验预期。使用 @fileName 语法引用现有字段。

**提示词示例 - 增强字段：**

```
Enhance the form fields with these specific requirements:

**Email Field (@email):**
- Make mandatory with real-time validation
- Show green checkmark when valid format entered
- Display helpful error message: "Please enter a valid email address"
- Add placeholder: "your.email@company.com"

**Phone Number (@phone):**
- Type: tel for mobile optimization
- Make mandatory for business customers, optional for personal
- Add placeholder: "Enter your phone number"

**Date of Birth (@dateOfBirth):**
- Type: date with date picker
- Validate age is 18+ for account opening
- Show error if under 18: "Must be 18 or older to open account"

**File Upload (@documents):**
- Accept: .pdf,.doc,.docx
- Multiple: true for multiple document upload
- Show upload progress and file names after upload
```

**字段特定的提示词：**

```
Add a **file upload field** for resume with these specs: Accept only PDF/DOC/DOCX files, allow multiple files, show upload progress, display file names after upload.
```

```
Create a **dropdown field** for country selection with all countries listed. Set default value based on user's location if available.
```

```
Build a **repeatable panel** for work experience where users can add/remove multiple jobs. Each entry needs: company, title, start date, end date, description.
```

## 条件逻辑和规则

**何时使用：**&#x200B;当您需要根据用户输入或业务规则实现动态表单行为时。

**如何使用：**&#x200B;明确定义条件和由此产生的行动。使用特定字段引用和逻辑运算符。

**提示词示例 - 复杂条件逻辑：**

```
Implement these conditional rules for the application form:

**Business vs Personal Account Logic:**
- If @accountType equals "Business", show:
  - Business name field (mandatory)
  - Tax ID field (mandatory)
  - Business address section
  - Number of employees dropdown
- If @accountType equals "Personal", hide all business fields

**Income-Based Requirements:**
- If @annualIncome is less than 25000:
  - Show additional verification section
  - Make co-signer information mandatory
  - Display message: "Additional documentation may be required"
- If @annualIncome is greater than 100000:
  - Show premium services options
  - Enable priority processing checkbox

**Age-Based Validation:**
- If @age is under 18:
  - Show parent/guardian information section
  - Make parent signature upload mandatory
  - Change submit button text to "Submit for Review"
- If @age is 65 or older:
  - Show senior discount options
  - Add accessibility preferences section
```

**规则特定的提示词：**

```
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership".
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups.
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override.
```

## 数据集成与提交

**何时使用：**&#x200B;当您需要将表单连接到后端系统、数据库或外部服务时。

**如何使用：**&#x200B;从基本的提交设置开始，然后逐步添加其他集成。指定集成类型、数据格式要求和错误处理偏好。

**提示词示例 - 从基本提交开始：**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**然后逐步添加次要操作：**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**提示词示例 - 高级多渠道提交：**

```
Configure form submission with multiple data destinations:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Include authentication header with API key
- Format data as JSON with nested objects for address and employment
- Handle success response (201) by showing thank you message

**Secondary Actions:**
- Send notification email to applicant at @email address
- Copy application data to tracking system
- Trigger workflow for approval process
- Create record in CRM with lead status "New Application"

**Error Handling:**
- If primary submission fails, save data locally and retry
- Show user-friendly error message: "Submission temporarily unavailable"
- Provide option to download form data as backup
- Send alert email to admin team about failed submission

**Success Flow:**
- Redirect to confirmation page with application reference number
- Send confirmation email with next steps
- Display estimated processing timeline
```

**集成特定的提示词：**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New".
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification.
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents.
```

## 设计导入和转化

**何时使用：**&#x200B;当您需要将现有的表单设计（PDF、Figma、图像）转换为功能性的 AEM 表单时。

**如何使用：**&#x200B;提供关于源设计的清晰背景，并明确说明所需的任何修改或改进。

**提示词示例 - PDF 表单转化：**

```
Convert this uploaded **PDF application form** into a functional AEM adaptive form:

**Source Analysis:**
- Analyze the PDF layout and identify all form fields
- Preserve the visual hierarchy and grouping
- Maintain the professional appearance and branding

**Field Mapping:**
- Convert PDF text fields to adaptive form text inputs
- Transform checkboxes to checkbox components
- Convert dropdown lists to AEM dropdown components
- Map signature areas to digital signature fields

**Enhancements:**
- Add real-time validation that wasn't possible in PDF
- Implement conditional logic for dependent fields
- Make the form responsive for mobile devices
- Add progress saving capability
- Include accessibility improvements (ARIA labels, keyboard navigation)

**Styling:**
- Match the original color scheme and fonts
- Maintain professional business appearance
- Ensure consistent spacing and alignment
- Add subtle animations for better user experience

Preserve all original field labels and help text, but improve the user experience with modern form interactions.
```

**设计导入提示词：**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness.
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields.
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes.
```

## 移动端优化与响应能力

**何时使用：**&#x200B;当表单需要在所有设备类型和屏幕尺寸上无缝工作时。

**如何使用：**&#x200B;从基本的移动端优化开始，然后通过高级功能将其增强。强调移动端优先的方法，逐步指定断点行为。

**提示词示例 - 从基本的移动端优化开始：**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**然后添加高级移动端功能：**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**提示词示例 - 全面的移动端优先优化：**

```
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

**Touch Optimization:**
- Larger checkbox and radio button targets
- Swipe gestures for multi-step navigation
- Pull-to-refresh for saved drafts
- Touch-friendly date/time pickers

**Performance:**
- Lazy load non-critical form sections
- Optimize images and icons for mobile
- Minimize JavaScript for faster loading
- Progressive enhancement approach
```

**移动设备特定的简单提示词：**

```
Make @checkoutForm mobile-optimized with large buttons and one-thumb navigation
```

```
Add touch-friendly controls to @surveyForm for tablet users
```

```
Enable offline functionality for @applicationForm with local data saving
```

## 无障碍访问和合规性

**何时使用：**&#x200B;表单必须符合无障碍访问标准（WCAG 2.1 AA）或合规性要求。

**如何使用：**&#x200B;指定必须满足的无障碍访问要求和合规标准。

**提示词示例 - 无障碍访问实施：**

```
Make this form **WCAG 2.1 AA compliant** with these accessibility features:

**Keyboard Navigation:**
- Logical tab order through all form elements
- Skip links to main content and form sections
- Keyboard shortcuts for common actions
- Focus indicators clearly visible on all interactive elements

**Screen Reader Support:**
- Proper ARIA labels for all form fields
- Descriptive error messages announced to screen readers
- Form section headings with proper hierarchy (h1, h2, h3)
- Progress announcements for multi-step forms

**Visual Accessibility:**
- Color contrast ratio minimum 4.5:1 for text
- Don't rely solely on color to convey information
- Text size minimum 16px for body text
- Scalable up to 200% without horizontal scrolling

**Motor Accessibility:**
- Large click targets (minimum 44x44px)
- Generous spacing between interactive elements
- No time limits or provide extension options
- Alternative input methods support

**Cognitive Accessibility:**
- Clear, simple language in all instructions
- Consistent navigation and layout patterns
- Error prevention and clear error recovery
- Help text and examples for complex fields

**Testing Requirements:**
- Test with screen readers (NVDA, JAWS, VoiceOver)
- Verify keyboard-only navigation
- Check color contrast with automated tools
- Validate HTML for semantic correctness
```

**合规性特定的提示词：**

```
Ensure this **healthcare form meets HIPAA requirements** with proper data encryption, audit logging, and privacy controls.
```

```
Make this **financial form PCI DSS compliant** with secure payment field handling and data protection measures.
```

```
Create a **government form meeting Section 508 standards** with full accessibility and plain language requirements.
```

## 测试和质量保证

**何时使用：**&#x200B;当您需要验证表单功能、用户体验和技术性能时。

**如何使用：**&#x200B;指定必须验证的测试场景、边缘情况和质量标准。

**提示词示例 - 综合表单测试：**

```
Create a **comprehensive testing plan** for this application form:

**Functional Testing:**
- Test all field validations with valid and invalid data
- Verify conditional logic shows/hides fields correctly
- Test file upload with various file types and sizes
- Validate calculation fields update correctly
- Test form submission with complete and incomplete data

**User Experience Testing:**
- Test form completion time (target: under 10 minutes)
- Verify error messages are helpful and actionable
- Test progress saving and restoration
- Validate mobile touch interactions
- Check form accessibility with assistive technologies

**Edge Case Testing:**
- Test with extremely long text inputs
- Verify behavior with special characters and emojis
- Test with slow internet connections
- Validate offline functionality if applicable
- Test browser back/forward button behavior

**Performance Testing:**
- Measure form load time (target: under 3 seconds)
- Test with large file uploads
- Verify memory usage with long form sessions
- Test concurrent user submissions
- Validate database performance under load

**Security Testing:**
- Test input sanitization and XSS prevention
- Verify CSRF protection is working
- Test file upload security restrictions
- Validate data encryption in transit and at rest
- Check authentication and authorization controls

**Cross-Browser Testing:**
- Test on Chrome, Firefox, Safari, Edge
- Verify mobile browsers (iOS Safari, Chrome Mobile)
- Test on different operating systems
- Validate older browser fallbacks
- Check print functionality across browsers
```

**测试特定的提示词：**

```
Create **automated test scripts** for this form's critical user paths: successful submission, validation errors, and conditional logic.
```

```
Design a **user acceptance testing plan** with realistic scenarios and success criteria for business stakeholders.
```

```
Set up **performance monitoring** to track form completion rates, abandonment points, and submission success rates.
```

## 高级功能和集成

**何时使用：**&#x200B;当您需要复杂的表单功能时，如 AI 辅助、高级工作流或复杂集成。

**如何使用：**&#x200B;明确定义高级功能和集成要求。

**提示词示例 - AI 增强表单：**

```
Add **AI-powered features** to enhance this application form:

**Smart Auto-Complete:**
- Use AI to suggest company names as user types
- Auto-populate address fields from partial input
- Suggest job titles based on industry selection
- Provide intelligent form completion suggestions

**Dynamic Question Generation:**
- Generate follow-up questions based on previous answers
- Adapt form complexity to user's experience level
- Show relevant optional fields based on user profile
- Personalize form sections for different user types

**Intelligent Validation:**
- Use AI to detect potentially incorrect information
- Suggest corrections for common data entry errors
- Validate business information against public databases
- Flag suspicious or inconsistent responses

**Content Optimization:**
- A/B test different form layouts automatically
- Optimize field order based on completion patterns
- Adjust form length based on user engagement
- Personalize help text based on user behavior

**Predictive Analytics:**
- Predict likelihood of form completion
- Identify users who might need assistance
- Suggest optimal times for form completion reminders
- Analyze drop-off points and suggest improvements

**Natural Language Processing:**
- Allow voice input for text fields
- Convert speech to text for accessibility
- Analyze open-text responses for sentiment
- Extract structured data from unstructured input
```

**高级集成提示词：**

```
Integrate with **CRM system** to pre-populate known customer data, update records in real-time, and trigger automated follow-up sequences.
```

```
Connect to **payment gateway** for secure transaction processing with PCI compliance, fraud detection, and multiple payment methods.
```

```
Implement **blockchain verification** for document authenticity, immutable audit trails, and decentralized identity verification.
```

## 错误修改和优化

**何时使用：**&#x200B;当表单存在性能问题、用户体验问题或技术难题时。

**如何使用：**&#x200B;清晰描述具体的问题和期望的结果。

**提示词示例 - 性能优化：**

```
Optimize this form for **better performance and user experience**:

**Current Issues:**
- Form takes 8+ seconds to load on mobile
- Users are abandoning at the address section (60% drop-off)
- File uploads frequently fail or timeout
- Validation errors are confusing users

**Performance Improvements:**
- Implement lazy loading for non-critical form sections
- Optimize images and reduce bundle size
- Add progressive loading indicators
- Cache frequently used data (country lists, etc.)
- Minimize JavaScript execution time

**User Experience Fixes:**
- Simplify the address section with auto-complete
- Add inline validation with helpful error messages
- Implement smart defaults based on user location
- Add progress saving every 30 seconds
- Provide clear instructions for each section

**Technical Optimizations:**
- Implement chunked file uploads with resume capability
- Add client-side validation before server submission
- Optimize database queries for faster responses
- Implement proper error handling and retry logic
- Add comprehensive logging for debugging

**Monitoring & Analytics:**
- Set up form analytics to track user behavior
- Monitor completion rates by section
- Track error rates and types
- Measure performance metrics continuously
- A/B test improvements with real users
```

**错误修改提示词：**

```
**Debug this form submission error:** Users report getting "500 Internal Server Error" when submitting. Check validation logic, server endpoints, and data formatting.
```

```
**Fix mobile layout issues:** Form fields are overlapping on iPhone screens and submit button is not visible. Ensure proper responsive design.
```

```
**Resolve validation conflicts:** Some users can't submit even with valid data. Review validation rules for conflicts and edge cases.
```

## 环境特定的最佳实践

### 表单管理用户界面

**何时使用：**&#x200B;用于高级表单创建和管理任务。

```
In Forms Management UI, create a new **customer survey template** that can be reused across different departments. Include standard branding, common field types, and configurable sections.
```

### 自适应表单编辑器

**何时使用：**&#x200B;用于详细的表单配置和复杂的规则创建。

```
In the Adaptive Forms Editor, configure **advanced business rules** for this loan application: calculate debt-to-income ratio, determine eligibility, and show appropriate next steps.
```

### 通用编辑器

**何时使用：**&#x200B;适用于具有可视化编辑功能的 Edge Delivery Services 表单。

```
In Universal Editor, create a **responsive contact form** for the company website. Ensure it matches the site design and integrates with the existing content management workflow.
```

## 命令参考快速指南

| 命令 | 最佳用例 | 示例 |
|---------|---------------|---------|
| `/create-form` | 开始构建新表单 | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | 将表单添加到页面 | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | 改变表单结构 | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | 更改字段属性 | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | 添加动态行为 | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | 组织表单部分 | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | 转换设计 | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | 设置数据处理 | `/configure-submit to CRM and send confirmation email` |
| `/help` | 获取帮助 | `/help how to implement multi-step validation?` |

## 支持的组件属性参考

### 通用属性（所有组件）

- **类型**：组件类型（文本、电子邮件、数字、电话、日期、复选框、单选按钮、下拉菜单、文件等）
- **名称**：表单提交的字段标识符
- **标签**：显示字段的文本
- **描述**：字段的帮助文本
- **可视**：表示初始可见性的布尔值
- **必填**：表示必填字段的布尔值

### 输入字段属性

- **值**：默认/初始值
- **占位符**：输入字段的提示文本
- **Min**：最小值（数字/日期）
- **Max**：最大值（数字/日期）

### 文件上传属性

- **接受**：文件类型（.pdf、.doc、.docx、.jpg、.png 等）
- **Multiple**：用于选择多个文件的布尔值

### 选择控制属性

- **选项**：下拉菜单的选项（逗号分隔的列表）
- **已选中**：复选框/单选框的默认选择

### 容器属性

- **Fieldset**：对相关字段进行分组
- **可重复**：可重复部分的布尔值

### 高级属性

- **可见表达式**：条件可见性的公式（=公式）
- **值表达式**：计算值的公式（=公式）

## 最佳实践摘要

### 技术指南

- **仅使用官方 AEM 表单组件规范中支持的属性**
- **遵循字段引用 (@fieldName) 和表达式 (=formula) 的正确语法** 
- **每次变更后**&#x200B;进行逐步测试，以便及早发现问题
- **从一开始就考虑无障碍访问**，而非事后补救
- **在每一个设计决策中考虑移动端用户** 
- **记录复杂的规则**，以便于未来维护和团队协作

### 战略方法

- **从用户需求入手** - 关注用户需要完成的任务，而不仅仅是技术特性
- **为完成表单而设计** - 在表单设计中尽量减少摩擦和认知负荷
- **尽早规划数据流** - 考虑如何处理、存储和使用数据
- **为规模化而构建** - 设计能够应对预期用户量和数据增长的表单
- **实现渐进式增强功能** - 确保基本功能正常运作，再添加高级功能

### 需要避免的常见陷阱

- **过于复杂的初始请求** - 将大型任务分解为多个更小、更易于管理的步骤
- **使用 AEM Forms 规范中不受支持的属性**
- **在开发过程的后期才考虑移动端体验**
- **跳过真实场景和边缘情况的用户测试**
- **假设人工智能无需提供明确、具体的指令就能理解上下文** 
- **忽略无障碍访问**&#x200B;和合规性要求
- **在进入下一步之前未验证更改** 

### 质量保证方法

1. **经常预览** - 每次做出重大更改后，在预览模式下进行检查
2. **测试边缘情况** - 尝试输入不常见的内容、长文本、特殊字符
3. **跨设备验证** - 在移动设备、平板电脑和桌面设备上进行测试
4. **检查无障碍访问** - 验证键盘导航和屏幕阅读器兼容性
5. **性能测试** - 确保表单快速加载并顺畅响应
6. **用户验收测试** - 部署前让真实用户测试表单


*此提示词库会根据用户反馈和新的 AI 助手功能不断更新。如需了解最新功能和示例，请查看 [AEM Forms 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=zh-Hans)。*
