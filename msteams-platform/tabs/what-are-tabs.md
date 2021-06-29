---
title: Microsoft Teams のタブ
author: surbhigupta
description: Teams プラットフォームでのカスタム タブの概要
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bde45728a957bee3aa06752328943fe13d1fa3fe
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179923"
---
# <a name="microsoft-teams-tabs"></a><span data-ttu-id="b597f-103">Microsoft Teams のタブ</span><span class="sxs-lookup"><span data-stu-id="b597f-103">Microsoft Teams tabs</span></span>

<span data-ttu-id="b597f-104">タブとは、Microsoft Teams に組み込まれている Teams 対応 Web ページです。</span><span class="sxs-lookup"><span data-stu-id="b597f-104">Tabs are Teams-aware webpages embedded in Microsoft Teams.</span></span> <span data-ttu-id="b597f-105">これらは簡単な HTML <iFrame \> タブで、アプリ マニフェストで宣言されたドメインを指していて、チーム内のチャネル、グループ チャット、または個々のユーザー用の個人用アプリとして追加できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-105">They are simple HTML <iframe\> tags that point to domains declared in the app manifest and can be added as part of a channel inside a team, group chat, or personal app for an individual user.</span></span> <span data-ttu-id="b597f-106">アプリにカスタム タブを含めて独自の Web コンテンツを Teams に埋め込んだり、Teams 固有の機能を Web コンテンツに追加したりできます。</span><span class="sxs-lookup"><span data-stu-id="b597f-106">You can include custom tabs with your app to embed your own web content in Teams or add Teams-specific functionality to your web content.</span></span> <span data-ttu-id="b597f-107">詳細については[、「JavaScript クライアント SDK Teamsを参照してください](/javascript/api/overview/msteams-client)。</span><span class="sxs-lookup"><span data-stu-id="b597f-107">For more information, see [Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

<span data-ttu-id="b597f-108">次の図は、個人用タブを示しています。</span><span class="sxs-lookup"><span data-stu-id="b597f-108">The following image shows personal tabs:</span></span>

![[個人] タブ](../assets/images/tabs/personaltab.png)

<span data-ttu-id="b597f-110">次の図は、Contoso チャネル タブを示しています。</span><span class="sxs-lookup"><span data-stu-id="b597f-110">The following image shows Contoso channel tabs:</span></span>

![チャネルまたはグループのタブ](../assets/images/tabs/tabs.png)

