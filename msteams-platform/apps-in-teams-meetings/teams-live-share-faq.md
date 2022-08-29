---
title: Live Share FAQ
author: surbhigupta
description: このモジュールでは、Live Share のよく寄せられる質問について説明します。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: b53d7c01722faa51824e0df17586bc8a385438b0
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425611"
---
---

# <a name="live-share-sdk-faq"></a>Live Share SDK FAQ

Live Share を使用する場合の一般的な質問に対する回答を取得します。<br>

<br>

<details>

<summary><b>独自の Azure Fluid Relay サービスを使用できますか?</b></summary>

はい。 `TeamsFluidClient` クラスを作成するときに、独自の `AzureConnectionConfig` を定義できます。 Live Share では、作成したコンテナーが会議に関連付けられますが、コンテナーのトークンに署名するためのインターフェイスを実装 `ITokenProvider` する必要があります。 たとえば、Azure クラウド関数を使用してサーバーからアクセス トークンを要求する指定 `AzureFunctionTokenProvider`された関数を使用できます。

ほとんどの場合、無料のホステッド サービスを使用することが有益であると思われますが、Live Share アプリに独自の Azure Fluid Relay サービスを使用することが有益な場合があります。 次の場合は、カスタム AFR サービス接続の使用を検討してください。

* 会議の有効期間を超えて、Fluid コンテナーにデータを格納する必要があります。
* カスタム セキュリティ ポリシーを必要とするサービスを介して機密データを送信します。
* たとえば、Teams の外部のアプリケーション用に、 `SharedMap`Fluid Framework を使用して機能を開発します。

詳細については、[Azure Fluid Relay のドキュメント](/azure/azure-fluid-relay/)[をガイドまたは参照する方法](./teams-live-share-how-to/how-to-custom-azure-fluid-relay.md)を参照してください。

<br>

</details>

<details>

<summary><b>Live Share のホストされたサービスに格納されているデータのアクセス可能期間はどれくらいですか?</b></summary>

Live Share のホストされた Azure Fluid Relay サービスによって作成された Fluid コンテナーを通じて送信または保存されたデータには、24 時間アクセスできます。 24 時間を超えてデータを保持したい場合は、ホストされている Azure Fluid Relay サービスを独自のサービスに置き換えることができます。 または、Live Share のホストされたサービスと並行して独自のストレージ プロバイダーを使用することもできます。

<br>

</details>

<details>

<summary><b>Live Share はどのような種類の会議をサポートしていますか?</b></summary>

プレビュー中は、スケジュールされた会議のみがサポートされ、すべての参加者が会議予定表に参加している必要があります。 1 対 1 の通話、グループ通話、今すぐ会議などの会議の種類はサポートされていません。

<br>

</details>

<details>

<summary><b>Live Share のメディア パッケージは DRM コンテンツで機能しますか?</b></summary>

いいえ。 Teams は現在、デスクトップ上のタブ アプリケーションの暗号化メディアをサポートしていません。 Chrome、Edge、モバイル クライアントがサポートされています。 詳細については、 [ここで問題を追跡](https://github.com/microsoft/live-share-sdk/issues/14)できます。

<br>

</details>

<details>
<summary><b>Live Share セッションに参加できるユーザーの数はどれくらいですか?</b></summary>

現在、Live Share はセッションごとに最大 100 人の出席者をサポートしています。 これが興味のある場合は、 [ここでディスカッションを開始](https://github.com/microsoft/live-share-sdk/discussions)できます。

<br>

</details>

<details>
<summary><b>Teams の外部で Live Share の一時的なデータ構造を使用できますか?</b></summary>

現在、Live Share パッケージでは、Teams クライアント SDK が正しく機能している必要があります。 Microsoft Teams 内の `@microsoft/live-share` 機能、または `@microsoft/live-share-media` Microsoft Teams 以外では機能しません。 これが興味のある場合は、 [ここでディスカッションを開始](https://github.com/microsoft/live-share-sdk/discussions)できます。

<br>

</details>

<details>
<summary><b>複数の Fluid コンテナーを使用できますか?</b></summary>

現在、Live Share では、提供されている Azure Fluid Relay サービスを使用してコンテナーを 1 つだけ使用できます。 ただし、Live Share コンテナーと、独自の Azure Fluid Relay インスタンスによって作成されたコンテナーの両方を使用することは可能です。

<br>

</details>

<details>
<summary><b>コンテナーの作成後に Fluid コンテナー スキーマを変更できますか?</b></summary>

現在、Live Share では、コンテナーを作成または参加した後に、Fluid `ContainerSchema` に新規`initialObjects`追加することはサポートされていません。 Live Share セッションは有効期間が短いため、これは最も一般的に、アプリに新機能を追加した後の開発中の問題です。

> [!NOTE]
> プロパティを `dynamicObjectTypes` 使用している場合は、任意の `ContainerSchema`時点で新しい型を追加できます。 後でスキーマから型を削除すると、それらの型の既存の DDS インスタンスは正常に失敗します。

ブラウザーでローカルでテストするときの変更に起因する `initialObjects` エラーを修正するには、URL からハッシュされたコンテナー ID を削除し、ページを再読み込みします。 Teams 会議でテストしている場合は、新しい会議を開始してもう一度やり直してください。

アプリを新規 `SharedObject` または `EphemeralObject` インスタンスで頻繁に更新する予定がある場合は、新しいスキーマ変更を運用環境にデプロイする方法を検討する必要があります。 実際のリスクは比較的低く、持続性は短くなりますが、変更をロールアウトする時点でアクティブなセッションが存在する可能性があります。 セッション内の既存のユーザーは影響を受けませんが、重大な変更をデプロイした後にそのセッションに参加しているユーザーは、セッションへの接続に問題がある可能性があります。 これを軽減するために、次の解決策の一部を検討してください。

* 通常の営業時間外に Web アプリケーションのスキーマ変更をデプロイします。
* 変更するのではなく`initialObjects`、スキーマに加えられたすべての変更に使用`dynamicObjectTypes`します。

> [!NOTE]
> Live Share は現在、バージョン管理を `ContainerSchema`サポートしていません。また、移行専用の API もありません。

<br>

</details>

<details>
<summary><b>Live Share を使用して出力できる変更イベントの数に制限はありますか?</b></summary>

Live Share はプレビュー段階ですが、Live Share を通じて生成されるイベントに対する制限は適用されません。 最適なパフォーマンスを得るには、50 ミリ秒以上ごとに 1 つのメッセージに対して、または`EphemeralObject`インスタンスから`SharedObject`生成された変更を破棄する必要があります。 これは、カーソルの位置の同期、インク、ページの周囲のオブジェクトのドラッグなど、マウスまたはタッチ座標に基づいて変更を送信する場合に特に重要です。

<br>

</details>

## <a name="have-more-questions-or-feedback"></a>その他の質問やフィードバックはありますか?

[Live Share SDK](https://github.com/microsoft/live-share-sdk) の SDK リポジトリに問題と機能要求を送信します。 `live-share` および `microsoft-teams` タグを使用して、[スタック オーバーフロー](https://stackoverflow.com/questions/tagged/live-share+microsoft-teams)に SDK に関するハウツーの質問を投稿します。

## <a name="see-also"></a>関連項目

* [GitHub リポジトリ](https://github.com/microsoft/live-share-sdk)
* [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
* [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
* [会議の Teams アプリ](teams-apps-in-meetings.md)
