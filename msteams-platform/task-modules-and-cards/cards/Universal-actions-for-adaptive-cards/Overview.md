---
title: アダプティブ カードのユニバーサル アクションの概要
description: デスクトップ環境とモバイル環境のユーザー固有のビュー、シーケンシャル ワークフローのサポートなど、アダプティブ カードのユニバーサル アクションの簡単な概要
ms.topic: overview
ms.localizationpriority: medium
ms.openlocfilehash: 8ec546b0345c1fd26caf0b3016a788e14b623ae2
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356165"
---
# <a name="universal-actions-for-adaptive-cards"></a>アダプティブ カードのユニバーサル アクション

アダプティブ カードユニバーサル アクションは、アダプティブ カードのレイアウトとレンダリングがユニバーサルであったとしても、アクション処理はそうではないという開発者のフィードバックから進化しました。 開発者が同じカードを別の場所に送信する場合でも、アクションを異なる方法で処理する必要があります。

アダプティブ カードのユニバーサル アクションは、アクションを処理するための共通のバックエンドとしてボットを導入し、Teams や Outlook などのアプリ間で動作する新しいアクションの種類 `Action.Execute` を導入します。

このドキュメントは、ユニバーサル アクション モデルを使用して、プラットフォームやアプリケーション間でアダプティブ カードを操作するユーザー エクスペリエンスを強化する方法を理解するのに役立ちます。

> [!NOTE]
> アダプティブ カード v1.4 のユニバーサル アクションのサポートは、ボットによって送信されたカードでのみ使用できます。 作成ボックスとリンク解除カードを介して送信されるカードのサポートは、近日公開される予定です。

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a>アダプティブ カードのユニバーサル アクションを使用してユーザー エクスペリエンスを強化する

アダプティブ カードのユニバーサル アクションは、次のシナリオを有効にすることでユーザー エクスペリエンスを強化します。

* [ユニバーサル アクション](#universal-actions)
* [ユーザー固有のビュー](#user-specific-views)
* [シーケンシャル ワークフロー サポート](#sequential-workflow-support)
* [最新のビュー](#up-to-date-views)

### <a name="universal-actions"></a>ユニバーサル アクション

アダプティブ カードのユニバーサル アクションの前は、次のように異なるホストによって異なるアクション モデルが提供されていました。

* Teams またはボットは、実際の通信モデルを基になるチャネルに延期するアプローチである `Action.Submit` を使用しました。
* Outlook は `Action.Http` を使用して、アダプティブ カード ペイロードで明示的に指定されたバックエンド サービスと通信しました。

次の図は、現在の不整合なアクション モデルを示しています。

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="不整合なアクション モデル":::

アダプティブ カードのユニバーサル アクションでは、`Action.Execute` を使用して、さまざまなプラットフォームでのアクション処理を行うことができます。 `Action.Execute` は、Teams や Outlook などのハブ間で機能します。 さらに、アダプティブ カードは、`Action.Execute` がトリガーされた呼び出し要求の応答として返すことができます。

次の図は、新しいユニバーサル アクション モデルを示しています。

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="アダプティブ カードの新しいユニバーサル アクション":::

Teams と Outlook の両方に同じカードを送信し、基になるボットを使用して相互に同期を維持できるようになりました。 いずれかのプラットフォームで実行されたすべてのアクションは、この *一度のビルドでどこででもデプロイする (アダプティブ カードのユニバーサル アクション) モデル* を使用して、もう一方のプラットフォームに反映されます。

次の図は、Teams と Outlook の両方のアダプティブ カードのユニバーサル アクションを示しています。

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="~/assets/images/mobile-universal-bots-teams-outlook.png" alt-text="Teams と Outlook に同じカードをモバイルする":::

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="Teams と Outlook に同じカード":::

* * *

### <a name="user-specific-views"></a>ユーザー固有のビュー

現在、Teams チャットまたはチャネルのすべてのユーザーは、アダプティブ カードでまったく同じビューとボタンアクションを表示します。 ただし、特定のシナリオでは、特定のユーザーが異なる動作をし、同じチャットまたはチャネル内の異なる情報にアクセスする必要があります。

たとえば、チャットまたはチャネルでインシデント レポート カードを送信する場合、インシデントが割り当てられているユーザーにのみ、**[解決]** ボタンが表示される必要があります。 一方、インシデント作成者は **[編集]** ボタンを表示する必要があり、他のすべてのユーザーはインシデントの詳細のみを表示できる必要があります。 これは、 `refresh` プロパティによって有効になっているユーザー固有のビューによって実現されます。

次の図は、チャット内の異なるユーザーが要件に基づいて異なるアクションを表示するチケット メッセージング拡張機能 (ME) の例を示しています。

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="モバイル ユーザー固有のビュー":::

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="ユーザー固有のビュー":::

* * *

詳細については、「[ユーザー固有のビューのサンプル](User-Specific-Views.md)」を参照してください。

### <a name="sequential-workflow-support"></a>シーケンシャル ワークフローのサポート

シーケンシャル ワークフローのサポートにより、ユーザーは異なるカードを個別に送信することなく、一連のワークフローを進めることができます。 これは、アクションに応答してアダプティブ カードを返す `Action.Execute` の機能によって実現されます。 また、チャットまたはチャネル内のすべてのユーザーは、チャット内の他のユーザーのカードを変更することなく、ワークフローを進めることができます。

次の図は、食品注文ボットの例を示しています。 <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

次の図は、チャットまたはチャネル内のさまざまなユーザーのさまざまな状態を示しています。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="ケータリング ボットの状態":::

詳細については、「[シーケンシャル ワークフローのサンプル](Sequential-Workflows.md)」を参照してください。

### <a name="up-to-date-views"></a>最新のビュー

自動的に更新されるアダプティブ カードを作成できます。 たとえば、ユーザーから送信された承認要求を指定できます。 承認後、カードには、要求の承認時刻と要求を承認したユーザーに関する詳細が自動的に表示される必要があります。 更新モデルを使用すると、このような最新のビューを提供できます。 次の図は、複数ステップの承認フローと、さまざまなユーザーのビューがどのように表示されるかを示しています。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="最新のユーザー固有ビュー":::

詳細については、「[最新のビューのサンプル](Up-To-Date-Views.md)」を参照してください。

これで、新しいユニバーサル アクション モデルでアダプティブ カードを変換して、独自の強化されたユーザー エクスペリエンスを提供する方法を理解できるようになりました。

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a>アダプティブ カードと新しいユニバーサル アクション モデル

アダプティブ カードは、テキストやグラフィックスなどのコンテンツと、ユーザーが実行できるアクションの組み合わせです。 詳細については「[アダプティブ カード](http://adaptivecards.io/)」を参照してください。 アダプティブ カードの新しいユニバーサル アクションを使用すると、プラットフォームやアプリケーション間でアダプティブ カード アクションを一般的に処理できます。 詳細については、「[ユニバーサル アクション モデル](/adaptive-cards/authoring-cards/universal-action-model)」を参照してください。

[クイック スタート ガイド](Work-with-universal-actions-for-adaptive-cards.md)を使用してシナリオを更新し、ユニバーサル アクションを活用することから始めることができます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)

## <a name="see-also"></a>関連項目

* [ボットとは](~/bots/what-are-bots.md)
* [アダプティブ カードの概要](~/task-modules-and-cards/what-are-cards.md)
* [アダプティブ カード @ Microsoft ビルド 2020](https://youtu.be/hEBhwB72Qn4?t=1393)
* [アダプティブ カード @ Ignite 2020](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)
