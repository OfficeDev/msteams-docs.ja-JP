## <a name="prerequisites"></a>前提条件

- このクイックスタートを完了するには、Office 365 テナントと、[*カスタムアプリをアップロードできるようにする*] をオンにして構成されたチームが必要です。 詳細については、「 [Office 365 テナントを準備](~/concepts/build-and-test/prepare-your-o365-tenant.md)する」を参照してください。

  - 現在 Office 365 アカウントを持っていない場合は、Office 365 開発者プログラムを使用して無料のサブスクリプションにサインアップできます。 このサブスクリプションは、継続的な開発のために使用している限り、アクティブのままです。 「 [Office 365 開発者プログラムへようこそ」を](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md)参照してください。

また、このプロジェクトでは、開発環境に次のものがインストールされている必要があります。

- 任意のテキストエディターまたは IDE。 [Visual Studio コード](https://code.visualstudio.com/download)を無料でインストールして使用することができます。

- [Node.js/npm](https://nodejs.org/en/)。 最新の LTS バージョンを使用する必要があります。 ノードパッケージマネージャー (npm) は、node.js のインストールによってシステムにインストールされます。

- Node.js のインストールが正常に完了したら、コマンドプロンプトに次のように入力して、 [gulp](https://www.npmjs.com/package/gulp-cli)パッケージと、cli パッケージを[インストールします](https://yeoman.io/)。

```bash
npm install yo gulp-cli --global
```

- コマンドプロンプトに次のように入力して、Microsoft Teams アプリジェネレーターをインストールします。

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a>プロジェクトを生成する

- コマンドプロンプトを開き、タブプロジェクト用の新しいディレクトリを作成します。

- ジェネレーターを開始するには、新しいディレクトリに移動し、次のコマンドを入力します。

```bash
yo teams
```

- 次に、アプリケーションの**manifest**ファイルで使用される一連の値を入力します。

![ジェネレーターの開いているスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

**ソリューション名は何ですか。**

これはプロジェクト名です。 Enter キーを押すと、提案された名前を承諾できます。

**ファイルをどこに保存しますか?**

現在、プロジェクトディレクトリにいます。 Enter キーを押します。

**Microsoft Teams アプリプロジェクトのタイトル**

これはアプリのパッケージ名で、アプリのマニフェストと説明に使用されます。

**(会社) 名(最大32文字)**

会社名はアプリマニフェストで使用されます。

<br>**使用するマニフェストのバージョンを選択してください。**

[既定のスキーマ] を選択します。

**Microsoft パートナー Id を入力します (必要な場合)。(空白のままにしてください)**

このフィールドは必須ではなく、既に[Microsoft パートナーネットワーク](https://partner.microsoft.com)に属している場合にのみ使用してください。

**プロジェクトに何を追加しますか?**

タブを&ast;選択します ()。

**このソリューションをホストする URL を指定します。**

既定では、ジェネレーターは Azure Web サイトの URL を提案します。 アプリのローカルテストのみが行われるため、このクイックスタートを完了するために有効な URL は必要ありません。

**テストフレームワークと初期テストを含めますか?(y/N)**

このプロジェクトのテストフレームワークを含め**ないこと**を選択します。 既定値は yes です。「 **n**」と入力します。

**テレメトリに Azure Application Insights を使用しますか?(y/N)**

[Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md)を含め**ないこと**を選択します。 既定値は [いいえ; です。「 **n**」と入力します。

**既定のタブ名 (最大16文字)?**

タブに名前を指定します。このタブ名は、ファイルまたは URL パスコンポーネントとしてプロジェクト全体で使用されます。
