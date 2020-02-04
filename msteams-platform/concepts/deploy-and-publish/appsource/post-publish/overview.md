---
title: 投稿の公開
description: アプリを発行した後の作業
keywords: teams 投稿の発行更新証明書
ms.openlocfilehash: 05e4ea47bbf81967ccf086230bf0ad8c633f6e0b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674719"
---
# <a name="maintain-and-support-your-published-app"></a>公開したアプリを保守およびサポートする 

アプリが承認され、パブリックアプリカタログに表示された後は、アプリの証明書を取得するか、web サイトの [ダウンロード] ボタンを追加することによって、ユーザーのリーチを増やすことができます。

## <a name="application-certificate"></a>アプリケーション証明書

Microsoft は、アプリ情報をコンパイルして[Microsoft Teams アプリのセキュリティとコンプライアンスのページ](https://aka.ms/AppCertification)に表示する[アプリケーション認定プログラム](./application-certification.md)を提供しています。 この情報は、管理者が組織にとって安全なアプリを選択できるようにすることを目的としています。

## <a name="add-a-download-button-to-your-product-site"></a>製品サイトにダウンロードボタンを追加する

アプリが Microsoft Teams ストアにある場合は、Teams を起動する web サイトへのリンクを生成し、ユーザーがアプリを追加するための同意とインストールダイアログを表示することができます。
形式は次の`https://teams.microsoft.com/l/app/<appId>`とおりです。 appID は、送信されたマニフェストで宣言する GUID です。
例: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd`は、Trello をインストールするためのリンクです。

## <a name="updating-your-existing-teams-app"></a>既存の Teams アプリを更新する

* アプリを再送信するには、[*新しいアプリの追加*] ボタンを使用しないでください。 代わりに、[概要] タブでアプリのタイルを使用します。
* 更新されたマニフェスト内の appId は、現在のマニフェストと同じであり、バージョン番号が増やされている必要があります。
* マニフェストでバージョン番号をインクリメントします。

### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a>アプリの更新によってユーザーの同意フローがトリガーされるのはいつですか?

ユーザーがアプリケーションをインストールするときに、最初に行うことは、アプリがジョブを実行するために必要なサービスと情報にアクセスするためのアクセス許可を付与するための同意です。 アプリを更新すると、特に以下の1つ以上の変更を行った場合に、この同意の動作を再始動することができます。

* アプリケーションに新しい機能を追加する。たとえば、タブのみのアプリに bot を追加することができます。
* マニフェスト内のアクセス許可の配列を変更します。
* マニフェストでアプリのバージョン番号をインクリメントします。
