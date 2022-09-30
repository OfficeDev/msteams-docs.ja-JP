---
title: Teams 会議用アプリ
author: surbhigupta
description: この記事では、参加者とユーザーの役割とアプリの拡張性に基づいて、Microsoft Teams 会議でアプリがどのように機能するかを説明します。
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 10604f4101185b2c18a619308e6551182809c290
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243207"
---
# <a name="apps-for-teams-meetings-and-calls"></a>Teams の会議と通話用のアプリ

会議ではコラボレーション、パートナーシップ、事前に連携された十分な情報に基づくコミュニケーション、及びフィードバックの共有が可能です。 会議アプリは、会議のライフサイクルの各段階でユーザー エクスペリエンスを提供できます。 会議のライフサイクルには、出席者の状態に応じた会議前、会議中、会議後のアプリ エクスペリエンスが含まれます。

> [!Note]
>
> インスタント会議、スケジュールされたパブリック チャネル会議、1 対 1、グループ通話用のアプリは、現在 [、パブリック 開発者向けプレビュー](../resources/dev-preview/developer-preview-intro.md)でのみ利用できます。

Teams では、次の会議の種類について、会議中のアプリへのアクセスがサポートされます。

* [**スケジュールされた会議**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop): Teams 予定表を通じてスケジュールされた会議。
* [**スケジュールされたチャネル会議**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop): Teams パブリック チャネルを通じてスケジュールされた会議。
* [**1 対 1 の通話: 1**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798) 対 1 チャットで開始された通話。
* [**グループ通話**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798): グループ チャットで開始された通話。
* [**インスタント会議**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5): Teams 予定表の **[今すぐ会議** ] ボタンを使用して開始された会議。

ユーザーは、Teams 会議ウィンドウのオプションを **+** 使用して、会議にアプリを追加できます。

:::image type="content" source="../assets/images/apps-in-meetings/add-app.png" alt-text="会議にアプリを追加する" border="true":::

[Teams ストア](https://go.microsoft.com/fwlink/p/?LinkID=2183121)にアクセスし、会議用に特別に設計されたアプリを探索します。

> [!Note]
>
> * 現在、1 対 1 の呼び出しにサード ユーザーが追加されると、新しいセッションが開始されることを意味するグループ呼び出しに呼び出しが昇格されます。 1 対 1 の呼び出しに追加されたアプリは、グループ呼び出しでは使用できません。 ただし、もう一度追加できます。
>
> * 現時点では、アプリ エクスペリエンスは Teams のインスタント チャネル会議ではサポートされていません。

次の図は、会議アプリの拡張機能のアイデアを示しています。

![会議アプリ拡張性](../assets/images/apps-in-meetings/meetingappextensibility.png)

この記事では、会議アプリの拡張性、API リファレンス、会議用のアプリの有効化と構成、および Teams のカスタム Together モード シーンの概要を説明します。

> [!Note]
>
> 会議アプリ (サイド パネル、会議ステージ) は、Teams デスクトップ クライアントでサポートされています。 Teams Web クライアントと同様に、開発者プレビューが有効になっている場合にのみサポートされます。

* **会議アプリを拡張** する: 会議機能拡張機能を使用して、会議エクスペリエンスを強化します。 この機能を使用すると、会議内にアプリを統合できます。 また、タブ、ボット、メッセージ拡張機能を統合できる会議のライフサイクルのさまざまなステージもあります。 さまざまな参加者の役割とユーザーの種類を識別し、会議イベントを取得し、会議中のダイアログを生成できます。
* **会議用のアプリを構成する: 会議** 用のアプリを使用して Teams をカスタマイズするには、アプリ マニフェストを更新して Teams 会議用のアプリを有効にし、会議シナリオ用にアプリを構成します。
* **Together Mode シーンを使用してカスタマイズ** する: 新しいカスタム Together Mode シーン機能を使用すると、ユーザーはチームと 1 か所で会議で共同作業できます。
* **共有チャネルでアプリのアクセス許可をカスタマイズ** する: アプリが共有チャネルで重要な情報を共有する場合は、外部メンバーのアプリ権限をカスタマイズできます。 [共有チャネル](../concepts/build-and-test/Shared-channels.md)のアプリのアクセス許可は、ホスト チームのアプリ名簿とホスト テナントのアプリ ポリシーに従います。
* **会議のトランスクリプトを取得する**: 会議後のシナリオで会議のトランスクリプトにアクセスして取得できます。 スケジュールされた会議のトランスクリプトを自動的に取得するようにアプリを構成し、それらを分析情報、インテリジェントな分析などのために使用します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [統合された会議アプリ](meeting-app-extensibility.md)

## <a name="see-also"></a>関連項目

* [Microsoft Teams 会議拡張機能の設計](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [会議アプリ API リファレンス - Teams](~/apps-in-teams-meetings/api-references.md)
* [カスタム Together モード シーン](~/apps-in-teams-meetings/teams-together-mode.md)
* [Teams 会議用にアプリを有効にして構成する](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
* [会議のライフサイクル](meeting-app-extensibility.md#meeting-lifecycle)
* [Live Share SDK による強化されたコラボレーション](teams-live-share-overview.md)
