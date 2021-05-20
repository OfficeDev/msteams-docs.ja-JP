---
title: Microsoft Teamsストア検証ガイドライン
description: Teams ストア (AppSource) に提出されたすべてのアプリが従う必要があるガイドラインについて説明します。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 4daa8b027d7525f0fb3223c2000eee301043398a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565138"
---
# <a name="microsoft-teams-store-validation-guidelines"></a><span data-ttu-id="f7dba-103">Microsoft Teamsストア検証ガイドライン</span><span class="sxs-lookup"><span data-stu-id="f7dba-103">Microsoft Teams store validation guidelines</span></span>

<span data-ttu-id="f7dba-104">これらのガイドラインに従うと、アプリがMicrosoft Teamsストアの送信プロセスに合格する可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-104">Following these guidelines increases the likelihood your app will pass the Microsoft Teams store submission process.</span></span> <span data-ttu-id="f7dba-105">これらのTeams固有のガイドラインは、Microsoft[の商用市場認定ポリシー](/legal/marketplace/certification-policies)を補完し、新機能、ユーザーからのフィードバック、およびビジネス ルールの変更を反映するように頻繁に更新されます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-105">These Teams-specific guidelines complement the Microsoft [commercial marketplace certification policies](/legal/marketplace/certification-policies) and are updated frequently to reflect new capabilities, user feedback, and business rule changes.</span></span>

> [!NOTE]
> <span data-ttu-id="f7dba-106">一部のガイドラインは、アプリに適用できない場合があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-106">Some guidelines may not be applicable to your app.</span></span> <span data-ttu-id="f7dba-107">たとえば、アプリにボットが含まれていない場合、ボット関連のガイドラインは無視できます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-107">For example, if your app doesn't include a bot, you can ignore bot-related guidelines.</span></span>

## <a name="10-value-proposition"></a><span data-ttu-id="f7dba-108">1.0 バリュープロポジション</span><span class="sxs-lookup"><span data-stu-id="f7dba-108">1.0 Value proposition</span></span>

### <a name="11-app-name"></a><span data-ttu-id="f7dba-109">1.1 アプリ名</span><span class="sxs-lookup"><span data-stu-id="f7dba-109">1.1 App name</span></span>

<span data-ttu-id="f7dba-110">アプリの名前は、ユーザーがストア内でアプリを検出する方法において重要な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="f7dba-110">An app's name plays a critical role in how users discover it in the store.</span></span> <span data-ttu-id="f7dba-111">アプリ名について、次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-111">Remember the following about app names:</span></span>

* <span data-ttu-id="f7dba-112">名前には、ユーザーに関連する用語を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-112">The name must include terms relevant to your users.</span></span>
* <span data-ttu-id="f7dba-113">**チャット**、**連絡先**、**予定表**、**通話**、**ファイル**、**アクティビティ\*\*\*\*、Teams、\*\*\*\*アプリ**、**ヘルプ**&#8212;などの&#8212;&#8212;コア Teams機能の名前は、アプリ名に含めるべきではありません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-113">Names of core Teams features&#8212;such as **Chat**, **Contacts**, **Calendar**, **Calls**, **Files**, **Activity**, **Teams**, **Apps**, and **Help**&#8212;should not be included in your app name.</span></span>
* <span data-ttu-id="f7dba-114">共通名詞には、開発者の名前 (たとえば、**タスク** ではなく **Contoso タスク**) のプレフィックスまたはサフィックスを付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-114">Common nouns must be prefixed or suffixed with the developer's name (for example, **Contoso Tasks** rather than **Tasks**).</span></span>
* <span data-ttu-id="f7dba-115">**Teams** またはその他のマイクロソフト製品名を使用して、共同ブランドまたは共同販売を誤って示す可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-115">Must not use **Teams** or other Microsoft product names that could falsely indicate co-branding or co-selling.</span></span> <span data-ttu-id="f7dba-116">(マイクロソフトのソフトウェア、製品、およびサービスの参照の詳細については、 [マイクロソフトの商標およびブランドガイドライン](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-116">(For more information about referencing Microsoft software, products, and services, see the [Microsoft Trademark and Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)).</span></span>
* <span data-ttu-id="f7dba-117">アプリが Microsoft との正式なパートナーシップの一部である場合は、アプリの名前が最初に表示される必要があります (たとえば **、Microsoft Teamsの Contoso コネクタ**)。</span><span class="sxs-lookup"><span data-stu-id="f7dba-117">If your app is part of an official partnership with Microsoft, the name of your app must come first (for example, **Contoso Connector for Microsoft Teams**).</span></span>
* <span data-ttu-id="f7dba-118">店舗または市販市場での他のオファーに記載されているアプリの名前をコピーしないでください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-118">Must not copy the name of an app listed in the store or other offer in the commercial marketplace.</span></span>
* <span data-ttu-id="f7dba-119">冒涜的または軽蔑的な用語を含んではなりません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-119">Must not contain profane or derogatory terms.</span></span> <span data-ttu-id="f7dba-120">また、人種的または文化的に無神経な言葉を含めてはならない。</span><span class="sxs-lookup"><span data-stu-id="f7dba-120">The name also must not include racially or culturally insensitive language.</span></span>
* <span data-ttu-id="f7dba-121">一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-121">Must be unique.</span></span> <span data-ttu-id="f7dba-122">たとえば、同じ名前と機能を持つ異なるリージョンの複数のアプリを一覧表示することはできません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-122">For example, you cannot list multiple apps for different regions with the same name and functionality.</span></span>

### <a name="12-suitable-for-workplace-consumption"></a><span data-ttu-id="f7dba-123">1.2 職場での消費に適しています</span><span class="sxs-lookup"><span data-stu-id="f7dba-123">1.2 Suitable for workplace consumption</span></span>

<span data-ttu-id="f7dba-124">アプリコンテンツは、一般的な職場での利用に適しており、商用市場の認証ポリシーに記載されているすべての制限に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-124">App content must be suitable for general workplace consumption and abide by all restrictions listed in the commercial marketplace certification policies.</span></span> <span data-ttu-id="f7dba-125">宗教、政治、ギャンブル、長期の娯楽に関するコンテンツは禁止されています。</span><span class="sxs-lookup"><span data-stu-id="f7dba-125">Content related to religion, politics, gambling, and prolonged entertainment is prohibited.</span></span> <span data-ttu-id="f7dba-126">詳細については、「 [商用市場の認定ポリシー](/legal/marketplace/certification-policies#10010-inappropriate-content)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-126">For more information, see the [commercial marketplace certification policies](/legal/marketplace/certification-policies#10010-inappropriate-content).</span></span>

<span data-ttu-id="f7dba-127">アプリは、グループのコラボレーションを促進し、個人の生産性を向上させるか、またはその両方を促進する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-127">Your app must facilitate group collaboration, improve an individual's productivity, or both.</span></span> <span data-ttu-id="f7dba-128">チームの絆と社交を目的としたアプリは、複数の参加者のために共同で設計されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-128">Apps intended for team bonding and socializing must be collaborative and designed for multiple participants.</span></span> <span data-ttu-id="f7dba-129">この種のアプリも、相当な時間の投資を必要としたり、生産性に影響を与えたりする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-129">These types of apps also should not require a substantial time investment or perceptively impact productivity.</span></span>

### <a name="13-similar-platforms-and-services"></a><span data-ttu-id="f7dba-130">1.3 類似プラットフォームとサービス</span><span class="sxs-lookup"><span data-stu-id="f7dba-130">1.3 Similar platforms and services</span></span>

<span data-ttu-id="f7dba-131">アプリが特定の相互運用性を提供しない限り、アプリはTeamsエクスペリエンスに焦点を当て、他の類似するチャット ベースのコラボレーション プラットフォームまたはサービスの名前、アイコン、画像を含めないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-131">Apps must focus on the Teams experience and not include the names, icons, or imagery of other similar chat-based collaboration platforms or services unless your app provides specific interoperability.</span></span>

### <a name="14-feature-names"></a><span data-ttu-id="f7dba-132">1.4 フィーチャー名</span><span class="sxs-lookup"><span data-stu-id="f7dba-132">1.4 Feature names</span></span>

<span data-ttu-id="f7dba-133">ボタンやその他の UI テキスト内のアプリ機能名は、Teamsやその他の Microsoft 製品用に予約されている用語と矛盾してはなりません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-133">App feature names in buttons and other UI text must not conflict with terminology reserved for Teams and other Microsoft products.</span></span> <span data-ttu-id="f7dba-134">たとえば、 **会議の開始**、 **通話の発信**、 **チャットの開始** などです。</span><span class="sxs-lookup"><span data-stu-id="f7dba-134">For example, **Start meeting**, **Make call**, or **Start chat**.</span></span> <span data-ttu-id="f7dba-135">[**会議** の開始] ではなく **[Contoso 会議を開始する**] など、この問題を完全に回避できない場合は、アプリ名を含めます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-135">Include your app name if you can't completely avoid this, such as **Start Contoso meeting** instead of **Start meeting**.</span></span>

## <a name="20-security"></a><span data-ttu-id="f7dba-136">2.0 セキュリティ</span><span class="sxs-lookup"><span data-stu-id="f7dba-136">2.0 Security</span></span>

### <a name="21-microsoft-365-app-compliance-program"></a><span data-ttu-id="f7dba-137">2.1 Microsoft 365アプリコンプライアンスプログラム</span><span class="sxs-lookup"><span data-stu-id="f7dba-137">2.1 Microsoft 365 App Compliance Program</span></span>

<span data-ttu-id="f7dba-138">[Microsoft 365 アプリ コンプライアンス プログラム](/microsoft-365-app-certification/overview)は、組織がアプリに関するセキュリティおよびコンプライアンス情報を評価することによってリスクを評価および管理するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-138">The [Microsoft 365 App Compliance Program](/microsoft-365-app-certification/overview) is intended to help organizations assess and manage risk by evaluating security and compliance information about your app.</span></span> <span data-ttu-id="f7dba-139">Teams ストアにアプリを発行する場合は、プログラムの次のレベルを完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-139">If you're publishing an app to the Teams store, you must complete the following tiers of the program:</span></span>

* <span data-ttu-id="f7dba-140">[Publisher検証](/azure/active-directory/develop/publisher-verification-overview): 管理者とエンド ユーザーが、Microsoft ID プラットフォームと統合するアプリ開発者の信頼性を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-140">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview): Helps admins and end users understand the authenticity of app developers integrating with the Microsoft identity platform.</span></span> <span data-ttu-id="f7dba-141">完了すると、青色の「検証済み」バッジがAzure Active Directory (Azure AD) の同意ダイアログやその他の画面に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-141">When completed, a blue "verified" badge displays on the Azure Active Directory (Azure AD) consent dialog and other screens.</span></span> <span data-ttu-id="f7dba-142">詳細については、「 [よく寄せられる質問](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)」、パブリッシャー [検証済みとしてアプリをマークする方法](/azure/active-directory/develop/mark-app-as-publisher-verified)、および [発行元の検証のトラブルシューティング](/azure/active-directory/develop/troubleshoot-publisher-verification)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-142">For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>
* <span data-ttu-id="f7dba-143">[Publisher構成証明](/microsoft-365-app-certification/docs/attestation): 一般的なデータ処理、セキュリティ情報、コンプライアンス情報を共有して、潜在的な顧客がアプリの使用に関する情報に基づいた意思決定を行う際に役立つプロセス。</span><span class="sxs-lookup"><span data-stu-id="f7dba-143">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation): A process in which you share general, data handling, and security and compliance information to help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="f7dba-144">以前に一覧表示されていないアプリを申請する場合、アプリがTeams ストアに入るまで、正式にPublisher構成証明を完了することはできません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-144">If you're submitting an app that hasn't been listed previously, you can't officially complete Publisher Attestation until your app is in the Teams store.</span></span> <span data-ttu-id="f7dba-145">一覧に表示されているアプリを更新する場合は、アプリの最新バージョンを提出する前に、Publisherの構成証明を完了します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-145">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app.</span></span>

