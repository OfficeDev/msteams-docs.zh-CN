---
title: 为你的应用设计自适应卡
description: 了解如何设计 Microsoft Teams 自适应卡并获取 Microsoft Teams UI Kit。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b016df98d57b9a3f5fe03e6cf26b31ad2d7b8db9
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887962"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>为 Microsoft Teams 应用设计自适应卡

自适应卡片包含卡片元素的自由格式正文和一系列可选操作。 自适应卡片是可操作的内容片段，可通过机器人或消息传递扩展添加到对话。 这些卡片使用文本、图形和按钮为受众提供丰富的通信体验。

自适应卡框架用于许多 Microsoft 产品，包括 Microsoft Teams。 可以通过机器人或消息传递扩展向用户发送消息内的卡片。 用户还可以在卡片上执行操作（如果存在）。

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="自适应卡概述示例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可在 Microsoft Teams UI Kit 中查看更全面的 Microsoft Teams 自适应卡设计指南，包括可根据需要获取和修改的元素。 UI 配套伯还涵盖主题、辅助功能和响应式大小等重要主题。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit（用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>自适应卡设计器

还可以直接在浏览器中开始设计自适应卡。

> [!div class="nextstepaction"]
> [适用自适应卡设计器](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>自适应卡类型

### <a name="hero"></a>主图

我们最大的卡片。用于共享用一张图像讲述大部分故事的文章或场景。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="示例显示了移动设备上的自适应卡主图卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="示例显示了自适应卡主图卡。" border="false":::

### <a name="thumbnail"></a>缩略图

用于发送简单的可操作消息。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="示例显示了移动设备上的自适应卡缩略图卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="示例显示了自适应卡缩略图卡。" border="false":::

### <a name="list"></a>列表

当你希望用户从列表中选中一项，但项不需要大量解释时使用。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="示例显示了移动设备上的自适应卡列表卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="示例显示了自适应卡列表卡。" border="false":::

### <a name="digest"></a>摘要

用于新闻摘要和综述文章。 注意: 建议单个更新或新闻项目采用缩略图卡。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="示例显示了移动端上的自适应卡摘要卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="示例显示了自适应卡的摘要卡。" border="false":::

### <a name="media"></a>媒体

在想要结合文本和媒体（如音频或视频）时使用。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="示例显示了移动设备上的自适应卡媒体卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="示例显示了自适应卡媒体卡。" border="false":::

### <a name="people"></a>人员

最适合用于有效传达任务相关人员。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="示例显示了移动设备上的自适应卡人员卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="示例显示了自适应卡人员卡。" border="false":::

### <a name="request-ticket"></a>请求票证

用于从用户获取快速输入以自动创建任务或票证。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="示例显示了移动设备上的自适应卡请求票证卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="示例显示了自适应卡请求票证卡。" border="false":::

### <a name="imageset"></a>ImageSet

用于发送多个图像缩略图。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="示例显示了移动设备上的自适应卡图像集卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="示例显示了自适应卡图像集卡。" border="false":::

### <a name="actionset"></a>ActionSet

当希望用户选择按钮，然后从同一张卡中收集添加用户输入时使用。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="示例显示了移动设备上的自适应卡操作集卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="示例显示了自适应卡操作集卡。" border="false":::

### <a name="choiceset"></a>ChoiceSet

用于从一个用户收集多个输入。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="示例显示了移动设备上的自适应卡选择集卡。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="示例显示了自适应卡选择集卡。" border="false":::

## <a name="anatomy"></a>解剖

自适应卡片具有极强的灵活性。 但作为最低要求，我们强烈建议在每张卡片中包含以下组件。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="示例：移动设备上的自适应卡片解剖。" border="false":::

|计数器|说明|
|----------|-----------|
|A|**标题**：让标题清晰简洁。|
|B|**正文文案**：传达过长或不够重要，不足以放在标题中的内容。|
|C|**主要操作**：作为最佳做法，包括 1-3 个主要操作。 可最多有 6 个。|

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="示例显示了自适应卡片解剖。" border="false":::

|计数器|说明|
|----------|-----------|
|A|**标题**：让标题清晰简洁。|
|B|**正文文案**：传达过长或不够重要，不足以放在标题中的内容。|
|C|**主要操作**：作为最佳做法，包括 1-3 个主要操作。 可最多有 6 个。|

## <a name="best-practices"></a>最佳实践

专为窄屏幕设计的卡片在宽屏幕上可以很好地缩放（反之则不然）。 你还应该假设用户不会只在桌面上查看你的卡片。

### <a name="column-layouts"></a>列布局

使用 [`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html) 将卡片内容格式化为表格或网格。 有几种设置列宽格式的选项。 这些指南可帮助你了解何时使用每个指南。

* `"width": "auto"`：`ColumnSet` 中每个列的大小，适合包含到该列中的任何应用内容。
   * **请**：当你有不同宽度的内容并且不需要优先考虑特定列时使用。
   * **请**：对于每个 `TextBlock`，设置 `"wrap": true`，因为默认情况下文本不换行。
   * **请勿**：对每个列容器设置 `"width": "auto"`。 例如，如果你有一个并排的输入和按钮，则该按钮可能会在某些屏幕上被切断。 相反，为带有按钮和其他其他必须始终完全可见的内容的列设置为 `auto`。
* `"width": "stretch"`：根据可用的 `ColumnSet` 宽度调整列大小。 当多个列使用 `"stretch"` 值时，它们平均共享可用宽度。
   * **请**：如果所有其他列都有静态宽度，请与一列一同使用。 例如，在一列中有宽 50 像素的缩略图。
* `"width": "<number>"`：使用可用的 `ColumnSet` 宽度的比例调整列大小。 例如，如果使用 `"width": "1"`、`"width": "4"` 和 `"width": "5"` 设置三列，则各列将占可用宽度的 10%、40% 和 50%。
* `"width": "<number>px"`：将列大小调整为特定的像素宽度。 此方法在创建表时很有用。
   * **请**：在显示的内容的宽度不需要更改时使用（例如，数字和百分比）。
   * **请勿**：意外超过卡片可以显示的宽度。 请记住，可用屏幕宽度取决于设备。 Teams 移动版也不支持像 Teams 桌面版那样的水平滚动。

#### <a name="example-knowing-when-to-stretch-columns"></a>示例：了解何时拉伸列

# <a name="design"></a>[设计](#tab/design)

**请**：在此屏幕中，将卡片底部设为两列。 输入组件宽度设置为 `stretch`，而 **选择** 按钮宽度设置为 `auto`。 这将确保按钮完全保留在视图中。

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="图像显示如何在自适应卡片中设置列宽。":::

**请勿**：在此屏幕中，将两列 `width` 均设置为 `auto`。 与输入相比，这会导致右侧的 **选择** 按钮被略微切断。

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-dont.png" alt-text="图像显示如何不在自适应卡片中设置列宽。":::

# <a name="code"></a>[代码](#tab/code)

下面是用于实现应遵循的设计示例的代码。

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.2",
  "body": [
    {
      "type": "TextBlock",
      "text": "I wasn't able to identify the type of expense. Select from the list:",
      "wrap": true,
      "id": "typePrompt",
      "spacing": "Medium",
      "size": "Medium"
    },
    {
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Submit",
          "title": "Phone Bill",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Phone Bill",
              "action": "Phone Bill"
            },
            "action": "Phone Bill"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Taxi and Other Transportation",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Taxi and Other Transportation",
              "action": "Taxi and Other Transportation"
            },
            "action": "Taxi and Other Transportation"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Entertainment_misc",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Entertainment_misc",
              "action": "Entertainment_misc"
            },
            "action": "Entertainment_misc"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Car Rental",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Car Rental",
              "action": "Car Rental"
            },
            "action": "Car Rental"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Airfare",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Airfare",
              "action": "Airfare"
            },
            "action": "Airfare"
          }
        }
      ],
      "spacing": "Medium"
    },
    {
      "type": "TextBlock",
      "text": "     ",
      "wrap": true
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "Input.ChoiceSet",
              "choices": [
                {
                  "title": "Meals",
                  "value": "Meals"
                },
                {
                  "title": "Parking/Tolls",
                  "value": "Parking/Tolls"
                },
                {
                  "title": "Accomodation",
                  "value": "Accomodation"
                },
                {
                  "title": "Fuel-Gas/Petrol/Diesel",
                  "value": "Fuel-Gas/Petrol/Diesel"
                },
                {
                  "title": "Hotel",
                  "value": "Hotel"
                },
                {
                  "title": "Meals - Employees Only",
                  "value": "Meals - Employees Only"
                },
                {
                  "title": "Accomodations",
                  "value": "Accomodations"
                },
                {
                  "title": "Misc.Expenses",
                  "value": "Misc.Expenses"
                },
                {
                  "title": "Please Categorize",
                  "value": "Please Categorize"
                }
              ],
              "placeholder": "All",
              "id": "expenseTypes",
              "value": "Meals - Employees Only"
            }
          ]
        },
        {
          "type": "Column",
          "width": "auto",
          "items": [
            {
              "type": "ActionSet",
              "actions": [
                {
                  "type": "Action.Submit",
                  "title": "Select",
                  "data": {
                    "msteams": {
                      "type": "messageBack",
                      "displayText": "Select",
                      "action": "applyType"
                    },
                    "action": "applyType"
                  }
                }
              ]
            }
          ]
        }
      ],
      "spacing": "ExtraLarge"
    }
  ]
}
```

---

#### <a name="example-using-fewer-columns"></a>示例：使用较少的列

**请**：在具有较少列的移动设备上显示布局效果更佳。

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-do.png" alt-text="图像显示自适应卡片中正确数量的列。":::

**请勿**：使用过多的列会使你的卡片内容在移动设备上变得混乱。

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-dont.png" alt-text="图像显示太多列会对自适应卡片布局产生负面影响。":::

#### <a name="example-fixed-width-has-its-place"></a>示例：固定宽度有其位置

# <a name="design"></a>[设计](#tab/design)

当显示内容的大小不需要更改时，将列设置为特定的像素宽度。 此示例显示大小为 50 像素的左列，而缩略图旁边的说明会拉伸卡片的长度

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="图像显示如何在自适应卡片中设置列宽。":::

# <a name="code"></a>[代码](#tab/code)

下面是用于实现设计示例的代码。

```json
{
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "Pick up where you left off?",
      "weight": "bolder"
    },
    {
      "type": "ColumnSet",
      "spacing": "medium",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1083",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "Silver Star Mountain Range"
            },
            {
              "type": "TextBlock",
              "text": "Maps",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.msn.com"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1082",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "style": "emphasis",
          "items": [
            {
              "type": "TextBlock",
              "text": "Kitchen Remodel for Homes"
            },
            {
              "type": "TextBlock",
              "text": "With EMPHASIS",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.AdaptiveCards.io"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1080",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "The Witcher: A Series"
            },
            {
              "type": "TextBlock",
              "text": "Netflix",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.outlook.com"
      }
    }
  ],
  "actions": [
    {
      "type": "Action.OpenUrl",
      "title": "Resume all",
      "url": "ms-cortana:resume-all"
    },
    {
      "type": "Action.OpenUrl",
      "title": "More activities",
      "url": "ms-cortana:more-activities"
    }
  ]
}
```

---

### <a name="text"></a>Text

无论是使用 [`TextBlock`](https://adaptivecards.io/explorer/TextBlock.html)、[`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html) 或 [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html)，将 `wrap` 属性设置为 `true`，这样卡片文本不会在移动电话上截断。

#### <a name="example-making-sure-text-doesnt-truncate"></a>示例：确保文本不截断

# <a name="design"></a>[设计](#tab/design)

**请**：在此屏幕中，将卡片的 `wrap` 属性设置为 `true`。 这允许文本适应任何屏幕大小。

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-true.png" alt-text="图像显示如何在自适应卡片中换行文本。":::

**请勿**：在此屏幕中，卡片不使用 `wrap` 属性，因此文本在移动屏幕上被切断。

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-false.png" alt-text="图像显示如果不在自适应卡片中换行，会发生什么情况。":::

# <a name="code"></a>[代码](#tab/code)

下面是用于实现应遵循的设计示例的代码。

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "What cuisine do you want?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor",
      "style": "compact",
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Chineese",
          "value": "1"
        },
        {
          "title": "Indian",
          "value": "2"
        },
        {
          "title": "Italian",
          "value": "3"
        }
      ]
    },
    {
      "type": "TextBlock",
      "text": "Select the dishes that you like?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor2",
      "style": "expanded",
      "wrap" : true,
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Cauliflower with potatoes sautéed with garam masala",
          "wrap" : true,
          "value": "1"
        },
        {
          "title": "Patties of potato mixed with some vegetables fried",
          "wrap" : true,
          "value": "2"
        },
        {
          "title": "Green capsicum with potatoes sautéed with cumin seeds",
          "wrap" : true,
          "value": "3"
        }
      ]
    }
  ]
}
```

---

### <a name="containers"></a>容器

使用 `Container` 可以将一组相关元素组合在一起。

* **请**：使用 `style` 属性突出容器。
* **请**：使用 `selectAction` 属性将操作与容器中的其他元素关联。
* **请**：使用 `Action.ToggleVisibility` 属性使一组元素可折叠。
* **请勿**：出于上述原因以外的任何原因使用容器。

### <a name="images"></a>图像

在卡片中包含图像时，请遵循以下指南。

* **请**：为高 DPI 屏幕设计图像以避免像素化。 在 50x50 像素下显示 100x100 像素图像比以其他方式显示效果更好。
* **请**：如果你需要控制图像的确切大小，请使用 `width` 和 `height` 属性。
* **请勿**：在图像中包含填充。 这通常会引入不需要的间距和布局问题。
* 关于背景色：
   * **请**：使用透明背景，使图像适应任何 Teams 主题。 
   * **请勿**：包含固定的背景色，除非用户必须看到特定颜色。
   * **请勿**：将背景色添加到 `TextBlock`，损害可读性。 例如，如果你的背景为深色，则使用较浅的文本颜色，反之亦然。

### <a name="actions"></a>操作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="有关如何在自适应卡上仅包含一小组操作的最佳实践。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>建议：最多使用六个主要操作

虽然自适应卡可以支持六个主要操作，但大多数卡并不需要这么多。 操作应做到清晰、简洁且直接。 操作越少，效率越高。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="有关如何避免在自适应卡上添加过多操作，而让用户感到不知所措的最佳实践。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>不建议：使用超过六个主要操作

自适应卡应提供快速、可操作的内容。 操作过多可能会使用户不知所措。

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>频率

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="有关自适应卡频率的最佳实践。" border="false":::

#### <a name="do-be-concise"></a>建议：做到简洁

将多个卡片发送到对话很容易，但一旦卡片滚动出视图，就会变得没那么有用。 尝试限制自己只传达必要内容。 在用户对自己认为是“干扰”的内容，容忍度更低的频道中尤其应注意这一点。

## <a name="see-also"></a>另请参阅

* [卡片和任务模块](~/task-modules-and-cards/cards-and-task-modules.md)
* [Teams 机器人中支持的卡片和任务模块](~/task-modules-and-cards/what-are-task-modules.md)
* [使用自适应卡的通用操作](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/work-with-universal-actions-for-adaptive-cards.md)
* [响应任务模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [用户特定视图](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/user-specific-views.md)
