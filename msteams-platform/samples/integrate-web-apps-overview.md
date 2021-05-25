---
title: Web アプリを統合する
author: Rajeshwari-v
description: Web アプリケーションとデバイス機能をアプリと統合するMicrosoft Teams概要。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 5136c598a3640b5cce92969ea3468c42a7a801db
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630447"
---
# <a name="integrate-web-apps"></a><span data-ttu-id="2c686-103">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="2c686-103">Integrate web apps</span></span>

<span data-ttu-id="2c686-104">既存の Web アプリケーションの機能を新しいプラットフォームに統合することで、充実したユーザー エクスペリエンスMicrosoft Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="2c686-104">You can provide an enriched user experience by integrating the features of an existing web application into Microsoft Teams platform.</span></span> <span data-ttu-id="2c686-105">アプリをアプリ[Teamsネイティブに](~/concepts/design/understand-use-cases.md)するための設計ガイドラインに従Teams。</span><span class="sxs-lookup"><span data-stu-id="2c686-105">Ensure to follow [Teams design guidelines](~/concepts/design/understand-use-cases.md) to make your app native to Teams.</span></span>
<span data-ttu-id="2c686-106">このドキュメントでは、Web アプリケーションを Teams、Power プラットフォームと統合して Power アプリ、Power Virtual Agents、Virtual Assistant、アプリ テンプレート、シフト コネクタ、Moodle LM Teams S を作成し、web サイトの共有ボタンを作成し、SharePoint で Microsoft Teams タブを追加し、ディープ リンクを作成し、デバイス機能を統合するための前提条件について説明します。</span><span class="sxs-lookup"><span data-stu-id="2c686-106">This document gives an overview of prerequisites to integrate web applications with Teams, Power platform to create Power apps, Power Virtual Agents, Virtual Assistant, app templates, Shift connectors, Moodle LMS, creating a Share-to-Teams button for your website, adding a Microsoft Teams tab in SharePoint, creating deep links, and integrating device capabilities.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c686-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="2c686-107">Prerequisites</span></span>   

<span data-ttu-id="2c686-108">効果的な統合を行う場合は、以下の前提条件について理解してください。</span><span class="sxs-lookup"><span data-stu-id="2c686-108">For effective integration, ensure to have a better understanding of the following prerequisites:</span></span>
* <span data-ttu-id="2c686-109">Teams機能。</span><span class="sxs-lookup"><span data-stu-id="2c686-109">Teams capabilities.</span></span> 
* <span data-ttu-id="2c686-110">SharePointストレージの要件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c686-110">SharePoint requirements for file and data storage.</span></span>
* <span data-ttu-id="2c686-111">API の要件。</span><span class="sxs-lookup"><span data-stu-id="2c686-111">API requirements.</span></span>
* <span data-ttu-id="2c686-112">認証。</span><span class="sxs-lookup"><span data-stu-id="2c686-112">Authentication.</span></span>
* <span data-ttu-id="2c686-113">アプリとアプリの詳細なTeams。</span><span class="sxs-lookup"><span data-stu-id="2c686-113">Deep linking of your app with Teams.</span></span>
* <span data-ttu-id="2c686-114">アプリの使用例をプラットフォームの機能Teamsマップします。</span><span class="sxs-lookup"><span data-stu-id="2c686-114">Map your app's use cases to Teams platform capabilities.</span></span>
* <span data-ttu-id="2c686-115">個人使用、共同作業、その両方など、アプリのエントリ ポイントを決定します。</span><span class="sxs-lookup"><span data-stu-id="2c686-115">Determine your app's entry points, such as personal use, collaboration, or both.</span></span>

## <a name="low-code-platforms"></a><span data-ttu-id="2c686-116">低コード プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="2c686-116">Low code platforms</span></span>

<span data-ttu-id="2c686-117">低コード プラットフォームは、ソフトウェア開発に直感的なアプローチを提供し、アプリケーションとプロセスを構築するためにコーディングをほとんどまたは全く必要とします。</span><span class="sxs-lookup"><span data-stu-id="2c686-117">Low code platforms provide an intuitive approach to software development and require little or no coding to build applications and processes.</span></span> <span data-ttu-id="2c686-118">低コード プラットフォームを使用すると、カスタム アプリを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="2c686-118">You can create custom apps easily with low code platforms.</span></span> <span data-ttu-id="2c686-119">これらのプラットフォームは、ビジュアル インターフェイス、バック エンド サービスへのコネクタ、およびアプリケーションのビルド、デバッグ、展開、および保守を行う組み込みのアプリ ライフサイクル管理システムで構成されます。</span><span class="sxs-lookup"><span data-stu-id="2c686-119">These platforms consist of a visual interface, connectors to back end services, and a built-in app lifecycle management system to build, debug, deploy, and maintain applications.</span></span> <span data-ttu-id="2c686-120">Microsoft では、低コード属性を使用して互換性のあるアプリTeams迅速に構築するための、次の革新的なゲートウェイを提供しています。</span><span class="sxs-lookup"><span data-stu-id="2c686-120">Microsoft provides the following innovative gateways to rapidly build Teams-compatible apps using low code attributes:</span></span>
* <span data-ttu-id="2c686-121">Microsoft Power プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="2c686-121">Microsoft Power platform</span></span>
* <span data-ttu-id="2c686-122">Microsoft Teams アプリ テンプレート</span><span class="sxs-lookup"><span data-stu-id="2c686-122">Microsoft Teams app templates</span></span>

