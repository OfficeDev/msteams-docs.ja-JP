---
title: Microsoft Teams アプリ承認プロセスガイダンス
description: Microsoft Teams アプリストアに公開されたアプリを取得するための承認プロセスについて説明します。
keywords: teams 発行ストア office 発行アプリソース
ms.openlocfilehash: b3efdf81aa4ecf79fb19375cb4ee5377fcad2f7f
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652078"
---
# <a name="understanding-the-appsource-submission-process"></a><span data-ttu-id="a97c5-104">AppSource 送信プロセスについて</span><span class="sxs-lookup"><span data-stu-id="a97c5-104">Understanding the AppSource submission process</span></span>

## <a name="teams-app-submission"></a><span data-ttu-id="a97c5-105">Teams アプリの提出</span><span class="sxs-lookup"><span data-stu-id="a97c5-105">Teams app submission</span></span>

<span data-ttu-id="a97c5-106">アプリを [Microsoft AppSource](https://appsource.microsoft.com) に発行することで、Teams アプリカタログと web 上で使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-106">Publishing  your app to [Microsoft AppSource](https://appsource.microsoft.com) makes it available in the Teams app catalog and on the web.</span></span> <span data-ttu-id="a97c5-107">高レベルでは、アプリを AppSource に提出するプロセスは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-107">At a high level, the process for submitting your app to AppSource is:</span></span>

1. <span data-ttu-id="a97c5-108">[デザインガイドライン](~/concepts/design/understand-use-cases.md)に従ってアプリを開発します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-108">Develop your app following our [design guidelines](~/concepts/design/understand-use-cases.md).</span></span> <span data-ttu-id="a97c5-109">タブは、 [タブデザインガイドライン](~/tabs/design/tabs.md)に準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-109">Tabs should follow our [tab design guidelines](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="a97c5-110">Bot は [bot 設計ガイドライン](~/bots/design/bots.md)に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-110">Bots should follow the [bot design guidelines](~/bots/design/bots.md).</span></span>
1. <span data-ttu-id="a97c5-111">アプリが Microsoft Teams のアプリの [検証ポリシー](/legal/marketplace/certification-policies) を満たしていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-111">Ensure your app meets the app [validation policies](/legal/marketplace/certification-policies) for Microsoft Teams.</span></span>
1. <span data-ttu-id="a97c5-112">[パートナーセンター](https://support.microsoft.com/help/4499930/partner-center-overview)で[開発者アカウントをセットアップ](/office/dev/store/open-a-developer-account)します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-112">[Set up a developer account](/office/dev/store/open-a-developer-account) in [Partner Center](https://support.microsoft.com/help/4499930/partner-center-overview).</span></span> <span data-ttu-id="a97c5-113">下記の FAQ セクションで、[パートナーセンターアカウントを作成する方法](#how-do-i-create-a-partner-center-account)に*ついても参照して*ください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-113">*See also* [How do I create a Partner Center account](#how-do-i-create-a-partner-center-account) in the FAQ section, below.</span></span>
1. <span data-ttu-id="a97c5-114">[提出のチェックリスト](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)に従って、アプリを提出する準備をします。</span><span class="sxs-lookup"><span data-stu-id="a97c5-114">Prepare your app for submission by following our [submission checklist](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).</span></span>
1. <span data-ttu-id="a97c5-115">[アプリの送信を成功させるためのヒントを](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)確認します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-115">Review our [tips for a successful app submission](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md).</span></span>
1. <span data-ttu-id="a97c5-116">[パートナーセンターを使用して、Appsource](/office/dev/store/use-partner-center-to-submit-to-appsource)にパッケージを提出します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-116">Submit your package to [AppSource through Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource).</span></span>
1. <span data-ttu-id="a97c5-117">パートナーセンターダッシュボードで承認プロセスを追跡します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-117">Track the approval process on your Partner Center dashboard.</span></span> <span data-ttu-id="a97c5-118">*「* [Partner Center の概要](https://support.microsoft.com/help/4499930/partner-center-overview)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-118">*See* [Partner Center Overview](https://support.microsoft.com/help/4499930/partner-center-overview).</span></span>
1. <span data-ttu-id="a97c5-119">投稿後: 公開された [アプリの管理とサポート](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)に関するガイダンスを確認してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-119">Post submission — review our guidance for [Maintaining and supporting your published app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).</span></span>

>[!NOTE]
>
>- <span data-ttu-id="a97c5-120">Teams アプリに bot が含まれている場合は、ボット開発者フレームワーク [の倫理](https://aka.ms/bf-conduct)規定に準拠する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-120">If your Teams app contains a bot, you must comply with the Bot Developer Framework [Code of Conduct](https://aka.ms/bf-conduct).</span></span>
>- <span data-ttu-id="a97c5-121">アプリに Office 365 コネクタが含まれている場合は、追加の用語が適用されることがあります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-121">If your app contains an Office 365 Connector, additional terms may apply.</span></span> <span data-ttu-id="a97c5-122">*「* [コネクタ開発者ダッシュボード](https://aka.ms/connectorsdashboard) と [アプリ開発者アグリーメント](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-122">*See* [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard) and [App Developer Agreement](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm).</span></span>

## <a name="faqs--teams-apps-and-partner-accounts"></a><span data-ttu-id="a97c5-123">Faq-Teams アプリとパートナーアカウント</span><span class="sxs-lookup"><span data-stu-id="a97c5-123">FAQs — Teams apps and partner accounts</span></span>

## <a name="how-do-i-create-a-partner-center-account"></a><span data-ttu-id="a97c5-124">パートナーセンターアカウントを作成するにはどうすればよいですか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-124">How do I create a Partner Center account?</span></span>

<span data-ttu-id="a97c5-125">パートナーセンターアカウントを作成するには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-125">There are two ways to create a Partner Center account:</span></span>

- <span data-ttu-id="a97c5-126">パートナーセンターを初めて使用していて、Microsoft ネットワーク内にアカウントがない場合は、 [パートナーセンターの登録ページを使用してアカウントを作成](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-126">If you're new to Partner Center and don't have an account  within the Microsoft network, [create an account using the Partner Center enrollment page](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment).</span></span>
- <span data-ttu-id="a97c5-127">パートナーネットワークに既に登録されている場合は、 [既存の登録を使用してパートナーセンターで直接アカウントを作成](/office/dev/store/)します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-127">If you're already enrolled in the Partner Network, [create an account directly in Partner Center using an existing enrollment](/office/dev/store/).</span></span>

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a><span data-ttu-id="a97c5-128">パートナーセンターで Office ストアアカウントが見つからない場合はどうすればよいですか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-128">What if I cannot find my Office Store account in Partner Center?</span></span>

<span data-ttu-id="a97c5-129">[パートナーセンターのサポートチケット](https://partner.microsoft.com/support/v2/?stage=1)を開いて、ドロップダウンメニューから次のものを選択してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-129">Please open a [Partner Center support ticket](https://partner.microsoft.com/support/v2/?stage=1) and select the following from the drop-down menus:</span></span>

| <span data-ttu-id="a97c5-130">メニュー</span><span class="sxs-lookup"><span data-stu-id="a97c5-130">Menu</span></span> | <span data-ttu-id="a97c5-131">オプション</span><span class="sxs-lookup"><span data-stu-id="a97c5-131">Option</span></span> |
| -------   | -------  |
|<span data-ttu-id="a97c5-132">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="a97c5-132">Category</span></span>| <span data-ttu-id="a97c5-133">コマーシャル市場</span><span class="sxs-lookup"><span data-stu-id="a97c5-133">Commercial Marketplace</span></span>|
| <span data-ttu-id="a97c5-134">トピック</span><span class="sxs-lookup"><span data-stu-id="a97c5-134">Topic</span></span> | <span data-ttu-id="a97c5-135">一般的な Marketplace のヘルプと操作方法に関する質問</span><span class="sxs-lookup"><span data-stu-id="a97c5-135">General Marketplace Help and How-to questions</span></span> |
| <span data-ttu-id="a97c5-136">サブ</span><span class="sxs-lookup"><span data-stu-id="a97c5-136">Subtopic</span></span>| <span data-ttu-id="a97c5-137">Office アドイン</span><span class="sxs-lookup"><span data-stu-id="a97c5-137">Office add-in</span></span> |

## <a name="where-can-i-get-support-for-my-partner-center-issues"></a><span data-ttu-id="a97c5-138">パートナーセンターの問題のサポートを受けるには、どうすればよいですか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-138">Where can I get support for my Partner Center issues?</span></span>

<span data-ttu-id="a97c5-139">「 [Publishers support」ページ](https://aka.ms/marketplacepublishersupport) にアクセスして、問題のトピックを検索し、ガイダンスを見つけてください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-139">Please visit our [publishers support page](https://aka.ms/marketplacepublishersupport) to search for your issue topic and find guidance.</span></span> <span data-ttu-id="a97c5-140">提供されているガイダンスが役に立たない場合は、 [パートナーセンターのサポートチケットを開き](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)ます。</span><span class="sxs-lookup"><span data-stu-id="a97c5-140">If the provided guidance is not helpful, [open a Partner Center support ticket](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket).</span></span>

## <a name="how-do-i-manage-my-office-store-account"></a><span data-ttu-id="a97c5-141">Office ストアアカウントを管理するにはどうすればよいですか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-141">How do I manage my Office Store account?</span></span>

<span data-ttu-id="a97c5-142">パートナーセンターで Office ストアアカウントを管理するためのガイダンスについては、「  [Partner center で Office ストアアカウントを管理する」](/office/dev/store/manage-account-settings-and-profile) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-142">Please visit our  [Manage your Office Store account in Partner Center](/office/dev/store/manage-account-settings-and-profile) for guidance on managing your Office Store account through Partner Center.</span></span>

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a><span data-ttu-id="a97c5-143">パートナープロファイルの連絡先セクションに電話番号を追加するにはどうすればよいですか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-143">How do I add my phone number to the partner profile contact section?</span></span>

<span data-ttu-id="a97c5-144">電話番号には、国番号、市外局番、電話番号の3つのパーツがあります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-144">The phone number has three parts — country code, area code, and the telephone number.</span></span> <span data-ttu-id="a97c5-145">電話番号に市外局番が含まれていない場合は、2番目のボックスを空のままにして、3番目のボックスに入力します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-145">If your phone number doesn't include an area code, then leave the second box empty, and complete the third box.</span></span>

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a><span data-ttu-id="a97c5-146">パートナーセンターでアカウントの設定とパートナーのプロファイルを管理するにはどうすればよいですか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-146">How do I manage my account settings and partner profile in Partner Center?</span></span>

<span data-ttu-id="a97c5-147">パートナーセンターのアカウント設定を管理するためのガイダンスについては、「 [Manage account settings and profile info](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) page」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-147">Please visit our [Manage account settings and profile info](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) page for guidance on managing your Partner Center account settings.</span></span>

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a><span data-ttu-id="a97c5-148">パートナーセンターからアドインを送信しようとすると、"このアカウントは公開されていません" というメッセージが表示されるのはなぜですか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-148">Why do I receive the message, "This account is not publish eligible," when I try to submit my add-in through Partner Center?</span></span>

<span data-ttu-id="a97c5-149">[アカウントの確認状態](/partner-center/verification-responses)が保留中の場合、上記のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a97c5-149">You'll receive the above error message when your [account verification status](/partner-center/verification-responses) is pending.</span></span> <span data-ttu-id="a97c5-150">パートナーセンターの[ダッシュボード](https://partner.microsoft.com/dashboard)で [**設定**] オプション (歯車アイコン) を選択し、[**開発者設定**] [  =>  **アカウント**   =>  **アカウント設定**] を選択することによって、アカウントの確認状態を確認できます。</span><span class="sxs-lookup"><span data-stu-id="a97c5-150">You can check your account verification status in the Partner Center [dashboard](https://partner.microsoft.com/dashboard) by selecting the **Settings** option (the gear icon) in the upper-right corner of the page header shell and choosing **Developer settings** => **Account**  => **Account settings** .</span></span>

![パートナーセンターのアカウント設定ページ](../../assets/images/partner-center-accts-page.png)

![パートナーセンターの確認状態](../../assets/images/partner-center-verification-status.png)

<span data-ttu-id="a97c5-153">アカウント検証プロセスの間に、各必要な手順の状態 (電子メールの所有権、雇用の確認、およびビジネスの確認) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a97c5-153">During the account verification process the status of each required step —  Email Ownership, Employment Verification, and Business Verification — will be displayed.</span></span> <span data-ttu-id="a97c5-154">検証プロセスが正常に完了すると、プロファイルページの登録の検証状態が "保留" から "承認済み" に変わり、プロセスの手順は表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-154">Once the verification process has been successfully completed, the verification status of your enrollment on the profile page will change from "pending" to "authorized," and the process steps will no longer be displayed.</span></span>

![パートナーセンターの検証エラー](../../assets/images/partner-center-acct-verification-error.png)

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-how-should-i-proceed"></a><span data-ttu-id="a97c5-156">自分のアカウントの確認状態が、電子メールの所有権を超える高度ではありません。</span><span class="sxs-lookup"><span data-stu-id="a97c5-156">My account Verification status has not advanced beyond Email Ownership.</span></span> <span data-ttu-id="a97c5-157">続行するにはどうすればよいですか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-157">How should I proceed?</span></span>

<span data-ttu-id="a97c5-158">**電子メールの所有権**の確認プロセスでは、確認メールがプライマリ連絡先の電子メールアドレスに送信されます。</span><span class="sxs-lookup"><span data-stu-id="a97c5-158">During the **Email Ownership** verification process, a verification email is sent to the primary contact email address.</span></span> <span data-ttu-id="a97c5-159">プライマリ連絡先の受信トレイで **maccount@<span>microsoft</span>.com** からの電子メールが必要です。そのためには、「件名を付けてください。」というアクションを必要とします。電子メール *アカウントが microsoft によって確認*され、電子メールの確認プロセスが完了することを要求します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-159">Please check your primary contact inbox for an email  from **maccount@<span>microsoft</span>.com** with the subject  line *Action needed: Verify your email account with Microsoft*, requesting that you complete the email verification process.</span></span> <span data-ttu-id="a97c5-160">確認メールは、パートナーセンターの [アカウント設定] ページに表示されている電子メールアドレスに送信されます。</span><span class="sxs-lookup"><span data-stu-id="a97c5-160">The verification email will be sent to the email address listed  in your account settings page in Partner Center.</span></span>

> [!NOTE]
 ><span data-ttu-id="a97c5-161">[電子メールの確認のリンクは、7日間のみ有効です。</span><span class="sxs-lookup"><span data-stu-id="a97c5-161">The email verification link is only valid for 7 days.</span></span> <span data-ttu-id="a97c5-162">パートナープロファイルページにアクセスして、[ **再送信の確認** ] の電子メールリンクを選択することによって、電子メールを送信するように要求することができます。</span><span class="sxs-lookup"><span data-stu-id="a97c5-162">You can request that we resend the email to you by visiting your partner profile page and selecting the **Resend verification email** link.</span></span> <span data-ttu-id="a97c5-163">電子メールが受信されるようにするには、microsoft.com からの電子メールを安全なドメインとしてホワイトリストし、迷惑メールフォルダーをチェックします。</span><span class="sxs-lookup"><span data-stu-id="a97c5-163">To ensure that the email is received, whitelist email from microsoft.com as a safe domain, and check your junk email folders.</span></span>

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a><span data-ttu-id="a97c5-164">自分のアカウント関連の問題について、さらにサポートを受けるにはどうすればよいですか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-164">How I do get further support for my account related issues?</span></span>

<span data-ttu-id="a97c5-165">サポートチケットを作成するためのガイダンスと手順については、「パートナーセンター」のページの「 [コマーシャル市場プログラムのサポート」](/azure/marketplace/partner-center-portal/support) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-165">Please visit our [Support for the Commercial Marketplace program in Partner Center](/azure/marketplace/partner-center-portal/support) page for guidance and steps to create a support ticket.</span></span>

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a><span data-ttu-id="a97c5-166">メールフォルダーをチェックしていて、確認の電子メールを受信していません。</span><span class="sxs-lookup"><span data-stu-id="a97c5-166">I've checked my mail folders and haven't received the verification email.</span></span> <span data-ttu-id="a97c5-167">次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-167">What  should I do next?</span></span>

<span data-ttu-id="a97c5-168">次のことを試してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-168">Please try the following:</span></span>

1. <span data-ttu-id="a97c5-169">迷惑メールフォルダーを確認してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-169">Check your junk/spam folder.</span></span>
1. <span data-ttu-id="a97c5-170">ブラウザーのキャッシュをクリアし、パートナーセンターのアカウントダッシュボードに移動し、[ **再送信確認** ] 電子メールリンクを選択して、確認の電子メールを電子メールアドレスに送信します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-170">Clear the browser cache, go to your Partner Center account dashboard, and select  the **Resend verification email** link to have the verification email resent to your email address.</span></span>
1. <span data-ttu-id="a97c5-171">別のブラウザーから [  **再送信の確認の電子メール** へのアクセスを試行してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-171">Try accessing the  **Resend verification email** link  from a different browser.</span></span>
1. <span data-ttu-id="a97c5-172">IT 部門と協力して、電子メールサーバーによって検証メールがブロックされないようにします。</span><span class="sxs-lookup"><span data-stu-id="a97c5-172">Work with your IT department to ensure that the verification emails are not blocked by the email server.</span></span>
1. <span data-ttu-id="a97c5-173">サーバーのスパムフィルターを調整して、maccount@microsoft からのすべての電子メールを許可またはホワイトリストに **します。 <span></span>com**。</span><span class="sxs-lookup"><span data-stu-id="a97c5-173">Adjust your server's spam filter to allow/whitelist all emails from **maccount@microsoft.<span></span>com**.</span></span>

## <a name="how-long-does-the-employment-verification-process-usually-take"></a><span data-ttu-id="a97c5-174">雇用確認プロセスには、通常どのくらいの時間がかかりますか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-174">How long does the employment verification process usually take?</span></span>

<span data-ttu-id="a97c5-175">送信されたすべての詳細が正しい場合、雇用の確認は 1 ~ 2 時間で完了します。</span><span class="sxs-lookup"><span data-stu-id="a97c5-175">If all the submitted details are correct, employment verification completes in 1 to 2 hours.</span></span>

## <a name="how-long-does-the-business-verification-process-usually-take"></a><span data-ttu-id="a97c5-176">"ビジネス検証" プロセスは、通常どのくらいの時間で実行されますか。</span><span class="sxs-lookup"><span data-stu-id="a97c5-176">How long does the “Business Verification” process usually take?</span></span>

<span data-ttu-id="a97c5-177">必要なすべてのドキュメントが送信された場合、ビジネスの検証は完了するまでに 1 ~ 2 営業日かかります。</span><span class="sxs-lookup"><span data-stu-id="a97c5-177">Business Verification takes 1 to 2 business days to complete, provided that all required documents have been submitted.</span></span>

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a><span data-ttu-id="a97c5-178">サポートチームに連絡した場合、チケットは優先されますか。</span><span class="sxs-lookup"><span data-stu-id="a97c5-178">If I reach out to the support team, will my ticket be expedited?</span></span>

<span data-ttu-id="a97c5-179">サポートチケットは、週の時間内に解決されます。</span><span class="sxs-lookup"><span data-stu-id="a97c5-179">Support tickets will be resolved within a week's time.</span></span> <span data-ttu-id="a97c5-180">サポートチケットの発生時に提供されたメールに送信される更新プログラムを探してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-180">Please look for the updates which will be sent to the email provided when the support ticket was raised.</span></span>

## <a name="my-issue-is-not-listed-here--are-there-other-pages-i-can-reference-for-partner-center-issues"></a><span data-ttu-id="a97c5-181">この一覧には表示されません。</span><span class="sxs-lookup"><span data-stu-id="a97c5-181">My issue is not listed here.</span></span>  <span data-ttu-id="a97c5-182">パートナーセンターの問題を参照できる他のページはありますか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-182">Are there other pages I can reference for Partner Center issues?</span></span>

<span data-ttu-id="a97c5-183">詳細については、「 [市販のマーケットプレース](/azure/marketplace/) 」のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="a97c5-183">Please refer to our [commercial marketplace documentation](/azure/marketplace/) for more help.</span></span>

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a><span data-ttu-id="a97c5-184">サポートチケットを作成したが、それは7営業日でしたが、更新を受信していません。</span><span class="sxs-lookup"><span data-stu-id="a97c5-184">I've created a support ticket, it has been 7 business days, and I haven't received an update.</span></span> <span data-ttu-id="a97c5-185">追加のヘルプはどこで入手できますか?</span><span class="sxs-lookup"><span data-stu-id="a97c5-185">Where can I get additional help?</span></span>

<span data-ttu-id="a97c5-186">次の情報を使用して、にメールを送信してください **<teamsubm@microsoft.com>** 。</span><span class="sxs-lookup"><span data-stu-id="a97c5-186">Please send an email to **<teamsubm@microsoft.com>** with the following details:</span></span>

1. <span data-ttu-id="a97c5-187">**件名行**</span><span class="sxs-lookup"><span data-stu-id="a97c5-187">**Subject Line**.</span></span> <span data-ttu-id="a97c5-188">\*<App_Name>のパートナーセンターのアカウントの問題 \* (アプリの名前を指定してください)。</span><span class="sxs-lookup"><span data-stu-id="a97c5-188">*Partner Center Account Issue for <App_Name>* (specify the name of your app).</span></span>
1. <span data-ttu-id="a97c5-189">**メール本文:**</span><span class="sxs-lookup"><span data-stu-id="a97c5-189">**Email body:**</span></span>
    * <span data-ttu-id="a97c5-190">サポートチケット番号:</span><span class="sxs-lookup"><span data-stu-id="a97c5-190">Support ticket number:</span></span>
    * <span data-ttu-id="a97c5-191">販売者 ID:</span><span class="sxs-lookup"><span data-stu-id="a97c5-191">Your seller ID:</span></span>
    * <span data-ttu-id="a97c5-192">問題のスクリーンショット (可能な場合):</span><span class="sxs-lookup"><span data-stu-id="a97c5-192">A screen shot of the issue (if possible):</span></span>

>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a97c5-193">Microsoft Teams のアプリの検証ポリシーの詳細情報</span><span class="sxs-lookup"><span data-stu-id="a97c5-193">Learn more about app validation policies for Microsoft Teams</span></span>](/legal/marketplace/certification-policies)
