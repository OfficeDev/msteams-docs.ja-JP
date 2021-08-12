---
title: チュートリアル - Yeoman ジェネレーターを使用して最初のアプリを作成する
description: Yeoman ジェネレーターを使用してアプリMicrosoft Teamsを開始する方法について学習します。
keywords: nodejs yeoman node.jsを開始する
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: fb37e49ad4cfe3b705832a1a5e419de56a859f43b601e5c8d7c026b120f37ab0
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57703202"
---
# <a name="build-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Yeoman ジェネレーターを使用Microsoft Teamsアプリをビルドする

> [!Note]
> このチュートリアルは、Wiki の[Yeoman ジェネレーター Teamsです](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。

このチュートリアルでは、Yeoman ジェネレーターを使用して最初のアプリをMicrosoft TeamsするMicrosoft Teams説明します。 また、Yeoman ジェネレーターを使用してアプリケーションをアップグレードTeams手順を説明します。 開始する前に、アプリのサイドローディングをTeamsアカウント[を持っている必要があります](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

![yeoman ジェネレーター git](~/assets/yeoman-demo.gif)

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>前提条件の取得

Yeoman ジェネレーターの使用を開始する前に、コンピューターに以下をインストールする必要があります。

* Node.js

   コンピューターにインストールNode.js必要があります。 最新の [LTS バージョンを使用する必要があります](https://nodejs.org)。

* コード エディター

   コード エディターが必要です。 このドキュメントと画像の大部分は、このドキュメントを使用[Visual Studio Code。](https://code.visualstudio.com) ただし、必要なテキスト エディターを自由に使用できます。

* Yeoman と Gulp CLI

   ジェネレーターを使用してプロジェクトをスキャフォールディングするには、Yeoman ツールと Gulp CLI タスク マネージャーをインストールする必要があります。

   コマンド プロンプトを開き、次の値を入力します。

   ```bash
   npm install yo gulp-cli --global
   ```

## <a name="install-the-generator"></a>ジェネレーターのインストール

次のコマンドTeams Yeoman ジェネレーターをインストールします。

```bash
npm init yo teams
```

次のコマンドを使用して、ジェネレーターのプレビュー バージョンをインストールします。

```bash
npm init yo teams@preview
```

## <a name="generate-your-project"></a>プロジェクトを生成する

このセクションでは、プロジェクトを生成する手順について説明します。

**プロジェクトを生成するには**

1. コマンド プロンプトを開き、プロジェクトを作成する新しいディレクトリを作成します。
1. ディレクトリに移動し、コマンドを実行します `yo teams` 。 ジェネレーターが起動します。
1. ジェネレーターから求める一連の質問に応答します。

   ![yo チーム](~/assets/yeoman-images/teams-first-app-1.png)

   1. プロジェクトの名前を入力します。 Enter キーを押すとそのままにできます。
   1. 新しいディレクトリを作成する場合は、新しいディレクトリのパスを入力します。 必要なディレクトリに既に存在する場合は、Enter キーを押します。
   1. プロジェクトのタイトルを入力します。 このタイトルは、アプリのマニフェストと説明で使用されます。 
   1. マニフェストでも使用する会社名を入力します。
   1. 使用するマニフェストのバージョンを入力します。 このチュートリアルでは、 `v1.5` 現在利用可能な一般的なスキーマを選択します。
   1. プロジェクトに追加するアイテムを選択します。 アイテムの 1 つまたは任意の組み合わせを選択できます。 このチュートリアルでは、タブを *選択します*。

    ![アイテムの選択](~/assets/yeoman-images/teams-first-app-2.png)

1. 手順 2 で選択した項目に基づいて表示される次のフォローアップ質問のセットに応答します。
1. ソリューションをホストする場所の URL を入力します。 

   > [!NOTE]
   > URL には任意の URL を指定できますが、既定ではジェネレーターは Azure Web サイトの URL を提案します。

1. ソリューションに単体テストを含める必要がある場合は、確認します。 既定の応答は Yes **です**。 単体テストを含める場合、生成されたプロジェクトには単体テスト フレームワークと、スキャフォールディングされるさまざまなアイテムに対する既定の単体テストが含まれます。 
   > [!NOTE]
   > * このチュートリアルでは、テスト フレームワークを含めないを選択します。
   > * ジェネレーターには、オプトインまたはオプトアウトできる多くの組み込みの高度な機能があります。

1. サインインを簡単に行う場合は、Azure Application インサイトを使用インサイトが表示されます。 [はい]**を選択** した場合は、Azure アプリケーション キーを指定インサイトがあります。 

   > [!NOTE]
   > このチュートリアルでは、Application インサイト を使用インサイト。

   次の質問のセットは、以前に選択したアイテムに基づいて行います。 タブの場合は、名前を指定し、必要に応じて、このアプリをオンライン Web パーツとして使用SharePoint選択する必要があります。 名前を指定すると、ジェネレーターはプロジェクトを生成し、すべての依存関係をインストールします。 これには 1 分または 2 分かかる場合があります。

## <a name="add-code-to-your-tab"></a>タブにコードを追加する

ジェネレーターが完了したら、お気に入りのコード エディターでソリューションを開くことができます。 1 分か 2 分で、コードの整理方法を理解します。 詳細については、「構造」[のドキュメントProject参照](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)してください。

タブがファイル内 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` にあります。 これは、タブの typeScript Reactベースのクラスです。 

1. メソッドを `render()` 見つけて、コントロール内にコード行を追加して `<PanelBody>` 、次のようにします。

   ``` TypeScript
   <PanelBody>
      <div style={styles.section}>
      Hello World! Yo Teams rocks!
      </div>
   </PanelBody>
   ```
1. ファイルを保存し、コマンド プロンプトに戻します。

## <a name="build-your-app"></a>アプリを作成する

これで、プロジェクトをビルドできます。 これは 2 つの手順で行います。

1. アプリにTeamsしたアプリのアプリ マニフェスト ファイルを作成Microsoft Teams。 これは Gulp タスクによって実行されます `gulp manifest` 。 これにより、マニフェストが検証され、ディレクトリに zip ファイルが作成 `./package` されます。
1. コマンドを `gulp build` 実行してソリューションをビルドします。 これにより、ソリューションがフォルダーに変換 `./dist` されます。 

## <a name="run-your-app"></a>アプリの実行

アプリを実行するには、コマンドを使用 `gulp serve` します。 これにより、アプリをテストするためのローカル Web サーバーが構築され、開始されます。 また、プロジェクトにファイルを保存するたびに、このコマンドはアプリケーションを再構築します。 

次に移動し、タブ `http://localhost:3007/myFirstAppTab/` がレンダリングされている必要があります。 ただし、まだMicrosoft Teamsされていません。 

**タブをレンダリングするには、Microsoft Teams**

![ブラウザーでサイトを表示する](~/assets/yeoman-images/teams-first-app-3.png)

### <a name="run-your-app-in-microsoft-teams"></a>アプリをアプリで実行Microsoft Teams

Microsoft Teamsアプリを localhost でホストすることはできませんので、パブリック URL に公開するか、ngrok などのプロキシを使用する必要があります。 良いニュースは、スキャフォールディングされたプロジェクトにこの組み込みがあります。 

**アプリをアプリで実行Teams**

1. ターミナル `gulp ngrok-serve` で実行します。 ngrok サービスを実行すると、一意のパブリック DNS エントリを使用してバックグラウンドで開始され、その一意の URL でマニフェストがパッケージ化され、その後とまったく同じ処理を実行 `gulp ngrok-serve` します `gulp serve` 。
1. 新しいチームをMicrosoft Teamsします。
1. [アプリ] で [チーム名> Teams 設定 >選択します。
1. 右下隅から、カスタム アプリアップロード **選択します**。
1. プロジェクト フォルダーの `package` 下のフォルダーに移動します。 
1. そのフォルダー内の zip ファイルを選択し、[開く] を選択します。 
   これで、アプリは次の方法でサイドMicrosoft Teams。

   ![サイドロードされたアプリ](~/assets/yeoman-images/teams-first-app-4.png)
1. [全般] チャネルに **戻り** 、新 **+** しいタブを追加します。タブの一覧にタブが表示されます。タブ ![ の構成](~/assets/yeoman-images/teams-first-app-5.png)
1. タブを選択し、指示に従って追加します。 カスタム構成ダイアログが表示され、ソースを編集できます。 [保存 *] を* 選択して、タブをチャネルに追加します。 これで、タブが読み込Microsoft Teams!

   ![teams でタブを実行する](~/assets/yeoman-images/teams-first-app-6.png)

### <a name="upgrade-microsoft-teams"></a>アップグレード Microsoft Teams

Yeoman ジェネレーターを使用してMicrosoft Teamsバージョンを最新バージョンにアップグレードMicrosoft Teamsできます。

**アップグレードするにはMicrosoft Teams**

1. 次のコマンドを使用してTeamsのバージョンを取得します。

   ```PowerShell
    yo teams --version
   ```
2. ジェネレーターを選択して更新するには、次のコマンドを使用します。

   ```PowerShell
    yo
   ```
3. 矢印キーを使用して [ **ジェネレーターの更新] を選択します**。

   ![YoSelectUpdatGen の画像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. ジェネレーターの一覧から必要なジェネレーターを選択します。
   > [!NOTE]
   > スペース バーを使用して、使用可能なオプションから選択したTeamsを選択または解除します。

    ![UseSpaceToSelectGenerators のイメージ](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > インストールが完了するには、数秒からTeams分かかります。

5. インストールが完了したら、次のコマンドを使用してインストールされているバージョンを確認します。

   ```PowerShell
    yo teams --version
   ```
   おめでとう! 最初のアプリをビルドしてMicrosoft Teamsしました。 また、アップグレードMicrosoft Teams。

 ## <a name="see-also"></a>関連項目

* [チュートリアルの概要](code-samples.md)
* [会話ボット アプリを作成する](first-app-bot.md)
* [メッセージング拡張機能を作成する](first-message-extension.md)
* [コード サンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples)