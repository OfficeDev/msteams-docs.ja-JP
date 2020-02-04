## <a name="prerequisites"></a><span data-ttu-id="380ac-101">前提条件</span><span class="sxs-lookup"><span data-stu-id="380ac-101">Prerequisites</span></span>

- <span data-ttu-id="380ac-102">このクイックスタートを完了するには、Office 365 テナントと、[*カスタムアプリをアップロードできるようにする*] をオンにして構成されたチームが必要です。</span><span class="sxs-lookup"><span data-stu-id="380ac-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="380ac-103">詳細については、「 [Office 365 テナントを準備](~/concepts/build-and-test/prepare-your-o365-tenant.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="380ac-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="380ac-104">現在 Office 365 アカウントを持っていない場合は、Office 365 開発者プログラムを使用して無料のサブスクリプションにサインアップできます。</span><span class="sxs-lookup"><span data-stu-id="380ac-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="380ac-105">このサブスクリプションは、継続的な開発のために使用している限り、アクティブのままです。</span><span class="sxs-lookup"><span data-stu-id="380ac-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="380ac-106">「 [Office 365 開発者プログラムへようこそ」を](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="380ac-106">See [Welcome to the Office 365 Developer Program](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).</span></span>

<span data-ttu-id="380ac-107">また、このプロジェクトでは、開発環境に次のものがインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="380ac-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="380ac-108">任意のテキストエディターまたは IDE。</span><span class="sxs-lookup"><span data-stu-id="380ac-108">Any text editor or IDE.</span></span> <span data-ttu-id="380ac-109">[Visual Studio コード](https://code.visualstudio.com/download)を無料でインストールして使用することができます。</span><span class="sxs-lookup"><span data-stu-id="380ac-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="380ac-110">[Node.js/npm](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="380ac-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="380ac-111">最新の LTS バージョンを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="380ac-111">You should use the latest LTS version.</span></span> <span data-ttu-id="380ac-112">ノードパッケージマネージャー (npm) は、node.js のインストールによってシステムにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="380ac-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="380ac-113">Node.js のインストールが正常に完了したら、コマンドプロンプトに次のように入力して、 [gulp](https://www.npmjs.com/package/gulp-cli)パッケージと、cli パッケージを[インストールします](https://yeoman.io/)。</span><span class="sxs-lookup"><span data-stu-id="380ac-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

```bash
npm install yo gulp-cli --global
```

- <span data-ttu-id="380ac-114">コマンドプロンプトに次のように入力して、Microsoft Teams アプリジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="380ac-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a><span data-ttu-id="380ac-115">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="380ac-115">Generate your project</span></span>

- <span data-ttu-id="380ac-116">コマンドプロンプトを開き、タブプロジェクト用の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="380ac-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="380ac-117">ジェネレーターを開始するには、新しいディレクトリに移動し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="380ac-117">To start the generator, navigate to your new directory and type the following command:</span></span>

```bash
yo teams
```

- <span data-ttu-id="380ac-118">次に、アプリケーションの**manifest**ファイルで使用される一連の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="380ac-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

![ジェネレーターの開いているスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

<span data-ttu-id="380ac-120">**ソリューション名は何ですか。**</span><span class="sxs-lookup"><span data-stu-id="380ac-120">**What is your solution name?**</span></span>

<span data-ttu-id="380ac-121">これはプロジェクト名です。</span><span class="sxs-lookup"><span data-stu-id="380ac-121">This is your project name.</span></span> <span data-ttu-id="380ac-122">Enter キーを押すと、提案された名前を承諾できます。</span><span class="sxs-lookup"><span data-stu-id="380ac-122">You can accept the suggested name by pressing enter.</span></span>

<span data-ttu-id="380ac-123">**ファイルをどこに保存しますか?**</span><span class="sxs-lookup"><span data-stu-id="380ac-123">**Where do you want to place the files?**</span></span>

<span data-ttu-id="380ac-124">現在、プロジェクトディレクトリにいます。</span><span class="sxs-lookup"><span data-stu-id="380ac-124">You're currently in your project directory.</span></span> <span data-ttu-id="380ac-125">Enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="380ac-125">Press enter.</span></span>

<span data-ttu-id="380ac-126">**Microsoft Teams アプリプロジェクトのタイトル**</span><span class="sxs-lookup"><span data-stu-id="380ac-126">**Title of your Microsoft Teams app project?**</span></span>

<span data-ttu-id="380ac-127">これはアプリのパッケージ名で、アプリのマニフェストと説明に使用されます。</span><span class="sxs-lookup"><span data-stu-id="380ac-127">This is your app package name and will be used in the app manifest and description.</span></span>

<span data-ttu-id="380ac-128">**(会社) 名(最大32文字)**</span><span class="sxs-lookup"><span data-stu-id="380ac-128">**Your (company) name? (max 32 characters)**</span></span>

<span data-ttu-id="380ac-129">会社名はアプリマニフェストで使用されます。</span><span class="sxs-lookup"><span data-stu-id="380ac-129">Your company name will be used in the app manifest.</span></span>

<br><span data-ttu-id="380ac-130">**使用するマニフェストのバージョンを選択してください。**</span><span class="sxs-lookup"><span data-stu-id="380ac-130">**Which manifest version would you like to use?**</span></span>

<span data-ttu-id="380ac-131">[既定のスキーマ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="380ac-131">Select the default schema.</span></span>

<span data-ttu-id="380ac-132">**Microsoft パートナー Id を入力します (必要な場合)。(空白のままにしてください)**</span><span class="sxs-lookup"><span data-stu-id="380ac-132">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

<span data-ttu-id="380ac-133">このフィールドは必須ではなく、既に[Microsoft パートナーネットワーク](https://partner.microsoft.com)に属している場合にのみ使用してください。</span><span class="sxs-lookup"><span data-stu-id="380ac-133">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

<span data-ttu-id="380ac-134">**プロジェクトに何を追加しますか?**</span><span class="sxs-lookup"><span data-stu-id="380ac-134">**What do you want to add to your project?**</span></span>

<span data-ttu-id="380ac-135">タブを&ast;選択します ()。</span><span class="sxs-lookup"><span data-stu-id="380ac-135">Select ( &ast; ) A Tab.</span></span>

<span data-ttu-id="380ac-136">**このソリューションをホストする URL を指定します。**</span><span class="sxs-lookup"><span data-stu-id="380ac-136">**The URL where you will host this solution?**</span></span>

<span data-ttu-id="380ac-137">既定では、ジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="380ac-137">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="380ac-138">アプリのローカルテストのみが行われるため、このクイックスタートを完了するために有効な URL は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="380ac-138">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

<span data-ttu-id="380ac-139">**テストフレームワークと初期テストを含めますか?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="380ac-139">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

<span data-ttu-id="380ac-140">このプロジェクトのテストフレームワークを含め**ないこと**を選択します。</span><span class="sxs-lookup"><span data-stu-id="380ac-140">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="380ac-141">既定値は yes です。「 **n**」と入力します。</span><span class="sxs-lookup"><span data-stu-id="380ac-141">The default is yes; enter **n**.</span></span>

<span data-ttu-id="380ac-142">**テレメトリに Azure Application Insights を使用しますか?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="380ac-142">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

<span data-ttu-id="380ac-143">[Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md)を含め**ないこと**を選択します。</span><span class="sxs-lookup"><span data-stu-id="380ac-143">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="380ac-144">既定値は [いいえ; です。「 **n**」と入力します。</span><span class="sxs-lookup"><span data-stu-id="380ac-144">The default is no; enter **n**.</span></span>

<span data-ttu-id="380ac-145">**既定のタブ名 (最大16文字)?**</span><span class="sxs-lookup"><span data-stu-id="380ac-145">**Default Tab Name (max 16 characters)?**</span></span>

<span data-ttu-id="380ac-146">タブに名前を指定します。このタブ名は、ファイルまたは URL パスコンポーネントとしてプロジェクト全体で使用されます。</span><span class="sxs-lookup"><span data-stu-id="380ac-146">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
