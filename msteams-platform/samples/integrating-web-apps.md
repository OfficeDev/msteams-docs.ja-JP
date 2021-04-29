---
author: heath-hamilton
description: 既存の Web アプリと Microsoft Teams を統合するためのベスト プラクティス
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Web アプリ
ms.openlocfilehash: 6227964fdf114fe4e4cd38f18fd1932db8bc5960
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075732"
---
# <a name="web-apps"></a><span data-ttu-id="9ee96-103">Web アプリ</span><span class="sxs-lookup"><span data-stu-id="9ee96-103">Web apps</span></span> 

<span data-ttu-id="9ee96-104">Web アプリを Teams と適切に統合することで、Teams のソーシャル機能や共同作業機能に適した Web アプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-104">You can make web apps suitable with Teams' social and collaborative features, by properly integrating them with Teams.</span></span>
  
<span data-ttu-id="9ee96-105">Teams と統合できるさまざまな種類のアプリは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="9ee96-105">The different types of apps which you can integrate with Teams are as follows:</span></span>
* <span data-ttu-id="9ee96-106">**スタンドアロン アプリ**: スタンドアロン アプリは、単一ページまたは大規模で複雑なアプリです。</span><span class="sxs-lookup"><span data-stu-id="9ee96-106">**Standalone apps**: A stand alone app is a single-page or large, and complex app.</span></span> <span data-ttu-id="9ee96-107">ユーザーは Teams でいくつかの側面を使用できます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-107">The user can use some aspects of it in Teams.</span></span>
* <span data-ttu-id="9ee96-108">**コラボレーション アプリ**: Teams に固有のソーシャル機能と共同作業機能用に既に構築されたアプリ。</span><span class="sxs-lookup"><span data-stu-id="9ee96-108">**Collaboration apps**: An app already built for the social and collaborative features inherent to Teams.</span></span>
* <span data-ttu-id="9ee96-109">**SharePoint**: Teams で表示する SharePoint ページ。</span><span class="sxs-lookup"><span data-stu-id="9ee96-109">**SharePoint**: A SharePoint page you want to surface in Teams.</span></span>

<span data-ttu-id="9ee96-110">統合シナリオに該当する適切なガイドラインをマップして従えます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-110">You can map and follow the appropriate guideline applicable to your integration scenario.</span></span>
<span data-ttu-id="9ee96-111">このドキュメントでは、Teams の機能の概要、ファイルとデータストレージの共有ポイント要件、API 要件、認証、アプリと Teams のディープリンクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="9ee96-111">This document gives an overview of Teams capabilities, share-point requirements for file and data storage, API requirements, authentication and deep-linking of your app with Teams.</span></span>
 
## <a name="get-to-know-teams-platform-capabilities"></a><span data-ttu-id="9ee96-112">Teams プラットフォームの機能を知る</span><span class="sxs-lookup"><span data-stu-id="9ee96-112">Get to know Teams platform capabilities</span></span>

<span data-ttu-id="9ee96-113">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="9ee96-113">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="9ee96-114">Teams アプリには、必要な共同作業機能と予期される共同作業機能が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ee96-114">Your Teams app must include required and expected collaborative features.</span></span> <span data-ttu-id="9ee96-115">アプリの統合を操作するには、Teams 開発の用語を理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="9ee96-115">To work with app integration, it is important to familiarize with Teams development terminology.</span></span>

