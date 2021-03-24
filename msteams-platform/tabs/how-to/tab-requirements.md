---
title: タブの要件について
author: laujan
description: Microsoft Teams のすべてのタブは、これらの要件に従う必要があります。
keywords: teams タブ グループ チャネル構成可能
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 087f894bd2a0a2c7a79e683f504e2c2f5a50c287
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034664"
---
# <a name="tab-requirements"></a>タブの要件

Teams タブは、次の要件に従う必要があります。

* X-Frame-Options または Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame で提供する必要があります。
  * ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 11 Internet Explorerの場合は、同様に `X-Content-Security-Policy` 設定します。
  * または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。 このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き尊重されています。
* 通常、クリック ジャッキに対するセーフガードとして、ログイン ページは iFrames でレンダリングされません。 したがって、認証ロジックでは、リダイレクト以外の方法を使用する必要があります (トークンベースまたは Cookie ベースの認証を使用するなど)。

> [!NOTE]
> Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 「[SameSite Cookie 属性 (2020 更新プログラム)](../../resources/samesite-cookie-update.md)」を *参照してください*。

* ブラウザーは、Web ページが Web ページにサービスを提供したドメインとは異なるドメインに対して要求を行うのを防ぐ同一発生元ポリシーの制限に従います。 ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトする必要がある場合があります。 クロスドメイン ナビゲーション ロジックを使用すると、Teams クライアントは、タブの読み込みまたは通信時に、アプリ マニフェストの静的な validDomains リストに対して原点を検証できます。

* シームレスなエクスペリエンスを作成するには、Teams クライアントのテーマ、デザイン、意図に基づいてタブのスタイルを設定する必要があります。 通常、タブは、特定の必要性に対処し、小さな一連のタスクまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。

* コンテンツ ページ内で、スクリプト タグを使用して [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) への参照を追加します。 ページの読み込み後に、 を呼び出します `microsoftTeams.initialize()` 。 ページを表示しない場合は、ページは表示されません。

* モバイル クライアントで認証を機能するには、Teams JavaScript SDK を少なくともバージョン 1.4.1 にアップグレードする必要があります。

* チャネルまたはグループ タブを Teams モバイル クライアントに表示する場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。