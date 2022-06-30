---
title: 管理同意を構成する
description: 管理同意の構成について説明します
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams 認証タブ Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: 4d072bba0e4900aecec63e06cb63f4ac2311d91a
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66557751"
---
# <a name="configure-admin-consent"></a>管理者の同意を構成する

公開された API のアプリ スコープを定義し、ユーザーがユーザーの同意が有効になっているディレクトリでこのスコープに同意できるかどうかを判断できます。 管理者のみが、より高い特権を持つアクセス許可に対する同意を提供できます。

## <a name="to-expose-an-api"></a>API を公開するには

1. 左側のウィンドウで [**API の公開** の **管理** > ] を選択します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-api-menu.png" alt-text="API メニュー オプションを公開します。":::

    [ **API の公開]** ページが表示されます。

1. [ **設定]** を選択して、アプリ ID URI を生成します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-an-api.png" alt-text="アプリ ID URI を設定する":::

    アプリ ID URI を設定するためのセクションが表示されます。

1. アプリ ID URI を入力し、[保存] を選択 **します**。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/set-app-id-uri.png" alt-text="アプリ ID URI":::

    アプリ ID URI が更新されたことを示すメッセージがブラウザーに表示されます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-msg.png" alt-text="アプリ ID URI メッセージ":::

    アプリ ID URI がページに表示されます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-added.png" alt-text="アプリ ID URI が更新されました":::

## <a name="to-configure-api-scope"></a>API スコープを構成するには

1. **[この API で定義された** スコープ] セクションで [+ スコープの **追加]** を選択します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-scope.png" alt-text="スコープを選択する":::

    [ **スコープの追加]** ページが表示されます。

1. アプリ スコープのアプリの詳細を入力します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-scope.png" alt-text="スコープの詳細を追加する":::

    1. スコープ名を入力します。 これは必須フィールドです。
    1. **管理者とユーザー** を選択して、ユーザーのログイン資格情報を使用することに同意できるユーザーを構成します。 既定のオプションは **管理者のみです**。
    1. **管理同意表示名** を入力します。 これは必須フィールドです。
    1. 管理者の同意の説明を入力します。 これは必須フィールドです。
    1. **[ユーザーの同意] 表示名** を入力します。
    1. ユーザー同意の説明の説明を入力します。
    1. 状態の **[有効]** オプションを選択します。
    1. **[スコープの追加]** を選択します。

    スコープが追加されたことを示すメッセージがブラウザーに表示されます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added-msg.png" alt-text="スコープが追加されたメッセージ":::

    アプリ ID URI がページに表示されます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added.png" alt-text="追加および表示されるスコープ":::

## <a name="to-configure-authorized-client-application"></a>承認されたクライアント アプリケーションを構成するには

1. **[Api の公開**] ページを **[承認済みクライアント アプリケーション**] セクションに移動し、[**+ クライアント アプリケーションの追加]** を選択します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/auth-client-apps.png" alt-text="承認されたクライアント アプリケーション":::

    [ **クライアント アプリケーションの追加]** ページが表示されます。

1. クライアント アプリケーションを追加するための詳細を入力します。 このセクションでは、2 つのクライアント アプリケーションを追加します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-app.png" alt-text="クライアント アプリケーションを追加する":::

    1. Teams モバイルまたはデスクトップ アプリケーションのクライアント ID として **、「1fec8e78-bce4-4aaf-ab1b-5451cc387264** 」と入力します。
    1. **承認されたスコープ** のアプリ用に作成したアプリ ID を選択します。
    1. **[アプリケーションの追加]** を選択します。

    クライアント アプリが追加されたことを示すメッセージがブラウザーに表示されます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="クライアント アプリケーションがメッセージを追加しました":::

    クライアント アプリ ID がページに表示されます。

1. 前の手順を繰り返して、Teams Web アプリケーション用のクライアント アプリを追加します。

    1. Web アプリのクライアント ID として **「5e3ce6c0-2b1f-4285-8d4b-75ee78787346** 」と入力します。
    1. **承認されたスコープ** のアプリ用に作成したアプリ ID を選択します。
    1. **[アプリケーションの追加]** を選択します。

    クライアント アプリが追加されたことを示すメッセージがブラウザーに表示されます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="クライアント アプリケーションが Web アプリのメッセージを追加しました":::

    クライアント アプリ ID がページに表示されます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-app-added.png" alt-text="クライアント アプリの追加と表示":::