## <a name="microsoft-power-platform"></a><span data-ttu-id="2c686-123">Microsoft Power プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="2c686-123">Microsoft Power platform</span></span>

<span data-ttu-id="2c686-124">Microsoft Power プラットフォームは、1 つの強力なアプリケーション プラットフォームで、Power BI、Power Apps、Power Automate、Power Virtual Agentsなど、4 つの堅牢な Microsoft テクノロジを組み合わせたプラットフォームです。</span><span class="sxs-lookup"><span data-stu-id="2c686-124">Microsoft Power platform combines four robust Microsoft technologies, such as Power BI, Power Apps, Power Automate, and Power Virtual Agents in one powerful application platform.</span></span> <span data-ttu-id="2c686-125">これらのテクノロジを使用すると、ソリューションの構築、プロセスの自動化、データの分析、統合された統合環境内での仮想エージェントの作成が可能になります。</span><span class="sxs-lookup"><span data-stu-id="2c686-125">These technologies empower you to build solutions, automate processes, analyze data, and create virtual agents within a unified and integrated environment.</span></span>

### <a name="power-apps"></a><span data-ttu-id="2c686-126">Power アプリ</span><span class="sxs-lookup"><span data-stu-id="2c686-126">Power Apps</span></span>

<span data-ttu-id="2c686-127">このPower Apps、ビジネス データに接続し、組織のニーズに合わせてカスタマイズされたビジネス アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="2c686-127">With Power Apps, you can build business apps that connect to your business data and are tailored to your organization's needs.</span></span> <span data-ttu-id="2c686-128">Power Appsキャンバス アプリを通じてビジネスの課題を解決するために、さまざまなアプリ シナリオを有効にします。</span><span class="sxs-lookup"><span data-stu-id="2c686-128">Power Apps enable a wide range of app scenarios to solve business challenges through canvas apps.</span></span> <span data-ttu-id="2c686-129">アプリを構築した後、アプリをメーカー ポータルからエクスポートしPower Appsに埋め込Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="2c686-129">After building the app, you can export it from the Power Apps maker portal and embed in Microsoft Teams.</span></span>

### <a name="power-virtual-agents"></a><span data-ttu-id="2c686-130">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="2c686-130">Power Virtual Agents</span></span>

<span data-ttu-id="2c686-131">Power Virtual Agent はコードなし、ガイド付きグラフィカル インターフェイス ソリューションです。</span><span class="sxs-lookup"><span data-stu-id="2c686-131">Power Virtual Agent is a no code, guided graphical interface solution.</span></span> <span data-ttu-id="2c686-132">これは、Microsoft Power Platform と Bot Framework 上に構築されています。</span><span class="sxs-lookup"><span data-stu-id="2c686-132">It is built on the Microsoft Power Platform and the Bot Framework.</span></span> <span data-ttu-id="2c686-133">この機能を使用すると、チームのすべてのメンバーが、チャット プラットフォームと簡単に統合できる豊富な会話型チャットボットを作成Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="2c686-133">It empowers every member of your team to create and maintain rich conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="2c686-134">開発環境をセットアップしたり、Web サービスを作成したり、ボット フレームワークに直接登録したりすることなく、Teams 用のインテリジェント仮想エージェントを設計、開発、発行できます。</span><span class="sxs-lookup"><span data-stu-id="2c686-134">You can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment, create a web service, or directly register with the Bot Framework.</span></span>

### <a name="create-virtual-assistant"></a><span data-ttu-id="2c686-135">仮想アシスタントを作成する</span><span class="sxs-lookup"><span data-stu-id="2c686-135">Create Virtual Assistant</span></span>

<span data-ttu-id="2c686-136">Virtual Assistant は、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープン ソース テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="2c686-136">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> 

## <a name="app-templates"></a><span data-ttu-id="2c686-137">アプリ テンプレート</span><span class="sxs-lookup"><span data-stu-id="2c686-137">App templates</span></span>

