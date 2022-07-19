---
title: Live Share 媒体功能
author: surbhigupta
description: 在本模块中，详细了解 Live Share 媒体功能、挂起和等待点、音频闪烁以及同步视频和音频。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: bf9d7c071a337a56373a9c58879d23a8d2638af7
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841873"
---
# <a name="live-share-media-capabilities"></a>Live Share 媒体功能

视频和音频是现代世界和工作场所的重要部分。 我们收到了广泛的反馈，建议我们还可以采取更多措施来提高在会议中一起观看视频的质量、辅助功能和许可证保护。

Live Share SDK 使 **媒体能够同步** 到任何 HTML `<video>` 和 `<audio>` 元素比以往更简单。 通过在播放器状态和传输控件层同步媒体，可以单独赋予视图和许可证，同时提供通过应用可获得的最高质量。

## <a name="install"></a>安装

若要使用 npm 将最新版本的 SDK 添加到应用程序，请执行以下操作：

```bash
npm install @microsoft/live-share --save
npm install @microsoft/live-share-media --save
```

OR

若要使用 [Yarn](https://yarnpkg.com/) 将最新版本的 SDK 添加到应用程序，请执行以下操作：

```bash
yarn add @microsoft/live-share
yarn add @microsoft/live-share-media
```

## <a name="media-sync-overview"></a>媒体同步概述

Live Share SDK 有两个与媒体同步相关的主类：

| 课程                                                                                                                  | 说明                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| [EphemeralMediaSession](/javascript/api/@microsoft/live-share-media/ephemeralmediasession)     | 自定义临时对象，旨在协调独立媒体流中的媒体传输控件和播放状态。 |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | 将本地 HTML 媒体元素与 `EphemeralMediaSession` 的一组远程 HTML 媒体元素同步。|

示例：

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { EphemeralMediaSession } from "@microsoft/live-share-media";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Setup the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { mediaSession: EphemeralMediaSession },
};
const { container } = await client.joinContainer(schema);
const { mediaSession } = container.initialObjects;

// Get the player from your document and create synchronizer
const player = document.getElementById("player");
const synchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles = ["Organizer", "Presenter"];
await mediaSession.start(allowedRoles);
```

`EphemeralMediaSession`自动侦听对组播放状态的更改，并通过 `MediaPlayerSynchronizer` 应用更改。 为了避免播放用户未有意启动的状态更改（如缓冲区事件），我们必须通过同步器调用传输控件，而不是直接通过播放器调用传输控件。

示例：

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
  <div class="player-controls">
    <button id="play-button">Play</button>
    <button id="pause-button">Pause</button>
    <button id="restart-button">Restart</button>
    <button id="change-track-button">Change track</button>
  </div>
</body>
```

```javascript
// ...

document.getElementById("play-button").onclick = () => {
  synchronizer.play();
};

document.getElementById("pause-button").onclick = () => {
  synchronizer.pause();
};

document.getElementById("restart-button").onclick = () => {
  synchronizer.seekTo(0);
};

document.getElementById("change-track-button").onclick = () => {
  synchronizer.setTrack({
    trackIdentifier: "SOME_OTHER_VIDEO_SRC",
  });
};
```

 > [!Note]
 > 虽然可以使用 `EphemeralMediaSession` 对象直接同步媒体，但除非你希望对同步逻辑进行更精细的控制，请使用 `MediaPlayerSynchronizer`。 根据你在应用中使用的玩家，你可能想要创建委托填充码，使 Web 播放器的界面与 HTML 媒体接口相匹配。

## <a name="suspensions-and-wait-points"></a>挂起和等待点

如果要暂时挂起 `EphemeralMediaSession` 对象的同步，可以使用挂起功能。 默认情况下，[MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/ephemeralmediasessioncoordinatorsuspension) 对象是本地对象，当用户可能想要跟进他们错过的内容、休息一下等等时，这很有帮助。 如果用户结束挂起，同步将自动恢复。

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

开始挂起时，还可以包含可选的 [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint) 参数，该参数允许用户定义所有用户应在其中发生挂起的时间戳。 在所有用户都已结束该等待点的挂起之前，同步不会恢复。 这对于在视频中的特定点添加测验或调查之类的内容非常有用。

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension();
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

## <a name="audio-ducking"></a>音频闪避

Live Share SDK 支持智能音频闪避。 可以在应用程序中使用 _实验性_ 功能，将以下内容添加到代码中：

```javascript
import * as microsoftTeams from "@microsoft/teams-js";

// ...

let volumeTimer;
microsoftTeams.meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

若要启用音频闪避，请将以下 [RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent) 权限添加到应用清单中：

```json
{
  // ...rest of your manifest here
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Chat",
          "type": "Delegated"
        },
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

> [!Note]
> 用于音频闪避的 `registerSpeakingStateChangeHandler` API 目前仅适用于正在讲话的非本地用户。

## <a name="code-samples"></a>代码示例

| 示例名称   | Description | JavaScript |
| -------------------- | ----------------------------| -----------------|
| React 视频          | 演示 EphemeralMediaSession 对象如何与 HTML5 视频配合工作的基本示例。                                                        | [View](https://aka.ms/liveshare-reactvideo)    |
| React 媒体模板 | 使所有连接的客户端能够一起观看视频、生成共享播放列表、转移在控制的人，并通过视频进行批注。 | [View](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [Agile Poker 教程](../sbs-teams-live-share.yml)

## <a name="see-also"></a>另请参阅

* [Live Share SDK 常见问题解答](teams-live-share-faq.md)
* [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
* [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
* [参考文档](https://aka.ms/livesharedocs)
* [会议中的 Teams 应用](teams-apps-in-meetings.md)
