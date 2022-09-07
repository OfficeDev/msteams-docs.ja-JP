---
title: Teams Toolkit で開発者ポータルと統合する
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit で開発者ポータルと統合する方法について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: b54e833f5c8292c0b426e859e63d858102860a47
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617223"
---
# <a name="integrate-with-developer-portal"></a>開発者ポータルと統合する

Teams Toolkit 内の開発者ポータルでアプリを構成および管理できます。

## <a name="to-publish-app-using-developer-portal"></a>開発者ポータルを使用してアプリを発行するには

次の手順は、開発者ポータルでアプリを発行するのに役立ちます。

1. [展開] で **[Teams の開発者ポータル****] を選択します**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/dev-portal-ttk.png" alt-text="Teams の開発者ポータル":::

   これで、開発者ポータルがブラウザーで開きます。

1. 対応するアカウントを使用して [Teams の開発者ポータル](https://dev.teams.microsoft.com) にサインインします。
1. zip 形式でアプリ パッケージをインポートし、[**アプリのインポート****]** >  を選択します。
1. [**発行]** >  を **選択して組織に公開します**。

## <a name="to-update-manifest-file-and-app-package"></a>マニフェスト ファイルとアプリ パッケージを更新するには

Teams アプリのマニフェスト ファイルに関連する変更がある場合は、マニフェストを更新して、Teams アプリをもう一度発行できます。 Teams アプリを手動で発行するために、[Teams の開発者ポータル](https://dev.teams.microsoft.com/home)を使用できます。

1. 対応するアカウントを使用して [Teams の開発者ポータル](https://dev.teams.microsoft.com) にサインインします。
1. zip 形式でアプリ パッケージをインポートし、[**アプリのインポート****]** >  を選択します。<br>
   以前に開発者ポータルにアップロードしたアプリを置き換える必要があります。
1. アプリを発行するには、[**発行** > ] を **選択して組織に公開します**。

開発者ポータルでは、次の構成を実行できます。

* **基本的な情報**: このセクションでは、アプリ名、アプリ ID、説明、バージョン、開発者情報、アプリ URL、アプリケーション (クライアント) ID、Microsoft Partner Network ID を編集できます。
* **ブランド** 化: このページには、アプリ アイコンの詳細が表示されます。
* **アプリの機能**: 次の機能をアプリに追加できます。
  * 個人用アプリ
  * Bot
  * Connector
  * シーン
  * グループ アプリとチャネル アプリ
  * メッセージング拡張機能
  * 会議の拡張機能
  * アクティビティ フィード通知
* **アクセス許可**: このセクションでは、デバイスのアクセス許可、チームのアクセス許可、チャットまたは会議のアクセス許可、アプリのユーザーアクセス許可を付与できます。
* **シングル サインオン**: シングル サインオン (SSO) でユーザーを認証するようにアプリを構成できます。
* **言語**: アプリの言語を設定または変更できます。
* **ドメイン**: Teams クライアントにアプリを読み込むドメインを追加できます (例: *.example.com)。

## <a name="see-also"></a>関連項目

* [Teams の開発者ポータル](../concepts/build-and-test/teams-developer-portal.md)
* [開発者ポータルでアプリを管理する](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)