<span data-ttu-id="2c686-138">アプリ テンプレートを使用して、組織のニーズに合わせてカスタム作成アプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="2c686-138">You can use app template to create custom made apps to suit your organizational needs.</span></span> <span data-ttu-id="2c686-139">これらは、コミュニティによって駆動され、オープンソースMicrosoft Teams、およびアプリで利用可能な、製品向けアプリGitHub。</span><span class="sxs-lookup"><span data-stu-id="2c686-139">These are production-ready apps for Microsoft Teams that are community driven, open-source, and available on GitHub.</span></span> <span data-ttu-id="2c686-140">各テンプレートには、組織のアプリを展開およびインストールする詳細な手順が含まれている。</span><span class="sxs-lookup"><span data-stu-id="2c686-140">Each template contains detailed instructions to deploy and install the app for your organization.</span></span> <span data-ttu-id="2c686-141">すぐにインストールして使用を開始できるすぐに使用できるアプリケーションが提供されます。</span><span class="sxs-lookup"><span data-stu-id="2c686-141">It provides a ready-to-use application that you can install and start using immediately.</span></span> 

## <a name="teams-shifts-work-force-management-connectors"></a><span data-ttu-id="2c686-142">TeamsShifts Work Force Management コネクタ</span><span class="sxs-lookup"><span data-stu-id="2c686-142">Teams Shifts Work Force Management connectors</span></span>

<span data-ttu-id="2c686-143">TeamsShifts Work Force Management コネクタは、運用対応、オープンソース、コミュニティ駆動型の統合です。</span><span class="sxs-lookup"><span data-stu-id="2c686-143">Teams Shifts Work Force Management connectors are production-ready, open-source, and community-driven integrations.</span></span> <span data-ttu-id="2c686-144">シームレスなエクスペリエンスと迅速なプロセスを提供し、シフトを使用したファーストラインワーカーのデジタルTeams提供します。</span><span class="sxs-lookup"><span data-stu-id="2c686-144">They offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span>

## <a name="install-moodle-lms"></a><span data-ttu-id="2c686-145">Moodle LMS のインストール</span><span class="sxs-lookup"><span data-stu-id="2c686-145">Install Moodle LMS</span></span>

<span data-ttu-id="2c686-146">Moodle は、一般的なオープン ソース学習管理システム (LMS) です。</span><span class="sxs-lookup"><span data-stu-id="2c686-146">Moodle is a popular open-source Learning Management System (LMS).</span></span> <span data-ttu-id="2c686-147">この機能は現在、Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="2c686-147">It is now integrated with Microsoft Teams.</span></span> <span data-ttu-id="2c686-148">この統合により、教育者と教師は、Moodle コースを中心に共同作業を行い、成績と課題に関する質問をし、通知を直接通知Teams。</span><span class="sxs-lookup"><span data-stu-id="2c686-148">This integration helps educators and teachers to collaborate around Moodle courses, ask questions about grades and assignments, and stay updated with notifications directly within Teams.</span></span>

## <a name="create-a-share-to-teams-button-for-your-website"></a><span data-ttu-id="2c686-149">Web サイトの [Teams で共有] ボタンを作成する</span><span class="sxs-lookup"><span data-stu-id="2c686-149">Create a Share-to-Teams button for your website</span></span>

<span data-ttu-id="2c686-150">サードパーティの Web サイトでは、ランチャー スクリプトを使用して、Web ページ上の Teamsボタンに Share を埋め込む可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2c686-150">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages.</span></span> <span data-ttu-id="2c686-151">ボタンを選択すると、ポップアップ ウィンドウで [共有Teamsを起動します。</span><span class="sxs-lookup"><span data-stu-id="2c686-151">When you select the button, it launches the Share to Teams experience in a pop-up window.</span></span> <span data-ttu-id="2c686-152">これにより、コンテキストを切り替えることなく、任意のユーザーまたはMicrosoft Teamsへのリンクを直接共有できます。</span><span class="sxs-lookup"><span data-stu-id="2c686-152">This allows you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a><span data-ttu-id="2c686-153">[ページ] Microsoft Teamsタブを追加SharePoint</span><span class="sxs-lookup"><span data-stu-id="2c686-153">Add a Microsoft Teams tab in SharePoint</span></span>

<span data-ttu-id="2c686-154">Microsoft Teams と SharePoint の間の豊富な統合エクスペリエンスを得るには、Microsoft Teams タブを SharePoint web パーツSPFx追加します。</span><span class="sxs-lookup"><span data-stu-id="2c686-154">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> 

## <a name="create-deep-link"></a><span data-ttu-id="2c686-155">ディープ リンクの作成</span><span class="sxs-lookup"><span data-stu-id="2c686-155">Create deep link</span></span>

