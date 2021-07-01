---
title: ユーザー選択機能の統合
author: Rajeshwari-v
description: JavaScript クライアント SDK Teamsを使用してユーザー選択機能を統合する方法
keywords: ユーザー選択コントロール
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 8399eeb1a088e4b60c466d51c223b9405ebf1711
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211637"
---
# <a name="integrate-people-picker-capability"></a><span data-ttu-id="32d45-104">ユーザー選択機能の統合</span><span class="sxs-lookup"><span data-stu-id="32d45-104">Integrate People Picker capability</span></span> 

<span data-ttu-id="32d45-105">[ユーザー選択] は、ユーザーを検索して選択するコントロールです。</span><span class="sxs-lookup"><span data-stu-id="32d45-105">People Picker is a control to search and select people.</span></span> <span data-ttu-id="32d45-106">これは、プラットフォームで使用できるネイティブTeamsです。</span><span class="sxs-lookup"><span data-stu-id="32d45-106">This is a native capability available in Teams platform.</span></span> <span data-ttu-id="32d45-107">ネイティブのユーザー選択Teamsコントロールを Web アプリと統合できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-107">You can integrate Teams native People Picker input control with your web apps.</span></span> <span data-ttu-id="32d45-108">単一または複数の選択、および構成 (チャット、チャネル、組織全体での検索の制限など) を選択できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-108">You can select between single or multi selection, and configurations, such as limiting search within a chat, channels, or across the entire organization.</span></span>

