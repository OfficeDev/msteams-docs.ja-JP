---
title: バックグランド プロセスのデバッグ
author: zyxiaoyuer
description: ローカル デバッグ中の Visual Studio Code と Teams Toolkit の機能
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 74aa3ef53aab329b0b2acae34dc976c142703e0e
ms.sourcegitcommit: 5e5d2d3fb621bcbd9d792a5b450f95167ec8548b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2022
ms.locfileid: "63731891"
---
# <a name="debug-background-process"></a>バックグランド プロセスのデバッグ

ローカル デバッグ ワークフローには、`.vscode/launch.json` と `.vscode/tasks.json` ファイルを使って Visual Studio Code でデバッガーを構成します。その後、Visual Studio Code はデバッガーを起動し、Microsoft Edge または Chrome デバッガーは次のように新しいブラウザー インスタンスを起動します:

1. `launch.json` ファイルは、Visual Studio Code でデバッガーを構成します。 

2. Visual Studio Code は、`.vscode/tasks.json` ファイルで複合 `preLaunchTask`、`Pre Debug Check & Start All` を実行します。

3. その後、Visual Studio Code は、**ボットにアタッチ**、**バックエンドにアタッチ**、**フロントエンドにアタッチ**、**ボットの起動** など、複雑な構成で指定されたデバッガーを立ち上げます。

4.  Microsoft Edge または Chrome デバッガーは、新しいブラウザー インスタンスを起動し、Teams クライアントを読み込む Web ページを開きます。

## <a name="prerequisites"></a>前提条件

Teams Toolkit は、デバッグ プロセス中に次の前提条件を確認します:

* Node.js。次のプロジェクトの種類に適用されます:

  |プロジェクトの種類|Node.js LTS バージョン|
  |----------|--------------------------------|
  |Azure Functions のないタブ | 10、12、 **14 (推奨)**、16 |
  |Azure Functions のあるタブ | 10、12、 **14 (推奨)**|
  |Bot |  10、12、 **14 (推奨)**、16|
  |メッセージング拡張機能 | 10、12、 **14 (推奨)**、16 |

   
* 有効な資格情報を持つ Microsoft 365 アカウント、サインインしていない場合は、Microsoft 365 アカウントにサインインするように Teams ツールキットから求められます。

* 開発者テナントのカスタム アプリのアップロードまたはサイドローディングが有効になります。 そうでない場合、ローカル デバッグは終了します。

* Ngrok バイナリ バージョン 2.3。ボットとメッセージング拡張機能に適用されます。  Ngrok がインストールされていないか、バージョンが要件に一致しない場合、Teams ツールキットは ngrok NPM パッケージ `ngrok@4.2.2` を `~/.fx/bin/ngrok` にインストールします。 Ngrok バイナリは、`/.fx/bin/ngrok/node modules/ngrok/bin` の Ngrok NPM パッケージによって管理されます。

* Azure Functions Core Tools バージョン 3。 Azure Functions Core Toolsがインストールされていない場合、またはバージョンが要件と一致しない場合、Teams ツールキットは、**Windows** および **macOs** 用に Azure Functions Core Tools NPM パッケージ、azure-functions-core-tools@3 を  `~/.fx/bin/func` にインストールされます。 `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` のAzure Functions Core Tools NPM パッケージは、バイナリAzure Functions Core Tools管理します。 Linux の場合、ローカル デバッグは終了します。

* .NET Core SDK バージョン。Azure Functions に適用されます。 .NET Core SDK がインストールされていない場合、またはバージョンが要件と一致しない場合、Teams Toolkit は Windows と MacOS 用の.NET Core SDKを `~/.fx/bin/dotnet` にインストールします。 Linux の場合、ローカル デバッグは終了します。

  次の表に、.NET Core のバージョンを示します:

  | プラットフォーム  | ソフトウェア|
  | --- | --- |
  |Windows、macOs (x64)、Linux | **3.1 (推奨)**、5.0、6.0 |
  |macOs (arm64) |6.0 |

* 開発証明書。Windows または macOS のタブに localhost の開発証明書がインストールされていない場合、Teams ツールキットによってインストールが求められます。

* `api/extensions.csproj` で定義されている Azure Functions バインド拡張機能。 Azure Functions バインド拡張機能がインストールされていない場合、Teams Toolkit は Azure Functions バインド拡張機能をインストールします。

