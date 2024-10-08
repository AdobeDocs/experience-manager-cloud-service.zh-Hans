---
title: 安装 [!DNL Workfront for Experience Manager enhanced connector]
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 2%

---

# 安装[!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html) |
| AEM as a Cloud Service | 本文 |

在[!DNL Adobe Experience Manager]中具有[!DNL Cloud Service]管理员访问权限的用户安装增强型连接器。 安装之前，请查看平台支持以及连接器](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)的其他[先决条件。

>[!IMPORTANT]
>
>自2022年6月起，Adobe发布了一个新的原生集成，用于将Workfront与Adobe Experience Manager Assetsas a Cloud Service连接。 这种集成已成为连接这两种解决方案的必需方法。 阻止将来as a Cloud Service与WorkfrontAEM Assets连接的增强型连接器（1.9.8及更高版本）的任何新实施。 有关如何设置此集成的更多信息，请参阅[配置Experience Manager Assetsas a Cloud Service集成](workfront-connector-configure.md)。

>[!IMPORTANT]
>
>* Adobe仅需要通过认证合作伙伴或[!DNL Adobe Professional Services]来部署和配置[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未使用认证合作伙伴或[!DNL Adobe Professional Services]进行部署和配置，则Adobe不支持该功能。
>
>* Adobe可能会发布使此连接器冗余的[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]更新；如果发生这种情况，客户可能需要从使用此连接器过渡。
>
>* Adobe支持增强型连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强型连接器版本，请参阅[增强型连接器安装说明](workfront-connector-install.md)的步骤5(a)。
>
>* 查看Experience Manager Assets增强型连接器的[Workfront合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 有关考试的信息，请参阅[考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。

在安装连接器之前，请按照以下预安装步骤操作：

1. 如果您的AEM as a Cloud Service程序配置了高级联网并启用了IP允许列表，则需要将Workfront IP添加到此允许列表，以允许事件订阅和各种API调用传递到AEM。

   * [Workfront群集IP](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=en#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9)。 若要了解[!DNL Workfront]中的IP群集，请导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 系统]** > **[!UICONTROL 客户信息]**。

   * [Workfront事件订阅API IP](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html)

   >[!IMPORTANT]
   >
   >* 如果您为程序配置了高级联网并且正在使用IP允许列表，则由于增强Workfront连接器体系结构的限制，您还需要将程序出口IP添加到Cloud Manager中的允许列表。
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* 要查找程序的IP，请打开终端窗口并运行命令，例如：
   >
   >    ```
   >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >    ```

1. 确保[!DNL Experience Manager]存储库中不存在以下叠加。 如果您在这些路径上预先存在叠加图，则需要删除叠加图，或合并两个路径之间的更改增量：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. 此安装要求了解如何在[!DNL Experience Manager]中将Maven项目设置为[!DNL Cloud Service]。 请使用以下资源了解如何在Maven项目中包含第三方软件包：

   * [在您的Maven项目中包含第三方包](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party)。
   * 使用 [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)部署[。

要将加载项作为[!DNL Cloud Service]安装在[!DNL Experience Manager]中，请执行以下步骤：

1. 从[Adobe软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)下载增强型连接器。

1. [访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en)并从Cloud Manager克隆AEM as a Cloud Service存储库。

1. 使用您选择的IDE打开克隆的AEM as a Cloud Service存储库。

1. 将步骤1中下载的增强型连接器zip文件放在以下路径中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果`resources`文件夹不存在，请创建该文件夹。


1. 添加`pom.xml`依赖项：

   1. 在父`pom.xml`中添加依赖项。

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
      >请确保在将依赖项复制到父`pom.xml`之前更新增强型连接器版本号。

   1. 在`all module pom.xml`中添加依赖项。

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. 添加`pom.xml`个嵌入。 将[!DNL Workfront for Experience Manager enhanced connector]包添加到所有子项目的`pom.xml`的`embeddeds`部分。 需要将其嵌入所有模块`pom.xml`。

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   嵌入节的目标设置为`/apps/<path-to-project-install-folder>/install`。 此JCR路径`/apps/<path-to-project-install-folder>`必须包含在`all/src/main/content/META-INF/vault/filter.xml`文件的筛选器规则中。 存储库的过滤器规则通常派生自项目名称。 使用文件夹名称作为现有规则中的目标。

1. 将更改推送到存储库。

1. 运行管道以[将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。

1. 要创建系统用户配置，请在[!DNL Experience Manager]用户组中创建`wf-workfront-users`并将权限`jcr:all`分配给`/content/dam`。 自动创建系统用户`workfront-tools`，并自动管理所需的权限。 来自[!DNL Workfront]且使用增强型连接器的所有用户都自动添加为该组的一部分。

若要将[!DNL Workfront for Experience Manager enhanced connector]从以前的版本更新到最新的版本，请单击[此处](update-workfront-enhanced-connector.md)。

## 将[!DNL Experience Manager]之间的连接配置为[!DNL Cloud Service]和[!DNL Workfront] {#configure-connection}

要创建与[!DNL Workfront]的连接，请执行以下步骤：

1. 在[!DNL Experience Manager]中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具配置]**。

1. 在左侧面板中选择`workfront-tools`，然后在页面的右上角区域中选择&#x200B;**[!UICONTROL 创建]**&#x200B;选项。

1. 在&#x200B;**[!UICONTROL Workfront连接]**&#x200B;对话框中，提供[!DNL Workfront]部署所需的详细信息，然后选择&#x200B;**[!UICONTROL 连接到Workfront]**&#x200B;选项。 成功连接后，将在[!DNL Workfront]环境中自动创建[!DNL Workfront]文档自定义集成。

   ![连接[!DNL Experience Manager]和[!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 导航到&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡，然后选择选项&#x200B;**[!UICONTROL 是服务器AEM as a Cloud Service]**。