<span data-ttu-id="32d45-109">Web アプリ内Microsoft Teamsユーザー選択機能を統合する API を提供する[JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK を `selectPeople` 使用できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-109">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides `selectPeople` API to integrate the People Picker capability within your web app.</span></span> 

## <a name="advantages-of-integrating-people-picker-capability"></a><span data-ttu-id="32d45-110">ユーザー選択機能を統合する利点</span><span class="sxs-lookup"><span data-stu-id="32d45-110">Advantages of integrating People Picker capability</span></span>

* <span data-ttu-id="32d45-111">People Picker コントロールは、タスク モジュール、Teams、チャネル、会議タブ、個人用アプリなど、すべてのユーザー 選択サーフェスで機能します。</span><span class="sxs-lookup"><span data-stu-id="32d45-111">The People Picker control works in all of Teams surfaces, such as task module, a chat, channel, meeting tab, and personal app.</span></span>
* <span data-ttu-id="32d45-112">このコントロールを使用すると、チャット、チャネル、または組織全体のユーザーを検索して選択できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-112">This control allows you to search for and select users within a chat, channel, or the entire organization.</span></span>
*  <span data-ttu-id="32d45-113">ユーザー選択機能は、タスクの割り当て、タグ付け、ユーザーへの通知に関するシナリオに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="32d45-113">The People Picker capability helps with scenarios involving task assignment, tagging, notifying a user.</span></span> 
* <span data-ttu-id="32d45-114">この簡単に利用できるコントロールは、Web アプリで使用できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-114">You can use this readily available control in your web app.</span></span> <span data-ttu-id="32d45-115">このようなコントロールを独自に構築する労力と時間を大幅に節約できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-115">It saves the effort and time significantly to build such a control on your own.</span></span>

<span data-ttu-id="32d45-116">ユーザー選択コントロールを `selectPeople` アプリに統合するには、API を呼び出Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="32d45-116">You must call the `selectPeople` API to integrate People Picker control in your Teams app.</span></span> <span data-ttu-id="32d45-117">効果的な統合を行う場合は、API を呼び出 [すコード スニペット](#code-snippet) について理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="32d45-117">For effective integration, you must have an understanding of [code snippet](#code-snippet) for calling the API.</span></span> <span data-ttu-id="32d45-118">Web アプリのエラーを処理するには [、API](#error-handling) 応答エラーについて理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="32d45-118">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your web app.</span></span>

> [!NOTE] 
> <span data-ttu-id="32d45-119">現在、Microsoft Teamsユーザー選択機能のサポートはモバイル クライアントでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-119">Currently, Microsoft Teams support for People Picker capability is available for mobile clients only.</span></span>

## <a name="selectpeople-api"></a><span data-ttu-id="32d45-120">`selectPeople` API</span><span class="sxs-lookup"><span data-stu-id="32d45-120">`selectPeople` API</span></span> 

<span data-ttu-id="32d45-121">`selectPeople`API を使用すると、web アプリTeamsネイティブ `People Picker input control` なアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-121">`selectPeople` API enables you to add Teams native `People Picker input control` to your web apps.</span></span>  
<span data-ttu-id="32d45-122">API の説明は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="32d45-122">The API description is as follows:</span></span>

| <span data-ttu-id="32d45-123">API</span><span class="sxs-lookup"><span data-stu-id="32d45-123">API</span></span>      | <span data-ttu-id="32d45-124">説明</span><span class="sxs-lookup"><span data-stu-id="32d45-124">Description</span></span>  |
| --- | --- |
|<span data-ttu-id="32d45-125">**selectPeople**</span><span class="sxs-lookup"><span data-stu-id="32d45-125">**selectPeople**</span></span>|<span data-ttu-id="32d45-126">ユーザー選択ツールを起動し、ユーザーがリストから 1 人または複数のユーザーを検索して選択できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-126">Launches a People Picker and allows the user to search and select one or more people from the list.</span></span><br/><br/><span data-ttu-id="32d45-127">この API は、選択したユーザーの ID、名前、電子メール アドレスを呼び出し元の Web アプリに返します。</span><span class="sxs-lookup"><span data-stu-id="32d45-127">This API returns the ID, name and email address of selected users to the calling web app.</span></span><br/><br/><span data-ttu-id="32d45-128">個人用アプリの場合、コントロールは組織全体を検索します。</span><span class="sxs-lookup"><span data-stu-id="32d45-128">In case of a personal app, the control searches across the organization.</span></span> <span data-ttu-id="32d45-129">アプリがチャットまたはチャネルに追加された場合、シナリオに応じて検索コンテキストが構成されます。</span><span class="sxs-lookup"><span data-stu-id="32d45-129">If the app is added to a chat or channel, then the search context is configured depending on the scenario.</span></span> <span data-ttu-id="32d45-130">検索は、そのチャット、チャネルのメンバー内で制限されている、または組織全体で利用できます。</span><span class="sxs-lookup"><span data-stu-id="32d45-130">The search is restricted within the members of that chat, channel, or made available across the organization.</span></span>|

<span data-ttu-id="32d45-131">`selectPeople`API には、次の入力構成が付属しています。</span><span class="sxs-lookup"><span data-stu-id="32d45-131">The `selectPeople` API comes along with following input configurations:</span></span>

|<span data-ttu-id="32d45-132">構成パラメーター</span><span class="sxs-lookup"><span data-stu-id="32d45-132">Configuration parameter</span></span>|<span data-ttu-id="32d45-133">種類</span><span class="sxs-lookup"><span data-stu-id="32d45-133">Type</span></span>|<span data-ttu-id="32d45-134">説明</span><span class="sxs-lookup"><span data-stu-id="32d45-134">Description</span></span>| <span data-ttu-id="32d45-135">既定値</span><span class="sxs-lookup"><span data-stu-id="32d45-135">Default value</span></span>|
|-----|------|--------------|------|
|`title`| <span data-ttu-id="32d45-136">String</span><span class="sxs-lookup"><span data-stu-id="32d45-136">String</span></span>| <span data-ttu-id="32d45-137">これはオプションのパラメーターです。</span><span class="sxs-lookup"><span data-stu-id="32d45-137">It is an optional parameter.</span></span> <span data-ttu-id="32d45-138">ユーザー選択コントロールのタイトルを設定します。</span><span class="sxs-lookup"><span data-stu-id="32d45-138">It sets title for the People Picker control.</span></span> | <span data-ttu-id="32d45-139">ユーザーを選択する</span><span class="sxs-lookup"><span data-stu-id="32d45-139">Select people</span></span>|
|`setSelected`|<span data-ttu-id="32d45-140">String</span><span class="sxs-lookup"><span data-stu-id="32d45-140">String</span></span>| <span data-ttu-id="32d45-141">これはオプションのパラメーターです。</span><span class="sxs-lookup"><span data-stu-id="32d45-141">It is an optional parameter.</span></span> <span data-ttu-id="32d45-142">事前に選択するユーザーの AAD の ID を渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="32d45-142">You must pass AAD IDs of the people to be preselected.</span></span> <span data-ttu-id="32d45-143">このパラメーターは、ユーザー選択コントロールの起動中にユーザーを事前に選択します。</span><span class="sxs-lookup"><span data-stu-id="32d45-143">This parameter preselects people while launching the People Picker control.</span></span> <span data-ttu-id="32d45-144">1 つの選択の場合、最初の有効なユーザーだけが、残りのユーザーを無視して事前設定されます。</span><span class="sxs-lookup"><span data-stu-id="32d45-144">In case of single selection, only the first valid user is prepopulated ignoring the rest.</span></span> |<span data-ttu-id="32d45-145">Null</span><span class="sxs-lookup"><span data-stu-id="32d45-145">Null</span></span>| 
|`openOrgWideSearchInChatOrChannel`|<span data-ttu-id="32d45-146">Boolean</span><span class="sxs-lookup"><span data-stu-id="32d45-146">Boolean</span></span> | <span data-ttu-id="32d45-147">これはオプションのパラメーターです。</span><span class="sxs-lookup"><span data-stu-id="32d45-147">It is an optional parameter.</span></span> <span data-ttu-id="32d45-148">true に設定すると、アプリがチャットやチャネルに追加された場合でも、組織全体のスコープでユーザー選択を起動します。</span><span class="sxs-lookup"><span data-stu-id="32d45-148">When it is set to true, it launches the People Picker in organization wide scope even if the app is added to a chat or channel.</span></span> |<span data-ttu-id="32d45-149">False</span><span class="sxs-lookup"><span data-stu-id="32d45-149">False</span></span>|
|`singleSelect`|<span data-ttu-id="32d45-150">Boolean</span><span class="sxs-lookup"><span data-stu-id="32d45-150">Boolean</span></span>|<span data-ttu-id="32d45-151">これはオプションのパラメーターです。</span><span class="sxs-lookup"><span data-stu-id="32d45-151">It is an optional parameter.</span></span> <span data-ttu-id="32d45-152">true に設定すると、選択を 1 人のユーザーにのみ制限するユーザー選択を起動します。</span><span class="sxs-lookup"><span data-stu-id="32d45-152">When it is set to true, it launches the People Picker restricting the selection to one user only.</span></span> |<span data-ttu-id="32d45-153">False</span><span class="sxs-lookup"><span data-stu-id="32d45-153">False</span></span>|

<span data-ttu-id="32d45-154">次の図は、サンプル Web アプリでのユーザー選択機能のエクスペリエンスを示しています。</span><span class="sxs-lookup"><span data-stu-id="32d45-154">The following image depicts the experience of People Picker capability in a sample web app:</span></span>

![ユーザー選択機能の Web アプリ エクスペリエンス](../../assets/images/tabs/people-picker-control-capability.png)

### <a name="code-snippet"></a><span data-ttu-id="32d45-156">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="32d45-156">Code snippet</span></span>

<span data-ttu-id="32d45-157">**通話 `selectPeople` リスト** からユーザーを選択する API:</span><span class="sxs-lookup"><span data-stu-id="32d45-157">**Calling `selectPeople` API** to select people from a list:</span></span>

```javascript
 microsoftTeams.people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
 {
    if (error) 
    {
        if (error.message) 
           {
             alert(" ErrorCode: " + error.errorCode + error.message);
           }
            else 
            {
              alert(" ErrorCode: " + error.errorCode);
            }
      }
    if (people)
     {
            output(" People length: " + people.length + " " + JSON.stringify(people));
      }
  });
```

## <a name="error-handling"></a><span data-ttu-id="32d45-158">エラー処理</span><span class="sxs-lookup"><span data-stu-id="32d45-158">Error handling</span></span>

<span data-ttu-id="32d45-159">Web アプリでエラーを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="32d45-159">You must ensure to handle the errors appropriately in your web app.</span></span> <span data-ttu-id="32d45-160">次の表に、エラー コードとエラーが生成される条件を示します。</span><span class="sxs-lookup"><span data-stu-id="32d45-160">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="32d45-161">エラー コード</span><span class="sxs-lookup"><span data-stu-id="32d45-161">Error code</span></span> |  <span data-ttu-id="32d45-162">エラー名</span><span class="sxs-lookup"><span data-stu-id="32d45-162">Error name</span></span>     | <span data-ttu-id="32d45-163">Condition</span><span class="sxs-lookup"><span data-stu-id="32d45-163">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="32d45-164">**100**</span><span class="sxs-lookup"><span data-stu-id="32d45-164">**100**</span></span> | <span data-ttu-id="32d45-165">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="32d45-165">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="32d45-166">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="32d45-166">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="32d45-167">**500**</span><span class="sxs-lookup"><span data-stu-id="32d45-167">**500**</span></span> | <span data-ttu-id="32d45-168">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="32d45-168">INTERNAL_ERROR</span></span> | <span data-ttu-id="32d45-169">ユーザー選択の起動中に内部エラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="32d45-169">Internal error is encountered while launching People Picker.</span></span>|
| <span data-ttu-id="32d45-170">**4000**</span><span class="sxs-lookup"><span data-stu-id="32d45-170">**4000**</span></span> | <span data-ttu-id="32d45-171">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="32d45-171">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="32d45-172">API は、間違った引数または不十分な必須引数を使用して呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="32d45-172">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="32d45-173">**8000**</span><span class="sxs-lookup"><span data-stu-id="32d45-173">**8000**</span></span> | <span data-ttu-id="32d45-174">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="32d45-174">USER_ABORT</span></span> |<span data-ttu-id="32d45-175">ユーザーが操作を取り消しました。</span><span class="sxs-lookup"><span data-stu-id="32d45-175">User cancelled the operation.</span></span>|
| <span data-ttu-id="32d45-176">**9000**</span><span class="sxs-lookup"><span data-stu-id="32d45-176">**9000**</span></span> | <span data-ttu-id="32d45-177">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="32d45-177">OLD_PLATFORM</span></span> | <span data-ttu-id="32d45-178">ユーザーは、API の実装が存在しない古いプラットフォーム ビルドに存在します。</span><span class="sxs-lookup"><span data-stu-id="32d45-178">User is on old platform build where implementation of the API is not present.</span></span>  <span data-ttu-id="32d45-179">ビルドをアップグレードすると、問題が解決します。</span><span class="sxs-lookup"><span data-stu-id="32d45-179">Upgrading the build resolves the issue.</span></span>|

## <a name="see-also"></a><span data-ttu-id="32d45-180">関連項目</span><span class="sxs-lookup"><span data-stu-id="32d45-180">See also</span></span>

* [<span data-ttu-id="32d45-181">メディア機能を統合Teams</span><span class="sxs-lookup"><span data-stu-id="32d45-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="32d45-182">QR コードまたはバーコード スキャナー機能をアプリに統合Teams</span><span class="sxs-lookup"><span data-stu-id="32d45-182">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="32d45-183">場所の機能を統合Teams</span><span class="sxs-lookup"><span data-stu-id="32d45-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
