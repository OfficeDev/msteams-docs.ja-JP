---
title: アプリの既定のインストール オプションを構成する
description: アプリの既定のインストール オプションを指定する方法について説明します。
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a4b70df70c7b9442e29953dae8a8c4e892cb72c1
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946491"
---
# <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="5358d-103">既定のインストール スコープとグループ機能を追加する</span><span class="sxs-lookup"><span data-stu-id="5358d-103">Add a default install scope and group capability</span></span>

<span data-ttu-id="5358d-104">アプリが Teams で複数のシナリオをサポートする場合は一般的ですが、特定の範囲と機能を念頭に置いて設計した可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5358d-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="5358d-105">たとえば、アプリが主にチームまたはチャネルを使用する場合は、ストアでユーザーに表示される最初のインストール オプションが [チームに追加] である必要 **があります**。</span><span class="sxs-lookup"><span data-stu-id="5358d-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

![アプリの追加](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="5358d-107">アプリの主な機能がボットである場合は、ユーザーがアプリをチームにインストールするときにボットを既定の機能にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="5358d-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span> 

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="5358d-108">アプリの既定のインストール スコープを構成する</span><span class="sxs-lookup"><span data-stu-id="5358d-108">Configure your app's default install scope</span></span>

<span data-ttu-id="5358d-109">アプリの既定のインストール スコープを構成します。</span><span class="sxs-lookup"><span data-stu-id="5358d-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="5358d-110">一度に設定できるスコープは 1 つのみです。</span><span class="sxs-lookup"><span data-stu-id="5358d-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="5358d-111">**アプリ マニフェストで既定のインストール スコープを構成するには**</span><span class="sxs-lookup"><span data-stu-id="5358d-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="5358d-112">アプリ マニフェストを開き、プロパティを追加 `defaultInstallScope` します。</span><span class="sxs-lookup"><span data-stu-id="5358d-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="5358d-113">、、または `personal` (以下の `team` 例 `groupchat` を参照) `meetings` の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="5358d-113">Set a value of `personal`, `team`, `groupchat`, or `meetings` (see an example below).</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="5358d-114">詳細については、「アプリ マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="5358d-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="5358d-115">共有スコープの既定の機能を構成する</span><span class="sxs-lookup"><span data-stu-id="5358d-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="5358d-116">チーム、会議、またはチャット用にアプリがインストールされている場合は、既定の機能を構成します。</span><span class="sxs-lookup"><span data-stu-id="5358d-116">Configure the default capability when your app is installed for a team, meeting, or chat.</span></span>

<span data-ttu-id="5358d-117">**アプリ マニフェストで詳細を構成するには**</span><span class="sxs-lookup"><span data-stu-id="5358d-117">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="5358d-118">アプリ マニフェストを開き、プロパティ `defaultGroupCapability` を追加します。</span><span class="sxs-lookup"><span data-stu-id="5358d-118">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="5358d-119">更新プログラムを保存します。</span><span class="sxs-lookup"><span data-stu-id="5358d-119">Save the updates.</span></span>

    <span data-ttu-id="5358d-120">JSON の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5358d-120">Following is a JSON example:</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```
> [!NOTE]
> <span data-ttu-id="5358d-121">完全なスキーマの詳細については、「マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="5358d-121">For information on full schema, see [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="5358d-122">次の手順</span><span class="sxs-lookup"><span data-stu-id="5358d-122">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5358d-123">アプリの配信方法を選ぶ</span><span class="sxs-lookup"><span data-stu-id="5358d-123">Choose how to distribute your app</span></span>](overview.md)
