---
title: Teams アプリを Microsoft 365 全体に拡張する (プレビュー)
description: Microsoft 365 全体で Teams アプリを拡張する方法について説明します (Teams、Outlook、Office でアプリケーション ホストとして実行)。
ms.date: 10/10/2022
ms.topic: Conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 91586eefe21836118ed2f0a0071070ac2034bf76
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789878"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Teams アプリを Microsoft 365 全体に拡張する

[Microsoft Teams JavaScript クライアント SDK](../tabs/how-to/using-teams-client-sdk.md) (バージョン 2.0.0 以降)、[Teams アプリ マニフェスト](../resources/schema/manifest-schema.md) (バージョン 1.13 以降)、[Teams Toolkit](../toolkit/visual-studio-code-overview.md) の最新リリースでは、他の使用率の高い Microsoft 365 製品で実行するように Teams アプリをビルドして更新し、Microsoft コマーシャル マーケットプレース ([Microsoft AppSource](https://appsource.microsoft.com/)) または組織のプライベート アプリ ストアに発行できます。

Microsoft 365 全体で Teams アプリを拡張すると、拡張されたユーザー対象ユーザーにクロスプラットフォーム アプリを配信するための合理化された方法が提供されます。1 つのコードベースから、Teams、Outlook、Office 環境に合わせて調整されたアプリ エクスペリエンスを作成できます。 エンド ユーザーがアプリを使用するために作業のコンテキストを離れる必要はなくなり、管理者は統合された管理とデプロイワークフローの恩恵を受けます。

Teams アプリ プラットフォームは引き続き進化し、Microsoft 365 エコシステムに全体的に拡大しています。 Microsoft 365 (アプリケーション ホストとしての Teams、Outlook、Office) 全体の Teams アプリ プラットフォーム要素の現在のサポートを次に示します。

| Teams アプリの機能| アプリ マニフェスト要素 | Teams のサポート |Outlook* のサポート | Office* サポート | メモ |
|--|--|--|--|--|--|
| [**個人用スコープをタブする**](../tabs/what-are-tabs.md)    |`staticTabs`  | Web、デスクトップ、モバイル | Web (ターゲット リリース)、デスクトップ (ベータ チャネル) | Web (ターゲット リリース)、デスクトップ (ベータ チャネル)、モバイル (Android)| チャネルとグループのスコープは、Microsoft 365 ではまだサポートされていません。 [ノート](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook)を参照してください。
| [**メッセージ拡張機能**](../messaging-extensions/what-are-messaging-extensions.md) の検索ベース| `composeExtensions` | Web、デスクトップ、モバイル| Web (ターゲット リリース)、デスクトップ (ベータ チャネル)| - |アクション ベースは、Microsoft 365 ではまだサポートされていません。 [ノート](extend-m365-teams-message-extension.md#troubleshooting)を参照してください。 |
| リンク展開 | `composeExtensions.messageHandlers` | Web、デスクトップ | Web (ターゲット リリース)、デスクトップ (ベータ チャネル) | - | [メモ](extend-m365-teams-message-extension.md#link-unfurling)を参照する |
| [**Office アドイン**](/office/dev/add-ins/develop/json-manifest-overview) (プレビュー) | `extensions` | - | Web、デスクトップ | - | [devPreview](../resources/schema/manifest-schema-dev-preview.md) マニフェスト バージョンでのみ使用できます。 [ノート](#office-add-ins-preview)を参照してください。|

\*[Microsoft 365 ターゲット リリース](/microsoft-365/admin/manage/release-options-in-office-365) オプションと[更新チャネル登録Microsoft 365 Apps](/deployoffice/change-update-channels)には、組織全体または選択したユーザーの管理者オプトインが必要です。 更新チャネルはデバイス固有であり、Windows で実行されている Office のインストールにのみ適用されます。

Teams アプリ マニフェストと SDK のバージョン管理ガイダンスに関するガイダンスと、Microsoft 365 全体の現在の Teams プラットフォーム機能サポートの詳細については、 [Teams JavaScript クライアント SDK の概要](../tabs/how-to/using-teams-client-sdk.md)に関するページを参照してください。

> [!NOTE]
> Microsoft 365 エコシステム全体で実行する Teams アプリを拡張する際に、フィードバックと問題報告を歓迎します。 フィードバックを送信するには、通常の [Microsoft Teams 開発者コミュニティ チャネル](/microsoftteams/platform/feedback) を使用してください。

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Outlook と Office の個人用タブとメッセージング拡張機能

Outlook と Office の両方で実行される [Teams 個人用タブ](extend-m365-teams-personal-tab.md) アプリケーションとして Web アプリを拡張することで、作業のコンテキストでユーザーにアクセスできます。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="スクリーンショットは、Outlook、Office、Teams で実行されている [個人用] タブを示す例です。":::

モバイルでは、 [Android 用 Office アプリ](extend-m365-teams-personal-tab.md#office-app-for-android)で実行されている Teams 個人用タブをテストしてデバッグできます。

:::image type="content" source="images/office-mobile-personal-tab.png" alt-text="スクリーンショットは、Office で実行されている個人用タブを示す例です。":::

また、検索ベース[の Teams メッセージ拡張機能](extend-m365-teams-message-extension.md)を Outlook on the web と Windows デスクトップに拡張して、Microsoft Teams クライアントに加えて、Outlook の新規作成メッセージ領域を通じて結果を検索および共有することもできます。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="スクリーンショットは、Outlook と Teams で実行されているメッセージ拡張機能を示す例です。":::

[リンク展開は](extend-m365-teams-message-extension.md#link-unfurling)  、Microsoft Teams の場合と同じように Outlook Web 環境と Windows 環境で動作します。Teams アプリ マニフェスト バージョン 1.13 以降を使用する場合と同様に、それ以上の作業は必要ありません。

:::image type="content" source="images/outlook-teams-link-unfurling.png" alt-text="スクリーンショットは、Outlook と Teams で実行されているリンク解除を示す例です。":::

最新の [Teams アプリ マニフェスト](../resources/schema/manifest-schema.md) と [Teams JavaScript クライアント SDK](../tabs/how-to/using-teams-client-sdk.md) を使用してアプリを構築し、統合された最新の Microsoft 365 アプリ開発プロセスを活用します。 次に、顧客向けに合理化されたデプロイ、インストール、管理エクスペリエンスを提供し、アプリのリーチと使用状況を拡大します。

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Microsoft 365 全体で Teams アプリ マニフェストを使用する

Microsoft 365 開発者エコシステムの簡素化と合理化を目的として、Microsoft 365 の他の領域に Teams アプリ マニフェストを次のように拡張し続けています。

### <a name="office-add-ins-preview"></a>Office アドイン (プレビュー)

Microsoft Teams アプリ マニフェストの [開発者プレビュー バージョン](../resources/schema/manifest-schema-dev-preview.md) で Office アドインを定義して展開できるようになりました。 現在、このプレビューは、サブスクリプション Office for Windows で実行されている Outlook アドインに限定されています。

詳細については、「[Office アドイン用のTeams マニフェスト (プレビュー)](/office/dev/add-ins/develop/json-manifest-overview)」を参照してください。

## <a name="microsoft-commercial-marketplace-submission"></a>Microsoft コマーシャル マーケットプレースの申請

[Microsoft コマーシャル マーケットプレース (Microsoft](https://appsource.microsoft.com/) AppSource) ストアで増え続ける運用 Teams アプリに参加し、Outlook および Office プレビュー (対象リリース) の対象ユーザーのサポートを拡大します。 [Outlook と Office で有効になっている Teams アプリのアプリ申請プロセス](../concepts/deploy-and-publish/appsource/publish.md)は、従来の Teams アプリの場合と同じです。 唯一の違いは、アプリ パッケージで Teams アプリ マニフェスト [バージョン 1.13](../tabs/how-to/using-teams-client-sdk.md) を使用することです。これにより、Microsoft 365 全体で実行される Teams アプリのサポートが導入されます。

アプリが Microsoft 365 対応の Teams アプリとして発行されると、アプリは Teams ストアに加えて、Outlook および Office アプリ ストアにインストール可能なアプリとして検出されます。 Outlook と Office で実行する場合、アプリは Teams で付与されたのと同じアクセス許可を使用します。 Teams 管理者は、組織内のユーザーに対 [する Microsoft 365 全体の Teams アプリへのアクセスを管理](/MicrosoftTeams/manage-third-party-teams-apps) できます。

詳細については、「 [Microsoft 365 用 Teams アプリを発行する](publish.md)」を参照してください。

## <a name="next-step"></a>次のステップ

開発環境を設定して、Microsoft 365 用の Teams アプリをビルドします。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)
