---
title: バックグランド プロセスのデバッグ
author: surbhigupta
description: このモジュールでは、Visual Studio コードと Teams Toolkit がローカル デバッグ プロセス中にどのように動作するか、また Teams アプリを登録して構成する方法
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 4d654d5da598b9bf2b9bacfc189c97df08f9a359
ms.sourcegitcommit: 707dad21dc3cf79ac831afe05096c0341bcf2fee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68653649"
---
# <a name="debug-background-process"></a>バックグランド プロセスのデバッグ

ローカル デバッグ プロセスには、 `.vscode/launch.json` Microsoft Visual Studio Code でデバッガーを構成するためのファイルと `.vscode/tasks.json` ファイルが含まれます。 Visual Studio Code によってデバッガーが起動され、Microsoft Edge または Google Chrome によって新しいブラウザー インスタンスが起動されます。

デバッグ プロセスワークフローは次のとおりです。

1. `launch.json` ファイルは Visual Studio Code でデバッガーを構成します。

2. Visual Studio Code では、複合 **preLaunchTask**、 **Start Teams App Locally** in file が `.vscode/tasks.json` 実行されます。

3. その後、Visual Studio Code は、**ボットにアタッチ**、**バックエンドにアタッチ**、**フロントエンドにアタッチ**、**ボットの起動** など、複雑な構成で指定されたデバッガーを立ち上げます。

4. Microsoft Edge または Google Chrome は、新しいブラウザー インスタンスを起動し、Teams クライアントを読み込む Web ページを開きます。

## <a name="verification-of-prerequisites"></a>前提条件の確認

Teams Toolkit は、デバッグ プロセス中に次の前提条件を確認します:

* Node.js。次のプロジェクトの種類に適用されます:

  |プロジェクトの種類|Node.js LTS バージョン|
  |----------|--------------------------------|
  |Tab | 14、16 (推奨) |
  |SPFx タブ | 14、16 (推奨)|
  |Bot |  14、16 (推奨)|
  |メッセージ拡張機能: | 14、16 (推奨) |

* 有効な資格情報でサインインしていない場合は、Teams Toolkit から Microsoft 365 アカウントへのサインインを求められます。
* ローカル デバッグの終了を防ぐために、開発者テナントのカスタム アプリのアップロードまたはサイドローディングが有効になっています。
* Ngrok がインストールされていない場合、またはバージョンが要件と一致しない場合、Teams Toolkit は Ngrok NPM パッケージ`ngrok@4.2.2``~/.fx/bin/ngrok`をインストールします。 Ngrok バイナリ バージョン 2.3 は、ボットとメッセージの拡張機能に適用できます。 Ngrok バイナリは、`/.fx/bin/ngrok/node modules/ngrok/bin` の Ngrok NPM パッケージによって管理されます。
* Teams Toolkit では、Azure Functions Core Tools バージョン 4 がインストールされていない場合、またはバージョンが要件と一致しない場合、Azure Functions Core Tools NPM パッケージ (**Windows** および **MacOs** `~/.fx/bin/func`用の azure-functions-core-tools@3) がインストールされます。 `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` のAzure Functions Core Tools NPM パッケージは、バイナリ Azure Functions Core Tools を管理します。 Linux の場合、ローカル デバッグは終了します。
* .NET Core SDK がインストールされていない場合、またはバージョンが要件と一致しない場合、Teams Toolkit は 、Azure Functionsに適用される .NET Core SDK バージョンに .NET Core SDK for **Windows** および **MacOS** `~/.fx/bin/dotnet`をインストールします。 Linux の場合、ローカル デバッグは終了します。

  次の表に、.NET Core のバージョンを示します:

  | プラットフォーム  | ソフトウェア|
  | --- | --- |
  |Windows、macOS (x64)、Linux | **3.1 (推奨)**、5.0、6.0 |
  |macOS (arm64) |6.0 |

