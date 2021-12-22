---
title: 针对应用程序开发人员的 CI Teams CD 支持
author: MuyangAmigo
description: 分时模板
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: acd12a96365bf97bd419045c415e71efd3a118e2
ms.sourcegitcommit: aede47694894d281f6b725083bc0b46ab0e4846d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "61591776"
---
# <a name="ci-or-cd-support-for-teams-application-developers"></a>为应用程序开发人员Teams CI 或 CD 支持

TeamsFx 有助于在构建应用程序的同时自动Teams工作流。 本文档提供了一些工具和预先准备的模板，可让你开始使用最常见的开发平台（包括 GitHub、Azure Devops 和 Jenkins）设置 CI 或 CD 管道。

|工具和模板|说明|
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|与 TeamsFx CLI GitHub即用即用的操作。|
|[github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) 和 [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHub应用创建 CI 或 CD Teams模板。 |
|[jenkins-ci-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) 和 [jenkins-cd-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|用于应用应用的 Jenkins CI 或 CD Teams模板。|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) 和 [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| 用于自动化的脚本模板GitHub。 |

## <a name="ci-or-cd-workflow-templates-in-github"></a>解决方案中的 CI 或 CD GitHub

**若要包含 CI 或 CD 工作流，Teams应用程序开发过程自动化** GitHub：

1. 在 下创建文件夹 `.github/workflows`
1. 将模板文件 (其中一个或两个模板) ：
    * [github-ci-template.yml（](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) 用于 CI 工作流）。
    * [用于 CD 工作流的 github-cd-template.yml。](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)
1. 自定义这些工作流以适合您的方案。

### <a name="customize-ci-workflow"></a>自定义 CI 工作流

您可以进行以下更改来调整项目的工作流：

1. 更改 CI 流的触发。 我们默认为创建针对分支的拉取 `dev` 请求。
1. 使用 npm 生成脚本，或自定义在自动化代码中生成项目的方式。
1. 使用返回零的 npm 测试脚本成功和/或更改测试命令。

### <a name="customize-cd-workflow"></a>自定义 CD 工作流

自定义 CD 工作流的以下步骤：

1. 默认情况下，当向分支提交新内容时，将触发 CD `main` 工作流。
1. 按GitHub[创建](https://docs.github.com/en/actions/reference/encrypted-secrets)存储库密码以保留 Azure 或Microsoft 365登录凭据。 下表列出了需要在 GitHub 上创建的所有密码，有关详细用法，请参阅 GitHub Actions [README.md](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md)。
1. 如有必要，请更改生成脚本。
1. 如果没有测试，请删除测试脚本。

> [!Note]
> 预配步骤不包含在 CD 模板中，因为它通常只执行一次。 你可以执行预配 在 Teams Toolkit TeamsFx CLI 中，或者使用单独的工作流。 请记住，在预配 (设置结果将保存在文件夹) 中，将 文件内容保存到 GitHub 存储库密码中，并命名供将来 `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` [](https://docs.github.com/en/actions/reference/encrypted-secrets) `USERDATA_CONTENT` 使用。

### <a name="environment-variables"></a>环境变量

在下列环境中创建环境变量GitHub：

1. 在"项目 **设置，导航到****"环境"** 部分，然后选择"**新建环境"。**
1. 输入环境的名称。 模板中提供的默认环境名称是 `test_environment` 。 选择 **"配置环境** "继续。
1. 下一页，选择" **添加** 密码"为下表中列出的每个项目添加密码。

|名称|说明|
|---|---|
|AZURE_ACCOUNT_NAME|用于预配资源的 Azure 的帐户名称。|
|AZURE_ACCOUNT_PASSWORD|Azure 帐户的密码。|
|AZURE_SUBSCRIPTION_ID|确定将在其中预配资源的订阅。|
|AZURE_TENANT_ID|标识订阅所在的租户。|
|Microsoft 365_ACCOUNT_NAME|用于创建Microsoft 365发布应用程序的应用程序Teams帐户。|
|Microsoft 365_ACCOUNT_PASSWORD|帐户Microsoft 365密码。|
|Microsoft 365_TENANT_ID|标识将在其中创建Teams/发布的租户。 此值是可选的，除非你拥有多租户帐户并且想要使用另一个租户。 阅读更多[有关如何查找租户Microsoft 365 ID。](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|

> [!NOTE]
> 请参阅配置[Microsoft 365/Azure](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret)凭据，以确保已针对工作流中使用的凭据禁用多重身份验证和安全默认值。

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>设置 CI 或 CD Pipelines与Azure DevOps

可以在脚本中设置自动Azure DevOps，并引用脚本。 请按照下面提供的步骤开始：

* [CI 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>设置 CI 管道

1. 将[CI 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)添加到Azure DevOps存储库，然后执行必要的自定义，正如您可能从脚本文件中的评论推断的。
1. 按照[步骤为 CI Azure DevOps管道](/azure/devops/pipelines/create-first-pipeline)。
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

您可以对脚本或工作流定义进行的潜在更改：

1. 更改 CI 流的触发。 我们默认为将新提交推送到分支 `dev` 时。
1. 更改如何安装节点和 npm 的方式。
1. 使用 npm 生成脚本，或自定义在自动化代码中生成的方式。
1. 使用 npm 测试脚本（成功时返回零）和/或更改测试命令。

### <a name="set-up-cd-pipeline"></a>设置 CD 管道

1. 将[CD 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)添加到Azure DevOps库，然后执行必要的自定义，正如您根据脚本文件中的评论推断的。
1. 创建Azure DevOps CD 管道，因为你可以参考[此链接](/azure/devops/pipelines/create-first-pipeline)。 管道的定义可以引用 CI 管道的以下示例定义。
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

- task: DownloadSecureFile@1
  name: userdata
  inputs:
    secureFile: 'staging.userdata'
- task: Bash@3
  inputs:
    targetType: 'inline'
    script: |
      mkdir -p .fx/states/
      cp $(userdata.secureFilePath) .fx/states/staging.userdata
  
- task: Bash@3
  env:
    AZURE_ACCOUNT_NAME: $(AZURE_ACCOUNT_NAME)
    AZURE_ACCOUNT_PASSWORD: $(AZURE_ACCOUNT_PASSWORD)
    AZURE_TENANT_ID: $(AZURE_TENANT_ID)
    Microsoft 365_ACCOUNT_NAME: $(Microsoft 365_ACCOUNT_NAME)
    Microsoft 365_ACCOUNT_PASSWORD: $(Microsoft 365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

您可以对脚本或工作流定义进行的潜在更改：

1. 如何触发 CD 流。 默认情况下，当向主分支进行新提交时 **，将发生** 此情况。
1. 更改如何安装节点和 npm 的方式。
1. 默认情况下，更改环境名称的暂 **存**。
1. 确保你拥有 npm 生成脚本，或自定义在自动化代码中生成的方式。
1. 确保有一个 npm 测试脚本，该脚本返回零以成功，并且/或更改测试命令。

> [!Note]
> 预配步骤不包含在 CD 模板中，因为它通常只执行一次。 可以在 TeamsFx CLI Teams Toolkit内执行预配，或者使用单独工作流。 请记住在预配后提交 (设置结果将存储到文件夹) 并上传到 Azure DevOps 安全文件中供 `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` 将来使用。 [](/azure/devops/pipelines/library/secure-files)

### <a name="environment-variables-for-azure-devops"></a>环境变量Azure DevOps

在管道中创建管道变量Azure DevOps：

1. 在"管道编辑"页中，选择 **右** 上方的"变量"，然后选择"**新建变量"。**
1. 输入变量的名称/值对。
1. 如有必要，请切换 **"将此值保密** "复选框。
1. 选择 **"** 确定"以创建变量。

|名称|说明|
|---|---|
|AZURE_ACCOUNT_NAME|用于预配资源的 Azure 的帐户名称。|
|AZURE_ACCOUNT_PASSWORD|Azure 帐户的密码。|
|AZURE_SUBSCRIPTION_ID|确定将在其中预配资源的订阅。|
|AZURE_TENANT_ID|标识订阅所在的租户。|
|Microsoft 365_ACCOUNT_NAME|用于创建Microsoft 365发布应用的应用程序Teams帐户。|
|Microsoft 365_ACCOUNT_PASSWORD|帐户Microsoft 365密码。|
|Microsoft 365_TENANT_ID|标识将在其中创建Teams/发布的租户。 此值是可选的，除非你拥有多租户帐户并且想要使用另一个租户。 阅读更多[有关如何查找租户Microsoft 365 ID。](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|

> [!NOTE]
> 预配步骤不包含在 CD 模板中，因为它通常只执行一次。 可以在 TeamsFx CLI Teams Toolkit内执行预配，或者使用单独工作流。 请记住，在预配 (预配结果将保存在文件夹) 中，将 的文件内容保存到 `.fx` Jenkins 凭据中供 `.fx/states/{YOUR_ENV_NAME}.userdata` 将来使用。

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Jenkins 中的 CI 或 CD 管道模板

若要将这些模板添加到存储库，你将需要[你的 jenkins-ci-template 版本。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile)和[jenkins-cd-template。要按分支位于存储库中的 Jenkinsfile。](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)

此外，你需要在 Jenkins 中创建 CI 或 CD 管道，这些管道指向相应的特定 **Jenkinsfile。**

按照以下步骤检查如何将 Jenkins 连接到不同的 SCM 平台：

1. [Jenkins 和 GitHub](https://www.jenkins.io/solutions/github/)
2. [Jenkins 和 Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [具有 GitLab 的 Jenkins](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [具有 Bitbucket 的 Jenkins](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>自定义 CI 管道

您可以进行一些潜在更改来调整项目：

1. 将模板文件重命名为 **Jenkinsfile，** 这是一种常见做法，并将其放在目标分支（例如， **开发** 分支）下。
1. 更改 CI 流的触发。 我们默认在将新更改推送到开发人员分支时使用 **pollSCM** **的** 触发器。
1. 确保你拥有 npm 生成脚本，或自定义在自动化代码中生成的方式。
1. 确保有一个 npm 测试脚本，该脚本返回零以成功，并且/或更改测试命令。

### <a name="customize-cd-pipeline"></a>自定义 CD 管道

更改以下步骤以自定义 CD 管道：

1. 将模板文件重命名为 **Jenkinsfile，** 这是一种常见做法，并将其放在目标分支（例如， **主** 分支）下。
1. 如何触发 CD 流。 我们默认在将新更改推送到主分支时使用 **pollSCM** **的** 触发器。
1. 创建 Jenkins[管道凭据](https://www.jenkins.io/doc/book/using/using-credentials/)以保留 Azure/Microsoft 365登录凭据。 下表列出了在 Jenkins 上需要创建的所有凭据。
1. 如有必要，请更改生成脚本。
1. 如果没有测试，请删除测试脚本。

> [!Note]
 预配步骤不包含在 CD 模板中，因为它通常只执行一次。 可以在 TeamsFx CLI Teams Toolkit内执行预配，或者使用单独的工作流。 请记住，在预配 (预配结果将保存在文件夹) 中，将 的文件内容保存到 `.fx` Jenkins 凭据中供 `.fx/states/{YOUR_ENV_NAME}.userdata` 将来使用。

### <a name="environment-variables-for-jenkins"></a>Jenkins 的环境变量

按照 [using-credentials](https://www.jenkins.io/doc/book/using/using-credentials/) 在 Jenkins 上创建凭据。

|名称|说明|
|---|---|
|AZURE_ACCOUNT_NAME|用于预配资源的 Azure 的帐户名称。|
|AZURE_ACCOUNT_PASSWORD|Azure 帐户的密码。|
|AZURE_SUBSCRIPTION_ID|确定将在其中预配资源的订阅。|
|AZURE_TENANT_ID|标识订阅所在的租户。|
|Microsoft 365_ACCOUNT_NAME|用于创建和发布 Teams 应用的 M3icrosoft 365 帐户。|
|Microsoft 365_ACCOUNT_PASSWORD|帐户Microsoft 365密码。|
|Microsoft 365_TENANT_ID|标识将在其中创建Teams/发布的租户。 此值是可选的，除非你拥有多租户帐户并且想要使用另一个租户。 阅读更多[有关如何查找租户Microsoft 365 ID。](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|
> 注意：请参阅配置[Microsoft 365/Azure](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret)凭据，以确保已针对管道中使用的凭据禁用多重身份验证和安全默认值。

## <a name="get-started-guide-for-other-platforms"></a>适用于其他平台的入门指南

你可以按照列出的预定义示例 Bash 脚本在其他平台上构建和自定义 CI 或 CD 管道：

* [CI 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) 脚本相当简单，大多数部分都是跨平台 CLI，因此很容易将其转换为其他类型的脚本，例如 PowerShell。

这些脚本基于跨平台 TeamsFx 命令行工具[TeamsFx-CLI。](https://www.npmjs.com/package/@microsoft/teamsfx-cli) 可以随文档一 `npm install -g @microsoft/teamsfx-cli` 起安装脚本 [，然后](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) 按照文档自定义脚本。

> [!Note]
> 若要启用 `@microsoft/teamsfx-cli` 在 CI 模式下运行，请通过 `CI_ENABLED` 打开 `export CI_ENABLED=true` 。 在 CI 模式下 `@microsoft/teamsfx-cli` ，适用于 CI 或 CD。

确保在环境变量中安全设置 Azure 和 M365 凭据。 例如，如果你使用 GitHub 作为源代码存储库，可以使用[Github 密码](https://docs.github.com/en/actions/reference/encrypted-secrets)安全地存储环境变量。

## <a name="publish-teams-app-using-teams-developer-portal"></a>使用Teams门户发布Teams应用

如果存在与应用清单Teams相关的任何更改，可能需要再次发布Teams应用以更新清单。

若要手动Teams应用，你可以利用[开发人员门户进行Teams。](https://dev.teams.microsoft.com/home)

**发布应用**

1. 使用[相应帐户Teams](https://dev.teams.microsoft.com)开发人员门户进行登录。
2. 通过选择 以 zip 导入你的应用包 `App -> Import app -> Replace` 。
3. 在应用列表中选择目标应用，你将转到概述页面。
4. 通过选择发布应用 `Publish -> Publish to your org`

### <a name="see-also"></a>另请参阅

* [快速入门GitHub操作](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [创建第一个Azure DevOps管道](/azure/devops/pipelines/create-first-pipeline)
* [创建首个 Jenkins 管道](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
