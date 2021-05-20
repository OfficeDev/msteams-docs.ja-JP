---
title: ストアの提出に関する問題を解決する
description: Microsoft Teams ストアの提出に関する問題のトラブルシューティングと修正方法を理解する。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 23c751d7a9fec96de128521f660213a559534283
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565110"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a><span data-ttu-id="579a9-103">Microsoft Teams ストアの送信に失敗した場合の問題の解決</span><span class="sxs-lookup"><span data-stu-id="579a9-103">Resolve issues if your Microsoft Teams store submission fails</span></span>

<span data-ttu-id="579a9-104">Microsoft Teams ストアに公開されるアプリは、[ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)と[商用マーケットプレース ポリシー](/legal/marketplace/certification-policies)Teams を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="579a9-104">Apps published to the Microsoft Teams store must meet the [Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) and [commercial marketplace policies](/legal/marketplace/certification-policies).</span></span>

<span data-ttu-id="579a9-105">ストアの提出に失敗した場合、Microsoft はアプリの準拠と公開を支援するコンシェルジュ検証サービスを提供します。</span><span class="sxs-lookup"><span data-stu-id="579a9-105">If your store submission fails, Microsoft provides a concierge validation service to help get your app compliant and published.</span></span>

## <a name="get-help-directly-from-microsoft"></a><span data-ttu-id="579a9-106">マイクロソフトから直接ヘルプを取得する</span><span class="sxs-lookup"><span data-stu-id="579a9-106">Get help directly from Microsoft</span></span>

<span data-ttu-id="579a9-107">Microsoft が提供するコンシェルジュ検証サービスは、開発者がアプリをTeams ストアに公開するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="579a9-107">The concierge validation service provided by Microsoft helps developers get their apps published to the Teams store.</span></span> <span data-ttu-id="579a9-108">Microsoft は、このサービスの一環として、アプリが説明どおりに動作し、すべての適切なメタデータを含み、ユーザーに価値を提供するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="579a9-108">As part of this service, Microsoft verifies if your app works as described, contains all appropriate metadata, and provides value to users.</span></span>

<span data-ttu-id="579a9-109">アプリの提出に失敗した場合、Microsoft は提出から 24 時間以内に推奨事項を含むレビュー レポートを送信します。</span><span class="sxs-lookup"><span data-stu-id="579a9-109">If your app submission fails, Microsoft sends you a review report with recommendations within 24 hours of submission.</span></span>

## <a name="resolve-issues-and-resubmit-your-app"></a><span data-ttu-id="579a9-110">問題を解決してアプリを再提出する</span><span class="sxs-lookup"><span data-stu-id="579a9-110">Resolve issues and resubmit your app</span></span>

<span data-ttu-id="579a9-111">パートナー センターでアプリを再送信する前に、Microsoft コンシェルジュ検証チームによって報告されたすべての問題を修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="579a9-111">You must fix all issues reported by the Microsoft concierge validation team before resubmitting your app on Partner Center.</span></span> <span data-ttu-id="579a9-112">マイクロソフトのレポートには、次の情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="579a9-112">The Microsoft report includes the following information:</span></span>

* <span data-ttu-id="579a9-113">各問題に対応する [検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) 。</span><span class="sxs-lookup"><span data-stu-id="579a9-113">A corresponding [validation guideline](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) for each issue.</span></span>
* <span data-ttu-id="579a9-114">各問題の再現方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="579a9-114">Instructions on how to reproduce each issue.</span></span>
* <span data-ttu-id="579a9-115">一般に公開されている開発者ドキュメントに基づいて、各問題を解決するための推奨事項。</span><span class="sxs-lookup"><span data-stu-id="579a9-115">Recommendations for resolving each issue based on publicly available developer documentation.</span></span>

<span data-ttu-id="579a9-116">問題を解決し、アプリを再送信するプロセスは、通常、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="579a9-116">The process for resolving issues and resubmitting an app typically goes like this:</span></span>

