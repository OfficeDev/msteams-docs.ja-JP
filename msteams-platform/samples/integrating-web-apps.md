---
author: heath-hamilton
description: 既存の Web アプリと Microsoft Teams を統合するためのベスト プラクティス
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: Web アプリを Microsoft Teams と統合する
ms.openlocfilehash: 4671d2277d5eb7c035421c51b1714eccaac06a31
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696487"
---
# <a name="integrate-web-apps-with-teams"></a><span data-ttu-id="ee63b-103">Web アプリを Teams と統合する</span><span class="sxs-lookup"><span data-stu-id="ee63b-103">Integrate web apps with Teams</span></span>

<span data-ttu-id="ee63b-104">Teams のソーシャル機能や共同作業機能に自然に適合すると思う Web アプリはありますか?</span><span class="sxs-lookup"><span data-stu-id="ee63b-104">Do you have a web app you think would fit naturally with Teams' social and collaborative features?</span></span> <span data-ttu-id="ee63b-105">これらのガイドラインは、次の種類のアプリを統合する方法を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ee63b-105">These guidelines can help you understand how to integrate the following types of apps:</span></span>

* <span data-ttu-id="ee63b-106">**スタンドアロン アプリ**: 単一ページ アプリまたは大規模で複雑なアプリで、Teams でユーザーがいくつかの側面を使用する場合があります。</span><span class="sxs-lookup"><span data-stu-id="ee63b-106">**Standalone apps**: Could be a single-page app or large, complex app you want people to use some aspects of in Teams.</span></span>
* <span data-ttu-id="ee63b-107">**コラボレーション アプリ**: Teams に固有のソーシャル機能と共同作業機能用に既に構築されたアプリ。</span><span class="sxs-lookup"><span data-stu-id="ee63b-107">**Collaboration apps**: An app already built for the social and collaborative features inherent to Teams.</span></span>
* <span data-ttu-id="ee63b-108">**SharePoint**: Teams で表示する SharePoint ページ。</span><span class="sxs-lookup"><span data-stu-id="ee63b-108">**SharePoint**: A SharePoint page you want to surface in Teams.</span></span>

<span data-ttu-id="ee63b-109">各ガイドラインについて、統合シナリオに該当する場合を確認できます。</span><span class="sxs-lookup"><span data-stu-id="ee63b-109">For each guideline, you can see if it's applicable to your integration scenario.</span></span>

## <a name="get-to-know-teams-platform-capabilities"></a><span data-ttu-id="ee63b-110">Teams プラットフォームの機能を知る</span><span class="sxs-lookup"><span data-stu-id="ee63b-110">Get to know Teams platform capabilities</span></span>

<span data-ttu-id="ee63b-111">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="ee63b-111">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="ee63b-112">Teams アプリには、共同作業時にユーザーが望む機能や期待できる機能を含め、Teams の開発用語に慣れていない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ee63b-112">Your Teams app can include features users want and might expect when collaborating, but you may be unfamiliar with Teams development terminology.</span></span>

