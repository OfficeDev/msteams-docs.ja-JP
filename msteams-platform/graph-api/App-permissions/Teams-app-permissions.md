---
title: Teams アプリのアクセス許可を管理する
author: surbhigupta
description: このモジュールでは、機能に基づいて Teams アプリをさまざまな場所で管理する方法について説明します。
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 2bc501444e52f31061312c325ddf7dd80370240a
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791845"
---
# <a name="permissions-in-teams-app"></a>Teams アプリのアクセス許可

Teams アプリのアクセス許可は、アプリの機能に応じて 2 か所で管理されます。

* [リソース固有の同意 (RSC)](#resource-specific-consent)
* [Azure Active Directory (Azure AD)](#azure-active-directory)

:::image type="content" source="../../assets/images/teams-app-permissions.png" alt-text="スクリーンショットでは、さまざまな Teams アプリのアクセス許可について説明しています。":::

## <a name="resource-specific-consent"></a>リソース固有の同意

RSC は Microsoft Teams と Microsoft Graph API統合であり、アプリで API エンドポイントを使用して、組織内の特定のリソース (チームまたはチャット) を管理できます。 詳細については、「 [Teams でリソース固有の同意を有効にする](../rsc/resource-specific-consent.md)」を参照してください。

RSC アクセス許可は、Teams クライアントにインストールされている Teams アプリでのみ使用でき、現在は Azure AD ポータルの一部ではなく、Teams アプリ マニフェスト (JSON) ファイルで宣言されています。

## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD は、クラウドベースの ID およびアクセス管理サービスです。 このサービスは、従業員が Microsoft 365、Azure portal、その他の何千もの SaaS アプリケーションなどの外部リソースにアクセスするのに役立ちます。 詳細については、「[Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis)」を参照してください。

### <a name="microsoft-graph-api-permission"></a>Microsoft Graph API アクセス許可

Graph APIアクセス許可は Azure AD で管理されます。 アプリから Microsoft Graph のデータにアクセスする場合、ユーザーまたは管理者は、同意のプロセスを通してそのアプリに正しいアクセス許可を付与する必要があります。 詳細については、「[Microsoft Graph のアクセス許可](/graph/permissions-reference)」を参照してください。

## <a name="capability-wise-management"></a>機能の賢明な管理

### <a name="bot-and-messaging-extension"></a>ボットとメッセージング拡張機能

ボットまたはメッセージング拡張機能 ID は、次の登録プラットフォームに基づいて生成されます。 この ID は、ボットまたはメッセージング拡張機能を Teams アプリに追加するために必要です。

* Azure AD ポータル
* 開発者ポータルまたは Bot Framework ポータル

#### <a name="azure-ad-portal"></a>Azure AD ポータル

ボットまたはメッセージング拡張機能が Azure AD ポータルに登録されると、Azure AD アプリ ID が関連付けられます。この ID は **、Azure AD** portal > **アプリ登録** にあります。 エンドポイントとその他のボット構成は、Azure portalで管理されます。

#### <a name="developer-or-bot-framework-portal"></a>開発者ポータルまたは Bot Framework ポータル

ボットまたはメッセージング拡張機能が開発者ポータルまたは Bot Framework ポータルに登録されている場合、Azure AD アプリ ID は含まれません。 ただし、ボットまたはメッセージング拡張機能 ID は、Bot Framework ポータルで確認できます。 エンドポイントとその他のボット構成は、Bot Framework ポータルで管理されます。

ボットの他の Teams 固有の構成は、アプリの [開発者ポータル] セクションで管理できます。

### <a name="connectors"></a>コネクタ

コネクタにはコネクタ ID があり、コネクタ開発者ダッシュボードを通じて登録および管理されます。 この ID は、Teams アプリにコネクタを導入するために必要です。 コネクタの他の Teams 固有の構成は、アプリの開発者ポータル セクションで管理できます。
