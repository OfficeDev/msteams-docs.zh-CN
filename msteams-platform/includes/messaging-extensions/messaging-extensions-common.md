## <a name="add-a-messaging-extension-to-your-app"></a>向您的应用程序添加消息扩展插件

邮件扩展是云托管的服务，它可侦听用户请求并使用结构化数据（如[卡片](~/task-modules-and-cards/what-are-cards.md)）进行响应。 您可以通过 Bot 框架`Activity`对象将服务与 Microsoft 团队集成。 用于机器人生成器 SDK 的 .NET 和 node.js 扩展可帮助您向您的应用程序添加消息扩展功能。

![邮件传递扩展的邮件流关系图](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>在 Bot 框架中注册

如果尚未执行此操作，则必须先在 Microsoft Bot 框架中注册一个 bot。 你的 bot 的 Microsoft app ID 和回叫终结点（定义在这里）将在你的邮件扩展中用于接收和响应用户请求。 请记住为你的机器人启用 Microsoft 团队频道。

记录你的 bot 应用 ID 和应用密码，将需要在你的应用程序清单中提供应用程序 ID。

### <a name="update-your-app-manifest"></a>更新应用程序清单

与 bot 和选项卡一样，您可以更新应用程序的[清单](~/resources/schema/manifest-schema.md#composeextensions)以包含邮件扩展属性。 这些属性控制您的邮件扩展在 Microsoft 团队客户端中的显示和行为。 从清单的1.0 版开始，支持邮件扩展。

#### <a name="declare-your-messaging-extension"></a>声明消息扩展

若要添加消息扩展，请在清单中将新的顶级 JSON 结构包含在`composeExtensions`属性中。 目前，您仅限于为您的应用程序创建一个邮件扩展插件。

> [!NOTE]
> 清单将邮件传递扩展作为`composeExtensions`引用。 这是为了保持向后兼容性。

扩展定义是一个具有以下结构的对象：

| 属性名称 | 用途 | 是否必需？ |
|---|---|---|
| `botId` | 与 Bot 框架一起注册的 bot 的唯一 Microsoft 应用 ID。 通常应与整个团队应用程序的 ID 相同。 | 是 |
| `scopes` | 数组声明此扩展是否可以添加到`personal`或`team`范围（或两者）。 | 是 |
| `canUpdateConfiguration` | 启用 "**设置**" 菜单项。 | 否 |
| `commands` | 此消息扩展支持的命令数组。 限制为10个命令。 | 是 |

#### <a name="define-commands"></a>定义命令

您的邮件扩展应声明一个命令，当用户从 "撰写" 框中的 "**更多选项**（**&#8943;**）" 按钮中选择您的应用程序时，将显示该命令。

![团队中的邮件扩展列表的屏幕截图](~/assets/images/compose-extensions/compose-extension-list.png)

在应用程序清单中，您的命令项是一个具有以下结构的对象：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 您分配给此命令的唯一 ID。 用户请求将包括此 ID。 | 是 | 1.0 |
| `title` | 命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `description` | 指示此命令执行的操作的帮助文本。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 设置命令的类型。 可取值包括 `query` 和 `action`。 如果不存在，则默认值设置为`query` | 否 | 1.4 |
| `initialRun` | 与命令一起使用的`query`可选参数。 如果设置为**true**，则指示应在用户在 UI 中选择此命令后立即执行此命令。 | 否 | 1.0 |
| `fetchTask` | 与命令一起使用的`action`可选参数。 设置为**true**以提取在[任务模块](~/task-modules-and-cards/what-are-task-modules.md)中显示的自适应卡片或 web url。 当`action`命令的输入是动态的，而不是一组静态参数时，将使用此参数。 请注意，如果设置为**true** ，则忽略命令的静态参数列表 | 否 | 1.4 |
| `parameters` | 命令的参数的静态列表。 | 是 | 1.0 |
| `parameter.name` | 参数的名称。 此项将发送到用户请求中的服务。 | 是 | 1.0 |
| `parameter.description` | 描述了此参数的用途或应提供的值的示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 短用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 设置为所需的输入类型。 可能的值`text`包括`textarea`、 `number`、 `date`、 `time`、 `toggle`、。 默认值设置为`text` | 否 | 1.4 |
| `context` | 用于定义消息操作在中可用的上下文的可选值数组。 可能的值`message`为`compose`、或`commandBox`。 默认值为 `["compose", "commandBox"]`。 | 否 | 1.5 |
