---
title: 为EDS Forms配置感谢页面
description: 为EDS Forms配置感谢页面
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 5%

---


# 配置表单块重定向

您可以选择将表单块配置为重定向到您网站上的其他页面，而不是默认的“感谢您”页面。 将其他页面设置为重定向目标

1. 打开 `[EDS Project]/blocks/form/form.js` 文件以供编辑。

   ![感谢节点的代码](/help/edge/assets/change-thankyou-node.png)

1. 更改 `thankyou` 节点到您选择的节点：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例如，

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'home';
   ```

   >[!NOTE]
   >
   > 确保在Microsoft SharePoint或Google Sheets上的Edge Delivery Service项目文件夹中创建同名文档页面（如果尚未创建）。


1. 继续将更新的“form.js”文件夹及其基础文件签入到GitHub上的边缘交付服务项目。 此更新确保表单现在重定向到指定的更新节点。