* 開発証明書。 **Windows** または **MacOS** のタブに localhost の開発証明書がインストールされていない場合は、Teams Toolkit からインストールを求めるメッセージが表示されます。
* Azure Functionsバインド拡張機能が`api/extensions.csproj`定義されています。バインド拡張機能Azure Functionsインストールされていない場合、Teams Toolkit はバインド拡張機能Azure Functionsインストールします。
* NPM パッケージ。タブ アプリ、ボット アプリ、メッセージ拡張機能アプリ、および Azure Functions に適用されます。 NPM パッケージがインストールされていない場合、Teams Toolkit はすべての NPM パッケージをインストールします。
* ボットとメッセージ拡張機能、Teams Toolkit は Ngrok を起動して、ボットとメッセージ拡張機能の HTTP トンネルを作成します。
* 使用可能なポート。タブ、ボット、メッセージ拡張機能、および Azure Functions ポートが使用できない場合、ローカル デバッグは終了します。

  次の表に、コンポーネントで使用できるポートのリストを示します:

  | コンポーネント  | ポート |
  | --- | --- |
  | Tab | 53000 |
  | ボットまたはメッセージ拡張機能 | 3978 |
  | ボットまたはメッセージ拡張機能のノード インスペクター | 9239 |
  | Azure Functions | 7071 |
  | Azure Functions のノード インスペクター | 9229 |

<!-- The following table lists the limitations if the required software is unavailable for debugging:

|Project type|Installation| Limitation|
|----------|--------------------------------|-----|
|Tab without Azure functions | Node.js LTS versions 10, 12, **14 (recommended)**, 16 | The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Tab with Azure functions | Node.js LTS versions 10, 12, **14 (recommended)** |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Bot | Node.js LTS versions 10, 12, **14 (recommended)**, 16|The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Message extension | Node.js LTS versions 10, 12, **14 (recommended)**, 16 |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Sign-in to Microsoft 365 account | Microsoft 365 credentials |Teams Toolkit prompts you to sign-in to Microsoft 365 account, if you haven't signed in. |
|Bot, message extension | Ngrok version 2.3| • If Ngrok isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Ngrok NPM package `ngrok@4.2.2` in `~/.fx/bin/ngrok`. </br> • The Ngrok binary is managed by Ngrok NPM package in `/.fx/bin/ngrok/node modules/ngrok/bin`.|
|Azure functions | Azure Functions Core Tools version 3| • If Azure Functions Core Tools isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Azure Functions Core Tools NPM package, azure-functions-core-tools@3 for **Windows** and for **macOs** in  `~/.fx/bin/func`. </br> • The Azure Functions Core Tools NPM package in `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` manages Azure Functions Core Tools binary. For Linux, the local debug terminates.|
|Azure functions |.NET Core SDK version|• If .NET Core SDK isn't installed or the version  doesn't match the requirement, the Toolkit installs .NET Core SDK for Windows and macOS in `~/.fx/bin/dotnet`.</br> • For Linux, the local debug terminates.|
|Azure functions | Azure functions binding extensions defined in `api/extensions.csproj`| If Azure functions binding extensions isn't installed, the Toolkit installs Azure functions binding extensions.|
|NPM packages| NPM packages for tab app, bot app, message extension app, and Azure functions|If NPM isn't installed, the Toolkit installs all NPM packages.|
|Bot and message extension | Ngrok |Toolkit starts Ngrok to create a HTTP tunnel for bot and message extension. |

> [!NOTE]
> If tab, bot, message extension, and Azure functions ports are unavailable, the local debug terminates.

Use the following .NET Core versions:

| Platform  | Software|
| --- | --- |
|Windows, macOs (x64), Linux | **3.1 (recommended)**, 5.0, 6.0 |
|macOs (arm64) |6.0 |

> [!NOTE]
> If the development certificate for localhost isn't installed for tab in Windows or MacOS, the Teams Toolkit prompts you to install it.</br> -->

**Start Debugging (F5)** を選択すると、Teams Toolkit の出力チャネルに、前提条件を確認した後の進行状況と結果が表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck1.png" alt-text="前提条件チェックの概要" lightbox="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck1.png":::

## <a name="register-and-configure-teams-app"></a>Teams アプリの登録と構成

セットアップ プロセスでは、Teams Toolkit によって、Teams アプリの次の登録と構成が準備されます:

