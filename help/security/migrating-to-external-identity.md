---
title: 迁移到外部标识和动态组成员资格
description: 在AEM as a Cloud Service中将本地用户和组迁移到具有动态组成员资格的外部身份模型的技术指南
solution: Experience Manager Sites
feature: Security
role: Developer, Admin
source-git-commit: 1f8bd9eea249e0b2242f3fbe1490b3d51052f546
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 1%

---

# 迁移到外部标识和动态组成员资格 {#migrating-to-external-identity}

## 概述 {#overview}

在AEM as a Cloud Service中启用[数据同步](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md#data-synchronization)后，可以将SAML身份验证处理程序配置为在管理用户和组创建时自动迁移到具有动态组成员资格的外部身份。 如果您的项目使用自定义代码创建用户或组，则必须更新它以创建外部用户和组，而不是本地用户和组。

### 为什么需要外部用户和组 {#why-external-required}

出于以下几个关键原因，从本地用户和组迁移到具有动态组成员资格的外部身份至关重要：

**性能优化：**

* **减少的存储库写入次数**：传统的本地组成员资格要求将成员资格关系写入组节点的单个多值属性中的存储库。 使用动态组成员资格时，用户具有包含所有组承担者的单个`rep:externalPrincipalNames`属性，从而无需同步组节点
* **同步速度更快**：在同步发布层节点间的用户时，具有动态组成员资格的外部用户所需的数据传输和写入操作都比具有传统组成员资格的本地用户少得多
* **可扩展性**：具有大量用户和组的系统从降低的存储库开销中受益匪浅。 即使对于非常大的组，动态组成员资格也可以高效地扩展。

本文档提供了以下方面的技术指导：

* 了解外部身份模型
* 修改自定义代码以创建外部用户和组
* 将现有本地用户和组迁移到外部身份模型

## 了解外部身份 {#understanding-external-identity}

### 外部用户 {#external-users}

外部用户由`rep:externalId`属性标识，该属性将用户链接到外部身份提供程序。 格式为：

```
userId;idpName
```

例如：`john.doe;saml-idp`。

>[!NOTE]
>
> `idpName`引用身份验证处理程序配置中定义的Oak身份提供程序(Idp)的名称。 对于SAML集成，这是SAML身份验证处理程序中为`idpIdentifier`属性设置的值。

**键属性：**

* `rep:externalId`：将用户标记为外部的必需属性（例如，`john.doe;saml-idp`）
* `rep:externalPrincipalNames`：包含动态成员资格的外部组主体的多值属性
* `rep:lastSynced`：上次同步的时间戳
* `rep:lastDynamicSync`：上次动态组成员资格同步的时间戳

### 外部组 {#external-groups}

外部组也由`rep:externalId`属性标识，并使用主体名称格式：

```
groupId;idpName
```

例如：`content-authors;saml-idp`

### 动态组成员资格 {#dynamic-group-membership}

动态组成员资格使用用户节点上的`rep:externalPrincipalNames`属性，而不是存储在存储库中的直接用户到组关系。 当用户具有与外部组的ID匹配的外部主体名称时，他们会自动成为该组的成员。 有关详细信息，请参阅[Apache Oak文档](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html)。

**优势：**

* 减少了存储库写入次数（在组中添加或删除用户时，不会修改组成员资格节点）
* 加快跨发布层节点的同步
* 可扩展的组成员资格管理
* 与数据同步要求兼容

## 服务用户配置 {#service-user-configuration}

所有创建或修改外部用户和组的操作都应使用正确配置为绕过&#x200B;**和**&#x200B;属性上的默认保护的`rep:externalId`服务用户`rep:externalPrincipalNames`来执行。

### 为什么需要服务用户 {#why-is-a-service-user-required}

默认情况下，Oak安全保护会阻止常规会话修改受保护的属性，例如：

* `rep:externalId` — 将用户/组标记为外部
* `rep:externalPrincipalNames` — 存储动态组成员资格主体

只有正确配置的服务用户才能修改这些属性。

### 服务用户配置和映射 {#service-user-configuration-mapping}

设置服务用户以管理外部身份需要三个协调的配置：

1. 通过`repoinit`创建服务用户
2. 配置`ExternalPrincipal`保护
3. 将服务用户映射到您的应用程序捆绑包。

有关这些步骤的详细说明，请参阅下文。

#### 步骤1：通过Repoinit创建服务用户 {#create-the-serviice-user-via-repoinit}

此步骤详细说明如何使用`repoinit`脚本创建具有必要权限的服务用户。

**配置文件：** `org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json`

**示例位置：** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "scripts": [
    "create service user group-provisioner with path system/yourproject",
    "set ACL for group-provisioner\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/users\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/groups\nend"
  ]
}
```

**权限概述**

* `jcr:read`：读取用户和组
* `jcr:readAccessControl`：读取ACL
* `jcr:modifyAccessControl`：修改ACL（设置属性所需）
* `rep:userManagement`：创建和管理用户/组
* `rep:write`：写入包括`rep:externalId`和`rep:externalPrincipalNames`的属性

>[!NOTE]
>
>服务用户是在`/home/users/system/yourproject`下创建的，以便与其他系统用户保持其组织性。

#### 步骤2：配置ExternalPrincipal保护 {#configure-externalprincipal-protection}

以下是用于将服务用户列入白名单的示例配置，这样它可以绕过应用于外部标识属性的保护。

**配置文件名：** `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json`

**示例位置：** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "protectExternalIdentities": "Warn",
  "systemPrincipalNames": [
    "group-provisioner",
    "saml-migration-service"
  ]
}
```