|<span data-ttu-id="9ee96-116">アプリの一般的な機能</span><span class="sxs-lookup"><span data-stu-id="9ee96-116">Common app features</span></span>   |<span data-ttu-id="9ee96-117">Teams プラットフォームの機能</span><span class="sxs-lookup"><span data-stu-id="9ee96-117">Teams platform capabilities</span></span>   |
|----------|-----------|
|<span data-ttu-id="9ee96-118">埋め込み Web ページ、ホームページ、または Web ビュー</span><span class="sxs-lookup"><span data-stu-id="9ee96-118">Embedded webpage, homepage, or webview</span></span>  |[<span data-ttu-id="9ee96-119">タブ</span><span class="sxs-lookup"><span data-stu-id="9ee96-119">Tabs</span></span>](../tabs/what-are-tabs.md)  |
|<span data-ttu-id="9ee96-120">ショートカットと拡張機能を共有する</span><span class="sxs-lookup"><span data-stu-id="9ee96-120">Share shortcuts and extensions</span></span>  |[<span data-ttu-id="9ee96-121">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="9ee96-121">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="9ee96-122">操作のショートカットと拡張機能</span><span class="sxs-lookup"><span data-stu-id="9ee96-122">Action shortcuts and extensions</span></span>  |[<span data-ttu-id="9ee96-123">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="9ee96-123">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="9ee96-124">チャットボット</span><span class="sxs-lookup"><span data-stu-id="9ee96-124">Chatbots</span></span>  |[<span data-ttu-id="9ee96-125">ボット</span><span class="sxs-lookup"><span data-stu-id="9ee96-125">Bots</span></span>](../bots/what-are-bots.md) |
|<span data-ttu-id="9ee96-126">チャネル通知</span><span class="sxs-lookup"><span data-stu-id="9ee96-126">Channel notifications</span></span>  |[<span data-ttu-id="9ee96-127">ボット</span><span class="sxs-lookup"><span data-stu-id="9ee96-127">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="9ee96-128">受信 Webhook</span><span class="sxs-lookup"><span data-stu-id="9ee96-128">Incoming webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[<span data-ttu-id="9ee96-129">Office 365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="9ee96-129">Office 365 Connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="9ee96-130">メッセージ外部サービス</span><span class="sxs-lookup"><span data-stu-id="9ee96-130">Message external services</span></span>  |[<span data-ttu-id="9ee96-131">ボット</span><span class="sxs-lookup"><span data-stu-id="9ee96-131">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="9ee96-132">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="9ee96-132">Outgoing webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="9ee96-133">モーダル</span><span class="sxs-lookup"><span data-stu-id="9ee96-133">Modals</span></span>  |[<span data-ttu-id="9ee96-134">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="9ee96-134">Task modules</span></span>](../task-modules-and-cards/what-are-task-modules.md)  |
|<span data-ttu-id="9ee96-135">コンテンツが豊富なカード</span><span class="sxs-lookup"><span data-stu-id="9ee96-135">Content-rich cards</span></span>  |[<span data-ttu-id="9ee96-136">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="9ee96-136">Adaptive Cards</span></span>](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a><span data-ttu-id="9ee96-137">機能のサブセットを決定する</span><span class="sxs-lookup"><span data-stu-id="9ee96-137">Determine a subset of functionality</span></span>

<span data-ttu-id="9ee96-138">\***統合シナリオ**: スタンドアロン アプリ\*</span><span class="sxs-lookup"><span data-stu-id="9ee96-138">\***Integration scenarios**: Standalone apps\*</span></span>

<span data-ttu-id="9ee96-139">既存のアプリケーションのすべての機能を Teams に統合すると、多くの場合、特に大規模なアプリでは、強制的または不自然なユーザー エクスペリエンスが発生します。</span><span class="sxs-lookup"><span data-stu-id="9ee96-139">Integrating all features of an existing application into Teams often leads to a forced or unnatural user experience, particularly in larger apps.</span></span> <span data-ttu-id="9ee96-140">最も影響の大きな機能と、Teams とより自然に統合する機能から始める。</span><span class="sxs-lookup"><span data-stu-id="9ee96-140">Start with the most impactful features and those that integrates more naturally with Teams.</span></span> <span data-ttu-id="9ee96-141">ユーザーがメイン アプリを起動し、一連の機能にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-141">You can allow users to launch the main app and access its full set of features.</span></span>

<span data-ttu-id="9ee96-142">**アプリを Teams に統合するための前提条件** アプリを Teams に統合するための前提条件を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9ee96-142">**Prerequisites to integrate your app with Teams** Following are the prerequisites to integrate your app with Teams.</span></span> 

1. <span data-ttu-id="9ee96-143">[アプリの使用例を Teams プラットフォームの機能にマップします](../concepts/design/map-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="9ee96-143">[Map your app's use cases to Teams platform capabilities](../concepts/design/map-use-cases.md).</span></span>
1. <span data-ttu-id="9ee96-144">[アプリのエントリ ポイントを決定します](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="9ee96-144">[Determine your app's entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="9ee96-145">個人の使用、共同作業、または両方の目的ですか?</span><span class="sxs-lookup"><span data-stu-id="9ee96-145">Is it for personal use, collaboration, or both?</span></span>

## <a name="understand-sharepoint-requirements-and-options"></a><span data-ttu-id="9ee96-146">SharePoint の要件とオプションについて</span><span class="sxs-lookup"><span data-stu-id="9ee96-146">Understand SharePoint requirements and options</span></span>

<span data-ttu-id="9ee96-147">\***統合シナリオ**: SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="9ee96-147">\***Integration scenarios**: SharePoint\*</span></span>

<span data-ttu-id="9ee96-148">既存の [SharePoint](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) ページを Teams タブとして統合するには、次の点を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ee96-148">To integrate an existing [SharePoint page](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) as a Teams tab, you must consider the following:</span></span>

* <span data-ttu-id="9ee96-149">最新の SharePoint *オンライン* ページである必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ee96-149">It must be a *modern* SharePoint online page.</span></span>
* <span data-ttu-id="9ee96-150">個人用タブのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-150">Only personal tabs are supported.</span></span> <span data-ttu-id="9ee96-151">ページをチャネル タブとして統合することはできません。</span><span class="sxs-lookup"><span data-stu-id="9ee96-151">You cannot integrate your page as a channel tab.</span></span>

<span data-ttu-id="9ee96-152">または、SharePoint Framework を使用して [Teams タブを作成することもできます](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)。</span><span class="sxs-lookup"><span data-stu-id="9ee96-152">Alternatively, you can build a Teams tab [using the SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).</span></span>

## <a name="aim-towards-multi-tenancy"></a><span data-ttu-id="9ee96-153">マルチテナントを目指す</span><span class="sxs-lookup"><span data-stu-id="9ee96-153">Aim towards multi-tenancy</span></span>

<span data-ttu-id="9ee96-154">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="9ee96-154">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="9ee96-155">アプリが複数の組織で使用されている場合は、製品の拡張性を高め、配布を大幅に簡素化するマルチテナント ホスティングを検討してください。</span><span class="sxs-lookup"><span data-stu-id="9ee96-155">If your app is used by multiple organizations, consider multi-tenant hosting that makes your product scalable and greatly simplify the distribution.</span></span>

## <a name="review-your-apis"></a><span data-ttu-id="9ee96-156">API を確認する</span><span class="sxs-lookup"><span data-stu-id="9ee96-156">Review your APIs</span></span>

<span data-ttu-id="9ee96-157">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ\*</span><span class="sxs-lookup"><span data-stu-id="9ee96-157">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="9ee96-158">Teams と統合する場合は、アプリの既存の API とデータ構造がアプリをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ee96-158">You must make your app's existing APIs and data structures support the app when integrating with Teams.</span></span> <span data-ttu-id="9ee96-159">サポートを拡張するには、ID マッピング、ディープ リンク サポート、および Microsoft Graph[](../concepts/authentication/configure-identity-provider.md)の組[](../concepts/build-and-test/deep-links.md)み込みのために、Teams に関するコンテキスト情報を使用して API とデータ構造を[拡張する必要があります](https://docs.microsoft.com/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="9ee96-159">To extend the support, you must augment the APIs and data structures with contextual information about Teams for [identity mapping](../concepts/authentication/configure-identity-provider.md), [deep-link support](../concepts/build-and-test/deep-links.md), and [incorporating Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="9ee96-160">Teams タブまたはボットのコンテキストを取得する [方法について詳しくは、以下をご](../tabs/how-to/access-teams-context.md) 覧 [ください](../bots/how-to/get-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="9ee96-160">Learn more about getting context for your Teams [tab](../tabs/how-to/access-teams-context.md) or [bot](../bots/how-to/get-teams-context.md).</span></span>

## <a name="understand-authentication-options"></a><span data-ttu-id="9ee96-161">認証オプションについて</span><span class="sxs-lookup"><span data-stu-id="9ee96-161">Understand authentication options</span></span>

<span data-ttu-id="9ee96-162">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="9ee96-162">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="9ee96-163">Azure Active Directory (AD) は Teams の ID プロバイダーです。</span><span class="sxs-lookup"><span data-stu-id="9ee96-163">Azure Active Directory (AD) is the identity provider for Teams.</span></span> <span data-ttu-id="9ee96-164">アプリで別の ID プロバイダーを使用する場合は、ID マッピングの演習を実行するか、Azure の ID プロバイダーと組み合わせるAD。</span><span class="sxs-lookup"><span data-stu-id="9ee96-164">If your app uses a different identity provider, you must either do an identity mapping exercise or combine with Azure AD.</span></span>

<span data-ttu-id="9ee96-165">Teams には、サード パーティ製アプリ用の Azure ADシングル サインオン (SSO) メカニズムがあります。</span><span class="sxs-lookup"><span data-stu-id="9ee96-165">Teams has single sign-on (SSO) mechanisms with Azure AD for third-party apps.</span></span> <span data-ttu-id="9ee96-166">また、OIDC と呼ばれる OAuth や Open ID Connect などの標準を使用して、他の ID プロバイダーに対する認証フローのガイダンスも提供します。</span><span class="sxs-lookup"><span data-stu-id="9ee96-166">It also provides the guidance for authentication flows to other identity providers using standards such as OAuth and Open ID Connect, known as OIDC.</span></span>

<span data-ttu-id="9ee96-167">SharePoint ページの場合は、SSO のみを使用し、その ID が SharePoint アプリであるとして SSO を別のアプリで動作する場合は、別の Azure AD ID を追加できません。</span><span class="sxs-lookup"><span data-stu-id="9ee96-167">For SharePoint pages, you can only use SSO and cannot add another Azure AD ID if you want SSO to work for another app as the ID is the SharePoint app.</span></span>

<span data-ttu-id="9ee96-168">Teams での認証 [について詳しくは、次のページを参照してください](../concepts/authentication/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="9ee96-168">Learn more about [authentication in Teams](../concepts/authentication/authentication.md).</span></span>

## <a name="follow-teams-design-guidelines"></a><span data-ttu-id="9ee96-169">Teams の設計ガイドラインに従う</span><span class="sxs-lookup"><span data-stu-id="9ee96-169">Follow Teams design guidelines</span></span>

<span data-ttu-id="9ee96-170">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ\*</span><span class="sxs-lookup"><span data-stu-id="9ee96-170">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="9ee96-171">Teams のデザイン [ガイドラインに従って、](../concepts/design/understand-use-cases.md) アプリを Teams にネイティブにしてください。</span><span class="sxs-lookup"><span data-stu-id="9ee96-171">Ensure to follow [Teams design guidelines](../concepts/design/understand-use-cases.md) to make your app native to Teams.</span></span> <span data-ttu-id="9ee96-172">既存のアプリ コンテンツを Teams タブに移行することはできません。アプリの設計の詳細については [、「Fluent Design System」を参照してください](https://fluentsite.z22.web.core.windows.net/)。</span><span class="sxs-lookup"><span data-stu-id="9ee96-172">You cannot migrate an existing app content to a Teams tab. For more information on app design, see [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).</span></span>

## <a name="maximize-deep-linking"></a><span data-ttu-id="9ee96-173">ディープ リンクを最大化する</span><span class="sxs-lookup"><span data-stu-id="9ee96-173">Maximize deep linking</span></span>

<span data-ttu-id="9ee96-174">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="9ee96-174">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="9ee96-175">Teams 内で情報と機能へのリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-175">You can create links to information and features within Teams.</span></span> <span data-ttu-id="9ee96-176">ディープ [リンクを使用](../concepts/build-and-test/deep-links.md) してアプリを Teams とリンクし、複数のアプリを結び付け、よりネイティブな Teams エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="9ee96-176">Use [deep links](../concepts/build-and-test/deep-links.md) to link your app with Teams as they tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="be-smart-when-messaging-users"></a><span data-ttu-id="9ee96-177">メッセージング ユーザーがスマートになる</span><span class="sxs-lookup"><span data-stu-id="9ee96-177">Be smart when messaging users</span></span>

<span data-ttu-id="9ee96-178">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="9ee96-178">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="9ee96-179">Webhook [よりも柔軟性](../bots/what-are-bots.md) が高い Teams アプリのボットをマルチスレッド会話に [使用します](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="9ee96-179">Use a [bot](../bots/what-are-bots.md) in your Teams app for multi-threaded conversation, as it offers more flexibility than a [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

<span data-ttu-id="9ee96-180">ボットでは、個々のユーザーまたは **チャネルにプロ** アクティブ メッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-180">Bots also allow you to send **proactive messages** to individual users or channels.</span></span> <span data-ttu-id="9ee96-181">プロアクティブ メッセージは、ボットに送信されるメッセージではなく、外部イベントによってトリガーされるプロプロンプトされていないメッセージです。</span><span class="sxs-lookup"><span data-stu-id="9ee96-181">The proactive messages are unprompted messages triggered by an outside event and not a message sent to a bot.</span></span> <span data-ttu-id="9ee96-182">たとえば、ボットがインストールされている場合、または新しいユーザーがチャネルに参加するときに、ボットからウェルカム メッセージが送信されます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-182">For example, your bot sends a welcome message when it is installed or a new user joins a channel.</span></span> 

<span data-ttu-id="9ee96-183">プロアクティブ メッセージを送信するには、Teams 固有の識別子が必要です。</span><span class="sxs-lookup"><span data-stu-id="9ee96-183">Sending proactive messages requires Teams-specific identifiers.</span></span> <span data-ttu-id="9ee96-184">この情報は、名簿[](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)またはユーザー プロファイル データのフェッチ、[](../bots/how-to/conversations/subscribe-to-conversation-events.md)会話イベントのサブスクライブ、または Microsoft Graph を使用して[取得できます](https://docs.microsoft.com/graph/teams-proactive-messaging)。</span><span class="sxs-lookup"><span data-stu-id="9ee96-184">You can capture the information by [fetching roster or user profile data](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), [subscribing to conversation events](../bots/how-to/conversations/subscribe-to-conversation-events.md), or using [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).</span></span>

<span data-ttu-id="9ee96-185">過剰なメッセージを持つユーザーに迷惑メールを送信しない。</span><span class="sxs-lookup"><span data-stu-id="9ee96-185">Do not spam users with excessive messages.</span></span> <span data-ttu-id="9ee96-186">Teams 機能でサポートされている場合、ユーザーはアプリの通知設定を構成できます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-186">If the Teams capability supports it, the users can configure notification settings for your app.</span></span>   
<span data-ttu-id="9ee96-187">通知メッセージの例を次に示します。プロンプトされていないメッセージ **は送信しません**。</span><span class="sxs-lookup"><span data-stu-id="9ee96-187">Following is an example of a notification message: **Don't send me unprompted messages**.</span></span>

## <a name="use-sharepoint-for-file-and-data-storage"></a><span data-ttu-id="9ee96-188">ファイルおよびデータ ストレージに SharePoint を使用する</span><span class="sxs-lookup"><span data-stu-id="9ee96-188">Use SharePoint for file and data storage</span></span>

<span data-ttu-id="9ee96-189">***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*</span><span class="sxs-lookup"><span data-stu-id="9ee96-189">***Integration scenarios:** Standalone apps, collaboration apps, SharePoint pages*</span></span>

<span data-ttu-id="9ee96-190">チームが作成されると、そのチームのファイルとデータ ストレージをサポートするために [SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) サイト コレクションも準備されます。</span><span class="sxs-lookup"><span data-stu-id="9ee96-190">When a team is created, a [SharePoint site collection](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) is also provisioned to support file and data storage for that team.</span></span> <span data-ttu-id="9ee96-191">アプリがファイルを操作する場合は、この機能を活用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ee96-191">Your app must leverage this feature if it interacts with files.</span></span> <span data-ttu-id="9ee96-192">サイト コレクションを使用して、生データを SharePoint リストと Excel に格納します。</span><span class="sxs-lookup"><span data-stu-id="9ee96-192">Use the site collection to store raw data in SharePoint Lists and Excel.</span></span>

## <a name="see-also"></a><span data-ttu-id="9ee96-193">関連項目</span><span class="sxs-lookup"><span data-stu-id="9ee96-193">See also</span></span>

[<span data-ttu-id="9ee96-194">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="9ee96-194">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
