---
title: クライアント シークレットを作成する
description: クライアント シークレットの作成について説明します
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams 認証タブ Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: 77d1c4e43c9bdfb9d2cb9e3e97ee3a26b8b0fa01
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558850"
---
# <a name="create-client-secret"></a>クライアント シークレットを作成する

クライアント シークレットは、トークンを要求するときにアプリケーションが ID を証明するために使用する文字列です。

1. [**証明書&シークレットの****管理** > ] を選択します。

2. **[+ 新しいクライアント シークレット**] を選択します。

    :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="クライアント シークレット ページ":::

   [ **クライアント シークレットの追加]** ページが表示されます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-secret.png" alt-text="クライアント シークレット ページを追加する":::

3. 説明を入力します。
4. シークレットの有効期間を選択します。
5. [**追加**] を選択します。

   クライアント シークレットが更新されたことを示すメッセージがブラウザーに表示され、クライアント シークレットがページに表示されます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-secret-added.png" alt-text="追加されたクライアント シークレット":::

6. クライアント シークレットの **値** の横にあるコピー ボタンを選択します。
7. 後で使用するためにコピーした値を保存します。

   > [!NOTE]
   > クライアント シークレットの作成直後に、必ず値をコピーしてください。 この値は、クライアント シークレットが作成された時点でのみ表示され、その後は表示できません。