**配置属性：**

* `protectExternalIdentities`：控制外部标识属性的保护级别：
   * `"Strict"`：只有白名单中的系统主体才能修改外部属性。 这是为生产推荐的级别。
   * `"Warn"`：记录警告，但允许修改。 对于开发/测试非常有用。
   * `"None"`：无保护。 不推荐。
* `systemPrincipalNames`：允许修改`rep:externalId`和`rep:externalPrincipalNames`的服务用户名列表。 包括需要管理外部标识的所有服务用户（例如，`group-provisioner`、`saml-migration-service`）。

>[!IMPORTANT]
>
>`systemPrincipalNames`中的服务用户名必须与在repoinit脚本中创建的服务用户ID完全匹配。

#### 步骤3：服务用户映射 {#service-user-mapping}

将服务用户映射到您的应用程序捆绑包，以便您的代码可以使用该服务用户。

**配置文件：** `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json`

**位置：** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "user.mapping": [
    "yourproject.core:group-provisioner=[group-provisioner]"
  ]
}
```

**映射格式：**

* `yourproject.core`：符号包名称（在`pom.xml` `<Bundle-SymbolicName>`中找到）
* `group-provisioner` （在`=`之前）：将在代码中使用的子服务名称
* `[group-provisioner]` （在`=`之后）：在repoinit中创建的实际服务用户ID

### 在代码中使用服务用户 {#using-the-service-user-in-code}

打开会话以执行迁移或用户/组创建操作时，必须使用服务用户：

```java
import org.apache.sling.jcr.api.SlingRepository;

@Reference
private SlingRepository repository;

// Login as the service user
Session serviceSession = repository.loginService("group-provisioner", null);

try {
    UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
    // Perform operations...
    serviceSession.save();
} finally {
    if (serviceSession != null && serviceSession.isLive()) {
        serviceSession.logout();
    }
}
```

>[!IMPORTANT]
>
>如果没有正确的服务用户配置，设置`rep:externalId`或`rep:externalPrincipalNames`的尝试将失败，并出现权限错误。 在尝试迁移之前，请确保已在`ExternalPrincipal`配置中正确配置您的服务用户。

## 完整配置示例 {#complete-configuration-example}

下面是一个完整的工作示例，其中显示了所有三种配置：

### 文件结构 {#file-structure}

```
ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/
└── config.publish/
    ├── org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json
    ├── org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json
    └── org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json
```

### 修改自定义代码 {#modifying-custom-code}

#### 创建外部用户 {#creating-external-users}

**之前（本地用户）：**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
User user = userManager.createUser(userId, password);
```

**之后（外部用户）：**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create user with principal
Principal userPrincipal = new Principal() {
    @Override
    public String getName() {
        return userId;
    }
};

User user = userManager.createUser(userId, null, userPrincipal, null);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
String externalId = externalRef.getString(); // Format: userId;idpName
user.setProperty("rep:externalId", valueFactory.createValue(externalId));

// Set sync timestamps to far future (workaround for OAK-12079)
// Set to 10 years in the future to prevent premature cleanup of external group memberships
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));

session.save();
```

#### 创建外部组 {#creating-external-groups}

**之前（本地组）：**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
Group group = userManager.createGroup(groupId);
```

