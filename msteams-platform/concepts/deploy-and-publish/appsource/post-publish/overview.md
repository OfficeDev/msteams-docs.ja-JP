---
title: 公開されたアプリの保守とサポート
description: アプリの公開後にすべきこと
ms.topic: how-to
keywords: teams post publish update certification app update manifest
ms.openlocfilehash: ce63b840307f7e12a5cd05a1c67aed017cf6199b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014328"
---
# <a name="maintain-and-support-your-published-app"></a>公開したアプリの保守およびサポート 

アプリが承認され、公開アプリ カタログに一覧表示された後は、Microsoft 365 アプリ コンプライアンス プログラムを完了するか、Web サイトにダウンロード ボタンを追加することで、リーチを拡大できます。

## <a name="microsoft-365-certified"></a>Microsoft 365 認定

[Microsoft 365 アプリ コンプライアンス](./application-certification.md)プログラムは、アプリのセキュリティとコンプライアンスに対する 3 層のアプローチです。 各層は次の階層に構築されます。お客様のニーズに合わせて階層化されたプログラムを提供します。 Teams アプリのセキュリティとコンプライアンスの体制の詳細については、コンプライアンス ページを [参照してください](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)。

## <a name="add-a-download-button-to-your-product-site"></a>製品サイトに [ダウンロード] ボタンを追加する

アプリが Microsoft Teams グローバル ストアにある場合は、Teams を起動し、ユーザーがアプリを追加する同意とインストールダイアログを表示する Web サイトのリンクを生成できます。
形式は `https://teams.microsoft.com/l/app/<appId>` で、appID は、送信されたマニフェストで宣言する GUID です。
たとえば、`https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` は、Trello をインストールするためのリンクになります。

## <a name="updating-your-existing-teams-app"></a>既存の Teams アプリを更新する

* アプリを再送信する際に、*[新しいアプリの追加]* ボタンは使用しないでください。 代わりに、[概要] タブのアプリのタイルを使用します。
* 更新されたマニフェストの appId は、現在のマニフェストと同じであり、バージョンの番号もインクリメントされている必要があります。
* アプリ名やマニフェスト内のメタデータなど、申請に変更を加えた場合は、マニフェストでバージョン番号を増やします。
* 更新された提出は、新しいレビューと検証プロセスを受ける必要があります。

## <a name="app-updates-and-the-user-consent-flow"></a>アプリの更新とユーザーの同意フロー

ユーザーがアプリケーションをインストールするとき、まず、アプリがジョブを実行するのに必要なサービスと情報へのアクセス許可をアプリに与えることに同意する必要があります。 ほとんどの場合、アプリの更新が完了すると、エンド ユーザーに新しいバージョンが自動的に表示されます。 ただし [、Teams](../../../../resources/schema/manifest-schema.md) アプリ マニフェストには、完了するためにユーザー承認が必要で、この同意動作を再トリガーできる更新プログラムがいくつか含まれています。

 >[!div class="checklist"]
>
> * ボットが追加または削除されました。
> * 既存のボットの一意の値 `botId` が変更されました。
> * 既存のボットのブール値 `isNotificationOnly` が変更されました。
> * 既存のボットのブール値 `supportsFiles` が変更されました。
> * メッセージング拡張機能 ( `composeExtensions` ) が追加または削除されました。
> * 新しいコネクタが追加されました。
> * 新しい静的/個人用タブが追加されました。
> * 新しい構成可能なグループ/チャネル タブが追加されました。
> * 値 `webApplicationInfo` が変更されました。
>

### <a name="images-of-user-consent-flow"></a>ユーザーの同意フローの画像:

**コネクタのセットアップ** - この画面は Teams ユーザーにのみ表示されます。

![同意フローのセットアップコネクタ図](../../../../assets/images/connector-teams-consentflow.png)

**ユーザーの同意フロー** - この画面は、個人用スコープとグループ スコープの両方で一般的です。 ここで、組織の代 **わりに [同意** ] チェック ボックスをオンにし、[承諾] を **選択します**。

![アクセス許可の図](../../../../assets/images/user-consent-flow.png)
