---
title: Teams 環境でのアプリのサイドロードとテスト
author: zyxiaoyuer
description: このモジュールでは、さまざまな環境でアプリをサイドロードしてテストする方法について説明します
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: ee1d3ee3a4f545a6c988c421fb18626a4a7276b7
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617217"
---
# <a name="sideload-and-test-app-in-teams-environment"></a>Teams 環境でのアプリのサイドロードとテスト

API 接続を追加した後、Teams Toolkit ローカル環境で API 接続をテストし、アプリケーションをクラウドにデプロイできます。 CI/CD パイプラインでは、異なるプラットフォームでセットアップした後、リソースをプロビジョニングおよびデプロイするために Azure サービス プリンシパルを作成する必要があります。

このセクションでは、次のことを学習します。

* [ローカル環境で API 接続をテストする](#test-api-connection-in-local-environment)
* [アプリケーションを Azure にデプロイする](#deploy-your-application-to-azure)
* [CI/CD リソースのプロビジョニングとデプロイ](#provision-and-deploy-cicd-resources)

## <a name="test-api-connection-in-local-environment"></a>ローカル環境で API 接続をテストする

次の手順は、Teams Toolkit ローカル環境で API 接続をテストするのに役立ちます。

 1. **npm install を実行する**

    下または`api`フォルダーで`bot`実行`npm install`して、追加されたパッケージをインストールします。

 2. **API 資格情報をローカル アプリケーション設定に追加する**

    Teams Toolkit は資格情報を要求しませんが、ローカル アプリケーション設定ファイルにプレースホルダーを残します。 プレースホルダーを API にアクセスするための適切な資格情報に置き換えます。 ローカル アプリケーション設定ファイルは、`.env.teamsfx.local`フォルダー内の`bot``api`ファイルです。

 3. **API クライアントを使用して API 要求を行う**

    API へのアクセスが必要なソース コードから API クライアントをインポートします。

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **ターゲット API に対する http 要求を生成する (Axios を使用)**

    生成された API クライアントは Axios API クライアントです。 Axios クライアントを使用して API に要求を行います。

     > [!Note]
     > [Axios](https://www.npmjs.com/package/axios) は、http 要求に役立つ一般的な nodejs パッケージです。 http 要求を行う方法の詳細については、 [axios のサンプル ドキュメント](https://axios-http.com/docs/example) を参照して、http を作成する方法を確認してください。

## <a name="deploy-your-application-to-azure"></a>アプリケーションを Azure にデプロイする

Azure にアプリケーションをデプロイするには、適切な環境のアプリケーション設定に認証を追加する必要があります。 たとえば、API の資格情報 `dev` が異なる場合があります `prod`。 環境のニーズに基づいて、Teams Toolkit を構成します。

Teams Toolkit では、ローカル環境が構成されます。 ブートストラップされたサンプル コードには、構成する必要があるアプリ設定を示すコメントが含まれています。 アプリケーション設定の詳細については、「アプリ設定の追加」を参照してください [。](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings)

## <a name="provision-and-deploy-cicd-resources"></a>CI/CD リソースのプロビジョニングとデプロイ

CI/CD 内で Azure を対象とするリソースをプロビジョニングおよび展開するには、使用する Azure サービス プリンシパルを作成する必要があります。

Azure サービス プリンシパルを作成するには、次の手順に従います。

1. Microsoft Azure Active Directory (Azure AD) アプリケーションをシングル テナントに登録します。
2. Azure AD アプリケーションに、Azure サブスクリプションにアクセスするためのロールを割り当てます。`Contributor` ロールをお勧めします。
3. 新しい Azure AD アプリケーション シークレットを作成します。

> [!TIP]
> 今後使用できるように、テナント ID、アプリケーション ID (AZURE_SERVICE_PRINCIPAL_NAME)、シークレット (AZURE_SERVICE_PRINCIPAL_PASSWORD) を保存します。

詳細については、「[Azure サービス プリンシパルのガイドライン](/azure/active-directory/develop/howto-create-service-principal-portal)」を参照してください。 サービス プリンシパルを作成する 3 つの方法を次に示します。

* [Microsoft Azure ポータル](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="see-also"></a>関連項目

* [Teams ツールキットを使用して Teams アプリを公開する](publish.md)
