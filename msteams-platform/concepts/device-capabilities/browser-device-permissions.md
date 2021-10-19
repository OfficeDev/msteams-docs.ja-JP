---
title: ブラウザーのデバイスのアクセス許可
keywords: teams アプリの機能のアクセス許可
description: Web クライアントのアプリに対するデバイスのアクセス許可のサポートを安全に取り戻す
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: b2e83ca784e5459edfd80a3862610ebab2f8df30
ms.sourcegitcommit: ce956267b620f807e15e6d2df7afa022ffacc22f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2021
ms.locfileid: "60496240"
---
# <a name="device-permissions-for-the-browser"></a>ブラウザーのデバイスのアクセス許可

> [!NOTE]
> ブラウザーでのデバイスのアクセス許可の処理方法の変更は、現在パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。 この変更は、2022 年 1 月 21 日までに一般に利用可能になります (GA)。

カメラやマイク へのアクセスなど、デバイスのアクセス許可を必要とするアプリケーションでは、Web ブラウザーのアプリ レベルごとにユーザーが手動で同意を付与する必要があります。 以前は、ブラウザーは、これらのアクセス許可の付与方法を処理しましたが、これらのアクセス許可は現在、Microsoft Teams。 これは、ブラウザーでこれらのアクセス許可が必要な場合にアプリケーションを設計する方法に影響します。

## <a name="change-in-behavior"></a>動作の変更
アプリケーションがアプリケーション マニフェストでデバイスのアクセス許可を必要とすると[](native-device-permissions.md)宣言した場合、ユーザーはアプリのデバイスのアクセス許可を有効にできる "アプリのアクセス許可" オプションが表示されます。 [アプリのアクセス許可] オプションは、個人用アプリ、タスク モジュール ダイアログ、チャット、チャネル、会議のタブに表示されます。

### <a name="personal-apps-and-task-module-dialogs"></a>個人用アプリとタスク モジュールのダイアログ
"アプリのアクセス許可" 設定は、右の右側に表示されます。
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

### <a name="chat-channel-or-meeting-tabs"></a>チャット、チャネル、または会議のタブ
[アプリのアクセス許可] 設定は、タブドロップダウンにあります。
![[アプリのアクセス許可] ドロップダウン](../../assets/images/tabs/drop-downapppermissions.png)

ユーザーは、これらのアクセス許可を有効にするには、ブラウザーでこれらのアクセス許可を有効にする必要があります。 ユーザーがブラウザーでアプリのデバイスのアクセス許可を変更すると、アプリケーションをブラウザーで再読み込みするように求Teams。 これらのアクセス許可を有効にするには、ユーザーに移動先を認識Microsoft Teams。

## <a name="recommendation"></a>推奨事項
Microsoft Teamsでデバイスのアクセス許可を必要とするアプリケーションでは、これらのアクセス許可を見つけて有効にする場所に関する指示がユーザーに表示Teamsされます。 アプリケーションが実行されているコンテキストに応じて、個人用アプリ、タスク モジュール ダイアログ、チャット、チャネル、会議のタブと異なって、これらのアクセス許可にアクセスするための場所をユーザーに正しく指示していることを確認する必要があります。

<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="see-also"></a>関連項目

* [デバイス機能の概要](device-capabilities-overview.md)
* [デバイスのアクセス許可を要求する](native-device-permissions.md)
