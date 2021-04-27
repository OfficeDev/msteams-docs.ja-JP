---
title: チュートリアル - Yeoman ジェネレーターを使用して最初のアプリを作成する
description: Yeoman ジェネレーターを使用して Microsoft Teams アプリの構築を開始する方法について説明します。
keywords: nodejs yeoman node.jsを開始する
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 9efbe6f6e6502120f1afdadb9b538182f1406c56
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018433"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Yeoman ジェネレーターを使用して最初の Microsoft Teams アプリを作成する

> [!Note]
> このチュートリアルは [、Teams Wiki の Yeoman ジェネレーターから提供されています](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。

このチュートリアルでは、Microsoft Teams Yeoman ジェネレーターを使用して最初の Microsoft Teams アプリを作成する方法について説明します。 また、Yeoman ジェネレーターを使用して Teams をアップグレードするプロセスについて説明します。 このチュートリアルから始める前提条件は、アプリのサイドローディングを許可する Teams [アカウントを持っている必要があります](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

![yeoman ジェネレーター git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>コンピューターのセットアップと準備

Yeoman ジェネレーターの使用を開始する前に、コンピューターに以下をインストールする必要があります。

### <a name="install-nodejs"></a>Node.js. のインストール

コンピューターにインストールNode.js必要があります。 最新の [LTS バージョンを使用する必要があります](https://nodejs.org)。

### <a name="install-a-code-editor"></a>コード エディターのインストール

コード エディターが必要です。 このドキュメントと画像の大部分は、コードの使用 [Visual Studio参照します](https://code.visualstudio.com)。 ただし、必要なテキスト エディターを自由に使用できます。

### <a name="install-yeoman-and-gulp-cli"></a>Yeoman と Gulp CLI をインストールする

ジェネレーターを使用してプロジェクトをスキャフォールディングするには、Yeoman ツールと Gulp CLI タスク マネージャーをインストールする必要があります。

コマンド プロンプトを開き、次の値を入力します。

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>ジェネレーターのインストール

次のコマンドを使用して Teams Yeoman ジェネレーターをインストールします。

```bash
npm install generator-teams --global
```

次のコマンドを使用して、ジェネレーターのプレビュー バージョンをインストールします。

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>プロジェクトを生成する

このセクションでは、プロジェクトを生成する手順について説明します。

**プロジェクトを生成するには**

1. コマンド プロンプトを開き、プロジェクトを作成する新しいディレクトリを作成し、そのディレクトリでコマンドを実行します `yo teams` 。 ジェネレーターが起動します。
1. ジェネレーターから求める一連の質問に応答します。

   ![yo チーム](~/assets/yeoman-images/teams-first-app-1.png)

   1. 最初の質問はプロジェクト名に関する質問で、Enter キーを押すことでそのままにできます。
   1. 次の質問では、新しいディレクトリを作成するか、現在のディレクトリを使用するかが問い合されます。 必要なディレクトリに既に存在する場合は、Enter キーを押します。
   1. 次の質問で、プロジェクトのタイトルを入力します。 このタイトルは、アプリのマニフェストと説明で使用されます。 
   1. 次に、マニフェストでも使用される会社名を求める質問が表示されます。
   1. 5 番目の質問では、使用するマニフェストのバージョンについて質問されます。 このチュートリアルでは、 `v1.5` 現在利用可能な一般的なスキーマを選択します。
   1. 次に、ジェネレーターは、プロジェクトに追加するアイテムを確認します。 アイテムの 1 つまたは任意の組み合わせを選択できます。 このチュートリアルでは、[タブ] *を選択します*。

    ![アイテムの選択](~/assets/yeoman-images/teams-first-app-2.png)

1. 手順 2 で選択したアイテムに基づいて表示される次のフォローアップ質問のセットに応答します。
1. ソリューションをホストする場所の URL を入力します。 

   > [!NOTE]
   > URL には任意の URL を指定できますが、既定ではジェネレーターは Azure Web サイトの URL を提案します。

1. 次の質問で、ソリューションに単体テストを含める必要がある場合に確認します。 既定の応答は yes *です*。 単体テストを含める場合、生成されたプロジェクトには単体テスト フレームワークと、スキャフォールディングされるさまざまなアイテムに対する既定の単体テストが含まれます。 
   > [!NOTE]
   > * このチュートリアルでは、テスト フレームワークを含めないを選択します。
   > * ジェネレーターには、オプトインまたはオプトアウトできる多くの組み込みの高度な機能があります。

1. サインインを簡単に行う場合は、サインインに Azure Application Insights を使用する必要がある場合も尋ねられるメッセージが表示されます。 [はい] *を選択* した場合は、Azure Application Insights キーを指定する必要があります。 

   > [!NOTE]
   > このチュートリアルでは、Application Insights の使用をオプトアウトします。

次の質問のセットは、以前に選択したアイテムに基づいて行います。 タブの場合は、名前を指定し、必要に応じてこのアプリを SharePoint Online Web パーツとして使用できる場合に選択する必要があります。 名前を指定すると、ジェネレーターはプロジェクトを生成し、すべての依存関係をインストールします。 これには 1 分または 2 分かかる場合があります。

## <a name="add-some-code-to-your-tab"></a>タブにコードを追加する

ジェネレーターが完了したら、お気に入りのコード エディターでソリューションを開くことができます。 1 分か 2 分で、コードの整理方法を理解します。 詳細については [、「Project Structure」のドキュメントを参照](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) してください。

タブがファイル内 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` にあります。 これは、タブの TypeScript React ベースのクラスです。メソッドを `render()` 見つけて、コントロール内にコード行を追加して `<PanelBody>` 、次のようにします。

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

ファイルを保存し、コマンド プロンプトに戻します。

## <a name="build-your-app"></a>アプリを作成する

これで、プロジェクトをビルドできます。 これは、2 つの手順 (または 1 つの手順を参照) で行います。

まず、Microsoft Teams にアップロードまたはサイドロードする Teams アプリ マニフェスト ファイルを作成する必要があります。 これは Gulp タスクによって実行されます `gulp manifest` 。 これにより、マニフェストが検証され、ディレクトリに zip ファイルが作成 `./package` されます。

ソリューションをビルドするには、コマンドを使用 `gulp build` します。 これにより、ソリューションがフォルダーに変換 `./dist` されます。 

## <a name="run-your-app"></a>アプリの実行

アプリを実行するには、コマンドを使用 `gulp serve` します。 これにより、アプリをテストするためのローカル Web サーバーが構築され、開始されます。 また、プロジェクトにファイルを保存するたびに、このコマンドはアプリケーションを再構築します。 

これで、タブがレンダリングされる `http://localhost:3007/myFirstAppTab/` のを確認するために参照できる必要があります。 ただし、まだ Microsoft Teams にはありません。

![ブラウザーでサイトを表示する](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Microsoft Teams でアプリを実行する

Microsoft Teams では、アプリを localhost でホストすることはできません。そのため、パブリック URL に発行するか、ngrok などのプロキシを使用する必要があります。

良いニュースは、スキャフォールディングされたプロジェクトにこの組み込みがあります。 ngrok サービスを実行すると、一意のパブリック DNS エントリを使用してバックグラウンドで開始され、その一意の URL でマニフェストがパッケージ化され、その後とまったく同じ処理を実行 `gulp ngrok-serve` します `gulp serve` 。

実行後、新しい Microsoft Teams チームを作成し、チーム名をクリックしてチームの設定に移動し、[アプリ] `gulp ngrok-serve` を選択 *します*。 右下隅に[カスタム アプリをアップロードする] リンクが表示されます。それを選択して、プロジェクト フォルダーとサブフォルダーを参照します `package` 。 そのフォルダー内の zip ファイルを選択し、[開く] を選択します。 これで、アプリは Microsoft Teams にサイドロードされます。

![サイドロードされたアプリ](~/assets/yeoman-images/teams-first-app-4.png)

[全般] チャネルに *戻り* 、新 *+* しいタブを追加します。タブの一覧にタブが表示されます。

![[構成] タブ](~/assets/yeoman-images/teams-first-app-5.png)

タブを選択し、指示に従って追加します。 カスタム構成ダイアログが表示され、ソースを編集できます。 [保存 *] を* 選択して、タブをチャネルに追加します。 完了したら、タブを Microsoft Teams 内に読み込む必要があります。

![teams でタブを実行する](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a>Microsoft Teams のアップグレード

Microsoft Teams Yeoman ジェネレーターを使用して、現在の Microsoft Teams バージョンを最新バージョンにアップグレードできます。

**Microsoft Teams をアップグレードするには**

1. 次のコマンドを使用して、Teams の現在のバージョンを取得します。

   ```PowerShell
    yo teams --version
   ```
2. 次のコマンドを使用して、ジェネレーターの更新を選択します。

   ```PowerShell
    yo
   ```
3. 矢印キーを使用して [ **ジェネレーターの更新] を選択します**。

   ![YoSelectUpdatGen の画像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. ジェネレーターの一覧から目的のジェネレーターを選択します。
   > [!NOTE]
   > スペース バーを使用して、使用可能なオプションから選択した Teams バージョンを選択またはクリアします。

    ![UseSpaceToSelectGenerators のイメージ](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > Teams のインストールが完了するには数秒から数分かかります。

5. インストールが完了したら、次のコマンドを使用してインストールされているバージョンを確認します。

   ```PowerShell
    yo teams --version
   ```
   
**おめでとう!最初の Microsoft Teams アプリをビルドして展開しました。Microsoft Teams もアップグレードしました。**
