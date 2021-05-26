---
title: 会議のTeamsアプリ
author: laujan
description: 参加者とユーザーの役割に基Teams会議でのアプリの概要
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 1fdf3d55219d80d6953ffa0865b223dd626053f6
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649665"
---
# <a name="apps-for-teams-meetings"></a><span data-ttu-id="62446-104">会議のTeamsアプリ</span><span class="sxs-lookup"><span data-stu-id="62446-104">Apps for Teams meetings</span></span>

<span data-ttu-id="62446-105">会議では、包括的でアクティブなフォーラムで、共同作業、パートナーシップ、情報に基づいたコミュニケーション、共有フィードバックが可能になります。</span><span class="sxs-lookup"><span data-stu-id="62446-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="62446-106">会議アプリは、出席者の状態に応じて、会議前、会議中、会議後のアプリ エクスペリエンスを含む会議ライフサイクルの各ステージに対してユーザー エクスペリエンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="62446-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting, and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="62446-107">ユーザーは、次に示すタブ ギャラリーを使用して会議中にアプリにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="62446-107">The users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="62446-108">かんばんボードを事前に設定します。</span><span class="sxs-lookup"><span data-stu-id="62446-108">Pre-stage a Kanban board.</span></span>
* <span data-ttu-id="62446-109">会議中の操作可能なダイアログを起動します。</span><span class="sxs-lookup"><span data-stu-id="62446-109">Launch an in-meeting actionable dialog.</span></span>
* <span data-ttu-id="62446-110">会議後のアンケートを作成します。</span><span class="sxs-lookup"><span data-stu-id="62446-110">Create a post-meeting survey.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/nKAy5rNDus4]

<span data-ttu-id="62446-111">この記事では、会議アプリの機能拡張、API リファレンス、会議用アプリの有効化と構成、および会議の一緒にモードの概要をTeams。</span><span class="sxs-lookup"><span data-stu-id="62446-111">This article provides an overview of meeting app extensibility, API references, enable and configure apps for meetings, and Together Mode in Teams.</span></span>

<span data-ttu-id="62446-112">会議の機能拡張機能を使用すると、会議のエクスペリエンスを向上できます。これにより、会議内でアプリを統合できます。</span><span class="sxs-lookup"><span data-stu-id="62446-112">You can enhance your meeting experience by using the meeting extensibility feature, which enables you to integrate your apps within meetings.</span></span> <span data-ttu-id="62446-113">また、タブ、ボット、メッセージング拡張機能を統合できる会議のライフサイクルの異なるステージも含まれています。</span><span class="sxs-lookup"><span data-stu-id="62446-113">It also includes different stages of a meeting lifecycle, where you can integrate tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="62446-114">会議機能拡張 API を使用すると、さまざまな参加者の役割とユーザーの種類を識別し、会議イベントを取得し、会議内ダイアログを生成できます。</span><span class="sxs-lookup"><span data-stu-id="62446-114">With meetings extensibility APIs, you can identify different participant roles and user types, get meeting events, generate in-meeting dialogs, and so on.</span></span>

<span data-ttu-id="62446-115">会議用Teamsを使用してアプリをカスタマイズするには、アプリ マニフェストを更新して Teams 会議のアプリを有効にし、会議のシナリオ用にアプリを構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="62446-115">To customize Teams with apps for meetings, you can enable your apps for Teams meetings by updating your app manifest and you can also configure your apps for meeting scenarios.</span></span>

<span data-ttu-id="62446-116">新しい Together Mode 機能により、ユーザーは、ボックスで区切ることなく、チームとの会議で 1 か所で共同作業を行えます。</span><span class="sxs-lookup"><span data-stu-id="62446-116">The new Together Mode feature enables users to collaborate in a meeting with their team in one place without being separated by boxes.</span></span>

## <a name="see-also"></a><span data-ttu-id="62446-117">関連項目</span><span class="sxs-lookup"><span data-stu-id="62446-117">See also</span></span>

* [<span data-ttu-id="62446-118">Tab</span><span class="sxs-lookup"><span data-stu-id="62446-118">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="62446-119">ボット</span><span class="sxs-lookup"><span data-stu-id="62446-119">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="62446-120">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="62446-120">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="62446-121">アプリをデザインする</span><span class="sxs-lookup"><span data-stu-id="62446-121">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="62446-122">会議でのアプリの前提条件と API Teams参照</span><span class="sxs-lookup"><span data-stu-id="62446-122">Prerequisites and API references for apps in Teams meetings</span></span>](create-apps-for-teams-meetings.md)
* [<span data-ttu-id="62446-123">一緒にモード</span><span class="sxs-lookup"><span data-stu-id="62446-123">Together Mode</span></span>](~/apps-in-teams-meetings/teams-together-mode.md)

## <a name="next-step"></a><span data-ttu-id="62446-124">次の手順</span><span class="sxs-lookup"><span data-stu-id="62446-124">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62446-125">会議アプリの機能拡張</span><span class="sxs-lookup"><span data-stu-id="62446-125">Meeting app extensibility</span></span>](meeting-app-extensibility.md)
