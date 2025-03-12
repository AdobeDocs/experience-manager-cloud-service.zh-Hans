---
title: 使用CTT后将主体批量上传到IMS
description: 有关为组和用户批量上传文件，以及如何在Admin Console中使用这些文件在IMS中创建组和用户的概述。
source-git-commit: c3a13f75757a478996918c6868a172d75158aafe
workflow-type: tm+mt
source-wordcount: '2382'
ht-degree: 0%

---


# 使用CTT后将主体批量上传到IMS {#bulk-principal-uploading}

>[!CONTEXTUALHELP]
>id="bulk-principal-uploading"
>title="主体批量上传"
>abstract="有关为组和用户批量上传文件，以及如何在Admin Console中使用这些文件在IMS中创建组和用户的概述。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="AEM Admin Console 文档"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

## 简介 {#introduction}

使用CTT和CAM将内容迁移到云会在AEM云实例上创建组，但它不会对在IMS中放置组或用户执行任何操作。 它们需要存在于IMS中才能由客户正确管理。 幸运的是，Admin Console提供了批量创建IMS组和用户的功能。 CAM摄取通过保存用于此批量创建的输入文件来帮助完成此过程，从而使客户能够作为其整体迁移过程的一部分完成此Admin Console操作。 创建了两种批量上传文件：一种用于组，另一种用于用户。

