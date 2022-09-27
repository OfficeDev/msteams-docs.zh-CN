---
title: Teams Toolkit for Visual Studio 中的 Teams 应用清单
author: surbhigupta
description: 在本模块中，了解如何在 Visual Studio 的不同环境中编辑、预览和自定义 Teams 应用清单。
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: c391df383c97638d3c8ff5944afab75db2400580
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027437"
---
# <a name="edit-teams-app-manifest-using-visual-studio"></a>使用 Visual Studio 编辑 Teams 应用清单

Visual Studio 中的 Teams 工具包通过预配和`config.{env}.json`准备应用依赖项时的配置`state.{env}.json`加载清单`manifest.template.json`。 还可以使用清单在 [开发人员门户](https://dev.teams.microsoft.com/apps) 中创建 Microsoft Teams 应用。

在基架之后，在文件夹下 `templates/appPackage` 的清单模板文件中， `manifest.template.json` 在本地和远程环境之间共享。

在清单模板中，选择 **“Project** > **Teams 工具包** > **打开清单文件**”。

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="打开清单文件":::

### <a name="customize-app-manifest-in-teams-toolkit"></a>在 Teams 工具包中自定义应用清单

以下两种类型的占位符 `manifest.template.json`：

- `{{state.xx}}` 是预定义的占位符，其值由 Teams 工具包解析，在其中 `state.{env}.json`定义。 建议不要修改其中的值 `state.{env}.json`。
- `{{config.manifest.xx}}` 是自定义占位符，其值从 `config.{env}.json`中解析。

可以通过以下方式添加自定义参数：

- 使用模式添加占位符 `manifest.template.json` ： `{{config.manifest.xx}}`.
- 在 `config.{env}.json`中添加配置值 。

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### <a name="preview-app-manifest-in-teams-toolkit"></a>Teams 工具包中的预览应用清单

可通过两种方式预览应用清单中的值：

- 将鼠标悬停在占位符上 `manifest.template.json`时，可以看到 **开发** 和 **本地** 环境的值。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="将鼠标悬停在占位符上":::

- 除了每个占位符 `manifest.template.json`之外，还可以将鼠标悬停在键上，可以查看 **开发** 和 **本地** 环境的相同值。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="将鼠标悬停在占位符旁边的键上":::

   > [!NOTE]
   > 如果尚未预配环境，或者 Teams 应用依赖项尚未准备，则表示尚未生成占位符的值。 请按照悬停内的指南生成相应的值。

### <a name="preview-manifest-file"></a>预览清单文件

可以通过执行以下步骤预览清单文件：

- 选择 **“Project** > **Teams 工具包”** 菜单，并在 **云中** 触发 **“准备 Teams 应用依赖项**”或“预配”，以便为本地或远程 Teams 应用生成配置。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="预览清单文件":::

- 若要使用真实内容预览清单，Teams 工具包将生成预览清单文件，右键单击 **appPackage** 文件夹下的 **manifest.template.json**。 选择 **适用于本地** 或 **Azure 的****预览清单文件** > 。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="预览上下文菜单":::

还有两种预览清单文件的方法：

- 选择 **Project** > **Teams 工具包** > **Zip 应用包** ，然后选择 **“本地** ”或 **“用于 Azure**”。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Zip 应用包":::

- 如果右键单击项目名称，然后在 **解决方案资源管理器下选择** **Teams 工具包**，则还可以看到 Project > Teams 工具包下的相同菜单列表。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="解决方案资源管理器中的 Teams 工具包菜单列表":::

    > [!NOTE]
    >在此方案中，项目名称为 **MyTeamsApp1**。

### <a name="sync-local-changes-to-developer-portal"></a>将本地更改同步到开发人员门户

预览清单文件后，本地更改可以同步到开发人员门户。 **在 Teams 开发人员门户中** 选择 **Project** > **Teams 工具包** > 更新清单，或从解决方案资源管理器中选择上下文菜单。

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Teams 开发人员门户中的更新清单":::

> [!NOTE]
> 更改将更新到 Teams 开发人员门户。 如果开发人员门户中有一些手动更新，则可以覆盖这些更新。 在 **“警告** ”对话框中，可以选择“ **覆盖”和“更新** ”或 **“取消**”。

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="更新警告":::

## <a name="see-also"></a>另请参阅

- [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
- [使用 Visual Studio 将 Teams 应用部署到云](deploy-teams-app.md)
