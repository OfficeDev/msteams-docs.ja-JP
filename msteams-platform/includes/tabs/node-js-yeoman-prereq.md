## <a name="prerequisites"></a><span data-ttu-id="5997a-101">前提条件</span><span class="sxs-lookup"><span data-stu-id="5997a-101">Prerequisites</span></span>

- <span data-ttu-id="5997a-102">このクイック スタートを完了するには、カスタム アプリのアップロードOffice 365許可を有効にしたテナントとチーム *が必要* です。</span><span class="sxs-lookup"><span data-stu-id="5997a-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="5997a-103">詳細については、「Prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="5997a-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="5997a-104">現在アカウントをお持ちOffice 365場合は、開発者プログラムから無料サブスクリプションOffice 365できます。</span><span class="sxs-lookup"><span data-stu-id="5997a-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="5997a-105">サブスクリプションは、継続的な開発に使用している限りアクティブなままです。</span><span class="sxs-lookup"><span data-stu-id="5997a-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="5997a-106">「[開発者プログラムへようこそOffice 365」を参照してください](https://docs.microsoft.com/office/developer-program/microsoft-365-developer-program)。</span><span class="sxs-lookup"><span data-stu-id="5997a-106">See [Welcome to the Office 365 Developer Program](https://docs.microsoft.com/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="5997a-107">さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="5997a-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="5997a-108">任意のテキスト エディターまたは IDE。</span><span class="sxs-lookup"><span data-stu-id="5997a-108">Any text editor or IDE.</span></span> <span data-ttu-id="5997a-109">無料でインストール[して使用Visual Studio Code](https://code.visualstudio.com/download)できます。</span><span class="sxs-lookup"><span data-stu-id="5997a-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="5997a-110">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="5997a-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="5997a-111">最新の LTS バージョンを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5997a-111">You should use the latest LTS version.</span></span> <span data-ttu-id="5997a-112">ノード ノード パッケージ マネージャー (npm) がインストールされたシステムにインストールNode.js。</span><span class="sxs-lookup"><span data-stu-id="5997a-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="5997a-113">インストールが正常に完了したらNode.jsに次のように入力して [、Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="5997a-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

```bash
npm install yo gulp-cli --global
```

- <span data-ttu-id="5997a-114">コマンド プロンプトにMicrosoft Teamsを入力して、アプリ ジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="5997a-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a><span data-ttu-id="5997a-115">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="5997a-115">Generate your project</span></span>

- <span data-ttu-id="5997a-116">コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="5997a-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="5997a-117">ジェネレーターを起動するには、新しいディレクトリに移動し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="5997a-117">To start the generator, navigate to your new directory and type the following command:</span></span>

```bash
yo teams
```

- <span data-ttu-id="5997a-118">次に、アプリケーションのファイルで使用される一連の値manifest.js **します** 。</span><span class="sxs-lookup"><span data-stu-id="5997a-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

![ジェネレーターの開くスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

<span data-ttu-id="5997a-120">**ソリューション名は何ですか?**</span><span class="sxs-lookup"><span data-stu-id="5997a-120">**What is your solution name?**</span></span>

<span data-ttu-id="5997a-121">これはプロジェクト名です。</span><span class="sxs-lookup"><span data-stu-id="5997a-121">This is your project name.</span></span> <span data-ttu-id="5997a-122">Enter キーを押すと、候補の名前を受け入れできます。</span><span class="sxs-lookup"><span data-stu-id="5997a-122">You can accept the suggested name by pressing enter.</span></span>

<span data-ttu-id="5997a-123">**ファイルをどこに保存しますか?**</span><span class="sxs-lookup"><span data-stu-id="5997a-123">**Where do you want to place the files?**</span></span>

<span data-ttu-id="5997a-124">現在、プロジェクト ディレクトリにいます。</span><span class="sxs-lookup"><span data-stu-id="5997a-124">You're currently in your project directory.</span></span> <span data-ttu-id="5997a-125">Enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="5997a-125">Press enter.</span></span>

<span data-ttu-id="5997a-126">**アプリ プロジェクトMicrosoft Teamsタイトル**</span><span class="sxs-lookup"><span data-stu-id="5997a-126">**Title of your Microsoft Teams app project?**</span></span>

<span data-ttu-id="5997a-127">これはアプリ パッケージ名であり、アプリ マニフェストと説明で使用されます。</span><span class="sxs-lookup"><span data-stu-id="5997a-127">This is your app package name and will be used in the app manifest and description.</span></span>

<span data-ttu-id="5997a-128">**(会社) の名前(最大 32 文字)**</span><span class="sxs-lookup"><span data-stu-id="5997a-128">**Your (company) name? (max 32 characters)**</span></span>

<span data-ttu-id="5997a-129">会社名はアプリ マニフェストで使用されます。</span><span class="sxs-lookup"><span data-stu-id="5997a-129">Your company name will be used in the app manifest.</span></span>

<br><span data-ttu-id="5997a-130">**どのマニフェスト バージョンを使用しますか?**</span><span class="sxs-lookup"><span data-stu-id="5997a-130">**Which manifest version would you like to use?**</span></span>

<span data-ttu-id="5997a-131">既定のスキーマを選択します。</span><span class="sxs-lookup"><span data-stu-id="5997a-131">Select the default schema.</span></span>

<span data-ttu-id="5997a-132">**クイック スキャフォールディング(Y/n)**</span><span class="sxs-lookup"><span data-stu-id="5997a-132">**Quick scaffolding? (Y/n)**</span></span>

<span data-ttu-id="5997a-133">既定値は yes です。 **n と入力** して Microsoft パートナー ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="5997a-133">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

<span data-ttu-id="5997a-134">**Microsoft パートナー ID をお持ちの場合は、Microsoft パートナー ID を入力してください。(スキップする場合は空白のままにする)**</span><span class="sxs-lookup"><span data-stu-id="5997a-134">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

<span data-ttu-id="5997a-135">このフィールドは必須ではありません。既に Microsoft パートナー ネットワークに参加している場合にのみ [使用してください](https://partner.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="5997a-135">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

<span data-ttu-id="5997a-136">**プロジェクトに何を追加しますか?**</span><span class="sxs-lookup"><span data-stu-id="5997a-136">**What do you want to add to your project?**</span></span>

<span data-ttu-id="5997a-137">[( &ast; ) ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="5997a-137">Select ( &ast; ) A Tab.</span></span>

<span data-ttu-id="5997a-138">**このソリューションをホストする URL**</span><span class="sxs-lookup"><span data-stu-id="5997a-138">**The URL where you will host this solution?**</span></span>

<span data-ttu-id="5997a-139">既定では、ジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="5997a-139">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="5997a-140">アプリをローカルでテストするだけなので、このクイック スタートを完了するために有効な URL は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="5997a-140">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

<span data-ttu-id="5997a-141">**テスト フレームワークと初期テストを含めるには?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="5997a-141">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

<span data-ttu-id="5997a-142">この **プロジェクトの** テスト フレームワークを含めないを選択します。</span><span class="sxs-lookup"><span data-stu-id="5997a-142">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="5997a-143">既定値は yes です。 **n と入力します**。</span><span class="sxs-lookup"><span data-stu-id="5997a-143">The default is yes; enter **n**.</span></span>

<span data-ttu-id="5997a-144">**テレメトリに Azure Applications Insights を使用しますか?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="5997a-144">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

<span data-ttu-id="5997a-145">Azure **Application** [Insights を含めないを選択します](/azure-docs/articles/azure-monitor/app/app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5997a-145">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="5997a-146">既定値は no です。 **n と入力します**。</span><span class="sxs-lookup"><span data-stu-id="5997a-146">The default is no; enter **n**.</span></span>

<span data-ttu-id="5997a-147">**既定のタブ名 (最大 16 文字)?**</span><span class="sxs-lookup"><span data-stu-id="5997a-147">**Default Tab Name (max 16 characters)?**</span></span>

<span data-ttu-id="5997a-148">タブの名前を指定します。このタブ名は、ファイル/URL パス コンポーネントとしてプロジェクト全体で使用されます。</span><span class="sxs-lookup"><span data-stu-id="5997a-148">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
