---
title: 受信 Webhook を作成する
author: laujan
description: 受信 Webhook をアプリに追加し、Teams Webhook を使用して外部要求をTeamsする方法について説明します。
keywords: teams タブ送信 Webhook
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 7ce63a8456eaa0b15bd03999dd06c202ee689113
ms.sourcegitcommit: ba911ce3de7d096514f876faf00e4174444e2285
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2021
ms.locfileid: "61178301"
---
# <a name="create-incoming-webhook"></a>受信 Webhook の作成

受信 Webhook を使用すると、外部アプリがチャネル内のコンテンツTeamsできます。 これらの Webhook は、追跡および通知ツールとして使用されます。 これらは一意の URL を提供し、カード形式のメッセージを含む JSON ペイロードを送信します。 カードは、1 つのトピックに関連するコンテンツとアクションを含むユーザー インターフェイス コンテナーです。 Teams機能内でカードを使用します。

* ボット
* メッセージング拡張機能
* コネクタ

## <a name="key-features-of-incoming-webhook"></a>受信 Webhook の主な機能

次の表に、受信 Webhook の機能と説明を示します。

| 機能 | 説明 |
| ------- | ----------- |
|受信 Webhook を使用したアダプティブ カード|アダプティブ カードは、受信 Webhooks 経由で送信できます。 詳細については、「受信 [Webhooks を使用してアダプティブ カードを送信する」を参照してください](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)。|
|アクション可能なメッセージングのサポート|アクション可能なメッセージ カードは、Teams を含むすべての Office 365 グループでサポートされています。 カードを介してメッセージを送信する場合は、操作可能なメッセージ カード形式を使用する必要があります。 詳細については、「従来の操作可能な [メッセージ カード参照と](/outlook/actionable-messages/message-card-reference) メッセージ カード [のプレイグラウンド」を参照してください](https://messagecardplayground.azurewebsites.net)。|
|独立した HTTPS メッセージングのサポート|カードは、情報を明確に一貫して提供します。 HTTPS POST 要求を送信できるツールまたはフレームワークは、受信 Webhook を介してTeamsにメッセージを送信できます。|
|Markdown のサポート|アクション可能なメッセージング カードのすべてのテキスト フィールドで、基本的な Markdown がサポートされています。 カードで HTML マークアップを使用しない。 HTML は無視され、プレーン テキストとして扱われます。|
|スコープ構成|受信 Webhook はスコープ設定され、チャネル レベルで構成されます。|
|セキュリティで保護されたリソース定義|メッセージは JSON ペイロードとして書式設定されます。 この宣言型メッセージング構造は、悪意のあるコードの挿入を防止します。|

> [!NOTE]
> * Teams、メッセージング拡張機能、受信 Webhook、およびボット フレームワークはアダプティブ カードをサポートします。 アダプティブ カードは、オープン クロス カード プラットフォーム フレームワークであり、Windows、Android、iOS など、すべてのプラットフォームで使用できます。 現在、Teams[は](../../webhooks-and-connectors/how-to/connectors-creating.md)アダプティブ カードをサポートされていません。 ただし、アダプティブ カードを[チャネルに投稿](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)するフローをTeamsできます。
> * カードと Webhook の詳細については、「アダプティブ カード [と受信 Webhooks」を参照してください](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)。

## <a name="create-incoming-webhook"></a>受信 Webhook の作成

**受信 Webhook を新しいチャネルにTeamsするには**

1. Webhook を追加するチャネルに移動し、上部の &#8226;&#8226;&#8226; から [その他 **の** オプション] を選択します。
1. ドロップダウン **メニューから [** コネクタ] を選択します。

    ![コネクタの選択](~/assets/images/connectors.png)

1. 受信 **Webhook を検索し、[** 追加] を **選択します**。
1. [ **構成]** を選択し、名前を指定し、必要に応じて webhook の画像をアップロードします。

    ![[構成] ボタン](~/assets/images/configure.png)

1. ダイアログ ウィンドウには、チャネルにマップされる一意の URL が表示されます。 Webhook URL をコピーして保存し、ユーザーに情報を送信Microsoft Teamsし、[完了] を **選択します**。

    ![一意の URL](~/assets/images/url.png)

Webhook は、webhook チャネルTeamsできます。

> [!NOTE]
> [Teams] で、[設定メンバーのアクセス許可] [コネクタの作成、更新、および削除をメンバーに許可する] を選択して、チーム メンバーがコネクタを追加、変更、または削除できます  >    >  。

## <a name="remove-incoming-webhook"></a>受信 Webhook の削除

**受信 Webhook をチャネルからTeamsするには**

1. チャネルに移動します。
1. 上部 &#8226;&#8226;&#8226; **バーから [その他のオプション** ] を選択します。
1. ドロップダウン **メニューから [** コネクタ] を選択します。
1. 左側の [管理] で **、[構成** 済み] を **選択します**。
1. [構成 **< *済みの 1*>] を** 選択して、現在のコネクタの一覧を表示します。

    ![構成済みの Webhook](~/assets/images/configured.png)

1. 削除 **するコネクタ** の横にある [管理] を選択します。

    ![Webhook の管理](~/assets/images/manage.png)

1. [削除 **] を選択します**。

    ![Webhook を削除する](~/assets/images/remove.png)

    [ **構成の削除]** ダイアログ ボックスが表示されます。

    ![構成の削除](~/assets/images/removeconfiguration.png)

1. ダイアログ ボックスのフィールドとチェック ボックスを入力し、[削除] を **選択します**。

    ![最終的な削除](~/assets/images/finalremove.png)

    webhook は、チャネルからTeamsされます。

## <a name="see-also"></a>関連項目

* [送信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)
* [[Teams で共有] ボタンを作成する](../../concepts/build-and-test/share-to-teams.md#create-share-to-teams-button)
* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
