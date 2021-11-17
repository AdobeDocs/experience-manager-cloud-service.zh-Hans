---
title: 安装 [!DNL Workfront for Experience Manager enhanced connector]
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 8ca25f86a8d0d61b40deaff0af85e56e438efbdc
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

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

1. 添加 `pom.xml` 依赖关系：

   1. 在父项中添加依赖项 `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>1.7.4</version>
      </dependency>
      ```

   1. 在所有模块中添加依赖项 [!DNL pom.xml].

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
         </dependency>
      ```

1. 添加 `pom.xml` 身份验证。

   1. 在adobe-public配置文件的pom.xml中包含以下存储库配置，以便在生成时（本地和Cloud Manager）可以解析连接器依赖项（上述）。 购买许可证后，将提供存储库访问凭据。 需要将凭据添加到服务器部分的settings.xml文件中。

      ```XML
      <repository>
         <id>hoodoo-maven</id>
         <name>Hoodoo Repository</name>
         <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
      </repository>
      ```

   1. 创建名为 `./cloudmanager/maven/settings.xml` 在项目根目录中。 要支持受密码保护的Maven存储库，请参阅 [如何设置项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md). 此外，还有一个示例 `settings.xml` 文件以供参考。 最后，更新您的本地 `settings.xml` 本地编译。

      ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
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

1. 要创建系统用户配置，请创建 `wf-workfront-users` in [!DNL Experience Manager] 用户组并分配权限 `jcr:all` to `/content/dam`. 系统用户 `workfront-tools` 将自动创建，并自动管理所需的权限。 所有用户 [!DNL Workfront] 使用enhanced连接器的用户将自动添加到此组中。

## 配置之间的连接 [!DNL Experience Manager] as a [!DNL Cloud Service] 和 [!DNL Workfront] {#configure-connection}

创建连接 [!DNL Workfront]，请执行以下步骤：

1. 在 [!DNL Experience Manager]，选择 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**.

1. 选择 `workfront-tools` ，然后选择 **[!UICONTROL 创建]** 选项。

1. 在 **[!UICONTROL Workfront连接]** 对话框中，提供您的 [!DNL Workfront] 部署，然后选择 **[!UICONTROL 连接到Workfront]** 选项。 成功连接后， [!DNL Workfront] 文档自定义集成将在 [!DNL Workfront] 环境。

   ![连接 [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 导航到 **[!UICONTROL 高级]** 选项卡，然后选择选项 **[!UICONTROL 服务器AEM是否as a Cloud Service]**.