### <a name="22-bots"></a><span data-ttu-id="f7dba-146">2.2 ボット</span><span class="sxs-lookup"><span data-stu-id="f7dba-146">2.2 Bots</span></span>

<span data-ttu-id="f7dba-147">ボットやメッセージング拡張機能など、Microsoft Azure Bot サービスを使用するアプリの場合は、Microsoft[オンライン サービスの条件](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)で定義されているすべての要件に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-147">For apps that use the Microsoft Azure Bot Service (such as bots and messaging extensions), you must follow all requirements defined in the Microsoft [Online Services Terms](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).</span></span>

<span data-ttu-id="f7dba-148">ボットは、ファイルのアップロード後にファイルをアップロードし、確認メッセージを表示する許可を常に要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-148">Bots must always ask permission to upload a file and display a confirmation message after the file uploads.</span></span>

### <a name="23-external-domains"></a><span data-ttu-id="f7dba-149">2.3 外部ドメイン</span><span class="sxs-lookup"><span data-stu-id="f7dba-149">2.3 External domains</span></span>

<span data-ttu-id="f7dba-150">ほとんどの場合、組織の管理下にないドメイン (ワイルドカードを含む) とトンネリング サービスをアプリのドメイン構成に含めないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-150">In most cases, you must not include domains outside of your organization's control (including wildcards) and tunneling services in your app's domain configurations.</span></span> <span data-ttu-id="f7dba-151">次の例外があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-151">The following exceptions include:</span></span>

* <span data-ttu-id="f7dba-152">アプリで Azure Bot サービスの OAuthCard を使用している場合は、 `token.botframework.com` 有効なドメインとして含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-152">If your app uses the Azure Bot Service's OAuthCard, you must include `token.botframework.com` as a valid domain or the **Sign in** button won't work.</span></span>
* <span data-ttu-id="f7dba-153">アプリがSharePointに依存している場合は、コンテキスト プロパティを使用して、関連付けられたルート SharePoint サイトを有効なドメインとして含めることができます `{teamSiteDomain}` 。</span><span class="sxs-lookup"><span data-stu-id="f7dba-153">If your app relies on SharePoint, you can include the associated root SharePoint site as a valid domain using the `{teamSiteDomain}` context property.</span></span>

### <a name="24-authentication"></a><span data-ttu-id="f7dba-154">2.4 認証</span><span class="sxs-lookup"><span data-stu-id="f7dba-154">2.4 Authentication</span></span>