* NPM パッケージ。タブ アプリ、ボット アプリ、メッセージング拡張機能アプリ、および Azure Functions に適用されます。 NPM がインストールされていない場合、Teams Toolkit はすべての NPM パッケージをインストールします。

* ボットとメッセージングの拡張機能。 Teams Toolkit は Ngrok を起動して、ボットとメッセージング拡張機能の HTTP トンネルを作成します。

* 使用可能なポート。タブ、ボット、メッセージング拡張機能、および Azure Functions ポートが使用できない場合、ローカル デバッグは終了します。

  次の表に、コンポーネントで使用できるポートのリストを示します:

  | コンポーネント  | ポート |
  | --- | --- |
  | Tab | 53000 |
  | ボット、またはメッセージングの拡張機能 | 3978 |
  | ボットまたはメッセージング拡張機能のノード インスペクター | 9239 |
  | Azure Functions | 7071 |
  | Azure Functions のノード インスペクター | 9229 |


<!-- The following table lists the limitations if the required software is unavailable for debugging:

|Project type|Installation| Limitation|
|----------|--------------------------------|-----|
|Tab without Azure functions | Node.js LTS versions 10, 12, **14 (recommended)**, 16 | The local debug terminates, if Node.js is not installed or the version doesn't match the requirement.|
|Tab with Azure functions | Node.js LTS versions 10, 12, **14 (recommended)** |The local debug terminates, if Node.js is not installed or the version doesn't match the requirement.|
|Bot | Node.js LTS versions 10, 12, **14 (recommended)**, 16|The local debug terminates, if Node.js is not installed or the version doesn't match the requirement.|
|Messaging extension | Node.js LTS versions 10, 12, **14 (recommended)**, 16 |The local debug terminates, if Node.js is not installed or the version doesn't match the requirement.|
|Sign in to Microsoft 365 account | Microsoft 365 credentials |Teams toolkit prompts you to sign in to Microsoft 365 account, if you haven't signed in. |
|Bot, messaging extension | Ngrok version 2.3| • If Ngrok is not installed or the version doesn't match the requirement, the Teams toolkit installs Ngrok NPM package `ngrok@4.2.2` in `~/.fx/bin/ngrok`. </br> • The Ngrok binary is managed by Ngrok NPM package in `/.fx/bin/ngrok/node modules/ngrok/bin`.|
|Azure functions | Azure Functions Core Tools version 3| • If Azure Functions Core Tools is not installed or the version doesn't match the requirement, the Teams toolkit installs Azure Functions Core Tools NPM package, azure-functions-core-tools@3 for **Windows** and for **macOs** in  `~/.fx/bin/func`. </br> • The Azure Functions Core Tools NPM package in  `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` manages Azure Functions Core Tools binary. For Linux, the local debug terminates.|
|Azure functions |.NET Core SDK version|• If .NET Core SDK is not installed or the version  doesn't match the requirement, the toolkit installs .NET Core SDK for Windows and macOS in `~/.fx/bin/dotnet`.</br> • For Linux, the local debug terminates.|
|Azure functions | Azure functions binding extensions defined in `api/extensions.csproj`| If Azure functions binding extensions is not installed, the toolkit installs Azure functions binding extensions.|
|NPM packages| NPM packages for tab app, bot app, messaging extension app, and Azure functions|If NPM is not installed, the toolkit installs all NPM packages.|
|Bot and messaging extension | Ngrok |Toolkit starts Ngrok to create a HTTP tunnel for bot and messaging extension. |

> [!NOTE]
> If tab, bot, messaging extension, and Azure functions ports are unavailable, the local debug terminates.

Use the following .NET Core versions:

| Platform  | Software|
| --- | --- |
|Windows, macOs (x64), Linux | **3.1 (recommended)**, 5.0, 6.0 |
|macOs (arm64) |6.0 |


> [!NOTE]
> If the development certificate for localhost is not installed for tab in Windows or macOS, the Teams toolkit prompts you to install it.</br> -->


**Start Debugging (F5)** を選択すると、Teams Toolkit の出力チャネルに、前提条件を確認した後の進行状況と結果が表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck.png" alt-text="前提条件":::

## <a name="register-and-configure-your-teams-app"></a>Teams アプリの登録と構成

セットアップ プロセスでは、Teams Toolkit によって、Teams アプリの次の登録と構成が準備されます:

