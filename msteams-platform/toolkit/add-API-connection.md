---
title: 既存の API にConnectする
author: MuyangAmigo
description: 既存の API への接続について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: b2dd6bfb1bc13b4d2b94ff57e2005b6450f59c23
ms.sourcegitcommit: 74623035d7c18194e339f566c820e0653bc3d8b6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656769"
---
# <a name="add-api-connection-to-teams-app"></a>Teams アプリへの API 接続の追加

Teams Toolkitは、Teams アプリケーションを構築するための既存の API にアクセスするのに役立ちます。 これらの API は、組織またはサード パーティによって開発されます。

## <a name="advantage"></a>メリット

Teams Toolkitは、これらの API にアクセスするための適切な SDK 言語がない場合に、サンプル コードをブートストラップして API にアクセスするのに役立ちます。

## <a name="connect-to-the-api"></a>API へのConnect

Teams Toolkitを使用して既存の API に接続すると、Teams Toolkitは次の関数を実行します。

* 下またはフォルダーに `./bot` サンプル コードを `./api` 生成する
* パッケージへの参照を `@microsoft/teamsfx` 追加する `package.json`
* ローカル デバッグを構成する API の  `.env.teamsfx.local` アプリケーション設定を追加する

### <a name="connect-to-api-in-visual-studio-code"></a>Visual Studio Code で API にConnectする

* Visual Studio Code のTeams Toolkitを使用して API 接続を追加できます。

    1. Microsoft Visual Studio Code を開きます。
    2. 左側のナビゲーション バー Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="API アイコン":::を選択します。
    3. **[開発**] で [**機能の追加]** を選択します。

        :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="API の機能の追加":::

       * コマンド パレットを開き、「**クラウド リソースの追加」Teams** 入力することもできます。

    4. ポップアップから、Teams アプリ プロジェクトに追加する **API 接続** を選択します。

        :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-select-features.png" alt-text="api select features":::

    5. **[OK]** をクリックします。

    6. API のエンドポイントを入力します。 プロジェクトのローカル アプリケーション設定に追加され、API 要求のベース URL です。

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-endpoint.png" alt-text="api エンドポイント":::

         > [!NOTE]
         > エンドポイントが有効な http URL であることを確認します。

    7. API にアクセスするコンポーネントを選択します。

    8. **[OK]** をクリックします。

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-invoke.png" alt-text="api invoke":::

    9. API のエイリアスを入力します。 エイリアスは、プロジェクトのローカル アプリケーション設定に追加される API のアプリケーション設定名を生成します。

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-alias.png" alt-text="api エイリアス":::

    10. API 認証 **の種類** から、API 要求に必要な認証を選択します。 適切なサンプル コードが生成され、選択した内容に基づいて対応するローカル アプリケーション設定が追加されます。

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-auth.png" alt-text="api auth":::

         > [!NOTE]
         > 選択した認証の種類に基づいて、追加の構成が必要です。

### <a name="api-connection-in-teamsfx-cli"></a>TeamsFx CLI での API 接続

この機能の基本コマンドは `teamsfx add api-connection [authentication type]`. 次の表に、さまざまな認証の種類とそれに対応するサンプル コマンドの一覧を示します。

 > [!Tip]
 > ヘルプ ドキュメントを取得するために使用 `teamsfx add api-connection [authentication type] -h` できます。

   |**認証の種類**|**サンプル コマンド**|
   |-----------------------|------------------|
   |基本|teamsfx add api-connection basic --endpoint <https://example.com> --component bot --alias example --user-name exampleuser --interactive false|
   |API キー|teamsfx add api-connection apikey --endpoint <https://example.com> --component bot --alias example --key-location header --key-name example-key-name --interactive false|
   |Azure AD|teamsfx add api-connection aad --endpoint <https://example.com> --component bot --alias example --app-type custom --tenant-id your_tenant_id --app-id your_app_id --interactive false|
   |証明 書|teamsfx add api-connection cert --endpoint <https://example.com> --component bot --alias example --interactive false|
   |カスタム|teamsfx add api-connection custom --endpoint <https://example.com> --component bot --alias example --interactive false|

## <a name="understand-toolkit-updates-to-your-project"></a>プロジェクトの更新Toolkit理解する

 Teams Toolkitは、`bot`選択した内容に基づいて変更または`api`フォルダーを変更します。

1. ファイルを生成 `{your_api_alias}.js/ts` します。 このファイルは、API の API クライアントを初期化し、API クライアントをエクスポートします。

2. パッケージを `package.json`.`@microsoft/teamsfx` このパッケージは、一般的な API 認証方法のサポートを提供します。

3. 環境変数を `.env.teamsfx.local`. これらは、選択した認証の種類の構成です。 生成されたコードは、環境変数から値を読み取ります。

## <a name="test-api-connection-in-local-environment"></a>ローカル環境で API 接続をテストする

