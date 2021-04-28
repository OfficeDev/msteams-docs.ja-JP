---
title: Web アプリを統合する
author: Rajeshwari-v
description: Web アプリケーションとデバイス機能を Microsoft Teams アプリと統合する概要。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 01977e22d79f7e39986367e647a2d48ea9b2905c
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058657"
---
# <a name="integrate-web-apps"></a><span data-ttu-id="17445-103">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="17445-103">Integrate web apps</span></span>

<span data-ttu-id="17445-104">既存の Web アプリケーションの機能を Microsoft Teams プラットフォームに統合することで、充実したユーザー エクスペリエンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="17445-104">You can provide an enriched user experience by integrating the features of an existing web application into Microsoft Teams platform.</span></span> <span data-ttu-id="17445-105">Teams のデザイン [ガイドラインに従って、](~/concepts/design/understand-use-cases.md) アプリを Teams にネイティブにしてください。</span><span class="sxs-lookup"><span data-stu-id="17445-105">Ensure to follow [Teams design guidelines](~/concepts/design/understand-use-cases.md) to make your app native to Teams.</span></span>
<span data-ttu-id="17445-106">このドキュメントでは、Web アプリケーションを Teams、Power プラットフォームと統合して Power アプリ、Power Virtual Agents、Virtual Assistant、アプリ テンプレート、シフト コネクタ、Moodle LMS を作成し、Web サイトの Share-to-Teams ボタンを作成し、SharePoint に Microsoft Teams タブを追加し、ディープ リンクを作成し、デバイス機能を統合するための前提条件について説明します。</span><span class="sxs-lookup"><span data-stu-id="17445-106">This document gives an overview of prerequisites to integrate web applications with Teams, Power platform to create Power apps, Power Virtual Agents, Virtual Assistant, app templates, Shift connectors, Moodle LMS, creating a Share-to-Teams button for your website, adding a Microsoft Teams tab in SharePoint, creating deep links, and integrating device capabilities.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17445-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="17445-107">Prerequisites</span></span>   

<span data-ttu-id="17445-108">効果的な統合を行う場合は、以下の前提条件について理解してください。</span><span class="sxs-lookup"><span data-stu-id="17445-108">For effective integration, ensure to have a better understanding of the following prerequisites:</span></span>
* <span data-ttu-id="17445-109">Teams の機能。</span><span class="sxs-lookup"><span data-stu-id="17445-109">Teams capabilities.</span></span> 
* <span data-ttu-id="17445-110">ファイルとデータストレージの SharePoint 要件。</span><span class="sxs-lookup"><span data-stu-id="17445-110">SharePoint requirements for file and data storage.</span></span>
* <span data-ttu-id="17445-111">API の要件。</span><span class="sxs-lookup"><span data-stu-id="17445-111">API requirements.</span></span>
* <span data-ttu-id="17445-112">認証。</span><span class="sxs-lookup"><span data-stu-id="17445-112">Authentication.</span></span>
* <span data-ttu-id="17445-113">アプリと Teams の深いリンク。</span><span class="sxs-lookup"><span data-stu-id="17445-113">Deep linking of your app with Teams.</span></span>
* <span data-ttu-id="17445-114">アプリの使用例を Teams プラットフォームの機能にマップします。</span><span class="sxs-lookup"><span data-stu-id="17445-114">Map your app's use cases to Teams platform capabilities.</span></span>
* <span data-ttu-id="17445-115">個人使用、共同作業、その両方など、アプリのエントリ ポイントを決定します。</span><span class="sxs-lookup"><span data-stu-id="17445-115">Determine your app's entry points, such as personal use, collaboration, or both.</span></span>

## <a name="low-code-platforms"></a><span data-ttu-id="17445-116">低コード プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="17445-116">Low code platforms</span></span>

<span data-ttu-id="17445-117">低コード プラットフォームは、ソフトウェア開発に直感的なアプローチを提供し、アプリケーションとプロセスを構築するためにコーディングをほとんどまたは全く必要とします。</span><span class="sxs-lookup"><span data-stu-id="17445-117">Low code platforms provide an intuitive approach to software development and require little or no coding to build applications and processes.</span></span> <span data-ttu-id="17445-118">低コード プラットフォームを使用すると、カスタム アプリを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="17445-118">You can create custom apps easily with low code platforms.</span></span> <span data-ttu-id="17445-119">これらのプラットフォームは、ビジュアル インターフェイス、バック エンド サービスへのコネクタ、およびアプリケーションのビルド、デバッグ、展開、および保守を行う組み込みのアプリ ライフサイクル管理システムで構成されます。</span><span class="sxs-lookup"><span data-stu-id="17445-119">These platforms consist of a visual interface, connectors to back end services, and a built-in app lifecycle management system to build, debug, deploy, and maintain applications.</span></span> <span data-ttu-id="17445-120">Microsoft では、低コード属性を使用して Teams 互換アプリを迅速に構築するための、次の革新的なゲートウェイを提供しています。</span><span class="sxs-lookup"><span data-stu-id="17445-120">Microsoft provides the following innovative gateways to rapidly build Teams-compatible apps using low code attributes:</span></span>
* <span data-ttu-id="17445-121">Microsoft Power プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="17445-121">Microsoft Power platform</span></span>
* <span data-ttu-id="17445-122">Microsoft Teams アプリ テンプレート</span><span class="sxs-lookup"><span data-stu-id="17445-122">Microsoft Teams app templates</span></span>

