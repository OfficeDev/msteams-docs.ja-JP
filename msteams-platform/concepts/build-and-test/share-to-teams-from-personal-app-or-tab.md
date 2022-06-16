---
title: 個人用アプリまたはタブから Teams に共有する
description: 個人用アプリまたはタブで [共有してTeams] ボタンを有効にする方法、制限事項、エンド ユーザー エクスペリエンスについて説明します。
ms.topic: reference
ms.localizationpriority: medium
ms.openlocfilehash: 6a676dd90d9b02332869b5584b1e067be8bfcf19
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123935"
---
# <a name="share-to-teams-from-personal-app-or-tab"></a>個人用アプリまたはタブから Teams に共有する

> [!NOTE]
> 現在、Teamsへの共有は[、パブリック開発者向けプレビュー](../../resources/dev-preview/developer-preview-intro.md)でのみ利用できます。

Teamsに共有すると、ユーザーは個人用アプリまたはタブから、Teams内の他のユーザーまたはグループまたはチャネルにコンテンツを共有できます。 ユーザーは[共有してTeams] を選択し、ポップアップ ウィンドウで [Share to Teams エクスペリエンス] を起動できます。 ポップアップ ウィンドウを使用すると、ユーザーは他のユーザーまたはグループまたはチャネルを追加してコンテンツを共有できます。

次の図は、[Teamsへの共有] ポップアップ ウィンドウを示しています。

:::image type="content" source="../../assets/images/share-to-teams/share-to-teams.PNG" alt-text="share-to-teams-pop-up":::

## <a name="enable-share-to-teams-button"></a>[Teamsに共有を有効にする] ボタン

> [!NOTE]
> [JavaScript クライアント SDK または Microsoft Teams JavaScript クライアント SDK](../../tabs/how-to/using-teams-client-sdk.md) [v2 プレビュー](../../tabs/how-to/using-teams-client-sdk.md) (`@microsoft/teams-js@1.11.0-beta.7`またはそれ以降) をMicrosoft Teamsして、個人用アプリまたはタブの [Share to Teams] を有効にしていることを確認します。

share to Teamsを有効にするには:

1. **Javascript クライアント SDK を使用して** 個人用アプリまたはタブTeams作成します。

2. **[Teamsに共有する**] ボタンを作成します。

3. [Teamsに共有] ボタンで、コンテンツ ペイロードを使用して呼び出`microsoftTeams.sharing.shareWebContent`します。

次の例では、コンテンツ ペイロードを作成する方法について説明します。

```json
microsoftTeams.sharing.shareWebContent({
        content: [
          {
            type: 'URL',
            url: '<URL to be shared>',
            message: 'Default message to be loaded in the compose box',
            preview: true
          }
        ]
      });
```

ペイロードには、次のパラメーターが含まれています。

| プロパティ名 | 用途 |
|---|---|
| `type` | 型は次の値にする必要があります。 `URL` |
| `url` | `URL` 共有する |
|`message`| 作成ボックスに読み込まれる既定のメッセージ |
| `preview` | URL プレビューを有効にするように設定する`true` |

次の図は、[Teamsに共有] オプションを示しています。

:::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="share-to-teams-button":::

## <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **100** | API は現在のプラットフォームではサポートされていません。 |
| **404** | 指定したファイルが指定された場所に見つかりませんでした。 |
| **500** | 必要な操作の実行中に内部エラーが発生しました。 |
| **501** | API は現在のコンテキストではサポートされていません。 |
| **1000** | ユーザーによって拒否されたアクセス許可。 |
| **2000** | ネットワークの問題。 |
| **3000** | 基になるハードウェアでは、この機能はサポートされていません。 |
| **4000** | いくつかの引数は無効です。 |
| **5000** | ユーザーはこの操作に対して承認されていません。 |
| **6000** | リソースが不足しているため、操作を完了できませんでした。 |
| **7000** | API が頻繁に呼び出されたため、プラットフォームによって要求が調整されました。 |
| **8000** | ユーザーが操作を中止しました。 |
| **9000** | プラットフォーム コードは古く、この API は実装されていません。 |
| **10,000** | 戻り値が大きすぎて、サイズの境界を超えています。 |

## <a name="limitations"></a>制限事項

[Teamsに共有] ボタンを追加する場合の制限事項:

* [Teamsに共有] ボタンは、Teams内で実行されているアプリでホストまたは埋め込むことができます。
* **Teams Javascript クライアント SDK** を使用して作成したアプリに、[Teamsに共有] ボタンを追加できます。

## <a name="end-user-share-to-teams-experience"></a>エンド ユーザーがTeamsエクスペリエンスに共有する

個人用アプリまたはタブで [チームへの共有] ボタンを有効にした後、コンテンツを共有できます。 アクセスするには、次の手順に従います。

1. 個人用アプリまたはタブを開き、[**Teamsに共有**] を選択します。

    :::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="share-to-teams-button":::

2. 他のユーザーまたはグループまたはチャネルを追加してコンテンツを共有します。

    :::image type="content" source="../../assets/images/share-to-teams/add-recepient.PNG" alt-text="add-recipient":::

    > [!NOTE]
    > これについて **何かを言って** メモを追加できます。

3. **共有** を選択します。

   :::image type="content" source="../../assets/images/share-to-teams/add-notes.PNG" alt-text="add-note":::

4. [ **表示]** を選択して、リンクが共有された会話にアクセスします。

   :::image type="content" source="../../assets/images/share-to-teams/link-shared.PNG" alt-text="share-to-teams-link-shared":::

## <a name="see-also"></a>関連項目

* [Web アプリから Teams に共有する](share-to-teams-from-web-apps.md)
* [プライベート タブを作成する](../../tabs/how-to/create-personal-tab.md)
