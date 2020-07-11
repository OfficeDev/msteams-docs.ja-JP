---
title: Microsoft Teams でカスタムアプリをアップロードする
description: Microsoft Teams でアプリをアップロードする方法について説明します。
keywords: teams アプリのアップロード
ms.openlocfilehash: c130ef48d3ad7476de9ca5afeb7b613197c43f18
ms.sourcegitcommit: 3ba5a5a7d9d9d906abc3ee1df9c2177de0cfd767
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2020
ms.locfileid: "45103027"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="d088b-104">Microsoft Teams にアプリ パッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="d088b-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="d088b-105">Microsoft Teams 内でアプリの使用状況をテストするには、アプリを Teams にアップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d088b-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="d088b-106">アップロードすると、選択したチームにアプリが追加され、チームメンバーはエンドユーザーと同じように操作できるようになります。</span><span class="sxs-lookup"><span data-stu-id="d088b-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="d088b-107">既存のアプリの更新されたパッケージを bot にアップロードすると、[会話] ウィンドウで表示されているときに、タブの変更が表示されない場合があります。</span><span class="sxs-lookup"><span data-stu-id="d088b-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="d088b-108">アプリをフライアウトでアクセスするか、クリーンなテスト環境でテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d088b-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="d088b-109">アップロードパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="d088b-109">Create your upload package</span></span>