<span data-ttu-id="2c686-156">エンティティへのディープ リンクを作成するには、Teams。</span><span class="sxs-lookup"><span data-stu-id="2c686-156">You can create deep links to the entities in Teams.</span></span> <span data-ttu-id="2c686-157">情報と機能へのリンクは、Teams。</span><span class="sxs-lookup"><span data-stu-id="2c686-157">You can create links to information and features within Teams.</span></span> <span data-ttu-id="2c686-158">これらのディープ リンクは、タブ内のコンテンツと情報に移動します。ディープ リンクを使用すると、アプリとアプリTeamsリンクし、アプリの複数の部分を結び付け、よりネイティブなエクスペリエンスTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="2c686-158">These deep links navigate to content and information within your tab. You can use deep links to link your app with Teams as they tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="integrate-device-capabilities"></a><span data-ttu-id="2c686-159">デバイス機能の統合</span><span class="sxs-lookup"><span data-stu-id="2c686-159">Integrate device capabilities</span></span>

<span data-ttu-id="2c686-160">Microsoft Teamsプラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。</span><span class="sxs-lookup"><span data-stu-id="2c686-160">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="2c686-161">拡張された Teams プラットフォームを使用すると、パートナーは、Microsoft Teams JavaScript クライアント SDK で利用できる専用 API を使用して、カメラ、QR またはバーコード スキャナー、フォト ギャラリー、マイク、場所などのネイティブ デバイス機能にアクセスして統合できます。</span><span class="sxs-lookup"><span data-stu-id="2c686-161">The enhanced Teams platform allows partners to access and integrate the native device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location using dedicated APIs available in Microsoft Teams JavaScript client SDK.</span></span> 

## <a name="see-also"></a><span data-ttu-id="2c686-162">関連項目</span><span class="sxs-lookup"><span data-stu-id="2c686-162">See also</span></span>

* [<span data-ttu-id="2c686-163">アプリの使用例をプラットフォームの機能Teamsマップする</span><span class="sxs-lookup"><span data-stu-id="2c686-163">Map your app's use cases to Teams platform capabilities</span></span>](~/concepts/design/map-use-cases.md)
* [<span data-ttu-id="2c686-164">アプリのエントリ ポイントを決定する</span><span class="sxs-lookup"><span data-stu-id="2c686-164">Determine your app's entry points</span></span>](~/concepts/extensibility-points.md)
* [<span data-ttu-id="2c686-165">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="2c686-165">Integrate web apps</span></span>](~/samples/integrating-web-apps.md)
* [<span data-ttu-id="2c686-166">低コードのカスタム アプリを作成Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2c686-166">Create low-code custom apps for Microsoft Teams</span></span>](~/samples/teams-low-code-solutions.md)
* [<span data-ttu-id="2c686-167">Power Virtual Agents チャットボットを追加する</span><span class="sxs-lookup"><span data-stu-id="2c686-167">Add a Power Virtual Agents chatbot</span></span>](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [<span data-ttu-id="2c686-168">仮想アシスタントの作成</span><span class="sxs-lookup"><span data-stu-id="2c686-168">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)
* [<span data-ttu-id="2c686-169">Microsoft Teams 用のアプリ テンプレート</span><span class="sxs-lookup"><span data-stu-id="2c686-169">App templates for Microsoft Teams</span></span>](~/samples/app-templates.md)
* [<span data-ttu-id="2c686-170">実稼働対応のシフト コネクタ</span><span class="sxs-lookup"><span data-stu-id="2c686-170">Production-ready Shift Connectors</span></span>](~/samples/shifts-wfm-connectors.md)
* [<span data-ttu-id="2c686-171">Moodle LMS のインストール</span><span class="sxs-lookup"><span data-stu-id="2c686-171">Install Moodle LMS</span></span>](~/resources/moodleinstructions.md)
* <span data-ttu-id="2c686-172">[[Teams で共有] ボタンを作成する](~/concepts/build-and-test/share-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="2c686-172">[Create a Share-to-Teams button](~/concepts/build-and-test/share-to-teams.md)</span></span>
* [<span data-ttu-id="2c686-173">SharePoint に Teams タブを追加する</span><span class="sxs-lookup"><span data-stu-id="2c686-173">Add a Teams tab to SharePoint</span></span>](~/tabs/how-to/tabs-in-sharepoint.md)
* [<span data-ttu-id="2c686-174">ディープ リンクの作成</span><span class="sxs-lookup"><span data-stu-id="2c686-174">Create deep links</span></span>](~/concepts/build-and-test/deep-links.md)
* [<span data-ttu-id="2c686-175">デバイス機能</span><span class="sxs-lookup"><span data-stu-id="2c686-175">Device capabilities</span></span>](~/concepts/device-capabilities/device-capabilities-overview.md)
