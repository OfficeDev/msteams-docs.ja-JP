---
title: Teams ツールキットを使用したシングルサインオン認証と、タブ用 Visual Studio コード
description: Microsoft Teams Toolkit を使用して、Visual Studio Code 内でシングルサインオンと Microsoft Graph の呼び出しを直接サポートするタブを構築する
keywords: teams visual studio code toolkit タブ sso graph authentication Azure identity platform
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: fe734143975688cd35c510cd68cd0779a2200a18
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "49477737"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Teams ツールキットを使用したシングルサインオン認証と、タブ用 Visual Studio コード

Microsoft Teams ツールキットを使用すると、tab アプリのシングルサインオン (SSO) 認証を Visual Studio Code 内で直接作成できます。 このツールキットではプロセスを順を追って説明しており、Azure portal で Microsoft identity platform の登録をプロビジョニングするなど、必要な情報をすべて提供しています。

## <a name="get-started--create-a-project"></a>作業の開始-プロジェクトを作成する

1. ツールキットに新しいプロジェクトを作成します。
1. 作成する拡張機能の種類として [タブ] を選択します。
1. SSO をサポートするオプションを選択します。

> [!TIP]
> インストール後に、Visual Studio Code アクティビティバーに Teams ツールキットが表示されます。 表示されていない場合は、アクティビティバー内を右クリックし、[ **Microsoft Teams** ] を選択して、簡単にアクセスできるようにツールキットを固定します。

## <a name="configure-your-project"></a>プロジェクトを構成する

1. Teams 内で SSO を有効にするには、アプリに Azure アプリ登録リソースが含まれている必要があります。 Teams ツールキットは、ユーザーの代わりにアプリの登録をプロビジョニングします。
1. アプリがホストされる URL を入力し、[ **次へ**] を選択します。 アプリの登録は、指定した URL を使用して構成されます。
1. アプリ登録の構成の詳細は、 `.env` プロジェクトのソースコード内のファイルに格納されます。

Azure アプリの登録方法の詳細については、「[シングルサインオン (SSO) に関するタブのサポート」の](../tabs/how-to/authentication/auth-aad-sso.md)ドキュメントを _参照_ してください。

> [!TIP]
> この URL を変更する場合は、 **Azure アプリの登録** に移動して、 *API URI* と *リダイレクト url* を更新する必要があります。

## <a name="run-your-project"></a>プロジェクトを実行する

1. フォルダーから [ **npm install** ] を選択し `api-server` ます。 その後、 **npm を開始** します。
1. フォルダーから [ **npm install** ] を選択し `.src` ます。 その後、 **npm を開始** します。
1. [Ngrok](https://ngrok.com/)のようなトンネリングサービスを使用している場合は、それを実行して、プロジェクト作成ウィザードで入力した URL と一致することを確認してください。 そうでない場合は、Azure で作成されたアプリ登録で _API URI_ と _リダイレクト URL_ を更新する必要があります。
1. Visual Studio の [コード] ウィンドウの左側にあるアクティビティバーに移動します。
1. [実行 **] アイコンを** 選択して、[ **実行] および [デバッグ** ] ビューを表示します。
1. キーボードショートカット **ctrl + Shift + D** を使用することもできます。

> [!TIP]
> ブラウザーでポップアップウィンドウが無効になっている場合、ブラウザーにアプリのインストールダイアログが表示されないことがあります。 この問題が発生した場合は、ポップアップウィンドウを有効にしてページを更新します。

> [!div class="nextstepaction"]
> [詳細情報: Microsoft Teams Toolkit と Visual Studio Code を使用してアプリをビルドする](visual-studio-code-overview.md)
