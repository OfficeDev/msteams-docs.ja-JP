---
title: タブの要件について
author: laujan
description: Microsoft Teams のすべてのタブは、これらの要件に従う必要があります。
keywords: teams タブ グループ チャネルを構成可能
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1f5a3eaa8ca16878944288d5dbbfa78cfe9fa3ce
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797943"
---
# <a name="tab-requirements"></a>タブの要件

Teams のタブは、次の要件に従う必要があります。

* X-Frame-Options や Content-Security-Policy HTTP 応答ヘッダーを介して、タブ ページを iFrame で提供する必要があります。
  * ヘッダーを設定します。 `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 11 Internet Explorerについては、同様に `X-Content-Security-Policy` 設定します。
  * または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。 このヘッダーは廃止されましたが、ほとんどのブラウザーで引き続き使用されています。
* 通常、クリックジャッキーに対する保護策として、ログイン ページは iFrame では表示されません。 したがって、認証ロジックではリダイレクト以外の方法を使用する必要があります (トークン ベースの認証や Cookie ベースの認証を使用する場合など)。

> [!NOTE]
> Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 「[SameSite Cookie 属性 (2020 更新プログラム)](../../resources/samesite-cookie-update.md)」を *参照してください*。

* ブラウザーは、Web ページにサービスを提供したドメインとは異なるドメインに対して Web ページが要求を行うのを防ぐため、同一発生元ポリシーの制限に従います。 ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトする必要がある場合があります。 クロスドメイン ナビゲーション ロジックでは、Teams クライアントがタブを読み込むまたはタブと通信するときに、アプリ マニフェストの静的 validDomains リストに対して原点を検証できる必要があります。

* シームレスなエクスペリエンスを作成するには、Teams クライアントのテーマ、デザイン、および意図に基づいてタブのスタイルを設定する必要があります。 通常、タブは、特定の必要性に対処し、小さなタスクセットまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てながら構築されている場合に最適に動作します。

* コンテンツ ページ内で、スクリプト タグを使用 [して Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) への参照を追加します。 ページの読み込み後、呼び出しを行います `microsoftTeams.initialize()` 。 表示しない場合、ページは表示されません。
