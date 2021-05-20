---
author: heath-hamilton
description: 既存の Web アプリをMicrosoft Teamsと統合するためのベスト プラクティス
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Web アプリ
ms.openlocfilehash: 6783a05079f876cf3c2475a0ad5ca0e1f6687fc4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566223"
---
# <a name="web-apps"></a><span data-ttu-id="2d88f-103">Web アプリ</span><span class="sxs-lookup"><span data-stu-id="2d88f-103">Web apps</span></span> 

<span data-ttu-id="2d88f-104">web アプリをTeamsと適切に統合することで、Teamsのソーシャル機能とコラボレーション機能に適したものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-104">You can make web apps suitable with Teams' social and collaborative features, by properly integrating them with Teams.</span></span>
  
<span data-ttu-id="2d88f-105">Teamsと統合できるさまざまな種類のアプリは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2d88f-105">The different types of apps which you can integrate with Teams are as follows:</span></span>
* <span data-ttu-id="2d88f-106">**スタンドアロン アプリ**: スタンドアロン アプリは、シングル ページまたは大規模で複雑なアプリです。</span><span class="sxs-lookup"><span data-stu-id="2d88f-106">**Standalone apps**: A stand alone app is a single-page or large, and complex app.</span></span> <span data-ttu-id="2d88f-107">ユーザーは、Teamsで、その一部の側面を使用できます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-107">The user can use some aspects of it in Teams.</span></span>
* <span data-ttu-id="2d88f-108">**コラボレーションアプリ**: Teamsに固有のソーシャルおよびコラボレーション機能用に既に構築されたアプリ。</span><span class="sxs-lookup"><span data-stu-id="2d88f-108">**Collaboration apps**: An app already built for the social and collaborative features inherent to Teams.</span></span>
* <span data-ttu-id="2d88f-109">**SharePoint**: Teamsに表示するSharePointページ。</span><span class="sxs-lookup"><span data-stu-id="2d88f-109">**SharePoint**: A SharePoint page you want to surface in Teams.</span></span>

<span data-ttu-id="2d88f-110">統合シナリオに適用可能な適切なガイドラインをマップして従うことができます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-110">You can map and follow the appropriate guideline applicable to your integration scenario.</span></span>
<span data-ttu-id="2d88f-111">このドキュメントでは、Teams機能、ファイルとデータのストレージに対する共有ポイント要件、API 要件、認証、およびアプリとTeamsとのディープ リンクの概要を説明します。</span><span class="sxs-lookup"><span data-stu-id="2d88f-111">This document gives an overview of Teams capabilities, share-point requirements for file and data storage, API requirements, authentication, and deep-linking of your app with Teams.</span></span>
 
## <a name="get-to-know-teams-platform-capabilities"></a><span data-ttu-id="2d88f-112">プラットフォームの機能Teams知る</span><span class="sxs-lookup"><span data-stu-id="2d88f-112">Get to know Teams platform capabilities</span></span>

<span data-ttu-id="2d88f-113">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="2d88f-113">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="2d88f-114">Teamsアプリには、必要なコラボレーション機能と必要なコラボレーション機能が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d88f-114">Your Teams app must include required and expected collaborative features.</span></span> <span data-ttu-id="2d88f-115">アプリの統合を操作するには、開発用語Teams理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="2d88f-115">To work with app integration, it is important to familiarize with Teams development terminology.</span></span>