**之后（外部组）：**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create group with principal
Principal groupPrincipal = new Principal() {
    @Override
    public String getName() {
        return groupId;
    }
};

Group group = userManager.createGroup(groupPrincipal);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(groupId, idpName);
String externalId = externalRef.getString(); // Format: groupId;idpName
group.setProperty("rep:externalId", valueFactory.createValue(externalId));

session.save();
```

#### 分配动态组成员资格 {#assigning-dynamic-membership}

**之前（直接成员资格）：**

```java
Group group = (Group) userManager.getAuthorizable(groupId);
User user = (User) userManager.getAuthorizable(userId);
group.addMember(user);
```

**之后（动态成员资格）：**

```java
User user = (User) userManager.getAuthorizable(userId);
ValueFactory valueFactory = session.getValueFactory();

// Get existing external principal names
Value[] existingValues = user.getProperty("rep:externalPrincipalNames");
List<String> principalNames = new ArrayList<>();

if (existingValues != null) {
    for (Value value : existingValues) {
        principalNames.add(value.getString());
    }
}

// Add new principal name (format: groupId;idpName)
String dynamicGroupPrincipal = groupId + ";" + idpName;
if (!principalNames.contains(dynamicGroupPrincipal)) {
    principalNames.add(dynamicGroupPrincipal);
    
    // Create new Value array
    Value[] newValues = new Value[principalNames.size()];
    for (int i = 0; i < principalNames.size(); i++) {
        newValues[i] = valueFactory.createValue(principalNames.get(i));
    }
    
    // Set the property
    user.setProperty("rep:externalPrincipalNames", newValues);
    
    // Update sync timestamps to far future (workaround for OAK-12079)
    // Set to 10 years in the future to prevent premature cleanup of external group memberships
    // See: https://issues.apache.org/jira/browse/OAK-12079
    java.util.Calendar future = java.util.Calendar.getInstance();
    future.add(java.util.Calendar.YEAR, 10);
    user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
    user.setProperty("rep:lastSynced", valueFactory.createValue(future));
}

