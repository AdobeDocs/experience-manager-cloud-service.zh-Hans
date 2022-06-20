---
title: 与 Adobe Target 集成
description: '与 Adobe Target 集成 '
feature: Administering
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
source-git-commit: a2fa676de0d6ca6d7cde3beedd5cc63850966b56
workflow-type: ht
source-wordcount: '1035'
ht-degree: 100%

---

# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为 Adobe Marketing Cloud 的一部分，Adobe Target 允许您通过在所有渠道中进行定位和衡量来提高内容相关性。集成 Adobe Target 和 AEM as a Cloud Service 需要：

* 使用 Touch UI 在 AEM as a Cloud Service 中创建 Target 配置（需要 IMS 配置）。
* 在 [Adobe Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html) 中将 Adobe Target 添加为扩展并进行配置。

Adobe Launch 是管理 AEM 页面（JS 库/标记）中 Analytics 和 Target 的客户端属性所必需的。也就是说，需要与 Launch 集成才能实施“体验定位”。您只需要 Adobe Target 配置和 IMS 即可将体验片段导出到 Target。

>[!NOTE]
>
>不具有现有 Target 帐户的 Adobe Experience Manager as a Cloud Service 客户可以请求对 Target Foundation Pack for Experience Cloud 的访问权限。此 Foundation Pack 提供了对 Target 的限量使用。

## 创建 Adobe Target 配置 {#create-configuration}

1. 导航到&#x200B;**工具** → **云服务**。
   ![导航](assets/cloudservice1.png "导航")
2. 选择 **Adobe Target**。
3. 选择&#x200B;**创建**按钮。
   ![创建](assets/tenant1.png "创建")
4. 填写详细信息（见下文），然后选择&#x200B;**连接**。
   ![连接](assets/open_screen1.png "连接")

### IMS 配置 {#ims-configuration}

