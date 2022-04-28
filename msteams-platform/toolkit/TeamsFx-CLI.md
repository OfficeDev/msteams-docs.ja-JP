---
title: TeamsFx コマンド ライン インターフェイス
author: MuyangAmigo
description: TeamsFx コマンド ライン インターフェイスについて説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 5fde7e94c198bfe76810a52ede78d0be7270ba0c
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104519"
---
# <a name="teamsfx-library"></a>TeamsFx ライブラリ

Microsoft Teams Framework (TeamsFx) は、一般的な機能と統合パターン (Microsoft Identity への簡単なアクセスなど) をカプセル化するライブラリです。 構成がゼロのMicrosoft Teams用のアプリをビルドできます。

TeamsFx の主な機能の一覧を次に示します。

* **TeamsFx コラボレーション**: 開発者とプロジェクト所有者が TeamsFx プロジェクトに他のコラボレーターを招待できるようにします。 TeamsFx プロジェクトをデバッグおよび展開するために共同作業を行うことができます。

* **TeamsFx CLI**: アプリケーション開発Teams高速化します。 また、自動化用のスクリプトに CLI を統合できる CI/CD シナリオも可能になります。

* **TeamsFx SDK**: TeamsFx ソフトウェア開発キット (SDK) は、Teams開発者向けに調整されたクライアントとサーバー側の両方のコードに対する単純な認証をカプセル化する TeamsFx コード ライブラリです。

## <a name="teamsfx-command-line-interface"></a>TeamsFx コマンド ライン インターフェイス

TeamsFx CLI は、Teamsアプリケーション開発を高速化するテキスト ベースのコマンド ライン インターフェイスです。 これは、Teams アプリケーションを構築する際にキーボード中心のエクスペリエンスを提供することを目的としています。 また、自動化用のスクリプトに CLI を統合できる CI/CD シナリオも可能になります。

詳細については、以下を参照してください。

