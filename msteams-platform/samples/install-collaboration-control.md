---
title: コラボレーション コントロールのインストール
author: surbhigupta
description: このモジュールでは、Power アプリとMicrosoft 365 E3を使用してコラボレーション コントロールをインストールする方法と、コラボレーション コントロール ソリューションをインストールする方法について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 5a253c9e7373a2df9e1161e6d3fc9d9b1c8ccdaa
ms.sourcegitcommit: f2ac771cbd608e872604e9ac8ffec2d08f55ee1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2022
ms.locfileid: "68373032"
---
# <a name="install-collaboration-controls"></a>コラボレーション コントロールのインストール

> [!NOTE]
> 現在、コラボレーション コントロールは [パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

この記事では、コラボレーション コントロールをインストールする方法について説明します。 コラボレーション コントロールを使用してCollaboration Manager アプリケーションをビルドおよびデプロイするには、次のものが必要です。

* **Power Apps**: コラボレーション コントロールを使用してモデル 駆動型アプリケーションをビルドして実行します。
* **M365 E3 以降**: カスタム アプリケーションを Microsoft Teams に展開し、Planner にタスクを格納し、SharePoint のファイル、Outlook の会議を保存します。

Power Platform 環境にコンポーネントをインストールするには、次のロールが必要です。

* システム カスタマイザー
* 環境メーカー

ロール特権の詳細については、「[環境でのユーザー セキュリティの構成」を](/power-platform/admin/database-security#predefined-security-roles)参照してください。

## <a name="install-the-collaboration-controls-solutions"></a>コラボレーション コントロール ソリューションをインストールする

コラボレーション コントロールは、[Microsoft AppSource](https://appsource.microsoft.com/en-us/product/dynamics-365/mscm.collaboration-toolkit-preview?flightCodes=collaborationcontrols&signInModalType=2&ctaType=1) を使用して dataverse 環境にインストールします。

独自のモデル駆動型アプリ内でコンポーネントを構成して使用できるのは、 [Microsoft AppSource](https://appsource.microsoft.com/en-us/product/dynamics-365/mscm.collaboration-toolkit-preview?flightCodes=collaborationcontrols&signInModalType=2&ctaType=1)  を参照し、Dataverse 環境にコラボレーション コントロールをインストールした後だけです。

コラボレーション コントロールには、次のソリューションが含まれます。

|**設定のソリューション** | **用途** |
|---|---|
| コラボレーション コントロールの設定 | コラボレーション コントロールを強化する設定インフラストラクチャを保持する |
| コラボレーション コントロールの設定オブジェクト | コラボレーション コントロールで使用される定義済みの設定値を提供します。|

|**コラボレーション ソリューション** | **用途** |
|---|---|
| コラボレーション コントロールタスク  | タスク PCF (Power Apps コンポーネント フレームワーク) コントロールが含まれています。 |
| コラボレーション コントロール イベント | Outlook と Teams の会議と予約の予定のイベント PCF コントロールが含まれています。 |
| コラボレーション コントロールノート | Dataverse にノートを格納するノート PCF コントロールが含まれます。 |
| コラボレーション コントロール ファイル | SharePoint 上のファイルにアクセスするための Files PCF コントロールが含まれています。 |
| コラボレーション コントロールのコア |カスタム コラボレーション API、イベント、ファイル、タスク コントロール用のコラボレーション データ モデルと仮想テーブルが含まれます。 |
| コラボレーション コントロールの承認 | 新しい承認 PCF コントロールが含まれています。 |
| コラボレーション コントロール コネクタ | 新しいコラボレーション Power Automate コネクタが含まれています |

> [!NOTE]
> 環境にインストールされているコントロールの既存のバージョンがある場合は、新しい環境を作成し、新しいインストールを完了して、最新バージョンに正常にアップグレードすることが必要になる場合があります。

インストールする前に、Power Platform 環境または管理者テナントである必要があります。 データベースを含むデータバース環境が必要です。 お持ちでない場合は、インストールを続行するために [新しい](/power-platform/admin/create-environment) ファイルを作成する必要があります。

ソリューションをインストールするには、 [Microsoft AppSource に](https://appsource.microsoft.com/en-us/product/dynamics-365/mscm.collaboration-toolkit-preview?flightCodes=collaborationcontrols&signInModalType=2&ctaType=1) 移動し、次の手順を実行します。

1. [ **今すぐ取得] ボタンを** 選択します。

   :::image type="content" source="../assets/images/collaboration-control/preview-form.png" alt-text="コラボレーション コントロールを表示するための [Get it now]\(今すぐ取得\) ボタンのスクリーンショット。"border="true":::

1. アカウントでサインインし、フォームに入力して **[続行**] を選択します。

   :::image type="content" source="../assets/images/collaboration-control/overview.png" alt-text="コラボレーション コントロールの概要のスクリーンショット。" border="true":::

   :::image type="content" source="../assets/images/collaboration-control/collaboration-controls-preview.png" alt-text="コラボレーション コントロールのインストール プレビューのスクリーンショット。" border="true":::

1. Power Platform 管理 センターに移動します。 ドロップダウン メニューから環境を選択し、使用条件とポリシーステートメントに同意します。

   > [!TIP]
   > 環境を選択したときにアクセス許可エラーが表示される場合は、環境のドロップダウン メニューの外側を選択して、問題が解決するかどうかを確認してください。

   :::image type="content" source="../assets/images/collaboration-control/install-environment.png" alt-text="インストール コラボレーション制御環境の例を示すスクリーンショット。" border="true":::

1. [ **インストール**] を選択すると、インストールが完了するまでに約 15 分かかる場合があります。

1. Power Apps プレビューに[https://make.powerapps.com/](https://make.powerapps.com/)[https://make.preview.powerapps.com/](https://make.preview.powerapps.com/)サインアップしている場合は、移動もサポートされます。

1. 環境を表示し、必要に応じて Power Apps ポータルの右上で変更できるため、コントロールがインストールされている環境に入っていることを確認します。

1. [ **ソリューション** ] タブを選択して、適切な環境にインストールしたすべてのソリューションを表示します。

   :::image type="content" source="../assets/images/collaboration-control/solutions.png" alt-text="すべてのソリューション コラボレーション コントロールを表示する [ソリューション] タブを示すスクリーンショット。" border= "true":::

> [!NOTE]
> コラボレーション コントロールはプレビューであり、要素は時間の経過と共に変化し、破壊的変更の可能性があります。 コラボレーション コントロールは、運用環境ではサポートされていません。

すべてのコラボレーション ソリューションを環境に正常にインストールすると、コラボレーション制御機能を利用できる新しいモデル駆動型アプリを構築できます。
