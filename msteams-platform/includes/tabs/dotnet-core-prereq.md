## <a name="prerequisites"></a>前提条件

- このクイックスタートを完了するには、Office 365 テナントと、[*カスタムアプリをアップロードできるようにする*] をオンにして構成されたチームが必要です。 詳細については、「 [Office 365 テナントを準備](~/concepts/build-and-test/prepare-your-o365-tenant.md)する」を参照してください。
  - 現在 Office 365 アカウントを持っていない場合は、 [office 365 開発者プログラム](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program)を使用して無料のサブスクリプションにサインアップできます。 このサブスクリプションは、継続的な開発のために使用している限り、アクティブのままです。

- アプリ Studio を使用して、アプリケーションを Teams にインポートします。 アプリ**studio をインストール** ![するには、](~/assets/images/tab-images/storeApp.png) Teams アプリの左下隅にある [アプリストアアプリの選択] を選択して、アプリ studio を検索します。 タイルを見つけたら、それを選択して、[ポップアップウィンドウ] ダイアログボックスの [インストール] を選択します。

また、このプロジェクトでは、開発環境に次のものがインストールされている必要があります。

- 現在のバージョン **.NET コアクロスプラットフォーム開発**ワークロードがインストールされた VISUAL Studio IDE。 Visual Studio をまだお持ちでない場合は、最新の[Microsoft Visual Studio コミュニティ](https://visualstudio.microsoft.com/downloads)バージョンを無料でダウンロードしてインストールすることができます。

- [Ngrok](https://ngrok.com)リバースプロキシツール。 Ngrok を使用して、ローカルに使用可能な web サーバーの公開された HTTPS エンドポイントへのトンネルを作成します。 ここから[ダウンロード](https://ngrok.com/download)できます。
