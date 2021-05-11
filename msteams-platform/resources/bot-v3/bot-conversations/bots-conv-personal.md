---
title: ボットとの 1 対 1 の会話
description: ボットと 1 対 1 の会話を行うというエンドツーエンドのシナリオについて説明Microsoft Teams
keywords: teams シナリオ 1on1 1to1 会話ボット
localization_priority: Normal
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: 2942a6c53bc99ce3199e140263d939e8b16d9db6
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020675"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="fea58-104">ユーザーボットと個人的な (1 対 1 の) 会話Microsoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="fea58-104">Have a personal (one-on-one) conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="fea58-105">Microsoft Teamsを使用すると、ユーザーは、アプリに基[Microsoft Bot Framework。](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="fea58-105">Microsoft Teams allows users to engage in direct conversations with bots built on the [Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="fea58-106">ユーザーは、[アプリの検出] ギャラリーでボットを見つけて、Teamsのエクスペリエンスに追加できます。</span><span class="sxs-lookup"><span data-stu-id="fea58-106">Users can find bots in the Discover Apps gallery and add them to their Teams experience for personal conversations.</span></span> <span data-ttu-id="fea58-107">適切なアクセス許可を持つチームの所有者とユーザーは、ボットをチーム メンバー[](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)として追加することもできます (「チーム チャネルでの対話」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="fea58-107">Team owners and users with the appropriate permissions can also add bots as team members (see [Interact in a team channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)), which not only makes them available in that team's channels, but for personal chat for all of those users as well.</span></span>

<span data-ttu-id="fea58-108">個人用チャットは、ユーザーがボットにアクセスする必要が@mention異なります。</span><span class="sxs-lookup"><span data-stu-id="fea58-108">Personal chat differs from chat in channels in that the user does not need to @mention the bot.</span></span> <span data-ttu-id="fea58-109">ボットが複数のコンテキスト (個人用、groupChat、またはチャネル) で使用されている場合は、ボットがグループ チャットまたはチャネル内にあるか検出し、メッセージを少し異なる方法で処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fea58-109">If a bot is used in multiple contexts (personal, groupChat or channel) you will need to detect if the bot is in a group chat or channel, and process messages a little differently.</span></span> <span data-ttu-id="fea58-110">詳細 [については、「チーム チャネルまたはグループ チャットでの対話」](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fea58-110">See [Interact in a team channel or group chat](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>

## <a name="designing-a-great-personal-bot"></a><span data-ttu-id="fea58-111">偉大な個人ボットの設計</span><span class="sxs-lookup"><span data-stu-id="fea58-111">Designing a great personal bot</span></span>

<span data-ttu-id="fea58-112">ユーザーが必要なMicrosoft Teams、ユーザーエクスペリエンスのコンテキスト内で、ユーザーが必要な情報をTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="fea58-112">A great bot in Microsoft Teams helps users get the information they need, all within the context of the Teams experience.</span></span> <span data-ttu-id="fea58-113">ボットとの個人的な会話は、ボットとそのユーザー間のプライベートなやり取りです。個人のコンテキストで、そのユーザーに固有で関連性の高い情報を提供する最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="fea58-113">Personal conversations with a bot are private exchanges between a bot and its user; they're a great way to provide information specific and relevant to that user in the personal context.</span></span> <span data-ttu-id="fea58-114">個人用チャット内のボットは、実際にはサービスと個人の間のダイアログであり、グループ チャットまたはチャネル内のボットがグループのユーザーにすべてをブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="fea58-114">A bot in personal chat is really a dialog between your service and the individual, where a bot in a group chat or channel broadcasts everything to a group of people.</span></span>

<span data-ttu-id="fea58-115">作成するエクスペリエンスに応じて、ボットは個人、groupChat、チームなど、複数のスコープで作業する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fea58-115">Depending on the experience you want to create, the bot might need to work in multiple scopes - personal, groupChat and/or team.</span></span> <span data-ttu-id="fea58-116">複数のスコープをサポートする作業は最小限です。</span><span class="sxs-lookup"><span data-stu-id="fea58-116">The work to support more than one scope is minimal.</span></span> <span data-ttu-id="fea58-117">Teams では、ボットがすべてのスコープで機能するとは思ってはいありませんが、ボットが意味を持ち、サポートするスコープでユーザー値を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fea58-117">There is no expectation in Teams that your bot function in all scopes, but you should ensure that your bot makes sense and provides user value in whatever scope(s) you choose to support.</span></span>

## <a name="best-practice-welcome-messages-in-personal-conversations"></a><span data-ttu-id="fea58-118">ベスト プラクティス: 個人的な会話でのウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="fea58-118">Best practice: Welcome messages in personal conversations</span></span>

<span data-ttu-id="fea58-119">ボットは、 [ユーザー](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) がボットとの個人用チャットを初めて (初めて) 開始する場合にのみ、事前にウェルカム メッセージを個人チャットに送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fea58-119">Your bot should [proactively send](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) a welcome message to a personal chat the first time (and only the first time) a user initiates a personal chat with your bot.</span></span> <span data-ttu-id="fea58-120">(この推奨事項は、チャネルの初回連絡先には適用されません)。</span><span class="sxs-lookup"><span data-stu-id="fea58-120">(This recommendation does not apply to first-time contacts in a channel.)</span></span>
