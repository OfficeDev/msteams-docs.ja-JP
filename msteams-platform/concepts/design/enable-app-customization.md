---
title: アプリのカスタマイズを有効にする
author: heath-hamilton
description: 管理者が組織Teamsアプリをカスタマイズする方法について説明します。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: bf1b43629c87dd4123520c634772e5dea14e0bb5
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915084"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a><span data-ttu-id="2d120-103">アプリMicrosoft Teamsカスタマイズを有効にする</span><span class="sxs-lookup"><span data-stu-id="2d120-103">Enable your Microsoft Teams app to be customized</span></span>

<span data-ttu-id="2d120-104">顧客が管理センターでアプリのMicrosoft TeamsをカスタマイズTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="2d120-104">You can allow customers to customize some aspects of your Microsoft Teams app in the Teams admin center.</span></span> <span data-ttu-id="2d120-105">この機能は、アプリ ストアに発行されたアプリTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="2d120-105">This feature is supported only for apps published to the Teams store.</span></span> <span data-ttu-id="2d120-106">組織用に公開されたサイドロードされたアプリとアプリはカスタマイズできません。</span><span class="sxs-lookup"><span data-stu-id="2d120-106">Sideloaded apps and apps published for an org can't be customized.</span></span>

<span data-ttu-id="2d120-107">この機能のいくつかの考えられる例は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2d120-107">Some possible examples of this feature include:</span></span>

* <span data-ttu-id="2d120-108">アプリのアクセントカラーを組織のブランドに合わせて変更する。</span><span class="sxs-lookup"><span data-stu-id="2d120-108">Changing the app's accent color to match an org's brand.</span></span>
* <span data-ttu-id="2d120-109">Contoso から Contoso *エージェント\*\*にアプリ* 名を更新すると、組織のユーザーに表示される名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="2d120-109">Updating the app name from *Contoso* to *Contoso Agent*, which is the name users in the org will see.</span></span> <span data-ttu-id="2d120-110">(注: チャットまたはチャネルにコネクタを追加するユーザーには、元のアプリ名 Contoso .) が引き続き *表示* されます。</span><span class="sxs-lookup"><span data-stu-id="2d120-110">(Note: Users adding a connector to a chat or a channel will still see the original app name, *Contoso*.)</span></span>

<span data-ttu-id="2d120-111">開発者ポータルでこの機能を有効に[Teams。](https://dev.teams.microsoft.com/home)</span><span class="sxs-lookup"><span data-stu-id="2d120-111">You can enable this feature in the [Developer Portal for Teams](https://dev.teams.microsoft.com/home).</span></span> <span data-ttu-id="2d120-112">これは、アプリ マニフェストの `configurableProperties` 1.10 より前のバージョンではTeams構成されます。</span><span class="sxs-lookup"><span data-stu-id="2d120-112">This configures `configurableProperties`, which aren't available in versions prior to 1.10 of the Teams app manifest.</span></span>

## <a name="test-your-app"></a><span data-ttu-id="2d120-113">アプリのテスト</span><span class="sxs-lookup"><span data-stu-id="2d120-113">Test your app</span></span>

<span data-ttu-id="2d120-114">開発中にこの機能をテストすることはできません。</span><span class="sxs-lookup"><span data-stu-id="2d120-114">You cannot test this feature during development.</span></span> <span data-ttu-id="2d120-115">アプリのカスタマイズは、組織のアプリ カタログへのサイドローディングまたは発行ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2d120-115">App customization is not supported for sideloading or publishing to an organization's app catalog.</span></span>

## <a name="user-considerations"></a><span data-ttu-id="2d120-116">ユーザーの考慮事項</span><span class="sxs-lookup"><span data-stu-id="2d120-116">User considerations</span></span>

<span data-ttu-id="2d120-117">アプリの発行元として、管理者のユーザーに次の情報Teamsします。</span><span class="sxs-lookup"><span data-stu-id="2d120-117">As the app publisher, provide the following information to customers in Teams admins:</span></span>
* <span data-ttu-id="2d120-118">実稼働環境で変更を加える前に、Teamsテナントでカスタマイズの変更をテストすることをお勧めのメモを含めます。</span><span class="sxs-lookup"><span data-stu-id="2d120-118">Include a note recommending to test customization changes in a Teams test tenant before making changes in their production environment.</span></span> 
* <span data-ttu-id="2d120-119">アプリをカスタマイズする方法のベスト プラクティスを提供します。</span><span class="sxs-lookup"><span data-stu-id="2d120-119">Provide best practices for how to customize your app.</span></span>

## <a name="see-also"></a><span data-ttu-id="2d120-120">関連項目</span><span class="sxs-lookup"><span data-stu-id="2d120-120">See also</span></span>

* [<span data-ttu-id="2d120-121">管理センターでアプリTeamsカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="2d120-121">Customize apps in the Teams admin center</span></span>](/MicrosoftTeams/customize-apps)
