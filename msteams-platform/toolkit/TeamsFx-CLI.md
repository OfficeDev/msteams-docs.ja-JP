---
title: TeamsFx コマンド ライン インターフェイス
author: MuyangAmigo
description: このモジュールでは、TeamsFx ライブラリ、TeamsFx コマンド ライン インターフェイス、サポートされているコマンドとそのシナリオについて説明します。
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d269da398280f51a3225414f279a25fcd5d9d7cf
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142074"
---
# <a name="teamsfx-library"></a>TeamsFx ライブラリ

Microsoft Teams Framework (TeamsFx) は、Microsoft Identity への簡単なアクセスなど、一般的な機能と統合パターンをカプセル化するライブラリです。 構成なしで Microsoft Teams 用のアプリを構築できます。

TeamsFx の主な機能の一覧を次に示します。

* **TeamsFx コラボレーション**: 開発者とプロジェクト所有者が TeamsFx プロジェクトに他のコラボレーターを招待できるようにします。 TeamsFx プロジェクトをデバッグおよび展開するために共同作業を行うことができます。

* **TeamsFx CLI**: アプリケーション開発Teams高速化します。 また、自動化用のスクリプトに CLI を統合できる CI/CD シナリオも可能になります。

* **TeamsFx SDK**: Teams開発者向けに調整されたクライアントとサーバー側の両方のコードに対する単純な認証を含むプライマリ TeamsFx コード ライブラリなど、データベースへのアクセスを提供します。

## <a name="teamsfx-command-line-interface"></a>TeamsFx コマンド ライン インターフェイス

TeamsFx は、Teams アプリケーションの開発を加速するテキスト ベースのコマンド ライン インターフェイスです。 これは、Teams アプリケーションを構築する際にキーボード中心のエクスペリエンスを提供することを目的としています。 また、自動化用のスクリプトに CLI を統合できる CI/CD シナリオも可能になります。

詳細については、以下を参照してください。

