---
title: タブの余白を削除Microsoft Teams
author: surbhigupta
description: タブ 余白を削除すると、開発者のエクスペリエンスが向上する方法について説明します。
keywords: タブの余白の余白の削除
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 4bbf7bce62e24c61d23e7fa90f1ccd3e6c5a3371
ms.sourcegitcommit: 1c4eaccee16dc63a1f2b5d7da2893d68f9c1533a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2021
ms.locfileid: "53534601"
---
# <a name="tab-margin-changes"></a>タブ余白の変更

このドキュメントでは、アプリを構築する際に、Microsoft Teamsタブの余白を削除すると、開発者のエクスペリエンスが向上する方法について説明します。 これは、2021 年にMicrosoft Teams拡張機能です。
すべてのタブの余白を削除すると、開発者はアプリのネイティブに見えるアプリをTeams。 これは、UI キットのデザイン [にも対応します](~/tabs/design/tabs.md)。 ほとんどのアプリは、エクスペリエンスを取り巻く余白がなくても、既に見た目が良くなります。 ただし、一部のタブは、この変更によって視覚的に影響を受け、開発者は必要な変更を行う必要があります。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="タブの wit と余白なし" border="false":::

> [!NOTE]
> モバイル クライアントで表示されるタブに余白が含まれるので、この機能はモバイル クライアントには適用されません。 

## <a name="timelines"></a>タイムライン

* 2021 年 3 月 5 日 - パブリック Developer Preview で [余白が削除されました](~/resources/dev-preview/developer-preview-intro.md)。
* 2021 年 7 月 31 日 - 実稼働環境で余白が削除されます。

## <a name="guidelines"></a>ガイドライン

Microsoft Teamsを使用するアプリは、この変更の影響を受ける可能性があります。 開発者は、タブ [の](~/resources/dev-preview/developer-preview-intro.md) 影響をDeveloper Previewし、必要な変更を行う場合は、[パブリック] に切り替える必要があります。

タブ開発者は、タブの周囲に余白Teamsを提供する必要があります。 開発者は、必要なタブ デザインの周囲に余白を追加する必要があります。 実稼働環境のアプリデザインは、追加のパディング、つまり、タブによって提供される余白Teams余白のように見えます。ただし、余分なパディングは一時的なだけであり、数週間で離れ、アプリが提供するパディングのみを残します。

## <a name="faq"></a>よくあるご質問 (FAQ)

**ヘッダー バーやタスク バーなどのアプリクロムがデザインの端に触れても問題ないか。**

はい、これは問題ありません。推奨されます。 これは、アプリがネイティブと感じるのに役立ちます。

**テキスト、ロゴ、画像などのアプリ コンテンツがデザインの左右の端に触れても問題ないか。**

いいえ、UI の端に触れ込むのを確認するには、すべてのアプリ コンテンツの左右に独自のパディングまたは余白を指定する必要があります。 必要に応じて、タブの上部に余白を追加することもできます。

**以前に適用した余白のTeamsは何ですか?**

* 左右: 20px
* Top: 16px
* 下: 0px

> [!IMPORTANT]
> * すべてのタブには、個人用タブ、(グループ) チャット タブ、会議タブ、チャネル タブなど、余白が削除されています。
> * この変更をオプトインまたはオプトアウトする方法はありません。 すべてのタブに適用されます。
> * この変更は、UI を囲む余白Microsoft Teamsに依存するタブに影響を与える可能性があります。

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