次の手順は、Teams Toolkitローカル環境で API 接続をテストするのに役立ちます。

 1. **npmインストールを実行する**

    下または`api`フォルダーで`bot`実行`npm install`して、追加されたパッケージをインストールします。

 2. **API 資格情報をローカル アプリケーション設定に追加する**

    Teams Toolkitは資格情報を要求しませんが、ローカル アプリケーション設定ファイルにプレースホルダーを残します。 プレースホルダーを API にアクセスするための適切な資格情報に置き換えます。 ローカル アプリケーション設定ファイルは、`.env.teamsfx.local`フォルダー内の`bot``api`ファイルです。

 3. **API クライアントを使用して API 要求を行う**

    API へのアクセスが必要なソース コードから API クライアントをインポートします。

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **ターゲット API に対する http 要求を生成する (Axios を使用)**

    生成された API クライアントは Axios API クライアントです。 Axios クライアントを使用して API に要求を行います。

     > [!Note]
     >[Axios](https://www.npmjs.com/package/axios) は、http 要求に役立つ一般的な nodejs パッケージです。 http 要求を行う方法の詳細については、 [axios のサンプル ドキュメント](https://axios-http.com/docs/example) を参照して、http を作成する方法を確認してください。

## <a name="deploy-your-application-to-azure"></a>アプリケーションを Azure にデプロイする

Azure にアプリケーションをデプロイするには、適切な環境のアプリケーション設定に認証を追加する必要があります。 たとえば、API の資格情報 `dev` が異なる場合があります `prod`。 環境のニーズに基づいて、Teams Toolkitを構成します。

Teams Toolkitローカル環境を構成します。 ブートストラップされたサンプル コードには、構成する必要があるアプリ設定を示すコメントが含まれています。 アプリケーション設定の詳細については、「アプリ設定の [追加](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings)」を参照してください。

## <a name="advanced-scenarios"></a>高度なシナリオ

  次のセクションでは、高度なシナリオについて説明します。

<br>

<details>
<summary><b>カスタム認証プロバイダー</b></summary>

パッケージに含まれる`@microsoft/teamsfx`認証プロバイダーに加えて、インターフェイスを実装して関数で`createApiClient(..)`使用するカスタマイズされた認証プロバイダーを実装`AuthProvider`することもできます。

```Bash
import { AuthProvider } from '@microsoft/teamsfx'

class CustomAuthProvider implements AuthProvider {
    constructor() {
        // You can add necessary parameters for your customized logic in constructor
    }

    AddAuthenticationInfo: (config: AxiosRequestConfig) => Promise<AxiosRequestConfig> = async (
        config
    ) => {
        /*
        * The config parameter contains all the request information and can be updated to include extra authentication info.
        * Refer https://axios-http.com/docs/req_config for detailed document for the config object.
        * 
        * Add your customized logic that returns updated config
        */
    };
}
```
</details>
<details>
<summary><b>Azure AD アクセス許可の API にConnectする</b></summary>
Azure AD では、一部のサービスが認証されます。 次の一覧は、API アクセス許可を構成するためにこれらのサービスにアクセスするのに役立ちます。

* [Access Control リスト (ACL) を使用する](#access-control-lists-acls)
* [Azure AD アプリケーションのアクセス許可を使用する](#azure-ad-application-permissions)

API の適切なリソース スコープを持つトークンを取得する方法は、API の実装によって異なります。

次の手順に従って、次の API にアクセスできます。

#### <a name="access-control-lists-acls"></a>Access Control リスト (ACL)

   1. プロジェクトのクラウド環境でローカル デバッグを開始します。 Teams アプリケーションの Azure AD アプリケーション登録が作成されます。
  
   2. を開 `.fx/states/state.{env}.json`き、under プロパティの値を `clientId` メモします `fx-resource-aad-app-for-teams` 。

   3. API サービスで ACL を構成するクライアント ID を API プロバイダーに指定します。

#### <a name="azure-ad-application-permissions"></a>Azure AD アプリケーションのアクセス許可

  1. 次のコンテンツを開 `templates/appPackage/aad.template.json` いてプロパティに `requiredResourceAccess` 追加します。

```JSON
 {
     "resourceAppId": "The AAD App Id for the service providing the API you are connecting to",
     "resourceAccess": [
         {
             "id": "Target API's application permission Id",
             "type": "Role"
         }
     ]
 }
```

   2. プロジェクトのクラウド環境でローカル デバッグを開始します。 Teams アプリケーションの Azure AD アプリケーション登録が作成されます。

   3. プロパティの下の`clientId`値を開`.fx/states/state.{env}.json`いてメモします`fx-resource-aad-app-for-teams`。 アプリケーション クライアント ID です。

   4. 必要なアプリケーションのアクセス許可に管理者の同意を付与する方法の詳細については、「 [管理者の同意を付与](/azure/active-directory/manage-apps/grant-admin-consent#grant-admin-consent-in-app-registrations)する」を参照してください。

        > [!NOTE]
        > アプリケーションのアクセス許可の場合は、クライアント ID を使用します。
</details>

## <a name="see-also"></a>関連項目

* [Teams ツールキットを使用して Teams アプリを公開する](publish.md)
