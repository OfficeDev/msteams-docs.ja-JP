---
author: heath-hamilton
description: 既存の Web アプリとアプリを統合するためのベスト プラクティスMicrosoft Teams
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Web アプリ
ms.openlocfilehash: b7f530198a8e1c240e3cf4b227d786af94f6c89e
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630433"
---
# <a name="web-apps"></a><span data-ttu-id="6e875-103">Web アプリ</span><span class="sxs-lookup"><span data-stu-id="6e875-103">Web apps</span></span> 

<span data-ttu-id="6e875-104">Web アプリを適切に統合することで、Teamsのソーシャル機能や共同作業機能に適Teams。</span><span class="sxs-lookup"><span data-stu-id="6e875-104">You can make web apps suitable with Teams' social and collaborative features, by properly integrating them with Teams.</span></span>
  
<span data-ttu-id="6e875-105">アプリと統合できるさまざまな種類のアプリはTeams次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="6e875-105">The different types of apps which you can integrate with Teams are as follows:</span></span>
* <span data-ttu-id="6e875-106">**スタンドアロン アプリ**: スタンドアロン アプリは、単一ページまたは大規模で複雑なアプリです。</span><span class="sxs-lookup"><span data-stu-id="6e875-106">**Standalone apps**: A stand alone app is a single-page or large, and complex app.</span></span> <span data-ttu-id="6e875-107">ユーザーは、その一部の側面をTeams。</span><span class="sxs-lookup"><span data-stu-id="6e875-107">The user can use some aspects of it in Teams.</span></span>
* <span data-ttu-id="6e875-108">**コラボレーション アプリ**: ソーシャル機能とコラボレーション機能に固有のアプリが既に構築Teams。</span><span class="sxs-lookup"><span data-stu-id="6e875-108">**Collaboration apps**: An app already built for the social and collaborative features inherent to Teams.</span></span>
* <span data-ttu-id="6e875-109">**SharePoint**: SharePointに表示するページTeams。</span><span class="sxs-lookup"><span data-stu-id="6e875-109">**SharePoint**: A SharePoint page you want to surface in Teams.</span></span>

<span data-ttu-id="6e875-110">統合シナリオに該当する適切なガイドラインをマップして従えます。</span><span class="sxs-lookup"><span data-stu-id="6e875-110">You can map and follow the appropriate guideline applicable to your integration scenario.</span></span>
<span data-ttu-id="6e875-111">このドキュメントでは、Teams 機能の概要、ファイルとデータストレージの共有ポイント要件、API 要件、認証、アプリと Teams のディープリンクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="6e875-111">This document gives an overview of Teams capabilities, share-point requirements for file and data storage, API requirements, authentication, and deep-linking of your app with Teams.</span></span>
 
## <a name="get-to-know-teams-platform-capabilities"></a><span data-ttu-id="6e875-112">プラットフォームの機能Teamsする</span><span class="sxs-lookup"><span data-stu-id="6e875-112">Get to know Teams platform capabilities</span></span>

<span data-ttu-id="6e875-113">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="6e875-113">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="6e875-114">アプリTeams必要な共同作業機能を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e875-114">Your Teams app must include required and expected collaborative features.</span></span> <span data-ttu-id="6e875-115">アプリの統合を操作するには、開発用語を理解Teams重要です。</span><span class="sxs-lookup"><span data-stu-id="6e875-115">To work with app integration, it is important to familiarize with Teams development terminology.</span></span>

