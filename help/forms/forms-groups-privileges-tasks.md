---
title: 内置 [!DNL AEM Forms] as a Cloud Service组
description: 现成用户组和分配给每个组的权限列表
exl-id: bd66ce92-14d9-47fe-b5d3-022e3e468d25
source-git-commit: d67e46e2f798e56e322d5c4aad536e718c7aae1a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 5%

---

# 组和权限 {#aem-forms-on-osgi-groups-and-privileges}

您可以 [创建组](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) 并分配策略和 [用户](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) 组。 这些策略控制属于组的用户的权限。

设置后 [!DNL AEM Forms] as a Cloud Service，下表所列的组，例如 [!DNL forms-users] 和Forms-power用户，可自动进行分配：

<table>
 <tbody>
  <tr>
   <td>组</td> 
   <td>权限</td> 
  </tr>
  <tr>
   <td>[!DNL forms-users] <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>创建、预览、发布和提交自适应Forms</li> 
    <!-- <li>Create, preview, and publish interactive communications and document fragments</li> -->
     <li>将资产上传到AEM实例</li> 
     <li>创建主题</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL forms-power-user]</td> 
   <td>
    <ul> 
     <li>创建、预览、发布和提交自适应Forms</li> 
     <!-- <li>Create, preview, and publish interactive communications and document fragments</li> 
     <li>Create scripts for Adaptive Forms using code editor</li> -->
     <li>上传资产（包括脚本）</li> 
     <li>创建主题</li> 
     <li>导入包含XDP的包</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Review submissions</li> 
     <li>Approve or reject submissions</li> 
    </ul> </td> 
  </tr> -->
  <tr>
   <td>[!DNL template-authors] <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>创建和预览自适应Forms <!-- or interactive communications --> 模板</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>[!DNL fdm-authors]</p> </td> 
   <td>
    <ul> 
     <li>创建和修改表单数据模型</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Access Correspondence Management letters or interactive communications using Agent UI</li> 
    </ul> </td> 
  </tr> --> 
  <!-- <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> -->
    <!-- <li>Create an inbox application</li>  -->
    <!-- <li>Create a workflow model</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL workflow-users]</td> 
   <td>
    <ul> 
     <li>Use AEM inbox applications<br /> -->
     <!-- 
     <strong>Note: </strong>You must have cm-agent-users and [!DNL workflow-users] group assignments to access Interactive Communications Agent UI in AEM inbox.</li>  -->
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL fd-administrators]</td> 
   <td>
    <ul> 
     <!-- <li>Configure PDF Generator</li> --> 
     <!-- <li>Configure Watched folder</li> -->
     <li>管理工作流应用程序</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>