1. <span data-ttu-id="579a9-117">レポート内のすべての問題を修正します。</span><span class="sxs-lookup"><span data-stu-id="579a9-117">You fix all issues in the report.</span></span>
1. <span data-ttu-id="579a9-118">次の情報は、teamsubm@microsoft.com の Microsoft コンシェルジュ検証 <a href="mailto:teamsubm@microsoft.com">チームに送信</a>します。</span><span class="sxs-lookup"><span data-stu-id="579a9-118">You send the following to the Microsoft concierge validation team at <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>:</span></span>
   * <span data-ttu-id="579a9-119">更新されたアプリ パッケージ</span><span class="sxs-lookup"><span data-stu-id="579a9-119">An updated app package</span></span>
   * <span data-ttu-id="579a9-120">アプリのノートをテストする (元の申請にメモを含めなかった場合):</span><span class="sxs-lookup"><span data-stu-id="579a9-120">Test notes for your app, if you didn't include these in your original submission:</span></span>
      * <span data-ttu-id="579a9-121">少なくとも 2 つのアカウントの資格情報 (1 人の管理者と 1 人の管理者以外)。</span><span class="sxs-lookup"><span data-stu-id="579a9-121">Credentials for at least two accounts (one admin and one non-admin).</span></span>
      * <span data-ttu-id="579a9-122">アプリを構成し、その機能をテストする手順。</span><span class="sxs-lookup"><span data-stu-id="579a9-122">Instructions to configure the app and test its functionality.</span></span>
      * <span data-ttu-id="579a9-123">Teamsで使用したアプリを示すビデオ。</span><span class="sxs-lookup"><span data-stu-id="579a9-123">A video showing your app used in Teams.</span></span>
1. <span data-ttu-id="579a9-124">Microsoft コンシェルジュ検証チームは、更新されたアプリを完全にテストします。</span><span class="sxs-lookup"><span data-stu-id="579a9-124">Microsoft concierge validation team fully tests your updated app.</span></span>
1. <span data-ttu-id="579a9-125">次のいずれかの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="579a9-125">You do one of the following:</span></span>
   * <span data-ttu-id="579a9-126">アプリに問題が発生する場合は、パートナー センターでアプリを再送信します。</span><span class="sxs-lookup"><span data-stu-id="579a9-126">If your app is free of issues, resubmit your app on Partner Center.</span></span>
   * <span data-ttu-id="579a9-127">問題が解決しない場合や、Microsoft が新しい問題を発見した場合は、修正の内容に関する別のレポートが表示されます。</span><span class="sxs-lookup"><span data-stu-id="579a9-127">If issues aren't resolved or Microsoft finds new issues, you receive another report on what to fix.</span></span> <span data-ttu-id="579a9-128">これらの問題を解決し、アプリの更新版を <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>に送信します。</span><span class="sxs-lookup"><span data-stu-id="579a9-128">Resolve those issues and send an updated version of the app to <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.</span></span>

> [!CAUTION]
> <span data-ttu-id="579a9-129">複数の送信エラーを回避するには、Microsoft コンシェルジュ検証チームがアプリを承認するまで、パートナー センターでアプリを再送信しないでください。</span><span class="sxs-lookup"><span data-stu-id="579a9-129">To avoid multiple submission failures, do not resubmit your app on Partner Center until the Microsoft concierge validation team approves your app.</span></span>

## <a name="faq"></a><span data-ttu-id="579a9-130">FAQ</span><span class="sxs-lookup"><span data-stu-id="579a9-130">FAQ</span></span>

<span data-ttu-id="579a9-131">アプリの送信に関する問題を解決する際に、よく寄せられる質問に対する回答を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="579a9-131">Get answers to some common questions when resolving app submission issues.</span></span>

<br>

<details>

<summary><span data-ttu-id="579a9-132"><b>アプリの公開にはどのくらいの時間がかかりますか?</b></span><span class="sxs-lookup"><span data-stu-id="579a9-132"><b>How long will it take to publish my app?</b></span></span></summary>

<span data-ttu-id="579a9-133">ストアの提出に問題がない場合、アプリは 1 ~ 2 営業日以内に公開されます。</span><span class="sxs-lookup"><span data-stu-id="579a9-133">If your store submission has no issues, your app will publish within 1-2 business days.</span></span> <span data-ttu-id="579a9-134">アプリが失敗した場合、Microsoft のチームが問題を解決するための推奨事項を提供します。</span><span class="sxs-lookup"><span data-stu-id="579a9-134">If your app fails, a team from Microsoft provides you with recommendations to fix the issues.</span></span> <span data-ttu-id="579a9-135">これらの修正を行い、更新されたアプリをそのチームに再送信すると、アプリを公開する準備ができているか、さらに作業が必要な場合は、24 時間以内に通知されます。</span><span class="sxs-lookup"><span data-stu-id="579a9-135">Once you make those fixes and resend an updated app to that team, you will be notified in 24 hours if your app is ready to publish or still needs more work.</span></span>

