---
title: 発行済みアプリの保守とサポート
description: アプリの公開後にすべきこと
ms.topic: how-to
keywords: teams post publish update certification app update manifest
ms.openlocfilehash: 8644db5e329e15d77062553eda4a41a36b2740ee
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585835"
---
# <a name="maintain-and-support-your-published-app"></a>公開したアプリの保守およびサポート 

アプリが承認され、パブリック アプリ カタログに表示された後は、Microsoft 365 アプリ コンプライアンス プログラムを完了するか、Web サイトにダウンロード ボタンを追加することで、リーチを拡大できます。

## <a name="microsoft-365-certified"></a>Microsoft 365 認定

[Microsoft 365 アプリ コンプライアンス プログラムは](./application-certification.md)、アプリのセキュリティとコンプライアンスに対する 3 層のアプローチです。 各層は、顧客のニーズに合わせて階層化されたプログラムを提供します。 Teams アプリのセキュリティとコンプライアンスの姿勢の詳細については、コンプライアンス ページを [参照してください](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)。

## <a name="add-a-download-button-to-your-product-site"></a>製品サイトに [ダウンロード] ボタンを追加する

アプリが Microsoft Teams グローバル ストアにある場合は、Teams を起動し、ユーザーがアプリを追加する同意とインストール ダイアログを表示する Web サイトのリンクを生成できます。
形式は `https://teams.microsoft.com/l/app/<appId>` で、appID は、送信されたマニフェストで宣言する GUID です。
たとえば、`https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` は、Trello をインストールするためのリンクになります。

## <a name="updating-your-existing-teams-app"></a>既存の Teams アプリを更新する

* アプリを再送信する際に、*[新しいアプリの追加]* ボタンは使用しないでください。 代わりに、[概要] タブのアプリのタイルを使用します。
* 更新されたマニフェストの appId は、現在のマニフェストと同じであり、バージョンの番号もインクリメントされている必要があります。
* アプリ名やマニフェスト内のメタデータなど、申請に変更を加えた場合は、マニフェストのバージョン番号を増やします。
* 新しいレビューと検証プロセスを受けるには、更新された申請が必要です。

## <a name="app-updates-and-the-user-consent-flow"></a>アプリの更新とユーザーの同意フロー

ユーザーがアプリケーションをインストールするとき、まず、アプリがジョブを実行するのに必要なサービスと情報へのアクセス許可をアプリに与えることに同意する必要があります。 ほとんどの場合、アプリの更新を完了すると、新しいバージョンがエンド ユーザーに自動的に表示されます。 ただし、Teams アプリ マニフェストには[](../../../../resources/schema/manifest-schema.md)、完了するためにユーザーの受け入れを必要とする更新プログラムがいくつか含まれています。この同意動作を再トリガーできます。

 >[!div class="checklist"]
>
> * ボットが追加または削除されます。
> * 既存のボットの一意の `botId` 値が変更されます。
> * 既存のボットのブール値 `isNotificationOnly` が変更されます。
> * 既存のボットまたはブール値 `supportsFiles` `supportsCalling` が変更されます。
> * メッセージング拡張機能が `composeExtensions` 追加または削除されます。
> * 新しいコネクタが追加されます。
> * 新しい静的タブまたは個人用タブが追加されます。
> * 新しい構成可能なグループまたはチャネル タブが追加されます。
> * 内部のプロパティ `webApplicationInfo` が変更されます。 に対する変更 `webApplicationInfo` については、Teams スコープでのみ同意が必要です。

### <a name="images-of-user-consent-flow"></a>ユーザーの同意フローのイメージ:

**コネクタを設定する** - この画面は Teams ユーザーにのみ表示されます。

![同意フローのセットアップ コネクタ図](../../../../assets/images/connector-teams-consentflow.png)

**ユーザーの同意フロー** - この画面は、個人スコープとグループ スコープの両方で一般的です。 ここでは、[組織の代理 **として同意する** ] チェック ボックスをオンにして、[同意する] を **選択します**。

![アクセス許可の図](../../../../assets/images/user-consent-flow.png)