* [ソース コード](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)
* [パッケージ (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>はじめに

`npm` から `teamsfx-cli` をインストールし、`teamsfx -h` を実行して、使用可能なすべてのコマンドを確認します。

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>サポート対象コマンド

| コマンド | 説明 |
|----------------|-------------|
| `teamsfx new`| 新しい Teams アプリケーションを作成します。|
| `teamsfx add`| Teams アプリケーションに機能を追加します。|
| `teamsfx account`| クラウド サービス アカウントを管理します。 サポートされているクラウド サービスは、'Azure' と 'Microsoft 365' です。 |
| `teamsfx env` | 環境を管理する。 |
| `teamsfx provision` | 現在のアプリケーションでクラウド リソースをプロビジョニングします。|
| `teamsfx deploy` | 現在のアプリケーションをデプロイします。  |
| `teamsfx package` | Teams アプリを発行用のパッケージにビルドします。|
| `teamsfx validate` | 現在のアプリケーションを検証します。|
| `teamsfx publish` | アプリを Teams に公開する。|
| `teamsfx preview` | 現在のアプリケーションをプレビューします。 |
| `teamsfx config`  | 構成データを管理します。 |
| `teamsfx permission`| 同じプロジェクトで他の開発者と共同作業を行います。|

## `teamsfx new`

既定では、対話型モードであり、`teamsfx new`新しいTeams アプリケーションを作成するためのガイドです。 フラグ`false`を [.] に設定`--interactive`すると、非対話型モードで作業できます。

| コマンド | 説明 |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | 既存のテンプレートからアプリを作成する |
| `teamsfx new template list`     | 使用可能なすべてのテンプレートを一覧表示する |

### <a name="parameters-for-teamsfx-new"></a>`teamsfx new` のパラメーター

| パラメーター | 要件 | 説明 |
|:---------------- |:-------------|:-------------|
|`--app-name` | はい| Teams アプリケーションの名前です。|
|`--interactive`| いいえ | オプションを対話形式で選択します。 オプションは `true` と `false` で、既定値は `true` です。|
|`--capabilities`| いいえ| Teamsアプリケーション機能を選択します。オプションは `tab`、 , , `tab-non-sso`, `tab-spfx`, `bot``message-extension`, `notification``command-bot`, . `search-app``sso-launch-page` 既定値は `tab` です。|
|`--programming-language`| いいえ| プロジェクトのプログラミング言語です。 オプションは `javascript` または `typescript` で、デフォルト値は `javascript` です。|
|`--folder`| いいえ | プロジェクト ディレクトリ。 このディレクトリの下に、アプリ名を持つサブ フォルダーが作成されます。 既定値は `./` です。|
|`--spfx-framework-type`| いいえ| `SPFx tab` 機能が選択されている場合に適用されます。 フロントエンド フレームワーク。 オプションは `none`、 `react` および `minimal`既定値 `none`です。|
|`--spfx-web part-name`| いいえ | `SPFx tab` 機能が選択されている場合に適用されます。 既定値は "helloworld" です。|
|`--bot-host-type-trigger`| なし | `Notification bot` 機能が選択されている場合に適用されます。 オプションは `http-restify`、、 `http-functions`、および `timer-functions`. 既定値は `http-restify` です。|

### <a name="scenarios-for-teamsfx-new"></a>`teamsfx new` のシナリオ

対話型モードを使用して、Teams アプリを作成できます。 次の一覧では、次を使用してすべてのパラメーター `teamsfx new`を制御するシナリオを示します。

* restify サーバーを使用した Http によってトリガーされた通知ボット

  ```bash
  teamsfx new --interactive false --capabilities "notification" --bot-host-type-trigger "http-restify" --programming-language "typescript" --folder "./" --app-name       MyAppName
  ```

* Teamsコマンドと応答ボット

  ```bash
  teamsfx new --interactive false --capabilities "command-bot" --programming-language "typescript" --folder "./" --app-name myAppName
  ```

* React を使用して SPFx でホストされているタブ アプリ

  ```bash
  teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
  ```

## `teamsfx add`

次の表に、Teams アプリケーションのさまざまな機能とその説明を示します。

| コマンド | 説明 |
|:----------------  |:-------------|
| `teamsfx add notification` | さまざまなトリガーを介してMicrosoft Teamsに通知を送信します。 |
| `teamsfx add command-and-response` | Microsoft Teams チャットで簡単なコマンドに応答します。|
| `teamsfx add sso-tab` | Microsoft Teamsに埋め込まれた id 対応 web ページをTeamsします。|
| `teamsfx add tab` | Microsoft Teamsに埋め込まれた Hello world Web ページ。|
| `teamsfx add bot` | ユーザーが簡単で反復的なタスクを実行するための Hello world chatbot。 |
| `teamsfx add message-extension` | ボタンとフォームを介した対話を可能にする Hello world メッセージ拡張機能。 |
| `teamsfx add azure-function`| より少ないコードを記述できる、サーバーレスのイベントドリブンコンピューティング ソリューション。 |
| `teamsfx add azure-apim` | すべての環境にわたる API 用のハイブリッドマルチクラウド管理プラットフォーム。|
| `teamsfx add azure-sql` | クラウド用に構築された常に最新のリレーショナル データベース サービス。 |
| `teamsfx add azure-keyvault` | シークレットを安全に格納してアクセスするためのクラウド サービス。 |
| `teamsfx add sso` | Teams起動ページとボット機能のシングル Sign-On機能を開発します。 |
| `teamsfx add api-connection [auth-type]` | TeamsFx SDK を使用して認証をサポートする API にConnectします。 |
| `teamsfx add cicd` | GitHub、Azure DevOps、または Jenkins の CI/CD ワークフローを追加します。|

## `teamsfx account`

次の表に、Azure やMicrosoft 365などのクラウド サービス アカウントを示します。

| コマンド | 説明 |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | 選択したクラウド サービスにログインします。 サービス オプションは、Microsoft 365または Azure です。 |
| `teamsfx account logout <service>`  | 選択したクラウド サービスからログアウトします。 サービス オプションは、Microsoft 365または Azure です。 |
| `teamsfx account set --subscription` | アカウント設定を更新してサブスクリプション ID を設定します。 |

## `teamsfx env`

次の表に、さまざまな環境を示します。

|  コマンド  | 説明 |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | 指定した環境からコピーして、新しい環境を追加します。 |
| `teamsfx env list` | すべての環境を一覧表示します。 |

### <a name="scenarios-for-teamsfx-env"></a>`teamsfx env` のシナリオ

既存の開発環境からコピーして新しい環境を作成します。

```bash
teamsfx env add staging --env dev
```

## `teamsfx provision`

現在のアプリケーションでクラウド リソースをプロビジョニングします。

| `teamsFx provision`コマンド | 説明 |
|:----------------  |:-------------|
| `teamsfx provision manifest` | 指定したマニフェスト ファイルで指定された対応する情報を使用して、Teams開発者ポータルでTeams アプリをプロビジョニングします。 |

### <a name="parameters-for-teamsfx-provision"></a>`teamsfx provision` のパラメーター

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい| プロジェクトの環境を選択します。 |
|`--subscription`| いいえ | Azure サブスクリプション ID を指定します。 |
|`--resource-group`| いいえ | 既存のリソース グループの名前を設定します。 |
|`--sql-admin-name`| なし | プロジェクトにSQLリソースがある場合に適用されます。 SQL の管理者名。|
|`--sql-password`| なし| プロジェクトにSQLリソースがある場合に適用されます。 SQL の管理者パスワード。|

## `teamsfx deploy`

このコマンドは、現在のアプリケーションをデプロイするために使用されます。 既定では、プロジェクト全体がデプロイされますが、部分的にデプロイすることもできます。 オプションは `frontend-hosting`、、`function`、`apim`、`bot``spfx``aad-manifest`、および`manifest`です。

### <a name="parameters-for-teamsfx-deploy"></a>`teamsfx deploy` のパラメーター

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい| プロジェクトの既存の環境を選択します。 |
|`--open-api-document`| いいえ | プロジェクトに APIM リソースがある場合に適用されます。 開いている API ドキュメント ファイルパス。 |
|`--api-prefix`| なし | プロジェクトに APIM リソースがある場合に適用されます。 API 名プレフィックス。 API の既定の一意の名前は `{api-prefix}-{resource-suffix}-{api-version}` です。 |
|`--api-version`| なし | プロジェクトに APIM リソースがある場合に適用されます。 API バージョン。 |
|`--include-app-manifest`| いいえ | アプリ マニフェストをTeams プラットフォームにデプロイするかどうか。 オプションは次`yes`のとおりです。`not` 既定値は `no` です。 |
|`--include-aad-manifest`| いいえ | aad マニフェストをデプロイするかどうか。 オプションは次`yes`のとおりです。`not` 既定値は `no` です。 |

## `teamsfx validate`

現在のアプリケーションを検証します。 このコマンドは、アプリケーションのマニフェスト ファイルを検証します。

### <a name="parameters-for-teamsfx-validate"></a>`teamsfx validate` のパラメーター

`--env`: プロジェクトの既存の環境を選択します。

## `teamsfx publish`

アプリを Teams に公開する。

### <a name="parameters-for-teamsfx-publish"></a>`teamsfx publish` のパラメーター

`--env`: プロジェクトの既存の環境を選択します。

## `teamsfx package`

Teams アプリを公開用のパッケージにビルドします。

## `teamsfx preview`

ローカルまたはリモートから現在のアプリケーションをプレビューします。

### <a name="parameters-for-teamsfx-preview"></a>`teamsfx preview` のパラメーター

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--local`| いいえ | ローカルからアプリケーションをプレビューします。 `--local` は `--remote` 専用です。 |
|`--remote`| なし | リモートからアプリケーションをプレビューします。 `--remote` は `--local` 専用です。 |
|`--env`| いいえ | パラメーター `--remote` が追加されたときに、プロジェクトの既存の環境を選択します。 |
|`--folder`| なし | プロジェクトのルート ディレクトリ。 既定値は `./` です。 |
|`--browser`| いいえ | Teams Web クライアントを開くためのブラウザー。 オプションはシステムの既定ブラウザなどの `chrome`、`edge`、`default` で、値は `default` です。 |
|`--browser-arg`| いいえ | ブラウザに渡す引数。--browser が必要です。たとえば、--browser-args="--guest" のように、複数回使用できます。 |
|`--sharepoint-site`| いいえ | SPFx プロジェクトのリモート プレビュー用の `{your-tenant-name}.sharepoint.com` などの SharePoint サイトの URL。 |
|`--m365-host`| Teams、Outlook、またはOfficeでアプリケーションをプレビューします。 オプションは `teams`、および `office``outlook` . 既定値は `teams` です。 |

### <a name="scenarios-for-teamsfx-preview"></a>`teamsfx preview` のシナリオ

次の一覧では、teamsfx プレビューの一般的なシナリオを示します。

* ローカル プレビュー

  依存関係:

  * Node.js
  * .NET SDK
  * Azure Functions Core Tools

  ```bash
  teamsfx preview --local
  teamsfx preview --local --browser chrome
  ```

* リモート プレビュー

  ```bash
  teamsfx preview --remote
  teamsfx preview --remote --browser edge
  ```

  > [!NOTE]
  > React などのバックグラウンド サービスのログは `~/.fx/cli-log/local-preview/` に保存されます。

## `teamsfx config`

構成データは、ユーザー スコープまたはプロジェクト スコープ内にあります。

|  コマンド  | 説明 |
|:----------------  |:-------------|
| `teamsfx config get [option]` | オプションの構成値を表示する |
| `teamsfx config set <option> <value>` | オプションの構成値を更新する |

### <a name="parameters-for-teamsfx-config"></a>`teamsfx config` のパラメーター

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい | プロジェクトの既存の環境を選択します。 |
|`--folder`| いいえ | プロジェクト構成の取得または設定に使用されるディレクトリProject。 既定値は `./` です。 |
|`--global`| いいえ | 構成に対応します。 true の場合、スコープはプロジェクト スコープではなくユーザー スコープに制限されます。 既定値は `false` です。 現在、サポートされているグローバル構成には`telemetry`、, , `validate-dotnet-sdk`, `validate-func-core-tools`. `validate-node` |

### <a name="scenarios-for-teamsfx-config"></a>`teamsfx config` のシナリオ

ファイル内の `.userdata` シークレットは暗号化され、 `teamsfx config` 必要な値を表示または更新するのに役立ちます。

* テレメトリ データの送信を停止する

  ```bash
  teamsfx config set telemetry off
  ```

* 環境チェッカーを無効にする

  Node.jsを有効または無効にする構成には、.NET SDK と Azure Functions Core Tools の検証の 3 つがあり、これらすべてが既定で有効になっています。 依存関係の検証が不要で、自分で依存関係をインストールする場合は、構成を "オフ" に設定できます。 次のガイドを確認してください。

  * [Node.js インストール ガイド](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
  * [.NET SDK インストール ガイド](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
  * [Azure Functions Core Tools インストール ガイド](<https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure>- functions-core-tools)。

  .NET SDK 検証を無効にするには、次のコマンドを使用します。

  ```bash
  teamsfx config set validate-dotnet-sdk off
  ```

  .NET SDK の検証を有効にするには、次のコマンドを使用します。

  ```bash
  teamsfx config set validate-dotnet-sdk on
  ```

* すべてのユーザー スコープ構成を表示する

  ```bash
  teamsfx config get -g
  ```

* プロジェクト内のすべての構成を表示する

  シークレットは以下では自動的に復号化されます。

    ```bash
    teamsfx config get --env dev
    ```

* プロジェクト内のシークレット構成を更新する

  ```bash
  teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
  ```

## `teamsfx permission`

TeamsFx CLI には、コラボレーション シナリオ用のコマンドが用意 `teamsFx permission` されています。

|  コマンド | 説明 |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | 指定された環境のプロジェクトに対して、共同編集者の Microsoft 365 アカウントにアクセス許可を付与します。 |
| `teamsfx permission status` | プロジェクトのアクセス許可の状態を表示する |

### <a name="parameters-for-teamsfx-permission-grant"></a>`teamsfx permission grant` のパラメーター

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい | env 名を指定します。 |
|`--email`| はい | コラボレーターの Microsoft 365 メール アドレスを指定します。 コラボレーターのアカウントが作成者と同じテナントにあることを確認します。 |

### <a name="parameters-for-teamsfx-permission-status"></a>`teamsfx permission status` のパラメーター

| パラメーター | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい | env 名を指定します。 |
|`--list-all-collaborators` | なし | このフラグを使用すると、Teams Toolkit CLI は、このプロジェクトのすべてのコラボレーターを出力します。 |

### <a name="scenarios-for-teamsfx-permission"></a>`teamsfx permission` のシナリオ

次の一覧は、プロジェクトに必要なアクセス許可を `TeamsFx` 提供します。

* アクセス許可の付与

  プロジェクトの作成者と共同作業者は、`teamsfx permission grant` コマンドを使用して、プロジェクトに新しい共同作業者を追加できます。

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  必要なアクセス許可を受け取った後、プロジェクト作成者とコラボレーターはGitHubによって新しいコラボレーターとプロジェクトを共有でき、新しいコラボレーターはMicrosoft 365 アカウントのすべてのアクセス許可を持つことができます。

* アクセス許可の状態を表示する

  Project作成者とコラボレーターは、コマンドを使用`teamsfx permission status`して、特定の env に対Microsoft 365アカウントのアクセス許可を表示できます。

  ```bash
  teamsfx permission status --env dev
  ```

* すべてのコラボレーターを一覧表示する

  プロジェクトの作成者と共同作業者は、`teamsfx permission status` コマンドを使用して、特定の環境のすべての共同作業者を表示できます。

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

* CLI での E2E コラボレーション作業フロー

  * プロジェクト作成者として:

    * 新しい TeamsFx タブまたはボット プロジェクトを作成し、ホストの種類として Azure を選択するには:

      ```bash
      teamsfx new --interactive false --app-name newapp --host-type azure
      ```

    * Microsoft 365 アカウントと Azure アカウントにログインするには:

      ```bash
      teamsfx account login azure
      teamsfx account login Microsoft 365
      ```

    * プロジェクトをプロビジョニングするには:

      ```bash
      teamsfx provision
      ```

    * 共同作業者を表示するには:

      ```bash
      teamsfx permission status --env dev --list-all-collaborators
      ```

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

    * 共同作業者として別のアカウントを追加する。 追加されたアカウントが同じテナントの下にあることを確認します。

      ```bash
      teamsfx permission grant --env dev --email user-email@user-tenant.com
      ```

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="permission":::

    * プロジェクトを GitHub にプッシュするには

  * Project Collaborator として:

    * GitHub からプロジェクトを複製します。
    * Microsoft 365 アカウントにログインします。 同じ Microsoft 365 アカウントが追加されていることを確認します。

      ```bash
      teamsfx account login Microsoft 365
      ```

    * すべての Azure リソースに対する共同作成者アクセス許可を持つ Azure アカウントにログインします。

      ```bash
      teamsfx account login azure
      ```

    * アクセス許可の状態を確認します。 プロジェクト 所有者のアクセス許可が自分にあることがわかります。

      ```bash
      teamsfx permission status --env dev
      ```

      ![アクセス許可の状態](./images/permission-status.png)

    * Tab コードを更新し、プロジェクトをリモートにデプロイします。
    * リモートを起動すると、プロジェクトは正常に動作します。

## <a name="see-also"></a>関連項目

* [TeamsFx SDK for TypeScript または JavaScript](TeamsFx-SDK.md)
* [Teams Toolkit で複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams Toolkit を使用して Teams プロジェクトで共同作業する](TeamsFx-collaboration.md)
* [Teams ツールキットの概要](teams-toolkit-fundamentals.md)