## <a name="microsoft-power-platform"></a><span data-ttu-id="17445-123">Microsoft Power プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="17445-123">Microsoft Power platform</span></span>

<span data-ttu-id="17445-124">Microsoft Power プラットフォームは、Power BI、Power Apps、Power Automate、Power Virtual Agents などの 4 つの堅牢な Microsoft テクノロジを 1 つの強力なアプリケーション プラットフォームに組み合わせたプラットフォームです。</span><span class="sxs-lookup"><span data-stu-id="17445-124">Microsoft Power platform combines four robust Microsoft technologies, such as Power BI, Power Apps, Power Automate, and Power Virtual Agents in one powerful application platform.</span></span> <span data-ttu-id="17445-125">これらのテクノロジを使用すると、ソリューションの構築、プロセスの自動化、データの分析、統合された統合環境内での仮想エージェントの作成が可能になります。</span><span class="sxs-lookup"><span data-stu-id="17445-125">These technologies empower you to build solutions, automate processes, analyze data, and create virtual agents within a unified and integrated environment.</span></span>

### <a name="power-apps"></a><span data-ttu-id="17445-126">Power Apps</span><span class="sxs-lookup"><span data-stu-id="17445-126">Power Apps</span></span>

<span data-ttu-id="17445-127">Power Apps を使用すると、ビジネス データに接続し、組織のニーズに合わせてカスタマイズされたビジネス アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="17445-127">With Power Apps, you can build business apps that connect to your business data and are tailored to your organization's needs.</span></span> <span data-ttu-id="17445-128">Power Apps を使用すると、キャンバス アプリを通じてビジネス上の課題を解決するために、さまざまなアプリ シナリオを利用できます。</span><span class="sxs-lookup"><span data-stu-id="17445-128">Power Apps enable a wide range of app scenarios to solve business challenges through canvas apps.</span></span> <span data-ttu-id="17445-129">アプリを構築した後、Power Apps メーカー ポータルからアプリをエクスポートし、Microsoft Teams に埋め込みできます。</span><span class="sxs-lookup"><span data-stu-id="17445-129">After building the app, you can export it from the Power Apps maker portal and embed in Microsoft Teams.</span></span>

### <a name="power-virtual-agents"></a><span data-ttu-id="17445-130">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="17445-130">Power Virtual Agents</span></span>

<span data-ttu-id="17445-131">Power Virtual Agent はコードなし、ガイド付きグラフィカル インターフェイス ソリューションです。</span><span class="sxs-lookup"><span data-stu-id="17445-131">Power Virtual Agent is a no code, guided graphical interface solution.</span></span> <span data-ttu-id="17445-132">これは、Microsoft Power Platform と Bot Framework 上に構築されています。</span><span class="sxs-lookup"><span data-stu-id="17445-132">It is built on the Microsoft Power Platform and the Bot Framework.</span></span> <span data-ttu-id="17445-133">チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できる豊富な会話型チャットボットを作成および維持できます。</span><span class="sxs-lookup"><span data-stu-id="17445-133">It empowers every member of your team to create and maintain rich conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="17445-134">開発環境をセットアップしたり、Web サービスを作成したり、ボット フレームワークに直接登録したりすることなく、Teams 用のインテリジェント仮想エージェントを設計、開発、発行できます。</span><span class="sxs-lookup"><span data-stu-id="17445-134">You can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment, create a web service, or directly register with the Bot Framework.</span></span>

### <a name="create-virtual-assistant"></a><span data-ttu-id="17445-135">仮想アシスタントを作成する</span><span class="sxs-lookup"><span data-stu-id="17445-135">Create Virtual Assistant</span></span>

<span data-ttu-id="17445-136">Virtual Assistant は、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープン ソース テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="17445-136">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> 

## <a name="app-templates"></a><span data-ttu-id="17445-137">アプリ テンプレート</span><span class="sxs-lookup"><span data-stu-id="17445-137">App templates</span></span>

