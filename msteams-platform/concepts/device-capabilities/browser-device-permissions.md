---
title: ブラウザーのデバイスのアクセス許可
keywords: teams アプリの機能のアクセス許可
description: Web クライアントのアプリに対するデバイスのアクセス許可のサポートを安全に取り戻す
localization_priority: medium
ms.topic: how-to
ms.openlocfilehash: fbdca08c813d341c12fcfc824d21a6ff96d02749
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059787"
---
# <a name="device-permissions-for-the-browser"></a>ブラウザーのデバイスのアクセス許可

> [!NOTE]
> ブラウザーでのデバイスのアクセス許可の処理方法に関する最新の更新プログラムは、現在パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。 この更新プログラムは、2022 年 2 月 1 日までに一般提供 (GA) される予定です。


Teamsアクセスなど、デバイスのアクセス許可を必要とするアプリでは、Web ブラウザーでアプリごとのレベルで手動でアクセス許可をユーザーに付与する必要があります。 以前は、ブラウザーはアクセス許可を付与する方法を処理しましたが、これらのアクセス許可は現在、Microsoft Teams。 これは、アプリケーションの設計方法や、ブラウザーでこれらのアクセス許可が必要な場合に影響します。

## <a name="enable-apps-device-permissions"></a>アプリのデバイスのアクセス許可を有効にする
Teamsマニフェストでデバイスのアクセス許可が必要であると宣言されている[](native-device-permissions.md#specify-permissions)場合は、ユーザーがアプリのデバイスのアクセス許可を有効にするための [アプリのアクセス許可] オプションが表示されます。 [ **アプリのアクセス許可]** オプションは、次の機能で使用できます。 

* **個人用アプリとタスク モジュールのダイアログ**: [ **アプリの** アクセス許可] オプションは、ページの右上隅にあります。
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

* **チャット、チャネル、または会議のタブ**: [ **アプリの** アクセス許可] オプションは、タブのドロップダウンで使用できます。 ![[アプリのアクセス許可] ドロップダウン](../../assets/images/tabs/drop-downapppermissions.png)

[アプリ **のアクセス許可] オプション** を選択すると、ユーザーがアクセス許可ボタンを有効にできるポップアップが表示されます。

ユーザーは、これらのアクセス許可を有効にするには、ブラウザーでこれらのアクセス許可を有効にする必要があります。 ユーザーがブラウザーでアプリのデバイスのアクセス許可を変更すると、アプリケーションをブラウザーで再読み込Teams。

> [!IMPORTANT]
> これらのアプリのアクセス許可を有効にする場所をユーザーに認識させる必要Microsoft Teams。

## <a name="recommendation"></a>推奨事項
Teamsでデバイスのアクセス許可を必要とするアプリでは、ユーザーに対して、これらのアクセス許可を検索して有効にする場所に関する指示を UI で表示Teamsがあります。 アプリケーションが実行されているコンテキストに応じて、個人用アプリ、タスク モジュール ダイアログ、チャット内のタブ、チャネルまたは会議で異なっているので、これらのアクセス許可にアクセスするための場所を修正するための指示がユーザーに指示されていることを確認する必要があります。

</br>
<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | Node.js |
|----------------|-----------------|--------------|
| ブラウザーのタブ デバイスのアクセス許可 | サンプル コードは、ブラウザーのデバイスのアクセス許可を表示する方法を示しています。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

ステップ バイ[ステップ ガイドに従って](../../sbs-tab-device-permissions.yml)、タブ デバイスにアクセス許可を付与Microsoft Teams。

## <a name="see-also"></a>関連項目

* [デバイス機能の概要](device-capabilities-overview.md)
* [デバイスのアクセス許可を要求する](native-device-permissions.md)
