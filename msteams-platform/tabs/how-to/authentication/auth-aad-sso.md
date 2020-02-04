---
title: 单一登录
description: 介绍单一登录（SSO）
keywords: 团队身份验证 SSO AAD
ms.openlocfilehash: 1857651aecd902f04bd57f5b4e2fb0fda88eb348
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673006"
---
# <a name="single-sign-on"></a>单一登录

> [!NOTE]
> "单一登录" API 目前仅在_开发人员预览版_中受支持。

用户使用其工作或学校（Office 365）帐户登录 Microsoft 团队，您可以使用单一登录（SSO）对 Microsoft "团队" 选项卡上的用户进行授权，以利用这一点。这意味着，如果用户同意在桌面上使用您的应用程序，则无需再次在手机上同意，并且将自动登录。 

## <a name="how-sso-works-at-runtime"></a>运行时 SSO 的工作方式

下图显示 SSO 进程的工作原理：

<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. 在 "" 选项卡中，JavaScript 调用 getAuthToken （）。 这将告知团队应用程序获取对选项卡应用程序的身份验证令牌。
2. 如果这是当前用户第一次使用您的选项卡应用程序，则系统会提示他们同意（如果需要同意）或要求他们处理分步身份验证（如双重身份验证）。
3. Microsoft 团队应用程序从 Azure AD v1.0 终结点请求当前用户的选项卡应用程序令牌。
4. Azure AD 将选项卡应用程序令牌发送给团队应用程序。
5. Microsoft 团队应用程序将选项卡应用程序令牌作为 getAuthToken （）调用返回的 result 对象的一部分发送到选项卡。
6. 选项卡应用程序中的 JavaScript 可以分析令牌，并提取所需的信息，如用户的电子邮件地址。
    * 注意：此令牌仅适用于同意一组有限的用户级 Api （ex：电子邮件、配置文件等），而不是对进一步的图表范围（如 Mail）有效。 如果你需要其他 Graph 作用域，请参阅本文档末尾的部分，了解建议的解决方法。

## <a name="develop-an-sso-microsoft-teams-tab"></a>开发 SSO Microsoft 团队选项卡

本节介绍创建使用 SSO 的 Microsoft "团队" 选项卡所涉及的任务。 其中介绍的这些任务与语言和框架无关。

### <a name="1-create-your-aad-application-in-azure"></a>1. 在 Azure 中创建 AAD 应用程序

在 Azure AD v1.0 终结点的注册门户中注册应用程序。 该流程用时 5-10 分钟，包括以下任务：

* 获取 AAD 应用程序 ID
* 指定应用程序对 AAD 终结点（也可以选择向 Microsoft Graph）所需的权限。 
* 向 Microsoft 团队桌面、web 和移动应用程序授予对应用程序的信任
* 预授权将 Microsoft 团队应用程序与默认作用域名称为的`access_as_user`应用程序结合使用。

> [!NOTE]
> 您应注意一些重要限制：
>
> * 仅支持用户级图形 API 权限（即 email、profile、offline_access、openid。 如果需要访问其他图表范围，请阅读本文档末尾的建议解决方法。
> * 您的应用程序的域名应注册到 Azure AD 应用程序，这一点很重要。 当在团队中请求身份验证令牌时，以及在团队清单中指定资源属性（下一节中的详细信息）时，此名称必须与应用程序运行的域名相同。
> * 目前，每个应用程序不支持多个域
> * 我们还不支持使用`azurewebsites.net`域的应用程序，因为此域太常见，可能存在安全风险

#### <a name="steps"></a>步骤

