---
title: 前提条件
author: surbhigupta
description: これらの要件にMicrosoft Teamsする必要があります。
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8566bb0457db76e4639593dcd67a0442749c0a31
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179938"
---
# <a name="prerequisites"></a>前提条件

Teamsは、次の前提条件に従う必要があります。

* X-Frame-Options と Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame に表示する必要があります。
  * ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 11 Internet Explorer互換性の場合は、 を設定します `X-Content-Security-Policy` 。
  * または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。 このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き受け入れ可能です。

* 通常、クリックジャックに対する保護手段として、ログイン ページは iFrames では表示されません。 認証ロジックでは、リダイレクト以外のメソッドを使用する必要があります。 たとえば、トークンベースまたは Cookie ベースの認証を使用します。

    > [!NOTE]
    > Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザー動作に依存するのではなく、Cookie の使用目的を設定することを推奨します。 詳細については [、「SameSite cookie 属性」を参照してください](../../resources/samesite-cookie-update.md)。

* ブラウザーは、同じオリジン ポリシーの制限に従います。 Web ページが、提供された Web ページとは異なるドメインに対して要求を行うのを防ぐ。 ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトできます。 クロスドメイン ナビゲーション ロジックを使用すると、Teams クライアントは、タブの読み込みまたは通信時にアプリ マニフェストの静的リストに対して原点を `validDomains` 検証できる必要があります。

* クライアントのテーマ、デザイン、および意図Teamsに基づいてタブのスタイルを設定する必要があります。 通常、タブは、特定の必要性に対処し、小さなタスクセットまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。

* コンテンツ ページ内で、スクリプト タグを使用Microsoft Teams [JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。 ページの読み込み後に、呼び出し `microsoftTeams.initialize()` を行います。それ以外の場合、ページは表示されません。

* モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。

* モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。

* [MS Teams] タブでは、自己署名証明書を使用するイントラネット Web サイトを読み込む機能はサポートされていません。

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
