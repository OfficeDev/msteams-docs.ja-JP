---
title: 個人用アプリのタブの順序を変更する
description: 個人用アプリで個人用アプリの静的タブの順序を変更する方法
keywords: teams タブの開発
ms.openlocfilehash: a8a7c3d23bac98ef1085a8f3443ca0fc92ae0a31
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49554830"
---
# <a name="reorder-personal-app-tabs"></a><span data-ttu-id="17e7c-104">個人用アプリのタブの順序を変更する</span><span class="sxs-lookup"><span data-stu-id="17e7c-104">Reorder personal app tabs</span></span>

<span data-ttu-id="17e7c-105">マニフェストバージョン1.7 の開発者は、個人用アプリのすべてのタブを再配置できます。</span><span class="sxs-lookup"><span data-stu-id="17e7c-105">Starting with manifest version 1.7 developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="17e7c-106">特に、開発者は、[個人情報] タブヘッダー内の任意の場所にある "bot チャット" タブ (常に最初の位置に既定で指定されています) を移動することができます。</span><span class="sxs-lookup"><span data-stu-id="17e7c-106">In particular, a developer can move the “bot chat” tab (which has always defaulted to the first position) anywhere in the personal app tab header.</span></span> <span data-ttu-id="17e7c-107">2つの予約済みタブ entityId キーワードを宣言しました。「会話」と「about」。</span><span class="sxs-lookup"><span data-stu-id="17e7c-107">We’ve declared two reserved tab entityId keywords: “conversations” and “about”.</span></span>

## <a name="moving-the-chatconversation-tab"></a><span data-ttu-id="17e7c-108">[チャット/会話] タブの移動</span><span class="sxs-lookup"><span data-stu-id="17e7c-108">Moving the “Chat/Conversation” tab</span></span>

<span data-ttu-id="17e7c-109">"Personal" スコープを持つ bot を作成すると、パーソナルアプリの最初のタブ位置に常に表示されます。</span><span class="sxs-lookup"><span data-stu-id="17e7c-109">If you create a bot with a “personal” scope, it will always show up in the first tab position in a personal app.</span></span> <span data-ttu-id="17e7c-110">別の位置に移動する場合は、予約済みのキーワード "会話" を使用して、静的な tab オブジェクトをマニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="17e7c-110">If you wish to move it to another position, you need to add a static tab object to your manifest with the reserved keyword “conversations”.</span></span> <span data-ttu-id="17e7c-111">「StaticTabs」配列に [会話] タブを追加すると、web とデスクトップに [会話] タブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="17e7c-111">Wherever you add the “conversations” tab in the “staticTabs” array, that’s where the conversation tab will appear on web and desktop.</span></span> 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

> [!NOTE]
> <span data-ttu-id="17e7c-112">個人用の bot チャットには、個人用アプリ内に専用の場所があるため、この動作はモバイルには反映されていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="17e7c-112">Note that this behavior is not reflected on mobile since the personal bot chat already has a dedicated place within the personal app.</span></span>

## <a name="moving-the-about-tab"></a><span data-ttu-id="17e7c-113">[バージョン情報] タブの移動</span><span class="sxs-lookup"><span data-stu-id="17e7c-113">Moving the “About” tab</span></span>

<span data-ttu-id="17e7c-114">[About] タブは、常に [個人用アプリ] タブのヘッダーバーの末尾に表示されます。</span><span class="sxs-lookup"><span data-stu-id="17e7c-114">The “About” tab always defaults to the end of the personal app tab header bar.</span></span> <span data-ttu-id="17e7c-115">別の位置に移動する場合は、"about" entityId を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="17e7c-115">If you wish to move it to another position, you need to use the “about” entityId.</span></span>

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
> [!NOTE]
> <span data-ttu-id="17e7c-116">[バージョン情報] タブは、モバイルでは表示されません。</span><span class="sxs-lookup"><span data-stu-id="17e7c-116">Note that the about tab is not shown on mobile.</span></span>

## <a name="example-code"></a><span data-ttu-id="17e7c-117">コード例</span><span class="sxs-lookup"><span data-stu-id="17e7c-117">Example code</span></span>

```json
{
   "staticTabs":[
      {
         "entityId":"homeTab",
         "name":"Home",
         "contentUrl":"https://www.contoso.com",
         "websiteUrl":" https://www.contoso.com ",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
