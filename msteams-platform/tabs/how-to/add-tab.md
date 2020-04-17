---
title: カスタムタブを使用して Teams アプリを拡張する
author: laujan
description: タブを作成するためのガイド
keywords: 構成可能な teams タブグループチャネル
ms.topic: conceptual
ms.author: ''
ms.openlocfilehash: 9f12f9eb39e4dfac4d5b725638bdbd2d7c2b4de6
ms.sourcegitcommit: b8b06929981ebbeef4ae489f338271bf09d349a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "43537272"
---
# <a name="extend-your-teams-app-with-a-custom-tab"></a><span data-ttu-id="5d0fc-104">カスタムタブを使用して Teams アプリを拡張する</span><span class="sxs-lookup"><span data-stu-id="5d0fc-104">Extend your Teams app with a custom tab</span></span>

<span data-ttu-id="5d0fc-105">カスタムタブを使用すると、チャネル、グループチャット、および個人ユーザーに対してホストする web コンテンツを提供できます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-105">Custom tabs allow you to serve web content that you host to your channel, group chat, and personal users.</span></span> <span data-ttu-id="5d0fc-106">高レベルでは、次の手順を実行してタブを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-106">At a high level, you'll need to complete the following steps to create a tab:</span></span>

1. <span data-ttu-id="5d0fc-107">開発環境を準備する。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-107">Prepare your development environment.</span></span>
1. <span data-ttu-id="5d0fc-108">ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-108">Create your page(s).</span></span>
1. <span data-ttu-id="5d0fc-109">アプリサービスをホストします。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-109">Host your app service.</span></span>
1. <span data-ttu-id="5d0fc-110">アプリパッケージを作成し、Microsoft Teams にアップロードします。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-110">Create your app package and upload to Microsoft Teams.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-pages"></a><span data-ttu-id="5d0fc-111">ページを作成する</span><span class="sxs-lookup"><span data-stu-id="5d0fc-111">Create your page(s)</span></span>

<span data-ttu-id="5d0fc-112">個人またはチャネル/グループのスコープ内にタブを表示するかどうかにかかわらず、ホストする1つ以上の HTML ページから構成されます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-112">Whether you present your tab within the personal or channel/group scope, it will consist of one or more HTML pages that you host.</span></span> <span data-ttu-id="5d0fc-113">個人のスコープを持つタブは単一のコンテンツページで構成され、チャネルまたはグループのスコープを持つタブでは、インストール時のユーザー入力に基づいてコンテンツページの URL を設定する構成ページが必要になります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-113">Tabs with a personal scope consist of a single content page, while tabs with a channel or group scope will require a configuration page that sets the URL of the content page based on user input at the time of installation.</span></span>

<span data-ttu-id="5d0fc-114">タブページには3つの種類があります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-114">There are three types of tab pages.</span></span> <span data-ttu-id="5d0fc-115">作成の詳細については、対応するドキュメントページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-115">See the corresponding documentation page for full details on creating them.</span></span>

1. <span data-ttu-id="5d0fc-116">[コンテンツページ](~/tabs/how-to/create-tab-pages/content-page.md)(タブに表示されるページ)。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-116">[Content page](~/tabs/how-to/create-tab-pages/content-page.md), the page displayed in a tab.</span></span>
1. <span data-ttu-id="5d0fc-117">[[構成] ページ](~/tabs/how-to/create-tab-pages/configuration-page.md)。コンテンツページの URL を設定または更新し、[チャネル/グループ] タブに追加するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-117">[Configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md), the page used to set or update the content page URL, and add it to a channel/group tab.</span></span>
1. <span data-ttu-id="5d0fc-118">[削除ページ](~/tabs/how-to/create-tab-pages/removal-page.md)。 [チャネル/グループ] タブが削除されたときに表示されるオプションのページです。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-118">[Removal page](~/tabs/how-to/create-tab-pages/removal-page.md), an optional page that is displayed when a channel/group tab is removed.</span></span>