session.save();
```

## 迁移过程 {#migration-process}

在启用Data Synchronization Services之前更新自定义代码时，不需要将现有本地用户和组迁移到外部身份。

如果本地用户和组已保留在存储库中并且环境被主动使用，我们建议您执行类似于以下内容的多步迁移，以避免中断或不一致。

>[!IMPORTANT]
>
>必须使用正确配置的服务用户（例如`group-provisioner`）执行所有迁移步骤，该用户已被授予绕过`rep:externalId`和`rep:externalPrincipalNames`属性的保护的权限。 有关详细信息，请参阅[服务用户配置](#service-user-configuration)。

### 步骤1：创建外部组结构 {#step-1-create-external-group-structure}

对于需要迁移的每个本地组：

1. 创建具有主体名称的相应外部组： `<localGroupId>;<idpName>`。 使用有助于将外部组与本地组关联的命名约定
1. 在外部组上设置`rep:externalId`属性，其值为： `<localGroupId>;<idpName>`
1. 添加外部组作为原始本地组的成员。

**验证**

* 可以通过检查每个本地组是否都有一个相应的外部组来验证结果。 此外，每个外部组都是相应本地组的成员。

**示例Servlet终结点：**

```java
@SlingServletPaths("/bin/migration/step1")
public class MigrationStep1Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String groupPath = request.getParameter("groupPath");
        String idpName = request.getParameter("idpName");

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Get local group
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        String localGroupId = localGroup.getID();
        
        // Create external group
        String externalGroupPrincipalName = localGroupId + ";" + idpName;
        // The function createExternalGroup performs the following steps:
        // 1. Creates a new external group with the given principal name (format: "<localGroupId>;<idpName>").
        // 2. Sets the 'rep:externalId' property on the group to mark it as an external group (value: "<localGroupId>;<idpName>").
        // 3. Sets the 'rep:principalName' property for the group if required.
        // 4. Assigns any other required group metadata, such as a title or description, if needed.
        // 5. Persists the new group node in the repository at the appropriate path under /home/groups.
        // 6. Returns the created Group object so it can be used for further operations, such as membership assignment.
        Group externalGroup = createExternalGroup(externalGroupPrincipalName, localGroupId, idpName);
        
        // Add external group to local group
        localGroup.addMember(externalGroup);
        
        session.save();
    }
}
```

**用法：**

```bash
curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/c/content-authors&idpName=saml-idp"
```

### 步骤2：转换用户并分配动态成员资格 {#step-2-convert-users-and-assign-dynamic-membership}

对于作为本地组成员的每个用户：

1. 请确保已设置`rep:externalId`（如果需要，转换为外部用户）。
1. 对于每个组成员资格，将相应的外部组主体添加到`rep:externalPrincipalNames`
1. 更新同步时间戳。

>[!IMPORTANT]
>
>在此过程中跳过系统组，如“所有人”。

**示例Servlet终结点：**

```java
@SlingServletPaths("/bin/migration/step2")
public class MigrationStep2Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String userId = request.getParameter("userId");
        String idpName = request.getParameter("idpName");
        
        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Login as the service user
        Session serviceSession = repository.loginService("group-provisioner", null);

        try {
            UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
            User user = (User) userManager.getAuthorizable(userId);
            
            // Ensure user has rep:externalId
            Value[] externalIdValues = user.getProperty("rep:externalId");
            if (externalIdValues == null || externalIdValues.length == 0) {
                ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
                user.setProperty("rep:externalId", 
                            valueFactory.createValue(externalRef.getString()));
            }
            
            // Get all group memberships
            Iterator<Group> groupIterator = user.declaredMemberOf();
            List<String> principalNames = new ArrayList<>();
            
            while (groupIterator.hasNext()) {
                Group group = groupIterator.next();
                String groupId = group.getID();
                
                // Skip system groups
                if ("everyone".equals(groupId)) {
                    continue;
                }
                
                // Add dynamic group principal
                String dynamicGroupPrincipal = groupId + ";" + idpName;
                principalNames.add(dynamicGroupPrincipal);
            }
            
            // Set rep:externalPrincipalNames
            if (!principalNames.isEmpty()) {
                Value[] newValues = new Value[principalNames.size()];
                for (int i = 0; i < principalNames.size(); i++) {
                    newValues[i] = valueFactory.createValue(principalNames.get(i));
                }
                user.setProperty("rep:externalPrincipalNames", newValues);
            }
            
            // Update timestamps to far future (workaround for OAK-12079)
            // Set to 10 years in the future to prevent premature cleanup of external group memberships
            // See: https://issues.apache.org/jira/browse/OAK-12079
            java.util.Calendar future = java.util.Calendar.getInstance();
            future.add(java.util.Calendar.YEAR, 10);
            user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
            user.setProperty("rep:lastSynced", valueFactory.createValue(future));
        
        // Perform operations...
        serviceSession.save();
    } finally {
        if (serviceSession != null && serviceSession.isLive()) {
            serviceSession.logout();
        }
}    }
}
```

**用法：**

```bash
curl -X POST "http://localhost:4503/bin/migration/step2?userId=john.doe&idpName=saml-idp"
```

**验证**

您可以通过检查每个用户是否具有每个外部组的`rep:externalId`的`rep:externalPrincipalName`和`principalName`属性，来验证这一点。 这些用户是外部组的本地组&#x200B;*和*&#x200B;的成员。

### 步骤3：删除直接用户成员资格 {#step-3-remove-direct-user-memberships}

用户配置动态组成员资格后：

1. 从本地组中删除直接用户成员资格
1. 保留组到组成员资格（包括外部组成员资格）

**示例Servlet终结点：**

```java
@SlingServletPaths("/bin/migration/step3")
public class MigrationStep3Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        String groupPath = request.getParameter("groupPath");
        
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        
        // Process each member
        Iterator<Authorizable> members = localGroup.getDeclaredMembers();
        
        while (members.hasNext()) {
            Authorizable member = members.next();
            
            // Remove only user members, keep group members
            if (!member.isGroup()) {
                localGroup.removeMember(member);
            }
        }
        
        session.save();
    }
}
```

**用法：**

```bash
curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/c/content-authors"
```

**验证**

* 您可以通过检查每个本地组是否仅将相应的外部组或其他组作为成员来进行验证。


## 迁移工作流 {#migration-workflow}

### 迁移前核对清单 {#pre-migration-checklist}

* **配置服务用户**：创建并配置具有适当权限的服务用户（例如`group-provisioner`）
* **验证ExternalPrincipal配置**：确保将服务用户配置为绕过`rep:externalId`和`rep:externalPrincipalNames`上的保护
* **测试服务用户权限**：验证服务用户是否可以在开发中设置外部标识属性
* 识别创建用户或组的所有自定义代码
* 审查并更新自定义代码以使用外部身份模型
* 在开发环境中测试更新的代码
* 清点所有要迁移的现有本地用户和组
* 在较低环境中测试迁移过程

### 执行步骤 {#execution-steps}

1. **部署更新的代码**：部署自定义代码更改以创建外部用户/组

1. **创建外部组**（针对每个本地组）：

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/g/my-group&idpName=saml-idp"
   ```