<br>

</details>

<details>

<summary><span data-ttu-id="579a9-136"><b>アプリが申請に合格する可能性を高めるにはどうすればよいですか?</b></span><span class="sxs-lookup"><span data-stu-id="579a9-136"><b>How do I increase the likelihood my app will pass submission?</b></span></span></summary>

<span data-ttu-id="579a9-137">次の操作を行うと、送信が成功する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="579a9-137">Doing the following can lead to a successful submission:</span></span>

1. <span data-ttu-id="579a9-138">[Teams設計ガイドライン](~/concepts/design/design-teams-app-overview.md)に基づいてアプリを開発する 。</span><span class="sxs-lookup"><span data-stu-id="579a9-138">Develop your app based on the [Teams design guidelines](~/concepts/design/design-teams-app-overview.md).</span></span>
1. <span data-ttu-id="579a9-139">アプリが[Teamsストア検証ガイドラインと](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) [Microsoft 商用市場認定ポリシー](/legal/marketplace/certification-policies)に準拠していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="579a9-139">Make sure your app adheres to the [Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) and [Microsoft commercial marketplace certification policies](/legal/marketplace/certification-policies).</span></span>
1. <span data-ttu-id="579a9-140">[アプリの検証ツールを使用してアプリ パッケージをテストMicrosoft Teams。](https://dev.teams.microsoft.com/appvalidation.html)</span><span class="sxs-lookup"><span data-stu-id="579a9-140">Test your app package with the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span>
1. <span data-ttu-id="579a9-141">[Teams ストアの提出を準備する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md):</span><span class="sxs-lookup"><span data-stu-id="579a9-141">[Prepare your Teams store submission](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).</span></span>

<br>

</details>

<details>

<summary><span data-ttu-id="579a9-142"><b>私のアプリはベータテスト中です。アプリを提出して、公開プロセスの時間を節約できますか?</b></span><span class="sxs-lookup"><span data-stu-id="579a9-142"><b>My app is in beta testing. Can I submit my app anyway to save time on the publishing process?</b></span></span></summary>

<span data-ttu-id="579a9-143">いいえ。</span><span class="sxs-lookup"><span data-stu-id="579a9-143">No.</span></span> <span data-ttu-id="579a9-144">マイクロソフトは、運用可能なアプリのみを検証します。</span><span class="sxs-lookup"><span data-stu-id="579a9-144">Microsoft only validates production-ready apps.</span></span>

<br>

</details>

<details>

<summary><span data-ttu-id="579a9-145"><b>パートナー センターで初めてアプリを提出する前に、teamsubm@microsoft.com メールに連絡できますか?</b></span><span class="sxs-lookup"><span data-stu-id="579a9-145"><b>May I contact the teamsubm@microsoft.com email before submitting my app for the first time on Partner Center?</b></span></span></summary>

<span data-ttu-id="579a9-146">いいえ。</span><span class="sxs-lookup"><span data-stu-id="579a9-146">No.</span></span> <span data-ttu-id="579a9-147">マイクロソフトでは、パートナー センターで初めてアプリを提出するまで、アプリの検証を開始しません。</span><span class="sxs-lookup"><span data-stu-id="579a9-147">Microsoft doesn't start validating your app until you submit your app for the first time on Partner Center.</span></span>

<br>

</details>

<details>

<summary><span data-ttu-id="579a9-148"><b>パートナー センターから、アプリの公開が承認されたというメールを受け取りました。アプリがTeams ストアにないのはなぜですか?</b></span><span class="sxs-lookup"><span data-stu-id="579a9-148"><b>I received an email from Partner Center saying my app was approved to publish. Why isn't my app in the Teams store?</b></span></span></summary>

<span data-ttu-id="579a9-149">アプリが承認されると、通常、アプリの機能に応じて 1 ~ 2 営業日かかります。</span><span class="sxs-lookup"><span data-stu-id="579a9-149">Once your app is approved, publishing usually takes 1-2 business days depending on the app's capabilities.</span></span><span data-ttu-id="579a9-150">アプリが 2 営業日を過ぎるとアプリが公開されていない場合は <a href="mailto:teamsubm@microsoft.com">、teamsubm@microsoft.com</a>に連絡してください。</span><span class="sxs-lookup"><span data-stu-id="579a9-150"> If your app hasn't published after two business days, contact <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.</span></span>

<br>

</details>
