---
title: 投稿の公開
description: アプリを発行した後の作業
keywords: teams 投稿の発行更新証明書
ms.openlocfilehash: 05e4ea47bbf81967ccf086230bf0ad8c633f6e0b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674719"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="b08e4-104">公開したアプリを保守およびサポートする</span><span class="sxs-lookup"><span data-stu-id="b08e4-104">Maintain and support your published app</span></span> 

<span data-ttu-id="b08e4-105">アプリが承認され、パブリックアプリカタログに表示された後は、アプリの証明書を取得するか、web サイトの [ダウンロード] ボタンを追加することによって、ユーザーのリーチを増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="b08e4-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="b08e4-106">アプリケーション証明書</span><span class="sxs-lookup"><span data-stu-id="b08e4-106">Application Certificate</span></span>

<span data-ttu-id="b08e4-107">Microsoft は、アプリ情報をコンパイルして[Microsoft Teams アプリのセキュリティとコンプライアンスのページ](https://aka.ms/AppCertification)に表示する[アプリケーション認定プログラム](./application-certification.md)を提供しています。</span><span class="sxs-lookup"><span data-stu-id="b08e4-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="b08e4-108">この情報は、管理者が組織にとって安全なアプリを選択できるようにすることを目的としています。</span><span class="sxs-lookup"><span data-stu-id="b08e4-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="b08e4-109">製品サイトにダウンロードボタンを追加する</span><span class="sxs-lookup"><span data-stu-id="b08e4-109">Add a download button to your product site</span></span>

<span data-ttu-id="b08e4-110">アプリが Microsoft Teams ストアにある場合は、Teams を起動する web サイトへのリンクを生成し、ユーザーがアプリを追加するための同意とインストールダイアログを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="b08e4-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="b08e4-111">形式は次の`https://teams.microsoft.com/l/app/<appId>`とおりです。 appID は、送信されたマニフェストで宣言する GUID です。</span><span class="sxs-lookup"><span data-stu-id="b08e4-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="b08e4-112">例: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd`は、Trello をインストールするためのリンクです。</span><span class="sxs-lookup"><span data-stu-id="b08e4-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="b08e4-113">既存の Teams アプリを更新する</span><span class="sxs-lookup"><span data-stu-id="b08e4-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="b08e4-114">アプリを再送信するには、[*新しいアプリの追加*] ボタンを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="b08e4-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="b08e4-115">代わりに、[概要] タブでアプリのタイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="b08e4-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="b08e4-116">更新されたマニフェスト内の appId は、現在のマニフェストと同じであり、バージョン番号が増やされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="b08e4-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="b08e4-117">マニフェストでバージョン番号をインクリメントします。</span><span class="sxs-lookup"><span data-stu-id="b08e4-117">Increment your version number in your manifest.</span></span>

### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a><span data-ttu-id="b08e4-118">アプリの更新によってユーザーの同意フローがトリガーされるのはいつですか?</span><span class="sxs-lookup"><span data-stu-id="b08e4-118">When does updating your app trigger the user consent flow?</span></span>

<span data-ttu-id="b08e4-119">ユーザーがアプリケーションをインストールするときに、最初に行うことは、アプリがジョブを実行するために必要なサービスと情報にアクセスするためのアクセス許可を付与するための同意です。</span><span class="sxs-lookup"><span data-stu-id="b08e4-119">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="b08e4-120">アプリを更新すると、特に以下の1つ以上の変更を行った場合に、この同意の動作を再始動することができます。</span><span class="sxs-lookup"><span data-stu-id="b08e4-120">When you update your app, that can re-trigger this consent behavior, particularly if you have made one or more of the following changes:</span></span>

* <span data-ttu-id="b08e4-121">アプリケーションに新しい機能を追加する。たとえば、タブのみのアプリに bot を追加することができます。</span><span class="sxs-lookup"><span data-stu-id="b08e4-121">Adding a new capability to an app such as adding a bot to an tab only app.</span></span>
* <span data-ttu-id="b08e4-122">マニフェスト内のアクセス許可の配列を変更します。</span><span class="sxs-lookup"><span data-stu-id="b08e4-122">Changing the permissions array in the manifest.</span></span>
* <span data-ttu-id="b08e4-123">マニフェストでアプリのバージョン番号をインクリメントします。</span><span class="sxs-lookup"><span data-stu-id="b08e4-123">Increment your app version number in your manifest.</span></span>
