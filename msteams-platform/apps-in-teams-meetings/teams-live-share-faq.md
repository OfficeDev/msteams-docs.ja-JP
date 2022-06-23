---
title: Live Share FAQ
description: このモジュールでは、Live Share のよく寄せられる質問について説明します。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 0c51d88ba08dea50e23b0b8eb451f84557f1f867
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189298"
---
---

# <a name="live-share-sdk-faq"></a>Live Share SDK FAQ

Live Share を使用する場合の一般的な質問に対する回答を取得します。<br>

<br>

<details>

<summary><b>独自の Azure Fluid Relay サービスを使用できますか?</b></summary>

はい。 `TeamsFluidClient` クラスを作成するときに、独自の `AzureConnectionConfig` を定義できます。 Live Share は、作成したコンテナーを会議に関連付けますが、コンテナーと地域の要件のトークンに署名するには、独自の Azure `ITokenProvider` を作成する必要があります。 詳細については、「Azure [Fluid Relay ドキュメント](/azure/azure-fluid-relay/)」を参照してください。

<br>

</details>

<details>

<summary><b>Live Share のホストされたサービスに格納されているデータのアクセス可能期間はどれくらいですか?</b></summary>

Live Share のホストされた Azure Fluid Relay サービスによって作成された Fluid コンテナーを通じて送信または保存されたデータには、24 時間アクセスできます。 24 時間を超えてデータを保持したい場合は、ホストされている Azure Fluid Relay サービスを独自のサービスに置き換えることができます。 または、Live Share のホストされたサービスと並行して独自のストレージ プロバイダーを使用することもできます。

<br>

</details>

<details>

<summary><b>Live Share はどのような種類の会議をサポートしていますか?</b></summary>

現在、スケジュールされた会議のみがサポートされており、すべての参加者が会議予定表に登録している必要があります。 1 対 1 の通話、グループ通話、今すぐ会議などの会議の種類はサポートされていません。

<br>

</details>

<details>

<summary><b>Live Share のメディア パッケージは DRM コンテンツで機能しますか?</b></summary>

いいえ。 Teams は現在、タブ アプリケーション用の暗号化されたメディアをサポートしていません。

<br>

</details>

<details>
<summary><b>Live Share セッションに参加できるユーザーの数はどれくらいですか?</b></summary>

現在、Live Share はセッションごとに最大 100 人の出席者をサポートしています。

<br>

</details>

## <a name="have-more-questions-or-feedback"></a>その他の質問やフィードバックはありますか?

[Live Share SDK](https://github.com/microsoft/live-share-sdk) の SDK リポジトリに問題と機能要求を送信します。 `live-share` および `microsoft-teams` タグを使用して、[スタック オーバーフロー](https://stackoverflow.com/questions/tagged/live-share+microsoft-teams)に SDK に関するハウツーの質問を投稿します。

## <a name="see-also"></a>関連項目

- [GitHub リポジトリ](https://github.com/microsoft/live-share-sdk)
- [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
- [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
- [会議の Teams アプリ](teams-apps-in-meetings.md)
