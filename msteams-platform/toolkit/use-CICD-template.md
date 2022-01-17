---
title: CI 或 CD 支持Teams应用程序开发人员
author: MuyangAmigo
description: 分时模板
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: b8a6506707626a80cabc9c730eef6fe11160e386
ms.sourcegitcommit: 7cccec0b2512f4e9366eb7c88998c5181a52681d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059066"
---
# <a name="cicd-guide"></a>CI/CD 指南

TeamsFx 有助于在构建应用程序的同时自动Teams工作流。 本文档提供了一些工具和模板，可让你开始使用 GitHub、Azure Devops 和 Jenkins 设置 CI 或 CD 管道。

|工具和模板|Description| 
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|GitHub TeamsFx CLI 的"操作"。|
|[github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) 和 [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHub应用的 CI 或 CD Teams模板。 |
|[jenkins-ci-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) 和 [jenkins-cd-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|用于应用应用的 Jenkins CI 或 CD Teams模板。|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) 和 [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| 用于自动化的脚本模板GitHub。 |

## <a name="ci-or-cd-workflow-templates-in-github"></a>解决方案中的 CI 或 CD 工作流GitHub

**若要包含 CI 或 CD 工作流，Teams应用程序开发过程自动化GitHub：**

1. 在 下创建文件夹 `.github/workflows`
1. 复制以下模板文件之一：
    * [github-ci-template.yml（](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) 用于 CI 工作流）。
    * [用于 CD 工作流的 github-cd-template.yml。](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)
1. 自定义适合您的方案的工作流。

### <a name="customize-ci-workflow"></a>自定义 CI 工作流

执行以下步骤来调整项目的工作流：

1. 更改 CI 流。 
1. 使用 npm 生成脚本，或自定义在自动化代码中生成项目的方式。
1. 使用 npm 测试脚本（成功返回零）并更改测试命令。

### <a name="customize-cd-workflow"></a>自定义 CD 工作流

执行以下步骤以自定义 CD 工作流：

1. 默认情况下，当向分支提交新内容时，将触发 CD `main` 工作流。
1. 创建GitHub[存储库](https://docs.github.com/en/actions/reference/encrypted-secrets)密码以保留 Azure 服务主体和 M365 帐户登录凭据。 有关详细信息，请参阅操作[GitHub操作](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md)。
1. 如有必要，请更改生成脚本。
1. 根据需要删除测试脚本。

> [!NOTE]
> 预配步骤不包含在 CD 模板中，因为它通常只执行一次。 可以在 TeamsFx CLI 中Teams Toolkit预配，或者使用单独的工作流。 确保在预配后提交。 设置结果将存放于 `.fx` 文件夹中。

### <a name="github-secrets"></a>Github 密码

下表列出了在环境中创建环境所需的GitHub：

1. 选择“**设置**”。
1. 转到" **环境"** 部分。
1. 选择 **"新建环境"。**
1. 输入环境的名称。 模板中提供的默认环境名称是 `test_environment` 。 
1. 选择 **"配置环境"。**
1. 选择 **"添加密码"。**

下表列出了创建环境所需的所有密钥：

|名称|说明|
|---|---|
|AZURE_SERVICE_PRINCIPAL_NAME|用于预配资源的 Azure 的服务主体名称。|
|AZURE_SERVICE_PRINCIPAL_PASSWORD|Azure 服务主体的密码。|
|AZURE_SUBSCRIPTION_ID|确定将在其中预配资源的订阅。|
|AZURE_TENANT_ID|标识订阅所在的租户。|
|M365_ACCOUNT_NAME|用于创建和发布应用的 M365 Teams帐户。|
|M365_ACCOUNT_PASSWORD|M365 帐户的密码。|
|M365_TENANT_ID|标识将在其中创建Teams/发布的租户。 此值是可选的，除非你拥有多租户帐户并且想要使用另一个租户。 有关详细信息，请参阅[如何查找 M365 租户 ID。](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|


> [!NOTE]
> 目前，Azure 的服务主体用于 CI/CD 工作流。 有关详细信息，请参阅创建 [azure 服务原则](#create-azure-service-principals)。

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>使用管道设置 CI 或 CD Azure DevOps

可以在脚本中设置自动Azure DevOps，并引用脚本。

执行以下步骤以开始使用：

* [CI 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>设置 CI 管道

1. 将[CI 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)添加到Azure DevOps存储库，然后执行必要的自定义，正如从脚本文件中的评论推断的。
1. 按照[步骤创建 CI Azure DevOps管道](/azure/devops/pipelines/create-first-pipeline)。
下面是常见 CI 管道脚本的方案：

```yml
trigger:
- dev 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true
  
- task: Bash@3
  inputs:
    filePath: './others-script-ci-template.sh'
```

以下是您可以对脚本或工作流定义所做的更改：

1. 更改 CI 流。 我们默认为将新提交推送到分支 `dev` 时。
1. 更改如何安装节点和 npm 的方式。
1. 使用 npm 生成脚本，或自定义在自动化代码中生成的方式。
1. 使用 npm 测试脚本（成功返回零）并更改测试命令。

### <a name="set-up-cd-pipeline"></a>设置 CD 管道

1. 将[CD 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)Azure DevOps库，然后执行必要的自定义，如从脚本文件中注释推断的。
1. 为 CD Azure DevOps管道。 有关详细信息，请参阅创建 [第一个管道](/azure/devops/pipelines/create-first-pipeline)。 管道的定义可以引用 CI 管道的以下示例定义。
1. 通过"定义变量 ["添加必要的变量](/azure/devops/pipelines/process/variables)，并在必要时将它们作为密钥。

```yml
trigger:
- main 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true
  
- task: Bash@3
  env:
    SP_NAME: $(AZURE_SERVICE_PRINCIPAL_NAME)
    SP_PASSWORD: $(AZURE_SERVICE_PRINCIPAL_PASSWORD)
    TENANT_ID: $(AZURE_TENANT_ID)
    AZURE_SUBSCRIPTION_ID: $(AZURE_SUBSCRIPTION_ID)
    M365_ACCOUNT_NAME: $(M365_ACCOUNT_NAME)
    M365_ACCOUNT_PASSWORD: $(M365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

以下是您可以对脚本或工作流定义所做的更改：

1. 如何触发 CD 流。 默认情况下，当向主分支进行新提交时 **，将发生** 此情况。
1. 更改如何安装节点和 npm 的方式。
1. 默认情况下，更改环境名称的暂 **存**。
1. 确保你拥有 npm 生成脚本，或自定义在自动化代码中生成的方式。
1. 确保有一个 npm 测试脚本，该脚本返回零以成功，并且/或更改测试命令。

### <a name="pipeline-variables-for-azure-devops"></a>用于管道的管道Azure DevOps

执行以下步骤以在 Azure DevOps：

1. 在"管道编辑"页中，选择 **"变量"，** 然后选择"**新建变量"。**
1. 输入变量的名称或值对。
1. 如有必要，请切换 **"将此值保密** "复选框。
1. 选择 **"** 确定"以创建变量。

|名称|说明|
|---|---|
|AZURE_SERVICE_PRINCIPAL_NAME|用于预配资源的 Azure 的服务主体名称。|
|AZURE_SERVICE_PRINCIPAL_PASSWORD|Azure 服务主体的密码。|
|AZURE_SUBSCRIPTION_ID|确定将在其中预配资源的订阅。|
|AZURE_TENANT_ID|标识订阅所在的租户。|
|M365_ACCOUNT_NAME|用于创建和发布 Teams 应用的 M365 帐户。|
|M365_ACCOUNT_PASSWORD|M365 帐户的密码。|
|M365_TENANT_ID|标识将在其中创建Teams/发布的租户。 此值是可选的，除非你拥有多租户帐户并且想要使用另一个租户。 阅读有关 [如何查找 M365 租户 ID 的更多信息](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)。|

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Jenkins 中的 CI 或 CD 管道模板

若要将这些模板添加到存储库，需要[jenkins-ci-template 的版本。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile)和[jenkins-cd-template。要按分支位于存储库中的 Jenkinsfile。](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)

此外，你需要在 Jenkins 中创建 CI 或 CD 管道，这些管道指向相应的特定 **Jenkinsfile。**

按照以下步骤检查如何将 Jenkins 连接到不同的 SCM 平台：

1. [Jenkins 和 GitHub](https://www.jenkins.io/solutions/github/)
2. [Jenkins 和 Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [具有 GitLab 的 Jenkins](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [具有 Bitbucket 的 Jenkins](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>自定义 CI 管道

下面是您可以为调整项目而进行一些更改：

1. 将模板文件重命名为 **Jenkinsfile，** 并将其放在目标分支（例如 **，dev** 分支）下。
1. 更改 CI 流的触发。 我们默认在将新更改推送到开发人员分支时使用 **pollSCM** **的** 触发器。
1. 确保你拥有 npm 生成脚本，或自定义在自动化代码中生成的方式。
1. 确保有一个 npm 测试脚本，该脚本返回零以成功，并且/或更改测试命令。

### <a name="customize-cd-pipeline"></a>自定义 CD 管道

执行以下步骤以自定义 CD 管道：

1. 将模板文件重命名为 **Jenkinsfile，** 并将其放在目标分支（例如，主分支 **）下。**
1. 更改 CD 流。 我们默认在将新更改推送到主分支时使用 **pollSCM** **的** 触发器。
1. 创建 Jenkins [管道凭据](https://www.jenkins.io/doc/book/using/using-credentials/) 以保留 Azure 服务主体和 M365 帐户登录凭据。
1. 如有必要，请更改生成脚本。
1. 如果没有测试，请删除测试脚本。

### <a name="credentials-for-jenkins"></a>Jenkins 的凭据

按照 [using-credentials](https://www.jenkins.io/doc/book/using/using-credentials/) 在 Jenkins 上创建凭据。

|名称|说明|
|---|---|
|AZURE_SERVICE_PRINCIPAL_NAME|用于预配资源的 Azure 的服务主体名称。|
|AZURE_SERVICE_PRINCIPAL_PASSWORD|Azure 服务主体的密码。|
|AZURE_SUBSCRIPTION_ID|确定将在其中预配资源的订阅。|
|AZURE_TENANT_ID|标识订阅所在的租户。|
|M365_ACCOUNT_NAME|用于创建和发布 Teams 应用的 M365 帐户。|
|M365_ACCOUNT_PASSWORD|M365 帐户的密码。|
|M365_TENANT_ID|标识将在其中创建Teams/发布的租户。 此值是可选的，除非你拥有多租户帐户并且想要使用另一个租户。 阅读有关 [如何查找 M365 租户 ID 的更多信息](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)。|

## <a name="get-started-guide-for-other-platforms"></a>适用于其他平台的入门指南

你可以按照列出的预定义示例 Bash 脚本在其他平台上构建和自定义 CI 或 CD 管道：

* [CI 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

这些脚本基于跨平台 TeamsFx 命令行工具[TeamsFx-CLI。](https://www.npmjs.com/package/@microsoft/teamsfx-cli) 可以随文档一 `npm install -g @microsoft/teamsfx-cli` 起安装脚本 [，然后](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) 按照文档自定义脚本。

> [!NOTE]
> * 若要启用 `@microsoft/teamsfx-cli` 在 CI 模式下运行，请通过 `CI_ENABLED` 打开 `export CI_ENABLED=true` 。 在 CI 模式下 `@microsoft/teamsfx-cli` ，适用于 CI 或 CD。
> * 若要启用 `@microsoft/teamsfx-cli` 在非交互模式下运行，请通过命令设置全局配置 `teamsfx config set -g interactive false` ：。 在非交互模式中 `@microsoft/teamsfx-cli` ，不会以交互方式提出输入问题。

确保在环境变量中安全设置 Azure 和 M365 凭据。 例如，如果你使用 GitHub 作为源代码存储库。 有关详细信息，请参阅[Github Secrets。](https://docs.github.com/en/actions/reference/encrypted-secrets)

## <a name="create-azure-service-principals"></a>创建 Azure 服务主体

若要在 CI/CD 内预配和部署面向 Azure 的资源，必须创建 Azure 服务主体以使用。

执行以下步骤以创建 Azure 服务主体：
1. 在单个Azure AD注册应用程序。
2. 将角色分配给Azure AD应用程序以访问 Azure 订阅， `Contributor` 建议使用角色。 
3. 创建新的应用程序Azure AD密码。

> [!TIP]
> 保存租户 ID、应用程序 id (AZURE_SERVICE_PRINCIPAL_NAME) 和密码 (AZURE_SERVICE_PRINCIPAL_PASSWORD) 供将来使用。

有关详细信息，请参阅 [Azure 服务主体指南](/azure/active-directory/develop/howto-create-service-principal-portal)。 以下是创建服务主体的三种方法： 
* [Azure 门户](/azure/active-directory/develop/howto-create-service-principal-portal)
* [PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>使用Teams门户发布Teams应用
如果存在与应用清单Teams相关的任何更改，可能需要再次发布Teams应用以更新清单。

若要手动Teams应用，你可以利用[开发人员门户进行Teams。](https://dev.teams.microsoft.com/home)

执行以下步骤以发布应用：
1. 使用相应的[帐户登录到开发人员Teams](https://dev.teams.microsoft.com)进行登录。
2. 通过选择 以 zip 导入你的应用包 `App -> Import app -> Replace` 。
3. 在应用列表中选择目标应用。
4. 通过选择发布应用 `Publish -> Publish to your org`

### <a name="see-also"></a>另请参阅

* [快速入门GitHub操作](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [创建第一个Azure DevOps管道](/azure/devops/pipelines/create-first-pipeline)
* [创建首个 Jenkins 管道](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [使用开发人员门户管理应用Microsoft Teams](/concepts/build-and-test/teams-developer-portal)
