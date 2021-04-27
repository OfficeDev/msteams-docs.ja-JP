---
title: Teams を使用したシングル サインオン認証ToolkitタブVisual Studioコード
description: Microsoft Teams を使用して、シングル サインオンと Microsoft Graph 呼び出しをサポートするタブVisual Studioコード内で直接Toolkit
keywords: teams visual studio コード ツールキット タブ sso graph 認証 Azure IDENTITY プラットフォーム
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: daf9a1b0bb64fee9584d0f58d749cf2b1ccaa4ef
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018426"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Teams を使用したシングル サインオン認証ToolkitタブVisual Studioコード

Microsoft Teams Toolkitを使用すると、コード内でタブ アプリのシングル サインオン (SSO) 認証Visual Studioできます。 このツールキットは、このプロセスをガイドし、Azure portal での Microsoft ID プラットフォーム登録のプロビジョニングなど、必要なすべてを提供します。

## <a name="get-started--create-a-project"></a>開始する - プロジェクトを作成する

1. ツールキットで新しいプロジェクトを作成します。
1. 作成する拡張機能の種類としてタブを選択します。
1. SSO をサポートするオプションを選択します。

> [!TIP]
> インストール後、[コード] アクティビティ バーに Teams ToolkitがVisual Studio表示されます。 設定されていない場合は、アクティビティ バー内を右クリックし **、[Microsoft Teams]** を選択してツールキットをピン留めして簡単にアクセスできます。

## <a name="configure-your-project"></a>プロジェクトを構成する

1. Teams 内で SSO を有効にするには、アプリに Azure アプリ登録リソースが必要です。 Teams のToolkit、ユーザーに代わってアプリ登録を準備します。
1. アプリがホストされる URL を入力し、[次へ] を **選択します**。 アプリの登録は、指定された URL を使用して構成されます。
1. アプリ登録の構成の詳細は、プロジェクトのソース コード内 `.env` のファイルに格納されます。

Azure アプリ登録のプロビジョニング方法の詳細については、タブのシングル サインオン[(SSO) の](../tabs/how-to/authentication/auth-aad-sso.md)サポートに関するドキュメントを参照してください。 

> [!TIP]
> この URL を変更するたびに **、Azure App Registrations** に移動して API URI を更新し *、URL* をリダイレクトする必要があります。

## <a name="run-your-project"></a>プロジェクトを実行する

1. フォルダー **から npm install** を `api-server` 選択します。 その **後、npm を開始します**。
1. フォルダー **から npm install** を `.src` 選択します。 その **後、npm を開始します**。
1. [ngrok](https://ngrok.com/)のようなトンネリング サービスを使用している場合は、それを実行し、URL がプロジェクト作成ウィザードで入力した URL と一致する必要があります。 更新されていない場合は、AZURE で作成されたアプリ登録で _API URI_ を更新し _、URL_ をリダイレクトする必要があります。
1. [コード] ウィンドウの左側にあるアクティビティ バー Visual Studio移動します。
1. [実行] **アイコンを** 選択して、[実行] ビュー **と [デバッグ] ビューを表示** します。
1. キーボード ショートカット Ctrl + **Shift +D を使用することもできます**。

> [!TIP]
> ブラウザーでポップアップ ウィンドウが無効になっている場合、ブラウザーにアプリインストールダイアログが表示されない場合があります。 この場合は、ポップアップ ウィンドウを有効にしてページを更新します。

> [!div class="nextstepaction"]
> [詳細: Microsoft Teams のコードとコードを使用ToolkitアプリVisual Studioする](visual-studio-code-overview.md)
