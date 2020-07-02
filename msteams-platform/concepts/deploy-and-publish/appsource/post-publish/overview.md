---
title: 公開後にすべきこと
description: アプリの公開後にすべきこと
keywords: Teams、公開後、更新、証明書
ms.openlocfilehash: 887e18ac7e27cf12aa4319ac240e42f21f05fd75
ms.sourcegitcommit: e355f59d2d21a2d5ae36cc46acad5ed4765b42e0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "45021574"
---
# <a name="maintain-and-support-your-published-app"></a>公開したアプリの保守およびサポート 

アプリが承認され、パブリックアプリカタログに表示された後で、Microsoft 365 App コンプライアンスプログラムを完了するか、web サイトに [ダウンロード] ボタンを追加することによって、リーチを拡大できます。

## <a name="m365-certified"></a>M365 認定

[Microsoft 365 App コンプライアンスプログラム](./application-certification.md)は、アプリのセキュリティとコンプライアンスに関する3つの階層手法です。 各層は次のように構築されており、ユーザーのニーズを満たす階層化プログラムを提供します。 Teams アプリのセキュリティとコンプライアンスの姿勢の詳細については、「[コンプライアンス」ページ](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)を参照してください。

## <a name="add-a-download-button-to-your-product-site"></a>製品サイトに [ダウンロード] ボタンを追加する

アプリが Microsoft Teams ストアにある場合、Web サイトのリンクを生成できます。このリンクによって、Teams が起動し、ユーザーがアプリを追加する際の同意とインストールのダイアログが表示されます。
形式は `https://teams.microsoft.com/l/app/<appId>` で、appID は、送信されたマニフェストで宣言する GUID です。
たとえば、`https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` は、Trello をインストールするためのリンクになります。

## <a name="updating-your-existing-teams-app"></a>既存の Teams アプリを更新する

* アプリを再送信する際に、*[新しいアプリの追加]* ボタンは使用しないでください。 代わりに、[概要] タブのアプリのタイルを使用します。
* 更新されたマニフェストの appId は、現在のマニフェストと同じであり、バージョンの番号もインクリメントされている必要があります。
* 送信に対してマニフェストに変更を加える場合は、マニフェストでバージョン番号をインクリメントします。
* 新しいレビューおよび検証プロセスを実行するには、更新された提出を行う必要があります。

## <a name="app-updates-and-the-user-consent-flow"></a>アプリの更新とユーザーの同意フロー

ユーザーがアプリケーションをインストールするとき、まず、アプリがジョブを実行するのに必要なサービスと情報へのアクセス許可をアプリに与えることに同意する必要があります。 ほとんどの場合、アプリの更新が完了すると、新しいバージョンがエンドユーザーに対して自動的に表示されます。 ただし、 [Teams アプリのマニフェスト](../../../../resources/schema/manifest-schema.md)には、ユーザーの承認を完了し、この同意の動作を再始動する必要がある、いくつかの更新があります。

 >[!div class="checklist"]
>
> * Bot が追加または削除されました。
> * 既存の bot の一意の `botId` 値が変更されました。
> * 既存の bot の `isNotificationOnly` ブール値が変更されました。
> * 既存の bot の `supportsFiles` ブール値が変更されました。
> * メッセージング拡張機能 ( `composeExtensions` ) が追加または削除されました。
> * 新しいコネクタが追加されました。
> * 新しい静的/個人用タブが追加されました。
> * 新しい [構成可能なグループ/チャネル] タブが追加されました。
> * `webApplicationInfo`値が変更されました。
>
