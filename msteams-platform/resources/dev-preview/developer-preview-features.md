---
title: パブリック サーバーの機能Developer Preview
description: Microsoft Teams の一般のパブリック コンテンツDeveloper Previewについて説明します
keywords: Teams のプレビュー開発者向け機能
ms.openlocfilehash: e607a6c65253a5fd94f8a805f1264a567bb8fd24
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819176"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft Teams のパブリック web サイトDeveloper Preview機能

開発者プレビューには、次の新機能が含まれています。

## <a name="adaptive-cards-v12-support"></a>アダプティブ カード v1.2 のサポート

Teams での [アダプティブ カード v1.2 の](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) サポートが、一般のパブリックで利用可能になりました。 ただし [、Teams プラットフォームの](https://adaptivecards.io/explorer/Media.html) アダプティブ カード v1.2 では、現在、Media 要素はサポートされていません。

## <a name="tabs-single-sign-on-sso"></a>タブ シングル サインオン (SSO)

シングル サインオン [(SSO) を使用して、Web コンテンツ](~/tabs/how-to/authentication/auth-aad-sso.md) ページからの Teams JavaScript SDK を使用して、デスクトップおよびモバイル上のユーザーのログインおよび認証を行うことができるようになりました。 その利点の 1 つに、ユーザーがサインインする必要がないことです。プロファイルを使ってアプリに同意した後は、そのタブ (モバイルを含む) に自動的にサインインします。

当社の開発者プレビューは、1.5 以降のマニフェスト バージョンで利用可能です。 現在の実装では、限定された量の Graph API しか取得できませんが、既存の認証 API を使用して追加の Graph API を取得するための回避策が提供されています。

## <a name="calls-and-online-meeting-bots"></a>通話ボットとオンライン会議ボット

通話およびオンライン会議 [用の Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta)が追加されているため、Microsoft Teams アプリは、音声やビデオを使用して豊富な方法でユーザーと対話できるようになりました。 これらの API を使用すると、インタブル音声応答 (IVR)、通話コントロール、通話や会議でのリアルタイムのオーディオやビデオ ストリームへのアクセスなどの新しいアプリ機能 (デスクトップやアプリの共有など) を追加できます。

通話およびオンライン会議ボットの作成方法について、概要から新しいセクションが追加 [されました](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。
