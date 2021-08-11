---
title: パブリック サービスのDeveloper Preview
description: '[パブリック] ページの機能Microsoft Teams詳細Developer Preview'
ms.topic: reference
localization_priority: Normal
keywords: teams プレビュー開発者向け機能
ms.openlocfilehash: f24f95245707097cb5fc79c041582efb5e1f11ef29877855003baf3707842c4c
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57704397"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>パブリック サービスの機能Developer Preview Microsoft Teams

> [!NOTE]
> このページは 2021 年 6 月に廃止される予定です。 開発者プレビューで利用できる機能の詳細については、「 [新機能」を参照してください。](~/whats-new.md)

開発者プレビューには、次の新機能が含まれています。

## <a name="app-customization"></a>アプリのカスタマイズ

これで、組織のニーズに基づいて、Teamsをカスタマイズまたは再ブランド化できるプロパティの選択セットを定義できます。 詳細については、「アプリのカスタマイズ [機能」を参照してください](~/concepts/design/design-teams-app-overview.md)。

## <a name="tabs-single-sign-on-sso"></a>タブのシングル サインオン (SSO)

シングル サインオン[(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md)を使用して、Web コンテンツ ページから javaScript SDK の Teamsを使用してデスクトップとモバイルでユーザーにログインして認証できます。 利点の 1 つは、ユーザーがサインインする必要がなさったことです。プロファイルを使用してアプリに同意すると、自動的にタブ (モバイルを含む) にサインインします。

開発者向けプレビューは、マニフェスト バージョン 1.5 以上で利用できます。 現在の実装では、限られた量の API のみを取得Graph、既存の認証 API を使用して追加の API を取得Graph回避策を提供します。

## <a name="calls-and-online-meeting-bots"></a>通話とオンライン会議ボット

通話やオンライン会議用[の Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)が追加されたので、Microsoft Teams アプリは音声とビデオを使用して豊富な方法でユーザーとやり取りできます。 これらの API を使用すると、対話型音声応答 (IVR)、通話制御、デスクトップやアプリ共有などの通話や会議のリアルタイムオーディオストリームやビデオ ストリームへのアクセスなどの新しいアプリ機能を追加できます。

概要から始まる通話とオンライン会議ボットを作成および開発する方法に関する新しいセクションが追加 [されました](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。


## <a name="image-enlarge-support"></a>画像の拡大サポート

ボットは、アダプティブ カード内で共有されているイメージを拡大Teams可能です。 これは、ボットを介して詳細な詳細な視覚的ガイドを共有するなどのシナリオで役立ちます。それ以外の場合はユーザーにとって読みにくい場合があります。 イメージを展開可能にするには、次のようにフラグ `allowExpand: true` を設定します。

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
これにより、web/Teamsクライアントがイメージにカーソルを合わせると、ユーザーがイメージを展開できます。
