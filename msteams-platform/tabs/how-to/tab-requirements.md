---
title: タブの要件
author: surbhigupta
description: これらの要件にMicrosoft Teamsする必要があります。
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a5d4b1a1c9b79d45d323acab7bfba2ba7ac2958d
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069211"
---
# <a name="tab-requirements"></a>タブの要件

Teamsタブは、次の要件に従う必要があります。

* X-Frame-Options および Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame で提供する必要があります。
  * ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 11 Internet Explorer互換性の場合は、 を設定します `X-Content-Security-Policy` 。
  * または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。 このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き受け入れ可能です。
* 通常、クリック ジャッキに対するセーフガードとして、ログイン ページは iFrames でレンダリングされません。 認証ロジックでは、リダイレクト以外のメソッドを使用する必要があります。 たとえば、トークンベースまたは Cookie ベースの認証を使用します。

    > [!NOTE]
    > Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザー動作に依存するのではなく、Cookie の使用目的を設定することを推奨します。 詳細については [、「SameSite cookie attribute 2020 update」を参照してください](../../resources/samesite-cookie-update.md)。

* ブラウザーは、Web ページが Web ページにサービスを提供したドメインとは異なるドメインに対して要求を行うのを防ぐ同一発生元ポリシーの制限に従います。 ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトできます。 クロスドメイン ナビゲーション ロジックでは、Teams クライアントがタブの読み込みまたは通信時にアプリ マニフェストの静的な validDomains リストに対して原点を検証できる必要があります。

* シームレスなエクスペリエンスを作成するには、クライアントのテーマ、デザイン、および意図に基づいてTeamsスタイルを設定する必要があります。 通常、タブは、特定の必要性に対処し、小さなタスクセットまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。

* コンテンツ ページ内で、スクリプト タグを使用Microsoft Teams [JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。 ページの読み込み後に、呼び出し `microsoftTeams.initialize()` を行います。それ以外の場合、ページは表示されません。

* モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。

* モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。

* [MS Teams] タブでは、自己署名証明書を使用するイントラネット Web サイトを読み込む機能はサポートされていません。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [カスタム 個人用タブを作成するには、Node.js と Yeoman Generator を使用Microsoft Teams](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)
