---
title: Teams ツールキットとタブ用 Visual Studio Code を使用したシングル サインオン認証
description: シングル サインオンをサポートするタブを作成し、Microsoft GraphがMicrosoft Teams Toolkitを使用して Visual Studio Code 内で直接呼び出します。
keywords: teams Visual Studio Code Toolkit タブ sso graph authentication Azure ID プラットフォーム
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 7cca78c2ca3669d647dd76dd71e0a2b999b09dd1
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123872"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Teams ツールキットとタブ用 Visual Studio Code を使用したシングル サインオン認証

> [!IMPORTANT]
> **このドキュメントでは、古いバージョンのTeams Toolkit**
>
> 現在の情報については、 [前提条件](../get-started/prerequisites.md) を確認し、新しいチュートリアルの 1 つに従ってください。

Microsoft Teams Toolkitを使用すると、Visual Studio Code 内でタブ アプリのシングル サインオン (SSO) 認証を直接作成できます。 このツールキットでは、プロセスをガイドし、Microsoft Azure ポータルでのMicrosoft ID プラットフォーム登録のプロビジョニングなど、必要なすべての情報を提供します。

## <a name="get-started--create-a-project"></a>概要 — プロジェクトを作成する

1. ツールキットで新しいプロジェクトを作成します。
1. 作成する拡張機能の種類としてタブを選択します。
1. SSO をサポートするオプションを選択します。

> [!TIP]
> インストール後、Visual Studio Code アクティビティ バーにTeams Toolkitが表示されます。 そうでない場合は、アクティビティ バー内を右クリックし **、Microsoft Teams** を選択してツールキットをピン留めし、簡単にアクセスできるようにします。

## <a name="configure-your-project"></a>プロジェクトを構成する

1. Teams内で SSO を有効にするには、アプリに Azure アプリ登録リソースが必要です。 Teams Toolkitは、ユーザーに代わってアプリの登録をプロビジョニングします。
1. アプリがホストされる URL を入力し、 **次を** 選択します。 アプリの登録は、指定された URL を使用して構成されます。
1. アプリ登録の構成の詳細は、プロジェクトの `.env` ソース コード内のファイルに格納されます。

Azure アプリ登録のプロビジョニング方法の詳細については、タブのドキュメントに [関するシングル サインオン (SSO) のサポートを](../tabs/how-to/authentication/tab-sso-overview.md)*参照* してください。

> [!TIP]
> **Azure アプリ登録** に移動し、*API URI* を更新し、この URL を変更するたびに *URL をリダイレクトする* 必要があります。

## <a name="run-your-project"></a>プロジェクトを実行する

1. フォルダーから **npmインストール** を`api-server`選択します。 次 **npm開始します**。
1. フォルダーから **npmインストール** を`.src`選択します。 次 **npm開始します**。
1. [ngrok](https://ngrok.com/) などのトンネリング サービスを使用している場合は、それを実行し、URL がプロジェクト作成ウィザードで入力したものと一致することを確認します。 そうでない場合は、 *API URI* を更新し、Azure で作成されたアプリ登録で *URL をリダイレクト* する必要があります。
1. [Visual Studio コード] ウィンドウの左側にあるアクティビティ バーに移動します。
1. **[実行**] アイコンを選択して、[**実行とデバッグ] ビューを** 表示します。
1. キーボード ショートカット **Ctrl + Shift + D** を使用することもできます。

> [!TIP]
> ブラウザーでポップアップ ウィンドウが無効になっている場合、ブラウザーにアプリのインストールダイアログが表示されない場合があります。 このような場合は、ポップアップ ウィンドウを有効にし、ページを更新します。

## <a name="see-also"></a>関連項目

[Microsoft Teams ツールキットと Visual Studio Code を使用してアプリを構築する](visual-studio-code-overview.md)
