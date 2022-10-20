---
title: 受信 Webhook を作成する
author: laujan
description: Teams アプリに着信 Webhook を作成し、Teams に外部要求を投稿します。 着信 Webhook を削除します。 着信 Webhook を使用してカードを送信するサンプル コード(C#,Node.js)。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 5f6aef184805aa4ef7a68eac827b08fa8d4c12f1
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615332"
---
# <a name="create-incoming-webhooks"></a>受信 Webhook を作成する

受信 Webhook を使用すると、外部アプリケーションからのコンテンツを Teams チャネル内で共有できるようになります。 Webhook は、追跡と通知を行うツールとして使用されます。 Webhook により、カード形式のメッセージを含む JSON ペイロードを送信するための一意の URL が提供されます。 カードは、1 つのトピックに関連するコンテンツとアクションを含むユーザー インターフェイス コンテナーです。 カードは、次の機能で使用できます。

* ボット
* メッセージ拡張機能
* コネクタ

> [!IMPORTANT]
> 受信 Webhook 以外の通知ボット Teams アプリを作成することもできます。 同様に実行されますが、通知ボットにはより多くの機能があります。 詳細については、「JavaScript または[受信 Webhook 通知サンプル](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification)[を使用した通知ボットのビルド](../../sbs-gs-notificationbot.yml)」を参照してください。 作業を開始するには、 [Teams Toolkit を](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) 今すぐダウンロードし、調査します。 詳細については、「 [Teams Toolkit ドキュメント」を](../../toolkit/teams-toolkit-fundamentals.md)参照してください。

受信 Webhook を作成する方法については、次のビデオを参照してください。
<br>
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4ODcY]

## <a name="key-features-of-an-incoming-webhook"></a>受信 Webhook の主な機能

次の表に、受信 Webhook の機能と説明を示します。

