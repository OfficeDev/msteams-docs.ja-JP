---
title: アプリを構築するための Teams ソリューション
author: heath-hamilton
description: Microsoft 365 の計画、設計、構築、拡張、テスト、配布、収益化、および Teams との統合を行う方法について説明します。
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 11/02/2021
ms.openlocfilehash: ac4f3a208484a093460a14777a351aa4abc10af7
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100785"
---
# <a name="the-teams-solution"></a>Teams ソリューション


Microsoft Teams プラットフォームは、Teams 用のアプリを作成するための強力かつ柔軟性のあるプラットフォームです。 アプリ開発をサポートする膨大な開発環境とツールのスイートを提供します。

## <a name="the-user-story"></a>ユーザー ストーリー

Teams のプランのビューが表示されました。 ユーザーのニーズに対応付けることができるようになりました。 シナリオをもう一度見てみましょう。

ツアーおよび旅行会社の開発者は、ユーザーである旅行者向けのアプリを構築したいと考えています。 アプリでは、次の手順を実行する必要があります:

- 旅行業者に登録されている旅行者に予報を確認して送信します。
- 計画できるように、出発日の前日にユーザーに通知します。

要件を照合し、Teams の機能にマップします。

| ユーザー アプリのニーズ | 予報を確認する | 旅行前の通知 | 登録済みユーザー |
| --- |:---:|:---:|:---:|
| **機能** | Bot | &nbsp; | &nbsp; |
| **統合** | &nbsp; | &nbsp; | :::image type="icon" source="assets/icons/microsoft-icon.png"::: Microsoft Graph、天気 API |
| **スコープ** | &nbsp; | 個人用アプリ | &nbsp; |
| **統合ポイント** | &nbsp; | チャット | &nbsp; |

**Teams アプリ ソリューション**: 個人チャット ボットアプリTeams で、旅行日より前に *登録ユーザー* に *予報通知を確認して送信* する Teams の *個人用チャット ボット*。

:::image type="content" source="../msteams-platform/assets/images/overview/developer-scenario-solution.png" alt-text="旅行会社の開発者は、旅行日よりも前に計画できるように、天気予報を顧客に送信する Teams 用のボットを構築します":::

Teams offers these and many more capabilities to bring your users a feature-rich app solution. To develop this app:

1. 個人用チャット ボット アプリを作成します。
1. 外部の天気予報 API と統合して接続し、特定の日付と場所の予報を要求します。
1. 登録済みユーザーの :::image type="icon" source="assets/icons/teams-icon.png"::: Microsoft Graph と統合します。
1. ユーザーの旅行日と旅行先の場所に基づいて、予報の詳細を確認して送信します。

## <a name="choose-what-suits-you"></a>自分に合ったものを選ぶ

アプリの要件に従って Teams アプリを構築できます。 ビジネス ニーズ、開発環境、ドメイン ナレッジなどの要因に基づいて、アプリを構築する環境とツールを選択します。

Teams アプリを使用すると、ビルド環境を柔軟に選択できます。 これには、アプリ開発に取り組むツール、フレームワーク、言語が含まれています。

:::image type="content" source="../msteams-platform/assets/images/overview/tools-of-your-choice.png" alt-text="ビジネス ニーズ アプリ":::

Build your Teams app in the environment that works for your particular requirements. You can even select a combination.

たとえば、Teams ツールキットを使用して JavaScript を使用してアプリをビルドし、SharePoint サイトでホストできます。

## <a name="teams-collaborative-platform"></a>Teams コラボレーション プラットフォーム

Teams アプリを使用すると、ユーザーはコラボレーション ワークスペースの利点を利用できます。

Teams は、アプリを構築するためのプラットフォームとして、さまざまなアプリとツールキットを提供します。 Teams プラットフォームは、アプリの計画から配布まで、あらゆる段階でサポートします。

:::image type="content" source="../msteams-platform/assets/images/overview/teams-dev-life-cycle.png" alt-text="Teams アプリ開発のライフ サイクルを説明します。計画、設計、ビルド、拡張、テスト、デプロイ、配布を以下に箇条書きにします。":::

