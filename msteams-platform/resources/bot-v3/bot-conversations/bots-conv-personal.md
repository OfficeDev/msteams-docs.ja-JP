---
title: ボットとの 1 対 1 の会話
description: Microsoft Teams でボットと 1 対 1 の会話を行うエンドツーエンドのシナリオについて説明します。
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
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="1812b-104">Microsoft Teams ボットとの個人的な (1 対 1 の) 会話を行う</span><span class="sxs-lookup"><span data-stu-id="1812b-104">Have a personal (one-on-one) conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="1812b-105">Microsoft Teams を使用すると、ユーザーは Microsoft Bot [Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true)上に構築されたボットと直接会話できます。</span><span class="sxs-lookup"><span data-stu-id="1812b-105">Microsoft Teams allows users to engage in direct conversations with bots built on the [Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="1812b-106">ユーザーは、[アプリの検出] ギャラリーでボットを見つけ、個人の会話のために Teams エクスペリエンスに追加できます。</span><span class="sxs-lookup"><span data-stu-id="1812b-106">Users can find bots in the Discover Apps gallery and add them to their Teams experience for personal conversations.</span></span> <span data-ttu-id="1812b-107">適切なアクセス許可を持つチームの所有者とユーザーは、ボットをチーム メンバー[](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)として追加することもできます (「チーム チャネルでの対話」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="1812b-107">Team owners and users with the appropriate permissions can also add bots as team members (see [Interact in a team channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)), which not only makes them available in that team's channels, but for personal chat for all of those users as well.</span></span>

<span data-ttu-id="1812b-108">個人用チャットは、ユーザーがボットにアクセスする必要が@mention異なります。</span><span class="sxs-lookup"><span data-stu-id="1812b-108">Personal chat differs from chat in channels in that the user does not need to @mention the bot.</span></span> <span data-ttu-id="1812b-109">ボットが複数のコンテキスト (個人用、groupChat、またはチャネル) で使用されている場合は、ボットがグループ チャットまたはチャネル内にあるか検出し、メッセージを少し異なる方法で処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1812b-109">If a bot is used in multiple contexts (personal, groupChat or channel) you will need to detect if the bot is in a group chat or channel, and process messages a little differently.</span></span> <span data-ttu-id="1812b-110">詳細 [については、「チーム チャネルまたはグループ チャットでの対話」](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1812b-110">See [Interact in a team channel or group chat](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>

## <a name="designing-a-great-personal-bot"></a><span data-ttu-id="1812b-111">偉大な個人ボットの設計</span><span class="sxs-lookup"><span data-stu-id="1812b-111">Designing a great personal bot</span></span>

<span data-ttu-id="1812b-112">Microsoft Teams の偉大なボットは、ユーザーが Teams エクスペリエンスのコンテキスト内で必要な情報を取得するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="1812b-112">A great bot in Microsoft Teams helps users get the information they need, all within the context of the Teams experience.</span></span> <span data-ttu-id="1812b-113">ボットとの個人的な会話は、ボットとそのユーザー間のプライベートなやり取りです。個人のコンテキストで、そのユーザーに固有で関連性の高い情報を提供する最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="1812b-113">Personal conversations with a bot are private exchanges between a bot and its user; they're a great way to provide information specific and relevant to that user in the personal context.</span></span> <span data-ttu-id="1812b-114">個人用チャット内のボットは、実際にはサービスと個人の間のダイアログであり、グループ チャットまたはチャネル内のボットがグループのユーザーにすべてをブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="1812b-114">A bot in personal chat is really a dialog between your service and the individual, where a bot in a group chat or channel broadcasts everything to a group of people.</span></span>

<span data-ttu-id="1812b-115">作成するエクスペリエンスに応じて、ボットは個人、groupChat、チームなど、複数のスコープで作業する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1812b-115">Depending on the experience you want to create, the bot might need to work in multiple scopes - personal, groupChat and/or team.</span></span> <span data-ttu-id="1812b-116">複数のスコープをサポートする作業は最小限です。</span><span class="sxs-lookup"><span data-stu-id="1812b-116">The work to support more than one scope is minimal.</span></span> <span data-ttu-id="1812b-117">Teams では、ボットがすべてのスコープで機能するとは思ってはいありませんが、ボットが意味を持ち、サポートするために選択したスコープでユーザー値を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1812b-117">There is no expectation in Teams that your bot function in all scopes, but you should ensure that your bot makes sense and provides user value in whatever scope(s) you choose to support.</span></span>

## <a name="best-practice-welcome-messages-in-personal-conversations"></a><span data-ttu-id="1812b-118">ベスト プラクティス: 個人的な会話でのウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="1812b-118">Best practice: Welcome messages in personal conversations</span></span>

<span data-ttu-id="1812b-119">ボットは、 [ユーザー](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) がボットとの個人用チャットを初めて (初めて) 開始する場合にのみ、事前にウェルカム メッセージを個人チャットに送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1812b-119">Your bot should [proactively send](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) a welcome message to a personal chat the first time (and only the first time) a user initiates a personal chat with your bot.</span></span> <span data-ttu-id="1812b-120">(この推奨事項は、チャネルの初回連絡先には適用されません)。</span><span class="sxs-lookup"><span data-stu-id="1812b-120">(This recommendation does not apply to first-time contacts in a channel.)</span></span>
