---
title: パブリック サービスのDeveloper Preview
description: Microsoft Teams パブリック サービスの機能のDeveloper Preview
ms.topic: reference
keywords: Teams プレビュー開発者向け機能
ms.openlocfilehash: 3275ef7ac0d4ba052f417f6e852f48e2fdf267f5
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014356"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft Teams のパブリック Developer Preview機能

開発者プレビューには、次の新機能が含まれています。

## <a name="tabs-single-sign-on-sso"></a>タブ のシングル サインオン (SSO)

シングル サインオン [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) を使用して、Web コンテンツ ページから Teams JavaScript SDK を使用して、デスクトップとモバイルでユーザーをログインおよび認証できます。 その利点の 1 つは、ユーザーがサインインする必要がなさらないという利点の 1 つです。プロファイルを使ってアプリに同意すると、タブ (モバイルを含む) に自動的にサインインします。

開発者プレビューは、マニフェスト バージョン 1.5 以上で利用できます。 現在の実装では、Graph API の量は限られていますが、既存の認証 API を使用して追加の Graph API を取得するための回避策を提供しています。

## <a name="calls-and-online-meeting-bots"></a>通話とオンライン会議ボット

通話やオンライン会議用 [の Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta)が追加されたので、Microsoft Teams アプリは音声とビデオを使用して豊富な方法でユーザーと対話できます。 これらの API を使用すると、対話型音声応答 (IVR)、通話制御、通話や、通話や会議のリアルタイムの音声ストリームやビデオ ストリーム (デスクトップやアプリ共有など) へのアクセスなどの新しいアプリ機能を追加できます。

概要から始め、通話とオンライン会議ボットを作成および開発する方法に関する新しいセクションを追加 [しました](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。

## <a name="image-enlarge-support"></a>画像の拡大サポート

ボットは、Teams のアダプティブ カードで共有されている画像を拡大できる画像を示す機能を利用できます。 これは、ユーザーにとって読みにくい詳細な視覚的ガイドをボット経由で共有するなどのシナリオで役立ちます。 イメージを展開可能にする場合は、次のようにフラグ `allowExpand: true` を設定します。

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
これにより、Teams Web/デスクトップ クライアントは、ユーザーがイメージを展開するために、イメージの上にホバーした時点で要素をレンダリングします。

