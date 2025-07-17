---
title: 优化HTML5表单
description: 您可以优化HTML5表单的输出大小。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: HTML5 Forms,Mobile Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 优化HTML5表单 {#optimizing-html-forms}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

HTML5表单以HTML5格式呈现表单。 根据窗体大小和窗体中的图像等因素，生成的输出可能会很大。 为了优化数据传输，建议的方法是使用为请求提供服务的Web服务器压缩HTML响应。 此方法可减少响应大小、网络流量以及在服务器和客户端计算机之间流式传输数据所需的时间。

本文介绍了使用JBoss为Apache Web Server 2.0 32位启用压缩所需的步骤。

>[!NOTE]
>
>以下说明不适用于32位Apache Web Server 2.0以外的服务器。

获取适用于您的操作系统的Apache Web Server软件：

* 对于Windows，请从Apache HTTP Server项目站点下载Apache Web Server。
* 对于Solaris 64位，请从Sunfreeware for Solaris网站下载Apache Web Server。
* 对于Linux，Apache Web Server预安装在Linux系统上。

Apache可以使用HTTP或AJP协议与JBoss通信。

1. 在&#x200B;*APACHE_HOME/conf/httpd.conf*&#x200B;文件中取消注释以下模块配置。

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >对于Linux，默认的APACHE_HOME目录为/etc/httpd/。

1. 在JBoss的端口8080上配置代理。

   将以下配置添加到&#x200B;*APACHE_HOME/conf/httpd.conf*&#x200B;配置文件。

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >使用代理时，需要进行以下配置更改：
   >
   >* 访问： *https://&lt;服务器>：&lt;端口>/system/console/configMgr*
   >* 编辑Apache Sling引用过滤器配置
   >* 在允许主机中，添加代理服务器的条目

1. 启用压缩。

   将以下配置添加到&#x200B;*APACHE_HOME/conf/httpd.conf*&#x200B;配置文件。

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don't compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. 要访问AEM服务器，请使用https://[Apache_server]：80。