> [!VIDEO https://www.youtube-nocookie.com/embed/Jw6i7Mkt0dg]


> [!VIDEO https://www.youtube-nocookie.com/embed/T2a8yJC3VcQ]

<span data-ttu-id="b597f-112">タブを操作する前に実行する必要がある前提条件は少なからずある。</span><span class="sxs-lookup"><span data-stu-id="b597f-112">There are few prerequisites that you must go through before working on tabs.</span></span>

<span data-ttu-id="b597f-113">個人用タブとチャネルタブ、またはグループタブには、Teams 2 種類があります。</span><span class="sxs-lookup"><span data-stu-id="b597f-113">There are two types of tabs available in Teams, personal and channel or group.</span></span> <span data-ttu-id="b597f-114">[個人用タブ](~/tabs/how-to/create-personal-tab.md)は、個人スコープのボットと共に個人用アプリの一部であり、1 人のユーザーを対象とします。</span><span class="sxs-lookup"><span data-stu-id="b597f-114">[Personal tabs](~/tabs/how-to/create-personal-tab.md), along with personally-scoped bots, are part of personal apps and are scoped to a single user.</span></span> <span data-ttu-id="b597f-115">簡単にアクセスできるように、左側のナビゲーション バーにピン留めすることができます。</span><span class="sxs-lookup"><span data-stu-id="b597f-115">They can be pinned to the left navigation bar for easy access.</span></span> <span data-ttu-id="b597f-116">[チャネルタブまたはグループ タブは](~/tabs/how-to/create-channel-group-tab.md) 、チャネルやグループ チャットにコンテンツを配信し、専用の Web ベースのコンテンツを中心に共同作業スペースを作成する優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="b597f-116">[Channel or group tabs](~/tabs/how-to/create-channel-group-tab.md) deliver content to channels and group chats, and are a great way to create collaborative spaces around dedicated web-based content.</span></span>

<span data-ttu-id="b597f-117">個人用タブ [、チャネル](~/tabs/how-to/create-tab-pages/content-page.md) またはグループ タブ、またはタスク モジュールの一部としてコンテンツ ページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-117">You can [create a content page](~/tabs/how-to/create-tab-pages/content-page.md) as part of a personal tab, channel or group tab, or task module.</span></span> <span data-ttu-id="b597f-118">Microsoft Teams[](~/tabs/how-to/create-tab-pages/configuration-page.md)アプリを構成し、チャネルまたはグループ チャット タブ、メッセージング拡張機能、または Office 365 Connector を構成する構成ページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-118">You can [create a configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) that enables users to configure Microsoft Teams app and use it to configure a channel or group chat tab, a messaging extension, or an Office 365 Connector.</span></span> <span data-ttu-id="b597f-119">ユーザーがインストール後にタブを再構成し、アプリケーション [のタブ削除ページ](~/tabs/how-to/create-tab-pages/removal-page.md) を作成できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-119">You can permit users to reconfigure your tab after installation and [create a tab removal page](~/tabs/how-to/create-tab-pages/removal-page.md) for your application.</span></span> <span data-ttu-id="b597f-120">タブを含むTeamsアプリをビルドする場合は、Android クライアントと[iOS](~/tabs/design/tabs-mobile.md)クライアントの両方でタブがどのように機能Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="b597f-120">When you build a Teams app that includes a tab, you must test how your [tab functions on both the Android and iOS Teams clients](~/tabs/design/tabs-mobile.md).</span></span> <span data-ttu-id="b597f-121">タブは、 [基本情報、](~/tabs/how-to/access-teams-context.md) ロケール、テーマ情報を使用してコンテキストを取得する必要があります。また、タブ内の情報 `entityId` `subEntityId` を識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b597f-121">Your tab must [get context](~/tabs/how-to/access-teams-context.md) through basic information, locale and theme information, and `entityId` or `subEntityId` that identifies what is in the tab.</span></span>

<span data-ttu-id="b597f-122">アダプティブ カードを使用してタブを構築し、ボットTeams別のバックエンドを不要にすることで、すべてのアプリ機能を一元化できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-122">You can build tabs with Adaptive Cards and centralize all Teams app capabilities by eliminating the need for a different backend for your bots and tabs.</span></span> <span data-ttu-id="b597f-123">[ステージ ビュー](~/tabs/tabs-link-unfurling.md)は、新しい UI コンポーネントで、画面全体で開いたコンテンツをTeamsタブとしてピン留めできます。既存の[リンク解除](~/tabs/tabs-link-unfurling.md)サービスが更新され、アダプティブ カードとチャット サービスを使用して URL をタブに変換するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b597f-123">[Stage View](~/tabs/tabs-link-unfurling.md) is a new UI component that allows you to render the content opened in full screen in Teams and pinned as a tab. The existing [link unfurling](~/tabs/tabs-link-unfurling.md) service is updated so that it is used to turn URLs into a tab using an Adaptive Card and Chat Services.</span></span> <span data-ttu-id="b597f-124">会話型[](~/tabs/how-to/conversational-tabs.md)のサブエンティティを使用して会話タブを作成できます。ユーザーは、タブ全体を議論する代わりに、特定のタスク、患者、販売機会などのサブエンティティに関する会話をタブで行えます。タブ余白を[変更して、](~/resources/removing-tab-margins.md)アプリを構築する際の開発者のエクスペリエンスを向上できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-124">You can [create conversational tabs](~/tabs/how-to/conversational-tabs.md) using conversational sub-entities that allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab. You can make changes to [tab margins](~/resources/removing-tab-margins.md) to enhance the developer's experience when building apps.</span></span>

## <a name="tab-features"></a><span data-ttu-id="b597f-125">タブ機能</span><span class="sxs-lookup"><span data-stu-id="b597f-125">Tab features</span></span>

<span data-ttu-id="b597f-126">タブ機能は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b597f-126">The tab features are as follows:</span></span>

* <span data-ttu-id="b597f-127">ボットも含むアプリにタブを追加すると、ボットもチームに追加されます。</span><span class="sxs-lookup"><span data-stu-id="b597f-127">If a tab is added to an app that also has a bot, the bot is also added to the team.</span></span>
* <span data-ttu-id="b597f-128">現在のAzure Active Directory (AAD) ID の認識。</span><span class="sxs-lookup"><span data-stu-id="b597f-128">Awareness of Azure Active Directory (AAD) ID of the current user.</span></span>
* <span data-ttu-id="b597f-129">ユーザーが言語を示すロケール認識 `en-us` 。</span><span class="sxs-lookup"><span data-stu-id="b597f-129">Locale awareness for the user to indicate language that is `en-us`.</span></span>
* <span data-ttu-id="b597f-130">サポートされている場合、シングル サインオン (SSO) 機能があります。</span><span class="sxs-lookup"><span data-stu-id="b597f-130">Single sign-on (SSO) capability, if supported.</span></span>
* <span data-ttu-id="b597f-131">ボットまたはアプリ通知を使用して、タブまたはサービス内のサブエンティティ (個々の作業項目など) へのディープ リンクを使用できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-131">Ability to use bots or app notifications to deep link to the tab or to a sub-entity within the service, for example an individual work item.</span></span>
* <span data-ttu-id="b597f-132">タブ内のリンクからタスク モジュールを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="b597f-132">The ability to open a task module from links within a tab.</span></span>
* <span data-ttu-id="b597f-133">タブ内で SharePoint Web パーツを再利用できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-133">Reuse of SharePoint web parts within the tab.</span></span>

## <a name="tabs-user-scenarios"></a><span data-ttu-id="b597f-134">タブのユーザー シナリオ</span><span class="sxs-lookup"><span data-stu-id="b597f-134">Tabs user scenarios</span></span>

<span data-ttu-id="b597f-135">**シナリオ:** Teams 内に既存の Web ベース リソースを取得します。</span><span class="sxs-lookup"><span data-stu-id="b597f-135">**Scenario:** Bring an existing web-based resource inside Teams.</span></span> \
<span data-ttu-id="b597f-136">**例:** 情報提供企業の Web サイトをユーザーに提供する Teams アプリに [個人] タブを作成します。</span><span class="sxs-lookup"><span data-stu-id="b597f-136">**Example:** You create a personal tab in your Teams app that presents an informational corporate website to users.</span></span>

<span data-ttu-id="b597f-137">**シナリオ:** Teams ボットまたはメッセージング拡張機能にサポート ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="b597f-137">**Scenario:** Add support pages to a Teams bot or messaging extension.</span></span> \
<span data-ttu-id="b597f-138">**例:** 作成する個人タブは **について** と **ヘルプの** を、Web ページ コンテンツをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="b597f-138">**Example:** You create personal tabs that provide **about** and **help** webpage content to users.</span></span>

<span data-ttu-id="b597f-139">**シナリオ:** 協力対話と共同作業のためにユーザーが定期的にやり取りするアイテムへのアクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="b597f-139">**Scenario:** Provide access to items that your users interact with regularly for cooperative dialogue and collaboration.</span></span> \
<span data-ttu-id="b597f-140">**例:** チャネルまたはグループ タブを作成し、個々のアイテムに深くリンクします。</span><span class="sxs-lookup"><span data-stu-id="b597f-140">**Example:** You create a channel or group tab with deep linking to individual items.</span></span>

## <a name="understand-how-tabs-work"></a><span data-ttu-id="b597f-141">タブの動作を理解する</span><span class="sxs-lookup"><span data-stu-id="b597f-141">Understand how tabs work</span></span>

<span data-ttu-id="b597f-142">次のいずれかの方法を使用して、タブを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-142">You can use one of the following methods to create tabs:</span></span>

* [<span data-ttu-id="b597f-143">アプリ マニフェストでカスタム タブを宣言する</span><span class="sxs-lookup"><span data-stu-id="b597f-143">Declare custom tab in app manifest</span></span>](#declare-custom-tab-in-app-manifest)
* [<span data-ttu-id="b597f-144">アダプティブ カードを使用してタブを作成する</span><span class="sxs-lookup"><span data-stu-id="b597f-144">Use Adaptive Card to build tabs</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)

### <a name="declare-custom-tab-in-app-manifest"></a><span data-ttu-id="b597f-145">アプリ マニフェストでカスタム タブを宣言する</span><span class="sxs-lookup"><span data-stu-id="b597f-145">Declare custom tab in app manifest</span></span>

<span data-ttu-id="b597f-146">カスタム タブは、アプリ パッケージのアプリ マニフェストで宣言されます。</span><span class="sxs-lookup"><span data-stu-id="b597f-146">A custom tab is declared in the app manifest of your app package.</span></span> <span data-ttu-id="b597f-147">アプリのタブとして含める Web ページごとに、URL と範囲を定義します。</span><span class="sxs-lookup"><span data-stu-id="b597f-147">For each webpage you want included as a tab in your app, you define a URL and a scope.</span></span> <span data-ttu-id="b597f-148">さらに、JavaScript クライアント[SDK](/javascript/api/overview/msteams-client) Teamsページに追加し、ページの読み込み後 `microsoftTeams.initialize()` に呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b597f-148">Additionally, you can add the [Teams JavaScript client SDK](/javascript/api/overview/msteams-client) to your page, and call `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="b597f-149">Teamsページを表示し、Teams特定の情報 (たとえば、クライアントが暗いテーマを実行Teamsなど) へのアクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="b597f-149">Teams displays your page and provides access to Teams-specific information, for example the Teams client is running the dark theme.</span></span>

<span data-ttu-id="b597f-150">チャネルまたはグループ内、または個人用スコープ内でタブを公開する場合は、タブに iframe HTML コンテンツ ページ<表示する \> 必要があります。 [](~/tabs/how-to/create-tab-pages/content-page.md)個人用タブの場合、コンテンツ URL は、配列内Teamsによってアプリ マニフェスト `contentUrl` に直接設定 `staticTabs` されます。</span><span class="sxs-lookup"><span data-stu-id="b597f-150">Whether you choose to expose your tab within the channel or group, or personal scope, you must present an <iframe\> HTML [content page](~/tabs/how-to/create-tab-pages/content-page.md) in your tab. For personal tabs, the content URL is set directly in your Teams app manifest by the `contentUrl` property in the `staticTabs` array.</span></span> <span data-ttu-id="b597f-151">タブのコンテンツは、すべてのユーザーで同じです。</span><span class="sxs-lookup"><span data-stu-id="b597f-151">Your tab's content is the same for all users.</span></span>

<span data-ttu-id="b597f-152">チャネルタブまたはグループ タブの場合は、追加の構成ページを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="b597f-152">For channel or group tabs, you can also create an additional configuration page.</span></span> <span data-ttu-id="b597f-153">このページでは、通常、URL クエリ文字列パラメーターを使用して、そのコンテキストに適したコンテンツを読み込むコンテンツ ページ URL を構成できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-153">This page allows you to configure content page URL, typically by using URL query string parameters to load the appropriate content for that context.</span></span> <span data-ttu-id="b597f-154">これは、チャネルまたはグループ タブを複数のチームまたはグループ チャットに追加できるためです。</span><span class="sxs-lookup"><span data-stu-id="b597f-154">This is because your channel or group tab can be added to multiple teams or group chats.</span></span> <span data-ttu-id="b597f-155">以降のインストールごとに、ユーザーはタブを構成でき、必要に応じてエクスペリエンスを調整できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-155">On each subsequent install, your users can configure the tab, allowing you to tailor the experience as required.</span></span> <span data-ttu-id="b597f-156">ユーザーがタブを追加または構成すると、URL は、ユーザー インターフェイス (UI) に表示されるタブTeams関連付けます。</span><span class="sxs-lookup"><span data-stu-id="b597f-156">When users add or configure a tab, a URL is associated with the tab that is presented in the Teams user interface (UI).</span></span> <span data-ttu-id="b597f-157">タブを構成すると、その URL に追加のパラメーターが追加されます。</span><span class="sxs-lookup"><span data-stu-id="b597f-157">Configuring a tab simply adds additional parameters to that URL.</span></span> <span data-ttu-id="b597f-158">たとえば、[ページ] タブをAzure Boardsすると、構成ページでタブが読み込まれるボードを選択できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-158">For example, when you add the Azure Boards tab, the configuration page allows you to choose, which board the tab loads.</span></span> <span data-ttu-id="b597f-159">構成ページの URL は、アプリ マニフェストの `configurableTabs` 配列の `configurationUrl` プロパティで指定します。</span><span class="sxs-lookup"><span data-stu-id="b597f-159">The configuration page URL is specified by the  `configurationUrl` property in the `configurableTabs` array in your app manifest.</span></span>

<span data-ttu-id="b597f-160">複数のチャネルまたはグループ タブ、およびアプリごとに最大 16 の個人用タブを使用できます。</span><span class="sxs-lookup"><span data-stu-id="b597f-160">You can have multiple channels or group tabs, and up to 16 personal tabs per app.</span></span>

## <a name="see-also"></a><span data-ttu-id="b597f-161">関連項目</span><span class="sxs-lookup"><span data-stu-id="b597f-161">See also</span></span>

* [<span data-ttu-id="b597f-162">デバイスのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="b597f-162">Request device permissions</span></span>](../concepts/device-capabilities/native-device-permissions.md)
* [<span data-ttu-id="b597f-163">メディア機能を統合する</span><span class="sxs-lookup"><span data-stu-id="b597f-163">Integrate media capabilities</span></span>](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [<span data-ttu-id="b597f-164">QR またはバーコード スキャナーを統合する</span><span class="sxs-lookup"><span data-stu-id="b597f-164">Integrate a QR or barcode scanner</span></span>](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [<span data-ttu-id="b597f-165">場所機能を統合する</span><span class="sxs-lookup"><span data-stu-id="b597f-165">Integrate location capabilities</span></span>](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a><span data-ttu-id="b597f-166">次の手順</span><span class="sxs-lookup"><span data-stu-id="b597f-166">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b597f-167">前提条件</span><span class="sxs-lookup"><span data-stu-id="b597f-167">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
