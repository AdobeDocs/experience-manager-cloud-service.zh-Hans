---
title: 如何在预览或发布实例上发布或取消发布表单？
description: 了解如何从AEM创作环境发布或取消发布表单以预览或发布实例。 无论您是在暂存环境中测试表单，还是为最终用户实时部署表单，AEM都提供了简化的工具来高效地管理此过程。
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, manage publication, , AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: 242dcbc5bb541dfac601454fb75dec3bdff1ea64
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---


# 在Experience Manager Forms中&#x200B;管理发布

作为Adobe Experience Manager Forms管理员，您可以将表单从创作实例发布到Experience Manager Forms。 您可以计划在稍后的日期或时间发布表单或文件夹。 发布后，用户可以访问和填写表单。

您可以使用Experience Manager Forms界面中的Publish或“管理发布”选项来发布或取消发布表单。 如果您随后在Experience Manager Forms中对原始表单或文件夹进行了修改，则在从Experience Manager Forms重新发布之前，这些更改不会反映在发布实例中。 它可确保进行中的更改在发布实例中不可用。 发布实例中只能使用管理员发布的更改。

## 使用Publish的Publish表单选项

利用发布选项，可立即发布表单。 在Experience Manager Forms控制台中，导航到父文件夹，然后选择要发布的表单。 单击工具栏中的Publish选项，查看将随表单一起发布的所有参考资源，然后单击Publish。

计算机屏幕截图

自动生成描述

## 使用管理发布Publish或取消发布表单


管理发布允许您向所选目标发布内容或从中取消发布内容，跨表单和文档文件夹向发布列表添加内容，选择要发布的引用，以及安排发布到晚一点的日期或时间。


在Experience Manager Forms控制台中，导航到父文件夹，然后选择要发布的表单。 单击工具栏中的管理发布选项。


计算机屏幕截图

自动生成描述



“管理发布”界面中有以下选项：

* 操作

   * Publish：将Publish表单发送到选定的目标
   * 取消发布：从目标取消发布表单

* 目标

   * Publish： Publish forms到Experience Manager Forms (AEM) Publish的实例。
   * 预览： Publish forms到Experience Manager Forms (AEM)的预览实例。

* 正在计划

   * 现在：Publish表单立即
   * 以后：根据激活日期或时间的Publish表单



若要继续，请单击&#x200B;**下一步**。 在“范围”选项卡中，使用“添加内容”选项可添加更多用于发布的内容。 例如，您可以添加更多Forms或记录文档文件。

### 添加内容

将发布到Experience Manager Forms允许您进一步向发布列表添加更多内容（表单、资源和文件夹）。 您可以从formsanddocuments文件夹向列表添加更多表单、资源或文件夹。 但是，您无法一次从多个文件夹添加资源。

计算机屏幕截图

自动生成描述

单击“**添加内容**”按钮可添加更多内容。 您可以从一个文件夹添加多个资源，也可以一次添加多个文件夹。 但是，您无法一次从多个文件夹添加资源。

要将引用配置为发布或不发布表单或其他资产，请选择该表单或资产，然后单击已发布引用。

计算机屏幕截图

自动生成描述

在已发布引用对话框中，取消选中您计划不发布的资产，然后单击完成。


计算机屏幕截图

自动生成描述


## Publish或稍后取消发布表单


除了允许您在以后的日期和时间发布或取消发布表单外，发布或取消发布选项还允许您配置工作流。 完成工作流后，将发布或取消发布表单。 要计划表单以供发布或取消发布，请执行以下操作：

1. 在Experience Manager Forms控制台中，导航到父文件夹，然后选择要计划发布的表单。
1. 单击工具栏中的管理发布选项。
1. 单击Publish或“从操作中取消发布”，然后选择要发布或取消发布内容的目标。

   * 预览：使用“预览”选项可发布或取消发布到Experience Manager Forms预览环境。 Experience Manager Forms预览环境用于测试开发表单。
   * Publish：使用Experience Manager Forms Publish选项可在表单准备好用于生产环境后将表单发送到Experience Manager Forms发布环境。


1. 在计划中选择稍后。

1. 选择激活日期并指定日期和时间。 单击“下一步”。

   计算机屏幕截图

   自动生成描述

1. 在范围选项卡中，添加内容（如有必要）。 单击“下一步”。

   计算机屏幕截图

   自动生成描述

1，（可选）在工作流选项卡中，指定工作流标题。 稍后单击Publish。

计算机屏幕截图

自动生成描述

## 确定发布状态

可通过多种方法确定发布状态：

* 登录到目标实例以验证发布的表单和其他资源（取决于计划的日期或时间）。

* 使用时间线视图确定发布状态。

* 使用自适应Forms编辑器中的页面信息菜单。