---
title: 公開開発者プレビューの機能
description: Microsoft Teams の公開開発者プレビューの機能について説明します。
keywords: teams のプレビュー開発者向け機能
ms.openlocfilehash: 7ed442072779917dcc5db3ebcb4afaac9db0407f
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210702"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft Teams の公開開発者プレビューの機能

開発者プレビューには、次の新機能が含まれています。

## <a name="adaptive-cards-v12-support"></a>アダプティブカード1.2 のサポート

Teams での[アダプティブカード](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)v2.0 のサポートは、一般公開されるようになりました。 ただし、 [Media 要素](https://adaptivecards.io/explorer/Media.html)は、Teams プラットフォームのアダプティブカード v2.0 では現在サポートされていません。

## <a name="tabs-single-sign-on-sso"></a>タブシングルサインオン (SSO)

[シングルサインオン (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md)を使用して、デスクトップおよびモバイルでユーザーのログインと認証を行うことができます。これには、web コンテンツページから TEAMS JavaScript SDK を使用します。 利点の1つは、ユーザーがサインインする必要がないことです。また、プロファイルを使用してアプリに同意されると、そのタブ (mobile を含む) に自動的にサインインします。

開発者向けプレビューは、1.5 以上のマニフェストバージョンで利用できます。 現在の実装では、限られた量のグラフ Api しか取得できませんが、既存の認証 API を使用して追加の Graph Api を取得するための回避策を提供しています。

## <a name="personal-apps-static-tabs-and-1-1-bots-enabled-on-mobile"></a>モバイルで有効になっている個人用アプリ (静的タブと1-1 ボット)

インストールされている個人用アプリ (静的タブと1-1 ボット) は、モバイルデバイスのアプリトレイで利用できるようになりました。 設計ガイダンスについては、「[モバイルの設計ガイドライン](~/tabs/design/tabs-mobile.md)」を参照してください。 アプリは、デスクトップまたは web クライアントからのみインストールでき、インストール後にモバイルで利用できるようになるまで最大4時間かかることがあります。

これには、システム管理者が[アプリのセットアップポリシー](/microsoftteams/teams-app-setup-policies)を使用してアプリを事前にピン留めする機能が含まれます。 固定されたアプリは、アプリのドロアーに表示されます。

## <a name="calls-and-online-meeting-bots"></a>通話とオンライン会議のボット

Microsoft [Graph api を呼び出しとオンライン会議に](/graph/api/resources/communications-api-overview?view=graph-rest-beta)追加することで、microsoft Teams アプリは音声とビデオを使用してさまざまな方法でユーザーと対話できるようになりました。 これらの Api を使用すると、対話式音声応答 (IVR)、通話コントロール、通話と会議のリアルタイムの音声/ビデオストリームへのアクセス、デスクトップやアプリの共有など、新しいアプリ機能を追加できます。

通話とオンライン会議のボットを作成して開発する方法について、[概要](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)から始まる新しいセクションを追加しました。
