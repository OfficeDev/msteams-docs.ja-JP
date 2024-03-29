---
title: 既存のサード パーティ API を統合する
author: MuyangAmigo
description: この記事では、ツールキットが既存の API へのサンプル アクセスをブートストラップする方法について説明します。 さまざまな認証の種類の一覧を提供します。
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: 6377f7d8a38054dacca76c0f87e39e51f466d925
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833143"
---
# <a name="integrate-existing-third-party-apis"></a>既存のサード パーティ API を統合する

Teams Toolkit は、Teams アプリケーションを構築するための既存の API にアクセスするのに役立ちます。 これらの API は、組織またはサード パーティによって開発されます。 Teams Toolkit を使用して既存の API に接続すると、Teams Toolkit は次の機能を実行します。

* または フォルダーの下にサンプル コードを`./bot``./api`生成します。
* パッケージへの参照を に `@microsoft/teamsfx` 追加します `package.json`。
* で、ローカル デバッグを構成する API の  `.env.teamsfx.local` アプリケーション設定を追加します。

## <a name="steps-to-connect-to-api"></a>API に接続する手順

Visual Studio Code と CLI コマンドを使用して API 接続を追加できます。

### <a name="add-api-connection-using-visual-studio-code"></a>Visual Studio Code を使用して API 接続を追加する

次の手順は、Visual Studio Code を使用して API 接続を追加するのに役立ちます。

1. Microsoft Visual Studio Code を開きます。
2. Visual Studio Code ツール バーから [Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="api] アイコン"::: を選択します。
3. [**開発**] で [**機能の追加] を** 選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="api add features":::

    * コマンド パレットを開き、「 **Teams: クラウド リソースの追加」** と入力することもできます。

4. ポップアップから、Teams アプリ プロジェクトに追加する **API 接続** を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-select-features.png" alt-text="api select features":::

5. **[OK]** をクリックします。

6. API のエンドポイントを入力します。 プロジェクトのローカル アプリケーション設定に追加され、API 要求のベース URL になります。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-endpoint.png" alt-text="api エンドポイント":::

     > [!NOTE]
     > エンドポイントが有効な http(s) URL であることを確認します。

7. API にアクセスするコンポーネントを選択します。

8. **[OK]** をクリックします。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-invoke.png" alt-text="api invoke":::

9. API のエイリアスを入力します。 エイリアスは、プロジェクトのローカル アプリケーション設定に追加される API のアプリケーション設定名を生成します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-alias.png" alt-text="api エイリアス":::

10. API 認証の種類から API 要求に必要な認証を選択 **します**。 適切なサンプル コードが生成され、選択内容に基づいて対応するローカル アプリケーション設定が追加されます。

     :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/myAPI connection.png" alt-text="api auth":::

     選択した認証の種類に基づいて、追加の構成を完了するには、次の手順が必要です

# <a name="basic"></a>[基本](#tab/basic)

* 基本認証のユーザー名を入力します。

  これで、サンプル コードが生成され、bot\myAPI.jsで API を呼び出すようになりました。

# <a name="certification"></a>[証明](#tab/certification)

   これで、サンプル コードが生成され、bot\myAPI.jsで API を呼び出すようになりました。

# <a name="azure-active-directory"></a>[Azure Active Directory](#tab/AAD)

  これで、サンプル コードが生成され、bot\myAPI.jsで API を呼び出すようになりました。

# <a name="api-key"></a>[API キー](#tab/apikey)

* 要求で必要な API キーの位置を選択します。

* API キー名を入力します。

  これで、サンプル コードが生成され、bot\myAPI.jsで API を呼び出すようになりました。

# <a name="custom-auth-implementation"></a>[カスタム認証の実装](#tab/CustomAuthImplementation)

  これで、サンプル コードが生成され、bot\myAPI.jsで API を呼び出すようになりました。

---

## <a name="add-api-connection-using-cli"></a>CLI を使用して API 接続を追加する

この機能の基本コマンドは です `teamsfx add api-connection [authentication type]`。 次の表に、さまざまな認証の種類とそれに対応するサンプル コマンドの一覧を示します。

 > [!TIP]
 > を使用 `teamsfx add api-connection [authentication type] -h` して、ヘルプ ドキュメントを取得できます。

   |**認証の種類**|**サンプル コマンド**|
   |-----------------------|------------------|
   |基本|teamsfx add api-connection basic--endpoint <https://example.com> --component bot--alias example--user-name exampleuser--interactive false|
   |API キー|teamsfx add api-connection apikey--endpoint <https://example.com> --component bot-alias example--key-location header--key-name example-key-name--interactive false|
   |Azure AD|teamsfx add api-connection aad--endpoint <https://example.com> --component bot--alias example--app-type custom--tenant-id your_tenant_id--app-id your_app_id--interactive false|
   |証明書|teamsfx add api-connection cert--endpoint <https://example.com> --component bot--alias example-interactive false|
   |Custom|teamsfx add api-connection custom--endpoint <https://example.com> --component bot--alias example--interactive false|

---

## <a name="directory-structure-updates-to-your-project"></a>プロジェクトのディレクトリ構造の更新

 Teams Toolkit では、選択内容 `bot` に基づいてフォルダーが変更されます `api` 。

1. ファイルを生成 `{your_api_alias}.js/ts` します。 このファイルは、API の API クライアントを初期化し、API クライアントをエクスポートします。

2. にパッケージを追加 `@microsoft/teamsfx` します `package.json`。 パッケージは、一般的な API 認証方法のサポートを提供します。

3. 環境変数を に追加します `.env.teamsfx.local`。 選択した認証の種類の構成です。 生成されたコードは、環境変数から値を読み取ります。

## <a name="advantages"></a>メリット

Teams Toolkit は、これらの API にアクセスするための適切な言語 SDK がない場合に、サンプル コードをブートストラップして API にアクセスするのに役立ちます。

## <a name="see-also"></a>関連項目

[Teams ツールキットを使用して Teams アプリを公開する](publish.md)
