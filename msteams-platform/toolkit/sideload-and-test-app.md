---
title: Teams 環境でのアプリのサイドロードとテスト
author: zyxiaoyuer
description: このモジュールでは、さまざまな環境でアプリをサイドロードしてテストする方法について説明します
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 721b3a30bcc8c2fa49bb06491f4ab24bbeb844fd
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833003"
---
# <a name="sideload-and-test-app-in-teams-environment"></a>Teams 環境でのアプリのサイドロードとテスト

API 接続を追加した後、Teams Toolkit ローカル環境で API 接続をテストし、アプリケーションをクラウドにデプロイできます。 CI/CD パイプラインでは、別のプラットフォームでセットアップした後、リソースをプロビジョニングしてデプロイするために Azure サービス プリンシパルを作成する必要があります。

このセクションでは、

* [ローカル環境での API 接続のテスト](#test-api-connection-in-local-environment)
* [アプリケーションを Azure にデプロイする](#deploy-your-application-to-azure)
* [CI/CD リソースのプロビジョニングとデプロイ](#provision-and-deploy-cicd-resources)

## <a name="test-api-connection-in-local-environment"></a>ローカル環境での API 接続のテスト

次の手順は、Teams Toolkit ローカル環境での API 接続のテストに役立ちます。

 1. **npm インストールを実行する**

    または `api` フォルダーで`bot`を実行`npm install`して、追加されたパッケージをインストールします。

 2. **ローカル アプリケーション設定に API 資格情報を追加する**

    Teams Toolkit は資格情報を要求しませんが、プレースホルダーはローカル アプリケーション設定ファイルに残ります。 プレースホルダーを、API にアクセスするための適切な資格情報に置き換えます。 ローカル アプリケーション設定ファイルは、 `.env.teamsfx.local` または `api` フォルダー内の`bot`ファイルです。

 3. **API クライアントを使用して API 要求を行う**

    API へのアクセスを必要とするソース コードから API クライアントをインポートします。

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **ターゲット API への http(s) 要求を生成する (Axios を使用)**

    生成された API クライアントは Axios API クライアントです。 Axios クライアントを使用して API に要求を行います。

     > [!Note]
     > [Axios](https://www.npmjs.com/package/axios) は、http(s) 要求に役立つ一般的な nodejs パッケージです。 http(s) 要求を行う方法の詳細については、http を作成する方法の詳細については、 [Axios のサンプル ドキュメント](https://axios-http.com/docs/example) を参照してください。

## <a name="deploy-your-application-to-azure"></a>アプリケーションを Azure にデプロイする

アプリケーションを Azure にデプロイするには、適切な環境のアプリケーション設定に認証を追加する必要があります。 たとえば、API の資格情報と の資格情報が`dev``prod`異なる場合があります。 環境のニーズに基づいて、Teams Toolkit を構成します。

Teams Toolkit によってローカル環境が構成されます。 ブートストラップされたサンプル コードには、構成する必要があるアプリ設定を示すコメントが含まれています。 アプリケーション設定の詳細については、「アプリ設定の[追加](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings)」を参照してください。

## <a name="provision-and-deploy-cicd-resources"></a>CI/CD リソースのプロビジョニングとデプロイ

CI/CD 内で Azure を対象とするリソースをプロビジョニングおよび展開するには、使用する Azure サービス プリンシパルを作成する必要があります。

Azure サービス プリンシパルを作成するには、次の手順に従います。

1. Microsoft Azure Active Directory (Azure AD) アプリケーションをシングル テナントに登録します。
2. Assign a role to your Azure AD application to access your Azure subscription. The `Contributor` role is recommended.
3. 新しい Azure AD アプリケーション シークレットを作成します。

> [!TIP]
> 今後使用できるように、テナント ID、アプリケーション ID (AZURE_SERVICE_PRINCIPAL_NAME)、シークレット (AZURE_SERVICE_PRINCIPAL_PASSWORD) を保存します。

詳細については、「[Azure サービス プリンシパルのガイドライン](/azure/active-directory/develop/howto-create-service-principal-portal)」を参照してください。 サービス プリンシパルを作成する 3 つの方法を次に示します。

* [Microsoft Azure ポータル](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="see-also"></a>関連項目

[Teams ツールキットを使用して Teams アプリを公開する](publish.md)
