---
title: 開発者ポータルを使用してアプリを管理する
description: この記事では、Microsoft Teams用開発者ポータルを使用してアプリを構成、配布、管理する方法について説明します。
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 12f1def758e4ef108f9670e0cc696c7ce197e485
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232445"
---
# <a name="manage-your-apps-in-developer-portal"></a>開発者ポータルでアプリを管理する

アプリを作成またはアップロードしたら、開発者ポータルで次の方法でアプリを管理できます。

* [概要](#overview)
* [構成](#configure)
* [詳細設定](#advanced)
* [Publish](#publish)

## <a name="overview"></a>概要

[ **概要** ] セクションには、アプリを管理するための次のコンポーネントが表示されます。

* ダッシュボード

  * [ **ダッシュボード** ] の [ **概要** ] セクションには、アプリの次のコンポーネントが表示されます。
    * **Teams ストアの検証**: アプリ検証ツールは、アプリを確認するときに Microsoft が使用するテスト ケースに対してアプリ パッケージをチェックします。
    * **お知らせ**: Teams 用開発者ポータルでのアプリの最新の更新プログラム
    * **アクティブユーザー (プレビュー)**: アクティブなユーザー数を表示します
    * **基本情報**: アプリ ID、バージョン、マニフェストのバージョンなどを表示します。

    :::image type="content" source="../../assets/images/tdp/dashboard-page.png" alt-text="スクリーンショットは、Teams 用開発者ポータルで作成したアプリの [概要] ページを示す例です。":::

* 分析

    [ **分析** ] ページの [ **概要** ] セクションで、アプリのアクティブなユーザーの合計数を確認できます。 詳細については、「 [アプリの使用状況を分析する](analyze-your-apps-usage-in-developer-portal.md)」を参照してください。

## <a name="configure"></a>Configure

Teams でアプリをインストールしてレンダリングするには、Teams が認識する一連の構成を含める必要があります。 Teams でアプリをアップロードするには、Teams でアプリを表示するためのすべてのアプリの詳細を含むアプリ マニフェストが必要です。 これは、開発者ポータルで使用できるコンポーネントとツールの助けを借りて実現できます。

[ **構成]** セクションには、アプリを管理してアクセスするための次のコンポーネントが表示されます。

* **基本的な情報**: このセクションでは、アプリ名、アプリ ID、説明、バージョン、開発者情報、アプリ URL、アプリケーション (クライアント) ID、Microsoft Partner Network ID を編集できます。
* **ブランド** 化: このページには、アプリ アイコンの詳細が表示されます。
* **アプリの機能**: 次の機能をアプリに追加できます。
  * 個人用アプリ
  * Bot
  * Connector
  * シーン
  * グループ アプリとチャネル アプリ
  * メッセージング拡張機能
  * 会議の拡張機能
  * アクティビティ フィード通知
* **アクセス許可**: このセクションでは、デバイスのアクセス許可、チームのアクセス許可、チャットまたは会議のアクセス許可、アプリのユーザーアクセス許可を付与できます。
* **シングル サインオン**: シングル サインオン (SSO) でユーザーを認証するようにアプリを構成できます。
* **言語**: アプリの言語を設定または変更できます。
* **ドメイン**: Teams クライアントにアプリを読み込むドメインを追加できます (例: *.example.com)。

:::image type="content" source="../../assets/images/tdp/configure.png" alt-text="このスクリーンショットは、開発者ポータルでアプリを管理およびアクセスするための機能を構成する方法を示す例です。":::

## <a name="advanced"></a>詳細情報

[ **詳細設定** ] セクションには、開発者ポータルでアプリを管理するための次のコンポーネントが表示されます。

* **所有者**

    各アプリには **[所有者]** ページが含まれています。このページでは、アプリの登録を組織内の他のユーザーと共有できます。 **管理者** ロールと **Operative** ロールを追加して、アプリの設定を変更できるユーザーを管理できます。 **Operative** ロールには、アプリを削除する以外は **管理者** ロールと同じアクセス許可があります。

    所有者を追加するには:

    1. [ **詳細設定** ] セクションで、[ **所有者**] を選択します。
    1. [ **所有者の追加] を選択します**。
    1. 名前を入力し、ドロップダウン リストからユーザー ID を選択します。
    1. [ **ロール]** で、[ **操作]** または **[管理者**] を選択します。
    1. **[追加]** を選択します。

* **アプリコンテンツ**: 次の追加機能を使用してアプリを構成できます。
  
  * 読み込みインジケーター: ホストされているアプリのコンテンツ (タブやタスク モジュールなど) が読み込み中であることをユーザーに知らせるインジケーターを表示します。
  * 全画面表示モード: アプリ ヘッダーのない個人用アプリを表示します。 組織に公開されたアプリでのみサポートされます。

* **環境**

    ローカル ランタイムから運用環境へのアプリの移行に役立つ環境とグローバル変数を構成できます。 グローバル変数は、すべての環境で使用されます。

    環境を設定するには:

    1. 開発者ポータルで、作業している **アプリ** を選択します。
    1. **[詳細設定**] セクションの [**環境**] に移動し、[**+ 環境の追加]** を選択します。
    1. **[追加]** を選択します。

  * **グローバル変数**

      1. [ **グローバル変数の追加]** を選択して、環境の構成変数を作成します。

      グローバル変数を使用するには:

      ハードコーディングされた値の代わりに変数名を使用して、アプリの構成を設定します。

      1. 開発者ポータルの任意のフィールドに入力 `{{` します。 選択した環境に対して作成したすべての変数とグローバル変数を含むドロップダウンが表示されます。  
      1. アプリ パッケージをダウンロードする前に (たとえば、Teams ストアに発行する準備ができたら)、使用する環境を選択します。 アプリの構成は、環境に基づいて自動的に更新されます。

* **プランと価格**: アプリのパートナー センターで作成した SaaS プランをリンクできます。
* **管理設定**:
  * アプリのカスタマイズ: アプリをカスタマイズできます
  * 既定でアプリをブロックする: テナント管理者がアプリを有効にするまで、既定でユーザーのアプリをブロックできます。

## <a name="publish"></a>公開

アプリは、組織または Teams ストアに発行できます。

* **組織にアプリを発行する**:

   1. アプリの **[概要** ] ページの [ **発行**] で、[ **組織に発行**] を選択します。
   1. [ **アプリの発行] を選択します**。

* **保存するアプリを発行します**。

   1. アプリの **[概要** ] ページの [ **発行**] で、[ **ストアに発行**] を選択します。
   1. [**発行**] を選択します。

   > [!NOTE]
   > アプリ検証ツールは、Microsoft がアプリの確認に使用するテスト ケースに対してアプリ パッケージをチェックします。 アプリを送信する前に、エラーまたは警告を解決し、 **アプリ提出チェックリスト** を読んでください。

   アプリ パッケージをダウンロードするには、[発行してストア] ページから **[アプリ パッケージのダウンロード** ] ボタンを選択します。

* **アプリ パッケージ**: アプリ パッケージは、アプリの機能、必要なリソース、マニフェスト内のその他の重要な属性を含むアプリの構成方法について説明します。 [アイコン] タブには、アプリに使用されるアイコンが表示されます。

## <a name="test-your-app-directly-in-teams"></a>Teams でアプリを直接テストする

開発者ポータルには、アプリをテストおよびデバッグするためのオプションが用意されています。

* [ **概要** ] ページでは、アプリが構成され、Teams ストアのテスト ケースに対して検証されているかどうかを示すスナップショットが表示されます。
* **[Teams のプレビュー**] ボタンをクリックすると、デバッグ用に Teams クライアントでアプリをすばやく起動します。

## <a name="use-tools-to-create-app-features"></a>ツールを使用してアプリ機能を作成する

開発者ポータルには、Teams アプリの主要な機能を構築するのに役立つツールも含まれています。 ツールを次に示します。

* **シーン スタジオ**: Teams 会議用の [カスタム Together Mode シーン](~/apps-in-teams-meetings/teams-together-mode.md) を設計します。
* **アダプティブ カード エディター**: アプリに含めるアダプティブ カードを作成してプレビューします。
* **Microsoft ID プラットフォーム管理**: ユーザーがサインインして API へのアクセスを提供できるように、アプリを Azure Active Directory に登録します。
* **Teams ストア アプリの検証**: Microsoft がアプリの確認に使用するテスト ケースに対してアプリ パッケージを確認します。
* **ボット管理**: ユーザーと通信し、質問に回答し、変更やその他のイベントについて事前に通知する会話ボットをアプリに追加します。

ボットを追加するには:

1. 開発者ポータルで、左側のウィンドウで **[ツール** ] を選択します。
1. **ボット管理** を選択します。
1. ボット管理ページで、[ **新しいボット**] を選択します。
1. 名前を入力し、[ **追加**] を選択します。

:::image type="content" source="../../assets/images/tdp/tools-in-dev-portal.png" alt-text="スクリーンショットは、開発者ポータルのツールを示す例です。これは、主な機能を構築するのに役立ちます。":::

開発者ポータルから Bot Framework ポータルに移動し、アイコンやその他のプロパティを更新するようにボットを構成できます。

## <a name="see-also"></a>関連項目

[Microsoft Teams アプリに SaaS オファーを含める](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)