|<span data-ttu-id="2d88f-116">アプリの一般的な機能</span><span class="sxs-lookup"><span data-stu-id="2d88f-116">Common app features</span></span>   |<span data-ttu-id="2d88f-117">Teamsプラットフォーム機能</span><span class="sxs-lookup"><span data-stu-id="2d88f-117">Teams platform capabilities</span></span>   |
|----------|-----------|
|<span data-ttu-id="2d88f-118">埋め込みウェブページ、ホームページ、またはウェブビュー</span><span class="sxs-lookup"><span data-stu-id="2d88f-118">Embedded webpage, homepage, or webview</span></span>  |[<span data-ttu-id="2d88f-119">タブ</span><span class="sxs-lookup"><span data-stu-id="2d88f-119">Tabs</span></span>](../tabs/what-are-tabs.md)  |
|<span data-ttu-id="2d88f-120">ショートカットと拡張機能を共有する</span><span class="sxs-lookup"><span data-stu-id="2d88f-120">Share shortcuts and extensions</span></span>  |[<span data-ttu-id="2d88f-121">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="2d88f-121">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="2d88f-122">アクションのショートカットと拡張機能</span><span class="sxs-lookup"><span data-stu-id="2d88f-122">Action shortcuts and extensions</span></span>  |[<span data-ttu-id="2d88f-123">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="2d88f-123">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="2d88f-124">チャットボット</span><span class="sxs-lookup"><span data-stu-id="2d88f-124">Chatbots</span></span>  |[<span data-ttu-id="2d88f-125">ボット</span><span class="sxs-lookup"><span data-stu-id="2d88f-125">Bots</span></span>](../bots/what-are-bots.md) |
|<span data-ttu-id="2d88f-126">チャンネル通知</span><span class="sxs-lookup"><span data-stu-id="2d88f-126">Channel notifications</span></span>  |[<span data-ttu-id="2d88f-127">ボット</span><span class="sxs-lookup"><span data-stu-id="2d88f-127">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="2d88f-128">受信 Webhook</span><span class="sxs-lookup"><span data-stu-id="2d88f-128">Incoming webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[<span data-ttu-id="2d88f-129">Office 365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="2d88f-129">Office 365 Connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="2d88f-130">メッセージ外部サービス</span><span class="sxs-lookup"><span data-stu-id="2d88f-130">Message external services</span></span>  |[<span data-ttu-id="2d88f-131">ボット</span><span class="sxs-lookup"><span data-stu-id="2d88f-131">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="2d88f-132">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="2d88f-132">Outgoing webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="2d88f-133">モーダル</span><span class="sxs-lookup"><span data-stu-id="2d88f-133">Modals</span></span>  |[<span data-ttu-id="2d88f-134">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="2d88f-134">Task modules</span></span>](../task-modules-and-cards/what-are-task-modules.md)  |
|<span data-ttu-id="2d88f-135">コンテンツが豊富なカード</span><span class="sxs-lookup"><span data-stu-id="2d88f-135">Content-rich cards</span></span>  |[<span data-ttu-id="2d88f-136">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="2d88f-136">Adaptive Cards</span></span>](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a><span data-ttu-id="2d88f-137">機能のサブセットを決定する</span><span class="sxs-lookup"><span data-stu-id="2d88f-137">Determine a subset of functionality</span></span>

<span data-ttu-id="2d88f-138">\***統合シナリオ**: スタンドアロン アプリ\*</span><span class="sxs-lookup"><span data-stu-id="2d88f-138">\***Integration scenarios**: Standalone apps\*</span></span>

<span data-ttu-id="2d88f-139">既存のアプリケーションのすべての機能をTeamsに統合すると、特に大規模なアプリでは、強制的なユーザー エクスペリエンスや不自然なユーザー エクスペリエンスが実現することがよくあります。</span><span class="sxs-lookup"><span data-stu-id="2d88f-139">Integrating all features of an existing application into Teams often leads to a forced or unnatural user experience, particularly in larger apps.</span></span> <span data-ttu-id="2d88f-140">最もインパクトのある機能と、より自然にTeamsと統合する機能から始めましょう。</span><span class="sxs-lookup"><span data-stu-id="2d88f-140">Start with the most impactful features and those that integrates more naturally with Teams.</span></span> <span data-ttu-id="2d88f-141">ユーザーがメイン アプリを起動し、その機能の完全なセットにアクセスすることを許可できます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-141">You can allow users to launch the main app and access its full set of features.</span></span>

<span data-ttu-id="2d88f-142">**アプリをTeamsと統合するための前提条件** アプリをTeamsに統合するための前提条件を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2d88f-142">**Prerequisites to integrate your app with Teams** Following are the prerequisites to integrate your app with Teams.</span></span> 

1. <span data-ttu-id="2d88f-143">[アプリのユース ケースをプラットフォームの機能にTeamsマップ](../concepts/design/map-use-cases.md)する 。</span><span class="sxs-lookup"><span data-stu-id="2d88f-143">[Map your app's use cases to Teams platform capabilities](../concepts/design/map-use-cases.md).</span></span>
1. <span data-ttu-id="2d88f-144">[アプリのエントリ ポイントを決定する](../concepts/extensibility-points.md):</span><span class="sxs-lookup"><span data-stu-id="2d88f-144">[Determine your app's entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="2d88f-145">個人的な使用、共同作業、またはその両方のためですか?</span><span class="sxs-lookup"><span data-stu-id="2d88f-145">Is it for personal use, collaboration, or both?</span></span>

## <a name="understand-sharepoint-requirements-and-options"></a><span data-ttu-id="2d88f-146">SharePoint要件とオプションを理解する</span><span class="sxs-lookup"><span data-stu-id="2d88f-146">Understand SharePoint requirements and options</span></span>

<span data-ttu-id="2d88f-147">\***統合シナリオ**: SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="2d88f-147">\***Integration scenarios**: SharePoint\*</span></span>

<span data-ttu-id="2d88f-148">既存の[SharePointページ](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites)をTeamsタブとして統合するには、次の点を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d88f-148">To integrate an existing [SharePoint page](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) as a Teams tab, you must consider the following:</span></span>

* <span data-ttu-id="2d88f-149">*これは、最新* のSharePointオンラインページでなければなりません。</span><span class="sxs-lookup"><span data-stu-id="2d88f-149">It must be a *modern* SharePoint online page.</span></span>
* <span data-ttu-id="2d88f-150">個人用タブのみがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-150">Only personal tabs are supported.</span></span> <span data-ttu-id="2d88f-151">ページをチャンネル タブとして統合することはできません。</span><span class="sxs-lookup"><span data-stu-id="2d88f-151">You cannot integrate your page as a channel tab.</span></span>

<span data-ttu-id="2d88f-152">または、 SharePoint Framework を[使用して](/sharepoint/dev/spfx/integrate-with-teams-introduction)Teams タブを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-152">Alternatively, you can build a Teams tab [using the SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).</span></span>

## <a name="aim-towards-multi-tenancy"></a><span data-ttu-id="2d88f-153">マルチテナンシーを目指す</span><span class="sxs-lookup"><span data-stu-id="2d88f-153">Aim towards multi-tenancy</span></span>

<span data-ttu-id="2d88f-154">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="2d88f-154">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="2d88f-155">アプリが複数の組織で使用されている場合は、製品をスケーラブルにし、配布を大幅に簡素化するマルチテナント ホスティングを検討してください。</span><span class="sxs-lookup"><span data-stu-id="2d88f-155">If your app is used by multiple organizations, consider multi-tenant hosting that makes your product scalable and greatly simplify the distribution.</span></span>

## <a name="review-your-apis"></a><span data-ttu-id="2d88f-156">API の確認</span><span class="sxs-lookup"><span data-stu-id="2d88f-156">Review your APIs</span></span>

<span data-ttu-id="2d88f-157">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ\*</span><span class="sxs-lookup"><span data-stu-id="2d88f-157">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="2d88f-158">Teamsと統合する場合は、アプリの既存の API とデータ構造がアプリをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d88f-158">You must make your app's existing APIs and data structures support the app when integrating with Teams.</span></span> <span data-ttu-id="2d88f-159">サポートを拡張するには[、ID マッピング](../concepts/authentication/configure-identity-provider.md)、[ディープリンク サポート](../concepts/build-and-test/deep-links.md)、および Microsoft Graph の[組み込み](/graph/teams-concept-overview)Teamsに関するコンテキスト情報を使用して、API とデータ構造を拡張する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d88f-159">To extend the support, you must augment the APIs and data structures with contextual information about Teams for [identity mapping](../concepts/authentication/configure-identity-provider.md), [deep-link support](../concepts/build-and-test/deep-links.md), and [incorporating Microsoft Graph](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="2d88f-160">Teams[タブ](../tabs/how-to/access-teams-context.md)または[ボット](../bots/how-to/get-teams-context.md)のコンテキストの取得の詳細については、こちらをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2d88f-160">Learn more about getting context for your Teams [tab](../tabs/how-to/access-teams-context.md) or [bot](../bots/how-to/get-teams-context.md).</span></span>

## <a name="understand-authentication-options"></a><span data-ttu-id="2d88f-161">認証オプションについて</span><span class="sxs-lookup"><span data-stu-id="2d88f-161">Understand authentication options</span></span>

<span data-ttu-id="2d88f-162">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="2d88f-162">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="2d88f-163">Azure Active Directory (AD) は、Teamsの ID プロバイダーです。</span><span class="sxs-lookup"><span data-stu-id="2d88f-163">Azure Active Directory (AD) is the identity provider for Teams.</span></span> <span data-ttu-id="2d88f-164">アプリで別の ID プロバイダーを使用する場合は、ID マッピングの演習を行うか、Azure AD と組み合わせる必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d88f-164">If your app uses a different identity provider, you must either do an identity mapping exercise or combine with Azure AD.</span></span>

<span data-ttu-id="2d88f-165">Teamsには、サード パーティ製アプリ用の Azure AD とのシングル サインオン (SSO) メカニズムがあります。</span><span class="sxs-lookup"><span data-stu-id="2d88f-165">Teams has single sign-on (SSO) mechanisms with Azure AD for third-party apps.</span></span> <span data-ttu-id="2d88f-166">また、OIDC と呼ばれる、OAuth や Open ID Connectなどの標準を使用して、他の ID プロバイダーへの認証フローのガイダンスも提供します。</span><span class="sxs-lookup"><span data-stu-id="2d88f-166">It also provides the guidance for authentication flows to other identity providers using standards such as OAuth and Open ID Connect, known as OIDC.</span></span>

<span data-ttu-id="2d88f-167">SharePoint ページの場合、SSO のみを使用でき、ID が SharePoint アプリであるため、別のアプリで SSO を動作させたい場合は、別の Azure AD ID を追加することはできません。</span><span class="sxs-lookup"><span data-stu-id="2d88f-167">For SharePoint pages, you can only use SSO and cannot add another Azure AD ID if you want SSO to work for another app as the ID is the SharePoint app.</span></span>

<span data-ttu-id="2d88f-168">認証の詳細については[、 Teams を参照](../concepts/authentication/authentication.md)してください。</span><span class="sxs-lookup"><span data-stu-id="2d88f-168">Learn more about [authentication in Teams](../concepts/authentication/authentication.md).</span></span>

## <a name="follow-teams-design-guidelines"></a><span data-ttu-id="2d88f-169">Teams設計ガイドラインに従う</span><span class="sxs-lookup"><span data-stu-id="2d88f-169">Follow Teams design guidelines</span></span>

<span data-ttu-id="2d88f-170">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ\*</span><span class="sxs-lookup"><span data-stu-id="2d88f-170">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="2d88f-171">アプリをネイティブ[Teams Teams](../concepts/design/understand-use-cases.md)に対応するように設計ガイドラインに従ってください。</span><span class="sxs-lookup"><span data-stu-id="2d88f-171">Ensure to follow [Teams design guidelines](../concepts/design/understand-use-cases.md) to make your app native to Teams.</span></span> <span data-ttu-id="2d88f-172">既存のアプリ コンテンツをTeams タブに移行することはできません。アプリのデザインの詳細については[、「Fluent デザイン システム](https://fluentsite.z22.web.core.windows.net/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d88f-172">You cannot migrate an existing app content to a Teams tab. For more information on app design, see [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).</span></span>

## <a name="maximize-deep-linking"></a><span data-ttu-id="2d88f-173">ディープリンクを最大化</span><span class="sxs-lookup"><span data-stu-id="2d88f-173">Maximize deep linking</span></span>

<span data-ttu-id="2d88f-174">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="2d88f-174">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="2d88f-175">Teams内の情報や機能へのリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-175">You can create links to information and features within Teams.</span></span> <span data-ttu-id="2d88f-176">[ディープ リンク](../concepts/build-and-test/deep-links.md)を使用して、アプリを複数のアプリを結び付けて、よりネイティブなTeamsエクスペリエンスを提供するTeamsとリンクします。</span><span class="sxs-lookup"><span data-stu-id="2d88f-176">Use [deep links](../concepts/build-and-test/deep-links.md) to link your app with Teams as they tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="be-smart-when-messaging-users"></a><span data-ttu-id="2d88f-177">ユーザーにメッセージを送信する際にスマートにする</span><span class="sxs-lookup"><span data-stu-id="2d88f-177">Be smart when messaging users</span></span>

<span data-ttu-id="2d88f-178">\***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="2d88f-178">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="2d88f-179">[マルチ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)スレッドの会話にはTeamsアプリで[ボット](../bots/what-are-bots.md)を使用します。</span><span class="sxs-lookup"><span data-stu-id="2d88f-179">Use a [bot](../bots/what-are-bots.md) in your Teams app for multi-threaded conversation, as it offers more flexibility than a [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

<span data-ttu-id="2d88f-180">ボットを使用すると、個々のユーザーまたはチャネルに **プロアクティブなメッセージ** を送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-180">Bots also allow you to send **proactive messages** to individual users or channels.</span></span> <span data-ttu-id="2d88f-181">プロアクティブ メッセージは、外部イベントによってトリガーされるメッセージで、ボットに送信されるメッセージではありません。</span><span class="sxs-lookup"><span data-stu-id="2d88f-181">The proactive messages are unprompted messages triggered by an outside event and not a message sent to a bot.</span></span> <span data-ttu-id="2d88f-182">たとえば、ボットがインストールされるとウェルカム メッセージを送信したり、新しいユーザーがチャネルに参加したりすると、ボットからウェルカム メッセージが送信されます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-182">For example, your bot sends a welcome message when it is installed or a new user joins a channel.</span></span> 

<span data-ttu-id="2d88f-183">プロアクティブ メッセージを送信するには、Teams固有の識別子が必要です。</span><span class="sxs-lookup"><span data-stu-id="2d88f-183">Sending proactive messages requires Teams-specific identifiers.</span></span> <span data-ttu-id="2d88f-184">情報を取得するには、[名簿またはユーザー プロファイル データを取得](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)するか、[会話イベントを購読](../bots/how-to/conversations/subscribe-to-conversation-events.md)するか、または[Microsoft Graph](/graph/teams-proactive-messaging)を使用します。</span><span class="sxs-lookup"><span data-stu-id="2d88f-184">You can capture the information by [fetching roster or user profile data](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), [subscribing to conversation events](../bots/how-to/conversations/subscribe-to-conversation-events.md), or using [Microsoft Graph](/graph/teams-proactive-messaging).</span></span>

<span data-ttu-id="2d88f-185">過度のメッセージでユーザーをスパムしないでください。</span><span class="sxs-lookup"><span data-stu-id="2d88f-185">Do not spam users with excessive messages.</span></span> <span data-ttu-id="2d88f-186">Teams機能がサポートしている場合、ユーザーはアプリの通知設定を構成できます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-186">If the Teams capability supports it, the users can configure notification settings for your app.</span></span>   
<span data-ttu-id="2d88f-187">次に、通知メッセージの例を示します: **メッセージを表示しないメッセージを送信しないでください**。</span><span class="sxs-lookup"><span data-stu-id="2d88f-187">Following is an example of a notification message: **Don't send me unprompted messages**.</span></span>

## <a name="use-sharepoint-for-file-and-data-storage"></a><span data-ttu-id="2d88f-188">ファイルとデータのストレージにSharePointを使用する</span><span class="sxs-lookup"><span data-stu-id="2d88f-188">Use SharePoint for file and data storage</span></span>

<span data-ttu-id="2d88f-189">***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*</span><span class="sxs-lookup"><span data-stu-id="2d88f-189">***Integration scenarios:** Standalone apps, collaboration apps, SharePoint pages*</span></span>

<span data-ttu-id="2d88f-190">チームを作成すると、そのチームのファイルとデータの格納をサポートするために[、SharePointサイト コレクション](/microsoftteams/sharepoint-onedrive-interact)も準備されます。</span><span class="sxs-lookup"><span data-stu-id="2d88f-190">When a team is created, a [SharePoint site collection](/microsoftteams/sharepoint-onedrive-interact) is also provisioned to support file and data storage for that team.</span></span> <span data-ttu-id="2d88f-191">アプリがファイルとやり取りする場合は、この機能を利用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d88f-191">Your app must leverage this feature if it interacts with files.</span></span> <span data-ttu-id="2d88f-192">サイト コレクションを使用して、SharePoint リストとExcelに生データを格納します。</span><span class="sxs-lookup"><span data-stu-id="2d88f-192">Use the site collection to store raw data in SharePoint Lists and Excel.</span></span>

## <a name="see-also"></a><span data-ttu-id="2d88f-193">関連項目</span><span class="sxs-lookup"><span data-stu-id="2d88f-193">See also</span></span>

[<span data-ttu-id="2d88f-194">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="2d88f-194">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
