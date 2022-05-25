---
title: Teams アプリを Microsoft 365 全体に拡張する (プレビュー)
description: Teams アプリ エクスペリエンスを、使用頻度の高い Microsoft 365 の他の領域に拡張します
ms.date: 05/24/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 9cc0d88d5f992aa596509a6206a26baa413bdcf1
ms.sourcegitcommit: c197fe4c721822b6195dfc5c7d8e9ccd47f142fe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2022
ms.locfileid: "65668145"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Teams アプリを Microsoft 365 全体に拡張する

[Microsoft Teams JavaScript クライアント SDK](../tabs/how-to/using-teams-client-sdk.md) (バージョン 2.0.0)、[Teams アプリ マニフェスト](../resources/schema/manifest-schema.md) (バージョン 1.13)、[Teams Toolkit](../toolkit/visual-studio-code-overview.md)の最新リリースでは、Teams アプリをビルドして更新して、他の高使用率のMicrosoft 365で実行できます。 製品を Microsoft コマーシャル マーケットプレース ([Microsoft AppSource](https://appsource.microsoft.com/)) に発行します。

Teams アプリをMicrosoft 365に拡張すると、1 つのコードベースから、Teams、Outlook、およびOffice環境に合わせてカスタマイズされたアプリ エクスペリエンスを作成できます。 エンド ユーザーは、アプリを使用するために作業のコンテキストから離れる必要はありません。管理者は、統合された管理と展開ワークフローの恩恵を受けます。

Teams アプリ プラットフォームは、引き続き進化を続け、Microsoft 365 エコシステムに包括的に拡大しています。 Microsoft 365 (アプリケーション ホストとしてのTeams、Outlook、Office) 全体でTeamsアプリ プラットフォーム要素の現在のサポートを次に示します。

|          | アプリ マニフェスト要素 | Teamsサポート |Outlook* サポート | Office* サポート | 備考 |
|--|--|--|--|--|--|
| [**タブ**](../tabs/what-are-tabs.md) (個人用スコープ)    |`staticTabs`  | Web、デスクトップ、モバイル | Web (ターゲット リリース)、デスクトップ (ベータ チャネル) | Web (対象となるリリース)| チャネルとグループのスコープは、Microsoft 365ではまだサポートされていません。 メモを参照 [してください](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook)。
| [**メッセージ拡張機能**](../messaging-extensions/what-are-messaging-extensions.md) (検索ベース)| `composeExtensions` | Web、デスクトップ、モバイル| Web (ターゲット リリース)、デスクトップ (ベータ チャネル)| |Microsoft 365に対してはまだサポートされていないアクション ベース。 メモを参照 [してください](extend-m365-teams-message-extension.md#preview-your-message-extension-in-outlook)。 |
| [**Graph コネクタ**](/microsoftsearch/connectors-overview)| `graphConnector` | Web、デスクトップ、モバイル| Web、デスクトップ | Web| [メモ](#graph-connectors)を表示する
| [**Office アドイン**](/office/dev/add-ins/develop/json-manifest-overview) (プレビュー) | `extensions` | | Web、デスクトップ  | | [devPreview](../resources/schema/manifest-schema-dev-preview.md) マニフェスト バージョンでのみ使用できます。 メモを参照 [してください](#office-add-ins-preview)。|

\*[Microsoft 365対象のリリース](/microsoft-365/admin/manage/release-options-in-office-365) オプションと[Microsoft 365 Apps更新チャネル](/deployoffice/change-update-channels)の登録には、組織全体または選択したユーザーの管理者オプトインが必要です。

Teams アプリ マニフェストと SDK のバージョン管理に関するガイダンスと、Microsoft 365全体での現在のTeamsプラットフォーム機能のサポートの詳細については、[Teams JavaScript クライアント SDK の概要](../tabs/how-to/using-teams-client-sdk.md)を参照してください。

> [!NOTE]
> Teams アプリをMicrosoft 365 エコシステム全体で実行するように拡張する際のフィードバックと問題の報告を歓迎します。 フィードバックを送信するには、通常の[Microsoft Teams開発者コミュニティ チャネル](/microsoftteams/platform/feedback)を使用してください。

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>OutlookとOfficeの個人用タブとメッセージング拡張機能

web アプリを、OutlookとOfficeの両方で実行されるTeams個人用タブ アプリケーションとして拡張することで、自分の作業のコンテキストでユーザーに直接アクセスします。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Outlook、Office、Teams で実行されている個人用タブ":::

また、検索ベースのTeamsメッセージ拡張機能をOutlook on the webデスクトップとWindows デスクトップに拡張して、顧客がMicrosoft Teams クライアントに加えて、Outlookの作成メッセージ領域を通じて結果を検索および共有することもできます。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Outlook と Teams で実行されているメッセージ拡張機能":::

最新の[Teams アプリ マニフェスト](../resources/schema/manifest-schema.md)と [Teams JavaScript クライアント SDK](../tabs/how-to/using-teams-client-sdk.md) を使用してアプリを構築すると、統合開発プロセスが提供されます。 効率的なデプロイ、インストール、および管理者エクスペリエンスを顧客に提供できるようにすることで、アプリの潜在的なリーチと使用状況を拡大できます。

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Microsoft 365全体Teamsアプリ マニフェストを使用する

Microsoft 365開発者エコシステムの簡素化と合理化を目的として、Teams アプリ マニフェストを次のようにMicrosoft 365の他の領域に拡大し続けています。

### <a name="graph-connectors"></a>Graph コネクタ

Microsoft Graph コネクタを使用すると、組織はサード パーティのデータにインデックスを付けて、Microsoft Search結果として表示されるようにし、Teams アプリで検索可能なコンテンツ ソースの種類を展開できます。
詳細については、[Microsoft Searchの Microsoft Graph コネクタの概要に関するページを](/microsoftsearch/connectors-overview)参照してください。

Teams アプリでグラフ コネクタの使用を開始するには、[Teams Toolkit Graph コネクタのサンプル](https://aka.ms/teamsfx-graph-connector-sample)と[開発者プレビュー マニフェスト スキーマリファレンスMicrosoft Teams](../resources/schema/manifest-schema-dev-preview.md)確認してください。

### <a name="office-add-ins-preview"></a>Office アドイン (プレビュー)

これで、Microsoft Teams アプリ マニフェストの[開発者プレビュー バージョン](../resources/schema/manifest-schema-dev-preview.md)で、Office アドインを定義してデプロイできるようになりました。 現在、このプレビューは、Windowsのサブスクリプション Officeで実行されているOutlook アドインに限定されています。

詳細については、「[Office アドイン (プレビュー)のTeams マニフェスト](/office/dev/add-ins/develop/json-manifest-overview)」を参照してください。

## <a name="microsoft-appsource-submission"></a>Microsoft AppSource の申請

[Microsoft AppSource](https://appsource.microsoft.com/) ストアで増え続ける運用Teams アプリに参加し、OutlookおよびOffice プレビュー (ターゲット リリース) の対象ユーザーに対するサポートを拡大します。 [OutlookとOfficeに対して有効になっているTeams アプリの申請プロセス](../concepts/deploy-and-publish/appsource/publish.md)は、従来のTeams アプリの場合と同じです。唯一の違いは、アプリ パッケージTeamsアプリ マニフェスト [バージョン 1.13](../tabs/how-to/using-teams-client-sdk.md) を使用することです。これにより、アプリ全体で実行されるTeams アプリのサポートが導入されます。Microsoft 365。

Microsoft 365対応のTeams アプリとして発行されると、アプリはTeams ストアに加えて、OutlookストアとOffice アプリ ストアからインストール可能なアプリとして検出できるようになります。 OutlookとOfficeで実行する場合、アプリはTeamsで付与されたのと同じアクセス許可を使用します。 Teams管理者は、組織内のユーザー[のMicrosoft 365全体でTeams アプリへのアクセスを管理](/MicrosoftTeams/manage-third-party-teams-apps)できます。

詳細については、「[Microsoft 365用のアプリTeams発行する」を](publish.md)参照してください。

## <a name="next-step"></a>次のステップ

Microsoft 365用のTeams アプリをビルドするように開発環境を設定します。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)