* [ソースコード](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)
* [パッケージ (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>はじめに

`npm`使用可能なすべてのコマンドをインストール`teamsfx-cli`して実行`teamsfx -h`します。

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>サポート対象コマンド

| コマンド | 説明 |
|----------------|-------------|
| `teamsfx new`| 新しいTeams アプリケーションを作成します。|
| `teamsfx account`| クラウド サービス アカウントを管理します。 サポートされているクラウド サービスは、"Azure" と "Microsoft 365" です。 |
| `teamsfx env` | 環境を管理します。 |
| `teamsfx capability`| 現在のアプリケーションに新しい機能を追加します。|
| `teamsfx resource`  | 現在のアプリケーションのリソースを管理します。|
| `teamsfx provision` | 現在のアプリケーションでクラウド リソースをプロビジョニングします。|
| `teamsfx deploy` | 現在のアプリケーションをデプロイします。  |
| `teamsfx package` | Teams アプリを発行用のパッケージにビルドします。|
| `teamsfx validate` | 現在のアプリケーションを検証します。|
| `teamsfx publish` | アプリをTeamsに発行します。|
| `teamsfx preview` | 現在のアプリケーションをプレビューします。 |
| `teamsfx config`  | 構成データを管理します。 |
| `teamsfx permission`| 同じプロジェクトで他の開発者と共同作業を行います。|

## `teamsfx new`

既定では、対話型モードになり、`teamsfx new`新しいTeams アプリケーションを作成するプロセスについて説明します。 フラグ`--interactive``false`を .

| `teamsFx new` コマンド | 説明 |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | 既存のテンプレートからアプリを作成する |
| `teamsfx new template list`     | 使用可能なすべてのテンプレートを一覧表示する |

### <a name="parameters-for-teamsfx-new"></a>のパラメーター `teamsfx new`

| パラメーター | 要件 | 説明 |
|:---------------- |:-------------|:-------------|
|`--app-name` | はい| Teams アプリケーションの名前。|
|`--interactive`| いいえ | オプションを対話形式で選択します。 オプションと既定値は`true``false`次のとおりです`true`。|
|`--capabilities`| いいえ| Teamsアプリケーションの機能を選択します。複数のオプションは `tab`、`bot`および `messaging-extension` `tab-spfx`. 既定値は `tab` です。|
|`--programming-language`| いいえ| プロジェクトのプログラミング言語。 オプションは `javascript` 、 `typescript` 既定値は `javascript`.|
|`--folder`| いいえ | Project ディレクトリ。 このディレクトリの下に、アプリ名を持つサブ フォルダーが作成されます。 既定値は `./` です。|
|`--spfx-framework-type`| なし| 機能が選択されている場合 `Tab(SPfx)` に適用されます。 フロントエンド フレームワーク。 オプションと既定値`none`は`react``none`次のとおりです。|
|`--spfx-web part-name`| いいえ | 機能が選択されている場合 `Tab(SPfx)` に適用されます。 既定値は "helloworld" です。|
|`--spfx-web part-desp`| いいえ | 機能が選択されている場合 `Tab(SPfx)` に適用されます。 既定値は "helloworld description" です。 |
|`--azure-resources`| いいえ| 機能が含まれている場合に `tab` 適用されます。 Azure リソースをプロジェクトに追加します。 複数のオプションは `sql` (Azure SQL Database) と `function` (Azure Functions) です。 |

### <a name="scenarios-for-teamsfx-new"></a>のシナリオ `teamsfx new`

対話型モードを使用して、Teams アプリを作成できます。すべてのパラメーター`teamsfx new`を制御するシナリオは次のとおりです。

#### <a name="tab-app-hosted-on-spfx-using-react"></a>Reactを使用してSPFxでホストされているタブ アプリ

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>タブ、ボット機能、Azure Functionsを使用して JavaScript でアプリをTeamsする

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Azure FunctionsとAzure SQLを含むタブ アプリをTeamsする

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

クラウド サービス アカウントを管理します。 サポートされているクラウド サービスは`Azure`次のとおりです。`Microsoft 365`

| `teamsFx account` コマンド | 説明 |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | 選択したクラウド サービスにログインします。 |
| `teamsfx account logout <service>`  | 選択したクラウド サービスからログアウトします。 |
| `teamsfx account set --subscription` | アカウント設定を更新してサブスクリプション ID を設定します。 |

## `teamsfx env`

環境を管理します。

| `teamsfx env` コマンド  | 説明 |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | 指定した環境からコピーして、新しい環境を追加します。 |
| `teamsfx env list` | すべての環境を一覧表示します。 |

### <a name="scenarios-for-teamsfx-env"></a>のシナリオ `teamsfx env`

`teamsfx env`シナリオは次のとおりです。

#### <a name="create-a-new-environment"></a>新しい環境を作成する

既存の開発環境からコピーして新しい環境を追加します。

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

現在のアプリケーションに新しい機能を追加します。

| `teamsFx capability` コマンド  | 説明 |
|:----------------  |:-------------|
| `teamsfx capability add tab` | タブを追加する |
| `teamsfx capability add bot` | ボットを追加する |
| `teamsfx capability add messaging-extension`| messagE 拡張機能を追加する |

> [!NOTE]
> プロジェクトにボットが含まれている場合は、メッセージ拡張機能を追加できず、その逆も適用されます。 新しいTeams アプリ プロジェクトを作成するときに、ボットとメッセージの両方の拡張機能をプロジェクトに含めることができます。

## `teamsfx resource`

現在のアプリケーションのリソースを管理します。 サポート対象 `<resource-type>` : `azure-sql`、 `azure-function` および `azure-apim` .

| `teamsFx resource` コマンド  | 説明 |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | 現在のアプリケーションにリソースを追加します。|
| `teamsfx resource show <resource-type>`      | リソースの構成の詳細を表示します。 |
| `teamsfx resource list`      | 現在のアプリケーション内のすべてのリソースを一覧表示します。 |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>のパラメーター `teamsfx resource add azure-function`

| パラメーター  | 要件 | 説明 |
|----------------  |-------------|-------------|
|`--function-name`| はい | 関数名を指定します。 既定値は `getuserprofile` です。 |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>のパラメーター `teamsfx resource add azure-sql`

#### `--function-name`

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--function-name`| はい | 関数名を指定します。 既定値は `getuserprofile` です。 |

> [!NOTE]
> 関数名はSQLとして検証され、サーバー ワークロードからアクセスする必要があります。 プロジェクトに含まれていない場合は `Azure Functions`、プロジェクトを作成します。

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>のパラメーター `teamsfx resource add azure-apim`

> [!TIP]
> 既存のインスタンスを使用しようとすると、オプションが `APIM` 有効になります。 既定では、オプションを指定する必要はありません。ステップ中 `teamsfx provision` に新しいインスタンスが作成されます。

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--subscription`| はい | Azure サブスクリプションを選択する|
|`--apim-resource-group`| はい| リソース グループの名前。 |
|`--apim-service-name`| はい | API 管理サービス インスタンスの名前。 |
|`--function-name`| はい | 関数名を指定します。 既定値は `getuserprofile` です。 |

> [!NOTE]
> `Azure API Management` を使用 `Azure Functions`する必要があります。 プロジェクトに含 `Azure Functions`まれていない場合は、プロジェクトを作成できます。

## `teamsfx provision`

現在のアプリケーションでクラウド リソースをプロビジョニングします。

### <a name="parameters-for-teamsfx-provision"></a>のパラメーター `teamsfx provision`

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい| プロジェクトの環境を選択します。 |
|`--subscription`| いいえ | Azure サブスクリプション ID を指定します。 |
|`--resource-group`| いいえ | 既存のリソース グループの名前を設定します。 |
|`--sql-admin-name`| なし | プロジェクトにSQLリソースがある場合に適用されます。 SQLの管理者名。|
|`--sql-password`| なし| プロジェクトにSQLリソースがある場合に適用されます。 SQLの管理者パスワード。|

## `teamsfx deploy`

このコマンドは、現在のアプリケーションをデプロイするために使用されます。 既定では、プロジェクト全体がデプロイされますが、部分的にデプロイすることもできます。 複数のオプションは`frontend-hosting`、、`apim``function``teamsbot`および`spfx`です。

### <a name="parameters-for-teamsfx-deploy"></a>のパラメーター `teamsfx deploy`

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい| プロジェクトの既存の環境を選択します。 |
|`--open-api-document`| いいえ | プロジェクトに APIM リソースがある場合に適用されます。 開いている API ドキュメント ファイルパス。 |
|`--api-prefix`| なし | プロジェクトに APIM リソースがある場合に適用されます。 API 名プレフィックス。 API の既定の一意の名前は `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| なし | プロジェクトに APIM リソースがある場合に適用されます。 API バージョン。 |

## `teamsfx validate`

現在のアプリケーションを検証します。 このコマンドは、アプリケーションのマニフェスト ファイルを検証します。

### <a name="parameters-for-teamsfx-validate"></a>のパラメーター `teamsfx validate`

`--env`: プロジェクトの既存の環境を選択します。

## `teamsfx publish`

アプリをTeamsに発行します。

### <a name="parameters-for-teamsfx-publish"></a>のパラメーター `teamsfx publish`

`--env`: プロジェクトの既存の環境を選択します。

## `teamsfx package`

Teams アプリを公開用のパッケージにビルドします。

## `teamsfx preview`

ローカルまたはリモートから現在のアプリケーションをプレビューします。

### <a name="parameters-for-teamsfx-preview"></a>のパラメーター `teamsfx preview`

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--local`| いいえ | ローカルからアプリケーションをプレビューします。 `--local`は .`--remote` |
|`--remote`| いいえ | リモートからアプリケーションをプレビューします。 `--remote`は .`--local` |
|`--env`| いいえ | パラメーター `--remote` が追加されたときに、プロジェクトの既存の環境を選択します。 |
|`--folder`| なし | ルート ディレクトリをProjectします。 既定値は `./` です。 |
|`--browser`| いいえ | Web クライアントを開くブラウザー Teams。 オプションは `chrome`、 `edge` `default` システムの既定のブラウザーなどであり、値は次のとおりです `default`。 |
|`--browser-arg`| いいえ | ブラウザーに渡す引数には --browser が必要です。--browser-args="--guest" など、複数回使用できます。 |
|`--sharepoint-site`| いいえ | SharePoint サイト URL (SPFx プロジェクトのリモート プレビューなど`{your-tenant-name}.sharepoint.com`)。 |

### <a name="scenarios-for-teamsfx-preview"></a>のシナリオ `teamsfx preview`

#### <a name="local-preview"></a>ローカル プレビュー

依存 関係：

* Node.js
* .NET SDK
* Azure Functions Core Tools

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>リモート プレビュー

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> Reactなどのバックグラウンド サービスの`~/.fx/cli-log/local-preview/`ログは 、 .

## `teamsfx config`

構成データは、ユーザー スコープまたはプロジェクト スコープで管理します。

| `teamsfx config` コマンド  | 説明 |
|:----------------  |:-------------|
| `teamsfx config get [option]` | オプションの構成値を表示する |
| `teamsfx config set <option> <value>` | オプションの構成値を更新する |

### <a name="parameters-for-teamsfx-config"></a>のパラメーター `teamsfx config`

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい | プロジェクトの既存の環境を選択します。 |
|`--folder`| いいえ | Project ディレクトリ。 これは、プロジェクトの構成を取得または設定するために使用されます。 既定値は `./` です。 |
|`--global`| いいえ | 構成に対応します。 これが true の場合、スコープはプロジェクト スコープではなくユーザー スコープに制限されます。 既定値は `false` です。 現在、サポートされているグローバル構成には `telemetry`、 , `validate-dotnet-sdk`, `validate-func-core-tools`, `validate-node`. |

### <a name="scenerios-for-teamsfx-config"></a>用のシーリオス `teamsfx config`

ファイル内の `.userdata` シークレットは暗号化され、 `teamsfx config` 値を表示または更新するのに役立ちます。

#### <a name="stop-sending-telemetry-data"></a>テレメトリ データの送信を停止する

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>環境チェッカーを無効にする

Node.js、.NET SDK、Azure Functions Core Tools 検証の 3 つの構成があり、これらすべてが既定で有効になっています。 依存関係の検証が不要で、自分で依存関係をインストールする場合は、構成を "オフ" に設定できます。 次のガイドを確認してください。

* [Node.js インストール ガイド](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [.NET SDK インストール ガイド](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [Azure Functions Core Tools インストール ガイド](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools)を参照してください。

.NET SDK 検証を無効にするには、次のコマンドを使用します。

```bash
teamsfx config set validate-dotnet-sdk off
```

.NET SDK の検証を有効にするには、次のコマンドを使用します。

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>すべてのユーザー スコープ構成を表示する

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>プロジェクト内のすべての構成を表示する

シークレットは自動的に復号化されます。

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>プロジェクト内のシークレット構成を更新する

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

TeamsFx CLI には、コラボレーション シナリオ用のコマンドが用意 `teamsFx permission` されています。

| `teamsFx permission` コマンド | 説明 |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | 指定した環境のプロジェクトに対するコラボレーターのMicrosoft 365 アカウントのアクセス許可を付与します。 |
| `teamsfx permission status` | プロジェクトのアクセス許可の状態を表示する |

### <a name="parameters-for-teamsfx-permission-grant"></a>のパラメーター `teamsfx permission grant`

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい | env 名を指定します。 |
|`--email`| はい | コラボレーターのMicrosoft 365メール アドレスを指定します。 コラボレーターのアカウントが作成者と同じテナントにあることを確認します。 |

### <a name="parameters-for-teamsfx-permission-status"></a>のパラメーター `teamsfx permission status`

| パラメーター | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい | env 名を指定します。 |
|`--list-all-collaborators` | なし | このフラグを使用すると、Teams Toolkit CLI は、このプロジェクトのすべてのコラボレーターを出力します。 |

### <a name="scenarios-for-teamsfx-permission"></a>のシナリオ `teamsfx permission`

プロジェクトの `TeamsFx` アクセス許可は次のとおりです。

#### <a name="grant-permission"></a>アクセス許可を付与する

Project作成者とコラボレーターは、コマンドを使用`teamsfx permission grant`して新しいコラボレーターをプロジェクトに追加できます。

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

必要なアクセス許可を受け取った後、プロジェクト作成者とコラボレーターは、GitHubによって新しいコラボレーターとプロジェクトを共有でき、新しいコラボレーターはMicrosoft 365アカウントのすべてのアクセス許可を持つことができます。

#### <a name="show-permission-status"></a>アクセス許可の状態を表示する

Project作成者とコラボレーターは、コマンドを使用`teamsfx permission status`して、特定の env に対するMicrosoft 365 アカウントのアクセス許可を表示できます。

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>すべてのコラボレーターを一覧表示する

作成者とコラボレーター Projectコマンドを使用`teamsfx permission status`して、特定の環境のすべてのコラボレーターを表示できます。

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>CLI での E2E コラボレーション作業フロー

プロジェクト作成者として:

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

* コラボレーターを表示するには:

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

* コラボレーターとして別のアカウントを追加する。 追加されたアカウントが同じテナントの下にあることを確認します。

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="permission":::

* プロジェクトをGitHubにプッシュするには

Projectコラボレーターとして:

* GitHubからプロジェクトを複製します。
* Microsoft 365 アカウントにログインします。 同じMicrosoft 365 アカウントが追加されていることを確認します。

  ```bash
  teamsfx account login Microsoft 365
  ```

* すべての Azure リソースに対する共同作成者アクセス許可を持つ Azure アカウントにログインします。

  ```bash
  teamsfx account login azure
  ```

* アクセス許可の状態を確認します。 プロジェクトの所有者のアクセス許可が自分にあることがわかります。

  ```bash
  teamsfx permission status --env dev
  ```

  ![アクセス許可の状態](./images/permission-status.png)

* Tab コードを更新し、プロジェクトをリモートにデプロイします。
* リモートを起動すると、プロジェクトは正常に動作します。

## <a name="see-also"></a>関連項目

* [TeamsFx SDK for TypeScript または JavaScript](TeamsFx-SDK.md)
* [Teams Toolkit で複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams Toolkitを使用してTeamsプロジェクトで共同作業する](TeamsFx-collaboration.md)
* [Teams ツールキットの概要](teams-toolkit-fundamentals.md)