1. [Azure AD アプリケーションを登録して構成](#registers-and-configures-azure-ad-application): Teams Toolkit は、Azure AD アプリケーションを登録して構成します。

1. [ボットを登録して構成](#registers-and-configures-bot): Teams Toolkit は、タブまたはメッセージング拡張機能アプリ用にボットを登録して構成します。

1. [Teams アプリを登録して構成](#registers-and-configures-teams-app): Teams Toolkit によって Teams アプリが登録および構成されます。

### <a name="registers-and-configures-azure-ad-application"></a>Azure AD アプリケーションを登録して構成

1. Azure AD アプリケーションを登録します。

1. クライアント シークレットを作成します。

1. API を公開します。

    a.  アプリケーション ID URI を構成します。 タブの場合、`api://localhost/{appId}`。 ボット、メッセージングの拡張機能の場合、  `api://botid-{botid}`。

    b. `access_as_user` という名前のスコープを追加します。 **管理者とユーザー** に対して有効にします。

次の表に、クライアント ID を持つ Microsoft 365 クライアント アプリケーションを示します。

  | Microsoft 365 クライアント アプリケーション |  クライアント ID  |
  | --- | --- |
  | Teams デスクトップ、モバイル | 1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
  | Teams Web | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
  | Office.com | 4345a7b9-9a63-4910-a426-35363201d503 |
  | Office.com | 4765445b-32c6-49b0-83e6-1d93765276ca |
  | Office デスクトップ | 0ec893e0-5785-4de6-99da-4ed124e5296c |
  | Outlook デスクトップ | d3590ed6-52b3-4102-aeff-aad2292ab01c |
  | Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
  | Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

4. API のアクセス許可を構成します。 Microsoft Graph のアクセス許可を **User.Read** に追加します。

次の表に、認証の構成を次のように示します:

  | プロジェクトの種類 | Web のリダイレクト URI | シングルページ アプリケーションのリダイレクト URI |
  | --- | --- | --- |
  | Tab | `https://localhost:53000/auth-end.html` | `https://localhost:53000/auth-end.html?clientId={appId>}` |
  | ボット、またはメッセージングの拡張機能 | `https://ngrok.io/auth-end.html` | 該当なし |
  
### <a name="registers-and-configures-bot"></a>ボットの登録と構成 

タブ アプリまたはメッセージング拡張機能アプリの場合:

1. Azure AD アプリケーションを登録します。

1. Azure AD アプリケーションのクライアント シークレットを作成します。

1. Azure AD アプリケーションを使用して、[Microsoft Bot Framework](https://dev.botframework.com/) にボットを登録します。

1. Microsoft Teams チャネル ピッカーが追加されます。

1. メッセージング エンドポイントが `https://{ngrokTunnelId}.ngrok.io/api/messages` として構成されます。

### <a name="registers-and-configures-teams-app"></a>Teams アプリを登録し構成

`templates/appPackage/manifest.local.template.json` のマニフェスト テンプレートを使用して、[Developer](https://dev.teams.microsoft.com/home) に Teams アプリを登録します。

アプリを登録して構成すると、ローカル デバッグ ファイルが生成されます。

## <a name="take-a-tour-of-your-app-source-code"></a>アプリのソース コードのツアーを開始する

Teams Toolkit がアプリを登録して構成した後、Visual Studio Code のエクスプローラー領域でプロジェクト フォルダーとファイルを表示できます。 次の表に、ローカル デバッグ ファイルと構成の種類を示します。

| フォルダー名| コンテンツ| デバッグ構成の種類 |
| --- | --- | --- |
|  `.fx/configs/localSettings.json` | ローカル デバッグ構成ファイル | 各構成の値は、ローカル デバッグ中に生成および保存されます。 |
|  `templates/appPackage/manifest.local.template.json` | ローカル デバッグ用の Teams アプリ マニフェスト テンプレート ファイル | ファイル内のプレースホルダーは、ローカル デバッグ中に解決されます。 |
|  `tabs/.env.teams.local`  | タブの環境変数ファイル  | 各環境変数の値は、ローカル デバッグ中に生成および保存されます。 |
|  `bot/.env.teamsfx.local` | ボットとメッセージング拡張機能の環境変数ファイル| 各環境変数の値は、ローカル デバッグ中に生成および保存されます。 |
| `api/.env.teamsfx.local`  | Azure Functions の環境変数ファイル | 各環境変数の値は、ローカル デバッグ中に生成および保存されます。 |


## <a name="see-also"></a>関連項目

[Teams Toolkit を使用して Teams アプリをデバッグする](debug-local.md)
