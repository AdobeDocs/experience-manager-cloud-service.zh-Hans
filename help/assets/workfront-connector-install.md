---
title: 安装 [!DNL Workfront for Experience Manager enhanced connector]
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: a5776453b261e6f4e6c891763934b236bade8f7f
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# 安装 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

具有 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 安装增强的连接器。 安装之前，请查看平台支持和其他 [连接器先决条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 仅通过认证合作伙伴或 [!DNL Adobe Professional Services]. 如果部署和配置时没有经过认证的合作伙伴或 [!DNL Adobe Professional Services]，则Adobe不支持此功能。
>
>Adobe可发布 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此连接器冗余；如果发生这种情况，客户可能需要从使用此连接器过渡。

在安装连接器之前，请执行以下预安装步骤：

1. [配置防火墙](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). 了解中的IP群集 [!DNL Workfront]，导航到 [!UICONTROL 设置] > [!UICONTROL 系统] > [!UICONTROL 客户信息].

1. 在调度程序上，允许名为 `authorization`, `username`和 `apikey`. 允许 `GET`, `POST`和 `PUT` 请求 `/bin/workfront-tools`.

1. 确保中不存在以下路径 [!DNL Experience Manager] 存储库：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 此安装需要具备在 [!DNL Experience Manager] as a [!DNL Cloud Service]. 请使用以下资源了解如何在Maven项目中包含第三方包：

   * [在Maven项目中包含第三方包](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [部署方式 [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

要在 [!DNL Experience Manager] as a [!DNL Cloud Service]，请执行以下步骤：

1. 从下载增强的连接器 [AdobeSoftware Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 和从Cloud Manager克隆AEMas a Cloud Service存储库。

1. 使用您选择的IDE打开克隆的AEMas a Cloud Service存储库。

1. 将步骤1中下载的增强型连接器zip文件放置在以下路径中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果 `resources` 文件夹不存在，请创建文件夹。


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
      >确保在将依赖项复制到父项之前更新增强的连接器版本号 `pom.xml`.

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


1. 添加 `pom.xml` 嵌入。 添加 [!DNL Workfront for Experience Manager enhanced connector] 包到 `embeddeds` 部分 `pom.xml` 所有子项目。 需要将其嵌入到所有模块中 `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   嵌入部分的目标设置为 `/apps/<path-to-project-install-folder>/install`. 此JCR路径 `/apps/<path-to-project-install-folder>` 必须包含在 `all/src/main/content/META-INF/vault/filter.xml` 文件。 存储库的筛选规则通常从程序名称派生。 在现有规则中使用文件夹的名称作为目标。

1. 将更改推送到存储库。

1. 运行管道以 [将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. 要创建系统用户配置，请创建 `wf-workfront-users` in [!DNL Experience Manager] 用户组并分配权限 `jcr:all` to `/content/dam`. 系统用户 `workfront-tools` 将自动创建，并自动管理所需的权限。 所有用户 [!DNL Workfront] 使用enhanced连接器的用户将自动添加到此组中。

## 配置之间的连接 [!DNL Experience Manager] as a [!DNL Cloud Service] 和 [!DNL Workfront] {#configure-connection}

创建连接 [!DNL Workfront]，请执行以下步骤：

1. 在 [!DNL Experience Manager]，选择 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**.

1. 选择 `workfront-tools` ，然后选择 **[!UICONTROL 创建]** 选项。

1. 在 **[!UICONTROL Workfront连接]** 对话框中，提供您的 [!DNL Workfront] 部署，然后选择 **[!UICONTROL 连接到Workfront]** 选项。 成功连接后， [!DNL Workfront] 文档自定义集成将在 [!DNL Workfront] 环境。

   ![连接 [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 导航到 **[!UICONTROL 高级]** 选项卡，然后选择选项 **[!UICONTROL 服务器AEM是否as a Cloud Service]**.