### <a name="tab-requirements"></a><span data-ttu-id="5d0fc-119">タブの要件</span><span class="sxs-lookup"><span data-stu-id="5d0fc-119">Tab requirements</span></span>

<span data-ttu-id="5d0fc-120">ページの種類に関係なく、タブは次の要件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-120">Regardless of the type of page, you're tab will need to adhere to the following requirements:</span></span>

* <span data-ttu-id="5d0fc-121">X フレームオプションまたはコンテンツセキュリティポリシーの HTTP 応答ヘッダーを使用して、IFrame でページを処理できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-121">You must allow your pages to be served in an IFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="5d0fc-122">Set header:`Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="5d0fc-122">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>        
  * <span data-ttu-id="5d0fc-123">Internet Explorer 11 との互換性の`X-Content-Security-Policy`ためにも設定します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-123">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>    
  * <span data-ttu-id="5d0fc-124">または、ヘッダー `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`を設定します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-124">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="5d0fc-125">このヘッダーは推奨されていませんが、ほとんどのブラウザーで尊重されています。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-125">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="5d0fc-126">通常、クリック-jacking に対する保護手段として、ログインページは Iframe では表示されません。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-126">Typically, as a safeguard against click-jacking, login pages don't render in IFrames.</span></span> <span data-ttu-id="5d0fc-127">そのため、認証ロジックでは、リダイレクト以外のメソッドを使用する必要があります (たとえば、トークンベースまたは cookie ベースの認証を使用します)。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-127">Therefore, your authentication logic needs to use a method other than redirect (e.g., use token-based or cookie-based authentication).</span></span>

