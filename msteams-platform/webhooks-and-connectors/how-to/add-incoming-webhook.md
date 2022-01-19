---
title: 受信 Webhook を作成する
author: laujan
description: では、Teams アプリに受信 Webhook を追加し、受信 Webhook を使用して Teams に外部要求を投稿する方法について説明します
keywords: teams タブの送信 Webhook
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 308eaf9f08e946f468f02d897ad556681d1cc832
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059764"
---
# <a name="create-incoming-webhook"></a>受信 Webhook の作成

受信 Webhook を使用すると、すべての外部アプリが Teams チャネルでコンテンツを共有できます。 これらの Webhook は、追跡および通知ツールとして使用されます。 一意の URL を提供し、カード形式のメッセージを含む JSON ペイロードを送信します。 カードは、1 つのトピックに関連するコンテンツとアクションを含むユーザー インターフェイス コンテナーです。 Teams では、次の機能内でカードが使用されます。

* ボット
* メッセージング拡張機能
* コネクタ

## <a name="key-features-of-incoming-webhook"></a>受信 Webhook の主な機能

次の表に、受信 Webhook の機能と説明を示します。

| 機能 | 説明 |
| ------- | ----------- |
|受信 Webhook を使用したアダプティブ カード|アダプティブ カードは、受信 Webhook を介して送信できます。 詳細については、「[受信 Webhookを使用してアダプティブ カードを送信する](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)」を参照してください。|
|アクション可能なメッセージングのサポート|アクション可能なメッセージ カードは、Teams を含むすべての Office 365 グループでサポートされています。 カード経由でメッセージを送信する場合は、アクション可能なメッセージ カード形式を使用する必要があります。 詳細については、「[従来の操作可能なメッセージ カード リファレンス](/outlook/actionable-messages/message-card-reference)」と「[メッセージ カードのプレイグラウンド](https://messagecardplayground.azurewebsites.net)」を参照してください。|
|独立した HTTPS メッセージングのサポート|カードは、情報を明確かつ一貫して提供します。 HTTPS POST 要求を送信できるツールまたはフレームワークは、受信 Webhook を介して Teams にメッセージを送信できます。|
|Markdown のサポート|アクション可能なメッセージング カードのすべてのテキスト フィールドで、基本的な Markdown がサポートされています。 カードで HTML マークアップを使用しないでください。 HTML は無視され、プレーン テキストとして扱われます。|
|スコープ構成|受信 Webhook のスコープが設定され、チャネル レベルで構成されます。|
|セキュリティで保護されたリソース定義|メッセージは JSON ペイロードとして書式設定されます。 この宣言型メッセージング構造は、悪意のあるコードの挿入を防ぎます。|

> [!NOTE]
> * Teams ボット、メッセージング拡張機能、受信 Webhook、およびBot Frameworkは、アダプティブ カードをサポートします。 アダプティブ カードは、Windows、Android、iOS などのすべてのプラットフォームで使用できるオープン なクロス カード プラットフォーム フレームワークです。 現時点では、 [Teams コネクタ](../../webhooks-and-connectors/how-to/connectors-creating.md) はアダプティブ カードをサポートしていません。 ただし、Teams チャネルにアダプティブ カードを投稿する [フロー](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) を作成することはできます。
> * カードと Webhook の詳細については、「[アダプティブ カード と受信 Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)」を参照してください。

## <a name="create-incoming-webhook"></a>受信 Webhook の作成

**Teams チャネルに受信 Webhook を追加するには**

1. Webhook を追加するチャネルに移動し、[&#8226;&#8226;&#8226;&#8226;上部のナビゲーション バーから **その他のオプション** を選択します。
1. ドロップダウン メニューから **コネクタ** を選択します。

    ![コネクタの選択](~/assets/images/connectors.png)

1. **受信 Webhook** を検索し、**[追加]** 選択します。
1. [**構成**］を選択し、名前を指定して、必要に応じて Webhook のイメージをアップロードします。

    ![[構成] ボタン](~/assets/images/configure.png)

1. ダイアログ ウィンドウには、チャネルにマップされる一意の URL が表示されます。 Webhook URL をコピーして保存し、Microsoft Teams に情報を送信し、 **[完了]** を選択します。

    ![一意の URL](~/assets/images/url.png)

Webhook は Teams チャネルで利用できます。

受信 Webhook または Office 365 コネクタを使用して、操作可能なメッセージを作成して送信できます。 詳細については、「[メッセージの作成と送信](~/webhooks-and-connectors/how-to/connectors-using.md)」を参照してください。

> [!NOTE]
> Teams で、[**設定]** > **[メンバーのアクセス許可** > **メンバーがコネクタを作成、更新、削除できるようにする]** を選択して、チーム メンバーがコネクタを追加、変更、または削除できるようにします。

## <a name="remove-incoming-webhook"></a>受信 Webhook の削除

**Teams チャネルから受信 Webhook を削除するには**

1. チャネルに移動します。
1. 上部 &#8226;&#8226;&#8226; ナビゲーションバーから [**その他のオプション** ] を選択します。
1. ドロップダウン メニューから **コネクタ** を選択します。
1. 左側の [**管理**] で、[ **構成済み**] を選択します。
1. **<*1*>構成済み** を選択して、現在のコネクタの一覧を表示します。

    ![構成済みの Webhook](~/assets/images/configured.png)

1. 削除したいコネクタの横にある [**管理**] を選択します。

    ![Webhook の管理](~/assets/images/manage.png)

1. **削除** を選択します。

    ![Webhook を削除する](~/assets/images/remove.png)

    [ **構成の削除**] ダイアログ ボックスが表示されます。

    ![構成の削除](~/assets/images/removeconfiguration.png)

1. ダイアログ ボックスのフィールドとチェック ボックスをオンにし、[**削除**]を選択します。

    ![最終削除](~/assets/images/finalremove.png)

    Webhook は Teams チャネルから削除されます。

## <a name="see-also"></a>関連項目

* [送信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)
* [[Teams で共有] ボタンを作成する](../../concepts/build-and-test/share-to-teams.md#create-share-to-teams-button)
* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
