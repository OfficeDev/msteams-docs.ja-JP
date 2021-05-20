---
title: Teams ToolkitとタブのVisual Studio Codeを使用したシングル サインオン認証
description: シングル サインオンと Microsoft Graph 呼び出しをサポートするタブを、Visual Studio Code内で直接Microsoft Teams Toolkit
keywords: チーム ビジュアル スタジオ コード ツールキット タブ sso グラフ認証 Azure ID プラットフォーム
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 11e642ce335dae4344f1c730b73763e9172fd76c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566832"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Teams ToolkitとタブのVisual Studio Codeを使用したシングル サインオン認証

Microsoft Teams Toolkitを使用すると、Visual Studio Code内で直接タブ アプリのシングル サインオン (SSO) 認証を作成できます。 ツールキットは、プロセスをガイドし、Azure ポータルでのMicrosoft ID プラットフォーム登録のプロビジョニングを含む必要なすべてを提供します。

## <a name="get-started--create-a-project"></a>はじめに - プロジェクトを作成する

1. ツールキットで新しいプロジェクトを作成します。
1. 作成する拡張機能の種類としてタブを選択します。
1. SSO をサポートするオプションを選択します。

> [!TIP]
> インストール後、Visual Studio CodeアクティビティバーにTeams Toolkitが表示されます。 アクセスできない場合は、アクティビティバー内を右クリックし **、Microsoft Teams** 選択してツールキットをピン留めして簡単にアクセスできます。

## <a name="configure-your-project"></a>プロジェクトを構成する

1. Teams内で SSO を有効にするには、アプリに Azure アプリ登録リソースが必要です。 Teams Toolkitは、ユーザーに代わってアプリ登録をプロビジョニングします。
1. アプリをホストする URL を入力し、[ **次へ**] を選択します。 アプリの登録は、指定された URL を使用して構成されます。
1. アプリの登録の詳細は、 `.env` プロジェクトのソース コード内のファイルに格納されます。

Azure アプリの登録がどのようにプロビジョニングされるかの詳細については、[タブのシングル サインオン (SSO) サポートを](../tabs/how-to/authentication/auth-aad-sso.md)_参照_ してください。

> [!TIP]
> この URL を変更するたびに **、Azure アプリの登録** に移動し *、API URI* を更新して *URL をリダイレクト* する必要があります。

## <a name="run-your-project"></a>プロジェクトを実行する

1. フォルダから **npm インストール** を選択 `api-server` します。 それから **npmは始まります**。
1. フォルダから **npm インストール** を選択 `.src` します。 それから **npmは始まります**。
1. [ngrok](https://ngrok.com/)のようなトンネリング サービスを使用している場合は、それを実行し、URL がプロジェクト作成ウィザードで入力した URL と一致することを確認します。 そうでない場合は _、API URI_ を更新し、Azure で作成されたアプリ登録で _URL をリダイレクト_ する必要があります。
1. Visual Studio Code ウィンドウの左側にあるアクティビティ バーに移動します。
1. [ **実行** ] アイコンを選択して、[ **実行] ビューと [デバッグ** ] ビューを表示します。
1. キーボード ショートカット Ctrl キーを押 **しながら Shift キーを押しながら D** キーを押すこともできます。

> [!TIP]
> ブラウザーでポップアップ ウィンドウが無効になっている場合、ブラウザーでアプリのインストール ダイアログが表示されないことがあります。 この場合は、ポップアップ ウィンドウを有効にしてページを更新します。

## <a name="see-also"></a>関連項目

- [Microsoft Teams ToolkitとVisual Studio Codeを使用してアプリを構築する](visual-studio-code-overview.md)
