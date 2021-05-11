## <a name="create-the-app-package"></a><span data-ttu-id="de5d9-101">アプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="de5d9-101">Create the app package</span></span>

<span data-ttu-id="de5d9-102">タブをテストするには、アプリ パッケージが必要Teams。</span><span class="sxs-lookup"><span data-stu-id="de5d9-102">You'll need an app package to test your tab in Teams.</span></span> <span data-ttu-id="de5d9-103">これは、次の必須ファイルを含む zip フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="de5d9-103">It's a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="de5d9-104">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="de5d9-104">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="de5d9-105">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="de5d9-105">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="de5d9-106">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="de5d9-106">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="de5d9-107">パッケージは gulp タスクを使用して作成され、ファイルのmanifest.jsを検証し、zip フォルダーを生成します `./package directory` 。</span><span class="sxs-lookup"><span data-stu-id="de5d9-107">The package is created via a gulp task that validates the manifest.json file and generates the zip folder in the `./package directory`.</span></span> <span data-ttu-id="de5d9-108">コマンド プロンプトで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="de5d9-108">In the command prompt enter:</span></span>

```bash
gulp manifest
```

## <a name="build-your-application"></a><span data-ttu-id="de5d9-109">アプリケーションのビルド</span><span class="sxs-lookup"><span data-stu-id="de5d9-109">Build your application</span></span>

<span data-ttu-id="de5d9-110">ビルド コマンドは、ソリューションを *./dist フォルダーに変換* します。</span><span class="sxs-lookup"><span data-stu-id="de5d9-110">The build command transpiles your solution into the *./dist* folder.</span></span> <span data-ttu-id="de5d9-111">次に、次に入力します。</span><span class="sxs-lookup"><span data-stu-id="de5d9-111">Next,enter:</span></span>

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a><span data-ttu-id="de5d9-112">localhost でアプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="de5d9-112">Run your application in localhost</span></span>

<span data-ttu-id="de5d9-113">次のコマンドを入力して、ローカル Web サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="de5d9-113">Start a local web server by entering the following:</span></span>

```bash
gulp serve
```

<span data-ttu-id="de5d9-114">ブラウザー `http://localhost:3007/<yourDefaultAppNameTab>/` に入力し、アプリケーションのホーム ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="de5d9-114">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your application's home page:</span></span>

![ホーム ページのスクリーンショット](~/assets/images/tab-images/homePage.png)