1. [Microsoft Azure Active Directory(Azure AD) アプリの登録と構成](#registers-and-configures-microsoft-azure-active-directoryazure-ad-app)

1. [ボットを登録して構成します](#registers-and-configures-bot)。

1. [Teams アプリを登録して構成します](#registers-and-configures-teams-app)。

### <a name="registers-and-configures-microsoft-azure-active-directoryazure-ad-app"></a>Microsoft Azure Active Directory(Azure AD) アプリの登録と構成

1. Azure AD アプリを登録します。

1. クライアント シークレットを作成します。

1. API を公開します。

    a.  アプリケーション ID URI を構成します。 タブの場合、`api://localhost/{appId}`。 ボット、メッセージングの拡張機能の場合、`api://botid-{botid}`。

    b. `access_as_user` という名前のスコープを追加します。 **管理者とユーザー** に対して有効にします。

4. API のアクセス許可を構成します。 Microsoft Graph のアクセス許可を **User.Read** に追加します。

    次の表に、認証の構成を示します。

      | プロジェクトの種類 | Web のリダイレクト URI | シングルページ アプリケーションのリダイレクト URI |
      | --- | --- | --- |
      | Tab | `https://localhost:53000/auth-end.html` | `https://localhost:53000/auth-end.html?clientId={appId>}` |
      | ボットまたはメッセージ拡張機能 | `https://ngrok.io/auth-end.html` | 該当なし |

    次の表に、クライアント ID を持つ Microsoft 365 クライアント アプリケーションを示します:

      | Microsoft 365 クライアント アプリケーション | クライアント ID |
      | --- | --- |
      | Teams デスクトップ、モバイル | 1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
      | Teams Web | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
      | Office.com | 4345a7b9-9a63-4910-a426-35363201d503 |
      | Office.com | 4765445b-32c6-49b0-83e6-1d93765276ca |
      | Office デスクトップ | 0ec893e0-5785-4de6-99da-4ed124e5296c |
      | Outlook デスクトップ | d3590ed6-52b3-4102-aeff-aad2292ab01c |
      | Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
      | Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

### <a name="registers-and-configures-bot"></a>ボットの登録と構成

タブ アプリまたはメッセージ拡張機能アプリの場合:

1. Azure AD アプリケーションを登録します。

1. Azure AD アプリケーションのクライアント シークレットを作成します。

1. Azure AD アプリケーションを使用して、[Microsoft Bot Framework](https://dev.botframework.com/) にボットを登録します。

1. Teams チャネルを追加します。

1. メッセージング エンドポイントが `https://{ngrokTunnelId}.ngrok.io/api/messages` として構成されます。

### <a name="registers-and-configures-teams-app"></a>Teams アプリを登録し構成

でマニフェスト テンプレートを使用して [、開発者ポータル](https://dev.teams.microsoft.com/home) に Teams アプリを登録します `templates/appPackage/manifest.template.json`。

アプリの登録と構成が終わったら、ローカル デバッグ ファイルが生成されます。

## <a name="take-a-tour-of-your-app-source-code"></a>アプリのソース コードのツアーを開始する

Teams Toolkit がアプリを登録して構成した後、Visual Studio Code の **エクスプローラー** でプロジェクト フォルダーとファイルを表示できます。 次の表に、ローカル デバッグ ファイルと構成の種類を示します。

| フォルダー名| コンテンツ| デバッグ構成の種類 |
| --- | --- | --- |
|  `.fx/configs/config.local.json` | ローカル デバッグ構成ファイル | 各構成の値は、ローカル デバッグ中に生成および保存されます。 |
|  `templates/appPackage/manifest.template.json` | ローカル デバッグ用の Teams アプリ マニフェスト テンプレート ファイル | ローカル デバッグ中のファイル内のプレースホルダー。 |
|  `tabs/.env.teams.local`  | タブの環境変数ファイル | 各環境変数の値は、ローカル デバッグ中に生成および保存されます。 |
|  `bot/.env.teamsfx.local` | ボットとメッセージ拡張機能の環境変数ファイル| 各環境変数の値は、ローカル デバッグ中に生成および保存されます。 |
| `api/.env.teamsfx.local`  | Azure Functions の環境変数ファイル | 各環境変数の値は、ローカル デバッグ中に生成および保存されます。 |

## <a name="see-also"></a>関連項目

* [Teams Toolkit を使用して Teams アプリをデバッグする](debug-local.md)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [クラウドにデプロイする](deploy.md)
* [Teams アプリ マニフェストのプレビューとカスタマイズ](TeamsFx-preview-and-customize-app-manifest.md)
