---
title: タブの要件について
author: laujan
description: これらの要件にMicrosoft Teamsする必要があります。
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a46a80401b29b5436807c9a5b94580beca3786f0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566664"
---
# <a name="tab-requirements"></a>タブの要件

Teamsタブは、次の要件に従う必要があります。

* X-Frame-Options または Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame で提供する必要があります。
  * ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 11 Internet Explorerの場合は、同様に `X-Content-Security-Policy` 設定します。
  * または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。 このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き尊重されています。
* 通常、クリック ジャッキに対するセーフガードとして、ログイン ページは iFrames でレンダリングされません。 したがって、認証ロジックではリダイレクト以外のメソッドを使用する必要があります。 たとえば、トークンベースまたは Cookie ベースの認証を使用します。

> [!NOTE]
> Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 詳細については [、「SameSite cookie 属性 (2020 update)」を参照してください](../../resources/samesite-cookie-update.md)。

* ブラウザーは、Web ページが Web ページにサービスを提供したドメインとは異なるドメインに対して要求を行うのを防ぐ同一発生元ポリシーの制限に従います。 ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトする必要がある場合があります。 クロスドメイン ナビゲーション ロジックを使用すると、Teams クライアントは、タブの読み込みまたは通信時に、アプリ マニフェストの静的な validDomains リストに対して原点を検証できます。

* シームレスなエクスペリエンスを作成するには、クライアントのテーマ、デザイン、および意図に基Teamsタブのスタイルを設定する必要があります。 通常、タブは、特定の必要性に対処し、小さな一連のタスクまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。

* コンテンツ ページ内で、スクリプト タグを使用Microsoft Teams [JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。 ページの読み込み後に、 を呼び出します `microsoftTeams.initialize()` 。 ページを表示しない場合は、ページは表示されません。

* モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。

* モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [カスタム 個人用タブを作成するには、Node.js と Yeoman Generator を使用Microsoft Teams](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)