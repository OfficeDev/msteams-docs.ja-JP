---
title: Teams ツールキットとタブ用 Visual Studio Code を使用したシングル サインオン認証
description: シングル サインオンと Microsoft の呼び出しをサポートするタブをビルドし、Graphを使用してVisual Studio Code直接呼び出Microsoft Teams Toolkit
keywords: teams visual studio コード ツールキット タブ sso graph 認証 Azure IDENTITY プラットフォーム
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: c971cd99be0e283050561db2a0f1b89c9e20c9cf
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452544"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Teams ツールキットとタブ用 Visual Studio Code を使用したシングル サインオン認証

> [!IMPORTANT]
> **このドキュメントでは、古いバージョンのバージョンのTeams Toolkit**
>
> 現在の情報については、前提条件を [読み](../get-started/prerequisites.md) 、新しいチュートリアルの 1 に従います。

このMicrosoft Teams Toolkitを使用すると、タブ アプリのシングル サインオン (SSO) 認証を直接、Visual Studio Code。 このツールキットは、プロセスをガイドし、ユーザー登録のプロビジョニングを含む必要Microsoft ID プラットフォームすべてをMicrosoft Azureします。

## <a name="get-started--create-a-project"></a>開始する - プロジェクトを作成する

1. ツールキットで新しいプロジェクトを作成します。
1. 作成する拡張機能の種類としてタブを選択します。
1. SSO をサポートするオプションを選択します。

> [!TIP]
> インストール後、アクティビティ バーのTeams ToolkitにVisual Studio Code表示されます。 表示されていない場合は、アクティビティ バー内を右クリックし、[**Microsoft Teams]を** 選択してツールキットをピン留めして簡単にアクセスできます。

## <a name="configure-your-project"></a>プロジェクトを構成する

1. アプリ内で SSO をTeamsするには、アプリに Azure アプリ登録リソースが必要です。 ユーザー Teams Toolkitにアプリ登録を準備します。
1. アプリをホストする URL を入力し、[次へ] を選択 **します**。 アプリの登録は、指定された URL を使用して構成されます。
1. アプリ登録の構成の詳細は、プロジェクトの `.env` ソース コード内のファイルに格納されます。

Azure アプリ登録のプロビジョニング方法の詳細については、タブのシングル サインオン [(SSO) の](../tabs/how-to/authentication/auth-aad-sso.md)サポートに関するドキュメントを参照してください。

> [!TIP]
> この URL を変更するたびに **、Azure App Registrations** に移動して *API URI* を更新し、URL をリダイレクトする必要があります。

## <a name="run-your-project"></a>プロジェクトを実行する

1. フォルダー **から npm install** を選択 `api-server` します。 その **後、npm を開始します**。
1. フォルダー **から npm install** を選択 `.src` します。 その **後、npm を開始します**。
1. [ngrok](https://ngrok.com/) のようなトンネリング サービスを使用している場合は、それを実行し、URL がプロジェクト作成ウィザードで入力した URL と一致する必要があります。 更新されていない場合は、AZURE で作成されたアプリ登録で *API URI* を更新し *、URL* をリダイレクトする必要があります。
1. ウィンドウの左側にあるアクティビティ バー Visual Studio Codeします。
1. [実行] **アイコンを** 選択して、[実行] ビュー **と [デバッグ] ビューを表示** します。
1. キーボード ショートカット Ctrl + **Shift+D を使用することもできます**。

> [!TIP]
> ブラウザーでポップアップ ウィンドウが無効になっている場合、ブラウザーにアプリインストールダイアログが表示されない場合があります。 この場合は、ポップアップ ウィンドウを有効にしてページを更新します。

## <a name="see-also"></a>関連項目

[Microsoft Teams ツールキットと Visual Studio Code を使用してアプリを構築する](visual-studio-code-overview.md)
