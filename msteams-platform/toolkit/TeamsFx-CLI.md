---
title: TeamsFx コマンド ライン インターフェイス
author: MuyangAmigo
description: TeamsFx コマンド ライン インターフェイスについて説明します
ms.author: zhany
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ab9bad973d337d783c1de70c2ad8575a67d6cb6e
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111438"
---
# <a name="teamsfx-library"></a>TeamsFx ライブラリ

Microsoft Teams Framework (TeamsFx) は、一般的な機能と統合パターン (Microsoft Identity への簡単なアクセスなど) をカプセル化するライブラリです。 構成なしで Microsoft Teams 用のアプリを構築できます。

TeamsFx の主な機能の一覧を次に示します。

* **TeamsFx コラボレーション**: 開発者とプロジェクト所有者が TeamsFx プロジェクトに他のコラボレーターを招待できるようにします。 TeamsFx プロジェクトをデバッグおよび展開するために共同作業を行うことができます。

* **TeamsFx CLI**: Teams アプリケーションの開発を高速化します。 また、自動化用のスクリプトに CLI を統合できる CI/CD シナリオも可能になります。

* **TeamsFx SDK**: TeamsFx ソフトウェア開発キット (SDK) は、Teams 開発者向けに調整されたクライアントとサーバー側の両方のコードに対する単純な認証をカプセル化する主要な TeamsFx コード ライブラリです。

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
| `teamsfx account`| クラウド サービス アカウントを管理します。 サポートされているクラウド サービスは、'Azure' と 'Microsoft 365' です。 |
| `teamsfx env` | 環境を管理する。 |
| `teamsfx capability`| 現在のアプリケーションに新しい機能を追加します。|
| `teamsfx resource`  | 現在のアプリケーションのリソースを管理します。|
| `teamsfx provision` | 現在のアプリケーションでクラウド リソースをプロビジョニングします。|
| `teamsfx deploy` | 現在のアプリケーションをデプロイします。  |
| `teamsfx package` | Teams アプリを発行用のパッケージにビルドします。|
| `teamsfx validate` | 現在のアプリケーションを検証します。|
| `teamsfx publish` | アプリを Teams に公開する。|
| `teamsfx preview` | 現在のアプリケーションをプレビューします。 |
| `teamsfx config`  | 構成データを管理します。 |
| `teamsfx permission`| 同じプロジェクトで他の開発者と共同作業を行います。|

## `teamsfx new`

既定では、`teamsfx new` は対話型モードになり、新しい Teams アプリケーションを作成するプロセスをガイドします。 `--interactive` フラグを `false` に設定して、非対話型モードで作業することもできます。

| `teamsFx new`コマンド | 説明 |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | 既存のテンプレートからアプリを作成する |
| `teamsfx new template list`     | 使用可能なすべてのテンプレートを一覧表示する |

### <a name="parameters-for-teamsfx-new"></a>`teamsfx new` のパラメーター

| パラメーター | 要件 | 説明 |
|:---------------- |:-------------|:-------------|
|`--app-name` | はい| Teams アプリケーションの名前です。|
|`--interactive`| いいえ | オプションを対話形式で選択します。 オプションは `true` と `false` で、既定値は `true` です。|
|`--capabilities`| いいえ| Teams アプリケーション機能を選択します。複数のオプションは `tab`、`bot`、`messaging-extension`、および `tab-spfx` です。 既定値は `tab` です。|
|`--programming-language`| いいえ| プロジェクトのプログラミング言語です。 オプションは `javascript` または `typescript` で、デフォルト値は `javascript` です。|
|`--folder`| いいえ | プロジェクト ディレクトリ。 このディレクトリの下に、アプリ名を持つサブ フォルダーが作成されます。 既定値は `./` です。|
|`--spfx-framework-type`| なし| `Tab(SPfx)` 機能が選択されている場合に適用されます。 フロントエンド フレームワーク。 オプションは `none` と `react` で、既定値は `none` です。|
|`--spfx-web part-name`| いいえ | `Tab(SPfx)` 機能が選択されている場合に適用されます。 既定値は "helloworld" です。|
|`--spfx-web part-desp`| なし | `Tab(SPfx)` 機能が選択されている場合に適用されます。 既定値は "helloworld description" です。 |
|`--azure-resources`| なし| `tab` 機能が含まれている場合に適用されます。 Azure リソースをプロジェクトに追加します。 複数のオプションは `sql` (Azure SQL Database) と `function` (Azure Functions) です。 |