<span data-ttu-id="d088b-110">開発および AppSource (旧称 Office ストア) の送信については、使用状況を説明する情報を含む uploadable パッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d088b-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="d088b-111">パッケージ (.zip ファイル) には、ユーザーの環境を一意に定義するアプリケーションマニフェストとアイコンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d088b-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="d088b-112">アップロードパッケージを作成するには、「 [Microsoft Teams アプリ用のパッケージを作成](../build-and-test/apps-package.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d088b-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="d088b-113">パッケージを作成すると、それをチームにアップロードできるようになります。</span><span class="sxs-lookup"><span data-stu-id="d088b-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="d088b-114">アップロードすると、選択したチームのすべてのユーザーと、そのチームのユーザーのみが使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="d088b-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="d088b-115">Teams にパッケージを読み込む</span><span class="sxs-lookup"><span data-stu-id="d088b-115">Load your package into Teams</span></span>

<span data-ttu-id="d088b-116">パッケージは、Teams にアップロードすることによってテストできます。</span><span class="sxs-lookup"><span data-stu-id="d088b-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="d088b-117">アップロードを機能させるには、テナント管理者が最初[にアプリのアップロードを有効に](/microsoftteams/admin-settings)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d088b-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="d088b-118">アプリを Teams にアップロードするには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="d088b-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="d088b-119">ストアの使用</span><span class="sxs-lookup"><span data-stu-id="d088b-119">Using the Store</span></span>
* <span data-ttu-id="d088b-120">[アプリ] タブの使用</span><span class="sxs-lookup"><span data-stu-id="d088b-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="d088b-121">ストアを使用してチームまたは会話にパッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="d088b-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="d088b-122">Teams の左下隅で、[ストア] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="d088b-123">[ストア] ページで、[カスタムアプリのアップロード] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-123">On the Store page, choose "Upload a custom app".</span></span>

   ![チームの表示](../../assets/images/store-upload-a-custom-app.png)

2. <span data-ttu-id="d088b-125">[*開く*] ダイアログで、アップロードするパッケージに移動し、[*開く*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

<span data-ttu-id="d088b-126">アップロードされたパッケージは、同意ダイアログで指定されたチームまたは会話で使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="d088b-126">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="d088b-127">アプリが表示されない場合、最も一般的な原因は、マニフェストのエラー、特にアプリ、ボット、およびメッセージング拡張機能の id です。</span><span class="sxs-lookup"><span data-stu-id="d088b-127">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="d088b-128">アプリのスコープがスレッドに設定されていない場合、そのオプションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="d088b-128">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="d088b-129">現在、会話中のアプリは[開発者向けプレビュー](../../resources/dev-preview/developer-preview-intro.md)です。 Teams がこのモードで実行されていない場合は、オプションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="d088b-129">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![アップロードされたボットのリストにある bot の例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="d088b-131">[アプリ] タブを使用して、チームにパッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="d088b-131">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="d088b-132">ターゲットチームで、[*その他のオプション*(**&#8943;**)] を選択し、[*チームの管理*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-132">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d088b-133">この機能を表示するには、チームの所有者であるか、または所有者がユーザーが適切なアプリの種類を追加できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d088b-133">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="d088b-134">[アプリ] タブを選択し、右下の [*カスタムアプリをアップロードする*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-134">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![エントリポイントのアップロード](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="d088b-136">使用しているコンピューターから .zip パッケージを参照して選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-136">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="d088b-137">しばらくすると、アップロードしたアプリが一覧に表示されます。</span><span class="sxs-lookup"><span data-stu-id="d088b-137">After a brief pause you will see your uploaded app in the list.</span></span>

   ![アップロードされたボットのリストにある bot の例](../../assets/images/botinlist.jpg)

<span data-ttu-id="d088b-139">アプリが読み込まれない場合、最も一般的な原因は、マニフェストのエラー、特にアプリ、ボット、およびメッセージング拡張機能の id です。</span><span class="sxs-lookup"><span data-stu-id="d088b-139">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="d088b-140">アップロード可能な設定済みタブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="d088b-140">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="d088b-141">アプリにタブが含まれている場合、ユーザーは標準のタブギャラリーのフローを使用して、それらを任意の会話またはチームチャネルに固定できます。</span><span class="sxs-lookup"><span data-stu-id="d088b-141">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="d088b-142">チーム内のチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="d088b-142">Go to a channel in the team.</span></span> <span data-ttu-id="d088b-143">*+* 既存のタブの右側にある (*タブを追加*する) を選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-143">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="d088b-144">表示されるギャラリーからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-144">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="d088b-145">同意のプロンプトを承諾します。</span><span class="sxs-lookup"><span data-stu-id="d088b-145">Accept the consent prompt.</span></span>

4. <span data-ttu-id="d088b-146">[[構成] ページ](../../tabs/how-to/create-tab-pages/configuration-page.md)を使用してタブを構成し、[*保存*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-146">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  ![[タブの追加] ダイアログボックス。使用可能なタブのギャラリーが表示されます。](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="d088b-148">アップロードした bot へのアクセス</span><span class="sxs-lookup"><span data-stu-id="d088b-148">Accessing your uploaded bot</span></span>

<span data-ttu-id="d088b-149">Bot をチームに追加する場合、bot の範囲定義に応じて、チームチャネル内外のすべてのユーザーがそのチームを使用できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d088b-149">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="d088b-150">チームに bot が追加されたことを示す、他のチームメンバーには、一般的なチャネルで投稿が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d088b-150">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="d088b-151">Teams 対応の bot の場合は、bot の名前を @mentioning して bot を呼び出すことができます。これは、オートコンプリートでなければなりません。</span><span class="sxs-lookup"><span data-stu-id="d088b-151">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="d088b-152">Bot との直接チャットをテストするには、アプリのホームからアクセスするか、チャネルで @mention するか、または**新しい [チャット**] ウィンドウで検索します。</span><span class="sxs-lookup"><span data-stu-id="d088b-152">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="d088b-153">Bot を会話に追加して、bot との直接的なチャットをテストする場合は、会話でそれを @mention するか、**新しいチャット**ウィンドウで検索します。</span><span class="sxs-lookup"><span data-stu-id="d088b-153">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="d088b-154">アップロードされたコネクタへのアクセス</span><span class="sxs-lookup"><span data-stu-id="d088b-154">Accessing your uploaded Connector</span></span>

<span data-ttu-id="d088b-155">チームまたは会話にアプリが組み込まれたので、ユーザーは標準のコネクタギャラリーフローを使用してコネクタを設定できます。</span><span class="sxs-lookup"><span data-stu-id="d088b-155">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="d088b-156">チーム内のチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="d088b-156">Go to a channel in the team.</span></span> <span data-ttu-id="d088b-157">[*その他のオプション*(*&#8943;*)] を選択し、[*コネクタ*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-157">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="d088b-158">下部にある**サイドロード**セクションからコネクタを選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-158">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="d088b-159">[構成ページ](../../webhooks-and-connectors/how-to/connectors-creating.md)からコネクタを構成し、[*保存*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-159">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  ![[タブの追加] ダイアログボックス。使用可能なタブのギャラリーが表示されます。](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="d088b-161">アップロードされたメッセージング拡張機能へのアクセス</span><span class="sxs-lookup"><span data-stu-id="d088b-161">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="d088b-162">メッセージ拡張機能を使用してアップロードしたアプリは、[新規作成] ボックスの [*その他のオプション*(*&#8943;*)] メニューに自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="d088b-162">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![メッセージングの拡張機能](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="d088b-164">アプリを削除または更新する</span><span class="sxs-lookup"><span data-stu-id="d088b-164">Removing or updating your app</span></span>

<span data-ttu-id="d088b-165">アプリを削除する場合は、[チームのボットの表示] リストのアプリ名の横にある [ごみ箱] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d088b-165">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="d088b-166">マニフェスト情報を変更する場合は、最初にアプリを削除してから、更新されたパッケージ ([パッケージをチームに読み込む](#load-your-package-into-teams)ごと) を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d088b-166">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="d088b-167">一般的には、サービス上でコードを変更しても、マニフェストの更新が必要になる (たとえば、URL への変更や bot の Microsoft アプリ ID など) 必要がある場合を除いて、マニフェストを再アップロードする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d088b-167">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="d088b-168">Bot を個人コンテキストから完全に削除する方法はありません。</span><span class="sxs-lookup"><span data-stu-id="d088b-168">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="d088b-169">Bot が削除されて再度追加されると、bot との追加の通信は前の会話に追加されます。</span><span class="sxs-lookup"><span data-stu-id="d088b-169">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="d088b-170">トラブルシューティングのメモ</span><span class="sxs-lookup"><span data-stu-id="d088b-170">Troubleshooting notes</span></span>

* <span data-ttu-id="d088b-171">マニフェストが読み込まれていない場合は、「[パッケージを作成](../../concepts/build-and-test/apps-package.md)し、[スキーマ](../../resources/schema/manifest-schema.md)に対してマニフェストを検証する」に記載されているすべての手順に従っていることをもう一度確認してください。</span><span class="sxs-lookup"><span data-stu-id="d088b-171">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>