|<span data-ttu-id="ee63b-113">アプリの一般的な機能</span><span class="sxs-lookup"><span data-stu-id="ee63b-113">Common app features</span></span>   |<span data-ttu-id="ee63b-114">Teams プラットフォームの機能</span><span class="sxs-lookup"><span data-stu-id="ee63b-114">Teams platform capabilities</span></span>   |
|----------|-----------|
|<span data-ttu-id="ee63b-115">埋め込み Web ページ、ホームページ、または Web ビュー</span><span class="sxs-lookup"><span data-stu-id="ee63b-115">Embedded webpage, homepage, or webview</span></span>  |[<span data-ttu-id="ee63b-116">タブ</span><span class="sxs-lookup"><span data-stu-id="ee63b-116">Tabs</span></span>](../tabs/what-are-tabs.md)  |
|<span data-ttu-id="ee63b-117">ショートカットと拡張機能を共有する</span><span class="sxs-lookup"><span data-stu-id="ee63b-117">Share shortcuts and extensions</span></span>  |[<span data-ttu-id="ee63b-118">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="ee63b-118">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="ee63b-119">操作のショートカットと拡張機能</span><span class="sxs-lookup"><span data-stu-id="ee63b-119">Action shortcuts and extensions</span></span>  |[<span data-ttu-id="ee63b-120">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="ee63b-120">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="ee63b-121">チャットボット</span><span class="sxs-lookup"><span data-stu-id="ee63b-121">Chatbots</span></span>  |[<span data-ttu-id="ee63b-122">ボット</span><span class="sxs-lookup"><span data-stu-id="ee63b-122">Bots</span></span>](../bots/what-are-bots.md) |
|<span data-ttu-id="ee63b-123">チャネル通知</span><span class="sxs-lookup"><span data-stu-id="ee63b-123">Channel notifications</span></span>  |[<span data-ttu-id="ee63b-124">ボット</span><span class="sxs-lookup"><span data-stu-id="ee63b-124">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="ee63b-125">受信 Webhook</span><span class="sxs-lookup"><span data-stu-id="ee63b-125">Incoming webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[<span data-ttu-id="ee63b-126">Office 365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="ee63b-126">Office 365 Connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="ee63b-127">メッセージ外部サービス</span><span class="sxs-lookup"><span data-stu-id="ee63b-127">Message external services</span></span>  |[<span data-ttu-id="ee63b-128">ボット</span><span class="sxs-lookup"><span data-stu-id="ee63b-128">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="ee63b-129">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="ee63b-129">Outgoing webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="ee63b-130">モーダル</span><span class="sxs-lookup"><span data-stu-id="ee63b-130">Modals</span></span>  |[<span data-ttu-id="ee63b-131">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="ee63b-131">Task modules</span></span>](../task-modules-and-cards/what-are-task-modules.md)  |
|<span data-ttu-id="ee63b-132">コンテンツが豊富なカード</span><span class="sxs-lookup"><span data-stu-id="ee63b-132">Content-rich cards</span></span>  |[<span data-ttu-id="ee63b-133">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="ee63b-133">Adaptive Cards</span></span>](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a><span data-ttu-id="ee63b-134">機能のサブセットを決定する</span><span class="sxs-lookup"><span data-stu-id="ee63b-134">Determine a subset of functionality</span></span>

<span data-ttu-id="ee63b-135">\***統合シナリオ**: スタンドアロン アプリ\*</span><span class="sxs-lookup"><span data-stu-id="ee63b-135">\***Integration scenarios**: Standalone apps\*</span></span>

<span data-ttu-id="ee63b-136">既存のアプリケーションのすべての機能を Teams に統合すると、多くの場合、特に大規模なアプリでは、強制的または不自然なユーザー エクスペリエンスが発生します。</span><span class="sxs-lookup"><span data-stu-id="ee63b-136">Integrating all features of an existing application into Teams often leads to a forced or unnatural user experience, particularly in larger apps.</span></span> <span data-ttu-id="ee63b-137">最も影響の大きな機能と、Teams とより自然に統合される機能から始めるのを検討してください。</span><span class="sxs-lookup"><span data-stu-id="ee63b-137">Consider starting with the most impactful features and those that will integrate more naturally with Teams.</span></span> <span data-ttu-id="ee63b-138">ユーザーがメイン アプリを起動し、一連の機能にアクセスできるのを常に許可できます。</span><span class="sxs-lookup"><span data-stu-id="ee63b-138">Remember, you can always allow users to launch the main app and access its full set of features.</span></span>

<span data-ttu-id="ee63b-139">技術的な作業を開始する前に、Teams アプリの計画を行います。</span><span class="sxs-lookup"><span data-stu-id="ee63b-139">Before you begin any technical work, do some planning for your Teams app:</span></span>

1. <span data-ttu-id="ee63b-140">[アプリの使用例を Teams プラットフォームの機能にマップします](../concepts/design/map-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-140">[Map your app's use cases to Teams platform capabilities](../concepts/design/map-use-cases.md).</span></span>
1. <span data-ttu-id="ee63b-141">[アプリのエントリ ポイントを決定します](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-141">[Determine your app's entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="ee63b-142">個人の使用、共同作業、または両方の目的ですか?</span><span class="sxs-lookup"><span data-stu-id="ee63b-142">Is it for personal use, collaboration, or both?</span></span>

## <a name="understand-sharepoint-requirements-and-options"></a><span data-ttu-id="ee63b-143">SharePoint の要件とオプションについて</span><span class="sxs-lookup"><span data-stu-id="ee63b-143">Understand SharePoint requirements and options</span></span>

<span data-ttu-id="ee63b-144">\***統合シナリオ**: SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="ee63b-144">\***Integration scenarios**: SharePoint\*</span></span>

<span data-ttu-id="ee63b-145">既存の [SharePoint](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) ページを Teams タブとして統合できます。次のことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="ee63b-145">You can integrate an existing [SharePoint page](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) as a Teams tab. Remember the following:</span></span>

* <span data-ttu-id="ee63b-146">最新の *SharePoint* Online ページである必要があります</span><span class="sxs-lookup"><span data-stu-id="ee63b-146">It must be a *modern* SharePoint Online page</span></span>
* <span data-ttu-id="ee63b-147">個人用タブだけがサポートされています (ページをチャネル タブとして統合できない)</span><span class="sxs-lookup"><span data-stu-id="ee63b-147">Only personal tabs are supported (you can't integrate your page as a channel tab)</span></span>

<span data-ttu-id="ee63b-148">または、SharePoint Framework を使用して [Teams タブを作成することもできます](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-148">Alternatively, you can build a Teams tab [using the SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).</span></span>

## <a name="aim-towards-multi-tenancy"></a><span data-ttu-id="ee63b-149">マルチテナントを目指す</span><span class="sxs-lookup"><span data-stu-id="ee63b-149">Aim towards multi-tenancy</span></span>

<span data-ttu-id="ee63b-150">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="ee63b-150">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="ee63b-151">アプリが複数の組織で使用されている場合は、製品の拡張性を高め、配布を大幅に簡素化するマルチテナント ホスティングを検討してください。</span><span class="sxs-lookup"><span data-stu-id="ee63b-151">If your app is used by multiple organizations, consider multi-tenant hosting that would make your product scalable and greatly simplify distribution.</span></span>

## <a name="review-your-apis"></a><span data-ttu-id="ee63b-152">API を確認する</span><span class="sxs-lookup"><span data-stu-id="ee63b-152">Review your APIs</span></span>

<span data-ttu-id="ee63b-153">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ\*</span><span class="sxs-lookup"><span data-stu-id="ee63b-153">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="ee63b-154">Teams と統合された場合、アプリの既存の API とデータ構造がアプリを完全にサポートすると想定していけない。</span><span class="sxs-lookup"><span data-stu-id="ee63b-154">Don't assume your app's existing APIs and data structures fully support the app when integrated with Teams.</span></span> <span data-ttu-id="ee63b-155">Id マッピング、ディープ リンクサポート、Microsoft Graph[](../concepts/authentication/configure-identity-provider.md)の組[](../concepts/build-and-test/deep-links.md)み込みのために、Teams に関するコンテキスト情報を使用してこれらを拡張[する必要がある場合があります](https://docs.microsoft.com/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-155">You might need to augment these with contextual information about Teams for [identity mapping](../concepts/authentication/configure-identity-provider.md), [deep-link support](../concepts/build-and-test/deep-links.md), and [incorporating Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="ee63b-156">Teams タブまたはボットのコンテキストを取得する [方法について詳しくは、以下をご](../tabs/how-to/access-teams-context.md) 覧 [ください](../bots/how-to/get-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-156">Learn more about getting context for your Teams [tab](../tabs/how-to/access-teams-context.md) or [bot](../bots/how-to/get-teams-context.md).</span></span>

## <a name="understand-authentication-options"></a><span data-ttu-id="ee63b-157">認証オプションについて</span><span class="sxs-lookup"><span data-stu-id="ee63b-157">Understand authentication options</span></span>

<span data-ttu-id="ee63b-158">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="ee63b-158">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="ee63b-159">Azure Active Directory (AD) は Teams の ID プロバイダーです。</span><span class="sxs-lookup"><span data-stu-id="ee63b-159">Azure Active Directory (AD) is the identity provider for Teams.</span></span> <span data-ttu-id="ee63b-160">アプリで別の ID プロバイダーを使用する場合は、ID マッピングの演習を行う必要があります。または Azure AD とフェデレーションする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ee63b-160">If your app uses a different identity provider, you must either do an identity mapping exercise or federate with Azure AD.</span></span>

<span data-ttu-id="ee63b-161">Teams には、サードパーティ アプリ用の Azure AD を使用したシングル サインオン (SSO) メカニズムと、OAuth や Open ID Connect (OIDC) などの標準を使用した他の ID プロバイダーへの認証フローのガイダンスがあります。</span><span class="sxs-lookup"><span data-stu-id="ee63b-161">Teams has single sign-on (SSO) mechanisms with Azure AD for third-party apps and guidance for authentication flows to other identity providers using standards such as OAuth and Open ID Connect (OIDC).</span></span>

<span data-ttu-id="ee63b-162">SharePoint ページの場合は、SSO のみを使用し、SSO を別のアプリ (ID は SharePoint アプリ) で動作する場合は、別の Azure AD ID を追加することはできません。</span><span class="sxs-lookup"><span data-stu-id="ee63b-162">For SharePoint pages, you can only use SSO and can't add another Azure AD ID if you want SSO to work for another app (since the ID is the SharePoint app).</span></span>

<span data-ttu-id="ee63b-163">Teams での認証 [について詳しくは、次のページを参照してください](../concepts/authentication/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-163">Learn more about [authentication in Teams](../concepts/authentication/authentication.md).</span></span>

## <a name="follow-teams-design-guidelines"></a><span data-ttu-id="ee63b-164">Teams の設計ガイドラインに従う</span><span class="sxs-lookup"><span data-stu-id="ee63b-164">Follow Teams design guidelines</span></span>

<span data-ttu-id="ee63b-165">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ\*</span><span class="sxs-lookup"><span data-stu-id="ee63b-165">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="ee63b-166">一般に、アプリは Teams で自然に感じる必要があります。</span><span class="sxs-lookup"><span data-stu-id="ee63b-166">In general, your app should feel natural in Teams.</span></span> <span data-ttu-id="ee63b-167">既存のアプリ コンテンツを Teams タブに移行する方法で十分だと思われる場合がありますが、Teams の設計ガイドラインに従ってアプリを使用することを強 [く推奨します](../concepts/design/understand-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-167">You might think migrating existing app content to a Teams tab is sufficient, but we strongly recommend your app follows [Teams design guidelines](../concepts/design/understand-use-cases.md).</span></span> <span data-ttu-id="ee63b-168">「Fluent [Design System」も参照してください](https://fluentsite.z22.web.core.windows.net/)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-168">See also: [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).</span></span>

## <a name="maximize-deep-linking"></a><span data-ttu-id="ee63b-169">ディープ リンクを最大化する</span><span class="sxs-lookup"><span data-stu-id="ee63b-169">Maximize deep linking</span></span>

<span data-ttu-id="ee63b-170">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="ee63b-170">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="ee63b-171">Teams のほとんどすべての情報は、ディープ リンクを使用して直接 [リンクできます](../concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-171">Almost everything in Teams can be linked to directly with a [deep link](../concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="ee63b-172">アプリでは、特定のメッセージやタブ コンテンツへのリンクやタブ コンテンツへのリンクなど、これらを最大限に活用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ee63b-172">Your app should maximize use of these, including linking to and from specific messages and tab content.</span></span> <span data-ttu-id="ee63b-173">ディープ リンクは、実際には複数のアプリを結び付け、よりネイティブな Teams エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="ee63b-173">Deep links can really tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="be-smart-when-messaging-users"></a><span data-ttu-id="ee63b-174">メッセージング ユーザーがスマートになる</span><span class="sxs-lookup"><span data-stu-id="ee63b-174">Be smart when messaging users</span></span>

<span data-ttu-id="ee63b-175">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="ee63b-175">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="ee63b-176">Teams アプリが現在および長期的に送信する可能性があるメッセージの種類を検討します。</span><span class="sxs-lookup"><span data-stu-id="ee63b-176">Consider the types of messages your Teams app might send now and in the long term.</span></span> <span data-ttu-id="ee63b-177">アプリがマルチスレッドの会話を行う可能性がある場合、ボットは Webhook よりも柔軟性が[高い可能性があります](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)。 [](../bots/what-are-bots.md)</span><span class="sxs-lookup"><span data-stu-id="ee63b-177">If you think your app will ever have a multi-threaded conversation, a [bot](../bots/what-are-bots.md) might offer more flexibility than a [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

<span data-ttu-id="ee63b-178">ボットでは、個々のユーザーまたは *チャネルにプロ* アクティブ メッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="ee63b-178">Bots also allow you to send *proactive messages* to individual users or channels.</span></span> <span data-ttu-id="ee63b-179">これらは、外部イベントによってトリガーされるプロンプトされていないメッセージであり、ボットに送信されるメッセージではありません。</span><span class="sxs-lookup"><span data-stu-id="ee63b-179">These are unprompted messages triggered by an outside event and not a message sent to a bot.</span></span> <span data-ttu-id="ee63b-180">(たとえば、ボットがインストールされている場合や、新しいユーザーがチャネルに参加するときに、ボットからウェルカム メッセージを送信できます)。</span><span class="sxs-lookup"><span data-stu-id="ee63b-180">(For example, your bot can send a welcome message when it's installed or a new user joins a channel.)</span></span>

<span data-ttu-id="ee63b-181">プロアクティブ メッセージを送信するには、Teams 固有の識別子が必要です。[](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)この情報は、名簿またはユーザー[](../bots/how-to/conversations/subscribe-to-conversation-events.md)プロファイル データをフェッチしたり、会話イベントをサブスクライブしたり[、Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging)を使用して取得できます。</span><span class="sxs-lookup"><span data-stu-id="ee63b-181">Sending proactive messages requires Teams-specific identifiers—you can capture this information by [fetching roster or user profile data](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), [subscribing to conversation events](../bots/how-to/conversations/subscribe-to-conversation-events.md), or using [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).</span></span>

<span data-ttu-id="ee63b-182">過剰なメッセージを持つユーザーに迷惑メールを送信しないように注意してください。</span><span class="sxs-lookup"><span data-stu-id="ee63b-182">Be careful not to spam users with excessive messages.</span></span> <span data-ttu-id="ee63b-183">Teams 機能でサポートされている場合は、ユーザーにアプリの通知設定を構成させる (たとえば、「プロンプされていないメッセージを送信しない」など) を検討してください。</span><span class="sxs-lookup"><span data-stu-id="ee63b-183">If the Teams capability supports it, consider letting users configure notification settings for your app (for example, "Don't send me unprompted messages.").</span></span>

## <a name="use-sharepoint-for-file-and-data-storage"></a><span data-ttu-id="ee63b-184">ファイルおよびデータ ストレージに SharePoint を使用する</span><span class="sxs-lookup"><span data-stu-id="ee63b-184">Use SharePoint for file and data storage</span></span>

<span data-ttu-id="ee63b-185">***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*</span><span class="sxs-lookup"><span data-stu-id="ee63b-185">***Integration scenarios:** Standalone apps, collaboration apps, SharePoint pages*</span></span>

<span data-ttu-id="ee63b-186">チームが作成されると、そのチームのファイルとデータ ストレージをサポートするために [SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) サイト コレクションも準備されます。</span><span class="sxs-lookup"><span data-stu-id="ee63b-186">When a team is created, a [SharePoint site collection](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) is also provisioned to support file and data storage for that team.</span></span> <span data-ttu-id="ee63b-187">アプリがファイルを操作する場合は、この機能を利用できます。また、この機能を利用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ee63b-187">Your app can and should leverage this feature if it interacts with files.</span></span> <span data-ttu-id="ee63b-188">サイト コレクションを使用して、生データを SharePoint リストと Excel に保存することもできます。</span><span class="sxs-lookup"><span data-stu-id="ee63b-188">You can also use the site collection to store raw data in SharePoint Lists and Excel.</span></span>
