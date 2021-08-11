---
title: タブ余白の変更
author: surbhigupta
description: タブ 余白を削除すると、アプリの作成エクスペリエンスが向上する方法について説明します。
keywords: タブの余白の余白の削除
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 4ca8356bddc0e578bc58b38112fb1268302a5ad0e84631bf81864c70cffbcb64
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57704387"
---
# <a name="tab-margin-changes"></a>タブ余白の変更

このドキュメントでは、アプリの構築エクスペリエンスを向上させる方法について説明Microsoft Teamsタブの余白を削除する方法について説明します。 これは、2021 年にMicrosoft Teams拡張機能です。
すべてのタブの余白を削除することで、Teamsネイティブに見えるアプリを作成できます。 余白が削除されたタブは、Microsoft Teams [UI キットのデザインと一致します](~/tabs/design/tabs.md)。 ほとんどのアプリでは、余白のない外観が強化されています。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="タブの wit と余白なし" border="false":::

> [!NOTE]
> モバイル クライアントで表示されるタブに余白が含まれるので、この機能はモバイル クライアントには適用されません。 

## <a name="guidelines"></a>ガイドライン

タブ余白の削除は、タブをTeamsアプリに影響します。 このような場合は、必要なタブ デザインの周囲に余白を追加できます。 実稼働環境のアプリデザインには、追加のパディング効果があります。つまり、タブによって提供される余白Teams余白が提供されます。ただし、余分なパディングは一時的なだけであり、数週間で消え、アプリが提供するパディングだけが残されます。

## <a name="faq"></a>よくあるご質問 (FAQ)

**ヘッダー バーやタスク バーなどのアプリクロムがデザインの端に触れても問題ないか。**

はい、これは問題ありませんが、Teamsを推奨します。 アプリがネイティブと感じるのに役立ちます。

**テキスト、ロゴ、画像などのアプリ コンテンツがデザインの左右の端に触れても問題ないか。**

いいえ、すべてのアプリ コンテンツの左右に独自のパディングまたは余白を指定して、UI の端に触れ去らなかっていないか確認する必要があります。 必要に応じて、タブの上部に余白を追加することもできます。

**以前に適用したタブ余白のTeamsは何ですか?**

* 左右: 20px
* Top: 16px
* 下: 0px

> [!IMPORTANT]
> * すべてのタブには、個人用タブ、(グループ) チャット タブ、会議タブ、チャネル タブなど、余白が削除されています。
> * タブ余白の削除の変更は、すべてのタブに適用されます。 変更をオプトインまたはオプトアウトする方法はありません。 
> * タブ 余白の変更は、UI を囲む余白Microsoft Teamsに依存するタブに影響を与える可能性があります。

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