1. **迁移用户** （针对每个用户）：

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step2?userId=username&idpName=saml-idp"
   ```

1. **清理**（对于每个迁移的组）：

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/g/my-group"
   ```

1. **验证**：检查用户组成员资格并测试访问权限

1. **启用数据同步**：联系客户支持以启用该功能

### 迁移后验证 {#post-migration-validation}

验证迁移：

1. **检查用户属性**：

   在用户节点上，验证是否存在：

   * `rep:externalId`：格式应为`userId;idpName`
   * `rep:externalPrincipalNames`：格式为`groupId;idpName`的组承担者数组
   * `rep:lastSynced`：时间戳设置为遥远的未来（从迁移日期算起约10年）
   * `rep:lastDynamicSync`：时间戳设置为遥远的未来（从迁移日期算起约10年）

   **注意**：作为OAK-12079的解决方法，时间戳特意设置为更远的将来日期。 这个行为符合预期。

1. **检查组属性**：

   在本地组节点上验证是否存在：

   * 格式为`groupId;idpName`的外部组成员
   * 无直接用户成员（仅在步骤3之后）

1. **测试用户登录**：验证用户是否可以登录并具有正确的权限

1. **测试访问控制**：验证用户是否可以访问受CUG/ACL保护的内容

## 疑难解答 {#troubleshooting}

### 常见问题 {#common-issues}

**问题：设置`rep:externalId`或`rep:externalPrincipalNames`**&#x200B;时出现权限错误

**错误消息：**

* `javax.jcr.AccessDeniedException: Access denied`
* `OakAccess0000: Access denied`
* `Cannot set property 'rep:externalId'`

**解决方案**：必须使用正确配置的服务用户打开会话，该用户已被授予绕过外部标识属性保护的权限。

**解决步骤：**

1. **验证服务用户是否存在**：确保服务用户（例如，`group-provisioner`）是通过repoinit创建的
1. **检查服务用户映射**：验证servlet或服务是否正在使用`repository.loginService("group-provisioner", null)`
1. **验证ExternalPrincipal配置**：确保`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration`配置正确
1. **检查服务用户权限**：服务用户需要`rep:write`和`rep:userManagement`的`/home/users`和`/home/groups`权限

