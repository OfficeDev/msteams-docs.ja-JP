---
title: 公開開発者プレビューの機能
description: Microsoft Teams の公開開発者プレビューの機能について説明します。
keywords: teams のプレビュー開発者向け機能
ms.openlocfilehash: 773e0334bddf45b7b86d31329b99607f3b70c534
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874843"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft Teams の公開開発者プレビューの機能

開発者プレビューには、次の新機能が含まれています。

## <a name="tabs-single-sign-on-sso"></a>タブシングルサインオン (SSO)

[シングルサインオン (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md)を使用して、デスクトップおよびモバイルでユーザーのログインと認証を行うことができます。これには、web コンテンツページから TEAMS JavaScript SDK を使用します。 利点の1つは、ユーザーがサインインする必要がないことです。また、プロファイルを使用してアプリに同意されると、そのタブ (mobile を含む) に自動的にサインインします。

開発者向けプレビューは、1.5 以上のマニフェストバージョンで利用できます。 現在の実装では、限られた量のグラフ Api しか取得できませんが、既存の認証 API を使用して追加の Graph Api を取得するための回避策を提供しています。

## <a name="calls-and-online-meeting-bots"></a>通話とオンライン会議のボット

Microsoft [Graph api を呼び出しとオンライン会議に](/graph/api/resources/communications-api-overview?view=graph-rest-beta)追加することで、microsoft Teams アプリは音声とビデオを使用してさまざまな方法でユーザーと対話できるようになりました。 これらの Api を使用すると、対話式音声応答 (IVR)、通話コントロール、通話と会議のリアルタイムの音声/ビデオストリームへのアクセス、デスクトップやアプリの共有など、新しいアプリ機能を追加できます。

通話とオンライン会議のボットを作成して開発する方法について、 [概要](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)から始まる新しいセクションを追加しました。

## <a name="image-enlarge-support"></a>画像の拡大サポート

Teams のアダプティブカードで共有されている画像を拡大することができます。 これは、ユーザーにとって特に難しい bot から、詳細なステップごとのビジュアルガイドを共有する場合などに便利です。 画像を展開可能にするには、次のようにフラグを設定し `allowExpand: true` ます。

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
これにより、Teams の web/デスクトップクライアントは、画像をポイントしたときに、イメージを拡張するための要素を表示することができます。