|<span data-ttu-id="6e875-116">アプリの一般的な機能</span><span class="sxs-lookup"><span data-stu-id="6e875-116">Common app features</span></span>   |<span data-ttu-id="6e875-117">Teams機能</span><span class="sxs-lookup"><span data-stu-id="6e875-117">Teams platform capabilities</span></span>   |
|----------|-----------|
|<span data-ttu-id="6e875-118">埋め込み Web ページ、ホームページ、または Web ビュー</span><span class="sxs-lookup"><span data-stu-id="6e875-118">Embedded webpage, homepage, or webview</span></span>  |[<span data-ttu-id="6e875-119">タブ</span><span class="sxs-lookup"><span data-stu-id="6e875-119">Tabs</span></span>](../tabs/what-are-tabs.md)  |
|<span data-ttu-id="6e875-120">ショートカットと拡張機能を共有する</span><span class="sxs-lookup"><span data-stu-id="6e875-120">Share shortcuts and extensions</span></span>  |[<span data-ttu-id="6e875-121">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="6e875-121">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="6e875-122">操作のショートカットと拡張機能</span><span class="sxs-lookup"><span data-stu-id="6e875-122">Action shortcuts and extensions</span></span>  |[<span data-ttu-id="6e875-123">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="6e875-123">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="6e875-124">チャットボット</span><span class="sxs-lookup"><span data-stu-id="6e875-124">Chatbots</span></span>  |[<span data-ttu-id="6e875-125">ボット</span><span class="sxs-lookup"><span data-stu-id="6e875-125">Bots</span></span>](../bots/what-are-bots.md) |
|<span data-ttu-id="6e875-126">チャネル通知</span><span class="sxs-lookup"><span data-stu-id="6e875-126">Channel notifications</span></span>  |[<span data-ttu-id="6e875-127">ボット</span><span class="sxs-lookup"><span data-stu-id="6e875-127">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="6e875-128">受信 Webhook</span><span class="sxs-lookup"><span data-stu-id="6e875-128">Incoming webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[<span data-ttu-id="6e875-129">Office 365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="6e875-129">Office 365 Connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="6e875-130">メッセージ外部サービス</span><span class="sxs-lookup"><span data-stu-id="6e875-130">Message external services</span></span>  |[<span data-ttu-id="6e875-131">ボット</span><span class="sxs-lookup"><span data-stu-id="6e875-131">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="6e875-132">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="6e875-132">Outgoing webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="6e875-133">モーダル</span><span class="sxs-lookup"><span data-stu-id="6e875-133">Modals</span></span>  |[<span data-ttu-id="6e875-134">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="6e875-134">Task modules</span></span>](../task-modules-and-cards/what-are-task-modules.md)  |
|<span data-ttu-id="6e875-135">コンテンツが豊富なカード</span><span class="sxs-lookup"><span data-stu-id="6e875-135">Content-rich cards</span></span>  |[<span data-ttu-id="6e875-136">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="6e875-136">Adaptive Cards</span></span>](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a><span data-ttu-id="6e875-137">機能のサブセットを決定する</span><span class="sxs-lookup"><span data-stu-id="6e875-137">Determine a subset of functionality</span></span>

<span data-ttu-id="6e875-138">\***統合シナリオ**: スタンドアロン アプリ\*</span><span class="sxs-lookup"><span data-stu-id="6e875-138">\***Integration scenarios**: Standalone apps\*</span></span>

<span data-ttu-id="6e875-139">既存のアプリケーションのすべての機能をアプリケーションに統合Teams、特に大規模なアプリでは、強制的または不自然なユーザー エクスペリエンスが発生します。</span><span class="sxs-lookup"><span data-stu-id="6e875-139">Integrating all features of an existing application into Teams often leads to a forced or unnatural user experience, particularly in larger apps.</span></span> <span data-ttu-id="6e875-140">最も影響の大きな機能と、より自然に機能と統合する機能からTeams。</span><span class="sxs-lookup"><span data-stu-id="6e875-140">Start with the most impactful features and those that integrates more naturally with Teams.</span></span> <span data-ttu-id="6e875-141">ユーザーがメイン アプリを起動し、一連の機能にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="6e875-141">You can allow users to launch the main app and access its full set of features.</span></span>

<span data-ttu-id="6e875-142">**アプリとアプリを統合するための前提条件Teams** アプリとアプリを統合するための前提条件は次Teams。</span><span class="sxs-lookup"><span data-stu-id="6e875-142">**Prerequisites to integrate your app with Teams** Following are the prerequisites to integrate your app with Teams.</span></span> 

1. <span data-ttu-id="6e875-143">[アプリの使用例をプラットフォームの機能Teamsマップします](../concepts/design/map-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="6e875-143">[Map your app's use cases to Teams platform capabilities](../concepts/design/map-use-cases.md).</span></span>
1. <span data-ttu-id="6e875-144">[アプリのエントリ ポイントを決定します](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="6e875-144">[Determine your app's entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="6e875-145">個人の使用、共同作業、または両方の目的ですか?</span><span class="sxs-lookup"><span data-stu-id="6e875-145">Is it for personal use, collaboration, or both?</span></span>

## <a name="understand-sharepoint-requirements-and-options"></a><span data-ttu-id="6e875-146">要件SharePointオプションについて理解する</span><span class="sxs-lookup"><span data-stu-id="6e875-146">Understand SharePoint requirements and options</span></span>

<span data-ttu-id="6e875-147">\***統合シナリオ**: SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="6e875-147">\***Integration scenarios**: SharePoint\*</span></span>

<span data-ttu-id="6e875-148">既存のページを[[SharePoint]](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites)タブTeams統合するには、次の点を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e875-148">To integrate an existing [SharePoint page](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) as a Teams tab, you must consider the following:</span></span>

* <span data-ttu-id="6e875-149">最新のオンライン ページ *SharePoint* 必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e875-149">It must be a *modern* SharePoint online page.</span></span>
* <span data-ttu-id="6e875-150">個人用タブのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="6e875-150">Only personal tabs are supported.</span></span> <span data-ttu-id="6e875-151">ページをチャネル タブとして統合することはできません。</span><span class="sxs-lookup"><span data-stu-id="6e875-151">You cannot integrate your page as a channel tab.</span></span>

<span data-ttu-id="6e875-152">または、タブを使用してTeamsタブ[を作成SharePoint Framework。](/sharepoint/dev/spfx/integrate-with-teams-introduction)</span><span class="sxs-lookup"><span data-stu-id="6e875-152">Alternatively, you can build a Teams tab [using the SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).</span></span>

## <a name="aim-towards-multi-tenancy"></a><span data-ttu-id="6e875-153">マルチテナントを目指す</span><span class="sxs-lookup"><span data-stu-id="6e875-153">Aim towards multi-tenancy</span></span>

<span data-ttu-id="6e875-154">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="6e875-154">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="6e875-155">アプリが複数の組織で使用されている場合は、製品の拡張性を高め、配布を大幅に簡素化するマルチテナント ホスティングを検討してください。</span><span class="sxs-lookup"><span data-stu-id="6e875-155">If your app is used by multiple organizations, consider multi-tenant hosting that makes your product scalable and greatly simplify the distribution.</span></span>

## <a name="review-your-apis"></a><span data-ttu-id="6e875-156">API を確認する</span><span class="sxs-lookup"><span data-stu-id="6e875-156">Review your APIs</span></span>

<span data-ttu-id="6e875-157">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ\*</span><span class="sxs-lookup"><span data-stu-id="6e875-157">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="6e875-158">アプリと統合する場合は、アプリの既存の API とデータ構造がアプリをサポートTeams。</span><span class="sxs-lookup"><span data-stu-id="6e875-158">You must make your app's existing APIs and data structures support the app when integrating with Teams.</span></span> <span data-ttu-id="6e875-159">サポートを拡張するには、ID マッピング、ディープ リンク サポート、Microsoft Graph の組み[](../concepts/authentication/configure-identity-provider.md)込みのために[](../concepts/build-and-test/deep-links.md)、Teams に関するコンテキスト情報を使用して API とデータ構造を拡張する[必要があります](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="6e875-159">To extend the support, you must augment the APIs and data structures with contextual information about Teams for [identity mapping](../concepts/authentication/configure-identity-provider.md), [deep-link support](../concepts/build-and-test/deep-links.md), and [incorporating Microsoft Graph](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="6e875-160">詳細については、「ユーザー設定]タブまたはボットのコンテキストTeamsを取得[する](../bots/how-to/get-teams-context.md)[」を](../tabs/how-to/access-teams-context.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="6e875-160">Learn more about getting context for your Teams [tab](../tabs/how-to/access-teams-context.md) or [bot](../bots/how-to/get-teams-context.md).</span></span>

## <a name="understand-authentication-options"></a><span data-ttu-id="6e875-161">認証オプションについて</span><span class="sxs-lookup"><span data-stu-id="6e875-161">Understand authentication options</span></span>

<span data-ttu-id="6e875-162">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="6e875-162">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="6e875-163">Azure Active Directory (AD) は、ユーザーの ID プロバイダー Teams。</span><span class="sxs-lookup"><span data-stu-id="6e875-163">Azure Active Directory (AD) is the identity provider for Teams.</span></span> <span data-ttu-id="6e875-164">アプリで別の ID プロバイダーを使用する場合は、ID マッピングの演習を実行するか、Azure の ID プロバイダーと組み合わせるAD。</span><span class="sxs-lookup"><span data-stu-id="6e875-164">If your app uses a different identity provider, you must either do an identity mapping exercise or combine with Azure AD.</span></span>

<span data-ttu-id="6e875-165">Teamsサード パーティ製アプリ向け Azure ADシングル サインオン (SSO) メカニズムがあります。</span><span class="sxs-lookup"><span data-stu-id="6e875-165">Teams has single sign-on (SSO) mechanisms with Azure AD for third-party apps.</span></span> <span data-ttu-id="6e875-166">また、OIDC と呼ばれる OAuth や Open ID などの標準を使用して、他の ID プロバイダー Connectガイダンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="6e875-166">It also provides the guidance for authentication flows to other identity providers using standards such as OAuth and Open ID Connect, known as OIDC.</span></span>

<span data-ttu-id="6e875-167">このSharePointでは、SSO のみを使用できます。また、SSO を別のアプリで使用する場合は、別の Azure AD ID を追加することはできません。この ID はアプリの SharePoint です。</span><span class="sxs-lookup"><span data-stu-id="6e875-167">For SharePoint pages, you can only use SSO and cannot add another Azure AD ID if you want SSO to work for another app as the ID is the SharePoint app.</span></span>

<span data-ttu-id="6e875-168">認証の詳細[については、「Teams」 を参照してください](../concepts/authentication/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="6e875-168">Learn more about [authentication in Teams](../concepts/authentication/authentication.md).</span></span>

## <a name="follow-teams-design-guidelines"></a><span data-ttu-id="6e875-169">設計Teamsに従う</span><span class="sxs-lookup"><span data-stu-id="6e875-169">Follow Teams design guidelines</span></span>

<span data-ttu-id="6e875-170">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ\*</span><span class="sxs-lookup"><span data-stu-id="6e875-170">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="6e875-171">アプリをアプリ[Teamsネイティブに](../concepts/design/understand-use-cases.md)するための設計ガイドラインに従Teams。</span><span class="sxs-lookup"><span data-stu-id="6e875-171">Ensure to follow [Teams design guidelines](../concepts/design/understand-use-cases.md) to make your app native to Teams.</span></span> <span data-ttu-id="6e875-172">既存のアプリ コンテンツを [アプリ] タブTeamsできません。アプリの設計の詳細については[、「Fluent Design System」を参照してください](https://fluentsite.z22.web.core.windows.net/)。</span><span class="sxs-lookup"><span data-stu-id="6e875-172">You cannot migrate an existing app content to a Teams tab. For more information on app design, see [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).</span></span>

## <a name="maximize-deep-linking"></a><span data-ttu-id="6e875-173">ディープ リンクを最大化する</span><span class="sxs-lookup"><span data-stu-id="6e875-173">Maximize deep linking</span></span>

<span data-ttu-id="6e875-174">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="6e875-174">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="6e875-175">情報と機能へのリンクは、Teams。</span><span class="sxs-lookup"><span data-stu-id="6e875-175">You can create links to information and features within Teams.</span></span> <span data-ttu-id="6e875-176">ディープ[リンクを使用](../concepts/build-and-test/deep-links.md)してアプリとアプリTeamsリンクし、アプリの複数の部分を結び付け、よりネイティブなエクスペリエンスTeamsします。</span><span class="sxs-lookup"><span data-stu-id="6e875-176">Use [deep links](../concepts/build-and-test/deep-links.md) to link your app with Teams as they tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="be-smart-when-messaging-users"></a><span data-ttu-id="6e875-177">メッセージング ユーザーがスマートになる</span><span class="sxs-lookup"><span data-stu-id="6e875-177">Be smart when messaging users</span></span>

<span data-ttu-id="6e875-178">\***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="6e875-178">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="6e875-179">Webhook[よりも柔軟性が](../bots/what-are-bots.md)高Teams、マルチスレッドの会話にアプリで[ボットを使用します](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="6e875-179">Use a [bot](../bots/what-are-bots.md) in your Teams app for multi-threaded conversation, as it offers more flexibility than a [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

<span data-ttu-id="6e875-180">ボットでは、個々のユーザーまたは **チャネルにプロ** アクティブ メッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="6e875-180">Bots also allow you to send **proactive messages** to individual users or channels.</span></span> <span data-ttu-id="6e875-181">プロアクティブ メッセージは、ボットに送信されるメッセージではなく、外部イベントによってトリガーされるプロプロンプトされていないメッセージです。</span><span class="sxs-lookup"><span data-stu-id="6e875-181">The proactive messages are unprompted messages triggered by an outside event and not a message sent to a bot.</span></span> <span data-ttu-id="6e875-182">たとえば、ボットがインストールされている場合、または新しいユーザーがチャネルに参加するときに、ボットからウェルカム メッセージが送信されます。</span><span class="sxs-lookup"><span data-stu-id="6e875-182">For example, your bot sends a welcome message when it is installed or a new user joins a channel.</span></span> 

<span data-ttu-id="6e875-183">プロアクティブ メッセージの送信には、Teams固有の識別子が必要です。</span><span class="sxs-lookup"><span data-stu-id="6e875-183">Sending proactive messages requires Teams-specific identifiers.</span></span> <span data-ttu-id="6e875-184">この情報は、名簿[](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)またはユーザー プロファイル データのフェッチ、[](../bots/how-to/conversations/subscribe-to-conversation-events.md)会話イベントのサブスクライブ、または Microsoft Graph[を使用して取得できます](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="6e875-184">You can capture the information by [fetching roster or user profile data](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), [subscribing to conversation events](../bots/how-to/conversations/subscribe-to-conversation-events.md), or using [Microsoft Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams).</span></span>

<span data-ttu-id="6e875-185">過剰なメッセージを持つユーザーに迷惑メールを送信しない。</span><span class="sxs-lookup"><span data-stu-id="6e875-185">Do not spam users with excessive messages.</span></span> <span data-ttu-id="6e875-186">この機能Teamsサポートしている場合、ユーザーはアプリの通知設定を構成できます。</span><span class="sxs-lookup"><span data-stu-id="6e875-186">If the Teams capability supports it, the users can configure notification settings for your app.</span></span>   
<span data-ttu-id="6e875-187">通知メッセージの例を次に示します。プロンプトされていないメッセージ **は送信しません**。</span><span class="sxs-lookup"><span data-stu-id="6e875-187">Following is an example of a notification message: **Don't send me unprompted messages**.</span></span>

## <a name="use-sharepoint-for-file-and-data-storage"></a><span data-ttu-id="6e875-188">ファイルSharePointストレージに使用する</span><span class="sxs-lookup"><span data-stu-id="6e875-188">Use SharePoint for file and data storage</span></span>

<span data-ttu-id="6e875-189">***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*</span><span class="sxs-lookup"><span data-stu-id="6e875-189">***Integration scenarios:** Standalone apps, collaboration apps, SharePoint pages*</span></span>

<span data-ttu-id="6e875-190">チームが作成されると、そのチーム[](/microsoftteams/sharepoint-onedrive-interact)SharePointファイルとデータ ストレージをサポートするサイト コレクションも準備されます。</span><span class="sxs-lookup"><span data-stu-id="6e875-190">When a team is created, a [SharePoint site collection](/microsoftteams/sharepoint-onedrive-interact) is also provisioned to support file and data storage for that team.</span></span> <span data-ttu-id="6e875-191">アプリがファイルを操作する場合は、この機能を活用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e875-191">Your app must leverage this feature if it interacts with files.</span></span> <span data-ttu-id="6e875-192">サイト コレクションを使用して、生データを [リスト] および [SharePoint] にExcel。</span><span class="sxs-lookup"><span data-stu-id="6e875-192">Use the site collection to store raw data in SharePoint Lists and Excel.</span></span>

## <a name="see-also"></a><span data-ttu-id="6e875-193">関連項目</span><span class="sxs-lookup"><span data-stu-id="6e875-193">See also</span></span>

[<span data-ttu-id="6e875-194">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="6e875-194">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
