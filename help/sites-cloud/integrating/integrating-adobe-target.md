---
title: 与 Adobe Target 集成
description: '与 Adobe Target 集成 '
feature: Administering
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
source-git-commit: a2fa676de0d6ca6d7cde3beedd5cc63850966b56
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 2%

---

# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为Adobe Marketing Cloud的一部分，Adobe Target允许您通过跨所有渠道进行定位和测量来提高内容相关性。 集成Adobe Target和AEMas a Cloud Service需要：

* 使用触屏UI在AEMas a Cloud Service中创建Target配置（需要IMS配置）。
* 将Adobe Target添加和配置为 [Adobe启动](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html).

AdobeLaunch是管理AEM页面（JS库/标记）中Analytics和Target的客户端属性所必需的。 尽管如此，“体验定位”需要与Launch集成。 要将体验片段导出到Target，您只需要Adobe Target配置和IMS。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service客户如果没有现有的Target帐户，则可以请求访问Target Foundation Pack以进行Experience Cloud。 Foundation Pack提供了对Target的卷限制使用。

## 创建Adobe Target配置 {#create-configuration}

1. 导航到 **工具** → **Cloud Services**.
   ![导航](assets/cloudservice1.png "导航")
2. 选择 **Adobe Target**.
3. 选择 **创建** 按钮。
   ![创建](assets/tenant1.png "创建")
4. 填写详细信息（请参阅下文），然后选择 **连接**.
   ![连接](assets/open_screen1.png "连接")

### IMS 配置 {#ims-configuration}

要将Target与AEM和Launch正确集成，必须同时为Launch和Target配置IMS。 虽然Launch的IMS配置在AEMas a Cloud Service中进行了预配置，但必须创建Target IMS配置（在配置Target后）。 请参阅 [此视频](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html) 和 [本页](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html) 了解如何创建Target IMS配置。

### Adobe Target租户ID和Adobe Target客户端代码 {#tenant-client}

配置Adobe Target租户ID和Adobe Target客户端代码字段时，请注意以下事项：

1. 对于大多数客户，租户ID和客户端代码是相同的。 这表示两个字段包含相同的信息且相同。 请确保在这两个字段中输入租户ID。
2. 出于旧版目的，您还可以在租户ID和客户端代码字段中输入不同的值。

在这两种情况下，请注意：

* 默认情况下，客户端代码（如果先添加）也会自动复制到租户ID字段中。
* 您可以选择更改默认的租户ID集。
* 因此，对Target的后端调用将基于租户ID，而对Target的客户端调用将基于客户端代码。

如前所述，第一种情况是AEMas a Cloud Service最常见的情况。 无论怎样，都要确保 **both** 字段包含正确的信息，具体取决于您的要求。

>[!NOTE]
>
> 如果要更改现有Target配置：
>
> 1. 重新输入租户ID。
> 2. 重新连接到Target。
> 3. 保存配置。


### 编辑Target配置 {#edit-target-configuration}

要编辑Target配置，请执行以下步骤：

1. 选择现有配置并单击 **属性**.
2. 编辑属性。
3. 选择 **重新连接到Adobe Target**.
4. 选择&#x200B;**保存并关闭**。

### 向站点添加配置 {#add-configuration}

要将触屏UI配置应用到站点，请转到： **站点** → **选择任意网站页面** → **属性** → **高级** → **配置** →选择配置租户。

## 使用Launch在AEM网站上集成Adobe Target {#integrate-target-launch}

AEM提供了与Experience Platform Launch的开箱即用集成。 通过将Adobe Target扩展添加到Experience Platform Launch，您可以在AEM网页上使用Adobe Target的功能。 Target库将仅通过使用Launch来呈现。

>[!NOTE]
>
>现有（旧版）框架仍然有效，但无法在触屏UI中配置。 建议在Launch中重新构建变量映射配置。

作为一般概述，集成步骤包括：

1. 创建Launch资产
2. 添加所需的扩展
3. 创建数据元素（用于捕获ContextHub参数）
4. 创建页面规则
5. 生成和发布

### 创建Launch资产 {#create-property}

资产是一个容器，其中填充了扩展、规则和数据元素。

1. 选择 **新建资产** 按钮。
2. 为您的资产提供名称。
3. 作为域，输入要加载Launch库的IP/主机。
4. 选择 **保存** 按钮。
   ![Launchproperty](assets/properties_newproperty1.png "Launchproperty")

### 添加所需的扩展 {#add-extension}

**扩展** 是管理核心库设置的容器。 Adobe Target扩展通过使用适用于新版Web的Target JavaScript SDK(at.js)支持客户端实施。 您必须将 **Adobe Target** 和 **AdobeContextHub** 扩展。

1. 选择扩展目录选项，然后在筛选器中搜索Target。
2. 选择 **Adobe Target** at.js中，然后单击安装选项。
   ![目标搜索](assets/search_ext1.png "目标搜索")
3. 选择 **配置** 按钮。 请注意导入了Target帐户凭据以及此扩展的at.js版本的配置窗口。
4. 选择 **保存** 将Target扩展添加到Launch资产中。 您应该能够在 **已安装的扩展** 列表。
   ![保存扩展](assets/configure_extension1.png "保存扩展")
5. 重复上述步骤以搜索 **AdobeContextHub** 扩展并安装它（与contexthub参数集成时需要此参数，具体取决于将要完成的定位）。

### 创建数据元素 {#data-element}

**数据元素** 是占位符，您可以将context hub参数映射到这些占位符。

1. 选择 **数据元素**.
2. 选择 **添加数据元素**.
3. 提供数据元素的名称，并将其映射到ContextHub参数。
4. 选择&#x200B;**保存**。
   ![数据元素](assets/data_elem1.png "数据元素")

### 创建页面规则 {#page-rule}

在 **规则** 我们定义并排序一系列在现场执行的操作，以实现定位。

1. 添加一组操作，如屏幕截图中所示。
   ![操作](assets/rules1.png "操作")
2. 在Add Params to All Mboxes中，将之前配置的数据元素（请参阅上面的数据元素）添加到将在mbox调用中发送的参数中。
   ![Mbox](assets/map_data1.png "操作")

### 生成和发布 {#build-publish}

要了解如何构建和发布，请参阅 [页面](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html).

## 经典UI和触屏UI配置之间的内容结构更改 {#changes-content-structure}

<table style="table-layout:auto">
  <tr>
    <th>更改</th>
    <th>经典UI配置</th>
    <th>触屏UI配置</th>
    <th>后果</th>
  </tr>
  <tr>
    <td>Target配置的位置。</td>
    <td>/etc/cloudservices/testandtarget/</td>
    <td>/conf/tenant/settings/cloudservices/target/</td>
    <td> 以前，在/etc/cloudservices/testandtarget下存在多个配置，但现在租户下存在单个配置。</td>
  </tr>
</table>

>[!NOTE]
>
>现有客户仍支持旧版配置（无法选择编辑或创建新配置）。 旧版配置将包含在使用VSTS的客户上传的内容包中。
