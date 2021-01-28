---
title: カスタム アプリをアップロードする
description: Microsoft Teams でアプリをアップロードする方法について説明します
ms.topic: how-to
keywords: Teams アプリのアップロード
ms.openlocfilehash: 2e7a21dc27fdfe824ecacebabbb61a3b99ae8e79
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014342"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="b8e0e-104">Microsoft Teams にアプリ パッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="b8e0e-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="b8e0e-105">Microsoft Teams でアプリ エクスペリエンスをテストするには、アプリを Teams にアップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="b8e0e-106">アップロードすると、アプリが選択したチームに追加されます。チーム メンバーは、エンド ユーザーのようにアプリを操作できます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="b8e0e-107">ボットを使用して既存のアプリの更新されたパッケージをアップロードすると、[会話] ウィンドウで、タブの変更が表示されない場合があります。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="b8e0e-108">アプリのフライアウトを介してアクセスするか、クリーンなテスト環境でテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="b8e0e-109">アップロード パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="b8e0e-109">Create your upload package</span></span>

<span data-ttu-id="b8e0e-110">開発および AppSource (以前の Office ストア) 提供の場合は、エクスペリエンスを説明する情報を含むアップロード可能なパッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="b8e0e-111">パッケージ (.zip ファイル) には、エクスペリエンスを一意に定義するアプリケーション マニフェストとアイコンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="b8e0e-112">アップロード パッケージを作成するには、[「Microsoft Teams アプリのパッケージを作成する」](../build-and-test/apps-package.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="b8e0e-113">パッケージを作成したら、チームにアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="b8e0e-114">アップロードすると、選択したチーム内のすべてのユーザーと、そのチームのユーザーのみが使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="b8e0e-115">パッケージを Teams に読み込む</span><span class="sxs-lookup"><span data-stu-id="b8e0e-115">Load your package into Teams</span></span>

<span data-ttu-id="b8e0e-116">パッケージを Teams にアップロードしてテストすることができます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="b8e0e-117">アップロードを機能させるには、テナント管理者が最初に[アプリのアップロードを有効にする](/microsoftteams/admin-settings)必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="b8e0e-118">アプリを Teams にアップロードするには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="b8e0e-119">ストアを使用する</span><span class="sxs-lookup"><span data-stu-id="b8e0e-119">Using the Store</span></span>
* <span data-ttu-id="b8e0e-120">[アプリ] タブを使用する</span><span class="sxs-lookup"><span data-stu-id="b8e0e-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="b8e0e-121">ストアを使用してチームまたは会話にパッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="b8e0e-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="b8e0e-122">Teams の左下にある [ストア] アイコンを選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="b8e0e-123">[ストア] ページで、[カスタム アプリのアップロード] を選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-123">On the Store page, choose "Upload a custom app".</span></span>

  ![チームを表示する](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="b8e0e-125">*[開く]* ダイアログで、アップロードするパッケージに移動し、*[開く]* を選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

   ![追加メニュー](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="b8e0e-127">アップロードしたパッケージは、[同意] ダイアログで指定されたチームまたは会話で使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-127">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="b8e0e-128">アプリが表示されない場合、最も一般的な理由は、マニフェスト、特にアプリ、ボット、メッセージング拡張機能の ID のエラーです。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-128">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="b8e0e-129">アプリに会話の範囲が設定されていない場合、このオプションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-129">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="b8e0e-130">現在、会話中のアプリは、[開発者プレビュー](../../resources/dev-preview/developer-preview-intro.md)に含まれていますが、Teams がこのモードで動作していない場合、このオプションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-130">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![アップロードされたボットのリストにあるボットの例](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="b8e0e-132">[アプリ] タブを使用してパッケージをチームにアップロードする</span><span class="sxs-lookup"><span data-stu-id="b8e0e-132">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="b8e0e-133">ターゲット チームで、*[その他のオプション]* (**&#8943;**) を選び、*[チームの管理]* を選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-133">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b8e0e-134">チームの所有者でなければなりません。または、所有者がこの機能を表示するために適切なアプリの種類をユーザーが追加できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-134">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="b8e0e-135">[アプリ] タブを選択し、右下の *[カスタムアプリのアップロード]* を選択します。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-135">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![アップロード エントリ ポイント](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="b8e0e-137">コンピューターから .zip パッケージを参照して選択します。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-137">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="b8e0e-138">しばらくすると、アップロードしたアプリがリストに表示されます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-138">After a brief pause you will see your uploaded app in the list.</span></span>

   ![アップロードされたボットのリストにあるボットの例](../../assets/images/botinlist.jpg)

<span data-ttu-id="b8e0e-140">アプリが読み込まれない場合、最も一般的な理由は、マニフェスト、特にアプリ、ボット、メッセージング拡張機能の ID のエラーです。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-140">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="b8e0e-141">アップロードした構成可能なタブにアクセスする</span><span class="sxs-lookup"><span data-stu-id="b8e0e-141">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="b8e0e-142">アプリにタブが含まれている場合、標準タブ ギャラリー フローを使用して、任意の会話またはチーム チャネルにユーザーをピン留めすることができます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-142">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="b8e0e-143">チーム内のチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-143">Go to a channel in the team.</span></span> <span data-ttu-id="b8e0e-144">既存のタブの右側にある *+* (*タブの追加*) を選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-144">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="b8e0e-145">表示されるギャラリーからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-145">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="b8e0e-146">同意プロンプトを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-146">Accept the consent prompt.</span></span>

4. <span data-ttu-id="b8e0e-147">[構成ページ](../../tabs/how-to/create-tab-pages/configuration-page.md)を介してタブを構成し、*[保存]* を選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-147">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  ![使用可能なタブのギャラリーが表示された [タブの追加] ダイアログ ボックス](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="b8e0e-149">アップロードしたボットにアクセスする</span><span class="sxs-lookup"><span data-stu-id="b8e0e-149">Accessing your uploaded bot</span></span>

<span data-ttu-id="b8e0e-150">ボットをチームに追加すると、ボットの範囲の定義に応じて、チームのチャネルの内外にあるチームのすべてのユーザーが使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-150">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="b8e0e-151">[全般] チャネルに、ボットがチームに追加されたことを示す投稿が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-151">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="b8e0e-152">Teams 対応のボットの場合、オートコンプリートする必要があるボットの名前を @ メンションすることで、ボットを呼び出すことから始めることができます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-152">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="b8e0e-153">ボットとの直接チャットをテストするには、アプリのホームからアクセスするか、チャネルで @ メンションするか、**[新しいチャネル]** ウィンドウで検索します。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-153">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="b8e0e-154">ボットを会話に追加するとき: ボットとの直接チャットをテストするには、会話で @ メンションするか、**[新しいチャット]** ウィンドウで検索します。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-154">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="b8e0e-155">アップロードしたコネクタにアクセスする</span><span class="sxs-lookup"><span data-stu-id="b8e0e-155">Accessing your uploaded Connector</span></span>

<span data-ttu-id="b8e0e-156">アプリがチームや会話に読み込まれると、ユーザーは標準コネクタ ギャラリー フローを使用してコネクタを設定できます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-156">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="b8e0e-157">チーム内のチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-157">Go to a channel in the team.</span></span> <span data-ttu-id="b8e0e-158">*[その他のオプション]* (*&#8943;*) を選び、*[コネクタ]* を選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-158">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="b8e0e-159">一番下にある **[サイドロード]** セクションから [コネクタ] を選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-159">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="b8e0e-160">[構成ページ](../../webhooks-and-connectors/how-to/connectors-creating.md)を介してコネクタを構成し、*[保存]* を選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-160">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  ![使用可能なタブのギャラリーが表示された [タブの追加] ダイアログ ボックス。](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="b8e0e-162">アップロードしたメッセージング拡張機能にアクセスする</span><span class="sxs-lookup"><span data-stu-id="b8e0e-162">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="b8e0e-163">メッセージング拡張機能を使用してアップロードされたアプリが自動的に [作成] ボックスの *[その他のオプション]* (*&#8943;*) メニューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-163">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![メッセージング拡張機能](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="b8e0e-165">アプリを削除または更新する</span><span class="sxs-lookup"><span data-stu-id="b8e0e-165">Removing or updating your app</span></span>

<span data-ttu-id="b8e0e-166">アプリを削除する場合は、[Teams ボットの表示] リストで、アプリ名の横にあるごみ箱アイコンを選びます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-166">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="b8e0e-167">マニフェスト情報を変更する場合は、まず、アプリを削除してから、更新されたパッケージを追加する必要があります ([パッケージをチームに読み込む](#load-your-package-into-teams)ごとに)。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-167">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="b8e0e-168">一般に、サービスに関するコード変更では、マニフェストの更新が必要な場合を除き (たとえば、URL の変更やボットの Microsoft アプリ ID の変更など)、マニフェストの再アップロードは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-168">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="b8e0e-169">ボットを個人コンテキストから完全に削除する方法はありません。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-169">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="b8e0e-170">ボットが削除されて再度追加された場合、ボットとの追加の通信が前の会話に追加されます。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-170">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="b8e0e-171">トラブルシューティングに関する注意</span><span class="sxs-lookup"><span data-stu-id="b8e0e-171">Troubleshooting notes</span></span>

* <span data-ttu-id="b8e0e-172">マニフェストが読み込まれない場合は、[「パッケージの作成」](../../concepts/build-and-test/apps-package.md)のすべての手順に従い、[スキーマ](../../resources/schema/manifest-schema.md)に対してマニフェストを検証したことを再確認してください。</span><span class="sxs-lookup"><span data-stu-id="b8e0e-172">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