1. 在 Azure Active Directory 中注册新应用程序[–应用注册](https://go.microsoft.com/fwlink/?linkid=2083908)门户
2. 选择 "新注册"。 在 "注册应用程序" 页上，按如下所示设置值：
    * 将**名称**设置为您的应用程序名称
    * 将**支持的帐户类型**设置为**任何组织目录和个人 Microsoft 帐户中的帐户**
    * 将**重定向 URI**留空
    * 选择 "**注册**"
3. 在 "概述" 页上，复制并保存**应用程序（客户端） ID**。 稍后在更新团队应用程序清单时，将需要它。
4. 在“管理”**** 下选择“公开 API”****。 选择 "**设置**" 链接，以以的形式生成应用程序 ID `api://{AppID}`URI。 在双正斜杠和 GUID 之间插入完全限定的域名（在末尾追加一个正斜杠 "/"）。 整个 ID 的形式应为：`api://fully-qualified-domain-name.com/{AppID}`
    * 例如： `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`。

> [!NOTE]
> 如果收到一条错误，指出域已有所有者，但你拥有该域，请按照[快速入门： 将自定义域名添加到 Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) 中的步骤进行操作来注册该域，然后重复此步骤。 （如果您未使用 Office 365 租赁中的管理员的凭据登录，也会发生此错误。

5. 选择“添加一个作用域”**** 按钮。 在打开的面板中，输入 `access_as_user` 作为“作用域名称”****。
6. 设置谁可以同意？为管理员和用户
7. 填写用于配置管理员和用户同意提示的字段，其中包含适用于该`access_as_user`范围的值。 建议：
    * **管理员同意职务：** 团队可以访问用户的配置文件
    * **管理员同意说明**：允许团队以当前用户的身份调用应用程序的 web api。
    * **用户同意标题**：团队可以访问您的用户配置文件并代表你发出请求
    * **用户同意说明：** 使团队可以使用你拥有的相同权限调用此应用的 Api
8. 确保将 "**状态**" 设置为 "**已启用**"
9. 选择 "**添加范围**"
    * 注意：在文本字段正下方显示的**范围名称**的域部分应自动匹配上一步中设置的**应用程序 ID** URI，并`/access_as_user`追加到末尾;例如： 
        * `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7/access_as_user`
10. 在 "**授权客户端应用程序**" 部分中，确定要授权给应用程序的 web 应用程序的应用程序。 需要输入以下每个 Id：
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`（团队移动/桌面应用程序）
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`（团队 web 应用程序）
11. 导航到 " **API 权限**"，并确保添加 "关注" 权限：
    * User。 Read （默认情况下已启用）
    * email
    * offline_access
    * openid
    * profile

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. 更新 Microsoft 团队应用程序清单

将新属性添加到 Microsoft 团队清单：

* **WebApplicationInfo** - 下列元素的父元素。
* **Id** -应用程序的客户端 Id。 这是在使用 Azure AD 1.0 终结点注册应用程序的过程中获得的应用程序 ID。
* **Resource** -应用程序的域和子域。 这是在 AAD 中注册应用时`api://`使用的 URI （包括协议）。 此 URI 的域部分应与在团队应用程序清单的部分的 Url 中使用的域（包括任何子域）相匹配。

```json
"webApplicationInfo": {
  "id": "<application_GUID here>",
  "resource": "<web_API resource here>"
}
```

注意：

* AAD 应用的资源通常只是其网站 URL 和 appID 的根（例如`api://subdomain.example.com/6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`）。 我们还使用此值来确保你的请求来自同一个域。 Therefor 确保您`contentURL`的选项卡使用与您的资源属性相同的域。
* 您需要使用清单版本1.5 或更高版本，才能使用这些字段。
* 清单在清单中不受支持，而是应在 Azure 门户中的 API 权限部分中指定。

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. 从客户端代码中获取身份验证令牌

身份验证 API 如下所示：

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); },
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

当你拨打`getAuthToken`并需要其他用户同意时（对于用户级权限），我们将向用户显示一个对话框，让他们鼓励他们授予额外的许可。 

<img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>

## <a name="demo-code"></a>演示代码

现在，您可以访问我们的测试应用程序[任务 Meow](https://github.com/ydogandjiev/taskmeow) ，并使用 SSO 清单并`teams.auth.service.js`签`sso.auth.service.js`出和文件，以查看如何处理身份验证工作流。

## <a name="known-limitations"></a>已知限制

### <a name="apps-that-require-additional-graph-scopes"></a>需要其他图表范围的应用程序

我们目前的 SSO 实施仅授予用户级权限（电子邮件、配置文件、offline_access、openid）的同意，而不授予对其他 Api （如 Mail）的同意。 如果您的应用程序需要更多图形范围，则有一些解决办法可实现此工作。

#### <a name="tenant-admin-consent"></a>租户管理员同意

最简单的方法是，让租户管理员代表组织进行预先同意。 这意味着用户无需同意这些作用域，然后可以使用 AAD 的[代表流](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)来免费交换令牌服务器端。 这种解决方法对于内部业务线应用程序是可接受的，但对于可能无法依赖租户管理员批准的 Isv 来说可能不够。

同意代表组织（作为租户管理员）的一种简单方法是访问：

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>使用 Auth API 请求其他许可

获取其他图表范围的另一种方法是，使用现有的[基于 web 的 aad 身份验证方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)呈现许可对话，这涉及弹出 AAD 同意对话框。 有一些显著的添加：

1. 使用 getAuthToken 检索到的令牌需要使用 AADs[代表流](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)进行交换，以获取对这些其他图形 api 的访问权限。
    * 请务必将 v2 Graph 终结点用于此 exchange
2. 如果 exchange 失败，AAD 将返回无效的授予异常。 通常有以下两种错误消息之一： `ConsentRequired``InteractionRequired`
3. 当 exchange 发生故障时，您需要请求其他许可。 建议显示一些 UI，要求用户授予更多许可。 此 UI 应包含使用我们的[AAD 身份验证 API](~/concepts/authentication/auth-silent-aad.md)触发 aad 同意对话的按钮。
4. 当询问来自 AAD 的其他许可时，您需要将`prompt=consent` [查询字符串参数](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)包括在您的 AAD 中，否则 aad 将不会询问其他作用域。
    * 而不是：`?scope={scopes}`
    * 使用以下命令：`?prompt=consent&scope={scopes}`
    * 确保`{scopes}`包含要提示用户的所有作用域（例如： Mail. Read 或 User. read）。
5. 一旦用户授予了其他权限，则重试代表流，以获取对这些附加 Api 的访问权限。

### <a name="non-aad-authentication"></a>非 AAD 身份验证

以上所述的身份验证解决方案仅适用于支持 Azure AD 作为标识提供程序的应用程序和服务。 若要使用基于非 AAD 的服务进行身份验证的应用程序，需要继续使用基于弹出窗口的[web 身份验证流](~/concepts/authentication.md)。
