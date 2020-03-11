---
title: 公開後にすべきこと
description: アプリの公開後にすべきこと
keywords: Teams、公開後、更新、証明書
ms.openlocfilehash: 54d0615c262e45729a36f556c3eda3b810d2a097
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "42582861"
---
# <a name="maintain-and-support-your-published-app"></a>公開したアプリの保守およびサポート 

アプリが承認され、公開アプリ カタログに一覧表示されたら、アプリの認定を取得するか、Web サイトに [ダウンロード] ボタンを追加して、利用対象者を増やすことができます。

## <a name="application-certificate"></a>アプリケーション証明書

Microsoft では、[アプリケーション証明書プログラム](./application-certification.md)を用意しています。アプリ情報を編集するプログラムで、[Microsoft Teams アプリのセキュリティとコンプライアンスのページ](https://aka.ms/AppCertification)で提供されます。 この情報は、管理者が組織にとって安全なアプリを選択できるようにすることを目的としています。

## <a name="add-a-download-button-to-your-product-site"></a>製品サイトに [ダウンロード] ボタンを追加する

アプリが Microsoft Teams ストアにある場合、Web サイトのリンクを生成できます。このリンクによって、Teams が起動し、ユーザーがアプリを追加する際の同意とインストールのダイアログが表示されます。
形式は `https://teams.microsoft.com/l/app/<appId>` で、appID は、送信されたマニフェストで宣言する GUID です。
たとえば、`https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` は、Trello をインストールするためのリンクになります。

## <a name="updating-your-existing-teams-app"></a>既存の Teams アプリを更新する

* アプリを再送信する際に、*[新しいアプリの追加]* ボタンは使用しないでください。 代わりに、[概要] タブのアプリのタイルを使用します。
* 更新されたマニフェストの appId は、現在のマニフェストと同じであり、バージョンの番号もインクリメントされている必要があります。
* 送信に対してマニフェストに変更を加える場合は、マニフェストでバージョン番号をインクリメントします。
* 新しいレビューおよび検証プロセスを実行するには、更新された提出を行う必要があります。


### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a>アプリ更新の際にユーザーの同意フローがトリガーされる場合

ユーザーがアプリケーションをインストールするとき、まず、アプリがジョブを実行するのに必要なサービスと情報へのアクセス許可をアプリに与えることに同意する必要があります。 アプリを更新し、以下の変更を 1 つまたは複数行った場合、この同意の動作が再びトリガーされます。

* タブのみのアプリへのボットの追加など、アプリに新しい機能を追加する。
* マニフェストでアクセス許可の配列を変更する。
* マニフェスト内のアプリのバージョン番号を増やします。
