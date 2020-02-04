## <a name="create-the-app-package"></a><span data-ttu-id="45436-101">アプリパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="45436-101">Create the app package</span></span>

<span data-ttu-id="45436-102">Teams でタブをテストするには、アプリパッケージが必要になります。</span><span class="sxs-lookup"><span data-stu-id="45436-102">You'll need an app package to test your tab in Teams.</span></span> <span data-ttu-id="45436-103">これは、次の必要なファイルが含まれる zip フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="45436-103">It's a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="45436-104">192 x 192 ピクセルを測定する**フルカラーアイコン**。</span><span class="sxs-lookup"><span data-stu-id="45436-104">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="45436-105">32 x 32 ピクセルを測定する**透明のアウトラインアイコン**。</span><span class="sxs-lookup"><span data-stu-id="45436-105">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="45436-106">アプリの属性を指定する**manifest.xml**ファイル。</span><span class="sxs-lookup"><span data-stu-id="45436-106">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="45436-107">パッケージは、gulp タスクを使用して作成され、マニフェストファイルを検証し、 `./package directory`で zip フォルダーを生成します。</span><span class="sxs-lookup"><span data-stu-id="45436-107">The package is created via a gulp task that validates the manifest.json file and generates the zip folder in the `./package directory`.</span></span> <span data-ttu-id="45436-108">コマンドプロンプトで、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="45436-108">In the command prompt enter:</span></span>

```bash
gulp manifest
```

## <a name="build-your-application"></a><span data-ttu-id="45436-109">アプリケーションをビルドする</span><span class="sxs-lookup"><span data-stu-id="45436-109">Build your application</span></span>

<span data-ttu-id="45436-110">Build コマンドは、ソリューションを*transpiles フォルダーに組み込みます。*</span><span class="sxs-lookup"><span data-stu-id="45436-110">The build command transpiles your solution into the *./dist* folder.</span></span> <span data-ttu-id="45436-111">次に、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="45436-111">Next,enter:</span></span>

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a><span data-ttu-id="45436-112">Localhost でアプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="45436-112">Run your application in localhost</span></span>

<span data-ttu-id="45436-113">次のように入力して、ローカル web サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="45436-113">Start a local web server by entering the following:</span></span>

```bash
gulp serve
```

<span data-ttu-id="45436-114">ブラウザー `http://localhost:3007/<yourDefaultAppNameTab>/`に Enter キーを押して、アプリケーションのホームページを表示します。</span><span class="sxs-lookup"><span data-stu-id="45436-114">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your application's home page:</span></span>

![ホームページのスクリーンショット](~/assets/images/tab-images/homePage.png)