From designing to building and distributing a Teams app, you can use various tools and services. An example development flow can be:

1. プロジェクトを計画し、要件を把握します。
1. Design the app. Use Teams UI Kit and UI Library for designing tabs UI.
1. Teams ツールキットを使用して JavaScript を使用してアプリを構築します。
1. :::image type="icon" source="assets/icons/microsoft-icon.png"::: Microsoft Graph を使用して、さらに Teams の機能と M365 データを追加して、機能を拡張します。
1. サンプル ユーザー データを使用して開発者テナントでアプリをテストします。
1. アプリを Azure にデプロイします。
1. 開発者ポータルを使用してアプリを管理し、ストアに公開します。 SaaS オファー、アプリ内購入などのオプションを使用してアプリを収益化します。

## <a name="next-step"></a>次の手順

:::row:::
    :::column span="1":::
        **構築の開始**
    :::column-end:::
    :::column span="2":::
        シンプルなアプリの作成や、一般的な機能の追加を通して、Teams 用アプリの作成にすばやく慣れていきましょう。

        > [!div class="nextstepaction"]
        > [初めてのアプリを構築する](get-started/get-started-overview.md)
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>関連項目

:::row:::
    :::column span="1":::
        **アプリを計画する**
    :::column-end:::
    :::column span="2":::
        アプリのユース ケースを理解し、Teams の機能にマップします。

        > [!div class="nextstepaction"]
        > [アプリを計画する](~/concepts/app-fundamentals-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **アプリをデザインする**
    :::column-end:::
    :::column span="2":::
        Teams UI Kit を使用してアプリ UI を設計します。

        > [!div class="nextstepaction"]
        > [Teams アプリを設計する](~/concepts/design/design-teams-app-process.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **アプリを作成する**
    :::column-end:::
    :::column span="2":::
        Looking for app development inspiration? Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways a Teams app can help your users.

        > [!div class="nextstepaction"]
        > [アプリのシナリオを見る](https://adoption.microsoft.com/en-us/extensibility-look-book-gallery/)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **アプリを Microsoft 365 全体に拡張する**
    :::column-end:::
    :::column span="2":::
Teams JavaScript クライアント SDK v2 Preview を使用すると、他の高使用率 Microsoft 365 エクスペリエンスで実行されている Teams アプリをプレビューできます。

        > [!div class="nextstepaction"]
        > [アプリを拡張する](m365-apps/overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **アプリのテスト**
    :::column-end:::
    :::column span="2":::
        アプリを Teams と統合した後、アプリを発行する前にテストする必要があります。

        > [!div class="nextstepaction"]
        > [アプリのテスト](concepts/build-and-test/test-app-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **アプリを配布する**
    :::column-end:::
    :::column span="2":::
        Teams アプリは、個人、チーム、組織、またはそれを使用する任意のユーザーに提供できます。

        > [!div class="nextstepaction"]
        > [アプリを配布する](~/concepts/deploy-and-publish/apps-publish-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **アプリを収益化する**
    :::column-end:::
    :::column span="2":::
        Teams ストアは、SaaS オファーやアプリ内購入などのアプリの収益化オプションを提供します。 Teams アプリに最適な収益化オプションを選択してください。

        > [!div class="nextstepaction"]
        > [アプリを収益化する](concepts/deploy-and-publish/appsource/prepare/monetize-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Teams との統合**
    :::column-end:::
    :::column span="2":::
        ユーザーが慣れ親しんでいる既存の Web アプリ、サービス、システムの機能と Teams のコラボレーション機能を融合させましょう。

        > [!div class="nextstepaction"]
        > [既存のアプリを統合する](samples/integrating-web-apps.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **小さなコードが大きな意味を持つ**
    :::column-end:::
    :::column span="2":::
        You don't need to be an expert programmer to build a great Teams app. Try one of several low-code solutions.

        > [!div class="nextstepaction"]
        > [ローコード アプリの作成](samples/teams-low-code-solutions.md)
    :::column-end:::
:::row-end:::