### <a name="scenarios-for-teamsfx-new"></a>`teamsfx new` のシナリオ

対話型モードを使用して Teams アプリを作成できます。`teamsfx new` すべてのパラメーターを制御するシナリオは次のとおりです。

#### <a name="tab-app-hosted-on-spfx-using-react"></a>React を使用して SPFx でホストされているタブ アプリ

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>タブ、ボット機能、Azure Functions を備えた JavaScript の Teams アプリ

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>AzureFunctions と Azure SQL を備えた Teams タブ アプリ

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

クラウド サービス アカウントを管理します。 サポートされているクラウド サービスは `Azure` と `Microsoft 365` です。

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

### <a name="scenarios-for-teamsfx-env"></a>`teamsfx env` のシナリオ

`teamsfx env` のシナリオは次のとおりです。

#### <a name="create-a-new-environment"></a>新しい環境を作成します。

既存の開発環境からコピーして新しい環境を追加します。

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

現在のアプリケーションに新しい機能を追加します。

| `teamsFx capability` コマンド  | 説明 |
|:----------------  |:-------------|
| `teamsfx capability add tab` | タブを追加する |
| `teamsfx capability add bot` | ボットを追加 |
| `teamsfx capability add messaging-extension`| messagE 拡張機能を追加する |

> [!NOTE]
> プロジェクトにボットが含まれている場合は、メッセージ拡張機能を追加できず、その逆も適用されます。 新しい Teams アプリ プロジェクトを作成するときに、ボットとメッセージの両方の拡張機能をプロジェクトに含めることができます。

## `teamsfx resource`

現在のアプリケーションのリソースを管理します。 サポート対象の `<resource-type>` は、`azure-sql`、`azure-function`、および `azure-apim` です。

| `teamsFx resource` コマンド  | 説明 |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | 現在のアプリケーションにリソースを追加します。|
| `teamsfx resource show <resource-type>`      | リソースの構成の詳細を表示します。 |
| `teamsfx resource list`      | 現在のアプリケーション内のすべてのリソースを一覧表示します。 |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>`teamsfx resource add azure-function` のパラメーター

| パラメーター  | 要件 | 説明 |
|----------------  |-------------|-------------|
|`--function-name`| はい | 関数名を指定します。 既定値は `getuserprofile` です。 |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>`teamsfx resource add azure-sql` のパラメーター

#### `--function-name`

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--function-name`| はい | 関数名を指定します。 既定値は `getuserprofile` です。 |

> [!NOTE]
> 関数名は SQL として検証され、サーバー ワークロードからアクセスする必要があります。 プロジェクトに `Azure Functions` が含まれていない場合は、作成してください。

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>`teamsfx resource add azure-apim` のパラメーター 

> [!TIP]
> これらのオプションは、既存の `APIM` インスタンスを使用しようとすると有効になります。 既定では、オプションを指定する必要はなく、`teamsfx provision` ステップ中に新しいインスタンスが作成されます。

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--subscription`| はい | Azure サブスクリプションを選択します|
|`--apim-resource-group`| はい| リソース グループの名前。 |
|`--apim-service-name`| はい | API 管理サービス インスタンスの名前。 |
|`--function-name`| はい | 関数名を指定します。 既定値は `getuserprofile` です。 |

> [!NOTE]
> `Azure API Management` は `Azure Functions` と連携する必要があります。 プロジェクトに `Azure Functions` が含まれていない場合は、プロジェクトを作成できます。

## `teamsfx provision`

現在のアプリケーションでクラウド リソースをプロビジョニングします。

### <a name="parameters-for-teamsfx-provision"></a>`teamsfx provision` のパラメーター

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい| プロジェクトの環境を選択します。 |
|`--subscription`| いいえ | Azure サブスクリプション ID を指定します。 |
|`--resource-group`| いいえ | 既存のリソース グループの名前を設定します。 |
|`--sql-admin-name`| なし | プロジェクトに SQL リソースがある場合に適用されます。 SQL の管理者名。|
|`--sql-password`| なし| プロジェクトに SQL リソースがある場合に適用されます。 SQL の管理者パスワード。|

## `teamsfx deploy`

このコマンドは、現在のアプリケーションをデプロイするために使用されます。 既定では、プロジェクト全体がデプロイされますが、部分的にデプロイすることもできます。 複数のオプションは、`frontend-hosting`、`function`、`apim`、`teamsbot`、および `spfx` です。

