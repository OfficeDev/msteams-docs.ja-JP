---
title: タブの要件について
author: laujan
description: Microsoft Teamsのすべてのタブは、これらの要件に準拠している必要があります。
keywords: チーム タブ グループ チャネルの構成可能
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

Teamsタブは、次の要件に準拠している必要があります。

* タブページを、X フレーム オプションまたはコンテンツ セキュリティ ポリシー HTTP 応答ヘッダーを介して iFrame で提供できるようにする必要があります。
  * ヘッダーを設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Internet Explorer 11 の互換性のためにも設定 `X-Content-Security-Policy` します。
  * または、ヘッダを設定 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` します。 このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き使用されます。
* 通常、クリックジャッキングに対する保護手段として、ログインページはiFrameでレンダリングされません。 したがって、認証ロジックでは、リダイレクト以外のメソッドを使用する必要があります。 たとえば、トークンベースまたはクッキーベースの認証を使用します。

> [!NOTE]
> Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 詳細については、 [SameSite クッキー属性 (2020 更新)](../../resources/samesite-cookie-update.md)を参照してください。

* ブラウザは、Web ページが Web ページを提供したドメインとは異なるドメインに対して要求を行うことを防ぐ、同一生成元ポリシーの制限に従います。 ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトする必要がある場合があります。 クロスドメイン ナビゲーション ロジックでは、Teams クライアントが、タブの読み込み時またはタブとの通信時に、アプリ マニフェストの静的な validDomains リストに対して元のドメインを検証できるようにする必要があります。

* シームレスなエクスペリエンスを作成するには、Teamsクライアントのテーマ、デザイン、および意図に基づいてタブのスタイルを設定する必要があります。 通常、タブは、特定のニーズに対応し、タブのチャネルの場所に関連する一連のタスクまたはデータのサブセットに焦点を当てるために作成されている場合に最適です。

* コンテンツ ページ内で、スクリプト タグを使用して[、Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。 ページの読み込みに続いて、 に電話をかけることができます `microsoftTeams.initialize()` 。 表示しない場合は、ページは表示されません。

* モバイル クライアントで認証を実行するには、JavaScript SDK Teams少なくともバージョン 1.4.1 にアップグレードする必要があります。

* モバイル クライアントにチャンネルタブまたはグループ タブを表示Teams選択した場合、 `setSettings()` 設定にはプロパティの値が必要 `websiteUrl` です。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Node.jsとヨーマンジェネレータを使用してカスタムパーソナルタブを作成Microsoft Teams](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)