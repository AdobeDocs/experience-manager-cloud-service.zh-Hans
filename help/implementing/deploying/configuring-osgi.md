---
title: 为Adobe Experience Manager as a Cloud Service配置OSGi
description: 具有机密值和特定于环境的值的OSGi配置
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
role: Admin
source-git-commit: 1289da67452be7fc0fa7f3126d2a3dbf051aa9b5
workflow-type: tm+mt
source-wordcount: '3321'
ht-degree: 1%

---


# 为Adobe Experience Manager as a Cloud Service配置OSGi {#configuring-osgi-for-aem-as-a-cloud-service}

[OSGi](https://www.osgi.org/)是Adobe Experience Manager (AEM)技术栈栈中的基本元素。 它用于控制AEM的复合捆绑包及其配置。

OSGi提供了标准化的基元，允许从小型、可重用的协作组件构建应用程序。 这些组件可以组合为一个应用程序并进行部署。 这样可以轻松地管理OSGi包，因为它们可以单独停止、安装和启动。 系统会自动处理相互依赖关系。 每个OSGi组件都包含在各种捆绑包中。 有关详细信息，请参阅[OSGi规范](https://help.eclipse.org/latest/index.jsp)。

您可以通过属于AEM代码项目一部分的配置文件来管理OSGi组件的配置设置。

>[!TIP]
>
>您可以使用Cloud Manager配置环境变量。 有关详细信息，请参阅[此处](/help/implementing/cloud-manager/environment-variables.md)的文档。

## OSGi配置文件 {#osgi-configuration-files}

配置更改在AEM项目的代码包(`ui.config`)中定义为运行模式特定的配置文件夹下的配置文件(`.cfg.json`)：

`/apps/example/config.<runmode>`

OSGi配置文件的格式基于JSON，使用Apache Sling项目定义的`.cfg.json`格式。

OSGi配置通过组件的永久标识(PID)来定位OSGi组件，该PID默认为OSGi组件的Java™类名称。 例如，为通过以下方式实施的OSGi服务提供OSGi配置：

`com.example.workflow.impl.ApprovalWorkflow.java`

在以下位置定义OSGi配置文件：

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

遵循`cfg.json` OSGi配置格式。

>[!NOTE]
>
>早期版本的AEM支持的OSGi配置文件使用不同的文件格式，如`.cfg`、`.config`和XML `sling:OsgiConfig`资源定义。 这些格式已被`.cfg.json` OSGi配置格式取代。

>[!NOTE]
>
>OSGi配置并不像云中的典型AEM实例那样存储在/apps下，而是存储在外部位置。 签入Cloud Manager [Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#configurations)以查看OSGi配置。

## 运行模式分辨率 {#runmode-resolution}

>[!TIP]
>
>AEM 6.x支持自定义运行模式，但AEM as a Cloud Service不支持。 AEM as a Cloud Service支持[完全一组运行模式](./overview.md#runmodes)。 必须使用[OSGi配置环境变量](#environment-specific-configuration-values)处理AEM as a Cloud Service环境之间的OSGi配置中的任何变化。

可以使用运行模式将特定OSGi配置定位到特定AEM实例。 要使用runmode，请在`/apps/example`下创建配置文件夹（例如，您的项目名称），格式为：

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

如果配置文件夹名称中定义的运行模式与AEM使用的运行模式匹配，则使用此类文件夹中的任何OSGi配置。

例如，如果AEM使用运行模式创作和开发，则应用`/apps/example/config.author/`和`/apps/example/config.author.dev/`中的配置节点，而不应用`/apps/example/config.publish/`和`/apps/example/config.author.stage/`中的配置节点。

如果同一PID有多个配置适用，则应用匹配运行模式数最多的配置。

此规则的粒度处于PID级别。 这意味着您不能在`/apps/example/config.author/`中为同一PID定义某些属性，也不能在`/apps/example/config.author.dev/`中为同一PID定义更具体的属性。 匹配运行模式数最高的配置对整个PID有效。

>[!NOTE]
>
>`config.preview` OSGi配置文件夹&#x200B;**无法以声明`config.publish`文件夹的方式进行声明**。 相反，预览层从发布层的值继承其OSGi配置。

在进行本地开发时，运行架构启动参数 `-r` 用于指定运行架构 OSGI 配置。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### 验证运行模式

AEM as a Cloud Service运行模式根据环境类型和服务进行良好的定义。 查看可用AEM as a Cloud Service运行模式的[完整列表](./overview.md#runmodes)。

可以通过以下方式验证由运行模式指定的OSGi配置值：

1. 正在打开AEM as a Cloud Service环境的[Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html)
1. 使用&#x200B;__Pod__&#x200B;下拉列表选择要检查的服务层
1. 选择&#x200B;__状态__&#x200B;选项卡
1. 从&#x200B;__状态转储__&#x200B;下拉列表中选择&#x200B;__配置__
1. 选择&#x200B;__获取状态__&#x200B;按钮

结果视图将显示选定层的所有OSGi组件配置及其适用的OSGi配置值。 这些值可以与AEM项目源代码中`/apps/example/osgiconfig/config.<runmode(s)>`下的OSGi配置值交叉引用。


要验证是否应用了适当的OSGi配置值，请执行以下操作：

1. 在Developer Console的配置输出中
1. 找到表示要验证的OSGi配置的`pid`；这是AEM项目源代码中的OSGi配置文件的名称。
1. Inspect `pid`的`properties`列表，并验证键和值是否与正在验证运行模式的AEM项目源代码中的OSGi配置文件匹配。


## OSGi配置值的类型 {#types-of-osgi-configuration-values}

有三种类型的OSGi配置值可以与Adobe Experience Manager as a Cloud Service一起使用。

1. **内联值**，这些值已硬编码到OSGi配置中并存储在Git中。 例如：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **密码值**，出于安全原因，这些值不能存储在Git中。 例如：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **特定于环境的值**，这些值在开发环境之间有所不同，因此无法通过运行模式准确地定位这些值(因为Adobe Experience Manager as a Cloud Service中存在单个`dev`运行模式)。 例如：

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   单个OSGi配置文件可以结合使用这些配置值类型的任意组合。 例如：

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 如何选择适当的OSGi配置值类型 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi的常见用例使用内联OSGi配置值。 特定于环境的配置仅用于开发环境之间的值不同的特定用例。

![有关如何使用适当配置值类型的决策树](assets/choose-configuration-value-type_res1.png)

特定环境的配置扩展了包含内联值的静态定义的传统OSGi配置，提供了通过Cloud Manager API从外部管理OSGi配置值的功能。 了解何时使用定义内联值并将其存储在Git中的常见传统方法以及何时将值抽象为特定于环境的配置非常重要。

以下指南介绍了何时使用特定于非机密和机密环境的配置：

### 何时使用内联配置值 {#when-to-use-inline-configuration-values}

内联配置值被视为标准方法，应尽可能使用。 内联配置具有以下优势：

* 它们会进行维护，在Git中具有治理和版本历史记录
* 值隐式绑定到代码部署
* 它们不需要任何其他部署考虑或协调

无论何时定义OSGi配置值，都从内联值开始，并且仅当用例需要时才选择机密或特定于环境的配置。

### 何时使用非机密环境特定的配置值 {#when-to-use-non-secret-environment-specific-configuration-values}

当预览层的值不同或开发环境的值不同时，仅将特定于环境的配置(`$[env:ENV_VAR_NAME]`)用于非机密配置值。 这包括本地开发实例和任何Adobe Experience Manager as a Cloud Service开发环境。 除了为预览层设置唯一值之外，请避免为Adobe Experience Manager as a Cloud Service暂存或生产环境使用非机密环境特定的配置。

* 仅将特定于非机密环境的配置用于发布层和预览层之间不同的配置值，或用于开发环境（包括本地开发实例）之间不同的值。
* 除了预览层必须不同于发布层的方案外，请在OSGi配置中为暂存和生产非机密值使用标准内联值。 因此，不建议使用特定于环境的配置来促进在运行时对暂存环境和生产环境进行配置更改；这些更改应通过源代码管理引入。

### 何时使用特定于机密环境的配置值 {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service要求对任何机密OSGi配置值（如密码、私有API密钥或出于安全原因不能存储在Git中的任何其他值）使用特定于环境的配置(`$[secret:SECRET_VAR_NAME]`)。

使用特定于密钥环境的配置来存储所有Adobe Experience Manager as a Cloud Service环境（包括暂存环境和生产环境）上的密钥值。

## 创建OSGi配置 {#creating-osgi-configurations}

创建OSGi配置的方法有两种，如下所述。 前者通常用于配置自定义OSGi组件，这些组件具有开发人员已知的OSGi属性和值，而后者则用于AEM提供的OSGi组件。

### 编写OSGi配置 {#writing-osgi-configurations}

JSON格式的OSGi配置文件可以直接在AEM项目中手动编写。 这通常是为已知的OSGi组件（尤其是由定义配置的同一开发人员设计和开发的自定义OSGi组件）创建OSGi配置的最快方法。 此方法还可用于在不同的运行模式文件夹中复制/粘贴和更新同一OSGi组件的配置。

1. 在IDE中，打开`ui.apps`项目，找到或创建配置文件夹(`/apps/.../config.<runmode>`)，该文件夹针对新OSGi配置需要生效的运行模式
1. 在此配置文件夹中，创建一个`<PID>.cfg.json`文件。 PID是OSGi组件的永久标识。 它通常是OSGi组件实现的完整类名。 例如：
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
OSGi配置工厂文件名使用`<factoryPID>-<name>.cfg.json`命名约定
1. 打开新的`.cfg.json`文件，并按照[JSON OSGi配置格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)定义OSGi属性和值对的键/值组合。
1. 将更改保存到新的`.cfg.json`文件
1. 添加新的OSGi配置文件并将其提交到Git

### 使用AEM SDK快速入门生成OSGi配置 {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK快速入门Jar的AEM Web控制台可用于配置OSGi组件，并将OSGi配置导出为JSON。 这对于配置AEM提供的OSGi组件非常有用，在AEM项目中定义OSGi配置的开发人员可能无法很好地了解这些组件的OSGi属性及其值格式。

>[!NOTE]
>
>AEM Web控制台的配置UI确实将`.cfg.json`文件写入存储库。 因此，请注意，当AEM项目定义的OSGi配置可能与生成的配置不同时，此工作流可避免在本地开发期间潜在的意外行为。

1. 以管理员用户身份登录到位于`https://<host>:<port>/system/console`的AEM SDK快速入门Jar的AEM Web控制台
1. 导航到&#x200B;**OSGi** > **配置**
1. 要进行配置，请找到OSGi组件并选择要编辑的其标题
   ![OSGi配置](./assets/configuring-osgi/configuration.png)
1. 根据需要通过Web UI编辑OSGi配置属性值
1. 将永久标识(PID)记录到安全位置。 这稍后将用于生成OSGi配置JSON
1. 选择保存
1. 导航到OSGi > OSGi安装程序配置打印机
1. 粘贴步骤5中复制的PID，确保序列化格式设置为“OSGi配置器JSON”
1. 选择打印
1. JSON格式的OSGi配置将显示在序列化配置属性部分中
   ![OSGi安装程序配置打印机](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. 在IDE中，打开`ui.apps`项目，找到或创建配置文件夹(`/apps/.../config.<runmode>`)，该文件夹针对新OSGi配置需要生效的运行模式。
1. 在此配置文件夹中，创建一个`<PID>.cfg.json`文件。 PID与步骤5中的值相同。
1. 将步骤10中的序列化配置属性粘贴到`.cfg.json`文件中。
1. 将更改保存到新的`.cfg.json`文件。
1. 添加新的OSGi配置文件并将其提交到Git。


## OSGi配置属性格式 {#osgi-configuration-property-formats}

### 内联值 {#inline-values}

内联值的格式为标准的名称 — 值对，遵循标准JSON语法。 例如：

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 特定于环境的配置值 {#environment-specific-configuration-values}

OSGi配置应为打算按环境定义的变量分配占位符：

```
use $[env:ENV_VAR_NAME]
```

客户应仅将此技术用于与其自定义代码相关的OSGi配置属性；不得使用此技术覆盖Adobe定义的OSGi配置。

>[!NOTE]
>
>占位符不能在[repoinit语句](/help/implementing/deploying/overview.md#repoinit)中使用。

### 密码配置值 {#secret-configuration-values}

OSGi配置应为要按环境定义的密钥分配一个占位符：

```
use $[secret:SECRET_VAR_NAME]
```

### 变量命名 {#variable-naming}

以下内容适用于特定于环境的配置值和机密配置值。

变量名称必须遵循以下规则：

* 最小长度：2
* 最大长度：100
* 必须匹配正则表达式： `[a-zA-Z_][a-zA-Z_0-9]*`

变量值不得超过2048个字符。

>[!CAUTION]
>
>有些规则与对变量名称使用某些前缀有关：
>
>1. 以`INTERNAL_`、`ADOBE_`或`CONST_`为前缀的变量名称由Adobe保留。 以这些前缀开头的任何客户设置变量都将被忽略。
>
>1. 客户也不能引用前缀为`INTERNAL_`或`ADOBE_`的变量。
>
>1. 前缀为`AEM_`的环境变量由产品定义为供客户使用和设置的公共API。
>   虽然客户可以使用和设置以前缀`AEM_`开头的环境变量，但他们不应使用此前缀定义自己的变量。

### 默认值 {#default-values}

以下内容适用于特定于环境的配置值和机密配置值。

如果未设置每个环境的值，则运行时不会替换占位符，并且由于没有发生插值，占位符将保留在原位。 为了避免这种情况，可以使用以下语法将默认值作为占位符的一部分提供：

```
$[env:ENV_VAR_NAME;default=<value>]
```

在提供了默认值的情况下，占位符会被替换为每个环境的值（如果提供）或提供的默认值。

### 本地开发 {#local-development}

以下内容适用于特定于环境的配置值和机密配置值。

变量可以在本地环境中定义，以便在运行时由本地AEM接收。 例如，在Linux®上：

```bash
export ENV_VAR_NAME=my_value
```

建议编写简单的bash脚本，以设置配置中使用的环境变量，并在启动AEM之前执行它。 诸如[https://direnv.net/](https://direnv.net/)之类的工具有助于简化此方法。 根据值的类型，如果这些值可以在所有人之间共享，则它们可能会被签入源代码管理。

从文件中读取密钥的值。 因此，对于使用密码的每个占位符，必须创建包含密码值的文本文件。

例如，如果使用`$[secret:server_password]`，则必须创建名为&#x200B;**server_password**&#x200B;的文本文件。 所有这些机密文件必须存储在同一目录中，并且框架属性`org.apache.felix.configadmin.plugin.interpolation.secretsdir`必须使用该本地目录进行配置。

>[!CAUTION]
>
>文本文件不允许使用文件扩展名。
>
>因此，对于上述示例，必须将该文本文件命名为&#x200B;**server_password** — 不带文件扩展名。

`org.apache.felix.configadmin.plugin.interpolation.secretsdir`是Sling框架属性；因此此属性不是在felix控制台(/system/console)中设置的，而是在系统引导时使用的sling.properties文件中设置的。 此文件可在提取的Jar/install文件夹(crx-quickstart/conf)的/conf子目录中找到。

示例：将此行添加到“crx-quickstart/conf/sling.properties”文件的末尾以将“crx-quickstart/secretsdir”配置为机密文件夹：

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### 作者与Publish配置 {#author-vs-publish-configuration}

如果OSGi属性对于创作与发布所需的值不同：

* 必须使用单独的`config.author`和`config.publish` OSGi文件夹，如[运行模式解析部分](#runmode-resolution)中所述。
* 创建独立变量名称有两种选项，应使用：
   * 推荐使用的第一个选项：在声明为定义不同值的所有OSGi文件夹（如`config.author`和`config.publish`）中，使用相同的变量名称。 例如
     `$[env:ENV_VAR_NAME;default=<value>]`，其中默认值对应于该层的默认值（创作或发布）。 在通过[Cloud Manager API](#cloud-manager-api-format-for-setting-properties)或通过客户端设置环境变量时，请按照[Cloud Manager API参考文档](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)中的说明，使用“服务”参数区分各个层。 “service”参数会将变量的值绑定到适当的OSGi层。 它可以是“创作”、“发布”或“预览”。
   * 第二个选项是使用前缀（如`author_<samevariablename>`和`publish_<samevariablename>`）声明不同的变量

### 配置示例 {#configuration-examples}

在下面的示例中，假设除了暂存环境和生产环境之外，还有三个开发环境。

**示例 1**

目的是使OSGi属性`my_var1`的值对于stage和prod是相同的，但三个开发环境的每个值都不同。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的内容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ 
 "my_var1"： "val"，
 "my_var2"： "abc"，
 "my_var3"：500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" ： "$[env：my_var1]"
 "my_var2"： "abc"，
 "my_var3"：500
}
</pre>
</td>
</tr>
</table>

**示例 2**

目的是使OSGi属性`my_var1`的值在暂存、生产和三个开发环境的每个中有所不同。 因此，必须调用Cloud Manager API为每个开发环境设置`my_var1`的值。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的内容</b>
</td>
</tr>
<tr>
<td>
config.stage
</td>
<td>
<pre>
{ 
 "my_var1"： "val1"，
 "my_var2"： "abc"，
 "my_var3"：500
}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ 
 "my_var1"： "val2"，
 "my_var2"： "abc"，
 "my_var3"：500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" ： "$[env：my_var1]"
 "my_var2"： "abc"，
 "my_var3"：500
}
</pre>
</td>
</tr>
</table>

**示例 3**

目的是使OSGi属性`my_var1`的值对于暂存、生产和仅其中一个开发环境是相同的，但对于其他两个开发环境不同。 在这种情况下，必须调用Cloud Manager API为每个开发环境（包括应与暂存和生产环境具有相同值的开发环境）设置`my_var1`值。 它不会继承文件夹&#x200B;**config**&#x200B;中设置的值。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的内容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ 
 "my_var1"： "val1"，
 "my_var2"： "abc"，
 "my_var3"：500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" ： "$[env：my_var1]"
 "my_var2"： "abc"，
 "my_var3"：500
}
</pre>
</td>
</tr>
</table>

完成此任务的另一种方法是为config.dev文件夹中的替换令牌设置默认值，使其与&#x200B;**config**&#x200B;文件夹中的值相同。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的内容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ 
 "my_var1"： "val1"，
 "my_var2"： "abc"，
 "my_var3"：500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1"： "$[env：my_var1；default=val1]"
 "my_var2"： "abc"，
 "my_var3"：500
}
</pre>
</td>
</tr>
</table>

## 用于设置属性的Cloud Manager API格式 {#cloud-manager-api-format-for-setting-properties}

有关Cloud Manager API以及应如何配置的信息，请参阅[在Adobe Developer网站上AdobeCloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/docs/)。

>[!NOTE]
>
>确保使用的Cloud Manager API已分配“部署管理员 — Cloud Service”角色。 其他角色无法执行以下所有命令。

>[!TIP]
>
>您还可以使用Cloud Manager配置环境变量。 有关详细信息，请参阅[Cloud Manager环境变量](/help/implementing/cloud-manager/environment-variables.md)。

### 通过API设置值 {#setting-values-via-api}

调用API会将新变量和值部署到云环境，类似于典型的客户代码部署管道。 创作和发布服务将重新启动并引用新值，通常需要几分钟的时间。

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```json
[
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

>[!NOTE]
>默认变量不是通过API设置的，而是在OSGi属性本身中设置的。
>
>有关详细信息，请参阅[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)。

### 通过API获取值 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

有关详细信息，请参阅[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)。

### 通过API删除值 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

要删除变量，请将其包含在空值中。

有关详细信息，请参阅[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)。

### 通过命令行获取值 {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### 通过命令行设置值 {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### 通过命令行删除值 {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>有关如何使用Cloud Manager插件为Adobe I/OCLI配置值的更多信息，请参阅GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)上的[aio-cli-plugin-cloudmanager 。

### 变量数 {#number-of-variables}

每个环境最多可以声明200个变量。

## 针对密钥和特定于环境的配置值的部署注意事项 {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

由于机密和特定于环境的配置值位于Git之外，因此不属于正式的Adobe Experience Manager as a Cloud Service部署机制，因此客户应该管理、治理并集成到Adobe Experience Manager as a Cloud Service部署过程中。

如上所述，调用API会将新变量和值部署到云环境，类似于典型的客户代码部署管道。 创作和发布服务将重新启动并引用新值，通常需要几分钟的时间。 在此过程中，不会执行在常规代码部署期间由Cloud Manager运行的质量审核和测试。

通常，客户在部署在Cloud Manager中依赖于环境变量的代码之前，会调用API来设置这些变量。 在某些情况下，可能需要在部署代码后修改现有变量。

>[!NOTE]
>
>当管道正在使用中(AEM更新或客户部署)时，API可能会失败，具体取决于当时正在执行的端到端管道的部分。 错误响应将指示请求不成功，但不会指示具体原因。

在某些情况下，计划客户代码部署依赖现有变量才能具有新值，而该值不适用于当前代码。 如果这是一个问题，建议以累加方式进行变量修改。 为此，请创建新的变量名称，而不是只更改旧变量的值，这样旧代码永远不会引用新值。 然后，当新客户版本看起来稳定时，您可以选择删除旧值。

同样，由于变量的值未进行版本控制，因此代码回滚可能会导致它引用导致问题的较新值。 前面提到的加性变量策略也会对此有所帮助。

此附加变量策略也可用于灾难恢复情况，在这些情况中，如果需要重新部署前几天生成的代码，则它引用的变量名称和值将保持不变。 这依赖于一种策略，即客户在删除这些旧变量之前等待几天，否则旧代码将没有合适的变量可引用。