### <a name="parameters-for-teamsfx-deploy"></a>`teamsfx deploy` のパラメーター

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい| プロジェクトの既存の環境を選択します。 |
|`--open-api-document`| いいえ | プロジェクトに APIM リソースがある場合に適用されます。 開いている API ドキュメント ファイルパス。 |
|`--api-prefix`| なし | プロジェクトに APIM リソースがある場合に適用されます。 API 名プレフィックス。 API の既定の一意の名前は `{api-prefix}-{resource-suffix}-{api-version}` です。 |
|`--api-version`| なし | プロジェクトに APIM リソースがある場合に適用されます。 API バージョン。 |

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

### <a name="scenarios-for-teamsfx-preview"></a>`teamsfx preview` のシナリオ

#### <a name="local-preview"></a>ローカル プレビュー

依存関係:

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
> React などのバックグラウンド サービスのログは `~/.fx/cli-log/local-preview/` に保存されます。

## `teamsfx config`

ユーザー スコープまたはプロジェクト スコープのいずれかで構成データを管理します。

| `teamsfx config` コマンド  | 説明 |
|:----------------  |:-------------|
| `teamsfx config get [option]` | オプションの構成値を表示する |
| `teamsfx config set <option> <value>` | オプションの構成値を更新する |

### <a name="parameters-for-teamsfx-config"></a>`teamsfx config` のパラメーター

| パラメーター  | 要件 | 説明 |
|:----------------  |:-------------|:-------------|
|`--env`| はい | プロジェクトの既存の環境を選択します。 |
|`--folder`| いいえ | プロジェクト ディレクトリ。 これは、プロジェクトの構成を取得または設定するために使用されます。 既定値は `./` です。 |
|`--global`| いいえ | 構成に対応します。 これが true の場合、スコープはプロジェクト スコープではなくユーザー スコープに制限されます。 既定値は `false` です。 現在、サポートされているグローバル構成には、`telemetry`、`validate-dotnet-sdk`、`validate-func-core-tools`、`validate-node` が含まれます。 |

### <a name="scenerios-for-teamsfx-config"></a>`teamsfx config` のシナリオ

`.userdata` ファイルのシークレットは暗号化されており、`teamsfx config` 値を表示または更新するのに役立ちます。

#### <a name="stop-sending-telemetry-data"></a>テレメトリ データの送信を停止する

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>環境チェッカーを無効にする

Node.js、.NET SDK、および Azure Functions Core Tools の検証をオンまたはオフにするための 3 つの構成があり、それらはすべて既定で有効になっています。 依存関係の検証が不要で、自分で依存関係をインストールする場合は、構成を "オフ" に設定できます。 次のガイドを確認してください。

* [Node.js インストール ガイド](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [.NET SDK インストール ガイド](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [Azure Functions Core Tools インストール ガイド](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools)。

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

シークレットは以下では自動的に復号化されます。

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>プロジェクト内のシークレット構成を更新する

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

TeamsFx CLI は、コラボレーションシナリオ用の `teamsFx permission` コマンドを提供します。

| `teamsFx permission` コマンド | 説明 |
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

`TeamsFx` プロジェクトのアクセス許可は次のとおりです。

#### <a name="grant-permission"></a>アクセス許可の付与

プロジェクトの作成者と共同作業者は、`teamsfx permission grant` コマンドを使用して、プロジェクトに新しい共同作業者を追加できます。

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

必要なアクセス許可を受け取った後、プロジェクトの作成者と共同作業者は GitHub によって新しい共同作業者とプロジェクトを共有でき、新しい共同編集者は Microsoft 365 アカウントに対するすべてのアクセス許可を持つことができます。

#### <a name="show-permission-status"></a>アクセス許可の状態を表示する

プロジェクトの作成者と共同作業者は、`teamsfx permission status` コマンドを使用して、特定の環境に対する Microsoft 365 アカウントのアクセス許可を表示できます。

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>すべてのコラボレーターを一覧表示する

プロジェクトの作成者と共同作業者は、`teamsfx permission status` コマンドを使用して、特定の環境のすべての共同作業者を表示できます。

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

Project Collaborator として:

* GitHub からプロジェクトを複製します。
* Microsoft 365 アカウントにログインします。 同じ Microsoft 365 アカウントが追加されていることを確認します。

  ```bash
  teamsfx account login Microsoft 365
  ```

* すべてのAzureリソースに対する共同作成者のアクセス許可を使用してAzureアカウントにログインします。

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
