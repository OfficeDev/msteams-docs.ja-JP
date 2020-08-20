---
title: 公開後にすべきこと
description: アプリの公開後にすべきこと
keywords: Teams、公開後、更新、証明書
ms.openlocfilehash: d2cc6c5427c5b4f7320f0ec2e022f2c69467a33d
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819155"
---
# <a name="maintain-and-support-your-published-app"></a>公開したアプリの保守およびサポート 

After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.

## <a name="microsoft-365-certified"></a>Microsoft 365 認定

[Microsoft 365 アプリ コンプライアンス プログラムは、アプリ](./application-certification.md)のセキュリティとコンプライアンスに対する 3 層のアプローチです。 各層は次の層に基づいて構築されます。レイヤー化されたプログラムは、顧客のニーズに合わせて提供されます。 コンプライアンス ページにアクセスして、Teams アプリのセキュリティとコンプライアンスの状況の詳細を [確認できます](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)。

## <a name="add-a-download-button-to-your-product-site"></a>製品サイトに [ダウンロード] ボタンを追加する

アプリが Microsoft Teams ストアにある場合、Web サイトのリンクを生成できます。このリンクによって、Teams が起動し、ユーザーがアプリを追加する際の同意とインストールのダイアログが表示されます。
形式は `https://teams.microsoft.com/l/app/<appId>` で、appID は、送信されたマニフェストで宣言する GUID です。
たとえば、`https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` は、Trello をインストールするためのリンクになります。

## <a name="updating-your-existing-teams-app"></a>既存の Teams アプリを更新する

* アプリを再送信する際に、*[新しいアプリの追加]* ボタンは使用しないでください。 代わりに、[概要] タブのアプリのタイルを使用します。
* 更新されたマニフェストの appId は、現在のマニフェストと同じであり、バージョンの番号もインクリメントされている必要があります。
* マニフェストのバージョン番号をインクリメントします (マニフェストに変更を加えい、申請に変更を加える場合)。
* 新しいレビューと検証プロセスを行るには、更新された提出が必要です。

## <a name="app-updates-and-the-user-consent-flow"></a>アプリの更新プログラムとユーザー同意フロー

ユーザーがアプリケーションをインストールするとき、まず、アプリがジョブを実行するのに必要なサービスと情報へのアクセス許可をアプリに与えることに同意する必要があります。 ほとんどの場合、アプリの更新の完了後には、新しいバージョンがエンド ユーザーに自動的に表示されます。 ただし、Teams アプリ マニフェストには、ユーザー受け [入れが必要](../../../../resources/schema/manifest-schema.md) になる更新プログラムがいくつかあり、これに対して同意する動作を再びトリガーできることが必要になります。

 >[!div class="checklist"]
>
> * ボットが追加または削除されました。
> * 既存のボットの固有の `botId` 値が変更されたとき。
> * 既存のボットのブー `isNotificationOnly` ル値が変更されました。
> * 既存のボットのブー `supportsFiles` ル値が変更されました。
> * メッセージング拡張機能 ( ) `composeExtensions` が追加または削除されました。
> * 新しいコネクタが追加されました。
> * 新しい静的/個人用タブが追加されました。
> * 新しい構成可能なグループ/チャネル タブが追加されました。
> * 値 `webApplicationInfo` は変更されます。
>
