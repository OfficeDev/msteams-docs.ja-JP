---
title: タブ余白の変更
author: surbhigupta
description: UI キットを使用して Microsoft Teams のタブの余白を削除する方法について説明します。 余分なパディング効果、左、右、上、および下の余白のサイズを把握します。
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: ba203cd89904acde77e1d9971175afc19c47d24d
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820074"
---
# <a name="tab-margin-changes"></a>タブ余白の変更

このドキュメントでは、Microsoft Teams のすべてのタブの余白を削除すると、アプリのビルドエクスペリエンスが向上する方法について説明します。 これは、2021 年に Teams で導入された機能強化です。
すべてのタブの周りの余白を削除することで、Teams のネイティブに見えるアプリを構築できます。 余白が削除されたタブは、Microsoft Teams の [UI キットデザイン](~/tabs/design/tabs.md)と一致します。 ほとんどのアプリでは、余白のない外観が強化されています。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="タブの表示と余白なし":::

> [!NOTE]
> モバイル クライアントで表示されるタブには余白がないため、この機能はモバイル クライアントには適用されません。

## <a name="guidelines"></a>ガイドライン

タブ余白の削除は、タブを使用する Teams アプリに影響します。 このような場合は、必要なタブ デザインの周囲に余白を追加できます。 運用環境のアプリデザインには、余分なパディング効果があります。つまり、Teams によって提供される余白とタブによって提供される余白です。ただし、余分なパディングは一時的なもので、数週間で消え、アプリの指定されたパディングのみが残ります。

## <a name="faq"></a>よく寄せられる質問

**ヘッダー バーやタスク バーなどのアプリクロムがデザインの端に触れても問題ありませんか?**

はい。これは問題なく、Teams ではこのような設計が推奨されます。 これは、アプリがネイティブと感じるのに役立ちます。

**テキスト、ロゴ、画像などのアプリ コンテンツがデザインの左右の端に触れても問題ありませんか?**

いいえ。UI の端に触れないように、すべてのアプリ コンテンツの左右に独自のパディングまたは余白を指定する必要があります。 必要に応じて、タブの上部に余白を追加することもできます。

**Teams が以前に適用したタブ余白のサイズは何ですか?**

* 左右: 20 ピクセル
* 上: 16 ピクセル
* 下: 0 ピクセル

> [!IMPORTANT]
>
> * 個人用タブ、(グループ) チャット タブ、会議タブ、チャネル タブなど、すべてのタブの余白が削除されています。
> * タブ余白の削除の変更は、すべてのタブに適用されます。 変更をオプトインまたはオプトアウトする方法はありません。
> * タブ余白の変更は、Microsoft Teams に依存して UI を囲む余白を提供するタブに影響する可能性があります。

## <a name="see-also"></a>関連項目

* [Teams の [ビルド] タブ](../tabs/what-are-tabs.md)
* [プライベート タブを作成する](../tabs/how-to/create-personal-tab.md)
* [チャネル タブまたはグループ タブを作成する](../tabs/how-to/create-channel-group-tab.md)
