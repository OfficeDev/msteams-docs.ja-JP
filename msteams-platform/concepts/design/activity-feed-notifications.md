---
title: アクティビティ フィード通知の設計
author: heath-hamilton
description: Teams アプリのアクティビティ フィード通知を設計し、Teams UI キットを取得する方法について説明します。 Visual Studio C で Teams チャネルからの通知を開発する#
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 923519965b5ae6debaf256032f9bc4cdaada2f6e
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558010"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのアクティビティ フィード通知の設計

アクティビティ フィードは、ユーザーが Microsoft Teams で通知にアクセスするための画面です。 フィードには、過去 4 週間の通知が保持されます。

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="例は、モバイル上の Teams アクティビティ フィードに表示されるアプリ通知を示しています。":::

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="例は、Teams アクティビティ フィードに表示されるアプリ通知を示しています。":::

---

## <a name="anatomy"></a>構造

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Teams アクティビティ フィード通知の設計構造。":::

|カウンター|説明|
|----------|-----------|
|1|**アバター**: アクティビティを開始したユーザーを示します。|
|2|**[アクティビティの種類/アプリ] アイコン**: アクティビティの種類を示します。 アプリ通知の場合、行アイコンはアプリ アイコンに置き換えられます。|
|3|**タイトル (1 行目): アクター + 理由**: *アクター*: アクティビティを開始したユーザーまたはアプリの名前。 *理由*: アクティビティについて説明します。|
|4|**タイムスタンプ**: アクティビティがいつ発生したかを示します。|
|5|**場所 (2 行目)**: Teams でアクティビティが発生した場所を示します。|
|6 |**テキスト プレビュー (3 行目)**: 通知の先頭から切り捨てられた行を表示します。|

## <a name="types-of-activity-feed-notification-cards"></a>アクティビティ フィード通知カードの種類

次のバリエーションは、表示できるアクティビティ フィード通知カードの種類を示しています。 アプリロゴは、アプリによって生成された通知のユーザー アバターに置き換えられます。

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Teams アクティビティ フィード カードのバリエーション。":::

## <a name="manage-activity-feed-notifications"></a>アクティビティ フィードの通知を管理する

ユーザーは、Teams 設定ページでアプリから送信された通知を管理できます。

## <a name="related-system-notifications"></a>関連するシステム通知

各アクティビティは、システム通知を生成します。 表示内容は、ユーザーが通知設定で構成する内容によって異なります。 ユーザーは、オペレーティング システムに基づいて通知スタイルを選択することもできます。

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Android と iOS 上の Teams アクティビティ フィード カードのバリエーション。":::

|カウンター|説明|
|----------|-----------|
|1|Android|
|2|iOS|

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="さまざまなオペレーティング システム上の Teams アクティビティ カードのバリアント。":::

|カウンター|説明|
|----------|-----------|
|1|Teams カスタム|
|2|Windows|
|3|Mac|

---

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アクティビティ フィード通知を実装する](/graph/teams-send-activityfeednotifications)
