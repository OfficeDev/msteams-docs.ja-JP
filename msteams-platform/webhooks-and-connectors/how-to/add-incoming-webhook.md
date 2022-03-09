---
title: 受信 Webhook を作成する
author: laujan
description: 受信 Webhook を Teams アプリに追加し、それを使用して外部要求を Teams に投稿する
keywords: teams タブの送信 Webhook
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8c38d3effd16a445caca72628978d8822e006b30
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355644"
---
# <a name="create-an-incoming-webhook"></a>受信 Webhook を作成する

受信 Webhook を使用すると、外部アプリケーションからのコンテンツを Teams チャネル内で共有できるようになります。 Webhook は、追跡と通知を行うツールとして使用されます。 Webhook により、カード形式のメッセージを含む JSON ペイロードを送信するための一意の URL が提供されます。 カードは、1 つのトピックに関連するコンテンツとアクションを含むユーザー インターフェイス コンテナーです。 カードは、次の機能で使用できます。

* ボット
* メッセージング拡張機能
* コネクタ

## <a name="key-features-of-an-incoming-webhook"></a>受信 Webhook の主な機能

次の表に、受信 Webhook の機能と説明を示します。

| 機能 | 説明 |
| -------- | ----------- |
|受信 Webhook を使用したアダプティブ カード | アダプティブ カードは、受信 Webhook を介して送信できます。 詳細については、「[受信 Webhookを使用してアダプティブ カードを送信する](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)」を参照してください。|
|アクション可能なメッセージングのサポート|アクション可能なメッセージ カードは、Teams を含むすべての Office 365 グループでサポートされています。 カード経由でメッセージを送信する場合は、アクション可能なメッセージ カード形式を使用する必要があります。 詳細については、「[従来の操作可能なメッセージ カード リファレンス](/outlook/actionable-messages/message-card-reference)」と「[メッセージ カードのプレイグラウンド](https://messagecardplayground.azurewebsites.net)」を参照してください。|
|独立した HTTPS メッセージングのサポート|カードでは、情報が明確にかつ一貫性をもって提供されます。HTTPS POST 要求を送信できるツールまたはフレームワークは、受信 Webhook を介して Teams にメッセージを送信できます。|
|Markdown のサポート|アクション可能なメッセージング カードのすべてのテキスト フィールドで、基本的な Markdown がサポートされています。 カードで HTML マークアップを使用しないでください。 HTML は無視され、プレーン テキストとして扱われます。|
|スコープ構成|受信 Webhook のスコープが設定され、チャネル レベルで構成されます。|
|セキュリティで保護されたリソース定義|メッセージは JSON ペイロードとして書式設定されます。 この宣言型メッセージング構造は、悪意のあるコードの挿入を防ぎます。|

<!--- TBD: A note should be short and eye-catching. No need to put a list item inside a Note or any admonition for that matter. Re-write the below list item.
--->

> [!NOTE]
> * Teams ボット、メッセージング拡張機能、受信 Webhook、およびBot Frameworkは、アダプティブ カードをサポートします。 アダプティブ カードは、Windows、Android、iOS などのすべてのプラットフォームで使用されているオープン なクロス カード プラットフォーム フレームワークです。 現時点では、 [Teams コネクタ](../../webhooks-and-connectors/how-to/connectors-creating.md) はアダプティブ カードをサポートしていません。 ただし、Teams チャネルにアダプティブ カードを投稿する [フロー](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) を作成することはできます。
> * カードと Webhook の詳細については、「[アダプティブ カード と受信 Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)」を参照してください。

## <a name="create-an-incoming-webhook"></a>受信 Webhook を作成する

Teams チャネルに受信 Webhook を追加するには、次の手順に従います。

1. Webhook を追加するチャネルを開き、上部のナビゲーション バーから &#8226;&#8226;&#8226; **[その他のオプション]** を選択します。
1. ドロップダウン メニューから **コネクタ** を選択します。

    ![コネクタの選択](~/assets/images/connectors.png)

1. **受信 Webhook** を検索し、**[追加]** 選択します。
1. **[構成］** を選択して名前を指定し、必要に応じて Webhook のイメージをアップロードします。

    ![[構成] ボタン](~/assets/images/configure.png)

1. ダイアログ ウィンドウに表示される一意の Webhook URL をコピーして保存します。 URL はチャネルにマッピングされ、それを使用して Teams に情報を送信することができます。 **[完了]** を選択します。

    ![一意の URL](~/assets/images/url.png)

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

    ![構成済みの Webhook](~/assets/images/configured.png)

1. 削除するコネクタの **[管理]** を選択します。

    ![Webhook の管理](~/assets/images/manage.png)

1. **[削除 ]** を選択して、**[構成の削除]** ダイアログ ボックスを表示します。

    ![構成の削除](~/assets/images/removeconfiguration.png)

1. ダイアログ ボックスのフィールドに入力し、チェックボックスをオンにし、**[削除]** を選択します。

    ![最終削除](~/assets/images/finalremove.png)

## <a name="see-also"></a>関連項目

* [送信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)
* [[Teams で共有] ボタンを作成する](../../concepts/build-and-test/share-to-teams.md#create-share-to-teams-button)
* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