<span data-ttu-id="17445-138">アプリ テンプレートを使用して、組織のニーズに合わせてカスタム作成アプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="17445-138">You can use app template to create custom made apps to suit your organizational needs.</span></span> <span data-ttu-id="17445-139">これらは、コミュニティ駆動型、オープンソースであり、GitHub で利用可能な Microsoft Teams 用の実稼働可能なアプリです。</span><span class="sxs-lookup"><span data-stu-id="17445-139">These are production-ready apps for Microsoft Teams that are community driven, open-source, and available on GitHub.</span></span> <span data-ttu-id="17445-140">各テンプレートには、組織のアプリを展開およびインストールする詳細な手順が含まれている。</span><span class="sxs-lookup"><span data-stu-id="17445-140">Each template contains detailed instructions to deploy and install the app for your organization.</span></span> <span data-ttu-id="17445-141">すぐにインストールして使用を開始できるすぐに使用できるアプリケーションが提供されます。</span><span class="sxs-lookup"><span data-stu-id="17445-141">It provides a ready-to-use application that you can install and start using immediately.</span></span> 

## <a name="teams-shifts-work-force-management-connectors"></a><span data-ttu-id="17445-142">Teams Shifts Work Force Management コネクタ</span><span class="sxs-lookup"><span data-stu-id="17445-142">Teams Shifts Work Force Management connectors</span></span>

<span data-ttu-id="17445-143">Teams Shifts Work Force Management コネクタは、運用対応、オープンソース、コミュニティ駆動型の統合です。</span><span class="sxs-lookup"><span data-stu-id="17445-143">Teams Shifts Work Force Management connectors are production-ready, open-source, and community-driven integrations.</span></span> <span data-ttu-id="17445-144">Teams Shifts を使用したファーストライン ワーカーのデジタル変換のためのシームレスなエクスペリエンスと迅速なプロセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="17445-144">They offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span>

## <a name="install-moodle-lms"></a><span data-ttu-id="17445-145">Moodle LMS のインストール</span><span class="sxs-lookup"><span data-stu-id="17445-145">Install Moodle LMS</span></span>

<span data-ttu-id="17445-146">Moodle は、一般的なオープン ソース学習管理システム (LMS) です。</span><span class="sxs-lookup"><span data-stu-id="17445-146">Moodle is a popular open-source Learning Management System (LMS).</span></span> <span data-ttu-id="17445-147">これで、Microsoft Teams と統合されました。</span><span class="sxs-lookup"><span data-stu-id="17445-147">It is now integrated with Microsoft Teams.</span></span> <span data-ttu-id="17445-148">この統合により、教育者と教師は、Moodle コースを中心に共同作業を行い、成績と課題に関する質問をし、Teams 内で直接通知を更新できます。</span><span class="sxs-lookup"><span data-stu-id="17445-148">This integration helps educators and teachers to collaborate around Moodle courses, ask questions about grades and assignments, and stay updated with notifications directly within Teams.</span></span>

## <a name="create-a-share-to-teams-button-for-your-website"></a><span data-ttu-id="17445-149">Web サイトの [Teams で共有] ボタンを作成する</span><span class="sxs-lookup"><span data-stu-id="17445-149">Create a Share-to-Teams button for your website</span></span>

<span data-ttu-id="17445-150">サードパーティの Web サイトでは、ランチャー スクリプトを使用して、Web ページに [Teams に共有] ボタンを埋め込む可能性があります。</span><span class="sxs-lookup"><span data-stu-id="17445-150">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages.</span></span> <span data-ttu-id="17445-151">ボタンを選択すると、ポップアップ ウィンドウで Teams への共有エクスペリエンスが起動します。</span><span class="sxs-lookup"><span data-stu-id="17445-151">When you select the button, it launches the Share to Teams experience in a pop-up window.</span></span> <span data-ttu-id="17445-152">これにより、コンテキストを切り替えることなく、任意のユーザーまたは Microsoft Teams チャネルへのリンクを直接共有できます。</span><span class="sxs-lookup"><span data-stu-id="17445-152">This allows you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a><span data-ttu-id="17445-153">SharePoint で [Microsoft Teams] タブを追加する</span><span class="sxs-lookup"><span data-stu-id="17445-153">Add a Microsoft Teams tab in SharePoint</span></span>

<span data-ttu-id="17445-154">SharePoint の [Microsoft Teams] タブを SPFx Web パーツとして追加すると、Microsoft Teams と SharePoint の豊富な統合エクスペリエンスを得られる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="17445-154">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> 