> [!NOTE]
> <span data-ttu-id="5d0fc-128">Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-128">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="5d0fc-129">既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-129">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="5d0fc-130">「[SameSite Cookie 属性 (2020 更新プログラム)](../../resources/samesite-cookie-update.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-130">*See* [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="5d0fc-131">ブラウザーは、web ページを提供するドメインとは別のドメインに対する要求を web ページから実行できないようにする、同一生成元ポリシー制限に従います。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-131">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="5d0fc-132">ただし、別のドメインまたはサブドメインに、構成ページまたはコンテンツページをリダイレクトする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-132">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="5d0fc-133">クロスドメインナビゲーションロジックにより、チームクライアントは、タブを読み込んだり通信したりするときに、アプリマニフェストの静的な validDomains リストに対して生成元を検証できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-133">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="5d0fc-134">シームレスな環境を作成するには、Teams クライアントのテーマ、設計、および目的に基づいて、タブのスタイルを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-134">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="5d0fc-135">通常、タブは、特定のニーズに対応するように構築され、タブのチャネルの場所に関連する一連の小さなタスクまたはデータのサブセットに焦点を当てるように構築されている場合に最適に機能します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-135">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="5d0fc-136">コンテンツページ内で、script タグを使用して[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-136">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="5d0fc-137">ページの読み込みの後、に`microsoftTeams.initialize()`電話をかけます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-137">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="5d0fc-138">使用しない場合、ページは表示されません。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-138">Your page will not be displayed if you do not.</span></span>

## <a name="host-your-app-service"></a><span data-ttu-id="5d0fc-139">アプリサービスをホストする</span><span class="sxs-lookup"><span data-stu-id="5d0fc-139">Host your app service</span></span>

<span data-ttu-id="5d0fc-140">コンテンツは HTTPS を使用して利用可能な公開 URL でホストされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-140">Your content needs to be hosted on a publicly available URL available using HTTPS.</span></span> <span data-ttu-id="5d0fc-141">テストのために、 [ngrok](https://ngrok.com/)などのリバースプロキシを使用して、ローカルポートをインターネットに接続する URL に公開することができます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-141">For testing, you can use a reverse proxy, such as [ngrok](https://ngrok.com/), to expose your local port to an internet-facing URL.</span></span>

## <a name="create-your-app-package-with-app-studio"></a><span data-ttu-id="5d0fc-142">アプリ Studio を使用してアプリパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="5d0fc-142">Create your app package with App Studio</span></span>

<span data-ttu-id="5d0fc-143">アプリのマニフェストを作成するために、Microsoft Teams クライアント内からアプリ Studio アプリを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-143">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span> <span data-ttu-id="5d0fc-144">Teams にアプリ studio がインストールされていない場合は、teams](/microsoftteams/platform/assets/images/tab-images/storeApp.png)アプリの左下隅にある [**アプリ** ![ストアアプリ] を選択して、アプリ studio を検索します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-144">If you do not have App studio installed in Teams, select **Apps** ![Store App](/microsoftteams/platform/assets/images/tab-images/storeApp.png) at the bottom-left corner of the Teams app, and search for App Studio.</span></span> <span data-ttu-id="5d0fc-145">タイルを見つけたら、それを選択して、[ポップアップウィンドウ] ダイアログボックスの [インストール] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-145">Once you find the tile, select it and choose install in the pop-up window dialog box.</span></span>

1. <span data-ttu-id="5d0fc-146">Microsoft Teams クライアントを開く- [web ベースのバージョン](https://teams.microsoft.com)を使用すると、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンドコードを検査できます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-146">Open the Microsoft Teams client—using the [web based version](https://teams.microsoft.com) will enable you to inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="5d0fc-147">App Studio を開き、[**マニフェストエディター** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-147">Open App Studio and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="5d0fc-148">[**新しいアプリタイルを作成する**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-148">Choose the **Create a new app** tile.</span></span>
1. <span data-ttu-id="5d0fc-149">アプリの詳細を追加します (各フィールドの詳細については、「[マニフェストスキーマ定義](~/resources/schema/manifest-schema.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-149">Add your app details (see the [manifest schema definition](~/resources/schema/manifest-schema.md) for full description of each field).</span></span>
1. <span data-ttu-id="5d0fc-150">[機能] セクションで、[**タブ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-150">In the capabilities section select **Tabs**.</span></span>
    * <span data-ttu-id="5d0fc-151">[個人] タブで、[*個人用タブの追加]* を選択し、[**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-151">For a personal tab, choose *Add a personal tab* and select **Add**.</span></span> <span data-ttu-id="5d0fc-152">ポップアップダイアログウィンドウが表示され、タブの詳細を追加できます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-152">You will be presented with a pop-up dialogue window where you can add your tab details.</span></span>
    * <span data-ttu-id="5d0fc-153">[チャネル/グループ] タブの [*チーム*] タブで、[**追加**] を選択し、[チーム] タブのポップアップウィンドウにあるタブの詳細フィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-153">For a channel/group tab, under *Team Tab* select **Add** and complete the tab details fields in the Team tab pop-up window.</span></span> <span data-ttu-id="5d0fc-154">が*構成を更新できることを確認するチーム*および*グループのチャット*ボックスがチェックされ、[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-154">Make sure the *can update configuration? Team* and *Group chat* boxes are checked and select **Save**.</span></span>
1. <span data-ttu-id="5d0fc-155">[*ドメインと権限*] セクションで、[*タブのドメイン*] フィールドに、HTTPS プレフィックスのないホストまたはリバースプロキシの URL が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-155">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your host or reverse proxy URL without the HTTPS prefix.</span></span>
1. <span data-ttu-id="5d0fc-156">**[** => **テストと配布**の終了] タブでは、アプリパッケージを**ダウンロード**するか、パッケージをチームに**インストール**するか、Teams アプリストアに**提出**して承認を受けることができます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-156">From the **Finish** => **Test and distribute** tab you can **Download** your app package, **Install** the package into a team, or **Submit** to the Teams app store for approval.</span></span> <span data-ttu-id="5d0fc-157">*リバースプロキシを使用している場合は、右側の [**説明**] フィールドに警告が表示されます。タブのテスト中は、この警告を無視でき*ます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-157">*If you are using a reverse proxy you will get a warning in the **Description** field on the right. The warning can be ignored while testing your tab*.</span></span>

## <a name="create-your-app-package-manually"></a><span data-ttu-id="5d0fc-158">アプリ パッケージを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="5d0fc-158">Create your app package manually</span></span>

<span data-ttu-id="5d0fc-159">ボットおよびメッセージング拡張機能と同様に、タブのプロパティを含むようにアプリの[アプリマニフェスト](~/resources/schema/manifest-schema.md)を更新します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-159">As with bots and messaging extensions, you update the [app manifest](~/resources/schema/manifest-schema.md) of your app to include the tab properties.</span></span> <span data-ttu-id="5d0fc-160">これらのプロパティは、タブが使用可能な範囲、使用する Url、およびその他のさまざまなプロパティを制御します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-160">These properties govern the scopes your tab is available in, the URLs to be used, and various other properties.</span></span>

### <a name="personal-tabs"></a><span data-ttu-id="5d0fc-161">個人用タブ</span><span class="sxs-lookup"><span data-stu-id="5d0fc-161">Personal Tabs</span></span>

<span data-ttu-id="5d0fc-162">個人用タブに表示されるコンテンツは、すべてのユーザーに対して同じで`staticTabs`あり、配列に構成されています。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-162">The displayed content for personal tabs is the same for all users and is configured in the `staticTabs` array.</span></span> <span data-ttu-id="5d0fc-163">アプリで最大16個の個人用タブを宣言することができます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-163">You may declare up to sixteen (16) personal tabs in an app.</span></span>

|<span data-ttu-id="5d0fc-164">名前</span><span class="sxs-lookup"><span data-stu-id="5d0fc-164">Name</span></span>| <span data-ttu-id="5d0fc-165">型</span><span class="sxs-lookup"><span data-stu-id="5d0fc-165">Type</span></span>| <span data-ttu-id="5d0fc-166">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="5d0fc-166">Maximum size</span></span> | <span data-ttu-id="5d0fc-167">必須</span><span class="sxs-lookup"><span data-stu-id="5d0fc-167">Required</span></span> | <span data-ttu-id="5d0fc-168">説明</span><span class="sxs-lookup"><span data-stu-id="5d0fc-168">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="5d0fc-169">String</span><span class="sxs-lookup"><span data-stu-id="5d0fc-169">String</span></span>|<span data-ttu-id="5d0fc-170">64 文字</span><span class="sxs-lookup"><span data-stu-id="5d0fc-170">64 characters</span></span>|<span data-ttu-id="5d0fc-171">✔</span><span class="sxs-lookup"><span data-stu-id="5d0fc-171">✔</span></span>|<span data-ttu-id="5d0fc-172">タブに表示されるエンティティの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-172">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="5d0fc-173">String</span><span class="sxs-lookup"><span data-stu-id="5d0fc-173">String</span></span>|<span data-ttu-id="5d0fc-174">128文字</span><span class="sxs-lookup"><span data-stu-id="5d0fc-174">128 characters</span></span>|<span data-ttu-id="5d0fc-175">✔</span><span class="sxs-lookup"><span data-stu-id="5d0fc-175">✔</span></span>|<span data-ttu-id="5d0fc-176">チャネルインターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-176">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="5d0fc-177">String</span><span class="sxs-lookup"><span data-stu-id="5d0fc-177">String</span></span>|<span data-ttu-id="5d0fc-178">2048 文字</span><span class="sxs-lookup"><span data-stu-id="5d0fc-178">2048 characters</span></span>|<span data-ttu-id="5d0fc-179">✔</span><span class="sxs-lookup"><span data-stu-id="5d0fc-179">✔</span></span>|<span data-ttu-id="5d0fc-180">Teams キャンバスに表示されるエンティティ UI をポイントする https://URL。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-180">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="5d0fc-181">String</span><span class="sxs-lookup"><span data-stu-id="5d0fc-181">String</span></span>|<span data-ttu-id="5d0fc-182">2048 文字</span><span class="sxs-lookup"><span data-stu-id="5d0fc-182">2048 characters</span></span>||<span data-ttu-id="5d0fc-183">ユーザーがブラウザーで表示をポイントしたかどうかを示す https://URL。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-183">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="5d0fc-184">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="5d0fc-184">Array of enum</span></span>|<span data-ttu-id="5d0fc-185">1-d</span><span class="sxs-lookup"><span data-stu-id="5d0fc-185">1</span></span>|<span data-ttu-id="5d0fc-186">✔</span><span class="sxs-lookup"><span data-stu-id="5d0fc-186">✔</span></span>|<span data-ttu-id="5d0fc-187">静的タブでは、 `personal`スコープのみがサポートされます。つまり、個人用アプリの一部としてのみプロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-187">Static tabs support only the `personal` scope, which means it can be provisioned only as part of a personal app.</span></span>|

#### <a name="simple-personal-tab-manifest-example"></a><span data-ttu-id="5d0fc-188">シンプルな個人用タブマニフェストの例</span><span class="sxs-lookup"><span data-stu-id="5d0fc-188">Simple personal tab manifest example</span></span>

<span data-ttu-id="5d0fc-189">次の例は、アプリ`staticTabs`マニフェストからの配列のみを示しています。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-189">The example below shows just the `staticTabs` array from an app manifest.</span></span>

```json
...
"staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name for tab",
      "contentUrl": "https:// yourURL.com/content ",
      "websiteUrl": "https://yourURL.com/website",
      "scopes": [ "personal" ]
    }
...
```

### <a name="channelgroup-tabs"></a><span data-ttu-id="5d0fc-190">チャネル/グループタブ</span><span class="sxs-lookup"><span data-stu-id="5d0fc-190">Channel/group tabs</span></span>

<span data-ttu-id="5d0fc-191">チャネルまたはグループのタブが`configurableTabs`配列に追加されます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-191">Channel/group tabs are added in the `configurableTabs` array.</span></span> <span data-ttu-id="5d0fc-192">配列には、 `configurableTabs` [チャネル/グループ] タブを1つだけ宣言できます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-192">You may declare only one channel/group tab in the `configurableTabs` array.</span></span>

|<span data-ttu-id="5d0fc-193">名前</span><span class="sxs-lookup"><span data-stu-id="5d0fc-193">Name</span></span>| <span data-ttu-id="5d0fc-194">型</span><span class="sxs-lookup"><span data-stu-id="5d0fc-194">Type</span></span>| <span data-ttu-id="5d0fc-195">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="5d0fc-195">Maximum size</span></span> | <span data-ttu-id="5d0fc-196">必須</span><span class="sxs-lookup"><span data-stu-id="5d0fc-196">Required</span></span> | <span data-ttu-id="5d0fc-197">説明</span><span class="sxs-lookup"><span data-stu-id="5d0fc-197">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="5d0fc-198">String</span><span class="sxs-lookup"><span data-stu-id="5d0fc-198">String</span></span>|<span data-ttu-id="5d0fc-199">2048 文字</span><span class="sxs-lookup"><span data-stu-id="5d0fc-199">2048 characters</span></span>|<span data-ttu-id="5d0fc-200">✔</span><span class="sxs-lookup"><span data-stu-id="5d0fc-200">✔</span></span>|<span data-ttu-id="5d0fc-201">Https://URL を構成するページ。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-201">The https:// URL to configuration page.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="5d0fc-202">Boolean</span><span class="sxs-lookup"><span data-stu-id="5d0fc-202">Boolean</span></span>|||<span data-ttu-id="5d0fc-203">作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-203">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="5d0fc-204">限り`true`</span><span class="sxs-lookup"><span data-stu-id="5d0fc-204">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="5d0fc-205">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="5d0fc-205">Array of enum</span></span>|<span data-ttu-id="5d0fc-206">1-d</span><span class="sxs-lookup"><span data-stu-id="5d0fc-206">1</span></span>|<span data-ttu-id="5d0fc-207">✔</span><span class="sxs-lookup"><span data-stu-id="5d0fc-207">✔</span></span>|<span data-ttu-id="5d0fc-208">構成可能なタブで`team`は`groupchat` 、および範囲のみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-208">Configurable tabs support only the `team` and `groupchat` scopes.</span></span> |

#### <a name="simple-channelgroup-tab-manifest-example"></a><span data-ttu-id="5d0fc-209">シンプルなチャネル/グループタブマニフェストの例</span><span class="sxs-lookup"><span data-stu-id="5d0fc-209">Simple channel/group tab manifest example</span></span>

<span data-ttu-id="5d0fc-210">次の例は、アプリ`configurableTabs`マニフェストからの配列のみを示しています。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-210">The example below shows just the `configurableTabs` array from an app manifest.</span></span>

```json
...
"configurableTabs": [
    {
      "configurationUrl": "https://yourURL.com/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
...
```

<span data-ttu-id="5d0fc-211">2つの必須アイコン`manifest.json`と共に、zip フォルダーでバンドルを完了した後。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-211">Once you have completed your `manifest.json` bundle it in a zip folder along with your two required icons.</span></span>

### <a name="upload-app-package-directly-to-a-team"></a><span data-ttu-id="5d0fc-212">アプリパッケージを直接チームにアップロードする</span><span class="sxs-lookup"><span data-stu-id="5d0fc-212">Upload app package directly to a team</span></span>

1. <span data-ttu-id="5d0fc-213">Microsoft Teams クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-213">Open the Microsoft Teams client.</span></span> <span data-ttu-id="5d0fc-214">[Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンドコードを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-214">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="5d0fc-215">左側の [*チーム*] パネルで、使用して`...`いるチームの横のメニューを選択して、タブのテストを行い、[**チームの管理**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-215">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
1. <span data-ttu-id="5d0fc-216">メインパネルで、タブバーから [**アプリ**] を選択し、ページの右下隅にある [**カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-216">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
1. <span data-ttu-id="5d0fc-217">プロジェクトディレクトリを開き、 **./パッケージ**フォルダーを参照して、アプリパッケージの zip フォルダーを選択し、[**開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-217">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="5d0fc-218">タブが Teams にアップロードされます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-218">Your tab will upload into Teams.</span></span>

### <a name="view-your-tab-in-teams"></a><span data-ttu-id="5d0fc-219">Teams でタブを表示する</span><span class="sxs-lookup"><span data-stu-id="5d0fc-219">View your tab in Teams</span></span>

1. <span data-ttu-id="5d0fc-220">[個人用] タブを表示します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-220">View your personal tab:</span></span>
    * <span data-ttu-id="5d0fc-221">Teams クライアントの左端にあるナビゲーションバーで、 `...`メニューを選択し、リストからアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-221">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>

1. <span data-ttu-id="5d0fc-222">[チャネル/グループ] タブを表示します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-222">View your channel/group tab:</span></span>
    * <span data-ttu-id="5d0fc-223">チームに戻り、タブを表示するチャネルを選択し、タブバーから [➕] を選択して、ギャラリーからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-223">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
    * <span data-ttu-id="5d0fc-224">タブを追加する手順に従います。 [チャネル/グループ] タブには、カスタム構成ダイアログがあることに注意してください。 [**保存**] を選択すると、タブがチャネルのタブバーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="5d0fc-224">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab. Select **Save** and your tab will be added to the channel's tab bar.</span></span>

## <a name="learn-more"></a><span data-ttu-id="5d0fc-225">詳細情報</span><span class="sxs-lookup"><span data-stu-id="5d0fc-225">Learn more</span></span>

* [<span data-ttu-id="5d0fc-226">タブのコンテンツページを作成する</span><span class="sxs-lookup"><span data-stu-id="5d0fc-226">Create a content page for your tab</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="5d0fc-227">タブの構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="5d0fc-227">Create a configuration page for your tab</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="5d0fc-228">タブを更新または削除する</span><span class="sxs-lookup"><span data-stu-id="5d0fc-228">Update or remove a tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
