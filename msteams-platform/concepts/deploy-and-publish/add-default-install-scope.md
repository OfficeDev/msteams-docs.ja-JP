---
title: アプリの既定のインストール オプションを構成する
description: アプリの既定のインストール オプションを指定する方法について説明します。
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 561a4f2910e703db5ffce6176f6177dfd661d2ce
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230933"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a><span data-ttu-id="dd3f2-103">アプリの既定のインストール オプションをMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="dd3f2-103">Configure default install options for your Microsoft Teams app</span></span>

<span data-ttu-id="dd3f2-104">アプリは、アプリで複数のシナリオをサポートTeams一般的ですが、特定の範囲と機能を念頭に置いて設計した可能性があります。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="dd3f2-105">たとえば、アプリが主にチームまたはチャネルを使用する場合は、ストアでユーザーに表示される最初のインストール オプションが [チームに追加] である必要 **があります**。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

:::row:::
   :::column span="2":::

![アプリのドロップダウンの例を追加する](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

<span data-ttu-id="dd3f2-107">アプリの主な機能がボットである場合は、ユーザーがアプリをチームにインストールするときにボットを既定の機能にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span>

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="dd3f2-108">アプリの既定のインストール スコープを構成する</span><span class="sxs-lookup"><span data-stu-id="dd3f2-108">Configure your app's default install scope</span></span>

<span data-ttu-id="dd3f2-109">アプリの既定のインストール スコープを構成します。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="dd3f2-110">一度に設定できるスコープは 1 つのみです。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="dd3f2-111">**アプリ マニフェストで既定のインストール スコープを構成するには**</span><span class="sxs-lookup"><span data-stu-id="dd3f2-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="dd3f2-112">アプリ マニフェストを開き、プロパティを追加 `defaultInstallScope` します。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="dd3f2-113">既定のインストール スコープの値を 、のいずれか `personal` `team` `groupchat` として設定します `meetings` 。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-113">Set default install scope value as, either `personal`, `team`, `groupchat`, or `meetings`.</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="dd3f2-114">詳細については、「アプリ マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="dd3f2-115">共有スコープの既定の機能を構成する</span><span class="sxs-lookup"><span data-stu-id="dd3f2-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="dd3f2-116">チーム、会議、またはグループチャット用にアプリがインストールされている場合は、既定の機能を構成します。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-116">Configure the default capability when your app is installed for a team, meeting, or groupchat.</span></span>

> [!NOTE]
> <span data-ttu-id="dd3f2-117">`defaultGroupCapability` は、チーム、グループチャット、または会議に追加される既定の機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-117">`defaultGroupCapability` provides the default capability that will be added to the team, groupchat, or meeting.</span></span> <span data-ttu-id="dd3f2-118">アプリの既定の機能としてタブ、ボット、またはコネクタを選択しますが、アプリ定義で選択した機能が提供されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-118">Select a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

<span data-ttu-id="dd3f2-119">**アプリ マニフェストで詳細を構成するには**</span><span class="sxs-lookup"><span data-stu-id="dd3f2-119">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="dd3f2-120">アプリ マニフェストを開き、プロパティ `defaultGroupCapability` を追加します。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-120">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="dd3f2-121">、または `team` の値 `groupchat` を設定します `meetings` 。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-121">Set a value of `team`, `groupchat`, or `meetings`.</span></span>
3. <span data-ttu-id="dd3f2-122">選択したグループ機能の場合、使用可能なグループ機能は `bot` `tab` 、、またはです `connector` 。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-122">For the selected group capability, the available group capabilities are, `bot`, `tab`, or `connector`.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="dd3f2-123">既定の機能 、、または選択したグループ機能の `bot` `tab` `connector` 1 つのみ選択できます。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-123">You can select only one default capability, `bot`, `tab`, or `connector` for the selected group capability.</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> <span data-ttu-id="dd3f2-124">詳細については、「アプリ マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="dd3f2-124">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="dd3f2-125">次の手順</span><span class="sxs-lookup"><span data-stu-id="dd3f2-125">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd3f2-126">アプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="dd3f2-126">Create your app package</span></span>](~/concepts/build-and-test/apps-package.md)
