---
title: 公開後にすべきこと
description: アプリの公開後にすべきこと
keywords: Teams、公開後、更新、証明書
ms.openlocfilehash: 05e4ea47bbf81967ccf086230bf0ad8c633f6e0b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674719"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="4fa81-104">公開したアプリの保守およびサポート</span><span class="sxs-lookup"><span data-stu-id="4fa81-104">Maintain and support your published app</span></span> 

<span data-ttu-id="4fa81-105">アプリが承認され、公開アプリ カタログに一覧表示されたら、アプリの認定を取得するか、Web サイトに [ダウンロード] ボタンを追加して、利用対象者を増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="4fa81-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="4fa81-106">アプリケーション証明書</span><span class="sxs-lookup"><span data-stu-id="4fa81-106">Application Certificate</span></span>

<span data-ttu-id="4fa81-107">Microsoft では、[アプリケーション証明書プログラム](./application-certification.md)を用意しています。アプリ情報を編集するプログラムで、[Microsoft Teams アプリのセキュリティとコンプライアンスのページ](https://aka.ms/AppCertification)で提供されます。</span><span class="sxs-lookup"><span data-stu-id="4fa81-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="4fa81-108">この情報は、管理者が組織にとって安全なアプリを選択できるようにすることを目的としています。</span><span class="sxs-lookup"><span data-stu-id="4fa81-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="4fa81-109">製品サイトに [ダウンロード] ボタンを追加する</span><span class="sxs-lookup"><span data-stu-id="4fa81-109">Add a download button to your product site</span></span>

<span data-ttu-id="4fa81-110">アプリが Microsoft Teams ストアにある場合、Web サイトのリンクを生成できます。このリンクによって、Teams が起動し、ユーザーがアプリを追加する際の同意とインストールのダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4fa81-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="4fa81-111">形式は `https://teams.microsoft.com/l/app/<appId>` で、appID は、送信されたマニフェストで宣言する GUID です。</span><span class="sxs-lookup"><span data-stu-id="4fa81-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="4fa81-112">たとえば、`https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` は、Trello をインストールするためのリンクになります。</span><span class="sxs-lookup"><span data-stu-id="4fa81-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="4fa81-113">既存の Teams アプリを更新する</span><span class="sxs-lookup"><span data-stu-id="4fa81-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="4fa81-114">アプリを再送信する際に、*[新しいアプリの追加]* ボタンは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="4fa81-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="4fa81-115">代わりに、[概要] タブのアプリのタイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="4fa81-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="4fa81-116">更新されたマニフェストの appId は、現在のマニフェストと同じであり、バージョンの番号もインクリメントされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fa81-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="4fa81-117">マニフェストのバージョン番号をインクリメントします。</span><span class="sxs-lookup"><span data-stu-id="4fa81-117">Increment your version number in your manifest.</span></span>

### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a><span data-ttu-id="4fa81-118">アプリ更新の際にユーザーの同意フローがトリガーされる場合</span><span class="sxs-lookup"><span data-stu-id="4fa81-118">When does updating your app trigger the user consent flow?</span></span>

<span data-ttu-id="4fa81-119">ユーザーがアプリケーションをインストールするとき、まず、アプリがジョブを実行するのに必要なサービスと情報へのアクセス許可をアプリに与えることに同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fa81-119">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="4fa81-120">アプリを更新し、以下の変更を 1 つまたは複数行った場合、この同意の動作が再びトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="4fa81-120">When you update your app, that can re-trigger this consent behavior, particularly if you have made one or more of the following changes:</span></span>

* <span data-ttu-id="4fa81-121">タブのみのアプリへのボットの追加など、アプリに新しい機能を追加する。</span><span class="sxs-lookup"><span data-stu-id="4fa81-121">Adding a new capability to an app such as adding a bot to an tab only app.</span></span>
* <span data-ttu-id="4fa81-122">マニフェストでアクセス許可の配列を変更する。</span><span class="sxs-lookup"><span data-stu-id="4fa81-122">Changing the permissions array in the manifest.</span></span>
* <span data-ttu-id="4fa81-123">マニフェストでのアプリのバージョン番号をインクリメントする。</span><span class="sxs-lookup"><span data-stu-id="4fa81-123">Increment your app version number in your manifest.</span></span>
