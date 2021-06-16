---
title: 開発者ポータルでアプリを管理する
description: 開発者ポータルを使用してアプリを管理する方法について説明Microsoft Teams。
keywords: 開発者ポータル チームの開始
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 6dca8723248441c3cf672931295b4b68e02cc24c
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949687"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>開発者ポータルを使用してアプリを管理Microsoft Teams

> [!NOTE]
> 開発者向け開発者ポータル Teamsパブリック開発者[プレビュー中です](~/resources/dev-preview/developer-preview-intro.md)。

開発者<a href="https://dev.teams.microsoft.com" target="_blank">ポータルは、Teams</a>アプリを構成、配布、および管理するための主要なMicrosoft Teamsです。 開発者ポータルを使用すると、アプリの同僚と共同作業を行い、ランタイム環境をセットアップできます。

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="開発者ポータルのホーム ページを示すスクリーンショットTeams。":::

## <a name="register-an-app"></a>アプリを登録します

開発者ポータルには、アプリを登録するためのいくつかのTeamsがあります。

* ブランドの新しいアプリを登録する
* 既存のアプリ パッケージをインポートする

> [!NOTE]
> アプリを作成する場合は、Microsoft Teams Toolkit[を](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)Visual Studio Code、開発者ポータルでそのアプリを管理できます。

## <a name="set-up-an-environment"></a>環境のセットアップ

環境とグローバル変数を構成して、アプリをローカル ランタイムから実稼働環境に移行できます。 グローバル変数は、すべての環境で使用されます。

**環境をセットアップするには**

1. 開発者ポータルで、作業しているアプリを選択します。
2. [環境] ページ **に移動し** 、[+ 環境 **の追加] を選択します**。
3. [+ **変数の追加] を** 選択して、環境の構成変数を作成します。

**変数を使用するには**

アプリの構成を設定するには、ハードコードされた値の代わりに変数名を使用します。

1. 開発者 `{{` ポータルの任意のフィールドに入力します。 選択した環境に対して作成した変数とグローバル変数のドロップダウンが表示されます。  
1. アプリ パッケージをダウンロードする前に (たとえば、Teams ストアに発行する準備が整った場合)、使用する環境を選択します。 アプリの構成は、環境に基づいて自動的に更新されます。 

## <a name="identify-app-owners"></a>アプリの所有者を特定する

各アプリには **[所有者] ページが** 含まれています。このページでは、組織の同僚とアプリ登録を共有できます。 **共同作成者の** 役割は、アプリを削除する機能を除き **、所有者** ロールと同じアクセス許可を持っています。

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>アプリの機能と他の重要なメタデータを構成する

アプリTeams Web アプリです。 すべての Web アプリと同様に、ソース コードは通常、IDE またはコード エディターで開発され、クラウドのどこか (Azure など) でホストされます。

アプリをインストールしてレンダリングするには、Teams認識する一連の構成Teams必要があります。 これは、アプリ のコンテンツを表示するために必要なすべてのメタデータを含む JSON ファイルであるアプリ マニフェストTeams作成することで行われ始めでした。 開発者ポータルでは、このプロセスを抽象化し、より成功するための新機能とツールが含まれています。

## <a name="test-your-app-directly-in-teams"></a>アプリをアプリで直接テストTeams

開発者ポータルには、アプリをテストおよびデバッグするためのオプションがあります。

* [概要 **] ページ** では、アプリの構成がストア テスト ケースに対して検証Teams確認できます。
* [**プレビューイン Teams]** ボタンを使用すると、デバッグ用にアプリを Teamsすぐに起動できます。

## <a name="distribute-your-app"></a>アプリを配布する

開発者ポータルから、[配布]ボタンを使用して、アプリ パッケージをダウンロードしたり、組織に発行したり、組織に発行したり、Teamsします。

詳細については、「アプリの[配布」をTeamsしてください](~/concepts/deploy-and-publish/apps-publish-overview.md)。

## <a name="analyze-your-apps-usage"></a>アプリの使用状況を分析する

[概要 **] ページ** で、アプリのアクティブなユーザーの総数を確認できます。 これらの指標は、開発者ポータルを通じて Teamsストアまたは組織のアプリ カタログに発行され、アプリ ID にスコープを設定したアプリで使用できます。

| 測定基準 | 定義 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *月次 R30* | 既定の使用状況メトリック。 UTC の 30 日間のローリング ウィンドウ内でアプリを使用した一意のアクティブ ユーザーの数が表示されます。 |
| *毎日* | UTC で特定の日にアプリを使用した一意のアクティブ ユーザーの数を示します。 |

過去 7 日間、30 日間、および 60 日間の月次および毎日の使用状況が表示されます。 24 ~ 48 時間以内に、特定の日の使用状況が反映されます。 新しいアプリの使用状況は、表示に最大で 3 ~ 5 日かかる場合があります。

## <a name="use-tools-to-create-app-features"></a>ツールを使用してアプリ機能を作成する

また、開発者ポータルには、アプリの主要な機能を構築するためのTeamsがあります。 これらのツールの一部は次のとおりです。

* **シーン スタジオ**: 会議 [のカスタム一](~/apps-in-teams-meetings/teams-together-mode.md)緒にモード のTeamsします。
* **アダプティブ カード エディター**: アプリに含めるアダプティブ カードを作成およびプレビューします。
* **Microsoft ID プラットフォーム管理**: アプリを Azure Active Directory (Azure AD) に登録して、ユーザーがサインインして API へのアクセスを提供します。
