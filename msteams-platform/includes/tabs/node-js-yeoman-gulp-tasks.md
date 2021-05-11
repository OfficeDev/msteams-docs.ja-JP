## <a name="create-the-app-package"></a>アプリ パッケージを作成する

タブをテストするには、アプリ パッケージが必要Teams。 これは、次の必須ファイルを含む zip フォルダーです。

- 192 x 192 ピクセルのフル カラー アイコン。 
- **32** x 32 ピクセルの透明なアウトライン アイコン。
- アプリ **manifest.js** を指定するファイルのプロパティです。

パッケージは gulp タスクを使用して作成され、ファイルのmanifest.jsを検証し、zip フォルダーを生成します `./package directory` 。 コマンド プロンプトで次のコマンドを入力します。

```bash
gulp manifest
```

## <a name="build-your-application"></a>アプリケーションのビルド

ビルド コマンドは、ソリューションを *./dist フォルダーに変換* します。 次に、次に入力します。

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a>localhost でアプリケーションを実行する

次のコマンドを入力して、ローカル Web サーバーを起動します。

```bash
gulp serve
```

ブラウザー `http://localhost:3007/<yourDefaultAppNameTab>/` に入力し、アプリケーションのホーム ページを表示します。

![ホーム ページのスクリーンショット](~/assets/images/tab-images/homePage.png)