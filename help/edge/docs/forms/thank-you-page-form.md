---
title: 配置 EDS Forms 的感谢页面
description: 配置 EDS Forms 的感谢页面
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: ht
source-wordcount: '139'
ht-degree: 100%

---


# 配置表单区块重定向

您可以选择将表单区块配置为重定向到网站上的其他页面，而不是默认的“谢谢”页面。将另一个页面设置为重定向目标

1. 打开 `[EDS Project]/blocks/form/form.js` 文件以供编辑。

   ![感谢节点代码](/help/edge/assets/change-thankyou-node.png)

1. 将以下行中的 `thankyou` 节点更改为您选择的节点：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例如，

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'home';
   ```

   >[!NOTE]
   >
   > 确保在 Microsoft SharePoint 或 Google Sheets 上的 Edge Delivery Service 项目文件夹中创建同名的文档页面（如果尚未创建）。


1. 然后将更新后的“form.js”文件夹及其底层文件签入 GitHub 上的 Edge Delivery Service 项目。此更新可确保表单现在重定向到指定的更新节点。