## <a name="create-deep-link"></a><span data-ttu-id="17445-155">ディープ リンクの作成</span><span class="sxs-lookup"><span data-stu-id="17445-155">Create deep link</span></span>

<span data-ttu-id="17445-156">Teams でエンティティへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="17445-156">You can create deep links to the entities in Teams.</span></span> <span data-ttu-id="17445-157">Teams 内で情報と機能へのリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="17445-157">You can create links to information and features within Teams.</span></span> <span data-ttu-id="17445-158">これらのディープ リンクは、タブ内のコンテンツと情報に移動します。ディープ リンクを使用すると、アプリを Teams とリンクし、複数のアプリを結び付け、よりネイティブな Teams エクスペリエンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="17445-158">These deep links navigate to content and information within your tab. You can use deep links to link your app with Teams as they tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="integrate-device-capabilities"></a><span data-ttu-id="17445-159">デバイス機能の統合</span><span class="sxs-lookup"><span data-stu-id="17445-159">Integrate device capabilities</span></span>

<span data-ttu-id="17445-160">Microsoft Teams プラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。</span><span class="sxs-lookup"><span data-stu-id="17445-160">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="17445-161">強化された Teams プラットフォームを使用すると、パートナーは、Microsoft Teams JavaScript クライアント SDK で利用できる専用 API を使用して、カメラ、QR、バーコード スキャナー、フォト ギャラリー、マイク、場所などのネイティブ デバイス機能にアクセスして統合できます。</span><span class="sxs-lookup"><span data-stu-id="17445-161">The enhanced Teams platform allows partners to access and integrate the native device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location using dedicated APIs available in Microsoft Teams JavaScript client SDK.</span></span> 

## <a name="see-also"></a><span data-ttu-id="17445-162">関連項目</span><span class="sxs-lookup"><span data-stu-id="17445-162">See also</span></span>

- [<span data-ttu-id="17445-163">アプリの使用例を Teams プラットフォーム機能にマップする</span><span class="sxs-lookup"><span data-stu-id="17445-163">Map your app's use cases to Teams platform capabilities</span></span>](~/concepts/design/map-use-cases.md)

- [<span data-ttu-id="17445-164">アプリのエントリ ポイントを決定する</span><span class="sxs-lookup"><span data-stu-id="17445-164">Determine your app's entry points</span></span>](~/concepts/extensibility-points.md)

- [<span data-ttu-id="17445-165">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="17445-165">Integrate web apps</span></span>](~/samples/integrating-web-apps.md)

- [<span data-ttu-id="17445-166">Microsoft Teams 用の低コードカスタム アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="17445-166">Create low-code custom apps for Microsoft Teams</span></span>](~/samples/teams-low-code-solutions.md)

- [<span data-ttu-id="17445-167">Power Virtual Agents チャットボットを追加する</span><span class="sxs-lookup"><span data-stu-id="17445-167">Add a Power Virtual Agents chatbot</span></span>](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)

- [<span data-ttu-id="17445-168">仮想アシスタントの作成</span><span class="sxs-lookup"><span data-stu-id="17445-168">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

- [<span data-ttu-id="17445-169">Microsoft Teams 用のアプリ テンプレート</span><span class="sxs-lookup"><span data-stu-id="17445-169">App templates for Microsoft Teams</span></span>](~/samples/app-templates.md)

- [<span data-ttu-id="17445-170">実稼働対応のシフト コネクタ</span><span class="sxs-lookup"><span data-stu-id="17445-170">Production-ready Shift Connectors</span></span>](~/samples/shifts-wfm-connectors.md)

- [<span data-ttu-id="17445-171">Moodle LMS のインストール</span><span class="sxs-lookup"><span data-stu-id="17445-171">Install Moodle LMS</span></span>](~/resources/moodleinstructions.md)

- <span data-ttu-id="17445-172">[[Teams で共有] ボタンを作成する](~/concepts/build-and-test/share-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="17445-172">[Create a Share-to-Teams button](~/concepts/build-and-test/share-to-teams.md)</span></span>

- [<span data-ttu-id="17445-173">SharePoint に Teams タブを追加する</span><span class="sxs-lookup"><span data-stu-id="17445-173">Add a Teams tab to SharePoint</span></span>](~/tabs/how-to/tabs-in-sharepoint.md)

- [<span data-ttu-id="17445-174">ディープ リンクの作成</span><span class="sxs-lookup"><span data-stu-id="17445-174">Create deep links</span></span>](~/concepts/build-and-test/deep-links.md)

- [<span data-ttu-id="17445-175">デバイス機能</span><span class="sxs-lookup"><span data-stu-id="17445-175">Device capabilities</span></span>](~/concepts/device-capabilities/device-capabilities-overview.md)
