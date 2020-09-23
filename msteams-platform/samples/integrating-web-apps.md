---
author: heath-hamilton
description: 既存の web アプリケーションを Microsoft Teams と統合するためのベストプラクティス
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: Web アプリを Microsoft Teams と統合する
ms.openlocfilehash: e7d4f74526f7a71fe33d5a70d9ed60be960adefc
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210273"
---
# <a name="integrate-web-apps-with-teams"></a><span data-ttu-id="75c2a-103">Web アプリを Teams と統合する</span><span class="sxs-lookup"><span data-stu-id="75c2a-103">Integrate web apps with Teams</span></span>

<span data-ttu-id="75c2a-104">Teams のソーシャル機能とコラボレーション機能によく当てはまる web アプリがありますか。</span><span class="sxs-lookup"><span data-stu-id="75c2a-104">Do you have a web app you think would fit naturally with Teams' social and collaborative features?</span></span> <span data-ttu-id="75c2a-105">これらのガイドラインは、次の種類のアプリを統合する方法を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-105">These guidelines can help you understand how to integrate the following types of apps:</span></span>

* <span data-ttu-id="75c2a-106">**スタンドアロンアプリ**: Teams では、1ページのアプリまたは大規模で複雑なアプリのいずれかを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-106">**Standalone apps**: Could be a single-page app or large, complex app you want people to use some aspects of in Teams.</span></span>
* <span data-ttu-id="75c2a-107">**コラボレーションアプリ**: Teams に固有のソーシャル機能とコラボレーション機能のために既に構築されているアプリ。</span><span class="sxs-lookup"><span data-stu-id="75c2a-107">**Collaboration apps**: An app already built for the social and collaborative features inherent to Teams.</span></span>
* <span data-ttu-id="75c2a-108">**Sharepoint**: Teams に表示する sharepoint ページ。</span><span class="sxs-lookup"><span data-stu-id="75c2a-108">**SharePoint**: A SharePoint page you want to surface in Teams.</span></span>

<span data-ttu-id="75c2a-109">各ガイドラインについて、統合シナリオに該当するかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-109">For each guideline, you can see if it's applicable to your integration scenario.</span></span>

## <a name="get-to-know-teams-platform-capabilities"></a><span data-ttu-id="75c2a-110">Teams プラットフォームの機能を理解する</span><span class="sxs-lookup"><span data-stu-id="75c2a-110">Get to know Teams platform capabilities</span></span>

<span data-ttu-id="75c2a-111">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="75c2a-111">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="75c2a-112">Teams アプリには、共同作業の際にユーザーが必要とする機能を含めることができますが、Teams 開発の用語についてはよくありません。</span><span class="sxs-lookup"><span data-stu-id="75c2a-112">Your Teams app can include features users want and might expect when collaborating, but you may be unfamiliar with Teams development terminology.</span></span>

