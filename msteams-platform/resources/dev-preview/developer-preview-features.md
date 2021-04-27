---
title: パブリック サービスのDeveloper Preview
description: Details the features in the Microsoft Teams Public Developer Preview
ms.topic: reference
localization_priority: Normal
keywords: teams プレビュー開発者向け機能
ms.openlocfilehash: 38acccedacb86437f5e6c949b674c0a62bbbd63c
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020619"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft Teams のパブリック Developer Preview機能

開発者プレビューには、次の新機能が含まれています。

## <a name="app-customization"></a>アプリのカスタマイズ

Teams 管理者が組織のニーズに基づいてカスタマイズまたは再ブランド化できるプロパティの選択セットを定義できます。 詳細については、「アプリのカスタマイズ [機能」を参照してください](~/concepts/design/design-teams-app-overview.md)。

## <a name="tabs-single-sign-on-sso"></a>タブのシングル サインオン (SSO)

Web コンテンツ ページから Teams JavaScript SDK を使用して、シングル サインオン [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) を使用してデスクトップとモバイルでユーザーにログインして認証できます。 利点の 1 つは、ユーザーがサインインする必要がなさったことです。プロファイルを使用してアプリに同意すると、自動的にタブ (モバイルを含む) にサインインします。

開発者向けプレビューは、マニフェスト バージョン 1.5 以上で利用できます。 現在の実装では、グラフ API の量は限られていますが、既存の認証 API を使用して追加の Graph API を取得するための回避策を提供しています。

## <a name="calls-and-online-meeting-bots"></a>通話とオンライン会議ボット

通話やオンライン会議に [Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)が追加されたので、Microsoft Teams アプリは音声とビデオを使用してユーザーと豊富なやり取りを行うことができます。 これらの API を使用すると、対話型音声応答 (IVR)、通話制御、デスクトップやアプリ共有などの通話や会議のリアルタイムオーディオストリームやビデオ ストリームへのアクセスなどの新しいアプリ機能を追加できます。

概要から始まる通話とオンライン会議ボットを作成および開発する方法に関する新しいセクションが追加 [されました](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。


## <a name="image-enlarge-support"></a>画像の拡大サポート

ボットは、Teams のアダプティブ カードで共有されているイメージを拡大して表示できます。 これは、ボットを介して詳細な詳細な視覚的ガイドを共有するなどのシナリオで役立ちます。それ以外の場合はユーザーにとって読みにくい場合があります。 イメージを展開可能にするには、次のようにフラグ `allowExpand: true` を設定します。

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
これにより、Teams の Web/デスクトップ クライアントは、イメージにカーソルを合わせると要素がレンダリングされ、ユーザーがイメージを展開できます。

