## <a name="prerequisites"></a><span data-ttu-id="ca8e3-101">前提条件</span><span class="sxs-lookup"><span data-stu-id="ca8e3-101">Prerequisites</span></span>

- <span data-ttu-id="ca8e3-102">このクイック スタートを完了するには、Office 365テナントと、カスタム アプリの *アップロードを許可する* を有効にして構成されたチームが必要です。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="ca8e3-103">詳細については[、「Office 365テナントの準備」を](~/concepts/build-and-test/prepare-your-o365-tenant.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="ca8e3-104">現在Office 365アカウントをお持ちの場合は、Office 365デベロッパープログラムを通じて無料のサブスクリプションにサインアップできます。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="ca8e3-105">サブスクリプションは、継続的な開発に使用している限り、アクティブなままになります。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="ca8e3-106">[「Office 365開発者プログラムへようこそ](/office/developer-program/microsoft-365-developer-program)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-106">See [Welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="ca8e3-107">さらに、このプロジェクトでは、開発環境に次のインストールが必要です。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="ca8e3-108">任意のテキスト エディタまたは IDE。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-108">Any text editor or IDE.</span></span> <span data-ttu-id="ca8e3-109">[Visual Studio Code](https://code.visualstudio.com/download)を無料でインストールして使用できます。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="ca8e3-110">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="ca8e3-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="ca8e3-111">最新の LTS バージョンを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-111">You should use the latest LTS version.</span></span> <span data-ttu-id="ca8e3-112">ノード パッケージ マネージャー (npm) は、Node.jsのインストールと共にシステムにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="ca8e3-113">Node.js正常にインストールできたら、コマンド プロンプトに次のように入力して [、Yeoman](https://yeoman.io/) と [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="ca8e3-114">コマンド プロンプトで次のように入力して、Microsoft Teams Apps ジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a><span data-ttu-id="ca8e3-115">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="ca8e3-115">Generate your project</span></span>

- <span data-ttu-id="ca8e3-116">コマンド プロンプトを開き、タブ プロジェクト用の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="ca8e3-117">ジェネレータを起動するには、新しいディレクトリに移動し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-117">To start the generator, navigate to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

- <span data-ttu-id="ca8e3-118">次に、アプリケーションの **manifest.jsファイル** で使用される一連の値を指定します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

    ![ジェネレータの開くスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="ca8e3-120">**ソリューション名は何ですか?**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-120">**What is your solution name?**</span></span>

    <span data-ttu-id="ca8e3-121">これはプロジェクト名です。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-121">This is your project name.</span></span> <span data-ttu-id="ca8e3-122">Enter キーを押すと、候補名を受け入れることができます。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-122">You can accept the suggested name by pressing enter.</span></span>

    <span data-ttu-id="ca8e3-123">**ファイルをどこに保存しますか?**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-123">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="ca8e3-124">現在プロジェクト ディレクトリに入っています。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-124">You're currently in your project directory.</span></span> <span data-ttu-id="ca8e3-125">Enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-125">Press enter.</span></span>

    <span data-ttu-id="ca8e3-126">**Microsoft Teams アプリ プロジェクトのタイトル**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-126">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="ca8e3-127">これはアプリ パッケージ名で、アプリ マニフェストと説明で使用されます。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-127">This is your app package name and will be used in the app manifest and description.</span></span>

    <span data-ttu-id="ca8e3-128">**あなたの(会社の)名前?(最大 32 文字)**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-128">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="ca8e3-129">会社名はアプリ マニフェストで使用されます。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-129">Your company name will be used in the app manifest.</span></span>

    <span data-ttu-id="ca8e3-130">**どのマニフェスト バージョンを使用しますか?**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-130">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="ca8e3-131">既定のスキーマを選択します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-131">Select the default schema.</span></span>

    <span data-ttu-id="ca8e3-132">**クイック足場?(Y/n)**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-132">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="ca8e3-133">デフォルトは yes です。 **n** と入力して、マイクロソフト パートナー ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-133">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="ca8e3-134">**マイクロソフト パートナー ID をお持ちの場合は、その Id を入力してください。(スキップするには空白のままにします)**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-134">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="ca8e3-135">このフィールドは必須ではなく、既に [Microsoft パートナー ネットワーク](https://partner.microsoft.com)に参加している場合にのみ使用してください。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-135">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="ca8e3-136">**プロジェクトに追加する項目を指定してください。**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-136">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="ca8e3-137">&ast;タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-137">Select ( &ast; ) A Tab.</span></span>

    <span data-ttu-id="ca8e3-138">**このソリューションをホストする URL?**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-138">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="ca8e3-139">既定では、ジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-139">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="ca8e3-140">アプリをローカルでテストするだけなので、このクイック スタートを完了するために有効な URL は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-140">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

    <span data-ttu-id="ca8e3-141">**テスト フレームワークと初期テストを含めますか?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-141">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="ca8e3-142">このプロジェクトのテスト フレームワークを含 **めないように** 選択します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-142">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="ca8e3-143">デフォルトは yes です。 **n** と入力します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-143">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="ca8e3-144">**テレメトリに Azure アプリケーションの洞察を使用しますか?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-144">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="ca8e3-145">Azure アプリケーション [インサイト](/azure-docs/articles/azure-monitor/app/app-insights-overview.md)を含 **まない** 場合に選択します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-145">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="ca8e3-146">デフォルトは no です。 **n** と入力します。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-146">The default is no; enter **n**.</span></span>

    <span data-ttu-id="ca8e3-147">**デフォルトのタブ名(最大16文字)?**</span><span class="sxs-lookup"><span data-stu-id="ca8e3-147">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="ca8e3-148">タブに名前を付けます。このタブ名は、プロジェクト全体でファイル/URL パスコンポーネントとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="ca8e3-148">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
