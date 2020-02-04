---
title: 公開開発者プレビューの機能
description: Microsoft Teams の公開開発者プレビューの機能について説明します。
keywords: teams のプレビュー開発者向け機能
ms.openlocfilehash: abec097d9f3b6fb48a4a50cb26d73cf811151149
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674654"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft Teams の公開開発者プレビューの機能

開発者プレビューには、次の新機能が含まれています。

## <a name="mention-support-in-adaptive-cards"></a>アダプティブカードでのサポートを説明します。

ボットとメッセージング拡張機能の応答に対して、アダプティブカードの本文内に @ メンションを追加できるようになりました。 カードの @ メンションは、通常のメッセージベースのメンションと同じ通知ロジックに従い、レンダリングします。 なお、カードベースのメンションは、現在 Web およびデスクトップクライアントでのみサポートされており、近日中にモバイルクライアントでのレンダリングをサポートしています。

## <a name="adaptive-12-support"></a>アダプティブ1.2 サポート

Microsoft Teams では、開発者向けプレビューで[アダプティブバージョン 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)がサポートされるようになりました。 [メディア要素](https://adaptivecards.io/explorer/Media.html)はまだサポートされていないことに注意してください。

## <a name="tabs-single-sign-on"></a>タブシングルサインオン

[シングルサインオン (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md)を使用して、デスクトップおよびモバイルでユーザーのログインと認証を行うことができます。これには、web コンテンツページから TEAMS JavaScript SDK を使用します。 利点の1つは、ユーザーがサインインする必要がないことです。また、プロファイルを使用してアプリに同意されると、そのタブ (mobile を含む) に自動的にサインインします。

開発者向けプレビューは、1.5 以上のマニフェストバージョンで利用できます。 現在の実装では、限られた量のグラフ Api しか取得できませんが、既存の認証 API を使用して追加の Graph Api を取得するための回避策を提供しています。

## <a name="personal-apps-static-tabs-and-1-1-bots-enabled-on-mobile"></a>モバイルで有効になっている個人用アプリ (静的タブと1-1 ボット)

インストールされている個人用アプリ (静的タブと1-1 ボット) は、モバイルデバイスのアプリトレイで利用できるようになりました。 設計ガイダンスについては、「[モバイルの設計ガイドライン](~/tabs/design/tabs-mobile.md)」を参照してください。 アプリは、デスクトップまたは web クライアントからのみインストールでき、インストール後にモバイルで利用できるようになるまで最大4時間かかることがあります。

これには、システム管理者が[アプリのセットアップポリシー](/microsoftteams/teams-app-setup-policies)を使用してアプリを事前にピン留めする機能が含まれます。 固定されたアプリは、アプリのドロアーに表示されます。

## <a name="calls-and-online-meeting-bots"></a>通話とオンライン会議のボット

Microsoft [Graph api を呼び出しとオンライン会議に](/graph/api/resources/communications-api-overview?view=graph-rest-beta)追加することで、microsoft Teams アプリは音声とビデオを使用してさまざまな方法でユーザーと対話できるようになりました。 これらの Api を使用すると、対話式音声応答 (IVR)、通話コントロール、通話と会議のリアルタイムの音声/ビデオストリームへのアクセス、デスクトップやアプリの共有など、新しいアプリ機能を追加できます。

通話とオンライン会議のボットを作成して開発する方法について、[概要](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)から始まる新しいセクションを追加しました。