有关管理AEM as a Cloud Service用户的更多详细信息，另请参阅[管理用户](https://helpx.adobe.com/cn/enterprise/using/users.html)。

## 上载文件的一般规则 {#rules}

对于编辑和使用这两种上载文件，有一些一般准则：

* 在遵循这些说明之前，必须先授予对Admin Console的管理员访问权限
* 请注意，在IMS中创建用户和组的方式有一些不同。  请参阅对Adobe Experience Manager as a Cloud Service的[IMS支持](/help/security/ims-support.md)，了解所有可用选项。  此处仅介绍Admin Console批量上传方法
* IMS中可能存在三种标识类型：**Adobe ID**、**Enterprise ID**&#x200B;和&#x200B;**Federated ID**。 本页上的说明仅针对&#x200B;**Adobe ID**&#x200B;提供。  如果您需要使用Enterprise ID或Federated ID，请参阅完整的[Admin Console文档](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)以及有关[Admin Console批量组上传](https://helpx.adobe.com/cn/enterprise/using/user-groups.html)和[Admin Console批量用户上传](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html)的特定文档。  对于这两种标识类型，上载文件的规范稍有不同
* 如果单个CSV字段允许多个条目（如多个产品配置文件、多个组或多个管理员），则条目必须用双引号包含并用逗号（即`"profile 1,profile 2"`）分隔
   * 对于这种情况，可以使用单引号而不是双引号，但在Microsoft Excel中编辑文件可能会导致解析问题。 如果使用Excel编辑这些文件，请确保使用双引号而不是单引号。

## 批量组上载 {#group-upload}

#### 用例：组已迁移到AEM as a Cloud Service，但这些组未出现在IMS/Admin Console中，因此需要通过Admin Console将它们上传到IMS。

要在运行CTT/CAM迁移后使用Admin Console的批量组上传功能，请执行以下步骤：
1. 从CAM下载批量组文件

   1. 在CAM中，转到&#x200B;**内容传输**&#x200B;并选择&#x200B;**引入作业**。
   1. 单击相关摄取行上的省略号(...)，然后选择&#x200B;**查看主体摘要**。
   1. 在出现的对话框中，从&#x200B;**下载文件……**&#x200B;下的下拉列表中选择&#x200B;**批量组文件**，然后单击&#x200B;**下载**&#x200B;按钮。
   1. 保存生成的CSV文件。

1. 编辑批量组文件

   * 每一行表示要上传的组，其中包含四个字段（字段的名称构成了文件的第一行）：

      * _用户组名称_ — 需要该组名称，最多可包含255个字符。  此组名称在IMS和AEM中必须相同
      * _描述_ — 此字段为可选字段，最多可包含255个字符
      * _用户组管理员_ — 此字段必须至少包含一个组管理员。 通过用逗号分隔每个管理员并将列表用引号引起来，可分配多个管理员。 每个管理员的条目必须包含用户的身份类型，后跟一个连字符，然后是电子邮件地址。  例如
        `"Adobe ID-myAdmin@example.com,Adobe ID-myOtherAdmin@example.com"`。不要在管理员之间的逗号后包含空格。 您不能在Admin Console中包含当前不属于组织的用户（作为管理员）
      * _已分配的产品配置文件_ — 此字段是可选的。 您可以通过以下方式分配多个产品配置文件：用逗号分隔每个配置文件，并将列表用引号引起来。 但是，您必须已经为组织设置所包含的产品配置文件。 请确保您指定的是产品配置文件名称，而不是产品名称。  分配给组的产品配置文件的成员资格将由该组中的所有用户继承。  要查找产品配置文件，请执行以下操作：
         1. 转到Admin Console
         1. 找到您的产品(即Adobe Experience Manager as a Cloud Service)，然后单击它
         1. 找到您的环境（实例），然后单击它
         1. 列出产品配置文件，然后单击适用于您的AEM环境的。 产品配置文件位于顶部，即&quot;_AEM用户 — 作者 — 项目12345 — 环境012345_&quot;。

   * 在编辑CSV时，某些应用程序可能会在保存时添加其他引号，从而导致处理失败。 好的做法是在简单的文本编辑器中检查原始CSV，以确保每个字段只有一个开头和结尾引号（并且它们不应是“智能引号”）。

1. 在Admin Console中上传批量组文件

   1. 在Admin Console中，依次转到&#x200B;**用户**&#x200B;和&#x200B;**用户组**
   1. 单击右侧的“……”按钮。 从菜单中选择&#x200B;**通过CSV添加用户组**，然后选择要上载的CSV。 单击&#x200B;**上传**
   1. 您会收到一个已将CSV上传(到Admin Console)的响应，但尚未将其导入到IMS
   1. 转到相同的“……”菜单，然后选择&#x200B;**批量操作结果**。 它将向您显示批量上传尝试的列表，并告诉您（在&#x200B;**状态**&#x200B;下）批量上传是正在处理、成功还是失败
      * 最初，它显示“正在处理”，指示它尚未完成
      * 成功完成后，单击链接&#x200B;**添加用户组**&#x200B;以查看每行的简单状态消息。
      * 如果失败，请单击&#x200B;**文件**&#x200B;下的小图标，它将提供有关失败原因的详细信息。  从行1开始引用组行号。
1. 使用Admin Console验证您的更改。

## 批量用户上传和编辑 {#bulk-user}

Admin Console包含两个用于上传和编辑用户详细信息的单独操作。 下面的说明介绍了如何向IMS添加新用户。 有关编辑现有IMS用户的说明，请参阅名为[批量用户编辑](#user-edit)的以下部分。

### 批量用户上传 {#user-upload}

#### 用例：组已迁移到AEM as a Cloud Service，并通过批量上传或其他方法上传。  用户可能不在IMS/Admin Console中，因此需要通过Admin Console上传他们并将其链接到IMS中的组。

要使用Admin Console的批量用户上传功能，请执行以下步骤：

1. 从CAM下载批量用户文件
1. 在CAM中，转到&#x200B;**内容传输**&#x200B;并选择&#x200B;**引入作业**。
1. 单击相关摄取行上的省略号(...)，然后选择&#x200B;**查看主体摘要**。
1. 在出现的对话框中，从&#x200B;**下载文件……**&#x200B;下的下拉列表中选择&#x200B;**批量用户文件**，然后单击&#x200B;**下载**&#x200B;按钮。
1. 保存生成的CSV文件

>[!NOTE]
>
>如果用户位于创建该文件的同一个引入期间引入的组中，则该用户将显示在&#x200B;**批量用户上传**&#x200B;文件中。 如果用户直接位于已迁移内容的ACL或CUG上，或者是位于已迁移内容的ACL或CUG上的内置组或本地组的成员，则也可能会出现此情况。 有关这些情况的详细信息，请参阅[组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)。

* 编辑批量用户文件
* 每一行表示要上传的用户，它有十五个字段（字段的名称构成了文件的第一行）。 某些字段是可选的，此处未对其进行说明。 请参阅[批量用户CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)。  这些字段包括：
   * _标识类型_ — 可选。  如果未指定，则将其创建为Adobe ID
   * _用户名_ — 可选，不用于Adobe ID上传
   * _域_ — 可选，不用于Adobe ID上传
   * _电子邮件_ — 必需。  该电子邮件地址将在用户首次登录时用于验证
   * _名字_ — 可选。  应使用，因为它与姓氏一起出现在多个位置
   * _姓氏_ — 可选。  应使用，因为它出现在多个位置
   * _国家/地区代码_ — 可选，不用于Adobe ID上传
   * _ID_ — 可选，不用于Adobe ID上传
   * _产品配置_ — 可选。 此字段也将从用户所属的任何组继承
   * _管理员角色_ — 可选。 如果用户是管理员，请使用此字段。 有关详细信息，请参阅[批量用户CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
   * _已管理产品配置_ — 可选。  有关详细信息，请参阅[批量用户CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)。 此字段也将从用户所属的任何组继承
   * _用户组_ — 可选。 用户应指定为成员的组的列表。 每个组必须是已存在的IMS组。 从CAM下载批量用户文件时，此字段预先填充了迁移前用户作为成员且启用了IMS的组的名称（直接或间接）
   * _用户组已管理_ — 可选。  有关详细信息，请参阅[批量用户CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)。 此字段也将从用户所属的任何组继承
   * _管理的产品_ — 可选。  有关详细信息，请参阅[批量用户CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)。 此字段也将从用户所属的任何组继承
   * _管理的合同_ — 可选。  有关详细信息，请参阅[批量用户CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
   * _开发人员访问权限_ — 可选。  有关详细信息，请参阅[批量用户CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
   * _自动分配的产品_ — 可选。  有关详细信息，请参阅[批量用户CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
   * 在编辑CSV时，某些应用程序可能会在保存时添加其他引号，从而导致处理失败。 好的做法是在简单的文本编辑器中检查原始CSV，以确保每个字段只有一个开头和结尾引号（并且它们不应是“智能引号”）

1. 在Admin Console中上传批量用户文件

   1. 在Admin Console中，转到“用户”
   1. 单击&#x200B;**通过CSV添加用户**&#x200B;按钮
   1. 拖放或选择从CAM下载的批量用户CSV文件
   1. 单击&#x200B;**上传**&#x200B;按钮
   1. 您会收到一个已将CSV上传(到Admin Console)的响应，但该CSV尚未导入到IMS。

1. 转到右侧的“……”菜单，然后选择&#x200B;**批量操作结果**。  它将显示批量上传尝试的列表，并显示（在&#x200B;**状态**&#x200B;下）批量上传是正在处理、成功还是失败。

   * 最初，它显示“正在处理”，指示它尚未完成
   * 成功完成后，单击链接&#x200B;**添加用户**&#x200B;以查看每行的简单状态消息
   * 如果失败，请单击&#x200B;**文件**&#x200B;下的小图标，它将为您提供有关失败原因的详细信息。 从行1开始引用用户行号。

1. 使用Admin Console验证您的更改。

>[!NOTE]
>
>非划出摄取后，以前在IMS中迁移并创建的用户可能会显示在批量用户上传文件中。 这可能有很多原因。 在这种情况下，再次上传用户将失败。 相反，请尝试从批量用户上传文件中删除用户，如果需要将该用户添加到其他组，请按照以下所述使用批量用户编辑文件。

### 批量用户编辑 {#user-edit}

#### 用例：组和用户已迁移到AEM as a Cloud Service，并通过批量上传或其他方法上传。 现在，需要一次性对多个用户进行某些更改，例如将其添加到现有IMS组。

要使用Admin Console的批量用户编辑功能，请执行以下步骤：

1. 从管理控制台下载批量用户文件

   1. 在Admin Console中，转到“用户”
   1. 单击右侧的“……”按钮。  从菜单中选择&#x200B;**通过CSV编辑用户详细信息**
   1. 单击&#x200B;**下载CSV模板**&#x200B;并选择&#x200B;**当前用户**。  CSV文件应显示在您的本地“下载”文件夹中。

1. 编辑批量用户文件

   1. 在Admin Console中，转到“用户”
   1. 使用文本编辑器（推荐）或电子表格应用程序（如Excel）编辑CSV文件。 使用应用程序可能会对数据做出不可预测的更改，因此建议在进行了所有编辑之后，使用文本编辑器来验证文件的格式
   1. 此文件中各个字段的描述与上文“批量用户上传”下的描述相同
   1. 删除所有未编辑的用户
   1. 如果更改用户组字段，请保留当前组并根据需要添加新组。 如果删除现有组，则会将该用户从IMS中的该组中移除
   1. 在编辑CSV时，某些应用程序可能会在保存时添加其他引号，从而导致处理失败。 好的做法是在简单的文本编辑器中检查原始CSV文件，以确保每个字段只有一个开头和结尾引号（并且它们不应是“智能引号”）

1. 在Admin Console中上传批量用户文件

   1. 在Admin Console中，转到“用户”
   1. 单击右侧的“……”按钮。 从菜单中选择&#x200B;**通过CSV编辑用户详细信息**
   1. 拖放或选择已编辑的批量用户CSV文件
   1. 单击“上载”按钮
   1. 您会收到一个已将CSV上传(到Admin Console)的响应，但尚未将其导入到IMS
   1. 转到右侧的“……”菜单，然后选择&#x200B;**批量操作结果**。 它将向您显示批量上传尝试的列表，并告诉您（在“状态”下）批量上传正在处理、成功还是失败。

   * 最初，它显示“正在处理”，指示它尚未完成
   * 成功完成后，单击&#x200B;**编辑用户详细信息**&#x200B;链接以查看每行的简单状态消息
   * 如果失败，请单击&#x200B;**文件**&#x200B;下的小图标，将显示更多有关失败原因的信息。 从行1开始引用用户行号。

1. 使用Admin Console验证您的更改。