<span data-ttu-id="f7dba-155">アプリ認証を実装する方法については[、「Teams の認証」を](~/concepts/authentication/authentication.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-155">For information on how to implement app authentication, see [authentication in Teams](~/concepts/authentication/authentication.md).</span></span>

#### <a name="241-authenticating-with-external-services"></a><span data-ttu-id="f7dba-156">2.4.1 外部サービスによる認証</span><span class="sxs-lookup"><span data-stu-id="f7dba-156">2.4.1 Authenticating with external services</span></span>

<span data-ttu-id="f7dba-157">アプリが外部サービスでユーザーを認証する場合は、次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-157">Remember the following if your app authenticates users with an external service.</span></span>

* <span data-ttu-id="f7dba-158">**サインイン、サインアウト、およびログインエクスペリエンス**:</span><span class="sxs-lookup"><span data-stu-id="f7dba-158">**Sign in, sign out, and sign up experiences**:</span></span>
  * <span data-ttu-id="f7dba-159">外部のアカウントやサービスに依存するアプリでは、明確でシンプルなサインイン、サインアウト、サインアップのエクスペリエンスを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-159">Apps that depend on external accounts or services must provide clear and simple sign in, sign out, and sign up experiences.</span></span>
  * <span data-ttu-id="f7dba-160">ユーザーがサインアウトした場合、ユーザーはアプリからのみサインアウトし、Teamsにサインインしたままにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-160">When a user signs out, they must sign out only from the app and remain signed in to Teams.</span></span>
* <span data-ttu-id="f7dba-161">**コンテンツ共有エクスペリエンス**: Teams チャネルでコンテンツを共有するために外部サービスとの認証を必要とするアプリは、ヘルプ ドキュメント (または同様のリソース) で、その機能が外部サービスでサポートされている場合にコンテンツの接続を解除または共有解除する方法を明確に示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-161">**Content sharing experiences**: Apps that require authentication with an external service to share content in Teams channels must clearly state in help documentation (or similar resources) how to disconnect or unshare content if that feature is supported on the external service.</span></span> <span data-ttu-id="f7dba-162">これは、コンテンツをアンシェアする機能がTeamsアプリに存在する必要があるわけではありません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-162">This does not mean the ability to unshare content must be present in your Teams app.</span></span>

#### <a name="242-government-community-cloud-listings"></a><span data-ttu-id="f7dba-163">2.4.2 Government Community Cloudリスト</span><span class="sxs-lookup"><span data-stu-id="f7dba-163">2.4.2 Government Community Cloud listings</span></span>

<span data-ttu-id="f7dba-164">Teams ストア内の重複リストを回避しながら、Government Community Cloud (GCC) ユーザーにアプリを配布するには、認証プロセスでユーザーを識別し、GCC固有または予期される URL にルーティングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-164">To distribute your app to Government Community Cloud (GCC) users while avoiding duplicate listings in the Teams store, the authentication process must identify and route users to a GCC-specific or expected URL.</span></span>

### <a name="25-sensitive-content"></a><span data-ttu-id="f7dba-165">2.5 機密コンテンツ</span><span class="sxs-lookup"><span data-stu-id="f7dba-165">2.5 Sensitive content</span></span>

<span data-ttu-id="f7dba-166">アプリは、クレジット カードや金融支払い手段のデータなどの機密データを投稿しないでください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-166">Your app must not post sensitive data, such as credit card or financial payment instrument data.</span></span> <span data-ttu-id="f7dba-167">また、アプリは、そのコンテンツを表示することを意図していない聴衆に、正常性、連絡先の追跡、またはその他の個人を特定できる情報 (PII) を表示してはなりません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-167">The app also must not display health, contact tracing, or other personally identifiable information (PII) to an audience not intended to view that content.</span></span>

<span data-ttu-id="f7dba-168">アプリがファイルや実行可能ファイル (.exe) をユーザーのコンピューターまたは環境にダウンロードする前に、ユーザーに警告します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-168">Warn users before your app downloads any files or executables (.exe) into the user's machine or environment.</span></span>

### <a name="26-financial-information"></a><span data-ttu-id="f7dba-169">2.6 財務情報</span><span class="sxs-lookup"><span data-stu-id="f7dba-169">2.6 Financial information</span></span>

<span data-ttu-id="f7dba-170">アプリは、Teamsインターフェイス内で支払いを行うためにユーザーに求めてはいけません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-170">Apps must not ask users to make payments within the Teams interface.</span></span> <span data-ttu-id="f7dba-171">金融商品の詳細は、ボットインターフェイスを介してユーザーに送信してはなりません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-171">Financial instrument details must not be transmitted to users through a bot interface.</span></span>

<span data-ttu-id="f7dba-172">ユーザーがアプリの使用に同意する前に、使用条件、プライバシー ポリシー、またはプロフィール ページまたは Web サイトで適切な開示を行った場合にのみ、安全な外部支払サービスにリンクすることができます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-172">You may link to secure, external payment services only if you made the appropriate disclosure in your terms of use, privacy policy, or any profile page or website before the user agreed to use the app.</span></span>

<span data-ttu-id="f7dba-173">iOS または Android バージョンの Teams で実行されているアプリは、次のガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-173">Apps running on the iOS or Android version of Teams must adhere to the following guidelines:</span></span>

* <span data-ttu-id="f7dba-174">アプリには、有料版へのアップセルを目的としたアプリ内購入、試用版、またはユーザーが他のコンテンツ、アプリ、アドインを購入または取得できるオンライン ストアへのリンクをアップセルする UI を含めないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-174">Apps must not include in-app purchases, trial offers, or UI that aims to upsell to paid versions or links to online stores where users can purchase or acquire other content, apps, or add-ins.</span></span>
* <span data-ttu-id="f7dba-175">アプリにアカウントが必要な場合、ユーザーはアカウントに無料でサインアップできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-175">If your app requires an account, users must be able to sign up for an account at no charge.</span></span> <span data-ttu-id="f7dba-176">**無料** または **無料** アカウントの使用は禁止されています。</span><span class="sxs-lookup"><span data-stu-id="f7dba-176">The use of the term **free** or **free account** is prohibited.</span></span>
* <span data-ttu-id="f7dba-177">アカウントが無期限に有効になっているか、期間限定でアクティブであるかを判断できますが、アカウントの有効期限が切れた場合は、支払いの必要性を示す UI、テキスト、またはリンクが表示されない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-177">You may determine whether an account is active indefinitely or for a limited time, but if the account expires, no UI, text, or links indicating the need to pay may be shown.</span></span>
* <span data-ttu-id="f7dba-178">アプリのプライバシー ポリシーと利用規約ページには、コマース関連の UI やリンクを含めずにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-178">Your app's privacy policy and terms of use pages must be free of any commerce-related UI or links.</span></span>

## <a name="30-general-functionality-and-performance"></a><span data-ttu-id="f7dba-179">3.0 一般的な機能とパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="f7dba-179">3.0 General functionality and performance</span></span>

### <a name="31-launching-external-functionality"></a><span data-ttu-id="f7dba-180">3.1 外部機能の起動</span><span class="sxs-lookup"><span data-stu-id="f7dba-180">3.1 Launching external functionality</span></span>

<span data-ttu-id="f7dba-181">アプリは、コア ユーザー シナリオのTeamsからユーザーを取り出してはなりません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-181">Apps must not take users out of Teams for core user scenarios.</span></span> <span data-ttu-id="f7dba-182">アプリのコンテンツと操作は、ボット、カード、タスク モジュールなどのTeams機能内で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-182">App content and interactions can occur within Teams capabilities, such as bots, cards, and task modules.</span></span>

<span data-ttu-id="f7dba-183">ユーザーは、外部サイトやアプリではなく、Teamsのどこかにリンクする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-183">You should link users somewhere in Teams and not to an external site or app.</span></span> <span data-ttu-id="f7dba-184">外部機能を必要とするシナリオでは、その機能を起動するための明示的なユーザー権限がアプリに必要です。</span><span class="sxs-lookup"><span data-stu-id="f7dba-184">For scenarios that require external functionality, your app must have explicit user permission to launch that functionality.</span></span>

### <a name="32-compatibility"></a><span data-ttu-id="f7dba-185">3.2 互換性</span><span class="sxs-lookup"><span data-stu-id="f7dba-185">3.2 Compatibility</span></span>

<span data-ttu-id="f7dba-186">アプリは、次のオペレーティング システムおよびブラウザーで完全に機能している必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-186">Apps must be fully functional on the following operating systems and browsers:</span></span>

* <span data-ttu-id="f7dba-187">マイクロソフト Windows 7 以降</span><span class="sxs-lookup"><span data-stu-id="f7dba-187">Microsoft Windows 7 and later</span></span>
* <span data-ttu-id="f7dba-188">macOS 10.10 以降</span><span class="sxs-lookup"><span data-stu-id="f7dba-188">macOS 10.10 and later</span></span>
* <span data-ttu-id="f7dba-189">Microsoft Edge 12 以降</span><span class="sxs-lookup"><span data-stu-id="f7dba-189">Microsoft Edge 12 and later</span></span>
* <span data-ttu-id="f7dba-190">モジラファイアフォックス47.0以降</span><span class="sxs-lookup"><span data-stu-id="f7dba-190">Mozilla Firefox 47.0 and later</span></span>
* <span data-ttu-id="f7dba-191">グーグルクローム51.0以降</span><span class="sxs-lookup"><span data-stu-id="f7dba-191">Google Chrome 51.0 and later</span></span>
* <span data-ttu-id="f7dba-192">iOS 9.0 以降</span><span class="sxs-lookup"><span data-stu-id="f7dba-192">iOS 9.0 and later</span></span>
* <span data-ttu-id="f7dba-193">アンドロイド4.4以降</span><span class="sxs-lookup"><span data-stu-id="f7dba-193">Android 4.4 and later</span></span>

### <a name="33-response-time"></a><span data-ttu-id="f7dba-194">3.3 応答時間</span><span class="sxs-lookup"><span data-stu-id="f7dba-194">3.3 Response time</span></span>

<span data-ttu-id="f7dba-195">Teamsアプリは、機能によって異なる妥当な期間内に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-195">Teams apps must respond within a reasonable timeframe, which varies depending on the capability.</span></span>

* <span data-ttu-id="f7dba-196">タブは 3 秒以内に応答するか、読み込みメッセージまたは警告を表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-196">Tabs must respond within three seconds or display a loading message or warning.</span></span>
* <span data-ttu-id="f7dba-197">ボットは、2 秒以内にユーザー コマンドに応答するか、入力インジケータを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-197">Bots must respond to user commands within two seconds or display a typing indicator.</span></span>
* <span data-ttu-id="f7dba-198">メッセージング拡張機能は、5 秒以内にユーザー コマンドに応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-198">Messaging extensions must respond to user commands within five seconds.</span></span>
* <span data-ttu-id="f7dba-199">通知は、ユーザー操作から 5 秒以内に表示される必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-199">Notifications must display within five seconds of the user action.</span></span>

## <a name="40-app-package-and-store-listing"></a><span data-ttu-id="f7dba-200">4.0 アプリパッケージとストアのリスト</span><span class="sxs-lookup"><span data-stu-id="f7dba-200">4.0 App package and store listing</span></span>

<span data-ttu-id="f7dba-201">アプリ パッケージは正しくフォーマットされ、必要な情報とコンポーネントをすべて含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-201">App packages must be correctly formatted and include all required information and components.</span></span>

### <a name="41-app-manifest"></a><span data-ttu-id="f7dba-202">4.1 アプリ マニフェスト</span><span class="sxs-lookup"><span data-stu-id="f7dba-202">4.1 App manifest</span></span>

<span data-ttu-id="f7dba-203">Teams アプリ マニフェストは、アプリの構成を定義します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-203">The Teams app manifest defines your app's configurations.</span></span>

* <span data-ttu-id="f7dba-204">マニフェストは最新のマニフェスト スキーマに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-204">Your manifest must conform to the latest manifest schema.</span></span> <span data-ttu-id="f7dba-205">詳細については、マニフェスト [リファレンス](~/resources/schema/manifest-schema.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-205">For information, see the [manifest reference](~/resources/schema/manifest-schema.md).</span></span>
* <span data-ttu-id="f7dba-206">アプリにボットまたはメッセージング拡張機能が含まれている場合、マニフェストはボット名、ロゴ、プライバシー ポリシー リンク、サービス利用規約リンクなど、Bot Framework メタデータと一貫性を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-206">If your app includes a bot or messaging extension, your manifest must be consistent with Bot Framework metadata, including bot name, logo, privacy policy link, and terms of service link.</span></span>
* <span data-ttu-id="f7dba-207">アプリで認証に Azure Active Directory (Azure AD) を使用する場合は、マニフェストに Azure AD アプリケーション (クライアント) ID を含めます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-207">If your app uses Azure Active Directory (Azure AD) for authentication, include the Azure AD Application (client) ID in the manifest.</span></span> <span data-ttu-id="f7dba-208">詳細については、 [マニフェスト リファレンス](~/resources/schema/manifest-schema.md#webapplicationinfo)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-208">For more information, see the [manifest reference](~/resources/schema/manifest-schema.md#webapplicationinfo).</span></span>

### <a name="42-app-icons"></a><span data-ttu-id="f7dba-209">4.2 アプリアイコン</span><span class="sxs-lookup"><span data-stu-id="f7dba-209">4.2 App icons</span></span>

<span data-ttu-id="f7dba-210">アイコンは、Teams ストアを参照するときに表示される主な要素の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="f7dba-210">Icons are one of the main elements people see when browsing the Teams store.</span></span> <span data-ttu-id="f7dba-211">アイコンは、アプリのブランドと目的を伝える一方で、次の要件にも準拠する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-211">Your icons should communicate your app's brand and purpose while also adhering to the following requirements:</span></span>

* <span data-ttu-id="f7dba-212">アプリ パッケージには、アプリ アイコンの PNG バージョンが 2 つ含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-212">Your app package must include two PNG versions of your app icon: A color icon and an outline icon.</span></span>
* <span data-ttu-id="f7dba-213">アイコンの色バージョンは、ほとんどのTeamsシナリオで表示され、192x192 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-213">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="f7dba-214">アイコンシンボル(96x96 ピクセル)は、任意の色または色を使用できますが、塗りつぶされた四角形または完全に透明な四角形の背景に置く必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-214">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>
* <span data-ttu-id="f7dba-215">アプリが使用中で、Teamsの左側のアプリ バーに "掲揚" が表示される場合や、ユーザーがアプリのメッセージング拡張機能をピンで固定すると、アイコンのアウトライン バージョンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-215">The outline version of your icon displays when your app is in use and “hoisted” on the app bar on the left side of Teams and when a user pins your app's messaging extension.</span></span> <span data-ttu-id="f7dba-216">32x32 ピクセルで、白色で透明な背景を使用するか、白の背景色を使用して透明にすることもできます (他の色は使用できません)。</span><span class="sxs-lookup"><span data-stu-id="f7dba-216">It must be 32x32 pixels and can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="f7dba-217">アイコンには、記号の周囲に余分なパディングを含めないでください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-217">The icon should not have any extra padding around the symbol.</span></span>
* <span data-ttu-id="f7dba-218">正しいサイズと書式設定されたアイコンは、アプリ パッケージに含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-218">Correctly sized and formatted icons must be included in your app package.</span></span> <span data-ttu-id="f7dba-219">アイコンは、ストアのリストメタデータと共に送信されたものと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-219">The icons also must match what's submitted with the store listing metadata.</span></span>

<span data-ttu-id="f7dba-220">詳細、ベスト プラクティス、および例については、「アプリ アイコンの[ガイドライン](~/concepts/build-and-test/apps-package.md#app-icons)Teams」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-220">For more information, best practices, and examples, see the Teams app [icon guidelines](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="43-app-descriptions"></a><span data-ttu-id="f7dba-221">4.3 アプリの説明</span><span class="sxs-lookup"><span data-stu-id="f7dba-221">4.3 App descriptions</span></span>

<span data-ttu-id="f7dba-222">アプリの短い説明と長い説明が必要です。</span><span class="sxs-lookup"><span data-stu-id="f7dba-222">You must have a short and long description of your app.</span></span> <span data-ttu-id="f7dba-223">アプリの構成とパートナー センターの説明は同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-223">The descriptions in your app configurations and Partner Center must be the same.</span></span>

<span data-ttu-id="f7dba-224">説明は、別のブランド(マイクロソフトが所有または他の方法で)を直接またはほのめかして、別のブランドを損なうべきではありません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-224">Descriptions should not directly or through insinuation disparage another brand (Microsoft owned or otherwise).</span></span> <span data-ttu-id="f7dba-225">説明に、実証できないクレーム (たとえば、"200% の効率向上が保証されている" など) が含まれていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-225">Make sure your description does not include claims that can't be substantiated (for example, "Guaranteed 200 percent increase in efficiency").</span></span>

#### <a name="431-short-description"></a><span data-ttu-id="f7dba-226">4.3.1 簡単な説明</span><span class="sxs-lookup"><span data-stu-id="f7dba-226">4.3.1 Short description</span></span>

<span data-ttu-id="f7dba-227">簡単な説明は、アプリの価値提案を強調し、ターゲットオーディエンスに向けられる簡潔な要約です。</span><span class="sxs-lookup"><span data-stu-id="f7dba-227">A short description is a concise summary of your app that highlights its value proposition and is directed at your target audience.</span></span>

<span data-ttu-id="f7dba-228">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="f7dba-228">**Do:**</span></span>

* <span data-ttu-id="f7dba-229">短い説明は 1 文に保ちます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-229">Keep the short description to one sentence.</span></span>
* <span data-ttu-id="f7dba-230">最も重要な情報を最初に説明します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-230">Put the most important information first.</span></span>
* <span data-ttu-id="f7dba-231">顧客が検索する可能性が高いキーワードを含めます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-231">Include keywords that customers are likely to search for.</span></span>

<span data-ttu-id="f7dba-232">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="f7dba-232">**Don't:**</span></span>

* <span data-ttu-id="f7dba-233">アプリ名を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-233">Repeat your app name.</span></span>
* <span data-ttu-id="f7dba-234">短い説明で **単語アプリ** を使用します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-234">Use the word **app** in the short description.</span></span>

#### <a name="432-long-description"></a><span data-ttu-id="f7dba-235">4.3.2 詳しい説明</span><span class="sxs-lookup"><span data-stu-id="f7dba-235">4.3.2 Long description</span></span>

<span data-ttu-id="f7dba-236">詳しい説明は、アプリのバリュープロポジション、主要な対象者、ターゲット業界を強調する魅力的な説明を提供します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-236">The long description can provide an engaging narrative that highlights your app's value proposition, primary audience, and target industry.</span></span> <span data-ttu-id="f7dba-237">この説明は 4,000 文字まで可能ですが、ほとんどのユーザーは 300 ~ 500 語の間でのみ読み取ります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-237">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

<span data-ttu-id="f7dba-238">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="f7dba-238">**Do:**</span></span>

* <span data-ttu-id="f7dba-239">[マークダウン](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772)を使用して、説明を書式設定します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-239">Use [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) to format your description.</span></span>
* <span data-ttu-id="f7dba-240">アクティブな音声を使用して、ユーザーに直接話す。</span><span class="sxs-lookup"><span data-stu-id="f7dba-240">Use active voice and speak to users directly.</span></span> <span data-ttu-id="f7dba-241">たとえば *、..*</span><span class="sxs-lookup"><span data-stu-id="f7dba-241">For example, *You can ...*.</span></span>
* <span data-ttu-id="f7dba-242">説明を簡単にスキャンできるように、箇条書きの機能を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-242">List features with bullet points so it's easier to scan the description.</span></span>
* <span data-ttu-id="f7dba-243">ユーザーがアプリをインストールする前に、リストおよび関連資料に記載されている機能、機能、および成果物の制限、条件、または例外を明確に記述します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-243">Clearly describe limitations, conditions, or exceptions to the functionality, features, and deliverables described in the listing and related materials before the user installs your app.</span></span> <span data-ttu-id="f7dba-244">アプリがサポートするTeams機能は、リストに記述されている主要な機能に関連する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-244">The Teams capabilities your app supports must relate to the core functions your listing describes.</span></span>
* <span data-ttu-id="f7dba-245">ヘルプまたはサポート リンクを含めます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-245">Include a help or support link.</span></span>
* <span data-ttu-id="f7dba-246">Office 365ではなく **Microsoft 365\*\*\*\*を参照** してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-246">Refer to **Microsoft 365** instead of **Office 365**.</span></span>
* <span data-ttu-id="f7dba-247">**Teams** 参照する必要がある場合は、最初の参照を **Microsoft Teams** として記述します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-247">If you need to reference **Teams**, write the first reference as **Microsoft Teams**.</span></span> <span data-ttu-id="f7dba-248">以降の参照は **、Teams** に短縮できます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-248">Subsequent references can be shortened to **Teams**.</span></span>
* <span data-ttu-id="f7dba-249">アプリがTeams (またはMicrosoft 365) でどのように動作するかを説明する際には、次の言語を使用します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-249">Use the following language when describing how the app works with Teams (or Microsoft 365):</span></span>
  * <span data-ttu-id="f7dba-250">"...Microsoft Teamsと連携する」</span><span class="sxs-lookup"><span data-stu-id="f7dba-250">"... works with Microsoft Teams."</span></span>
  * <span data-ttu-id="f7dba-251">"...Microsoft Teamsと協力する」</span><span class="sxs-lookup"><span data-stu-id="f7dba-251">"... working with Microsoft Teams."</span></span>
  * <span data-ttu-id="f7dba-252">"...Microsoft Teams内で」</span><span class="sxs-lookup"><span data-stu-id="f7dba-252">"... within Microsoft Teams."</span></span>
  * <span data-ttu-id="f7dba-253">"...Microsoft Teamsのために」</span><span class="sxs-lookup"><span data-stu-id="f7dba-253">"... for Microsoft Teams."</span></span>

<span data-ttu-id="f7dba-254">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="f7dba-254">**Don't:**</span></span>

* <span data-ttu-id="f7dba-255">500語を超える。</span><span class="sxs-lookup"><span data-stu-id="f7dba-255">Exceed 500 words.</span></span>
* <span data-ttu-id="f7dba-256">**マイクロソフト** を **MS** または **MSFT** として短縮します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-256">Abbreviate **Microsoft** as **MS** or **MSFT**.</span></span>
* <span data-ttu-id="f7dba-257">アプリがマイクロソフトのスローガンやキャッチフレーズの使用を含む、マイクロソフトからの提供であることを示します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-257">Indicate the app is an offering from Microsoft, including using Microsoft slogans or taglines.</span></span>
* <span data-ttu-id="f7dba-258">所有していない著作権で保護されたブランド名を使用します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-258">Use copyrighted brand names you don't own.</span></span>
* <span data-ttu-id="f7dba-259">入力ミス、文法上の誤り、および不要な大文字と大文字/作を含めます (たとえば、 **ユーザー** の代わりに **ユーザー**)。</span><span class="sxs-lookup"><span data-stu-id="f7dba-259">Include typos, grammatical errors, and unnecessary capitalizations (for example, **Users** instead of **users**).</span></span>
* <span data-ttu-id="f7dba-260">アプリソースへのリンクを含めます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-260">Include links to AppSource.</span></span>
* <span data-ttu-id="f7dba-261">マイクロソフト認定パートナーでない限り、次の言語を使用してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-261">Use the following language unless you are a certified Microsoft partner:</span></span>
  * <span data-ttu-id="f7dba-262">"...Microsoft Teams」と統合</span><span class="sxs-lookup"><span data-stu-id="f7dba-262">"... integrated with Microsoft Teams"</span></span>
  * <span data-ttu-id="f7dba-263">"...と統合されます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-263">"... integrates with ..."</span></span>
  * <span data-ttu-id="f7dba-264">"...のために建てられました.</span><span class="sxs-lookup"><span data-stu-id="f7dba-264">"... built for ..."</span></span>
  * <span data-ttu-id="f7dba-265">"...上に構築.</span><span class="sxs-lookup"><span data-stu-id="f7dba-265">"... built on ..."</span></span>
  * <span data-ttu-id="f7dba-266">"...上で実行されます.</span><span class="sxs-lookup"><span data-stu-id="f7dba-266">"... runs on ..."</span></span>
  * <span data-ttu-id="f7dba-267">"...によって有効に ."</span><span class="sxs-lookup"><span data-stu-id="f7dba-267">"... enabled by ..."</span></span>
  * <span data-ttu-id="f7dba-268">"...の認定を受けています。</span><span class="sxs-lookup"><span data-stu-id="f7dba-268">"... certified for ..."</span></span>
  * <span data-ttu-id="f7dba-269">"...のために開発されました.</span><span class="sxs-lookup"><span data-stu-id="f7dba-269">"... developed for ..."</span></span>
  * <span data-ttu-id="f7dba-270">"...のために設計されています.</span><span class="sxs-lookup"><span data-stu-id="f7dba-270">"... designed for ..."</span></span>

### <a name="44-screenshots"></a><span data-ttu-id="f7dba-271">4.4 スクリーンショット</span><span class="sxs-lookup"><span data-stu-id="f7dba-271">4.4 Screenshots</span></span>

<span data-ttu-id="f7dba-272">スクリーンショットは、アプリの名前、アイコン、説明を補完する、目立つ視覚的プレビューを提供します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-272">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span> <span data-ttu-id="f7dba-273">スクリーンショットについて次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-273">Remember the following about screenshots:</span></span>

* <span data-ttu-id="f7dba-274">リストごとに最大 5 つのスクリーンショットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-274">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="f7dba-275">サポートされるファイルの種類には、PNG、JPEG、GIF などがあります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-275">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="f7dba-276">寸法は 1366x768 ピクセルにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-276">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="f7dba-277">最大サイズは 1,024 KB です。</span><span class="sxs-lookup"><span data-stu-id="f7dba-277">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="f7dba-278">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="f7dba-278">**Do:**</span></span>

* <span data-ttu-id="f7dba-279">アプリの機能 (たとえば、ボットとの通信方法) に注目します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-279">Focus on your app's capabilities (for example, how people can communicate with your bot).</span></span>
* <span data-ttu-id="f7dba-280">アプリを正確に表すコンテンツを含めます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-280">Include content that accurately represents your app.</span></span>
* <span data-ttu-id="f7dba-281">慎重にテキストを使用します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-281">Use text judiciously.</span></span>
* <span data-ttu-id="f7dba-282">[Freshdesk のリスト](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview)の例に似た、ブランドを反映し、マーケティング コンテンツを含む色のフレーム のスクリーンショット (ディメンション要件はスクリーンショットだけでなく画像全体に適用されます)。</span><span class="sxs-lookup"><span data-stu-id="f7dba-282">Frame screenshots with a color that reflects your brand and include marketing content, similar to the [Freshdesk listing](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) example (dimension requirements apply to the whole image and not just the screenshot).</span></span>

<span data-ttu-id="f7dba-283">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="f7dba-283">**Don't:**</span></span>

* <span data-ttu-id="f7dba-284">電話やラップトップなど、特定のデバイスを表示します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-284">Show specific devices, such as phones or laptops.</span></span>
* <span data-ttu-id="f7dba-285">アプリにないクロムまたは UI を表示します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-285">Display chrome or UI that isn't in your app.</span></span>
* <span data-ttu-id="f7dba-286">スクリーンショットにTeamsやブラウザーの UI をキャプチャします。</span><span class="sxs-lookup"><span data-stu-id="f7dba-286">Capture any Teams or browser UI in your screenshots.</span></span>
* <span data-ttu-id="f7dba-287">アプリが外部で使用されていることを示すなど、アプリの実際の UI を不正確に反映するモックアップTeams含めます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-287">Include mockups that inaccurately reflect your app's actual UI, such as showing your app being used outside of Teams.</span></span>

> [!TIP]
> <span data-ttu-id="f7dba-288">ビデオは、ユーザーがアプリを使用する理由を伝える最も効果的な方法です。</span><span class="sxs-lookup"><span data-stu-id="f7dba-288">A video can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="f7dba-289">動画は、ユーザーがリストで最初に表示する内容でもあります(デフォルトでは、スクリーンショットの前にビデオが表示されます)。</span><span class="sxs-lookup"><span data-stu-id="f7dba-289">A video also is the first thing users see in your listing (by default, a video displays before screenshots).</span></span> <span data-ttu-id="f7dba-290">詳細については、「 [ストア登録情報のビデオを作成する」を](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-290">For more information, see [create a video for your store listing](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video).</span></span>

### <a name="45-privacy-policy"></a><span data-ttu-id="f7dba-291">4.5 プライバシーポリシー</span><span class="sxs-lookup"><span data-stu-id="f7dba-291">4.5 Privacy policy</span></span>

<span data-ttu-id="f7dba-292">プライバシー ポリシーは、Teams アプリに固有のポリシー、またはすべてのサービスの全体的なポリシーに固有のポリシーにすることができます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-292">The privacy policy can be specific to your Teams app or an overall policy for all of your services.</span></span>

* <span data-ttu-id="f7dba-293">汎用プライバシー ポリシー テンプレートを使用する場合は、**サービス**、**アプリケーション**、**およびプラットフォーム** を参照して、Teams アプリとサービスまたは Web サイトを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-293">If you use a generic privacy policy template, you must reference **services**, **applications**, and **platforms** to include your Teams app and your service or website.</span></span>
* <span data-ttu-id="f7dba-294">ユーザー データの保存、保存、削除の処理方法を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-294">Must include how you handle user data storage, retention, and deletion.</span></span> <span data-ttu-id="f7dba-295">また、データ保護に使用するセキュリティ制御についても説明する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-295">You also must describe the security controls you use for data protection.</span></span>
* <span data-ttu-id="f7dba-296">連絡先情報を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-296">Must include your contact information.</span></span>
* <span data-ttu-id="f7dba-297">破損している URL、ベータ版またはステージング目的の URL を含めないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-297">Should not contain URLs that are broken or for beta or staging purposes.</span></span>
* <span data-ttu-id="f7dba-298">AppSource へのリンクを含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-298">Must not include links to AppSource.</span></span>

### <a name="46-terms-of-use"></a><span data-ttu-id="f7dba-299">4.6 利用規約</span><span class="sxs-lookup"><span data-stu-id="f7dba-299">4.6 Terms of use</span></span>

<span data-ttu-id="f7dba-300">使用条件は、お客様の提供に固有のものであり、適用可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-300">Your terms of use should be specific and applicable to your offering.</span></span>

### <a name="47-support-links"></a><span data-ttu-id="f7dba-301">4.7 サポートリンク</span><span class="sxs-lookup"><span data-stu-id="f7dba-301">4.7 Support links</span></span>

<span data-ttu-id="f7dba-302">アプリのサポート URL には認証が必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-302">Your app's support URLs should not require authentication.</span></span> <span data-ttu-id="f7dba-303">たとえば、ユーザーは、ユーザーに連絡するためにログインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-303">For example, users should not have to log in to contact you.</span></span>

### <a name="48-localization"></a><span data-ttu-id="f7dba-304">4.8 ローカリゼーション</span><span class="sxs-lookup"><span data-stu-id="f7dba-304">4.8 Localization</span></span>

<span data-ttu-id="f7dba-305">アプリがローカライズをサポートしている場合、アプリ パッケージには、Teams言語設定に基づいて表示される言語翻訳を含むファイルを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-305">If your app supports localization, your app package must include a file with language translations that display based on the Teams language setting.</span></span> <span data-ttu-id="f7dba-306">ファイルは、Teamsのローカリゼーション スキーマに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-306">The file must conform to the Teams localization schema.</span></span> <span data-ttu-id="f7dba-307">詳細については、「 [Teamsのローカライズ スキーマ](~/concepts/build-and-test/apps-localization.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-307">For more information, see the [Teams localization schema](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="50-tabs"></a><span data-ttu-id="f7dba-308">5.0 タブ</span><span class="sxs-lookup"><span data-stu-id="f7dba-308">5.0 Tabs</span></span>

<span data-ttu-id="f7dba-309">アプリにタブが含まれている場合は、これらのガイドラインに準拠していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-309">If your app includes a tab, make sure it adheres to these guidelines.</span></span>

> [!TIP]
> <span data-ttu-id="f7dba-310">高品質なアプリ エクスペリエンスの作成については[、「Teams タブのデザイン ガイドライン](~/tabs/design/tabs.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-310">For information on creating a high-quality app experience, see the [Teams tab design guidelines](~/tabs/design/tabs.md).</span></span>

### <a name="51-setup"></a><span data-ttu-id="f7dba-311">5.1 セットアップ</span><span class="sxs-lookup"><span data-stu-id="f7dba-311">5.1 Setup</span></span>

* <span data-ttu-id="f7dba-312">タブ設定は、新しいユーザーを行き止まってはいけません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-312">Tab setup must not dead-end a new user.</span></span> <span data-ttu-id="f7dba-313">アクションまたはワークフローを完了する方法に関するメッセージを提供します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-313">Provide a message on how to complete the action or workflow.</span></span>
* <span data-ttu-id="f7dba-314">認証はタブのセットアップ中に行われ、その後は行われません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-314">Authentication should happen during tab setup and not after.</span></span>

### <a name="52-views"></a><span data-ttu-id="f7dba-315">5.2 ビュー</span><span class="sxs-lookup"><span data-stu-id="f7dba-315">5.2 Views</span></span>

* <span data-ttu-id="f7dba-316">サインイン画面領域では、大きなロゴを使用したり、Web ページ全体を表示したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-316">The sign-in screen area must not use large logos or display an entire webpage.</span></span>
* <span data-ttu-id="f7dba-317">コンテンツは、複数のタブに分け、簡素化できます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-317">Content can be simplified by breaking it down across multiple tabs.</span></span>
* <span data-ttu-id="f7dba-318">タブには、重複するヘッダーを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-318">Tabs should not have a duplicate header.</span></span> <span data-ttu-id="f7dba-319">タブフレームワークには既にアプリのアイコンと名前が表示されているため、iframeからロゴを削除します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-319">Remove the logo from the iframe since the tab framework already displays the app icon and name.</span></span>

### <a name="53-navigation"></a><span data-ttu-id="f7dba-320">5.3 ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="f7dba-320">5.3 Navigation</span></span>

* <span data-ttu-id="f7dba-321">タブには、3 つ以上のナビゲーション レベルを設定することはできません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-321">Tabs must not have more than three levels of navigation.</span></span>
* <span data-ttu-id="f7dba-322">タブは、プライマリTeams ナビゲーションと競合するナビゲーションを提供できません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-322">Tabs must not provide navigation that conflicts with the primary Teams navigation.</span></span>
* <span data-ttu-id="f7dba-323">タブの 2 番目のページと 3 番目のページは、階層リンクまたは左ナビゲーションを介して移動するメイン タブ領域のレベル 2 およびレベル 3 ビューで開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-323">The secondary and tertiary pages in a tab must be opened in a level two and level three view in the main tab area, which is navigated via breadcrumbs or left nav.</span></span> <span data-ttu-id="f7dba-324">タブナビゲーションを支援するために、次のコンポーネントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-324">You can also include the following components to aid tab navigation:</span></span>
    * <span data-ttu-id="f7dba-325">戻るボタン</span><span class="sxs-lookup"><span data-stu-id="f7dba-325">Back buttons</span></span>
    * <span data-ttu-id="f7dba-326">ページ ヘッダー</span><span class="sxs-lookup"><span data-stu-id="f7dba-326">Page headers</span></span>
    * <span data-ttu-id="f7dba-327">ハンバーガーメニュー</span><span class="sxs-lookup"><span data-stu-id="f7dba-327">Hamburger menus</span></span>
* <span data-ttu-id="f7dba-328">タブには水平スクロールを含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-328">Tab should not have horizontal scroll.</span></span>
* <span data-ttu-id="f7dba-329">タブ内のディープリンクは、外部のWebページにリンクするのではなく、Teams内のどこかへリンクする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-329">Deep links in tabs must not link to an external webpage but somewhere within Teams.</span></span> <span data-ttu-id="f7dba-330">たとえば、タスク モジュールやその他のタブなどです。</span><span class="sxs-lookup"><span data-stu-id="f7dba-330">For example, task modules or other tabs.</span></span>
* <span data-ttu-id="f7dba-331">ユーザーがコア アプリ エクスペリエンスの外部Teamsを移動することを許可するタブはありません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-331">Tabs should not allow users to navigate outside Teams for the core app experience.</span></span>

### <a name="54-usability"></a><span data-ttu-id="f7dba-332">5.4 使いやすさ</span><span class="sxs-lookup"><span data-stu-id="f7dba-332">5.4 Usability</span></span>

* <span data-ttu-id="f7dba-333">タブは、既存の Web サイトをホストするだけの価値を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-333">Tabs must provide value beyond just hosting an existing website.</span></span>
* <span data-ttu-id="f7dba-334">ユーザーは、タブ内の最後の操作を元に戻すことができる必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-334">Users must be able to undo their last action in the tab.</span></span>
* <span data-ttu-id="f7dba-335">個人コンテキストのタブは、アプリの共有インスタンスからコンテンツを集約できます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-335">Tabs in a personal context may aggregate content from shared instances of the app.</span></span>
* <span data-ttu-id="f7dba-336">タブは、Teamsテーマに対応する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-336">Tabs must be responsive to Teams themes.</span></span> <span data-ttu-id="f7dba-337">ユーザーがテーマを変更する場合、アプリのテーマに選択内容が反映されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-337">When a user changes the theme, the app's theme must reflect the selection.</span></span>
* <span data-ttu-id="f7dba-338">タブは、Teams フォント、タイプ ランプ、カラー パレット、グリッド システム、モーション、音声のトーンなど、Teams スタイルのコンポーネントを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-338">Tabs must use Teams-styled components, such as, Teams fonts, type ramps, color palettes, grid system, motion, tone of voice, and so on whenever possible.</span></span>
* <span data-ttu-id="f7dba-339">**設定** タブを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-339">You must include a **Settings** tab.</span></span>
* <span data-ttu-id="f7dba-340">タブは、ページ内のナビゲーション、ダイアログの位置と使用、情報階層などの対話設計Teams従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-340">Tabs must follow Teams interaction design, such as, in-page navigation, position and use of dialogs, information hierarchies, and so on whenever possible.</span></span>
* <span data-ttu-id="f7dba-341">iframe のタブコンテンツには、Teamsコア機能を模倣する機能を含む必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-341">Tab content in the iframe must not include features that mimic Teams core capabilities.</span></span> <span data-ttu-id="f7dba-342">たとえば、ボット、メッセージング拡張機能、通話、会議などです。</span><span class="sxs-lookup"><span data-stu-id="f7dba-342">For example, bots, messaging extensions, calling, meeting, and so on.</span></span>

> [!TIP]
>
> * <span data-ttu-id="f7dba-343">個人用のボットを個人用タブと一緒に含めます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-343">Include a personal bot alongside a personal tab.</span></span>
> * <span data-ttu-id="f7dba-344">ユーザーが個人用タブからコンテンツを共有できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f7dba-344">Allow users to share content from their personal tab.</span></span>

## <a name="60-bots"></a><span data-ttu-id="f7dba-345">6.0 ボット</span><span class="sxs-lookup"><span data-stu-id="f7dba-345">6.0 Bots</span></span>

<span data-ttu-id="f7dba-346">アプリにボットが含まれている場合は、これらのガイドラインに準拠していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-346">If your app includes a bot, make sure it adheres to these guidelines.</span></span>

> [!TIP]
> <span data-ttu-id="f7dba-347">高品質なアプリ エクスペリエンスの作成については[、「Teamsのボット設計ガイドライン](~/bots/design/bots.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-347">For information on creating a high-quality app experience, see the [Teams bot design guidelines](~/bots/design/bots.md).</span></span>

### <a name="61-bot-commands"></a><span data-ttu-id="f7dba-348">6.1 ボットコマンド</span><span class="sxs-lookup"><span data-stu-id="f7dba-348">6.1 Bot commands</span></span>

<span data-ttu-id="f7dba-349">ユーザー入力の分析とユーザーの意図の予測は困難です。</span><span class="sxs-lookup"><span data-stu-id="f7dba-349">Analyzing user input and predicting user intent is difficult.</span></span> <span data-ttu-id="f7dba-350">Bot コマンドは、ユーザーが理解している一連の単語やフレーズをユーザーに提供するので、ユーザー (およびボット) は推測する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-350">Bot commands provide users a set of words or phrases your bot understands so they (and your bot) don't have to guess.</span></span>

* <span data-ttu-id="f7dba-351">アプリの構成でサポートされているボット コマンドの一覧表示を強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f7dba-351">Listing supported bot commands in your app configurations is highly recommended.</span></span> <span data-ttu-id="f7dba-352">これらのコマンドは、ユーザーがボットにメッセージを送信しようとすると、作成ボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-352">These commands display in the compose box when a user tries to message your bot.</span></span>
* <span data-ttu-id="f7dba-353">ボットがサポートするすべてのコマンドは **、Hi** **、Hello、\*\*\*\*および Help** コマンドを含めて、正しく動作する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-353">All commands that your bot supports must work correctly, including the **Hi**, **Hello**, and **Help** command.</span></span>

> [!TIP]
> <span data-ttu-id="f7dba-354">個人ボットの場合は、ボットができることについて詳しく説明する **[ヘルプ** ] タブを追加します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-354">For personal bots, include a **Help** tab that further describes what your bot can do.</span></span>

### <a name="62-bot-welcome-messages"></a><span data-ttu-id="f7dba-355">6.2 ボットのウェルカムメッセージ</span><span class="sxs-lookup"><span data-stu-id="f7dba-355">6.2 Bot welcome messages</span></span>

* <span data-ttu-id="f7dba-356">ボットは、ほとんどの場合、最初の実行時にウェルカム メッセージを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-356">Bots should almost always send a welcome message during first run.</span></span> <span data-ttu-id="f7dba-357">最適なエクスペリエンスを得るためには、メッセージにボットの価値提案、ボットの構成方法、サポートされているすべてのボット コマンドの簡単な説明を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-357">For the best experience, the message should include the value proposition of your bot, how to configure the bot, and briefly describe all supported bot commands.</span></span> <span data-ttu-id="f7dba-358">使いやすさを高めるため、アダプティブ カードを使用してボタンを使用してメッセージを表示できます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-358">You can display the message using an Adaptive Card with buttons for better usability.</span></span> <span data-ttu-id="f7dba-359">詳細については、「 [ボットのウェルカム メッセージをトリガーする方法](~/bots/how-to/conversations/send-proactive-messages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-359">For more information, see [how to trigger a bot welcome message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="f7dba-360">特にボットが個人用で使用でき、同様のアクションを実行する場合は、チャネルやチャットのボットウェルカム メッセージは、最初の実行時にオプションです。</span><span class="sxs-lookup"><span data-stu-id="f7dba-360">Bot welcome messages in channels and chats are optional during first run, especially if the bot is available for personal use and performs similar actions.</span></span> <span data-ttu-id="f7dba-361">ボットがウェルカム メッセージを送信する場合、これらのメッセージをユーザーに個別に送信しないでください (これは [スパムと見なされます](#63-bot-message-spamming))。</span><span class="sxs-lookup"><span data-stu-id="f7dba-361">If your bot does send welcome messages, it must not send these to users individually (this is considered [spamming](#63-bot-message-spamming)).</span></span> <span data-ttu-id="f7dba-362">メッセージには、ボットを追加したユーザーも示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-362">The message should also mention the person who added the bot.</span></span>
* <span data-ttu-id="f7dba-363">通知のみのボットは、ユーザーのメッセージに返信しないことを通知するウェルカム メッセージを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-363">Notification-only bots must send a welcome message that conveys it will not reply to users' messages.</span></span>

> [!TIP]
> <span data-ttu-id="f7dba-364">個々のユーザーへのウェルカム メッセージでは、カルーセル ツアーを使用して、ボットやその他のアプリ機能の概要を効果的に把握できます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-364">In welcome messages to individual users, a carousel tour can provide an effective overview of your bot and any other app features.</span></span> <span data-ttu-id="f7dba-365">ボタンを含めると、ユーザーはボットコマンドを試すことができます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-365">Including buttons the let users try bot commands is encouraged.</span></span> <span data-ttu-id="f7dba-366">たとえば、 **タスクの作成**。</span><span class="sxs-lookup"><span data-stu-id="f7dba-366">For example, **Create a task**.</span></span>

### <a name="63-bot-message-spamming"></a><span data-ttu-id="f7dba-367">6.3 ボットメッセージスパム</span><span class="sxs-lookup"><span data-stu-id="f7dba-367">6.3 Bot message spamming</span></span>

<span data-ttu-id="f7dba-368">ボットは、複数のメッセージを連続して送信してユーザーにスパムを送信してはなりません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-368">Bots must not spam users by sending multiple messages in short succession.</span></span>

* <span data-ttu-id="f7dba-369">**チャンネルやチャットでメッセージを送信** する : 別の投稿を作成してユーザーにスパムを送信しないでください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-369">**Bot messages in channels and chats**: Don't spam users by creating separate posts.</span></span> <span data-ttu-id="f7dba-370">同じスレッド内に返信を含む 1 つの投稿を作成します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-370">Create a single post with replies in the same thread.</span></span>
* <span data-ttu-id="f7dba-371">**個人アプリでのボットメッセージ**: 複数のメッセージを連続して送信しないでください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-371">**Bot messages in personal apps**: Don't send multiple messages in quick succession.</span></span> <span data-ttu-id="f7dba-372">完全な情報を含む 1 つのメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-372">Send one message with complete information.</span></span> <span data-ttu-id="f7dba-373">複数のスレッドを使用して 1 つのワークフローを完了しないようにします。</span><span class="sxs-lookup"><span data-stu-id="f7dba-373">Avoid multi-turn conversations to complete a single workflow.</span></span> <span data-ttu-id="f7dba-374">代わりに、フォーム (またはタスク モジュール) を使用して、ユーザーからのすべての入力を一度に収集することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-374">Instead, consider using a form (or task module) to collect all inputs from a user at one time.</span></span>
* <span data-ttu-id="f7dba-375">**ウェルカムメッセージ**: 同じウェルカムメッセージを定期的に繰り返すのは許可されておらず、スパムと見なされます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-375">**Welcome messages**: Repeating the same welcome message over regular intervals is not allowed and considered spamming.</span></span> <span data-ttu-id="f7dba-376">たとえば、新しいメンバーをチームに追加した場合、他のメンバーにウェルカム メッセージをスパムしないでください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-376">For example, when a new member is added to a team, don't spam the other members with a welcome message.</span></span> <span data-ttu-id="f7dba-377">代わりに、新しいメンバーに個人的にメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-377">Message the new member personally instead.</span></span>

### <a name="64-bot-notifications"></a><span data-ttu-id="f7dba-378">6.4 ボット通知</span><span class="sxs-lookup"><span data-stu-id="f7dba-378">6.4 Bot notifications</span></span>

<span data-ttu-id="f7dba-379">ボット通知には、ボットに定義するスコープ (チーム、チャット、または個人) に関連するコンテンツを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-379">Bot notifications must include content relevant for the scope you define for the bot (team, chat, or personal).</span></span>

### <a name="65-bots-and-adaptive-cards"></a><span data-ttu-id="f7dba-380">6.5 ボットとアダプティブカード</span><span class="sxs-lookup"><span data-stu-id="f7dba-380">6.5 Bots and Adaptive Cards</span></span>

<span data-ttu-id="f7dba-381">アダプティブ カードは、ボット メッセージを表示する方法として推奨されています。</span><span class="sxs-lookup"><span data-stu-id="f7dba-381">Adaptive Cards are a highly recommended way to display bot messages.</span></span> <span data-ttu-id="f7dba-382">カードは軽量で、1~3 個のアクションのみを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-382">Your cards must be lightweight and include only 1-3 actions.</span></span> <span data-ttu-id="f7dba-383">さらにコンテンツを表示する必要がある場合は、タスク モジュールまたはタブの使用を検討してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-383">If you need to display more content, consider using a task module or tab.</span></span>

<span data-ttu-id="f7dba-384">詳細については、以下のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-384">See the following resources for more information:</span></span>

* [<span data-ttu-id="f7dba-385">アダプティブ カードをデザインする</span><span class="sxs-lookup"><span data-stu-id="f7dba-385">Designing Adaptive Cards</span></span>](~/task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="f7dba-386">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="f7dba-386">Cards reference</span></span>](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="70-messaging-extensions"></a><span data-ttu-id="f7dba-387">7.0 メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7dba-387">7.0 Messaging extensions</span></span>

<span data-ttu-id="f7dba-388">アプリにメッセージング拡張機能が含まれている場合は、これらのガイドラインに準拠していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-388">If your app includes a messaging extension, make sure it adheres to these guidelines.</span></span>

> [!TIP]
> <span data-ttu-id="f7dba-389">高品質なアプリ エクスペリエンスの作成については、「[メッセージング拡張機能のデザイン ガイドラインTeams」](~/messaging-extensions/design/messaging-extension-design.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-389">For information on creating a high-quality app experience, see the [Teams messaging extension design guidelines](~/messaging-extensions/design/messaging-extension-design.md).</span></span>

### <a name="71-action-commands"></a><span data-ttu-id="f7dba-390">7.1 アクションコマンド</span><span class="sxs-lookup"><span data-stu-id="f7dba-390">7.1 Action commands</span></span>

<span data-ttu-id="f7dba-391">アクション ベースのメッセージング拡張機能は、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-391">Action-based messaging extensions should do the following:</span></span>

* <span data-ttu-id="f7dba-392">サインインなどの中間ステップを完了せずに、メッセージに対するアクションをトリガーできるようにします。</span><span class="sxs-lookup"><span data-stu-id="f7dba-392">Allow users to trigger actions on a message without completing intermediate steps, such as signing in.</span></span>
* <span data-ttu-id="f7dba-393">メッセージ コンテキストを次の作業状態に渡します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-393">Pass the message context to the next work state.</span></span>

### <a name="72-preview-links-link-unfurling"></a><span data-ttu-id="f7dba-394">7.2 プレビューリンク(リンクの展開)</span><span class="sxs-lookup"><span data-stu-id="f7dba-394">7.2 Preview links (link unfurling)</span></span>

<span data-ttu-id="f7dba-395">メッセージング拡張機能では、[Teams作成] ボックスで認識されたリンクをプレビューする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-395">Messaging extensions should preview recognized links in the Teams compose box.</span></span> <span data-ttu-id="f7dba-396">コントロールの外にあるドメイン (絶対 URL またはワイルドカード) は追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-396">Do not add domains that are outside your control (either absolute URLs or wildcards).</span></span> <span data-ttu-id="f7dba-397">たとえば、 `yourapp.onmicrosoft.com` 有効ですが `*.onmicrosoft.com` 、無効です。</span><span class="sxs-lookup"><span data-stu-id="f7dba-397">For example, `yourapp.onmicrosoft.com` is valid but `*.onmicrosoft.com` is not valid.</span></span> <span data-ttu-id="f7dba-398">トップレベル ドメインも禁止されています (たとえば、 `*.com` `*.org` または )。</span><span class="sxs-lookup"><span data-stu-id="f7dba-398">Top-level domains also are prohibited (for example, `*.com` or `*.org`).</span></span>

### <a name="73-search-commands"></a><span data-ttu-id="f7dba-399">7.3 検索コマンド</span><span class="sxs-lookup"><span data-stu-id="f7dba-399">7.3 Search commands</span></span>

* <span data-ttu-id="f7dba-400">検索ベースのメッセージング拡張機能は、ユーザーが効果的に検索するためのテキストを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-400">Search-based messaging extensions must provide text that helps users effectively search.</span></span>
* <span data-ttu-id="f7dba-401">@mention実行可能ファイルは、明確で、理解しやすく、読みやすくなければなりません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-401">@mention executables must be clear, easy to understand, and readable.</span></span>

## <a name="80-task-modules"></a><span data-ttu-id="f7dba-402">8.0 タスクモジュール</span><span class="sxs-lookup"><span data-stu-id="f7dba-402">8.0 Task modules</span></span>

<span data-ttu-id="f7dba-403">タスク モジュールには、アイコンと、関連付けられているアプリの短い名前を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-403">A task module must include an icon and the short name of the app it's associated with.</span></span>

> [!TIP]
> <span data-ttu-id="f7dba-404">高品質なアプリ エクスペリエンスの作成については[、「Teams タスク モジュール設計ガイドライン](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-404">For information on creating a high-quality app experience, see the [Teams task module design guidelines](~/task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="90-meeting-extensions"></a><span data-ttu-id="f7dba-405">9.0 会議の拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7dba-405">9.0 Meeting extensions</span></span>

<span data-ttu-id="f7dba-406">アプリに会議の拡張機能が含まれている場合は、これらのガイドラインに準拠していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f7dba-406">If your app includes a meeting extension, make sure it adheres to these guidelines.</span></span>

> [!TIP]
> <span data-ttu-id="f7dba-407">高品質なアプリ エクスペリエンスの作成については[、「Teamsミーティング拡張設計ガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-407">For information on creating a high-quality app experience, see the [Teams meeting extension design guidelines](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).</span></span>

### <a name="91-pre--and-post-meeting-experience"></a><span data-ttu-id="f7dba-408">9.1 会議前および会議後の経験</span><span class="sxs-lookup"><span data-stu-id="f7dba-408">9.1 Pre- and post-meeting experience</span></span>

* <span data-ttu-id="f7dba-409">会議前および会議後の画面は、一般的なタブ設計ガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-409">Pre- and post-meeting screens must adhere to general tab design guidelines.</span></span> <span data-ttu-id="f7dba-410">詳細については[、Teams設計ガイドライン](~/tabs/design/tabs.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-410">For more information, see the [Teams design guidelines](~/tabs/design/tabs.md).</span></span>
* <span data-ttu-id="f7dba-411">タブには水平スクロールを含めないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-411">Tabs must not have horizontal scrolling.</span></span>
* <span data-ttu-id="f7dba-412">複数の項目を表示する場合、タブは整理されたレイアウトにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-412">Tabs should have an organized layout when displaying multiple items.</span></span> <span data-ttu-id="f7dba-413">たとえば、10 以上のアンケートやアンケート。</span><span class="sxs-lookup"><span data-stu-id="f7dba-413">For instance, more than 10 polls or surveys.</span></span> <span data-ttu-id="f7dba-414">[サンプルレイアウト](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-414">See an [example layout](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).</span></span>
* <span data-ttu-id="f7dba-415">アンケートまたはアンケートの結果がエクスポートされたときに、アプリは「結果が正常にダウンロードされました」と通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-415">Your app must notify users when the results of a survey or poll are exported by stating, "Results successfully downloaded".</span></span>

### <a name="92-in-meeting-experience"></a><span data-ttu-id="f7dba-416">9.2 会議中の経験</span><span class="sxs-lookup"><span data-stu-id="f7dba-416">9.2 In-meeting experience</span></span>

* <span data-ttu-id="f7dba-417">アプリは、会議中にのみ暗いテーマを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-417">Apps must only use a dark theme during meetings.</span></span> <span data-ttu-id="f7dba-418">詳細については[、Teams設計ガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-418">For more information, see the [Teams design guidelines](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming).</span></span>
* <span data-ttu-id="f7dba-419">会議中にアプリアイコンの上にマウスを移動すると、ツールヒントにアプリ名が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-419">A tooltip should display the app name when hovering over the app icon during meetings.</span></span>
* <span data-ttu-id="f7dba-420">メッセージング拡張機能は、会議中は外部の会議と同じように機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-420">Messaging extensions must function the same during meetings as they do outside meetings.</span></span>

### <a name="93-in-meeting-tabs"></a><span data-ttu-id="f7dba-421">9.3 会議中タブ</span><span class="sxs-lookup"><span data-stu-id="f7dba-421">9.3 In-meeting tabs</span></span>

* <span data-ttu-id="f7dba-422">応答性が必要です。</span><span class="sxs-lookup"><span data-stu-id="f7dba-422">Must be responsive.</span></span> <span data-ttu-id="f7dba-423">パディングとコンポーネントサイズを維持してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-423">Make sure to maintain padding and component sizes.</span></span>
* <span data-ttu-id="f7dba-424">ナビゲーションのレイヤーが複数ある場合は、戻るボタンが必要です。</span><span class="sxs-lookup"><span data-stu-id="f7dba-424">Must have a back button if there is more than one layer of navigation.</span></span>
* <span data-ttu-id="f7dba-425">複数の閉じるボタンまたは閉じるボタンを含めないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-425">Must not include more than one dismiss or close button.</span></span> <span data-ttu-id="f7dba-426">既に組み込みのヘッダー ボタンがタブを閉じるため、ユーザーが混乱する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-426">This may confuse users since there's already a built-in header button to dismiss the tab.</span></span>
* <span data-ttu-id="f7dba-427">水平スクロールを含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-427">Must not have horizontal scrolling.</span></span>

### <a name="94-in-meeting-dialogs"></a><span data-ttu-id="f7dba-428">9.4 インミーティングダイアログ</span><span class="sxs-lookup"><span data-stu-id="f7dba-428">9.4 In-meeting dialogs</span></span>

* <span data-ttu-id="f7dba-429">軽くてタスク指向のシナリオでは、控えめに使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-429">Should be used sparingly and for scenarios that are light and task-oriented.</span></span>
* <span data-ttu-id="f7dba-430">コンテンツを 1 つの列に表示する必要があり、複数のナビゲーション レベルを持たない必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-430">Must display content in a single column and not have multiple navigation levels.</span></span>
* <span data-ttu-id="f7dba-431">タスク モジュールを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-431">Must not use task modules.</span></span>
* <span data-ttu-id="f7dba-432">会議ステージの中心に合わせる必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-432">Must align with the center of the meeting stage.</span></span>
* <span data-ttu-id="f7dba-433">ユーザーがボタンを選択するか、アクションを実行すると、閉じられます。</span><span class="sxs-lookup"><span data-stu-id="f7dba-433">Should be dismissed once a user selects a button or performs an action.</span></span>

## <a name="100-notifications"></a><span data-ttu-id="f7dba-434">10.0 通知</span><span class="sxs-lookup"><span data-stu-id="f7dba-434">10.0 Notifications</span></span>

<span data-ttu-id="f7dba-435">[Microsoft Graph によって提供されるアクティビティ フィード API をアプリが](/graph/teams-send-activityfeednotifications)使用している場合は、次のガイドラインに従っていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="f7dba-435">If your app uses the [activity feed APIs provided by Microsoft Graph](/graph/teams-send-activityfeednotifications), make sure it adheres to the following guidelines.</span></span>

### <a name="101-general"></a><span data-ttu-id="f7dba-436">10.1 一般</span><span class="sxs-lookup"><span data-stu-id="f7dba-436">10.1 General</span></span>

* <span data-ttu-id="f7dba-437">アプリの構成で指定されたすべての通知トリガーは、アプリで通知を受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-437">All the notification triggers specified in your app configurations should get a notification in the app.</span></span>
* <span data-ttu-id="f7dba-438">通知は、アプリに対して構成されているサポート対象言語ごとにローカライズする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-438">Notifications must be localized per the supported languages configured for your app.</span></span>
* <span data-ttu-id="f7dba-439">通知は、ユーザー操作から 5 秒以内に表示される必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-439">Notifications must display within five seconds of user action.</span></span>

### <a name="102-avatars"></a><span data-ttu-id="f7dba-440">10.2 アバター</span><span class="sxs-lookup"><span data-stu-id="f7dba-440">10.2 Avatars</span></span>

* <span data-ttu-id="f7dba-441">通知アバターは、アプリの色アイコンと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-441">The notification avatar should match your app's color icon.</span></span>
* <span data-ttu-id="f7dba-442">ユーザーがトリガーする通知には、ユーザーのアバターを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-442">Notifications triggered by a user should include the user's avatar.</span></span>

### <a name="103-spamming"></a><span data-ttu-id="f7dba-443">10.3 スパム</span><span class="sxs-lookup"><span data-stu-id="f7dba-443">10.3 Spamming</span></span>

* <span data-ttu-id="f7dba-444">アプリは、ユーザーに 1 分間に 10 を超える通知を送信することはできません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-444">Apps must not send more than 10 notifications per minute to a user.</span></span>
* <span data-ttu-id="f7dba-445">ボットとアクティビティ フィードは、重複した通知をトリガーしないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-445">Bots and the activity feed should not trigger duplicate notifications.</span></span>
* <span data-ttu-id="f7dba-446">通知は、ユーザーに何らかの価値を提供する必要があり、些細なイベントや無関係なイベントには使用されません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-446">Notifications must provide some value to users and not be used for trivial or irrelevant events.</span></span>

### <a name="104-navigation-and-layout"></a><span data-ttu-id="f7dba-447">10.4 ナビゲーションとレイアウト</span><span class="sxs-lookup"><span data-stu-id="f7dba-447">10.4 Navigation and layout</span></span>

* <span data-ttu-id="f7dba-448">通知は、アクティビティ フィードのレイアウトとエクスペリエンスTeamsに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-448">Notifications must adhere to the Teams activity feed layout and experience.</span></span>
* <span data-ttu-id="f7dba-449">通知を選択する際、ユーザーはTeams内の関連コンテンツに誘導され、Teamsエクスペリエンスから除外される必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7dba-449">When selecting a notification, the user must be directed to relevant content within Teams and not taken out of the Teams experience.</span></span>

## <a name="110-advertising"></a><span data-ttu-id="f7dba-450">11.0 広告</span><span class="sxs-lookup"><span data-stu-id="f7dba-450">11.0 Advertising</span></span>

<span data-ttu-id="f7dba-451">動的広告、バナー広告、メッセージ内の広告などの広告を表示することはできません。</span><span class="sxs-lookup"><span data-stu-id="f7dba-451">Apps must not display advertising, including dynamic ads, banner ads, and ads in messages.</span></span>

## <a name="see-also"></a><span data-ttu-id="f7dba-452">関連項目</span><span class="sxs-lookup"><span data-stu-id="f7dba-452">See also</span></span>

[<span data-ttu-id="f7dba-453">4.0 アプリパッケージとストアのリスト</span><span class="sxs-lookup"><span data-stu-id="f7dba-453">4.0 App package and store listing</span></span>](#40-app-package-and-store-listing)

## <a name="next-step"></a><span data-ttu-id="f7dba-454">次の手順</span><span class="sxs-lookup"><span data-stu-id="f7dba-454">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7dba-455">パートナー センター アカウントを作成する</span><span class="sxs-lookup"><span data-stu-id="f7dba-455">Create a Partner Center account</span></span>](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
