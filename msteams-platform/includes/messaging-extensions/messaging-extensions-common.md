## <a name="add-a-message-extension-to-your-app"></a>向应用添加消息扩展

消息扩展是云托管的服务，用于侦听用户请求并使用结构化数据（如 [卡片](~/task-modules-and-cards/what-are-cards.md)）进行响应。 通过 Bot Framework `Activity` 对象将服务与 Microsoft Teams 集成。 Bot Builder SDK 的 .NET 和 Node.js 扩展可以帮助你向应用添加消息扩展功能。

![消息扩展的消息流图](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>在 Bot Framework 中注册

如果尚未这样做，则必须先将机器人注册到 Microsoft Bot Framework。 机器人的 Microsoft 应用 ID 和回调终结点将在消息扩展插件中用于接收和响应用户请求。 请记住为机器人启用 Microsoft Teams 通道。

记录机器人应用 ID 和应用密码，需要在应用清单中提供应用 ID。

### <a name="update-your-app-manifest"></a>更新应用清单

与机器人和选项卡一样，更新 [应用清单以](~/resources/schema/manifest-schema.md#composeextensions) 包含消息扩展属性。 这些属性控制消息扩展在 Microsoft Teams 客户端中的显示和行为方式。 从清单的 v1.0 开始支持消息扩展。

#### <a name="declare-your-message-extension"></a>声明消息扩展

若要添加消息扩展插件，请在清单 `composeExtensions` 中包含具有该属性的新顶级 JSON 结构。 目前，只能为应用创建单个消息扩展。

> [!NOTE]
> 清单将消息扩展名引用为 `composeExtensions`。 这是为了保持向后兼容性。

扩展定义是具有以下结构的对象：

| 属性名称 | 用途 | 是否必需？ |
|---|---|---|
| `botId` | 使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 这通常应与整个 Teams 应用的 ID 相同。 | 是 |
| `scopes` | 声明是否可以将此扩展添加到 `personal` (或 `team`) 范围的数组。 | 是 |
| `canUpdateConfiguration` | 启用 **“设置”** 菜单项。 | 否 |
| `commands` | 此消息扩展支持的命令数组。 你只能使用 10 个命令。 | 是 |

#### <a name="define-commands"></a>定义命令

消息扩展应声明一个命令，当用户从撰写框中的“ **更多”选项** 中选择应用 (**&#8943;**) 按钮时，将显示该命令。

![Teams 中消息扩展列表的屏幕截图](~/assets/images/compose-extensions/compose-extension-list.png)

在应用清单中，命令项是具有以下结构的对象：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 分配给此命令的唯一 ID。 用户请求将包含此 ID。 | 是 | 1.0 |
| `title` | 命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `description` | 帮助文本，指示此命令的作用。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 设置命令的类型。 可取值包括 `query` 和 `action`。 如果没有，则将默认值设置为 `query`。 | 否 | 1.4 |
| `initialRun` | 可选参数，与命令一起 `query` 使用。 如果设置为 **true**，则指示用户在 UI 中选择此命令后应立即执行此命令。 | 否 | 1.0 |
| `fetchTask` | 可选参数，与命令一起 `action` 使用。 设置为 **true** 以提取要在 [任务模块](~/task-modules-and-cards/what-are-task-modules.md)中显示的自适应卡片或 Web URL。 当对命令的 `action` 输入是动态的，而不是一组静态参数时，将使用此方法。 请注意，如果设置为 **true** ，则忽略该命令的静态参数列表。 | 否 | 1.4 |
| `parameters` | 命令的参数静态列表。 | 是 | 1.0 |
| `parameter.name` | 参数的名称。 这会在用户请求中发送到服务。 | 是 | 1.0 |
| `parameter.description` | 描述此参数的目的或应提供的值的示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 设置为所需的输入类型。 可能的值包括`text`， `textarea`， `number`， `date`， `time`。 `toggle` 默认设置为 `text`. | 否 | 1.4 |
| `context` | 定义消息操作可用上下文的值的可选数组。 可能的值为`message`或 `compose``commandBox`. 默认值为“`["compose", "commandBox"]`”。 | 否 | 1.5 |