有关完整的设置说明，请参阅[服务用户配置](#service-user-configuration)。

**问题：`OakConstraint0072: Property 'rep:externalPrincipalNames' requires 'rep:externalId' to be present`**

**解决方案**：用户必须在设置`rep:externalId`之前设置`rep:externalPrincipalNames`。 请确保第2步先将用户转换为外部用户。

**问题：用户在迁移后失去组成员资格**

**解决方案**：验证：

* 已使用正确的主体名称格式(`groupId;idpName`)创建外部组
* 外部组已添加为本地组的成员（步骤1）
* 用户在`rep:externalPrincipalNames`中具有正确的外部主体名称（步骤2）
* 步骤3清理仅在步骤1和步骤2完成后执行

**问题：用户登录后意外删除了外部组成员资格(OAK-12079)**

**问题**：由于Oak错误[OAK-12079](https://issues.apache.org/jira/browse/OAK-12079)，Oak同步机制可能会根据`rep:lastSynced`和`rep:lastDynamicSync`时间戳提前清理外部组成员资格。

**解决方案**：将`rep:lastSynced`和`rep:lastDynamicSync`时间戳设置为遥远的将来日期（从现在起的10年后），而不是当前时间。 这样可防止同步清理过程删除外部组成员资格。

**实现：**

```java
// Workaround for OAK-12079
// Set to 10 years in the future to prevent premature cleanup
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
```

**为什么这有效**：通过将时间戳设置为遥远的将来日期，Oak同步逻辑将这些用户视为“最近同步”，并且不会触发将删除外部主体名称和组成员资格的清理过程。

**注意**：在未来Oak版本中解决OAK-12079之前，这是一个临时解决方法。 本文档中的所有代码示例均已包含此解决方法。

**问题：系统组“所有人”导致错误**

**解决方案**：在用户迁移期间始终跳过“所有人”系统组（步骤2）。 此组由AEM自动管理。

### 回滚过程 {#rollback-procedure}

如果迁移遇到问题：

1. 停止迁移过程
1. 如果关键数据受到影响，则从备份中恢复
1. 回滚对代码所做的更改以创建具有动态组成员资格的外部用户和组
1. 在重新尝试迁移之前，请查看并修复问题。

## 最佳做法 {#best-practices}

* **彻底测试**：始终在生产之前在开发和暂存环境中测试迁移
* **批处理**：对于大型用户群，请批量处理迁移以避免超时问题
* **监视性能**：监视迁移期间的存储库性能
* **维护审核记录**：记录所有迁移操作以进行疑难解答
* **服务用户权限**：确保迁移servlet使用具有所需权限的适当服务用户。 必须在ExternalPrincipal配置中将服务用户配置为绕过`rep:externalId`和`rep:externalPrincipalNames`属性的保护
* **幂等运算**：设计可安全重新运行的迁移代码
* **在每个步骤进行验证**：在继续之前，请检查每个迁移步骤之后的结果

## 保护迁移Servlet {#securing-migration-servlets}

迁移servlet具有创建和修改用户和组的提升权限。 限制对这些端点的访问以防止未经授权的访问至关重要。

### 推荐的方法： IMS技术帐户身份验证 {#recommended-approach-ims-technical-account}

推荐的方法是使用Adobe IMS集成保护这些servlet，只允许授权的技术帐户访问它们。

#### 步骤1：在AEM Developer Console中创建技术帐户 {#create-a-technical-account-in-aem-developer-console}

1. 依次导航到[Experience Manager](https://experience.adobe.com/)和&#x200B;**Cloud Manager**
1. 选择您的项目，然后单击要创建技术帐户的环境
1. 在环境的省略号菜单中单击&#x200B;**Developer Console**
1. 在AEM Developer Console中，转到&#x200B;**集成**&#x200B;选项卡
1. 单击&#x200B;**新建技术帐户**
1. 提供集成的名称（例如，“迁移服务帐户”）
1. 单击&#x200B;**创建**
1. 请注意所创建集成的以下值：
   * **客户端ID**
   * **客户端密码**
   * **技术帐户ID** （这将是访问您的servlet的用户ID — 格式： `XXXXXXXXXXXXXXXXXXXXXXXX@techacct.adobe.com`）

有关详细说明，请参阅[为服务器端API生成访问令牌文档](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。

检查调用方是否获得授权的示例代码：

```
    private boolean isAuthorizedCaller(SlingHttpServletRequest request, 
                                       SlingHttpServletResponse response) {

        Session session = request.getResourceResolver().adaptTo(Session.class);
        String callerId = session != null ? session.getUserID() : null;
               
        if (!ALLOWED_TECHNICAL_ACCOUNT.equals(callerId)) {
            LOG.warn("Unauthorized access attempt by user: '{}' (expected: '{}')", callerId,   ALLOWED_TECHNICAL_ACCOUNT);
            response.setStatus(SlingHttpServletResponse.SC_FORBIDDEN);
            return false;
        }
        
        return true;
    }
```

### 深入防御：基于IP的限制 {#defense-in-depth-ip-based-restrictions}

作为附加的安全层，您可以配置CDN规则，以按IP地址限制对迁移端点的访问。 在从已知基础架构中运行迁移时，这非常有用。

>[!NOTE]
>
>仅靠IP限制是不够的。 如上所述，始终将身份验证检查结合使用。

### 安全清单 {#security-checklist}

在将迁移servlet部署到生产环境之前：

* 在AEM Developer Console中创建IMS集成
* 配置servlet以验证技术帐户ID
* 在开发/暂存环境中测试身份验证流程
* 考虑CDN级别的其他基于IP的限制
* 规划在迁移完成后禁用或删除迁移servlet
* 审核并记录对迁移端点的所有访问

>[!IMPORTANT]
>
>迁移完成后，请考虑从部署中禁用或删除迁移servlet以消除任何潜在的安全风险。

## 其他资源 {#additional-resources}

* [发布层的用户和组同步](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)
* [SAML 2.0身份验证处理程序](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=zh-Hans)
* [外部身份提供程序](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)
* [动态组成员资格](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html)
