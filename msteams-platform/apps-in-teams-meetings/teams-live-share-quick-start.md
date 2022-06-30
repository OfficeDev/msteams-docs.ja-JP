---
title: Live Share クイック スタート
description: このモジュールでは、Dice Roller サンプルをすばやく試す方法について説明します
ms.topic: concept
ms.localizationpriority: high
ms.author: stevenic
ms.openlocfilehash: 98150265f0c5876e726710cacc873db2ac23e9ee
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66484587"
---
---

# <a name="quick-start-guide"></a>クイック スタート ガイド

Dice Roller サンプルを使用して Live Share SDK の使用を開始することは、[流動フレームワーク クイック スタート](https://fluidframework.com/docs/start/quick-start/)の進化形であり、コンピューターのローカルホストで Live Share SDK ベースの [Dice Roller サンプル](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller)をすばやく実行するように設計されています。

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="DiceRoller サンプル":::

> [!NOTE]
> このガイドでは、ブラウザーでローカルで Live Share を使用する方法について説明します。 Teams 会議で SDK を使用する方法の詳細については、[Agile Agile のチュートリアル](../sbs-teams-live-share.yml)をお試しください。

## <a name="set-up-your-development-environment"></a>開発環境をセットアップする

開始するには、次のものをインストールします。

* [Node.js](https://nodejs.org/en/download): Live Share SDK では、Node.js LTS バージョン 12.17 以降がサポートされます。
* [Visual Studio Code の最新バージョン](https://code.visualstudio.com/)。
* [Git](https://git-scm.com/downloads)

## <a name="build-and-run-the-dice-roller-app"></a>アプリの構築と実行

1. [Dice Roller](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) サンプル アプリに移動します。

1. [Live Share SDK](https://github.com/microsoft/live-share-sdk) リポジトリを複製して、サンプル アプリをテストします。

    ```bash
    $ git clone https://github.com/microsoft/live-share-sdk.git
    ```

1. 次のコマンドを実行して、Dice Roller サンプル アプリ フォルダーに移動します。

   ```bash
    $ cd live-share-sdk\samples\01.dice-roller
   ```

1. 次のコマンドを実行して、依存関係パッケージをインストールします。

    ```bash
    $ npm install
    ```

1. 次のコマンドを実行してローカルの Web サーバーを起動します。

   ```bash
   $ npm start
   ```
  
     新しいブラウザー タブで `http://localhost:8080` URL が開き、Dice Roller ゲームが表示されます。

1. ID を含むブラウザーで完全な URL をコピーし、新しいウィンドウまたは別のブラウザーに URL を貼り付けます。

   サイコロ ローラー アプリケーションの 2 番目のクライアントが開きます。

1. 両方のウィンドウを開き、1 つのウィンドウで [**ロール**] ボタンを選択します。 サイコロの状態は両方のクライアントで変化します。

    :::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="サイコロ ローラーの複数のタブ":::
  
   **おめでとうございます。** Live Share SDK を使用してアプリをビルドして実行する方法を学習しました。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [サイコロ ローラーのチュートリアル](teams-live-share-tutorial.md)

## <a name="see-also"></a>関連項目

* [GitHub リポジトリ](https://github.com/microsoft/live-share-sdk)
* [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
* [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
* [Live Share 機能](teams-live-share-capabilities.md)
* [Live Share FAQ](teams-live-share-faq.md)
* [会議の Teams アプリ](teams-apps-in-meetings.md)
