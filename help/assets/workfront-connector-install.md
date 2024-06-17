---
title: 安装 [!DNL Workfront for Experience Manager enhanced connector]
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 1%

---

# 安装 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html) |
| AEM as a Cloud Service | 本文 |

在中具有管理员访问权限的用户 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 安装增强型连接器。 安装之前，请查看平台支持及其他 [连接器的先决条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>自2022年6月起，Adobe发布了一个新的原生集成，用于将Workfront与Adobe Experience Manager Assetsas a Cloud Service连接。 这种集成已成为连接这两种解决方案的必需方法。 阻止将来Workfront与AEM Assetsas a Cloud Service连接的增强型连接器（1.9.8及更高版本）的任何新实施。 有关如何设置此集成的更多信息，请参阅 [配置Experience Manager Assetsas a Cloud Service集成](workfront-connector-configure.md).

>[!IMPORTANT]
>
>* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 仅通过认证合作伙伴或 [!DNL Adobe Professional Services]. 如果部署与配置时没有认证合作伙伴或 [!DNL Adobe Professional Services]，Adobe不支持它。
>
>* Adobe可能会将更新发布到 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此连接器成为冗余连接器；如果发生这种情况，客户可能需要从使用此连接器过渡到使用此连接器。
>
>* Adobe支持增强型连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强的连接器版本，请参阅的步骤5(a) [增强型连接器安装说明](workfront-connector-install.md).
>
>* 请参阅 [Workfront for Experience Manager Assets增强型连接器的合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有关考试的信息，请参见 [考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

在安装连接器之前，请按照以下预安装步骤操作：

1. 如果您的AEMas a Cloud Service程序配置了高级联网并启用了IP允许列表，则需要将Workfront IP添加到此允许列表，以允许事件订阅和各种API调用传递到AEM。

   * [Workfront群集IP](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=en#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9). 了解中的IP群集 [!DNL Workfront]，导航到 **[!UICONTROL 设置]** > **[!UICONTROL 系统]** > **[!UICONTROL 客户信息]**.

   * [Workfront事件订阅API IP](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html)

   >[!IMPORTANT]
   >
   >* 如果您为程序配置了高级网络并且正在使用IP允许列表，则由于增强Workfront连接器体系结构的限制，您还需要将程序出口IP添加到Cloud Manager中的允许列表。
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* 要查找程序的IP，请打开终端窗口并运行命令，例如：
   >
   >    ```
   >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >    ```

1. 确保中不存在以下叠加 [!DNL Experience Manager] 存储库。 如果您在这些路径上预先存在叠加图，则需要删除叠加图，或合并两个路径之间的更改增量：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. 此安装要求您具备在中设置Maven项目的知识 [!DNL Experience Manager] as a [!DNL Cloud Service]. 请使用以下资源了解如何在Maven项目中包含第三方软件包：

   * [在您的Maven项目中包含第三方包](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [部署方式 [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

在中安装加载项 [!DNL Experience Manager] as a [!DNL Cloud Service]，请按照以下步骤操作：

1. 从下载增强型连接器 [AdobeSoftware Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 并从Cloud Manager中克隆AEMas a Cloud Service存储库。

1. 使用您选择的IDE打开克隆的AEMas a Cloud Service存储库。

1. 将步骤1中下载的增强型连接器zip文件放在以下路径中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果 `resources` 文件夹不存在，请创建该文件夹。


1. 添加 `pom.xml` 依赖关系：

   1. 在父项中添加依赖项 `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
      ```

      >[!NOTE]
      >
      >请确保在将依赖项复制到父级之前更新增强型连接器的版本号 `pom.xml`.

   1. 在中添加依赖项 `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. 添加 `pom.xml` 嵌入。 添加 [!DNL Workfront for Experience Manager enhanced connector] 将包发送至 `embeddeds` 的部分 `pom.xml` 您的所有子项目的。 需要将其嵌入所有模块 `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   嵌入部分的目标设置为 `/apps/<path-to-project-install-folder>/install`. 此JCR路径 `/apps/<path-to-project-install-folder>` 必须包含在的过滤器规则中 `all/src/main/content/META-INF/vault/filter.xml` 文件。 存储库的过滤器规则通常派生自项目名称。 使用文件夹名称作为现有规则中的目标。

1. 将更改推送到存储库。

1. 将管道运行到 [将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. 要创建系统用户配置，请创建 `wf-workfront-users` 在 [!DNL Experience Manager] 用户组和分配权限 `jcr:all` 到 `/content/dam`. 系统用户 `workfront-tools` 将自动创建，并自动管理所需的权限。 所有用户来自 [!DNL Workfront] 使用增强型连接器的用户会自动添加为该组的一部分。

有关更新 [!DNL Workfront for Experience Manager enhanced connector] 从以前的版本到最新的版本，单击 [此处](update-workfront-enhanced-connector.md).

## 配置之间的连接 [!DNL Experience Manager] as a [!DNL Cloud Service] 和 [!DNL Workfront] {#configure-connection}

创建连接 [!DNL Workfront]，请按照以下步骤操作：

1. 在 [!DNL Experience Manager]，选择 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具配置]**.

1. 选择 `workfront-tools` 在左侧面板中选择 **[!UICONTROL 创建]** 选项。

1. 在 **[!UICONTROL Workfront连接]** 对话框，请提供您所需的详细信息 [!DNL Workfront] 部署，然后选择 **[!UICONTROL 连接到Workfront]** 选项。 成功连接后， [!DNL Workfront] 文档自定义集成是在以下位置自动创建的： [!DNL Workfront] 环境。

   ![连接 [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 导航至 **[!UICONTROL 高级]** 选项卡并选择选项 **[!UICONTROL 服务器AEMas a Cloud Service]**.