| 機能 | 説明 |
| -------- | ----------- |
|受信 Webhook を使用したアダプティブ カード | アダプティブ カードは、受信 Webhook を介して送信できます。 詳細については、「[受信 Webhookを使用してアダプティブ カードを送信する](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)」を参照してください。|
|アクション可能なメッセージングのサポート|アクション可能なメッセージ カードは、Teams を含むすべての Office 365 グループでサポートされています。 カード経由でメッセージを送信する場合は、アクション可能なメッセージ カード形式を使用する必要があります。 詳細については、「[従来の操作可能なメッセージ カード リファレンス](/outlook/actionable-messages/message-card-reference)」と「[メッセージ カードのプレイグラウンド](https://messagecardplayground.azurewebsites.net)」を参照してください。|
|独立した HTTPS メッセージングのサポート|Cards provide information clearly and consistently. Any tool or framework that can send HTTPS POST requests can send messages to Teams through an Incoming Webhook.|
|Markdown のサポート|アクション可能なメッセージング カードのすべてのテキスト フィールドで、基本的な Markdown がサポートされています。 カードで HTML マークアップを使用しないでください。 HTML は無視され、プレーン テキストとして扱われます。|
|スコープ構成|受信 Webhook のスコープが設定され、チャネル レベルで構成されます。|
|セキュリティで保護されたリソース定義|メッセージは JSON ペイロードとして書式設定されます。 この宣言型メッセージング構造は、悪意のあるコードの挿入を防ぎます。|

<!--- TBD: A note should be short and eye-catching. No need to put a list item inside a Note or any admonition for that matter. Re-write the below list item.
--->

> [!NOTE]
>
> * Teams ボット、メッセージング拡張機能、受信 Webhook、およびBot Frameworkは、アダプティブ カードをサポートします。 アダプティブ カードは、Windows、Android、iOS などのすべてのプラットフォームで使用されているオープン なクロス カード プラットフォーム フレームワークです。 現時点では、 [Teams コネクタ](../../webhooks-and-connectors/how-to/connectors-creating.md) はアダプティブ カードをサポートしていません。 ただし、Teams チャネルにアダプティブ カードを投稿する [フロー](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) を作成することはできます。
> * カードと Webhook の詳細については、「[アダプティブ カード と受信 Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)」を参照してください。

## <a name="create-an-incoming-webhook"></a>受信 Webhook を作成する

Teams チャネルに受信 Webhook を追加するには、次の手順に従います。

1. Webhook を追加するチャネルを開き、上部のナビゲーション バーから &#8226;&#8226;&#8226; **[その他のオプション]** を選択します。
1. ドロップダウン メニューから **コネクタ** を選択します。

   :::image type="content" source="../../assets/images/connectors.png" alt-text="このスクリーンショットは、コネクタを選択する方法を示しています。":::

1. **受信 Webhook** を検索し、**[追加]** 選択します。
1. **[構成］** を選択して名前を指定し、必要に応じて Webhook のイメージをアップロードします。

   :::image type="content" source="../../assets/images/configure.png" alt-text="このスクリーンショットは、Webhook のイメージを構成してアップロードする方法を示しています。":::

1. ダイアログ ウィンドウに表示される一意の Webhook URL をコピーして保存します。 URL はチャネルにマッピングされ、それを使用して Teams に情報を送信することができます。 **[完了]** を選択します。

   :::image type="content" source="../../assets/images/url.png" alt-text="このスクリーンショットは、一意の Webhook URL を示しています。":::

Webhook は Teams チャネルで利用できます。

受信 Webhook または Office 365 コネクタを使用して、操作可能なメッセージを作成して送信できます。 詳細については、「[メッセージの作成と送信](~/webhooks-and-connectors/how-to/connectors-using.md)」を参照してください。

> [!NOTE]
> Teams で、[**設定]** > **[メンバーのアクセス許可** > **メンバーがコネクタを作成、更新、削除できるようにする]** を選択して、チーム メンバーがコネクタを追加、変更、または削除できるようにします。

## <a name="remove-an-incoming-webhook"></a>受信 Webhook を削除する

Teams チャネルから受信 Webhook を削除するには、次の手順に従います。

1. チャネルを開き、上部のナビゲーション バーから &#8226;&#8226;&#8226; **[その他のオプション]** を選択します。
1. ドロップダウン メニューから **コネクタ** を選択します。
1. **[管理]** で **[構成済み]** を選択します。
1. **<*1*>構成済み** を選択して、現在のコネクタの一覧を表示します。

   :::image type="content" source="../../assets/images/configured.png" alt-text="このスクリーンショットは、現在のコネクタの一覧を表示するように構成する方法を示しています。":::

1. 削除するコネクタの **[管理]** を選択します。

   :::image type="content" source="../../assets/images/manage.png" alt-text="このスクリーンショットは、削除するコネクタを管理する方法を示しています。":::

1. **[削除 ]** を選択して、**[構成の削除]** ダイアログ ボックスを表示します。

   :::image type="content" source="../../assets/images/removeconfiguration.png" alt-text="このスクリーンショットは、[構成の削除] ダイアログ ボックスを表示する方法を示しています。":::

1. ダイアログ ボックスのフィールドに入力し、チェックボックスをオンにし、**[削除]** を選択します。

   :::image type="content" source="../../assets/images/finalremove.png" alt-text="このスクリーンショットは、Teams チャネルから受信 Webhook を削除する方法を示しています。":::

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | C#    |  TypeScript |
|:---------------------|:--------------|:---------|:--------|
|着信 Webhook|このサンプル コードでは、受信 Webhook を使用してカードを送信する方法を示します。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/incoming-webhook/csharp)|[表示](https://github.com/OfficeDev/TeamsFx-Samples/tree/release/incoming-webhook-notification) |

## <a name="see-also"></a>関連項目

* [送信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Web アプリから Teams に共有する](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
* [Azure Logic Apps でアクセスとデータをセキュリティ保護する](/azure/logic-apps/logic-apps-securing-a-logic-app)
* [JavaScript を使用した通知ボットのビルド](../../sbs-gs-notificationbot.yml)
* [JavaScript を使用して初めてのボット アプリを構築する](../../sbs-gs-bot.yml)
