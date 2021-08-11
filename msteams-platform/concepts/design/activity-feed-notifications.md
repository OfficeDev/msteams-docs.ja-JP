---
title: アクティビティ フィード通知の設計
author: heath-hamilton
description: アプリのアクティビティ フィード通知を設計し、Teams UI キットをMicrosoft Teamsする方法について学習します。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 4a2b5510c2e5d0b26897593bbf0fdc0dc493b46ead3be669ff8b72d7cc3970eb
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705150"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>アプリのアクティビティ フィード通知をMicrosoft Teamsする

アクティビティ フィードは、ユーザーが自分の通知にアクセスする画面Microsoft Teams。 フィードは過去 4 週間の通知を保持します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="例では、アクティビティ フィードに表示されるアプリ通知Teams示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="例は、モバイルのアクティビティ フィードのTeamsアプリ通知を示しています。" border="false":::

---

## <a name="anatomy"></a>構造

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="アクティビティ フィード通知のTeams構造を設計します。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アバター**: アクティビティを開始したユーザーを示します。|
|2|**[アクティビティの種類/アプリ] アイコン**: アクティビティの種類を示します。 アプリ通知の場合、行アイコンはアプリ アイコンに置き換わります。|
|3|**タイトル (最初の行): Actor + Reason**: *Actor*: アクティビティを開始したユーザーまたはアプリの名前。 *理由*: アクティビティについて説明します。|
|4 |**タイムスタンプ**: アクティビティが発生した日時を示します。|
|5 |**場所 (2 行目)**: アクティビティが 2 行目で発生した場所Teams。|
|6 |**第 3 の情報 (3 行目)**: オプション。 プレビュー テキストまたは追加情報を表示します。|

## <a name="types-of-activity-feed-notification-cards"></a>アクティビティ フィード通知カードの種類

次のバリアントは、表示できるアクティビティ フィード通知カードの種類を示しています。 アプリロゴは、アプリで生成された通知のユーザー アバターを置き換える。

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="アクティビティ フィード Teamsのバリアント。" border="false":::

## <a name="manage-activity-feed-notifications"></a>アクティビティ フィード通知の管理

ユーザーは、[アプリの設定] ページでアプリから送信Teams管理できます。

## <a name="related-system-notifications"></a>関連するシステム通知

各アクティビティは、システム通知を生成します。 表示される内容は、ユーザーが通知設定で構成する内容によって異なります。 ユーザーは、オペレーティング システムに基づいて通知スタイルを選択できます。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="さまざまなオペレーティング システムTeamsアクティビティ カードのバリアント。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|Teamsカスタム|
|2|Windows|
|3|Mac|

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Android および iOS Teamsアクティビティ フィード カードのバリアント。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|Android|
|2|iOS|

---

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アクティビティ フィード通知の実装](/graph/teams-send-activityfeednotifications)
