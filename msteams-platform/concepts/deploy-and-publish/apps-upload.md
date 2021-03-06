---
title: カスタム アプリをアップロードする
description: Microsoft Teams でアプリをアップロードする方法について説明します
ms.topic: how-to
ms.author: lajanuar
keywords: teams アプリのアップロード
ms.openlocfilehash: 3ca086cf8dbb992de84b22b7499f739d7c80b9d6
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479884"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="84fb7-104">Microsoft Teams にアプリ パッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="84fb7-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="84fb7-105">Microsoft Teams でアプリ エクスペリエンスをテストするには、アプリを Teams にアップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="84fb7-106">アップロードすると、選択したチームにアプリが追加され、すべてのチーム メンバーがエンド ユーザーと同様に操作できます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-106">Uploading adds the app to the selected team and all the team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="84fb7-107">ボットを使用して既存のアプリの更新されたパッケージをアップロードすると、会話ウィンドウで表示されるタブの変更が表示されない場合があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the conversations window.</span></span> <span data-ttu-id="84fb7-108">アプリは、クリーンな環境でアプリの飛び出しやテストを通じてアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-108">You can access the app through the apps fly-out or test in a clean environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="84fb7-109">アップロード パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="84fb7-109">Create your upload package</span></span>

<span data-ttu-id="84fb7-110">開発および AppSource 申請では、アップロードできるパッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-110">For development and AppSource submission, you must create a package that you can upload.</span></span> <span data-ttu-id="84fb7-111">パッケージには、エクスペリエンスを説明する情報が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-111">The package must contain the information to describe your experience.</span></span> <span data-ttu-id="84fb7-112">パッケージは、アプリケーション マニフェストとエクスペリエンスを一意に定義するアイコンを含む .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="84fb7-112">The package is a .zip file that contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="84fb7-113">アップロード パッケージを作成するには、[「Microsoft Teams アプリのパッケージを作成する」](../build-and-test/apps-package.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="84fb7-113">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="84fb7-114">パッケージを作成した後、チームにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="84fb7-114">After you create the package, upload it into a team.</span></span> <span data-ttu-id="84fb7-115">アップロードされたパッケージは、選択したチームのユーザーだけが使用できます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-115">The uploaded package is only available to the users of the selected team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="84fb7-116">パッケージを Teams に読み込む</span><span class="sxs-lookup"><span data-stu-id="84fb7-116">Load your package into Teams</span></span>

<span data-ttu-id="84fb7-117">パッケージを Teams にアップロードしてテストすることができます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-117">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="84fb7-118">アップロードを機能させるには、テナント管理者が最初に[アプリのアップロードを有効にする](/microsoftteams/admin-settings)必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-118">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="84fb7-119">アプリを Teams にアップロードするには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-119">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="84fb7-120">ストアを使用する</span><span class="sxs-lookup"><span data-stu-id="84fb7-120">Using the Store</span></span>
* <span data-ttu-id="84fb7-121">[アプリ] タブを使用する</span><span class="sxs-lookup"><span data-stu-id="84fb7-121">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="84fb7-122">ストアを使用してチームまたは会話にパッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="84fb7-122">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="84fb7-123">Teams の左下隅で、[ストア] アイコン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-123">In the lower left corner of Teams, choose the **Store** icon.</span></span> <span data-ttu-id="84fb7-124">[ストア] ページで、[カスタム アプリ **のアップロード] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="84fb7-124">On the Store page, choose **Upload a custom app**.</span></span>

  ![チームを表示する](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="84fb7-126">[開く **]** ダイアログで、アップロードするパッケージに移動し、[開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-126">In the **Open** dialog, navigate to the package you want to upload and choose Open.</span></span>

   ![追加メニュー](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="84fb7-128">アップロードされたパッケージは、同意ダイアログで指定されたチームまたは会話で使用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-128">The uploaded package must be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="84fb7-129">アプリが表示されない場合、最も一般的な理由は、マニフェストのエラー、特にアプリ、ボット、メッセージング拡張機能の ID です。</span><span class="sxs-lookup"><span data-stu-id="84fb7-129">If your app does not appear, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span> <span data-ttu-id="84fb7-130">アプリがスレッドのスコープに設定されていない場合、オプションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="84fb7-130">If the app is not scoped for conversations that option does not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="84fb7-131">会話内のアプリは現在 [Developer Previewで](../../resources/dev-preview/developer-preview-intro.md)、Teams がそのモードで実行されていない場合、このオプションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="84fb7-131">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option does not appear if Teams is not running in that mode.</span></span>

![アップロードされたボットのリストにあるボットの例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="84fb7-133">[アプリ] タブを使用してパッケージをチームにアップロードする</span><span class="sxs-lookup"><span data-stu-id="84fb7-133">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="84fb7-134">ターゲット チームで、[その他のオプション] ( **[&#8943;]** を **選択し、[** チームの管理] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="84fb7-134">In the target team, choose **More options** (**&#8943;**) and select **Manage team**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="84fb7-135">この機能を表示するには、チームの所有者である必要があります。または所有者がユーザーにアクセス権を与え、この機能に適したアプリの種類を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-135">You must be the team owner or the owner must give access to users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="84fb7-136">[アプリ **] タブを** 選択し、右下 **の [カスタム アプリのアップロード** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-136">Select the **Apps** tab and choose **Upload a custom app** on the lower right.</span></span>

   ![アップロード エントリ ポイント](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="84fb7-138">コンピューターから .zip パッケージを選択します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-138">Select your .zip package from the computer.</span></span>

4. <span data-ttu-id="84fb7-139">アップロードしたアプリを一覧で確認できます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-139">You can see your uploaded app in the list.</span></span>

   ![アップロードされたボットのリストにあるボットの例](../../assets/images/botinlist.jpg)

<span data-ttu-id="84fb7-141">アプリが読み込めない場合、最も一般的な理由は、マニフェストのエラー、特にアプリ、ボット、メッセージング拡張機能の ID です。</span><span class="sxs-lookup"><span data-stu-id="84fb7-141">If your app does not load, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span>

## <a name="access-your-uploaded-configurable-tab"></a><span data-ttu-id="84fb7-142">アップロードした構成可能なタブにアクセスする</span><span class="sxs-lookup"><span data-stu-id="84fb7-142">Access your uploaded configurable tab</span></span>

<span data-ttu-id="84fb7-143">アプリにタブが含まれている場合、標準タブ ギャラリー フローを使用して、任意の会話またはチーム チャネルにユーザーをピン留めすることができます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-143">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="84fb7-144">チーム内のチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-144">Go to a channel in the team.</span></span> <span data-ttu-id="84fb7-145">既存 **+** のタブの右側にタブを追加する場合に選択します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-145">Choose **+** to add a tab to the right of the existing tabs.</span></span>

2. <span data-ttu-id="84fb7-146">表示されるギャラリーからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-146">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="84fb7-147">同意プロンプトを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-147">Accept the consent prompt.</span></span>

4. <span data-ttu-id="84fb7-148">構成ページでタブを [構成し、[保存](../../tabs/how-to/create-tab-pages/configuration-page.md) ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="84fb7-148">Configure your tab through its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and select **Save**.</span></span>

  ![使用可能なタブのギャラリーが表示された [タブの追加] ダイアログ ボックス](../../assets/images/tab_gallery.png)

## <a name="access-your-uploaded-bot"></a><span data-ttu-id="84fb7-150">アップロードしたボットにアクセスする</span><span class="sxs-lookup"><span data-stu-id="84fb7-150">Access your uploaded bot</span></span>

<span data-ttu-id="84fb7-151">ボットをチームに追加した後は、ボットスコープの定義に応じて、チームチャネルの内側と外側の誰でもボットを使用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-151">After adding the bot to a team, it must be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="84fb7-152">すべてのチーム メンバーは、ボットがチームに追加されたことを示す投稿を [全般] チャネルに表示できます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-152">All team members can see a post in the **General** channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="84fb7-153">Teams ボットの場合は、まずボットの名前を@mentioningしてボットを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-153">For a Teams bot, you can start by invoking your bot by @mentioning the name of the bot.</span></span>

<span data-ttu-id="84fb7-154">ボットと直接チャットをテストするには、アプリ ホームからアクセスするか、チャネルで@mention、新しいチャット ウィンドウで **検索します。**</span><span class="sxs-lookup"><span data-stu-id="84fb7-154">To test direct chats with your bot, you can either access it through the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="84fb7-155">ボットを@mentionチャットで確認したり、[新しいチャット] ウィンドウでボットを検索したりして、ボットとの直接チャットをテストできます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-155">You can @mention the bot in a conversation or search for it in the **New Chat** window to test direct chats with your bot.</span></span>

## <a name="access-your-uploaded-connector"></a><span data-ttu-id="84fb7-156">アップロードしたコネクタにアクセスする</span><span class="sxs-lookup"><span data-stu-id="84fb7-156">Access your uploaded Connector</span></span>

<span data-ttu-id="84fb7-157">アプリがチームや会話に読み込まれると、ユーザーは標準コネクタ ギャラリー フローを使用してコネクタを設定できます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-157">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="84fb7-158">チーム内のチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-158">Go to a channel in the team.</span></span> <span data-ttu-id="84fb7-159">**[その他のオプション]** (*&#8943;*) を選び、**[コネクタ]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-159">Choose **More options** (*&#8943;*) and choose **Connectors**.</span></span>

2. <span data-ttu-id="84fb7-160">一番下にある **[サイドロード]** セクションから [コネクタ] を選びます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-160">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="84fb7-161">構成ページでコネクタを [構成し、[保存](../../webhooks-and-connectors/how-to/connectors-creating.md) ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="84fb7-161">Configure your connector through its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and select **Save**.</span></span>

  ![使用可能なタブのギャラリーが表示された [タブの追加] ダイアログ ボックス。](../../assets/images/connector_gallery.png)

## <a name="access-your-uploaded-messaging-extension"></a><span data-ttu-id="84fb7-163">アップロードしたメッセージング拡張機能にアクセスする</span><span class="sxs-lookup"><span data-stu-id="84fb7-163">Access your uploaded messaging extension</span></span>

<span data-ttu-id="84fb7-164">メッセージング拡張機能を使用してアップロードされたアプリが自動的に [作成] ボックスの **[その他のオプション]** (*&#8943;*) メニューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-164">An uploaded app with a messaging extension automatically appears in the **More options** (*&#8943;*) menu in the compose box.</span></span>

![メッセージング拡張機能](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="84fb7-166">既定のインストール スコープとグループ機能を追加する</span><span class="sxs-lookup"><span data-stu-id="84fb7-166">Add a default install scope and group capability</span></span>

> [!NOTE]
> <span data-ttu-id="84fb7-167">既定のインストール スコープとグループ機能は、現在開発者プレビューでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-167">The default install scope and group capability is currently available in developer preview only.</span></span>

<span data-ttu-id="84fb7-168">個人用スコープにアプリをインストールすると、ほとんどのアプリで動作しますが、Teams ストアの一部のアプリでは、個人用スコープとチーム スコープの両方がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="84fb7-168">Although installing an app in the personal scope works for most apps, some of the apps in Teams Store support both personal and team scopes.</span></span>
<span data-ttu-id="84fb7-169">これらのアプリの中には、チーム、会議、またはグループチャットで動作することを目的とします。個人用アプリのエクスペリエンスはセカンダリです。</span><span class="sxs-lookup"><span data-stu-id="84fb7-169">Some of these apps are intended to work in a team, meetings, or a groupchat, with personal app experience being secondary.</span></span>
<span data-ttu-id="84fb7-170">既定のインストール スコープの選択は、発行する `defaultInstallScope` アプリを指定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-170">The default install scope selection helps you to specify the `defaultInstallScope` for the apps that you publish.</span></span> <span data-ttu-id="84fb7-171">アプリのインストール エクスペリエンスでは、ユーザーが既定のオプションを使用できます。残りはイメージで強調表示されているシェブロンの下に移動されます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-171">The app installation experience makes the default options available to the user, while the rest is moved under the chevron as highlighted in the image.</span></span>

![アプリの追加](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="84fb7-173">プロパティ `defaultInstallScope` は、個人、チーム、グループチャット、会議などの値をサポートします。</span><span class="sxs-lookup"><span data-stu-id="84fb7-173">The `defaultInstallScope` property supports values, such as personal, team, groupchat, or meetings.</span></span>

> [!NOTE]
><span data-ttu-id="84fb7-174">`defaultGroupCapability` は、チーム、グループチャット、または会議に追加される既定の機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-174">`defaultGroupCapability` provides the default capability that is added to the team, groupchat or meetings.</span></span> <span data-ttu-id="84fb7-175">アプリの既定の機能としてタブ、ボット、またはコネクタを選択しますが、アプリ定義で選択した機能が提供されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-175">Choose a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

## <a name="remove-or-update-your-app"></a><span data-ttu-id="84fb7-176">アプリを削除または更新する</span><span class="sxs-lookup"><span data-stu-id="84fb7-176">Remove or update your app</span></span>

<span data-ttu-id="84fb7-177">アプリを削除するには、[Teams ボットの表示] ボックスの一覧でアプリ名の横にある **削除アイコン** を選択します。</span><span class="sxs-lookup"><span data-stu-id="84fb7-177">To remove your app, select the delete icon next to the app name in the **View Teams** bots list.</span></span> <span data-ttu-id="84fb7-178">マニフェスト情報を変更する場合は、まずアプリを削除してから、更新されたパッケージを追加します。「パッケージをチームに読み込む」 [を参照してください](#load-your-package-into-teams)。</span><span class="sxs-lookup"><span data-stu-id="84fb7-178">If you change manifest information, first remove the app and then add the updated package, see [Load your package into a team](#load-your-package-into-teams).</span></span> <span data-ttu-id="84fb7-179">サービスのコード変更では、マニフェストを再度アップロードする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="84fb7-179">Code changes on your service do not require you to upload your manifest again.</span></span> <span data-ttu-id="84fb7-180">ただし、コードの変更で URL の変更やボットの Microsoft アプリ ID などのマニフェストの更新が必要な場合は、マニフェストを再度アップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="84fb7-180">However, if the code changes require manifest updates, such as changes to the URL or the Microsoft app ID for its bot, you must upload the manifest again.</span></span>

> [!NOTE]
> <span data-ttu-id="84fb7-181">個人用コンテキストからボットを完全に削除することはできません。</span><span class="sxs-lookup"><span data-stu-id="84fb7-181">You cannot remove a bot from a personal context entirely.</span></span> <span data-ttu-id="84fb7-182">ボットが削除され、再度追加された場合は、ボットとの追加の通信が前の会話に追加されます。</span><span class="sxs-lookup"><span data-stu-id="84fb7-182">If the bot is removed and added again, additional communication with the bot appends to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="84fb7-183">トラブルシューティングに関する注意</span><span class="sxs-lookup"><span data-stu-id="84fb7-183">Troubleshooting notes</span></span>

<span data-ttu-id="84fb7-184">マニフェストの読み込みに失敗した場合は、「パッケージの作成」のすべての手順[](../../concepts/build-and-test/apps-package.md)に従い、スキーマに対してマニフェストを検証したのか確認[します](../../resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="84fb7-184">If the manifest fails to load, check if you have followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