|<span data-ttu-id="75c2a-113">一般的なアプリの機能</span><span class="sxs-lookup"><span data-stu-id="75c2a-113">Common app features</span></span>   |<span data-ttu-id="75c2a-114">Teams プラットフォームの機能</span><span class="sxs-lookup"><span data-stu-id="75c2a-114">Teams platform capabilities</span></span>   |
|----------|-----------|
|<span data-ttu-id="75c2a-115">埋め込まれた web ページ、ホームページ、または webview</span><span class="sxs-lookup"><span data-stu-id="75c2a-115">Embedded webpage, homepage, or webview</span></span>  |[<span data-ttu-id="75c2a-116">タブ</span><span class="sxs-lookup"><span data-stu-id="75c2a-116">Tabs</span></span>](../tabs/what-are-tabs.md)  |
|<span data-ttu-id="75c2a-117">共有のショートカットと拡張機能</span><span class="sxs-lookup"><span data-stu-id="75c2a-117">Share shortcuts and extensions</span></span>  |[<span data-ttu-id="75c2a-118">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="75c2a-118">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="75c2a-119">アクションのショートカットと拡張機能</span><span class="sxs-lookup"><span data-stu-id="75c2a-119">Action shortcuts and extensions</span></span>  |[<span data-ttu-id="75c2a-120">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="75c2a-120">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="75c2a-121">Chatbots</span><span class="sxs-lookup"><span data-stu-id="75c2a-121">Chatbots</span></span>  |[<span data-ttu-id="75c2a-122">ボット</span><span class="sxs-lookup"><span data-stu-id="75c2a-122">Bots</span></span>](../bots/what-are-bots.md) |
|<span data-ttu-id="75c2a-123">チャネル通知</span><span class="sxs-lookup"><span data-stu-id="75c2a-123">Channel notifications</span></span>  |[<span data-ttu-id="75c2a-124">ボット</span><span class="sxs-lookup"><span data-stu-id="75c2a-124">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="75c2a-125">受信 Webhook</span><span class="sxs-lookup"><span data-stu-id="75c2a-125">Incoming webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[<span data-ttu-id="75c2a-126">Office 365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="75c2a-126">Office 365 Connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="75c2a-127">メッセージ外部サービス</span><span class="sxs-lookup"><span data-stu-id="75c2a-127">Message external services</span></span>  |[<span data-ttu-id="75c2a-128">ボット</span><span class="sxs-lookup"><span data-stu-id="75c2a-128">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="75c2a-129">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="75c2a-129">Outgoing webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="75c2a-130">Modals</span><span class="sxs-lookup"><span data-stu-id="75c2a-130">Modals</span></span>  |[<span data-ttu-id="75c2a-131">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="75c2a-131">Task modules</span></span>](../task-modules-and-cards/what-are-task-modules.md)  |
|<span data-ttu-id="75c2a-132">コンテンツの豊富なカード</span><span class="sxs-lookup"><span data-stu-id="75c2a-132">Content-rich cards</span></span>  |[<span data-ttu-id="75c2a-133">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="75c2a-133">Adaptive Cards</span></span>](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a><span data-ttu-id="75c2a-134">機能のサブセットを決定する</span><span class="sxs-lookup"><span data-stu-id="75c2a-134">Determine a subset of functionality</span></span>

<span data-ttu-id="75c2a-135">\***統合シナリオ**: スタンドアロンアプリ \*</span><span class="sxs-lookup"><span data-stu-id="75c2a-135">\***Integration scenarios**: Standalone apps\*</span></span>

<span data-ttu-id="75c2a-136">既存のアプリケーションのすべての機能を Teams に統合することにより、多くの場合、特に大規模なアプリでは、強制または不自然なユーザー環境が発生します。</span><span class="sxs-lookup"><span data-stu-id="75c2a-136">Integrating all features of an existing application into Teams often leads to a forced or unnatural user experience, particularly in larger apps.</span></span> <span data-ttu-id="75c2a-137">インパクトのほとんどの機能から始めて、Teams でより自然に統合するものを検討してください。</span><span class="sxs-lookup"><span data-stu-id="75c2a-137">Consider starting with the most impactful features and those that will integrate more naturally with Teams.</span></span> <span data-ttu-id="75c2a-138">常に、ユーザーがメインアプリを起動して、機能の完全なセットにアクセスできるようにすることを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="75c2a-138">Remember, you can always allow users to launch the main app and access its full set of features.</span></span>

<span data-ttu-id="75c2a-139">技術的な作業を開始する前に、Teams アプリの計画を行います。</span><span class="sxs-lookup"><span data-stu-id="75c2a-139">Before you begin any technical work, do some planning for your Teams app:</span></span>

1. <span data-ttu-id="75c2a-140">[アプリのユースケースを Teams プラットフォームの機能にマップ](../concepts/design/map-use-cases.md)します。</span><span class="sxs-lookup"><span data-stu-id="75c2a-140">[Map your app's use cases to Teams platform capabilities](../concepts/design/map-use-cases.md).</span></span>
1. <span data-ttu-id="75c2a-141">[アプリのエントリポイントを決定](../concepts/extensibility-points.md)します。</span><span class="sxs-lookup"><span data-stu-id="75c2a-141">[Determine your app's entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="75c2a-142">個人利用、グループ作業、またはその両方を対象としていますか?</span><span class="sxs-lookup"><span data-stu-id="75c2a-142">Is it for personal use, collaboration, or both?</span></span>

## <a name="understand-sharepoint-requirements-and-options"></a><span data-ttu-id="75c2a-143">SharePoint の要件とオプションについて</span><span class="sxs-lookup"><span data-stu-id="75c2a-143">Understand SharePoint requirements and options</span></span>

<span data-ttu-id="75c2a-144">\***統合シナリオ**: SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="75c2a-144">\***Integration scenarios**: SharePoint\*</span></span>

<span data-ttu-id="75c2a-145">既存の [SharePoint ページ](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) を Teams タブとして統合することができます。次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="75c2a-145">You can integrate an existing [SharePoint page](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) as a Teams tab. Remember the following:</span></span>

* <span data-ttu-id="75c2a-146">SharePoint Online の *モダン* ページである必要があります。</span><span class="sxs-lookup"><span data-stu-id="75c2a-146">It must be a *modern* SharePoint Online page</span></span>
* <span data-ttu-id="75c2a-147">個人用タブのみがサポートされています (ページを [チャネル] タブとして統合することはできません)</span><span class="sxs-lookup"><span data-stu-id="75c2a-147">Only personal tabs are supported (you can't integrate your page as a channel tab)</span></span>

<span data-ttu-id="75c2a-148">または、 [SharePoint Framework を使用して](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)Teams タブを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-148">Alternatively, you can build a Teams tab [using the SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).</span></span>

## <a name="aim-towards-multi-tenancy"></a><span data-ttu-id="75c2a-149">マルチテナントを目指す</span><span class="sxs-lookup"><span data-stu-id="75c2a-149">Aim towards multi-tenancy</span></span>

<span data-ttu-id="75c2a-150">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="75c2a-150">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="75c2a-151">アプリが複数の組織で使用されている場合は、製品をスケーラブルで、配布を大幅に簡素化するマルチテナントのホスティングを検討してください。</span><span class="sxs-lookup"><span data-stu-id="75c2a-151">If your app is used by multiple organizations, consider multi-tenant hosting that would make your product scalable and greatly simplify distribution.</span></span>

## <a name="review-your-apis"></a><span data-ttu-id="75c2a-152">Api を確認する</span><span class="sxs-lookup"><span data-stu-id="75c2a-152">Review your APIs</span></span>

<span data-ttu-id="75c2a-153">\***統合シナリオ**: スタンドアロンアプリ、グループ作業アプリ \*</span><span class="sxs-lookup"><span data-stu-id="75c2a-153">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="75c2a-154">Teams と統合する場合、アプリの既存の Api とデータ構造がアプリを完全にサポートしないことを前提としていません。</span><span class="sxs-lookup"><span data-stu-id="75c2a-154">Don't assume your app's existing APIs and data structures fully support the app when integrated with Teams.</span></span> <span data-ttu-id="75c2a-155">[Id マッピング](../concepts/authentication/configure-identity-provider.md)、[ディープリンクサポート](../concepts/build-and-test/deep-links.md)、 [Microsoft Graph の組み込み](https://docs.microsoft.com/graph/teams-concept-overview)に関する Teams に関するコンテキスト情報を使用して、これらを拡張する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="75c2a-155">You might need to augment these with contextual information about Teams for [identity mapping](../concepts/authentication/configure-identity-provider.md), [deep-link support](../concepts/build-and-test/deep-links.md), and [incorporating Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="75c2a-156">Teams [タブ](../tabs/how-to/access-teams-context.md) または [bot](../bots/how-to/get-teams-context.md)のコンテキスト取得の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="75c2a-156">Learn more about getting context for your Teams [tab](../tabs/how-to/access-teams-context.md) or [bot](../bots/how-to/get-teams-context.md).</span></span>

## <a name="understand-authentication-options"></a><span data-ttu-id="75c2a-157">認証オプションについて</span><span class="sxs-lookup"><span data-stu-id="75c2a-157">Understand authentication options</span></span>

<span data-ttu-id="75c2a-158">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="75c2a-158">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="75c2a-159">Azure Active Directory (AD) は Teams の id プロバイダーです。</span><span class="sxs-lookup"><span data-stu-id="75c2a-159">Azure Active Directory (AD) is the identity provider for Teams.</span></span> <span data-ttu-id="75c2a-160">アプリで異なる id プロバイダーを使用する場合は、id マッピングの実習または Azure AD とのフェデレーションのどちらかを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="75c2a-160">If your app uses a different identity provider, you must either do an identity mapping exercise or federate with Azure AD.</span></span>

<span data-ttu-id="75c2a-161">Teams には、サードパーティ製アプリ用の Azure AD のシングルサインオン (SSO) メカニズムと、OAuth や Open ID Connect (OIDC) などの標準を使用する他の id プロバイダーへの認証フローに関するガイダンスがあります。</span><span class="sxs-lookup"><span data-stu-id="75c2a-161">Teams has single sign-on (SSO) mechanisms with Azure AD for third-party apps and guidance for authentication flows to other identity providers using standards such as OAuth and Open ID Connect (OIDC).</span></span>

<span data-ttu-id="75c2a-162">SharePoint ページの場合、sso のみを使用でき、別のアプリ (ID は SharePoint アプリ) に SSO を使用する場合は、別の Azure AD ID を追加することはできません。</span><span class="sxs-lookup"><span data-stu-id="75c2a-162">For SharePoint pages, you can only use SSO and can't add another Azure AD ID if you want SSO to work for another app (since the ID is the SharePoint app).</span></span>

<span data-ttu-id="75c2a-163">[Teams での認証の](../concepts/authentication/authentication.md)詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="75c2a-163">Learn more about [authentication in Teams](../concepts/authentication/authentication.md).</span></span>

## <a name="follow-teams-design-guidelines"></a><span data-ttu-id="75c2a-164">Teams 設計ガイドラインに従う</span><span class="sxs-lookup"><span data-stu-id="75c2a-164">Follow Teams design guidelines</span></span>

<span data-ttu-id="75c2a-165">\***統合シナリオ**: スタンドアロンアプリ、グループ作業アプリ \*</span><span class="sxs-lookup"><span data-stu-id="75c2a-165">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="75c2a-166">一般に、アプリは Teams で自然に感じられます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-166">In general, your app should feel natural in Teams.</span></span> <span data-ttu-id="75c2a-167">既存のアプリコンテンツを Teams タブに移行することは十分ですが、アプリは [teams 設計ガイドライン](../concepts/design/understand-use-cases.md)に従うことを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="75c2a-167">You might think migrating existing app content to a Teams tab is sufficient, but we strongly recommend your app follows [Teams design guidelines](../concepts/design/understand-use-cases.md).</span></span> <span data-ttu-id="75c2a-168">「 [Fluent Design System](https://fluentsite.z22.web.core.windows.net/)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="75c2a-168">See also: [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).</span></span>

## <a name="maximize-deep-linking"></a><span data-ttu-id="75c2a-169">ディープリンクを最大化する</span><span class="sxs-lookup"><span data-stu-id="75c2a-169">Maximize deep linking</span></span>

<span data-ttu-id="75c2a-170">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="75c2a-170">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="75c2a-171">Teams のほぼすべてのことは、 [ディープリンク](../concepts/build-and-test/deep-links.md)を使用して直接リンクすることができます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-171">Almost everything in Teams can be linked to directly with a [deep link](../concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="75c2a-172">アプリでは、特定のメッセージとタブコンテンツとの間のリンクを含め、これらの使用を最大化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="75c2a-172">Your app should maximize use of these, including linking to and from specific messages and tab content.</span></span> <span data-ttu-id="75c2a-173">深いリンクは、多くの場合、ネイティブなチームの環境でアプリの複数の要素を結合します。</span><span class="sxs-lookup"><span data-stu-id="75c2a-173">Deep links can really tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="be-smart-when-messaging-users"></a><span data-ttu-id="75c2a-174">メッセージングユーザーにとって賢い</span><span class="sxs-lookup"><span data-stu-id="75c2a-174">Be smart when messaging users</span></span>

<span data-ttu-id="75c2a-175">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="75c2a-175">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="75c2a-176">Teams アプリが今すぐに送信する可能性があるメッセージの種類と長期間について検討します。</span><span class="sxs-lookup"><span data-stu-id="75c2a-176">Consider the types of messages your Teams app might send now and in the long term.</span></span> <span data-ttu-id="75c2a-177">アプリにマルチスレッドの会話があると考えられる場合、 [bot](../bots/what-are-bots.md) は [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)よりも高い柔軟性を提供します。</span><span class="sxs-lookup"><span data-stu-id="75c2a-177">If you think your app will ever have a multi-threaded conversation, a [bot](../bots/what-are-bots.md) might offer more flexibility than a [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

<span data-ttu-id="75c2a-178">また、ボットを使用すると、個々のユーザーやチャネルに *予防的なメッセージ* を送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-178">Bots also allow you to send *proactive messages* to individual users or channels.</span></span> <span data-ttu-id="75c2a-179">これらのメッセージは、外部イベントによってトリガーされるメッセージであり、bot に送信されるメッセージではありません。</span><span class="sxs-lookup"><span data-stu-id="75c2a-179">These are unprompted messages triggered by an outside event and not a message sent to a bot.</span></span> <span data-ttu-id="75c2a-180">(たとえば、ボットがインストールされているときに、または新しいユーザーがチャネルに参加したときに、ウェルカムメッセージを送信することができます)。</span><span class="sxs-lookup"><span data-stu-id="75c2a-180">(For example, your bot can send a welcome message when it's installed or a new user joins a channel.)</span></span> 

<span data-ttu-id="75c2a-181">予防的なメッセージを送信するには Teams 固有の識別子が必要です。この情報は、 [名簿またはユーザープロファイルデータを取得](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile)したり、 [会話イベントにサブスクライブ](../bots/how-to/conversations/subscribe-to-conversation-events.md)したり、 [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging)を使用したりすることで取得できます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-181">Sending proactive messages requires Teams-specific identifiers—you can capture this information by [fetching roster or user profile data](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile), [subscribing to conversation events](../bots/how-to/conversations/subscribe-to-conversation-events.md), or using [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).</span></span>

<span data-ttu-id="75c2a-182">過剰なメッセージがある場合は、スパムではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="75c2a-182">Be careful not to spam users with excessive messages.</span></span> <span data-ttu-id="75c2a-183">Teams 機能でサポートされている場合は、ユーザーがアプリの通知設定を構成することを検討してください (たとえば、[非表示メッセージを送信しない])。</span><span class="sxs-lookup"><span data-stu-id="75c2a-183">If the Teams capability supports it, consider letting users configure notification settings for your app (for example, "Don't send me unprompted messages.").</span></span>

## <a name="use-sharepoint-for-file-and-data-storage"></a><span data-ttu-id="75c2a-184">ファイルとデータの記憶域に SharePoint を使用する</span><span class="sxs-lookup"><span data-stu-id="75c2a-184">Use SharePoint for file and data storage</span></span>

<span data-ttu-id="75c2a-185">***統合シナリオ:** スタンドアロンアプリ、グループ作業アプリ、SharePoint ページ*</span><span class="sxs-lookup"><span data-stu-id="75c2a-185">***Integration scenarios:** Standalone apps, collaboration apps, SharePoint pages*</span></span>

<span data-ttu-id="75c2a-186">チームを作成すると、 [SharePoint サイトコレクション](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) も、そのチームのファイルとデータストレージをサポートするように準備されます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-186">When a team is created, a [SharePoint site collection](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) is also provisioned to support file and data storage for that team.</span></span> <span data-ttu-id="75c2a-187">アプリは、ファイルを操作する場合にこの機能を利用することができます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-187">Your app can and should leverage this feature if it interacts with files.</span></span> <span data-ttu-id="75c2a-188">サイトコレクションを使用して、SharePoint リストおよび Excel の生データを保存することもできます。</span><span class="sxs-lookup"><span data-stu-id="75c2a-188">You can also use the site collection to store raw data in SharePoint Lists and Excel.</span></span>