需要适用于 Launch 和 Target 的 IMS 配置才能将 Target 与 AEM 和 Launch 正确集成。虽然已在 AEM as a Cloud Service 中预配置适用于 Launch 的 IMS 配置，但必须创建 Target IMS 配置（在设置 Target 后）。请参阅[本视频](https://helpx.adobe.com/cn/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html)和[本页面](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html)，了解如何创建 Target IMS 配置。

### Adobe Target 租户 ID 和 Adobe Target 客户端代码 {#tenant-client}

在配置 Adobe Target 租户 ID 和 Adobe Target 客户端代码字段时，请注意以下几点：

1. 对于大多数客户来说，租户 ID 和客户代码是相同的。这意味着，这两个字段包含相同的信息并且是相同的。确保在这两个字段中输入租户 ID。
2. 对于遗留问题，您还可以在“租户 ID”和“客户端代码”字段中输入不同的值。

在这两种情况下，请注意：

* 默认情况下，客户端代码（如果首先添加）也会自动复制到“租户 ID”字段中。
* 您可以选择更改默认租户 ID 集。
* 因此，对 Target 进行的后端调用将基于租户 ID，而对 Target 进行的客户端调用将基于客户端代码。

如前所述，对于 AEM as a Cloud Service，第一种情况最常见。无论哪种方式，请确保&#x200B;**两个**&#x200B;字段都包含正确的信息，具体取决于您的要求。

>[!NOTE]
>
> 如果要更改现有 Target 配置，请：
>
> 1. 重新输入租户 ID。
> 2. 重新连接到 Target。
> 3. 保存配置。


### 编辑 Target 配置 {#edit-target-configuration}

要编辑 Target 配置，请执行以下步骤：

1. 选择现有配置，并单击&#x200B;**属性**。
2. 编辑属性。
3. 选择&#x200B;**重新连接到 Adobe Target**。
4. 选择&#x200B;**保存并关闭**。

### 将配置添加到站点 {#add-configuration}

要将 Touch UI 配置应用于站点，请转至：**站点** → **选择任何站点页面** → **属性** → **高级** → **配置** → 选择配置租户。

## 使用 Adobe Launch 在 AEM Sites 上集成 Adobe Target {#integrate-target-launch}

AEM 提供与 Experience Platform Launch 的现成集成。通过将 Adobe Target 扩展添加到 Experience Platform Launch，您可以在 AEM 网页上使用 Adobe Target 的功能。Target 库将仅通过 Launch 呈现。

>[!NOTE]
>
>虽然现有（旧式）框架仍有效，但无法在 Touch UI 中进行配置。建议在 Launch 中重新构建变量映射配置。

作为一般概述，集成步骤为：

1. 创建 Launch 属性
2. 添加所需的扩展
3. 创建数据元素（以捕获 ContextHub 参数）
4. 创建页面规则
5. 构建和发布

### 创建 Launch 属性 {#create-property}

属性是一个填充了扩展、规则和数据元素的容器。

1. 选择&#x200B;**新属性**&#x200B;按钮。
2. 为属性提供名称。
3. 作为域，输入要加载 Launch 库的 IP/主机。
4. 选择&#x200B;**保存**按钮。
   ![Launchproperty](assets/properties_newproperty1.png "Launchproperty")

### 添加所需的扩展 {#add-extension}

**扩展**&#x200B;是管理核心库设置的容器。Adobe Target 扩展通过使用适用于现代 Web at.js 的 Target JavaScript SDK 来支持客户端实施。您必须同时添加 **Adobe Target** 和 **Adobe ContextHub** 扩展。

1. 选择“扩展目录”选项，然后在过滤器中搜索 Target。
2. 选择 **Adobe Target** at.js，然后单击“安装”选项。
   ![Target Search](assets/search_ext1.png "Target Search")
3. 选择&#x200B;**配置**&#x200B;按钮。请注意包含已导入 Target 帐户凭据的配置窗口，以及此扩展的 at.js 版本。
4. 选择&#x200B;**保存**&#x200B;以将 Target 扩展添加到 Launch 属性。**安装的扩展**列表的下方应列出 Target 扩展。
   ![保存扩展](assets/configure_extension1.png "保存扩展")
5. 重复上述步骤以搜索 **Adobe ContextHub** 扩展并安装它（这是与 ContextHub 参数集成所必需的，并基于将执行的定位）。

### 创建数据元素 {#data-element}

**数据元素**&#x200B;是可将 ContextHub 参数映射到的占位符。

1. 选择&#x200B;**数据元素**。
2. 选择&#x200B;**添加数据元素**。
3. 提供数据元素的名称并将它映射到 ContextHub 参数。
4. 选择&#x200B;**保存**。
   ![数据元素](assets/data_elem1.png "数据元素")

### 创建页面规则 {#page-rule}

在&#x200B;**规则**&#x200B;中，我们定义了对站点执行的一系列操作并对它们进行了排序以实现定位。

1. 添加一组操作，如屏幕快照所示。
   ![操作](assets/rules1.png "操作")
2. 在“将参数添加到所有 Mbox”中，将之前配置的数据元素（参见上面的数据元素）添加到将在 mbox 调用中发送的参数。
   ![Mbox](assets/map_data1.png "操作")

### 构建和发布 {#build-publish}

要了解如何构建和发布，请参阅此[页面](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html)。

## 经典和 Touch UI 配置之间的内容结构变化 {#changes-content-structure}

<table style="table-layout:auto">
  <tr>
    <th>更改</th>
    <th>经典 UI 配置</th>
    <th>Touch UI 配置</th>
    <th>结果</th>
  </tr>
  <tr>
    <td>Target 配置的位置。</td>
    <td>/etc/cloudservices/testandtarget/</td>
    <td>/conf/tenant/settings/cloudservices/target/</td>
    <td> 之前，多个配置位于 /etc/cloudservices/testandtarget 下，而现在单个配置位于租户下。</td>
  </tr>
</table>

>[!NOTE]
>
>现有客户仍支持旧版配置（未提供编辑配置或创建新配置的选项）。旧版配置将成为客户使用 VSTS 上传的内容包的一部分。
