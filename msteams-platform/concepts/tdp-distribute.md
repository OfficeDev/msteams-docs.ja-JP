---
title: アプリの配布
description: 開発者ポータルを使用してアプリを配布する方法についてMicrosoft Teams。
keywords: 開発者ポータル チームの開始
localization_priority: Normal
ms.topic: Conceptual
ms.openlocfilehash: d1d098b295492a7dc3b691db4625307b6c3170ce
ms.sourcegitcommit: 25539046d408c4270b988fd826d7cf1275f4b9dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2021
ms.locfileid: "52763141"
---
# <a name="distribute-your-apps"></a>アプリの配布

## <a name="distribute"></a>均等割り付け

アプリケーションの定義が完了したら、[配布] セクションを使用してアプリの定義を zip ファイルとしてエクスポートし、テスト用に Teams クライアントに共有およびアップロードできます。 [Export] (エクスポート) をクリックすると、zip ファイルが **appname.zip** として既定のダウンロード ディレクトリにダウンロードされます。

:::image type="content" source="~/assets/images/tdp/tdp_distribute_1.png" alt-text="開発者ポータルの [配布] ページをTeamsスクリーンショット。":::

### <a name="manifest"></a>マニフェスト

マニフェストは、アプリの機能、必要なリソース、その他の重要な属性など、アプリの構成方法について説明します。 詳細 [については、「マニフェスト スキーマ](~/resources/schema/manifest-schema.md) 」を参照してください。

### <a name="flights"></a>フライト

アプリの更新プログラムを取得するユーザーを制御します。 たとえば、Microsoft の従業員に更新プログラムをリリースして、バグを特定して修正してから一般公開することができます。 [新 **しい要求の作成] を** 選択して、新しいフライト要求を作成します。

### <a name="publish-to-org"></a>組織に発行する

組織のユーザーがアプリを利用できます。IT 管理者によって承認されると、組織向けの [アプリ] Teams [>] の下にアプリが表示されます。

### <a name="publish-your-app-to-teams-store"></a>アプリをストアにTeamsする

プロジェクトのホーム ページでは、アプリをチーム向けにアップロードしたり、組織内のユーザー向けに会社のカスタム App Store に提出したり、すべての Teams ユーザー向けに App Source に提出したりできます。 これらの送信内容は、IT 管理者によって審査されます。 **[Publish]** (発行) ページに戻ると提出ステータスを確認することができ、アプリが IT 管理者によって承認または却下されたかどうかを確認できます。このページでは、アプリの更新プログラムを提出したり、現在提出中のアプリをキャンセルしたりすることもできます。

## <a name="see-also"></a>関連項目

* [開発者ポータルTeams概要](~/concepts/build-and-test/teams-developer-portal.md)
* [開発者ポータルTeams構成する](~/concepts/tdp-configuration.md)
* [開発者ポータルTeamsツール](~/concepts/tdp-tools.md)