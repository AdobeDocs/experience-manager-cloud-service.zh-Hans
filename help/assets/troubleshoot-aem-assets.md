---
title: AEM Assets中的故障排除
description: 使用关键AEM Assetss=区域（如上传、元数据、搜索、投放等）的文章链接，解决常见AEM Assets问题。
hidefromtoc: true
hide: true
source-git-commit: c8f1c40e4300b26141cc394a9208641769da1f1e
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---


# AEM Assets问题疑难解答 {#troubleshoot-aem-assets}

AEM Assets as a Cloud Service为企业提供了云原生的PaaS解决方案，不仅可用于执行其数字资产管理和Dynamic Media操作，而且还可使用新一代智能功能，如AI/ML。 所有这一切都来自一个始终最新、始终可用和不断学习的系统。

但是，可能会出现影响资源上传、元数据、搜索或投放以及其他AEM Assets关键领域的问题。 本文提供了故障诊断步骤，以帮助您诊断和解决这些常见的AEM Assets问题。

<table>
  <tbody>
  <tr>
    <td>在AEM的资源下载ZIP文件中缺少<a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27140">演绎版</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26616">内容片段未包含在AEM Assets许可证中</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26928">尽管具有读取权限，但在Assets视图中评论受到限制</a> </td> 
    </tr>
    <tr>
    <td>在AEM Dynamic Media<a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26715">中，</a>(Dynamic Media)旋转集停滞在处理状态 </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26639">数字资源管理(DAM)呈现版本与AEM中的原始文件不匹配</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26873">未在AEMaaCS中生成智能裁剪演绎版</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26533">(Dynamic Media)修复了AEM中的视频上传、处理和渲染问题</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26922">(Asset Link) Adobe Asset Link使链接在使用InDesign</a>时保持不可访问状态 </td>
    <td>AEMaaCS中Dynamic Media与DAM卡视图之间的视频缩略图不匹配<a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26677"></a> </td> 
    </tr>
    <tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM as a Cloud Service中大型MP4文件的资源处理失败</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26871">(Dynamic Media) Dynamic Media视频播放器在较低环境中无法正常工作</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26103">（具有OpenAPI的Dynamic Media）使用基于IMS用户组的开放API，激活对Dynamic Media的受限Assets访问</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23916">将采用ZIP压缩格式的Tiff文件上传到AEM Assets时，不会生成演绎版</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM在10万个令牌之后截断从大型PDF提取的文本</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17628">(Dynamic Media)更改DM Assets的Dynamic Media URL</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26655">解决AEMaaCS中非管理员用户的元数据架构可见性问题</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26637">(Dynamic Media) Dynamic Media中TIFF图像演绎版的背景颜色更改问题</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26528">AEMaaCS资产轮换问题使后续轮换不可见</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26367">(Dynamic Media)解决Adobe Experience Manager 6.5 Dynamic Media中的智能裁剪损坏的图像问题</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26450">提高Photoshop Firefly API集成的单部分资源上传限制</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26461">(Dynamic Media)解决PDF文件在AEM环境中存在的Dynamic Media资源名称差异</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26233">某些图像在Adobe Experience Manager (AEM) as a Cloud Service - Asset中不显示缩略图演绎版</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25294">(Dynamic Media)“Dynamic Media常规设置”页面未打开</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26197">(Dynamic Media)在AEM中使用Dynamic Media解决视频文件中的音频问题</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25925">在AEM as a Cloud Service中自动标记新上传的资源</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25889">在AEM中将JWT迁移到OAuth后，智能标记功能不起作用</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25903">解决AEM Managed Services中的共享链接问题</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25607">(Dynamic Media) AEM Dynamic Media中的资源处理失败</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25885">(Dynamic Media) Adobe Experience Manager (AEM) Dynamic Media中的资源同步失败</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25829">在AEM as a Cloud Service中更新视频资源的自定义缩略图</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25828">Adobe Experience Manager (AEM) Assets中的图像元数据差异</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21865">将资源文件夹拖放到AEM Assets Web UI失败</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25525">(Dynamic Media)解决AEM as a Cloud Service中的资源处理问题</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25518">Adobe Experience Manager as a Cloud Service中大型PDF的文本提取限制</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25562">(Asset Link)解决InDesign中的Adobe Experience Manager (AEM) asset Link连接问题</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25506">(Asset Link) Adobe Asset Link插件网络错误：无法访问服务器</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25471">(Dynamic Media) Dynamic Media同步用户建议</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26902">(Dynamic Media)使用API从Dynamic Media导出资源和元数据</a></td>
  <td></td>
</tr>

</tbody>
  <table>


