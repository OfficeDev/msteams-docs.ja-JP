---
title: アプリ ユーザーの認証
description: シングル サインオン (SSO) やサード パーティの OAuth プロバイダーの使用など、Teams アプリで有効にできる認証方法について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: b7ab4f007c0b7f9400e63d1654c5e0a930274468
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2022
ms.locfileid: "67587009"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Microsoft Teams でユーザーを認証する

認証はすべて、アプリ ユーザーを検証し、アプリとアプリのユーザーを不当なアクセスから保護することです。 アプリに適した認証方法を使用して、Teams アプリを使用たいアプリ ユーザーを検証できます。

次の 2 つの方法のいずれかで、アプリの認証を追加することを選択します。

- **Teams アプリでシングル サインオン (SSO) を有効にする: Teams** 内の SSO は、アプリ ユーザーの Teams ID を使用してアプリへのアクセスを提供する認証方法です。 Teams にログインしているユーザーは、Teams 環境内でアプリに再度ログインする必要はありません。 アプリ ユーザーからの同意のみが必要な場合、Teams アプリは Azure Active Directory (AD) からそれらのアクセスの詳細を取得します。 アプリ ユーザーが同意した後は、再検証しなくても、他のデバイスからでもアプリにアクセスできます。

- **サード パーティの OAuth プロバイダーを使用して認証を有効にする**: サード パーティの OAuth ID プロバイダー (IdP) を使用して、アプリ ユーザーを認証できます。 アプリ ユーザーは ID プロバイダーに登録されます。ID プロバイダーには、アプリとの信頼関係があります。 ユーザーがログインしようとすると、ID プロバイダーはアプリ ユーザーを検証し、アプリへのアクセスを提供します。 Azure AD は、このようなサード パーティの OAuth プロバイダーの 1 つです。 Google、Facebook、GitHub、その他のプロバイダーなど、他のプロバイダーを使用できます。

## <a name="select-authentication-method"></a>認証方法を選択する

タブ アプリ、ボット アプリ、メッセージング拡張機能アプリで、SSO またはサード パーティの OAuth IDP を使用して認証を有効にします。 アプリで認証を追加するには、次の 2 つの方法のいずれかを選択します。

:::row:::
    :::column span="1":::
        SSO
    :::column-end:::
    :::column span="1":::
        &nbsp;
    :::column-end:::
    :::column span="1":::
        OAuth
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-sso-icon.png" alt-text="タブ アプリの SSO" link="../../tabs/how-to/authentication/tab-sso-overview.md":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  **タブ アプリ**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-app-idp.png" alt-text="タブ アプリ用のサード パーティの OAuth プロバイダーを使用した認証。" link="../../tabs/how-to/authentication/auth-tab-aad.md":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-sso-icon.png" alt-text="ボット アプリの SSO" link="../../bots/how-to/authentication/auth-aad-sso-bots.md":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;**ボット アプリ**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-app-idp.png" alt-text="ボット アプリ用のサード パーティ OAuth プロバイダーを使用した認証。" link="../../bots/how-to/authentication/add-authentication.md":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-sso-icon.png" alt-text="メッセージング拡張機能アプリの SSO" link="../../messaging-extensions/how-to/enable-SSO-auth-me.md":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; **メッセージ拡張機能アプリ**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-app-idp.png" alt-text="メッセージング拡張機能アプリ用のサード パーティの oAuth IdP を使用した認証。" link="../../messaging-extensions/how-to/add-authentication.md":::
    :::column-end:::
:::row-end:::

> [!NOTE]
> サイレント認証ページは、リソース モジュールに移動されます。 詳細については、「 [サイレント認証](../../tabs/how-to/authentication/auth-silent-aad.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [タブ アプリでシングル サインオンを有効にする](../../tabs/how-to/authentication/tab-sso-overview.md)
- [タブの Microsoft Teams 認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)
- [ボットのシングル サインオンのサポート](~/bots/how-to/authentication/auth-aad-sso-bots.md)
- [メッセージ拡張機能に認証を追加する](~/messaging-extensions/how-to/add-authentication.md)
