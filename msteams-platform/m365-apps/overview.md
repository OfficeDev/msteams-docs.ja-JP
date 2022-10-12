---
title: Teams アプリを Microsoft 365 全体に拡張する (プレビュー)
description: Microsoft 365 全体で Teams アプリを拡張する方法 (Teams、Outlook、Office でアプリケーション ホストとして実行) について説明します。
ms.date: 10/10/2022
ms.topic: Conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 4c05fbe0c763d9b650573e33edfa5e332aaba90d
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537541"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Teams アプリを Microsoft 365 全体に拡張する

[Microsoft Teams JavaScript クライアント SDK](../tabs/how-to/using-teams-client-sdk.md) (バージョン 2.0.0 以降)、[Teams アプリ マニフェスト](../resources/schema/manifest-schema.md) (バージョン 1.13 以降)、[Teams Toolkit](../toolkit/visual-studio-code-overview.md) の最新リリースでは、他の高使用率の Microsoft 365 製品で実行される Teams アプリをビルドおよび更新し、Microsoft コマーシャル マーケットプレース ([Microsoft AppSource](https://appsource.microsoft.com/)) または組織のプライベート アプリ ストアに発行できます。

Microsoft 365 全体に Teams アプリを拡張すると、1 つのコードベースから Teams、Outlook、Office 環境向けにカスタマイズされたアプリ エクスペリエンスを作成できます。 エンド ユーザーは、アプリを使用するために作業のコンテキストから離れる必要はありません。管理者は、統合された管理と展開ワークフローの恩恵を受けます。

Teams アプリ プラットフォームは、Microsoft 365 エコシステムに全体的に進化し、拡大し続けています。 Microsoft 365 全体の Teams アプリ プラットフォーム要素 (Teams、Outlook、Office をアプリケーション ホストとして) の現在のサポートを次に示します。

| Teams アプリの機能| アプリ マニフェスト要素 | Teams のサポート |Outlook* のサポート | Office* のサポート | メモ |
|--|--|--|--|--|--|
| [**タブ**](../tabs/what-are-tabs.md) の個人用スコープ    |`staticTabs`  | Web、デスクトップ、モバイル | Web (ターゲット リリース)、デスクトップ (ベータ チャネル) | Web (対象リリース)、デスクトップ (ベータ チャネル)、Mobile (Android)| Microsoft 365 では、チャネルスコープとグループ スコープはまだサポートされていません。 メモを参照 [してください](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook)。
| [**メッセージ表示オプション**](../messaging-extensions/what-are-messaging-extensions.md) の検索ベース| `composeExtensions` | Web、デスクトップ、モバイル| Web (ターゲット リリース)、デスクトップ (ベータ チャネル)| - |Microsoft 365 では、アクション ベースはまだサポートされていません。 メモを参照 [してください](extend-m365-teams-message-extension.md#troubleshooting)。 |
| リンク展開 | `composeExtensions.messageHandlers` | Web、デスクトップ | Web (ターゲット リリース)、デスクトップ (ベータ チャネル) | - | [メモ](extend-m365-teams-message-extension.md#link-unfurling)を表示する |
| [**Office アドイン**](/office/dev/add-ins/develop/json-manifest-overview) (プレビュー) | `extensions` | - | Web、デスクトップ | - | [devPreview](../resources/schema/manifest-schema-dev-preview.md) マニフェスト バージョンでのみ使用できます。 メモを参照 [してください](#office-add-ins-preview)。|

\*[Microsoft 365 の対象となるリリース](/microsoft-365/admin/manage/release-options-in-office-365) オプションと[Microsoft 365 Apps更新プログラム チャネル](/deployoffice/change-update-channels)の登録には、組織全体または選択したユーザーの管理者オプトインが必要です。 更新チャネルはデバイス固有であり、Windows で実行されている Office のインストールにのみ適用されます。

Teams アプリ マニフェストと SDK のバージョン管理に関するガイダンス、および Microsoft 365 全体での現在の Teams プラットフォーム機能のサポートの詳細については、 [Teams JavaScript クライアント SDK の概要](../tabs/how-to/using-teams-client-sdk.md)を参照してください。

> [!NOTE]
> Microsoft 365 エコシステム全体で実行するように Teams アプリを拡張する際のフィードバックと問題報告を歓迎します。 フィードバックを送信するには、通常の [Microsoft Teams 開発者コミュニティ チャネル](/microsoftteams/platform/feedback) を使用してください。

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Outlook と Office の個人用タブとメッセージング拡張機能

Outlook と Office の両方で実行される [Teams 個人用タブ](extend-m365-teams-personal-tab.md) アプリケーションとして Web アプリを拡張することで、自分の仕事の状況に合わせて、ユーザーに連絡を取ります。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="スクリーンショットは、Outlook、Office、Teams で実行されている個人用タブを示す例です。":::

モバイルでは、 [Android 用 Office アプリ](extend-m365-teams-personal-tab.md#office-app-for-android)で実行されている Teams 個人用タブをテストしてデバッグできます。

:::image type="content" source="images/office-mobile-personal-tab.png" alt-text="スクリーンショットは、Office で実行されている個人用タブを示す例です。":::

また、検索ベース[の Teams メッセージ拡張機能](extend-m365-teams-message-extension.md)をOutlook on the webと Windows デスクトップに拡張して、Microsoft Teams クライアントに加えて、Outlook の作成メッセージ領域で結果を検索および共有することもできます。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="スクリーンショットは、Outlook と Teams で実行されているメッセージ拡張機能を示す例です。":::

Outlook Web および Windows 環境での[リンク解除](extend-m365-teams-message-extension.md#link-unfurling)の動作は、Teams アプリ マニフェスト バージョン 1.13 以降を使用する場合と同じように、Microsoft Teams で行う場合と同じです。

:::image type="content" source="images/outlook-teams-link-unfurling.png" alt-text="スクリーンショットは、Outlook と Teams で実行されているリンクの展開を示す例です。":::

最新の [Teams アプリ マニフェスト](../resources/schema/manifest-schema.md) と [Teams JavaScript クライアント SDK](../tabs/how-to/using-teams-client-sdk.md) を使用してアプリを構築し、最新の統合 Microsoft 365 アプリ開発プロセスに役立ちます。 その後、アプリのリーチと使用状況を拡大する、合理化されたデプロイ、インストール、および管理者エクスペリエンスを顧客に提供します。

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Microsoft 365 全体で Teams アプリ マニフェストを使用する

Microsoft 365 開発者エコシステムの簡素化と合理化を目的として、Teams アプリ マニフェストを次のように Microsoft 365 の他の領域に拡大し続けています。

### <a name="office-add-ins-preview"></a>Office アドイン (プレビュー)

Microsoft Teams アプリ マニフェストの [開発者プレビュー バージョン](../resources/schema/manifest-schema-dev-preview.md) で Office アドインを定義して展開できるようになりました。 現在、このプレビューは、サブスクリプション Office for Windows で実行されている Outlook アドインに限定されています。

詳細については、「[Office アドイン用のTeams マニフェスト (プレビュー)](/office/dev/add-ins/develop/json-manifest-overview)」を参照してください。

## <a name="microsoft-commercial-marketplace-submission"></a>Microsoft コマーシャル マーケットプレースの申請

[Microsoft コマーシャル マーケットプレース (Microsoft](https://appsource.microsoft.com/) AppSource) ストアで増え続ける運用 Teams アプリに参加し、Outlook および Office プレビュー (対象リリース) の対象ユーザーに対するサポートを拡大します。 [Outlook と Office で有効になっている Teams アプリのアプリ申請プロセス](../concepts/deploy-and-publish/appsource/publish.md)は、従来の Teams アプリと同じです。 唯一の違いは、アプリ パッケージで Teams アプリ マニフェスト [バージョン 1.13](../tabs/how-to/using-teams-client-sdk.md) を使用することです。これにより、Microsoft 365 全体で実行される Teams アプリのサポートが導入されます。

Microsoft 365 対応の Teams アプリとして公開されると、アプリは、Teams ストアに加えて、Outlook および Office アプリ ストアからインストール可能なアプリとして検出できるようになります。 Outlook と Office で実行している場合、アプリは Teams で付与されたのと同じアクセス許可を使用します。 Teams 管理者は、組織内のユーザー [に対して Microsoft 365 全体の Teams アプリへのアクセスを管理](/MicrosoftTeams/manage-third-party-teams-apps) できます。

詳細については、「 [Microsoft 365 用の Teams アプリの発行」を](publish.md)参照してください。

## <a name="next-step"></a>次のステップ

Microsoft 365 用の Teams アプリをビルドするように開発環境を設定します。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)
