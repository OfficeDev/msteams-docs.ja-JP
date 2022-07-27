---
title: ブラウザーのデバイスのアクセス許可
description: Web クライアント内のアプリのカメラやマイクへのアクセスなど、デバイスのアクセス許可を安全に取り戻す方法について説明します。
localization_priority: medium
ms.topic: how-to
ms.openlocfilehash: ac4695d119b04ee71334ccb2baa820c0e15bff88
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035080"
---
# <a name="device-permissions-for-the-browser"></a>ブラウザーのデバイスのアクセス許可

カメラやマイクへのアクセスなど、デバイスのアクセス許可を必要とする Teams アプリでは、ユーザーが Web ブラウザーでアプリレベルごとに手動でアクセス許可を付与する必要があります。 以前は、ブラウザーがアクセス許可を付与する方法を処理していましたが、これらのアクセス許可は Microsoft Teams で処理されるようになりました。 これは、アプリケーションの設計方法と、ブラウザーでこれらのアクセス許可が必要かどうかに影響します。

## <a name="enable-apps-device-permissions"></a>アプリのデバイスのアクセス許可を有効にする

Teams アプリが [アプリケーション マニフェスト](native-device-permissions.md#specify-permissions)でデバイスのアクセス許可が必要であると宣言している場合、ユーザーがアプリのデバイスのアクセス許可を有効にするための **[アプリのアクセス許可]** オプションが表示されます。 **[アプリのアクセス許可]** オプションは、次の機能で使用できます。

* **個人用アプリとタスク モジュールのダイアログ**: **[アプリのアクセス許可]** オプションは、ページの右上隅にあります。
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

* **チャット、チャネル、または会議のタブ**: **[アプリのアクセス許可]**] オプションは、タブのドロップダウンで使用できます。 ![[アプリのアクセス許可] ドロップダウン](../../assets/images/tabs/drop-downapppermissions.png)

**[アプリのアクセス許可**] オプションを選択すると、ユーザーがアクセス許可ボタンを有効にできるポップアップが表示されます。

これらのアクセス許可を有効にするには、ユーザーがブラウザーでこれらのアクセス許可を有効にする必要があります。 ユーザーがブラウザーでアプリのデバイスのアクセス許可を変更すると、Teams でアプリケーションを再読み込みするように求められます。

> [!IMPORTANT]
> Teams でこれらの **アプリのアクセス許可** を有効にする場所をユーザーに認識させる必要があります。

## <a name="recommendation"></a>推奨事項

ブラウザーでデバイスのアクセス許可を必要とする Teams アプリでは、Teams UI でこれらのアクセス許可を見つけて有効にする場所についてユーザーに指示を表示する必要があります。 アプリケーションが実行されているコンテキストに応じて、これらのアクセス許可にアクセスするための正しい場所をユーザーに指示する手順を確認する必要があります。 アクセス許可は、個人用アプリ、タスク モジュール ダイアログ、チャット内のタブ、チャネルまたは会議では異なります。

</br>
<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | Node.js |
|----------------|-----------------|--------------|
| ブラウザーのタブ デバイスのアクセス許可 | サンプル コードは、ブラウザのデバイス権限を表示する方法を示しています。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

Teams でタブ デバイスのアクセス許可を付与するには、 [ステップ バイ ステップ ガイド](../../sbs-tab-device-permissions.yml) に従います。

## <a name="see-also"></a>関連項目

* [デバイス機能の概要](device-capabilities-overview.md)
* [デバイスのアクセス許可を要求する](native-device-permissions.md)
