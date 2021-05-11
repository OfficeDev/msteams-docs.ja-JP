---
title: Microsoft Teamsの検証ガイドライン
description: アプリ ストア (AppSource) に送信Teamsガイドラインについて説明します。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: df60cf9e4a173186fbacacc90621c2efb23ba17f
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230926"
---
# <a name="microsoft-teams-store-validation-guidelines"></a><span data-ttu-id="4c9be-103">Microsoft Teamsの検証ガイドライン</span><span class="sxs-lookup"><span data-stu-id="4c9be-103">Microsoft Teams store validation guidelines</span></span>

<span data-ttu-id="4c9be-104">これらのガイドラインに従って、アプリがストア申請プロセスに合格するMicrosoft Teams増加します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-104">Following these guidelines increases the likelihood your app will pass the Microsoft Teams store submission process.</span></span> <span data-ttu-id="4c9be-105">これらのTeams固有のガイドライン[は、Microsoft](https://docs.microsoft.com/legal/marketplace/certification-policies)の商用マーケットプレース認定ポリシーを補完し、新機能、ユーザー フィードバック、およびビジネス ルールの変更を反映するように頻繁に更新されます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-105">These Teams-specific guidelines complement the Microsoft [commercial marketplace certification policies](https://docs.microsoft.com/legal/marketplace/certification-policies) and are updated frequently to reflect new capabilities, user feedback, and business rule changes.</span></span>

> [!NOTE]
> <span data-ttu-id="4c9be-106">一部のガイドラインは、アプリに適用できない場合があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-106">Some guidelines may not be applicable to your app.</span></span> <span data-ttu-id="4c9be-107">たとえば、アプリにボットが含まれる場合は、ボット関連のガイドラインを無視できます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-107">For example, if your app doesn't include a bot, you can ignore bot-related guidelines.</span></span>

## <a name="10-value-proposition"></a><span data-ttu-id="4c9be-108">1.0 Value proposition</span><span class="sxs-lookup"><span data-stu-id="4c9be-108">1.0 Value proposition</span></span>

### <a name="11-app-name"></a><span data-ttu-id="4c9be-109">1.1 アプリ名</span><span class="sxs-lookup"><span data-stu-id="4c9be-109">1.1 App name</span></span>

<span data-ttu-id="4c9be-110">アプリの名前は、ユーザーがストアでアプリを検出する方法において重要な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="4c9be-110">An app's name plays a critical role in how users discover it in the store.</span></span> <span data-ttu-id="4c9be-111">アプリ名については、次の情報を覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-111">Remember the following about app names:</span></span>

* <span data-ttu-id="4c9be-112">名前には、ユーザーに関連する用語が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-112">The name must include terms relevant to your users.</span></span>
* <span data-ttu-id="4c9be-113">チャット、Teams、予定表、通話、ファイル、アクティビティ **、Teams、** アプリ、ヘルプ&#8212;などのコア Teams&#8212;機能の名前は、アプリ名に含めません。     </span><span class="sxs-lookup"><span data-stu-id="4c9be-113">Names of core Teams features&#8212;such as **Chat**, **Contacts**, **Calendar**, **Calls**, **Files**, **Activity**, **Teams**, **Apps**, and **Help**&#8212;should not be included in your app name.</span></span>
* <span data-ttu-id="4c9be-114">一般的な名詞には、開発者の名前 (たとえば、タスクではなく **Contoso タスク** ) のプレフィックスまたは接尾辞が付く必要 **があります**。</span><span class="sxs-lookup"><span data-stu-id="4c9be-114">Common nouns must be prefixed or suffixed with the developer's name (for example, **Contoso Tasks** rather than **Tasks**).</span></span>
* <span data-ttu-id="4c9be-115">共同ブランド **化Teams** 共同販売を誤って示す可能性がある Microsoft 製品名または Microsoft 製品名を使用しなけれ。</span><span class="sxs-lookup"><span data-stu-id="4c9be-115">Must not use **Teams** or other Microsoft product names that could falsely indicate co-branding or co-selling.</span></span> <span data-ttu-id="4c9be-116">(Microsoft ソフトウェア、製品、サービスの参照の詳細については、「Microsoft 商標およびブランド ガイドライン [」を参照してください](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general))。</span><span class="sxs-lookup"><span data-stu-id="4c9be-116">(For more information about referencing Microsoft software, products, and services, see the [Microsoft Trademark and Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)).</span></span>
* <span data-ttu-id="4c9be-117">アプリが Microsoft との公式パートナーシップの一部である場合は、アプリの名前が最初に指定されている必要があります (たとえば **、Contoso Connector for microsoft Microsoft Teams)。**</span><span class="sxs-lookup"><span data-stu-id="4c9be-117">If your app is part of an official partnership with Microsoft, the name of your app must come first (for example, **Contoso Connector for Microsoft Teams**).</span></span>
* <span data-ttu-id="4c9be-118">ストアまたは商用マーケットプレースの他のオファーに一覧表示されているアプリの名前をコピーしなけり。</span><span class="sxs-lookup"><span data-stu-id="4c9be-118">Must not copy the name of an app listed in the store or other offer in the commercial marketplace.</span></span>
* <span data-ttu-id="4c9be-119">不適切な用語や軽蔑的な用語を含めずにしてください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-119">Must not contain profane or derogatory terms.</span></span> <span data-ttu-id="4c9be-120">また、人種的または文化的に無神経な言語を含めずに名前を付けなければならない。</span><span class="sxs-lookup"><span data-stu-id="4c9be-120">The name also must not include racially or culturally insensitive language.</span></span>
* <span data-ttu-id="4c9be-121">一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-121">Must be unique.</span></span> <span data-ttu-id="4c9be-122">たとえば、同じ名前と機能を持つ異なる地域の複数のアプリを一覧表示することはできません。</span><span class="sxs-lookup"><span data-stu-id="4c9be-122">For example, you cannot list multiple apps for different regions with the same name and functionality.</span></span>

<span data-ttu-id="4c9be-123">[「4.0 App package and store listing」も参照](#40-app-package-and-store-listing)</span><span class="sxs-lookup"><span data-stu-id="4c9be-123">See also: [4.0 App package and store listing](#40-app-package-and-store-listing)</span></span>

### <a name="12-suitable-for-workplace-consumption"></a><span data-ttu-id="4c9be-124">1.2 職場での使用に適しています</span><span class="sxs-lookup"><span data-stu-id="4c9be-124">1.2 Suitable for workplace consumption</span></span>

<span data-ttu-id="4c9be-125">アプリ コンテンツは、一般的な職場での使用に適している必要があります。また、商用マーケットプレース認定ポリシーに記載されているすべての制限に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-125">App content must be suitable for general workplace consumption and abide by all restrictions listed in the commercial marketplace certification policies.</span></span> <span data-ttu-id="4c9be-126">宗教、政治、ギャンブル、長期にわたる娯楽に関連するコンテンツは禁止されています。</span><span class="sxs-lookup"><span data-stu-id="4c9be-126">Content related to religion, politics, gambling, and prolonged entertainment is prohibited.</span></span> <span data-ttu-id="4c9be-127">詳細については、「商用マーケットプレース [認定ポリシー」を参照してください](https://docs.microsoft.com/legal/marketplace/certification-policies#10010-inappropriate-content)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-127">For more information, see the [commercial marketplace certification policies](https://docs.microsoft.com/legal/marketplace/certification-policies#10010-inappropriate-content).</span></span>

<span data-ttu-id="4c9be-128">アプリでは、グループの共同作業を容易にするか、個人の生産性を向上させるか、その両方を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-128">Your app must facilitate group collaboration, improve an individual's productivity, or both.</span></span> <span data-ttu-id="4c9be-129">チームの結合と人付き合いを目的としたアプリは、複数の参加者を対象に共同作業と設計が必要です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-129">Apps intended for team bonding and socializing must be collaborative and designed for multiple participants.</span></span> <span data-ttu-id="4c9be-130">また、これらの種類のアプリでは、大幅な時間の投資や、生産性に対する影響を知覚的に必要としない必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-130">These types of apps also should not require a substantial time investment or perceptively impact productivity.</span></span>

### <a name="13-similar-platforms-and-services"></a><span data-ttu-id="4c9be-131">1.3 類似のプラットフォームとサービス</span><span class="sxs-lookup"><span data-stu-id="4c9be-131">1.3 Similar platforms and services</span></span>

<span data-ttu-id="4c9be-132">アプリは、特定の相互運用性を提供しない限り、Teams エクスペリエンスに焦点を当て、他の同様のチャット ベースのコラボレーション プラットフォームまたはサービスの名前、アイコン、または画像を含めずに行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-132">Apps must focus on the Teams experience and not include the names, icons, or imagery of other similar chat-based collaboration platforms or services unless your app provides specific interoperability.</span></span>

### <a name="14-feature-names"></a><span data-ttu-id="4c9be-133">1.4 機能名</span><span class="sxs-lookup"><span data-stu-id="4c9be-133">1.4 Feature names</span></span>

<span data-ttu-id="4c9be-134">ボタンや他の UI テキスト内のアプリ機能名は、Teams および他の Microsoft 製品用に予約されている用語 (会議の開始、通話の開始、チャットの開始など) と競合しなけい。 </span><span class="sxs-lookup"><span data-stu-id="4c9be-134">App feature names in buttons and other UI text must not conflict with terminology reserved for Teams and other Microsoft products (for example, **Start meeting**, **Make call**, or **Start chat**).</span></span> <span data-ttu-id="4c9be-135">会議の開始ではなく Contoso 会議の開始など、これを完全に回避できない場合は、アプリ名を **含める必要があります**。</span><span class="sxs-lookup"><span data-stu-id="4c9be-135">Include your app name if you can't completely avoid this, such as **Start Contoso meeting** instead of **Start meeting**.</span></span>

## <a name="20-security"></a><span data-ttu-id="4c9be-136">2.0 セキュリティ</span><span class="sxs-lookup"><span data-stu-id="4c9be-136">2.0 Security</span></span>

### <a name="21-microsoft-365-app-compliance-program"></a><span data-ttu-id="4c9be-137">2.1 Microsoft 365 コンプライアンス プログラム</span><span class="sxs-lookup"><span data-stu-id="4c9be-137">2.1 Microsoft 365 App Compliance Program</span></span>

<span data-ttu-id="4c9be-138">アプリ[コンプライアンス Microsoft 365は](https://docs.microsoft.com/microsoft-365-app-certification/overview)、組織がアプリに関するセキュリティとコンプライアンス情報を評価してリスクを評価および管理することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="4c9be-138">The [Microsoft 365 App Compliance Program](https://docs.microsoft.com/microsoft-365-app-certification/overview) is intended to help organizations assess and manage risk by evaluating security and compliance information about your app.</span></span> <span data-ttu-id="4c9be-139">アプリをアプリ ストアに発行するTeams、プログラムの次の階層を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-139">If you're publishing an app to the Teams store, you must complete the following tiers of the program:</span></span>

* <span data-ttu-id="4c9be-140">[Publisher検証](/azure/active-directory/develop/publisher-verification-overview): 管理者とエンド ユーザーがアプリ開発者とアプリ開発者の統合の真正性を理解Microsoft ID プラットフォーム。</span><span class="sxs-lookup"><span data-stu-id="4c9be-140">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview): Helps admins and end users understand the authenticity of app developers integrating with the Microsoft identity platform.</span></span> <span data-ttu-id="4c9be-141">完了すると、青い "検証済み" バッジが Azure Active Directory (Azure AD) の同意ダイアログや他の画面に表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-141">When completed, a blue "verified" badge displays on the Azure Active Directory (Azure AD) consent dialog and other screens.</span></span> <span data-ttu-id="4c9be-142">詳細については、「よく寄せられる質問[」、](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)アプリを[](/azure/active-directory/develop/mark-app-as-publisher-verified)発行元の検証済みとしてマークする方法、および発行元の検証の[トラブルシューティングを参照してください](/azure/active-directory/develop/troubleshoot-publisher-verification)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-142">For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>
* <span data-ttu-id="4c9be-143">[Publisher構成](/microsoft-365-app-certification/docs/attestation)証明: 一般情報、データ処理情報、セキュリティ情報、コンプライアンス情報を共有して、潜在的な顧客がアプリの使用に関する情報に基づいた意思決定を行う際に役立つプロセス。</span><span class="sxs-lookup"><span data-stu-id="4c9be-143">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation): A process in which you share general, data handling, and security and compliance information to help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="4c9be-144">以前に一覧に記載されていないアプリを提出する場合は、アプリが Teams ストアに保存されるまで、Publisher 構成証明を正式に完了Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-144">If you're submitting an app that hasn't been listed previously, you can't officially complete Publisher Attestation until your app is in the Teams store.</span></span> <span data-ttu-id="4c9be-145">リストされているアプリを更新する場合は、最新Publisher提出する前に、構成証明を完了してください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-145">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app.</span></span>

### <a name="22-bots"></a><span data-ttu-id="4c9be-146">2.2 ボット</span><span class="sxs-lookup"><span data-stu-id="4c9be-146">2.2 Bots</span></span>

<span data-ttu-id="4c9be-147">Microsoft Azure ボット サービス (ボットやメッセージング拡張機能など) を使用するアプリの場合は、Microsoft Online Services Terms で定義されている要件に従う[必要があります](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-147">For apps that use the Microsoft Azure Bot Service (such as bots and messaging extensions), you must follow all requirements defined in the Microsoft [Online Services Terms](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).</span></span>

<span data-ttu-id="4c9be-148">ボットは常に、ファイルをアップロードするためのアクセス許可を求め、ファイルのアップロード後に確認メッセージを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-148">Bots must always ask permission to upload a file and display a confirmation message after the file uploads.</span></span>

### <a name="23-external-domains"></a><span data-ttu-id="4c9be-149">2.3 外部ドメイン</span><span class="sxs-lookup"><span data-stu-id="4c9be-149">2.3 External domains</span></span>

<span data-ttu-id="4c9be-150">ほとんどの場合、組織の制御外のドメイン (ワイルドカードを含む) およびトンネリング サービスをアプリのドメイン構成に含めずにいなければならない。</span><span class="sxs-lookup"><span data-stu-id="4c9be-150">In most cases, you must not include domains outside of your organization's control (including wildcards) and tunneling services in your app's domain configurations.</span></span> <span data-ttu-id="4c9be-151">次の例外が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-151">The following exceptions include:</span></span>

* <span data-ttu-id="4c9be-152">アプリで Azure Bot Service の OAuthCard を使用する場合は、有効なドメインとして含める必要があります。または [サインイン] `token.botframework.com` ボタンが機能しません。 </span><span class="sxs-lookup"><span data-stu-id="4c9be-152">If your app uses the Azure Bot Service's OAuthCard, you must include `token.botframework.com` as a valid domain or the **Sign in** button won't work.</span></span>
* <span data-ttu-id="4c9be-153">アプリがサイトに依存しているSharePoint、context プロパティを使用して、関連付けられたルート SharePointを有効なドメイン `{teamSiteDomain}` として含めできます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-153">If your app relies on SharePoint, you can include the associated root SharePoint site as a valid domain using the `{teamSiteDomain}` context property.</span></span>

### <a name="24-authentication"></a><span data-ttu-id="4c9be-154">2.4 認証</span><span class="sxs-lookup"><span data-stu-id="4c9be-154">2.4 Authentication</span></span>

<span data-ttu-id="4c9be-155">アプリ認証を実装する方法については、「アプリ認証」を参照[Teams。](~/concepts/authentication/authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4c9be-155">For information on how to implement app authentication, see [authentication in Teams](~/concepts/authentication/authentication.md).</span></span>

#### <a name="241-authenticating-with-external-services"></a><span data-ttu-id="4c9be-156">2.4.1 外部サービスでの認証</span><span class="sxs-lookup"><span data-stu-id="4c9be-156">2.4.1 Authenticating with external services</span></span>

<span data-ttu-id="4c9be-157">アプリが外部サービスを使用してユーザーを認証する場合は、次のことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-157">Remember the following if your app authenticates users with an external service.</span></span>

* <span data-ttu-id="4c9be-158">**サインイン、サインアウト、およびサインアップ エクスペリエンス**:</span><span class="sxs-lookup"><span data-stu-id="4c9be-158">**Sign in, sign out, and sign up experiences**:</span></span>
  * <span data-ttu-id="4c9be-159">外部アカウントまたはサービスに依存するアプリは、明確で簡単なサインイン、サインアウト、サインアップエクスペリエンスを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-159">Apps that depend on external accounts or services must provide clear and simple sign in, sign out, and sign up experiences.</span></span>
  * <span data-ttu-id="4c9be-160">ユーザーがサインアウトする場合は、アプリからのみサインアウトし、アプリにサインインTeams。</span><span class="sxs-lookup"><span data-stu-id="4c9be-160">When a user signs out, they must sign out only from the app and remain signed in to Teams.</span></span>
* <span data-ttu-id="4c9be-161">コンテンツ **共有エクスペリエンス**: Teams チャネルでコンテンツを共有するために外部サービスとの認証を必要とするアプリは、その機能が外部サービスでサポートされている場合、コンテンツを切断または共有解除する方法をヘルプ ドキュメント (または類似のリソース) で明確に示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-161">**Content sharing experiences**: Apps that require authentication with an external service to share content in Teams channels must clearly state in help documentation (or similar resources) how to disconnect or unshare content if that feature is supported on the external service.</span></span> <span data-ttu-id="4c9be-162">これは、コンテンツの共有を解除する機能がアプリ内に存在するTeamsではありません。</span><span class="sxs-lookup"><span data-stu-id="4c9be-162">This does not mean the ability to unshare content must be present in your Teams app.</span></span>

#### <a name="242-government-community-cloud-listings"></a><span data-ttu-id="4c9be-163">2.4.2 Government Community Cloudリスト</span><span class="sxs-lookup"><span data-stu-id="4c9be-163">2.4.2 Government Community Cloud listings</span></span>

<span data-ttu-id="4c9be-164">Teams ストアで重複するリストを避けながらアプリを Government Community Cloud (GCC) ユーザーに配布するには、認証プロセスでユーザーを特定し、GCC 固有または予期される URL にルーティングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-164">To distribute your app to Government Community Cloud (GCC) users while avoiding duplicate listings in the Teams store, the authentication process must identify and route users to a GCC-specific or expected URL.</span></span>

### <a name="25-sensitive-content"></a><span data-ttu-id="4c9be-165">2.5 機密性の高いコンテンツ</span><span class="sxs-lookup"><span data-stu-id="4c9be-165">2.5 Sensitive content</span></span>

<span data-ttu-id="4c9be-166">アプリは、クレジット カードや金融支払い手段のデータなどの機密データを投稿しなけり。</span><span class="sxs-lookup"><span data-stu-id="4c9be-166">Your app must not post sensitive data, such as credit card or financial payment instrument data.</span></span> <span data-ttu-id="4c9be-167">また、アプリは、そのコンテンツを表示することを意図していない対象ユーザーに対して、正常性、連絡先トレース、または他の個人を特定できる情報 (PII) を表示しなけらね。</span><span class="sxs-lookup"><span data-stu-id="4c9be-167">The app also must not display health, contact tracing, or other personally identifiable information (PII) to an audience not intended to view that content.</span></span>

<span data-ttu-id="4c9be-168">アプリがファイルまたは実行可能ファイル (.exe) をユーザーのコンピューターまたは環境にダウンロードする前に、ユーザーに警告します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-168">Warn users before your app downloads any files or executables (.exe) into the user's machine or environment.</span></span>

### <a name="26-financial-information"></a><span data-ttu-id="4c9be-169">2.6 財務情報</span><span class="sxs-lookup"><span data-stu-id="4c9be-169">2.6 Financial information</span></span>

<span data-ttu-id="4c9be-170">アプリは、ユーザーに対して、アプリ インターフェイス内で支払いをTeamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-170">Apps must not ask users to make payments within the Teams interface.</span></span> <span data-ttu-id="4c9be-171">ボット インターフェイスを介してユーザーに金融商品の詳細を送信しなけり。</span><span class="sxs-lookup"><span data-stu-id="4c9be-171">Financial instrument details must not be transmitted to users through a bot interface.</span></span>

<span data-ttu-id="4c9be-172">ユーザーがアプリの使用に同意する前に、使用条件、プライバシー ポリシー、またはプロファイル ページまたは Web サイトで適切な開示を行った場合にのみ、セキュリティで保護された外部支払いサービスにリンクできます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-172">You may link to secure, external payment services only if you made the appropriate disclosure in your terms of use, privacy policy, or any profile page or website before the user agreed to use the app.</span></span>

<span data-ttu-id="4c9be-173">iOS または Android バージョンのアプリで実行Teamsガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-173">Apps running on the iOS or Android version of Teams must adhere to the following guidelines:</span></span>

* <span data-ttu-id="4c9be-174">アプリには、有料版へのアップセルを目的としたアプリ内購入、試用オファー、または UI を含めず、ユーザーが他のコンテンツ、アプリ、アドインを購入または取得できるオンライン ストアへのリンクを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-174">Apps must not include in-app purchases, trial offers, or UI that aims to upsell to paid versions or links to online stores where users can purchase or acquire other content, apps, or add-ins.</span></span>
* <span data-ttu-id="4c9be-175">アプリでアカウントが必要な場合、ユーザーは無料でアカウントにサインアップできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-175">If your app requires an account, users must be able to sign up for an account at no charge.</span></span> <span data-ttu-id="4c9be-176">無料または無料のアカウント **という用語** の **使用** は禁止されています。</span><span class="sxs-lookup"><span data-stu-id="4c9be-176">The use of the term **free** or **free account** is prohibited.</span></span>
* <span data-ttu-id="4c9be-177">アカウントが無期限または期間限定でアクティブかどうかを判断できますが、アカウントの有効期限が切れた場合は、支払う必要を示す UI、テキスト、またはリンクが表示されない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-177">You may determine whether an account is active indefinitely or for a limited time, but if the account expires, no UI, text, or links indicating the need to pay may be shown.</span></span>
* <span data-ttu-id="4c9be-178">アプリのプライバシー ポリシーと使用条件ページは、コマース関連の UI またはリンクを含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-178">Your app's privacy policy and terms of use pages must be free of any commerce-related UI or links.</span></span>

## <a name="30-general-functionality-and-performance"></a><span data-ttu-id="4c9be-179">3.0 一般的な機能とパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="4c9be-179">3.0 General functionality and performance</span></span>

### <a name="31-launching-external-functionality"></a><span data-ttu-id="4c9be-180">3.1 外部機能の起動</span><span class="sxs-lookup"><span data-stu-id="4c9be-180">3.1 Launching external functionality</span></span>

<span data-ttu-id="4c9be-181">アプリは、コア ユーザー シナリオでユーザーをTeamsを取り出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-181">Apps must not take users out of Teams for core user scenarios.</span></span> <span data-ttu-id="4c9be-182">アプリのコンテンツと操作は、ボットTeamsタスク モジュールなど、ユーザーの機能内で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-182">App content and interactions can occur within Teams capabilities, such as bots, cards, and task modules.</span></span>

<span data-ttu-id="4c9be-183">外部サイトやアプリではなく、Teamsのどこかにユーザーをリンクする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-183">You should link users somewhere in Teams and not to an external site or app.</span></span> <span data-ttu-id="4c9be-184">外部機能が必要なシナリオでは、アプリに、その機能を起動するための明示的なユーザーアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-184">For scenarios that require external functionality, your app must have explicit user permission to launch that functionality.</span></span>

### <a name="32-compatibility"></a><span data-ttu-id="4c9be-185">3.2 互換性</span><span class="sxs-lookup"><span data-stu-id="4c9be-185">3.2 Compatibility</span></span>

<span data-ttu-id="4c9be-186">アプリは、次のオペレーティング システムとブラウザーで完全に機能している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-186">Apps must be fully functional on the following operating systems and browsers:</span></span>

* <span data-ttu-id="4c9be-187">Microsoft Windows 7 以降</span><span class="sxs-lookup"><span data-stu-id="4c9be-187">Microsoft Windows 7 and later</span></span>
* <span data-ttu-id="4c9be-188">macOS 10.10 以降</span><span class="sxs-lookup"><span data-stu-id="4c9be-188">macOS 10.10 and later</span></span>
* <span data-ttu-id="4c9be-189">Microsoft Edge 12 以降</span><span class="sxs-lookup"><span data-stu-id="4c9be-189">Microsoft Edge 12 and later</span></span>
* <span data-ttu-id="4c9be-190">Mozilla Firefox 47.0 以降</span><span class="sxs-lookup"><span data-stu-id="4c9be-190">Mozilla Firefox 47.0 and later</span></span>
* <span data-ttu-id="4c9be-191">Google Chrome 51.0 以降</span><span class="sxs-lookup"><span data-stu-id="4c9be-191">Google Chrome 51.0 and later</span></span>
* <span data-ttu-id="4c9be-192">iOS 9.0 以降</span><span class="sxs-lookup"><span data-stu-id="4c9be-192">iOS 9.0 and later</span></span>
* <span data-ttu-id="4c9be-193">Android 4.4 以降</span><span class="sxs-lookup"><span data-stu-id="4c9be-193">Android 4.4 and later</span></span>

### <a name="33-response-time"></a><span data-ttu-id="4c9be-194">3.3 応答時間</span><span class="sxs-lookup"><span data-stu-id="4c9be-194">3.3 Response time</span></span>

<span data-ttu-id="4c9be-195">Teamsは、機能によって異なる妥当な時間枠内に対応する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-195">Teams apps must respond within a reasonable timeframe, which varies depending on the capability.</span></span>

* <span data-ttu-id="4c9be-196">タブは 3 秒以内に応答するか、読み込みメッセージまたは警告を表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-196">Tabs must respond within three seconds or display a loading message or warning.</span></span>
* <span data-ttu-id="4c9be-197">ボットは、2 秒以内にユーザー コマンドに応答するか、入力インジケーターを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-197">Bots must respond to user commands within two seconds or display a typing indicator.</span></span>
* <span data-ttu-id="4c9be-198">メッセージング拡張機能は、5 秒以内にユーザー コマンドに応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-198">Messaging extensions must respond to user commands within five seconds.</span></span>
* <span data-ttu-id="4c9be-199">通知は、ユーザー操作から 5 秒以内に表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-199">Notifications must display within five seconds of the user action.</span></span>

## <a name="40-app-package-and-store-listing"></a><span data-ttu-id="4c9be-200">4.0 アプリ パッケージとストアの一覧</span><span class="sxs-lookup"><span data-stu-id="4c9be-200">4.0 App package and store listing</span></span>

<span data-ttu-id="4c9be-201">アプリ パッケージは正しく書式設定され、必要なすべての情報とコンポーネントが含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-201">App packages must be correctly formatted and include all required information and components.</span></span>

### <a name="41-app-manifest"></a><span data-ttu-id="4c9be-202">4.1 アプリ マニフェスト</span><span class="sxs-lookup"><span data-stu-id="4c9be-202">4.1 App manifest</span></span>

<span data-ttu-id="4c9be-203">アプリ マニフェストTeams、アプリの構成を定義します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-203">The Teams app manifest defines your app's configurations.</span></span>

* <span data-ttu-id="4c9be-204">マニフェストは、最新のマニフェスト スキーマに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-204">Your manifest must conform to the latest manifest schema.</span></span> <span data-ttu-id="4c9be-205">詳細については、マニフェスト参照 [を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-205">For information, see the [manifest reference](~/resources/schema/manifest-schema.md).</span></span>
* <span data-ttu-id="4c9be-206">アプリにボットまたはメッセージング拡張機能が含まれる場合、マニフェストはボット名、ロゴ、プライバシー ポリシー リンク、サービス条件リンクなどの Bot Framework メタデータと一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-206">If your app includes a bot or messaging extension, your manifest must be consistent with Bot Framework metadata, including bot name, logo, privacy policy link, and terms of service link.</span></span>
* <span data-ttu-id="4c9be-207">アプリで認証に Azure Active Directory (Azure AD) を使用する場合は、マニフェストに Azure AD アプリケーション (クライアント) ID を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-207">If your app uses Azure Active Directory (Azure AD) for authentication, include the Azure AD Application (client) ID in the manifest.</span></span> <span data-ttu-id="4c9be-208">詳細については、「マニフェストリファレンス」 [を参照してください](~/resources/schema/manifest-schema.md#webapplicationinfo)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-208">For more information, see the [manifest reference](~/resources/schema/manifest-schema.md#webapplicationinfo).</span></span>

### <a name="42-app-icons"></a><span data-ttu-id="4c9be-209">4.2 アプリのアイコン</span><span class="sxs-lookup"><span data-stu-id="4c9be-209">4.2 App icons</span></span>

<span data-ttu-id="4c9be-210">アイコンは、ユーザーがストアを閲覧するときに表示される主なTeamsです。</span><span class="sxs-lookup"><span data-stu-id="4c9be-210">Icons are one of the main elements people see when browsing the Teams store.</span></span> <span data-ttu-id="4c9be-211">アイコンは、アプリのブランドと目的を伝え、次の要件にも準拠する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-211">Your icons should communicate your app's brand and purpose while also adhering to the following requirements:</span></span>

* <span data-ttu-id="4c9be-212">アプリ パッケージには、2 つの PNG バージョンのアプリ アイコン (色アイコンとアウトライン アイコン) が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-212">Your app package must include two PNG versions of your app icon: A color icon and an outline icon.</span></span>
* <span data-ttu-id="4c9be-213">アイコンの色バージョンは、ほとんどのシナリオで表示Teams 192x192 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-213">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="4c9be-214">アイコン 記号 (96x96 ピクセル) は、任意の色または色を指定できますが、単色または完全に透明な四角形の背景に位置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-214">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>
* <span data-ttu-id="4c9be-215">アイコンのアウトライン バージョンは、アプリが使用され、Teams の左側のアプリ バーに "起重" され、ユーザーがアプリのメッセージング拡張機能をピンで固定するときに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-215">The outline version of your icon displays when your app is in use and “hoisted” on the app bar on the left side of Teams and when a user pins your app's messaging extension.</span></span> <span data-ttu-id="4c9be-216">32x32 ピクセルで、透明な背景を持つ白、または白い背景を持つ透明な色を指定できます (他の色は使用できません)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-216">It must be 32x32 pixels and can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="4c9be-217">アイコンには、シンボルの周囲に余分なパディングを配置する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4c9be-217">The icon should not have any extra padding around the symbol.</span></span>
* <span data-ttu-id="4c9be-218">適切なサイズと書式設定されたアイコンは、アプリ パッケージに含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-218">Correctly sized and formatted icons must be included in your app package.</span></span> <span data-ttu-id="4c9be-219">また、アイコンは、ストア登録情報のメタデータと送信された情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-219">The icons also must match what's submitted with the store listing metadata.</span></span>

<span data-ttu-id="4c9be-220">詳細、ベスト プラクティス、および例については、「アプリ アイコンのガイドラインTeams[を参照してください](~/concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-220">For more information, best practices, and examples, see the Teams app [icon guidelines](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="43-app-descriptions"></a><span data-ttu-id="4c9be-221">4.3 アプリの説明</span><span class="sxs-lookup"><span data-stu-id="4c9be-221">4.3 App descriptions</span></span>

<span data-ttu-id="4c9be-222">アプリの短い説明と長い説明が必要です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-222">You must have a short and long description of your app.</span></span> <span data-ttu-id="4c9be-223">アプリ構成とパートナー センターの説明は同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-223">The descriptions in your app configurations and Partner Center must be the same.</span></span>

<span data-ttu-id="4c9be-224">説明は、直接またはインシニュエーションを通じて、別のブランド (Microsoft が所有している、またはそれ以外の場合) を切り離す必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-224">Descriptions should not directly or through insinuation disparage another brand (Microsoft owned or otherwise).</span></span> <span data-ttu-id="4c9be-225">説明に、実証できないクレームが含されていないことを確認します (たとえば、「効率を 200% 向上させる」など)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-225">Make sure your description does not include claims that can't be substantiated (for example, "Guaranteed 200 percent increase in efficiency").</span></span>

#### <a name="431-short-description"></a><span data-ttu-id="4c9be-226">4.3.1 簡単な説明</span><span class="sxs-lookup"><span data-stu-id="4c9be-226">4.3.1 Short description</span></span>

<span data-ttu-id="4c9be-227">簡単な説明は、アプリの価値提案を強調し、ターゲットユーザーに向けられた簡潔な要約です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-227">A short description is a concise summary of your app that highlights its value proposition and is directed at your target audience.</span></span>

<span data-ttu-id="4c9be-228">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="4c9be-228">**Do:**</span></span>

* <span data-ttu-id="4c9be-229">短い説明を 1 つの文に保つ。</span><span class="sxs-lookup"><span data-stu-id="4c9be-229">Keep the short description to one sentence.</span></span>
* <span data-ttu-id="4c9be-230">最も重要な情報を最初に説明します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-230">Put the most important information first.</span></span>
* <span data-ttu-id="4c9be-231">顧客が検索する可能性が高いキーワードを含める。</span><span class="sxs-lookup"><span data-stu-id="4c9be-231">Include keywords that customers are likely to search for.</span></span>

<span data-ttu-id="4c9be-232">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="4c9be-232">**Don't:**</span></span>

* <span data-ttu-id="4c9be-233">アプリ名を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-233">Repeat your app name.</span></span>
* <span data-ttu-id="4c9be-234">簡単な説明で **アプリ** という単語を使用します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-234">Use the word **app** in the short description.</span></span>

#### <a name="432-long-description"></a><span data-ttu-id="4c9be-235">4.3.2 詳細</span><span class="sxs-lookup"><span data-stu-id="4c9be-235">4.3.2 Long description</span></span>

<span data-ttu-id="4c9be-236">長い説明では、アプリの価値提案、主要な対象ユーザー、ターゲット業界を強調する魅力的なストーリーを提供できます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-236">The long description can provide an engaging narrative that highlights your app's value proposition, primary audience, and target industry.</span></span> <span data-ttu-id="4c9be-237">この説明は 4,000 文字までですが、ほとんどのユーザーは 300 ~ 500 語しか読み取りできません。</span><span class="sxs-lookup"><span data-stu-id="4c9be-237">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

<span data-ttu-id="4c9be-238">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="4c9be-238">**Do:**</span></span>

* <span data-ttu-id="4c9be-239">Markdown [を使用して](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) 説明の書式を設定します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-239">Use [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) to format your description.</span></span>
* <span data-ttu-id="4c9be-240">アクティブな音声を使用し、ユーザーに直接話します (たとえば *、..)。*</span><span class="sxs-lookup"><span data-stu-id="4c9be-240">Use active voice and speak to users directly (for example, *You can ...*).</span></span>
* <span data-ttu-id="4c9be-241">説明を簡単にスキャンするために、箇条書きポイントを含む機能を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-241">List features with bullet points so it's easier to scan the description.</span></span>
* <span data-ttu-id="4c9be-242">ユーザーがアプリをインストールする前に、リストと関連資料に記載されている機能、機能、成果物に対する制限、条件、または例外を明確に説明します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-242">Clearly describe limitations, conditions, or exceptions to the functionality, features, and deliverables described in the listing and related materials before the user installs your app.</span></span> <span data-ttu-id="4c9be-243">アプリTeams機能は、リストで説明するコア機能に関連している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-243">The Teams capabilities your app supports must relate to the core functions your listing describes.</span></span>
* <span data-ttu-id="4c9be-244">ヘルプまたはサポート リンクを含める。</span><span class="sxs-lookup"><span data-stu-id="4c9be-244">Include a help or support link.</span></span>
* <span data-ttu-id="4c9be-245">代わりに **Microsoft 365** を参照 **Office 365。**</span><span class="sxs-lookup"><span data-stu-id="4c9be-245">Refer to **Microsoft 365** instead of **Office 365**.</span></span>
* <span data-ttu-id="4c9be-246">ファイルを参照する必要がある **場合Teams** 最初の参照を "Microsoft Teams"**とMicrosoft Teams。**</span><span class="sxs-lookup"><span data-stu-id="4c9be-246">If you need to reference **Teams**, write the first reference as **Microsoft Teams**.</span></span> <span data-ttu-id="4c9be-247">後続の参照は、次の参照に **短縮Teams。**</span><span class="sxs-lookup"><span data-stu-id="4c9be-247">Subsequent references can be shortened to **Teams**.</span></span>
* <span data-ttu-id="4c9be-248">アプリとアプリの動作を説明する場合は、次の言語を使用Teams (またはMicrosoft 365)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-248">Use the following language when describing how the app works with Teams (or Microsoft 365):</span></span>
  * <span data-ttu-id="4c9be-249">"...を使用Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="4c9be-249">"... works with Microsoft Teams."</span></span>
  * <span data-ttu-id="4c9be-250">"...を操作Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="4c9be-250">"... working with Microsoft Teams."</span></span>
  * <span data-ttu-id="4c9be-251">"...内Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="4c9be-251">"... within Microsoft Teams."</span></span>
  * <span data-ttu-id="4c9be-252">"...for Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="4c9be-252">"... for Microsoft Teams."</span></span>

<span data-ttu-id="4c9be-253">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="4c9be-253">**Don't:**</span></span>

* <span data-ttu-id="4c9be-254">500 単語を超える。</span><span class="sxs-lookup"><span data-stu-id="4c9be-254">Exceed 500 words.</span></span>
* <span data-ttu-id="4c9be-255">Microsoft を **MS** または **MSFT** と **略します**。</span><span class="sxs-lookup"><span data-stu-id="4c9be-255">Abbreviate **Microsoft** as **MS** or **MSFT**.</span></span>
* <span data-ttu-id="4c9be-256">Microsoft のスローガンやタグラインの使用を含め、アプリが Microsoft からのオファリングである場合を示します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-256">Indicate the app is an offering from Microsoft, including using Microsoft slogans or taglines.</span></span>
* <span data-ttu-id="4c9be-257">所有しない著作権で保護されたブランド名を使用します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-257">Use copyrighted brand names you don't own.</span></span>
* <span data-ttu-id="4c9be-258">入力ミス、文法上のエラー、不要な大文字を含める (たとえば、**ユーザー** ではなく **ユーザー)。**</span><span class="sxs-lookup"><span data-stu-id="4c9be-258">Include typos, grammatical errors, and unnecessary capitalizations (for example, **Users** instead of **users**).</span></span>
* <span data-ttu-id="4c9be-259">AppSource へのリンクを含める。</span><span class="sxs-lookup"><span data-stu-id="4c9be-259">Include links to AppSource.</span></span>
* <span data-ttu-id="4c9be-260">認定された Microsoft パートナーである場合を限り、次の言語を使用します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-260">Use the following language unless you are a certified Microsoft partner:</span></span>
  * <span data-ttu-id="4c9be-261">"...と統合Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="4c9be-261">"... integrated with Microsoft Teams"</span></span>
  * <span data-ttu-id="4c9be-262">"...と統合されます。."</span><span class="sxs-lookup"><span data-stu-id="4c9be-262">"... integrates with ..."</span></span>
  * <span data-ttu-id="4c9be-263">"......" 用に構築されています。</span><span class="sxs-lookup"><span data-stu-id="4c9be-263">"... built for ..."</span></span>
  * <span data-ttu-id="4c9be-264">"...に構築されています。."</span><span class="sxs-lookup"><span data-stu-id="4c9be-264">"... built on ..."</span></span>
  * <span data-ttu-id="4c9be-265">"...で実行されます。."</span><span class="sxs-lookup"><span data-stu-id="4c9be-265">"... runs on ..."</span></span>
  * <span data-ttu-id="4c9be-266">"...によって有効になります。."</span><span class="sxs-lookup"><span data-stu-id="4c9be-266">"... enabled by ..."</span></span>
  * <span data-ttu-id="4c9be-267">"...の認定を受けています。</span><span class="sxs-lookup"><span data-stu-id="4c9be-267">"... certified for ..."</span></span>
  * <span data-ttu-id="4c9be-268">".....用に開発されました。</span><span class="sxs-lookup"><span data-stu-id="4c9be-268">"... developed for ..."</span></span>
  * <span data-ttu-id="4c9be-269">"......" 用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="4c9be-269">"... designed for ..."</span></span>

### <a name="44-screenshots"></a><span data-ttu-id="4c9be-270">4.4 スクリーンショット</span><span class="sxs-lookup"><span data-stu-id="4c9be-270">4.4 Screenshots</span></span>

<span data-ttu-id="4c9be-271">スクリーンショットは、アプリ名、アイコン、説明を補完するアプリの目立つ視覚的なプレビューを提供します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-271">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span> <span data-ttu-id="4c9be-272">スクリーンショットについては、次の情報を覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-272">Remember the following about screenshots:</span></span>

* <span data-ttu-id="4c9be-273">リストごとに最大 5 つのスクリーンショットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-273">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="4c9be-274">サポートされているファイルの種類には、PNG、JPEG、GIF が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-274">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="4c9be-275">ディメンションは 1366x768 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-275">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="4c9be-276">最大サイズは 1,024 KB です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-276">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="4c9be-277">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="4c9be-277">**Do:**</span></span>

* <span data-ttu-id="4c9be-278">アプリの機能 (ユーザーがボットと通信する方法など) に集中します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-278">Focus on your app's capabilities (for example, how people can communicate with your bot).</span></span>
* <span data-ttu-id="4c9be-279">アプリを正確に表すコンテンツを含める。</span><span class="sxs-lookup"><span data-stu-id="4c9be-279">Include content that accurately represents your app.</span></span>
* <span data-ttu-id="4c9be-280">テキストを十分に使用します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-280">Use text judiciously.</span></span>
* <span data-ttu-id="4c9be-281">ブランドを反映し、マーケティング コンテンツを含む色でスクリーンショットをフレーム化します [。Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) のリストの例と同様です (ディメンション要件は、スクリーンショットではなく画像全体に適用されます)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-281">Frame screenshots with a color that reflects your brand and include marketing content, similar to the [Freshdesk listing](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) example (dimension requirements apply to the whole image and not just the screenshot).</span></span>

<span data-ttu-id="4c9be-282">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="4c9be-282">**Don't:**</span></span>

* <span data-ttu-id="4c9be-283">電話やノート PC などの特定のデバイスを表示します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-283">Show specific devices, such as phones or laptops.</span></span>
* <span data-ttu-id="4c9be-284">アプリに表示されていないクロムまたは UI を表示します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-284">Display chrome or UI that isn't in your app.</span></span>
* <span data-ttu-id="4c9be-285">スクリーンショットにTeamsまたはブラウザーの UI をキャプチャします。</span><span class="sxs-lookup"><span data-stu-id="4c9be-285">Capture any Teams or browser UI in your screenshots.</span></span>
* <span data-ttu-id="4c9be-286">アプリの実際の UI を不正確に反映するモックアップ (アプリがアプリの外部で使用されているTeams。</span><span class="sxs-lookup"><span data-stu-id="4c9be-286">Include mockups that inaccurately reflect your app's actual UI, such as showing your app being used outside of Teams.</span></span>

> [!TIP]
> <span data-ttu-id="4c9be-287">ビデオは、ユーザーがアプリを使用する理由を伝える最も効果的な方法です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-287">A video can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="4c9be-288">ビデオは、ユーザーがリストに最初に表示する機能です (既定では、スクリーンショットの前にビデオが表示されます)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-288">A video also is the first thing users see in your listing (by default, a video displays before screenshots).</span></span> <span data-ttu-id="4c9be-289">詳細については、「ストア登録 [情報のビデオを作成する」を参照してください](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-289">For more information, see [create a video for your store listing](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video).</span></span>

### <a name="45-privacy-policy"></a><span data-ttu-id="4c9be-290">4.5 プライバシー ポリシー</span><span class="sxs-lookup"><span data-stu-id="4c9be-290">4.5 Privacy policy</span></span>

<span data-ttu-id="4c9be-291">プライバシー ポリシーは、お客様のアプリまたはTeamsサービスの全体的なポリシーに固有の場合があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-291">The privacy policy can be specific to your Teams app or an overall policy for all of your services.</span></span>

* <span data-ttu-id="4c9be-292">一般的なプライバシー ポリシー テンプレートを使用する場合は、サービス、アプリケーション、およびプラットフォームを参照して、Teamsサービスまたは Web サイトを含める必要があります。 </span><span class="sxs-lookup"><span data-stu-id="4c9be-292">If you use a generic privacy policy template, you must reference **services**, **applications**, and **platforms** to include your Teams app and your service or website.</span></span>
* <span data-ttu-id="4c9be-293">ユーザー データの保存、保持、および削除の処理方法を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-293">Must include how you handle user data storage, retention, and deletion.</span></span> <span data-ttu-id="4c9be-294">また、データ保護に使用するセキュリティ制御について説明する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-294">You also must describe the security controls you use for data protection.</span></span>
* <span data-ttu-id="4c9be-295">連絡先情報を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-295">Must include your contact information.</span></span>
* <span data-ttu-id="4c9be-296">壊れている URL やベータ版またはステージング用の URL を含めずにしてください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-296">Should not contain URLs that are broken or for beta or staging purposes.</span></span>
* <span data-ttu-id="4c9be-297">AppSource へのリンクは含めずにしてください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-297">Must not include links to AppSource.</span></span>

### <a name="46-terms-of-use"></a><span data-ttu-id="4c9be-298">4.6 利用規約</span><span class="sxs-lookup"><span data-stu-id="4c9be-298">4.6 Terms of use</span></span>

<span data-ttu-id="4c9be-299">ご利用条件は、お客様の提供に固有で適用可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-299">Your terms of use should be specific and applicable to your offering.</span></span>

### <a name="47-support-links"></a><span data-ttu-id="4c9be-300">4.7 サポート リンク</span><span class="sxs-lookup"><span data-stu-id="4c9be-300">4.7 Support links</span></span>

<span data-ttu-id="4c9be-301">アプリのサポート URL は認証を必要としない必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-301">Your app's support URLs should not require authentication.</span></span> <span data-ttu-id="4c9be-302">たとえば、ユーザーがログインして連絡する必要はないとします。</span><span class="sxs-lookup"><span data-stu-id="4c9be-302">For example, users should not have to log in to contact you.</span></span>

### <a name="48-localization"></a><span data-ttu-id="4c9be-303">4.8 ローカライズ</span><span class="sxs-lookup"><span data-stu-id="4c9be-303">4.8 Localization</span></span>

<span data-ttu-id="4c9be-304">アプリでローカライズがサポートされている場合、アプリ パッケージには、言語の設定に基づいて表示される言語翻訳を含むTeams必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-304">If your app supports localization, your app package must include a file with language translations that display based on the Teams language setting.</span></span> <span data-ttu-id="4c9be-305">ファイルは、ローカライズ スキーマのTeamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-305">The file must conform to the Teams localization schema.</span></span> <span data-ttu-id="4c9be-306">詳細については、「ローカライズ スキーマTeams[参照してください。](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="4c9be-306">For more information, see the [Teams localization schema](~/concepts/build-and-test/apps-localization.md)</span></span>

## <a name="50-tabs"></a><span data-ttu-id="4c9be-307">5.0 タブ</span><span class="sxs-lookup"><span data-stu-id="4c9be-307">5.0 Tabs</span></span>

<span data-ttu-id="4c9be-308">アプリにタブが含まれる場合は、これらのガイドラインに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-308">If your app includes a tab, make sure it adheres to these guidelines.</span></span>

> [!TIP]
> <span data-ttu-id="4c9be-309">高品質のアプリ エクスペリエンスを作成する方法の詳細については[、「Teams」を参照してください](~/tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-309">For information on creating a high-quality app experience, see the [Teams tab design guidelines](~/tabs/design/tabs.md).</span></span>

### <a name="51-setup"></a><span data-ttu-id="4c9be-310">5.1 セットアップ</span><span class="sxs-lookup"><span data-stu-id="4c9be-310">5.1 Setup</span></span>

* <span data-ttu-id="4c9be-311">タブのセットアップは、新しいユーザーを終了しなけれはしない必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-311">Tab setup must not dead-end a new user.</span></span> <span data-ttu-id="4c9be-312">アクションまたはワークフローを完了する方法に関するメッセージを提供します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-312">Provide a message on how to complete the action or workflow.</span></span>
* <span data-ttu-id="4c9be-313">認証は、タブのセットアップ中に行う必要があります。その後は行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-313">Authentication should happen during tab setup and not after.</span></span>

### <a name="52-views"></a><span data-ttu-id="4c9be-314">5.2 ビュー</span><span class="sxs-lookup"><span data-stu-id="4c9be-314">5.2 Views</span></span>

* <span data-ttu-id="4c9be-315">サインイン画面領域で大きなロゴを使用したり、Web ページ全体を表示したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="4c9be-315">The sign-in screen area must not use large logos or display an entire webpage.</span></span>
* <span data-ttu-id="4c9be-316">コンテンツを複数のタブで分割することで、コンテンツを簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-316">Content can be simplified by breaking it down across multiple tabs.</span></span>
* <span data-ttu-id="4c9be-317">タブに重複するヘッダーは含めずにしてください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-317">Tabs should not have a duplicate header.</span></span> <span data-ttu-id="4c9be-318">タブ フレームワークにアプリのアイコンと名前が既に表示されている場合は、iframe からロゴを削除します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-318">Remove the logo from the iframe since the tab framework already displays the app icon and name.</span></span>

### <a name="53-navigation"></a><span data-ttu-id="4c9be-319">5.3 ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="4c9be-319">5.3 Navigation</span></span>

* <span data-ttu-id="4c9be-320">タブには、3 つ以上のレベルのナビゲーションを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-320">Tabs must not have more than three levels of navigation.</span></span>
* <span data-ttu-id="4c9be-321">タブは、プライマリ ナビゲーションと競合するナビゲーションを提供Teams必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-321">Tabs must not provide navigation that conflicts with the primary Teams navigation.</span></span>
* <span data-ttu-id="4c9be-322">タブ内のセカンダリ ページと第 3 ページは、メイン タブ領域のレベル 2 ビューとレベル 3 ビューで開く必要があります。このビューは、階層リンクまたは左ナビゲーション経由で移動されます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-322">The secondary and tertiary pages in a tab must be opened in a level two and level three view in the main tab area, which is navigated via breadcrumbs or left nav.</span></span> <span data-ttu-id="4c9be-323">次のコンポーネントを含め、タブ ナビゲーションを支援することもできます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-323">You can also include the following components to aid tab navigation:</span></span>
    * <span data-ttu-id="4c9be-324">戻るボタン</span><span class="sxs-lookup"><span data-stu-id="4c9be-324">Back buttons</span></span>
    * <span data-ttu-id="4c9be-325">ページ ヘッダー</span><span class="sxs-lookup"><span data-stu-id="4c9be-325">Page headers</span></span>
    * <span data-ttu-id="4c9be-326">ハンバーガー メニュー</span><span class="sxs-lookup"><span data-stu-id="4c9be-326">Hamburger menus</span></span>
* <span data-ttu-id="4c9be-327">Tab に水平方向のスクロールを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-327">Tab should not have horizontal scroll.</span></span>
* <span data-ttu-id="4c9be-328">タブ内のディープ リンクは、外部 Web ページにリンクする必要がありますが、Teams (タスク モジュールや他のタブなど) 内のどこかにリンクする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-328">Deep links in tabs must not link to an external webpage but somewhere within Teams (for example, task modules or other tabs).</span></span>
* <span data-ttu-id="4c9be-329">タブでは、ユーザーがコア アプリ エクスペリエンスTeams外部に移動できない必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-329">Tabs should not allow users to navigate outside Teams for the core app experience.</span></span>

### <a name="54-usability"></a><span data-ttu-id="4c9be-330">5.4 使いやすさ</span><span class="sxs-lookup"><span data-stu-id="4c9be-330">5.4 Usability</span></span>

* <span data-ttu-id="4c9be-331">タブは、既存の Web サイトをホストする以外の価値を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-331">Tabs must provide value beyond just hosting an existing website.</span></span>
* <span data-ttu-id="4c9be-332">ユーザーは、タブ内の最後の操作を元に戻す必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-332">Users must be able to undo their last action in the tab.</span></span>
* <span data-ttu-id="4c9be-333">個人用コンテキストのタブは、アプリの共有インスタンスからコンテンツを集約する場合があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-333">Tabs in a personal context may aggregate content from shared instances of the app.</span></span>
* <span data-ttu-id="4c9be-334">タブは、他のテーマにTeamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-334">Tabs must be responsive to Teams themes.</span></span> <span data-ttu-id="4c9be-335">ユーザーがテーマを変更すると、アプリのテーマは選択内容を反映する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-335">When a user changes the theme, the app's theme must reflect the selection.</span></span>
* <span data-ttu-id="4c9be-336">タブでは、Teams スタイルのコンポーネント (Teams フォント、タイプ ランプ、カラー パレット、グリッド システム、モーション、音声トーンなどを使用する) を可能な限り使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-336">Tabs must use Teams-styled components (adopting Teams fonts, type ramps, color palettes, grid system, motion, tone of voice, etc.) whenever possible.</span></span>
* <span data-ttu-id="4c9be-337">[プロパティ] タブを **設定する必要** があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-337">You must include a **Settings** tab.</span></span>
* <span data-ttu-id="4c9be-338">タブは、Teams操作設計 (ページ内ナビゲーション、ダイアログの位置と使用、情報階層など) に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-338">Tabs must follow Teams interaction design (in-page navigation, position and use of dialogs, information hierarchies, etc.) whenever possible.</span></span>
* <span data-ttu-id="4c9be-339">iframe のタブ コンテンツには、Teamsコア機能 (ボット、メッセージング拡張機能、通話、会議など) を模倣する機能を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="4c9be-339">Tab content in the iframe must not include features that mimic Teams core capabilities (for example, bots, messaging extensions, calling, meeting, etc.).</span></span>

> [!TIP]
>
> * <span data-ttu-id="4c9be-340">個人用タブと一緒に個人用ボットを含める。</span><span class="sxs-lookup"><span data-stu-id="4c9be-340">Include a personal bot alongside a personal tab.</span></span>
> * <span data-ttu-id="4c9be-341">ユーザーが自分の個人用タブからコンテンツを共有できます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-341">Allow users to share content from their personal tab.</span></span>

## <a name="60-bots"></a><span data-ttu-id="4c9be-342">6.0 ボット</span><span class="sxs-lookup"><span data-stu-id="4c9be-342">6.0 Bots</span></span>

<span data-ttu-id="4c9be-343">アプリにボットが含まれる場合は、これらのガイドラインに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-343">If your app includes a bot, make sure it adheres to these guidelines.</span></span>

> [!TIP]
> <span data-ttu-id="4c9be-344">高品質のアプリ エクスペリエンスを作成する方法については、「ボットの設計[Teamsを参照してください](~/bots/design/bots.md)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-344">For information on creating a high-quality app experience, see the [Teams bot design guidelines](~/bots/design/bots.md).</span></span>

### <a name="61-bot-commands"></a><span data-ttu-id="4c9be-345">6.1 ボット コマンド</span><span class="sxs-lookup"><span data-stu-id="4c9be-345">6.1 Bot commands</span></span>

<span data-ttu-id="4c9be-346">ユーザー入力を分析し、ユーザーの意図を予測することは困難です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-346">Analyzing user input and predicting user intent is difficult.</span></span> <span data-ttu-id="4c9be-347">ボット コマンドは、ボットが理解している一連の単語または語句をユーザーに提供します。そのため、ボット (およびボット) は推測する必要がなされます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-347">Bot commands provide users a set of words or phrases your bot understands so they (and your bot) don't have to guess.</span></span>

* <span data-ttu-id="4c9be-348">アプリ構成でサポートされているボット コマンドの一覧を作成することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4c9be-348">Listing supported bot commands in your app configurations is highly recommended.</span></span> <span data-ttu-id="4c9be-349">ユーザーがボットにメッセージを送信しようとすると、これらのコマンドが作成ボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-349">These commands display in the compose box when a user tries to message your bot.</span></span>
* <span data-ttu-id="4c9be-350">ボットがサポートしているすべてのコマンドは **、Hi、Hello、ヘルプ** コマンドなど、正しく **動作する必要** があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-350">All commands that your bot supports must work correctly, including the **Hi**, **Hello**, and **Help** command.</span></span>

> [!TIP]
> <span data-ttu-id="4c9be-351">個人用ボットの場合は、ボット **が実行** できる操作をさらに説明する [ヘルプ] タブを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-351">For personal bots, include a **Help** tab that further describes what your bot can do.</span></span>

### <a name="62-bot-welcome-messages"></a><span data-ttu-id="4c9be-352">6.2 ボットのウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="4c9be-352">6.2 Bot welcome messages</span></span>

* <span data-ttu-id="4c9be-353">ボットは、ほとんどの場合、最初の実行時にウェルカム メッセージを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-353">Bots should almost always send a welcome message during first run.</span></span> <span data-ttu-id="4c9be-354">最適なエクスペリエンスを得る場合は、ボットの価値提案、ボットの構成方法、およびサポートされているすべてのボット コマンドを簡単に説明する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-354">For the best experience, the message should include the value proposition of your bot, how to configure the bot, and briefly describe all supported bot commands.</span></span> <span data-ttu-id="4c9be-355">ボタン付きアダプティブ カードを使用してメッセージを表示すると、使いやすさが向上します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-355">You can display the message using an Adaptive Card with buttons for better usability.</span></span> <span data-ttu-id="4c9be-356">詳細については、「ボットのウェルカム [メッセージをトリガーする方法」を参照してください](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-356">For more information, see [how to trigger a bot welcome message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="4c9be-357">チャネルとチャット内のボットウェルカム メッセージは、最初の実行時に省略できます。特にボットが個人用に使用できる場合、同様のアクションを実行します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-357">Bot welcome messages in channels and chats are optional during first run, especially if the bot is available for personal use and performs similar actions.</span></span> <span data-ttu-id="4c9be-358">ボットがウェルカム メッセージを送信する場合は、これらをユーザーに個別に送信し (これは [spamming と見なされます) 必要があります](#63-bot-message-spamming)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-358">If your bot does send welcome messages, it must not send these to users individually (this is considered [spamming](#63-bot-message-spamming)).</span></span> <span data-ttu-id="4c9be-359">メッセージには、ボットを追加したユーザーも示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-359">The message should also mention the person who added the bot.</span></span>
* <span data-ttu-id="4c9be-360">通知専用ボットは、ユーザーのメッセージに返信しないウェルカム メッセージを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-360">Notification-only bots must send a welcome message that conveys it will not reply to users' messages.</span></span>

> [!TIP]
> <span data-ttu-id="4c9be-361">個々のユーザーへのウェルカム メッセージでは、カルーセル ツアーを使用すると、ボットの効果的な概要と他のアプリ機能を提供できます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-361">In welcome messages to individual users, a carousel tour can provide an effective overview of your bot and any other app features.</span></span> <span data-ttu-id="4c9be-362">ユーザーがボットのコマンドを試すことができるボタンを含めることが推奨されます (例：**タスクを作成する**)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-362">Including buttons the let users try bot commands is encouraged (for example, **Create a task**).</span></span>

### <a name="63-bot-message-spamming"></a><span data-ttu-id="4c9be-363">6.3 ボット メッセージの spamming</span><span class="sxs-lookup"><span data-stu-id="4c9be-363">6.3 Bot message spamming</span></span>

<span data-ttu-id="4c9be-364">ボットは、複数のメッセージを短時間連続で送信してユーザーに迷惑メールを送信しなけり。</span><span class="sxs-lookup"><span data-stu-id="4c9be-364">Bots must not spam users by sending multiple messages in short succession.</span></span>

* <span data-ttu-id="4c9be-365">**チャネルとチャットのボット メッセージ**: 個別の投稿を作成してユーザーに迷惑メールを送信しない。</span><span class="sxs-lookup"><span data-stu-id="4c9be-365">**Bot messages in channels and chats**: Don't spam users by creating separate posts.</span></span> <span data-ttu-id="4c9be-366">同じスレッドに返信を含む 1 つの投稿を作成します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-366">Create a single post with replies in the same thread.</span></span>
* <span data-ttu-id="4c9be-367">**個人用アプリのボット メッセージ**: 複数のメッセージを連続して送信しない。</span><span class="sxs-lookup"><span data-stu-id="4c9be-367">**Bot messages in personal apps**: Don't send multiple messages in quick succession.</span></span> <span data-ttu-id="4c9be-368">完全な情報を含む 1 つのメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-368">Send one message with complete information.</span></span> <span data-ttu-id="4c9be-369">複数ターンの会話を避けて、1 つのワークフローを完了します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-369">Avoid multi-turn conversations to complete a single workflow.</span></span> <span data-ttu-id="4c9be-370">代わりに、フォーム (またはタスク モジュール) を使用して、ユーザーから一度にすべての入力を収集する方法を検討してください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-370">Instead, consider using a form (or task module) to collect all inputs from a user at one time.</span></span>
* <span data-ttu-id="4c9be-371">**ウェルカム メッセージ**: 同じウェルカム メッセージを一定の間隔で繰り返す操作は許可されません。また、spamming と見なされます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-371">**Welcome messages**: Repeating the same welcome message over regular intervals is not allowed and considered spamming.</span></span> <span data-ttu-id="4c9be-372">たとえば、新しいメンバーがチームに追加された場合、他のメンバーにウェルカム メッセージを迷惑メールで送信しない。</span><span class="sxs-lookup"><span data-stu-id="4c9be-372">For example, when a new member is added to a team, don't spam the other members with a welcome message.</span></span> <span data-ttu-id="4c9be-373">代わりに、新しいメンバーに個人的にメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-373">Message the new member personally instead.</span></span>

### <a name="64-bot-notifications"></a><span data-ttu-id="4c9be-374">6.4 ボット通知</span><span class="sxs-lookup"><span data-stu-id="4c9be-374">6.4 Bot notifications</span></span>

<span data-ttu-id="4c9be-375">ボット通知には、ボットに対して定義した範囲 (チーム、チャット、または個人) に関連するコンテンツが含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-375">Bot notifications must include content relevant for the scope you define for the bot (team, chat, or personal).</span></span>

### <a name="65-bots-and-adaptive-cards"></a><span data-ttu-id="4c9be-376">6.5 ボットとアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="4c9be-376">6.5 Bots and Adaptive Cards</span></span>

<span data-ttu-id="4c9be-377">アダプティブ カードは、ボット メッセージを表示することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4c9be-377">Adaptive Cards are a highly recommended way to display bot messages.</span></span> <span data-ttu-id="4c9be-378">カードは軽量で、1 ~ 3 つのアクションのみを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-378">Your cards must be lightweight and include only 1-3 actions.</span></span> <span data-ttu-id="4c9be-379">より多くのコンテンツを表示する必要がある場合は、タスク モジュールまたはタブの使用を検討してください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-379">If you need to display more content, consider using a task module or tab.</span></span>

<span data-ttu-id="4c9be-380">詳細については、以下のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-380">See the following resources for more information:</span></span>

* [<span data-ttu-id="4c9be-381">アダプティブ カードをデザインする</span><span class="sxs-lookup"><span data-stu-id="4c9be-381">Designing Adaptive Cards</span></span>](~/task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="4c9be-382">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="4c9be-382">Cards reference</span></span>](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="70-messaging-extensions"></a><span data-ttu-id="4c9be-383">7.0 メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="4c9be-383">7.0 Messaging extensions</span></span>

<span data-ttu-id="4c9be-384">アプリにメッセージング拡張機能が含まれる場合は、これらのガイドラインに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-384">If your app includes a messaging extension, make sure it adheres to these guidelines.</span></span>

> [!TIP]
> <span data-ttu-id="4c9be-385">高品質のアプリ エクスペリエンスを作成する方法については、「メッセージング拡張機能[の設計Teamsガイドライン」を参照してください](~/messaging-extensions/design/messaging-extension-design.md)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-385">For information on creating a high-quality app experience, see the [Teams messaging extension design guidelines](~/messaging-extensions/design/messaging-extension-design.md).</span></span>

### <a name="71-action-commands"></a><span data-ttu-id="4c9be-386">7.1 アクション コマンド</span><span class="sxs-lookup"><span data-stu-id="4c9be-386">7.1 Action commands</span></span>

<span data-ttu-id="4c9be-387">アクション ベースのメッセージング拡張機能は、次の操作を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-387">Action-based messaging extensions should do the following:</span></span>

* <span data-ttu-id="4c9be-388">サインインなどの中間手順を完了せずに、ユーザーがメッセージに対するアクションをトリガーできます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-388">Allow users to trigger actions on a message without completing intermediate steps, such as signing in.</span></span>
* <span data-ttu-id="4c9be-389">メッセージ コンテキストを次の作業状態に渡します。</span><span class="sxs-lookup"><span data-stu-id="4c9be-389">Pass the message context to the next work state.</span></span>

### <a name="72-preview-links-link-unfurling"></a><span data-ttu-id="4c9be-390">7.2 リンクのプレビュー (リンクの分岐解除)</span><span class="sxs-lookup"><span data-stu-id="4c9be-390">7.2 Preview links (link unfurling)</span></span>

<span data-ttu-id="4c9be-391">メッセージング拡張機能は、[メッセージ作成] ボックスで認識されたリンクTeamsプレビューする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-391">Messaging extensions should preview recognized links in the Teams compose box.</span></span> <span data-ttu-id="4c9be-392">コントロールの外部にあるドメイン (絶対 URL またはワイルドカード) は追加しません。</span><span class="sxs-lookup"><span data-stu-id="4c9be-392">Do not add domains that are outside your control (either absolute URLs or wildcards).</span></span> <span data-ttu-id="4c9be-393">たとえば、有効 `yourapp.onmicrosoft.com` ですが `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-393">For example, `yourapp.onmicrosoft.com` is valid but `*.onmicrosoft.com` is not valid.</span></span> <span data-ttu-id="4c9be-394">また、上位レベルのドメインも禁止されています (たとえば、 `*.com` または `*.org` )。</span><span class="sxs-lookup"><span data-stu-id="4c9be-394">Top-level domains also are prohibited (for example, `*.com` or `*.org`).</span></span>

### <a name="73-search-commands"></a><span data-ttu-id="4c9be-395">7.3 検索コマンド</span><span class="sxs-lookup"><span data-stu-id="4c9be-395">7.3 Search commands</span></span>

* <span data-ttu-id="4c9be-396">検索ベースのメッセージング拡張機能は、ユーザーが効果的に検索するのに役立つテキストを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-396">Search-based messaging extensions must provide text that helps users effectively search.</span></span>
* <span data-ttu-id="4c9be-397">@mentionは、明確でわかりやすい、読みやすくする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-397">@mention executables must be clear, easy to understand, and readable.</span></span>

## <a name="80-task-modules"></a><span data-ttu-id="4c9be-398">8.0 タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="4c9be-398">8.0 Task modules</span></span>

<span data-ttu-id="4c9be-399">タスク モジュールには、アイコンと、関連付けられているアプリの短い名前が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-399">A task module must include an icon and the short name of the app it's associated with.</span></span>

> [!TIP]
> <span data-ttu-id="4c9be-400">高品質のアプリ エクスペリエンスを作成する方法については、「タスク モジュールの設計[Teams」を参照してください](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-400">For information on creating a high-quality app experience, see the [Teams task module design guidelines](~/task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="90-meeting-extensions"></a><span data-ttu-id="4c9be-401">9.0 会議の拡張機能</span><span class="sxs-lookup"><span data-stu-id="4c9be-401">9.0 Meeting extensions</span></span>

<span data-ttu-id="4c9be-402">アプリに会議の拡張機能が含まれる場合は、これらのガイドラインに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-402">If your app includes a meeting extension, make sure it adheres to these guidelines.</span></span>

> [!TIP]
> <span data-ttu-id="4c9be-403">高品質のアプリ エクスペリエンスを作成する方法については、「会議拡張[Teamsガイドライン」を参照してください](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-403">For information on creating a high-quality app experience, see the [Teams meeting extension design guidelines](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).</span></span>

### <a name="91-pre--and-post-meeting-experience"></a><span data-ttu-id="4c9be-404">9.1 会議の開催前と会議後のエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="4c9be-404">9.1 Pre- and post-meeting experience</span></span>

* <span data-ttu-id="4c9be-405">会議前および会議後の画面は、一般的なタブデザインガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-405">Pre- and post-meeting screens must adhere to general tab design guidelines.</span></span> <span data-ttu-id="4c9be-406">詳細については、「デザイン ガイドライン」[をTeamsしてください](~/tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-406">For more information, see the [Teams design guidelines](~/tabs/design/tabs.md).</span></span>
* <span data-ttu-id="4c9be-407">タブに水平スクロールを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-407">Tabs must not have horizontal scrolling.</span></span>
* <span data-ttu-id="4c9be-408">複数のアイテム (10 件を超えるポーリングやアンケートなど) を表示する場合、タブには整理されたレイアウトが必要です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-408">Tabs should have an organized layout when displaying multiple items (for instance, more than 10 polls or surveys).</span></span> <span data-ttu-id="4c9be-409">レイアウトの例 [を参照してください](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-409">See an [example layout](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).</span></span>
* <span data-ttu-id="4c9be-410">アンケートまたはアンケートの結果がエクスポートされると、アプリはユーザーに通知する必要があります。"結果が正常にダウンロードされました" というメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-410">Your app must notify users when the results of a survey or poll are exported by stating, "Results successfully downloaded".</span></span>

### <a name="92-in-meeting-experience"></a><span data-ttu-id="4c9be-411">9.2 会議中のエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="4c9be-411">9.2 In-meeting experience</span></span>

* <span data-ttu-id="4c9be-412">アプリは、会議中にのみ暗いテーマを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-412">Apps must only use a dark theme during meetings.</span></span> <span data-ttu-id="4c9be-413">詳細については、「デザイン ガイドライン」[をTeamsしてください](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)。</span><span class="sxs-lookup"><span data-stu-id="4c9be-413">For more information, see the [Teams design guidelines](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming).</span></span>
* <span data-ttu-id="4c9be-414">会議中にアプリ アイコンにカーソルを合わせると、ツールヒントにアプリ名が表示されます。</span><span class="sxs-lookup"><span data-stu-id="4c9be-414">A tooltip should display the app name when hovering over the app icon during meetings.</span></span>
* <span data-ttu-id="4c9be-415">メッセージング拡張機能は、会議の外部で行う場合と同様に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-415">Messaging extensions must function the same during meetings as they do outside meetings.</span></span>

### <a name="93-in-meeting-tabs"></a><span data-ttu-id="4c9be-416">9.3 会議中のタブ</span><span class="sxs-lookup"><span data-stu-id="4c9be-416">9.3 In-meeting tabs</span></span>

* <span data-ttu-id="4c9be-417">応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-417">Must be responsive.</span></span> <span data-ttu-id="4c9be-418">パディングとコンポーネントのサイズは必ず維持してください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-418">Make sure to maintain padding and component sizes.</span></span>
* <span data-ttu-id="4c9be-419">ナビゲーションのレイヤーが複数ある場合は、戻るボタンが必要です。</span><span class="sxs-lookup"><span data-stu-id="4c9be-419">Must have a back button if there is more than one layer of navigation.</span></span>
* <span data-ttu-id="4c9be-420">複数の [閉じる] ボタンまたは [閉じる] ボタンを含めずに指定してください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-420">Must not include more than one dismiss or close button.</span></span> <span data-ttu-id="4c9be-421">これは、タブを閉じ込む組み込みのヘッダー ボタンが既にあるので、ユーザーを混乱させる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-421">This may confuse users since there's already a built-in header button to dismiss the tab.</span></span>
* <span data-ttu-id="4c9be-422">水平スクロールを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-422">Must not have horizontal scrolling.</span></span>

### <a name="94-in-meeting-dialogs"></a><span data-ttu-id="4c9be-423">9.4 会議中のダイアログ</span><span class="sxs-lookup"><span data-stu-id="4c9be-423">9.4 In-meeting dialogs</span></span>

* <span data-ttu-id="4c9be-424">軽くてタスク指向のシナリオで使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-424">Should be used sparingly and for scenarios that are light and task-oriented.</span></span>
* <span data-ttu-id="4c9be-425">1 つの列にコンテンツを表示し、複数のナビゲーション レベルを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-425">Must display content in a single column and not have multiple navigation levels.</span></span>
* <span data-ttu-id="4c9be-426">タスク モジュールを使用しない。</span><span class="sxs-lookup"><span data-stu-id="4c9be-426">Must not use task modules.</span></span>
* <span data-ttu-id="4c9be-427">会議ステージの中央に揃える必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-427">Must align with the center of the meeting stage.</span></span>
* <span data-ttu-id="4c9be-428">ユーザーがボタンを選択するか、アクションを実行すると、削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-428">Should be dismissed once a user selects a button or performs an action.</span></span>

## <a name="100-notifications"></a><span data-ttu-id="4c9be-429">10.0 通知</span><span class="sxs-lookup"><span data-stu-id="4c9be-429">10.0 Notifications</span></span>

<span data-ttu-id="4c9be-430">アプリで Microsoft Graphによって提供されるアクティビティ フィード API を使用[している場合は](https://docs.microsoft.com/graph/teams-send-activityfeednotifications)、次のガイドラインに準拠してください。</span><span class="sxs-lookup"><span data-stu-id="4c9be-430">If your app uses the [activity feed APIs provided by Microsoft Graph](https://docs.microsoft.com/graph/teams-send-activityfeednotifications), make sure it adheres to the following guidelines.</span></span>

### <a name="101-general"></a><span data-ttu-id="4c9be-431">10.1 全般</span><span class="sxs-lookup"><span data-stu-id="4c9be-431">10.1 General</span></span>

* <span data-ttu-id="4c9be-432">アプリ構成で指定された通知トリガーはすべて、アプリで通知を受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-432">All the notification triggers specified in your app configurations should get a notification in the app.</span></span>
* <span data-ttu-id="4c9be-433">通知は、アプリ用に構成されたサポートされている言語ごとにローカライズする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-433">Notifications must be localized per the supported languages configured for your app.</span></span>
* <span data-ttu-id="4c9be-434">通知は、ユーザーの操作から 5 秒以内に表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-434">Notifications must display within five seconds of user action.</span></span>

### <a name="102-avatars"></a><span data-ttu-id="4c9be-435">10.2 アバター</span><span class="sxs-lookup"><span data-stu-id="4c9be-435">10.2 Avatars</span></span>

* <span data-ttu-id="4c9be-436">通知アバターは、アプリの色アイコンと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-436">The notification avatar should match your app's color icon.</span></span>
* <span data-ttu-id="4c9be-437">ユーザーによってトリガーされる通知には、ユーザーのアバターを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-437">Notifications triggered by a user should include the user's avatar.</span></span>

### <a name="103-spamming"></a><span data-ttu-id="4c9be-438">10.3 Spamming</span><span class="sxs-lookup"><span data-stu-id="4c9be-438">10.3 Spamming</span></span>

* <span data-ttu-id="4c9be-439">アプリは、1 分あたり 10 件を超える通知をユーザーに送信しなけり。</span><span class="sxs-lookup"><span data-stu-id="4c9be-439">Apps must not send more than 10 notifications per minute to a user.</span></span>
* <span data-ttu-id="4c9be-440">ボットとアクティビティ フィードは、重複する通知をトリガーしなけい。</span><span class="sxs-lookup"><span data-stu-id="4c9be-440">Bots and the activity feed should not trigger duplicate notifications.</span></span>
* <span data-ttu-id="4c9be-441">通知は、ユーザーに一部の値を提供する必要があります。また、些細なイベントや無関係なイベントには使用できません。</span><span class="sxs-lookup"><span data-stu-id="4c9be-441">Notifications must provide some value to users and not be used for trivial or irrelevant events.</span></span>

### <a name="104-navigation-and-layout"></a><span data-ttu-id="4c9be-442">10.4 ナビゲーションとレイアウト</span><span class="sxs-lookup"><span data-stu-id="4c9be-442">10.4 Navigation and layout</span></span>

* <span data-ttu-id="4c9be-443">通知は、アクティビティ フィードのレイアウトTeamsエクスペリエンスに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-443">Notifications must adhere to the Teams activity feed layout and experience.</span></span>
* <span data-ttu-id="4c9be-444">通知を選択する場合、ユーザーはユーザーエクスペリエンスから取り出され、Teams内の関連コンテンツにTeamsがあります。</span><span class="sxs-lookup"><span data-stu-id="4c9be-444">When selecting a notification, the user must be directed to relevant content within Teams and not taken out of the Teams experience.</span></span>

## <a name="110-advertising"></a><span data-ttu-id="4c9be-445">11.0 広告</span><span class="sxs-lookup"><span data-stu-id="4c9be-445">11.0 Advertising</span></span>

<span data-ttu-id="4c9be-446">アプリは、動的広告、バナー広告、メッセージ内の広告を含む広告を表示しなけり。</span><span class="sxs-lookup"><span data-stu-id="4c9be-446">Apps must not display advertising, including dynamic ads, banner ads, and ads in messages.</span></span>

## <a name="next-step"></a><span data-ttu-id="4c9be-447">次の手順</span><span class="sxs-lookup"><span data-stu-id="4c9be-447">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4c9be-448">パートナー センター アカウントを作成する</span><span class="sxs-lookup"><span data-stu-id="4c9be-448">Create a Partner Center account</span></span>](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)