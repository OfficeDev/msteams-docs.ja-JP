---
title: Teams Toolkit で Azure Active Directory マニフェストを編集する
author: zyxiaoyuer
description: Teams Toolkit での Azure Active Directory アプリケーションの管理について説明します
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 0df9cc75b6a9775f9369b6a3bf8b95c35941207b
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499322"
---
# <a name="edit-azure-ad-manifest"></a>Azure AD マニフェストを編集する

[Azure Active Directory (Azure AD) マニフェスト](/azure/active-directory/develop/reference-app-manifest)には、Microsoft ID プラットフォーム内の Azure AD アプリケーション オブジェクトのすべての属性の定義が含まれています。

Teams Toolkit は、Teams アプリケーション開発ライフサイクル中にマニフェスト ファイルを信頼のソースとして使用して Azure AD アプリケーションを管理するようになりました。

このセクションでは、次の手順について説明します。

* [Azure AD マニフェスト テンプレートをカスタマイズする](#customize-azure-ad-manifest-template)
* [Azure AD マニフェスト テンプレートプレースホルダー](#azure-ad-manifest-template-placeholders)
* [コード レンズを使用して Azure AD マニフェストを作成してプレビューする](#author-and-preview-azure-ad-manifest-with-code-lens)
* [ローカル環境用に Azure AD アプリケーションの変更をデプロイする](#deploy-azure-ad-application-changes-for-local-environment)
* [リモート環境用に Azure AD アプリケーションの変更をデプロイする](#deploy-azure-ad-application-changes-for-remote-environment)
* [Azure portalで Azure AD アプリケーションを表示する](#view-azure-ad-application-on-the-azure-portal)
* [既存の Azure AD アプリケーションを使用する](#use-an-existing-azure-ad-application)
* [Teams アプリケーション開発ライフサイクルにおける Azure AD アプリケーション](#azure-ad-application-in-teams-application-development-lifecycle)

## <a name="customize-azure-ad-manifest-template"></a>Azure AD マニフェスト テンプレートをカスタマイズする

Azure AD マニフェスト テンプレートをカスタマイズして、Azure AD アプリケーションを更新できます。

1. プロジェクトで開きます `aad.template.json` 。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add template.png" alt-text="template":::

2. テンプレートを直接更新するか、 [別のファイルから値を参照します](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#Placeholders-in-AAD-manifest-template)。 ここでは、いくつかのカスタマイズ シナリオを確認できます。
  
   * [アプリケーションのアクセス許可を追加する](#add-an-application-permission)
   * [クライアント アプリケーションの事前認証](#preauthorize-a-client-application)
   * [認証応答のリダイレクト URL を更新する](#update-redirect-url-for-authentication-response)

3. [ローカル環境用に Azure AD アプリケーションの変更をデプロイ](#deploy-azure-ad-application-changes-for-local-environment)します。
  
4. [リモート環境用に Azure AD アプリケーションの変更をデプロイします](#deploy-azure-ad-application-changes-for-remote-environment)。

### <a name="add-an-application-permission"></a>アプリケーションのアクセス許可を追加する

Teams アプリケーションで追加のアクセス許可を持つ API を呼び出すより多くのアクセス許可が必要な場合は、Azure AD マニフェスト テンプレートのプロパティを更新 `requiredResourceAccess` する必要があります。 このプロパティの次の例を確認できます。

```JSON

   "requiredResourceAccess": [
    {
        "resourceAppId": "Microsoft Graph",
        "resourceAccess": [
            {
                "id": "User.Read", // For Microsoft Graph API, you can also use uuid for permission id
                "type": "Scope" // Scope is for delegated permission
            },
            {
                "id": "User.Export.All",
                "type": "Role" // Role is for application permission
            }
        ]
    },
    {
        "resourceAppId": "Office 365 SharePoint Online",
        "resourceAccess": [
            {
                "id": "AllSites.Read",
                "type": "Scope"
            }
        ]
    }
]
```

* `resourceAppId` プロパティは、さまざまな API に使用されます。 UUID `Microsoft Graph` の代わりに名前を直接入力し`Office 365``SharePoint Online`、他の API の場合は UUID を使用します。

* `resourceAccess.id` プロパティは、さまざまなアクセス許可に使用されます。 `Microsoft Graph` UUID の`Office 365 SharePoint Online`代わりにアクセス許可名を直接入力し、他の API の場合は UUID を使用します。

* `resourceAccess.type` プロパティは、委任されたアクセス許可またはアプリケーションのアクセス許可に使用されます。 `Scope` は委任されたアクセス許可を意味し、 `Role` アプリケーションのアクセス許可を意味します。

### <a name="preauthorize-a-client-application"></a>クライアント アプリケーションの事前認証

プロパティを使用 `preAuthorizedApplications` して、クライアント アプリケーションを承認して、API がアプリケーションを信頼していることを示すことができます。 クライアントが公開された API を呼び出しても、ユーザーは同意しません。 このプロパティの次の例を確認できます。

```JSON

    "preAuthorizedApplications": [
        {
            "appId": "1fec8e78-bce4-4aaf-ab1b-5451cc387264",
            "permissionIds": [
                "{{state.fx-resource-aad-app-for-teams.oauth2PermissionScopeId}}"
            ]
        }
        ...
    ]
```

`preAuthorizedApplications.appId` プロパティは、承認するアプリケーションに使用されます。 アプリケーション ID がわからない場合に、アプリケーション名のみを知っている場合は、次の手順に従ってアプリケーション ID を検索します。

1. [Azure portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)に移動し、**アプリケーション登録** を開きます。

1. **[すべてのアプリケーション**] を選択し、アプリケーション名を検索します。

1. アプリケーション名を選択し、概要ページからアプリケーション ID を取得します。

### <a name="update-redirect-url-for-authentication-response"></a>認証応答のリダイレクト URL を更新する

  リダイレクト URL は、認証に成功した後にトークンなどの認証応答を返す際に使用されます。 プロパティ `replyUrlsWithType`を使用してリダイレクト URL をカスタマイズできます。 たとえば、リダイレクト URL として追加 `https://www.examples.com/auth-end.html` するには、次の例のように追加します。

``` JSON
"replyUrlsWithType": [
    ...
    {
        "url": "https://www.examples.com/auth-end.html",
        "type": "Spa"
    }
]
```

## <a name="azure-ad-manifest-template-placeholders"></a>Azure AD マニフェスト テンプレートプレースホルダー

Azure AD マニフェスト ファイルには、{{{..}} のプレースホルダー引数が含まれています 異なる環境のビルド中に置き換えられるステートメント。 プレースホルダー引数を使用して、構成ファイル、状態ファイル、および環境変数への参照を作成できます。

### <a name="reference-state-file-values-in-azure-ad-manifest-template"></a>Azure AD マニフェスト テンプレートの参照状態ファイルの値

状態ファイルは (xxx は異なる環境を表します) にあります `.fx\states\state.xxx.json` 。 次の例は、一般的な状態ファイルを示しています。

``` JSON
{
    "solution": {
        "teamsAppTenantId": "uuid",
        ...
    },
    "fx-resource-aad-app-for-teams": {
        "applicationIdUris": "api://xxx.com/uuid",
        ...
    }
    ...
}
```

このプレースホルダー引数は、Azure AD マニフェストで使用できます。`{{state.fx-resource-aad-app-for-teams.applicationIdUris}}`プロパティの`fx-resource-aad-app-for-teams`値を指定`applicationIdUris`できます。

### <a name="reference-config-file-values-in-azure-ad-manifest-template"></a>Azure AD マニフェスト テンプレートの参照構成ファイルの値

構成ファイルは (xxx は異なる環境を表します) にあります `.fx\configs\config.xxx.json` 。 次の例は、構成ファイルを示しています。

``` JSON
{
  "$schema": "https://aka.ms/teamsfx-env-config-schema",
  "description": "description.",
  "manifest": {
    "appName": {
      "short": "app",
      "full": "Full name for app"
    }
  }
}
```

値を参照`short`するには、Azure AD マニフェスト`{{config.manifest.appName.short}}`でプレースホルダー引数を使用できます。

### <a name="reference-environment-variable-in-azure-ad-manifest-template"></a>Azure AD マニフェスト テンプレートの参照環境変数

Azure AD マニフェスト テンプレートの値をハードコーディングしたくない場合があります。 たとえば、値がシークレットの場合などです。 Azure AD マニフェスト テンプレート ファイルでは、参照環境変数の値がサポートされています。 パラメーター値の構文 `{{env.YOUR_ENV_VARIABLE_NAME}}` を使用して、現在の環境変数の値を解決するようにツールに指示できます。

## <a name="author-and-preview-azure-ad-manifest-with-code-lens"></a>コード レンズを使用して Azure AD マニフェストを作成してプレビューする

Azure AD マニフェスト テンプレート ファイルには、確認と編集を行うコード レンズがあります。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/preview view.png" alt-text="previewview":::

### <a name="azure-ad-manifest-template-file"></a>Azure AD マニフェスト テンプレート ファイル

Azure AD マニフェスト テンプレート ファイルの先頭にプレビュー コード レンズがあります。 選択した環境に基づいて Azure AD マニフェストを生成するコード レンズを選択します。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add codelens.png" alt-text="addcodelens":::

### <a name="placeholder-argument-code-lens"></a>プレースホルダー引数コード レンズ

プレースホルダー引数コード レンズは、ローカル デバッグと開発環境の値をすばやく確認するのに役立ちます。 プレースホルダー引数にマウス ポインターを置くと、すべての環境の値のツールヒント ボックスが表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add arguments.png" alt-text="addarguments":::

### <a name="required-resource-access-code-lens"></a>必要なリソース アクセス コード レンズ

これは、プロパティ内`requiredResourceAccess`の ID が UUID のみをサポートする`resourceAppId`公式[の Azure AD マニフェスト スキーマ](/azure/active-directory/develop/reference-app-manifest)とは`resourceAccess`異なります。 Teams Toolkit の Azure AD マニフェスト テンプレートでは、ユーザーが読み取り可能な文字列と`Microsoft Graph``Office 365 SharePoint Online`アクセス許可もサポートされています。 UUID を入力すると、コード レンズはユーザーが読み取り可能な文字列を示し、それ以外の場合は UUID を示します。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add resource.png" alt-text="Addresource":::

### <a name="pre-authorized-applications-code-lens"></a>事前に承認されたアプリケーション コード レンズ

コード レンズは、プロパティの事前に承認されたアプリケーション ID のアプリケーション名を `preAuthorizedApplications` 示します。

## <a name="deploy-azure-ad-application-changes-for-local-environment"></a>ローカル環境用に Azure AD アプリケーションの変更をデプロイする

1. でコード レンズを`aad.template.json`選択します`Preview`。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy1.png" alt-text="deploy1":::

2. **ローカル環境を** 選択します。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy2.png" alt-text="deploy2":::

3. でコード レンズを`aad.local.json`選択します`Deploy Azure AD Manifest`。

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy3.png" alt-text="deploy3":::

4. ローカル環境で使用される Azure AD アプリケーションの変更がデプロイされます。
  
## <a name="deploy-azure-ad-application-changes-for-remote-environment"></a>リモート環境用に Azure AD アプリケーションの変更をデプロイする

1. コマンド パレットを開き、次を選択します `Teams: Deploy Azure Active Directory application manifest`。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy4.png" alt-text="deploy4":::

2. また、右クリックして `aad.template.json` コンテキスト メニューから選択 `Deploy Azure Active Directory application manifest` することもできます。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy5.png" alt-text="deploy5":::

## <a name="view-azure-ad-application-on-the-azure-portal"></a>Azure portalで Azure AD アプリケーションを表示する

1. プロパティ内の () ファイルから `state.xxx.json` Azure AD アプリケーション クライアント ID をコピーします `fx-resource-aad-app-for-teams` 。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view1.png" alt-text="view1":::

   > [!NOTE]
   > クライアント ID の xxx は、Azure AD アプリケーションをデプロイした環境名を示します。

2. [Azure portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)に移動し、Microsoft 365 アカウントにサインインします。
  
   > [!NOTE]
   > Teams アプリケーションと M365 アカウントのログイン資格情報が同じであることを確認します。

3. [[アプリの登録] ページを](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)開き、前にコピーしたクライアント ID を使用して Azure AD アプリケーションを検索します。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view2.png" alt-text="view2":::

4. 検索結果から Azure AD アプリケーションを選択して、詳細情報を表示します。
  
5. Azure AD アプリ情報ページで、メニューを `Manifest` 選択して、このアプリケーションのマニフェストを表示します。 マニフェストのスキーマは、ファイル内 `aad.template.json` のスキーマと同じです。 マニフェストの詳細については、「 [Azure Active Directory アプリケーション マニフェスト」を](/azure/active-directory/develop/reference-app-manifest)参照してください。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view3.png" alt-text="view3":::

6. **[その他のメニュー] を** 選択すると、ポータルを使用して Azure AD アプリケーションを表示または構成できます。
  
## <a name="use-an-existing-azure-ad-application"></a>既存の Azure AD アプリケーションを使用する

Teams プロジェクトに既存の Azure AD アプリケーションを使用できます。詳細については、「Teams [アプリケーションに既存の Azure AD アプリケーションを使用する](https://github.com/OfficeDev/TeamsFx/wiki/Customize-provision-behaviors#use-an-existing-aad-app-for-your-teams-app)」を参照してください。

## <a name="azure-ad-application-in-teams-application-development-lifecycle"></a>Teams アプリケーション開発ライフサイクルにおける Azure AD アプリケーション

Teams アプリケーション開発ライフサイクルのさまざまな段階で、Azure AD アプリケーションと対話する必要があります。

1. **プロジェクトを作成するには**

      既定で SSO のサポートが付属する Teams Toolkit を使用してプロジェクトを作成できます (例:`SSO-enabled tab` 新しいアプリの作成の詳細については、「 [Teams Toolkit を使用して新しい Teams アプリケーションを作成する」を](create-new-project.md)参照してください。 Azure AD マニフェスト ファイルが自動的に作成されます `templates\appPackage\aad.template.json`。 Teams Toolkit は、ローカル開発中またはクラウドへのアプリケーションの移動中に、Azure AD アプリケーションを作成または更新します。

2. **ボットまたはタブに SSO を追加するには**

      SSO が組み込まれずに Teams アプリケーションを作成すると、Teams Toolkit はプロジェクトの SSO を追加するのに段階的に役立ちます。 その結果、Azure AD マニフェスト ファイルが自動的に作成されます `templates\appPackage\aad.template.json`。

      Teams Toolkit は、次のローカル デバッグ セッション中、またはアプリケーションをクラウドに移動するときに、Azure AD アプリケーションを作成または更新します。

3. **ローカルでビルドするには**

    Teams Toolkit は、ローカル開発中または F5 と呼ばれる場合に、次の機能を実行します。

    * ファイルを `state.local.json` 読み取って、既存の Azure AD アプリケーションを見つけます。 Azure AD アプリケーションが既に存在する場合、Teams Toolkit は既存の Azure AD アプリケーションを再利用します。 それ以外の場合は、ファイルを使用して新しいアプリケーションを作成する `aad.template.json` 必要があります。

    * マニフェスト ファイルを使用した新しい Azure AD アプリケーションの作成時に、より多くのコンテキストを必要とするマニフェスト ファイル内の一部のプロパティ (ローカル デバッグ エンドポイントを必要とする replyUrls プロパティなど) を最初に無視します。

    * ローカル開発環境が正常に開始されると、作成ステージ中に使用できない Azure AD アプリケーションの identifierUris、replyUrls、およびその他のプロパティがそれに応じて更新されます。

    * Azure AD アプリケーションに対して行った変更は、次のローカル デバッグ セッション中に読み込まれます。 [Azure AD アプリケーションの変更](https://github.com/OfficeDev/TeamsFx/wiki/)を手動で適用する Azure AD アプリケーションの変更を確認できます。

4. **クラウド リソースをプロビジョニングするには**

      クラウド リソースをプロビジョニングし、アプリケーションをクラウドに移行するときにアプリケーションをデプロイする必要があります。 Teams Toolkit は、ローカル開発などの段階で次の作業を行います。

      * ファイルを `state.{env}.json` 読み取って、既存の Azure AD アプリケーションを見つけます。 Azure AD アプリケーションが既に存在する場合、Teams Toolkit は既存の Azure AD アプリケーションを再利用します。 それ以外の場合は、ファイルを使用して新しいアプリケーションを作成する `aad.template.json` 必要があります。

      * マニフェスト ファイルを使用して新しい Azure AD アプリケーションを作成するときに、最初に、より多くのコンテキストを必要とするマニフェスト ファイルの一部のプロパティ (replyUrls プロパティにはフロントエンドまたはボット エンドポイントが必要) が無視されます。

      * 他のリソースのプロビジョニングが完了すると、Azure AD アプリケーションの identifierUris と replyUrl が適切なエンドポイントに従って更新されます。

5. **アプリケーションをビルドするには**

    * クラウド コマンドにデプロイすると、プロビジョニングされたリソースにアプリケーションがデプロイされます。 加えた Azure AD アプリケーションの変更のデプロイは含まれません。

    * リモート環境用に [Azure AD アプリケーションの変更をデプロイして、リモート環境用](#deploy-azure-ad-application-changes-for-remote-environment) に Azure AD アプリケーションの変更をデプロイする方法を確認できます。

    * Teams Toolkit は、Azure AD マニフェスト テンプレート ファイルに従って Azure AD アプリケーションを更新します。

## <a name="limitations"></a>制限事項

1. Teams Toolkit 拡張機能では、Azure AD マニフェスト スキーマに一覧表示されているすべてのプロパティがサポートされているわけではありません。
  
      次の表に、Teams Toolkit 拡張機能でサポートされていないプロパティを示します。

      |**サポートされていないプロパティ**|**理由**|
      |-----------|----------|
      |passwordCredentials|マニフェストでは許可されません|
      |createdDateTime|読み取り専用で変更できない|
      |logoUrl|読み取り専用で変更できない|
      |publisherDomain|読み取り専用で変更できない|
      |oauth2RequirePostResponse|Graph APIに存在しない|
      |oauth2AllowUrlPathMatching|Graph APIに存在しない|
      |samlMetadataUrl|Graph APIに存在しない|
      |orgRestrictions|Graph APIに存在しない|
      |認定|Graph APIに存在しない|

2. 現在、`requiredResourceAccess`プロパティは、ユーザーが読み取り可能なリソース アプリケーション名またはアクセス許可名の文字列のみを API に使用`Microsoft Graph``Office 365 SharePoint Online`できます。 他の API の場合は、代わりに UUID を使用する必要があります。 次の手順に従って、Azure portalから ID を取得できます。

    * Azure portalに新しい Azure AD アプリケーションを登録[します](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)。
    * Azure AD アプリケーション ページから選択 `API permissions` します。
    * 目的のアクセス許可を追加する場合に選択 `add a permission` します。
    * プロパティから `requiredResourceAccess` 、API とアクセス許可の ID を選択`Manifest`します。

## <a name="see-also"></a>関連項目

* [Toolkit でのアプリ マニフェストのプレビューとカスタマイズ](TeamsFx-preview-and-customize-app-manifest.md)
