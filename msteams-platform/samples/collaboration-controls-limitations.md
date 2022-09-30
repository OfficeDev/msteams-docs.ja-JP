---
title: コラボレーション コントロール アプリの制限事項と既知の問題
author: surbhigupta
description: このモジュールでは、Microsoft Teams のコラボレーション コントロール アプリの制限事項と既知の問題について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: fe403c566b47be6509ff0d11113c34a8fc667cc9
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243389"
---
# <a name="limitations-and-known-issues"></a>制限事項と既知の問題

> [!NOTE]
> 現在、コラボレーション コントロールは [パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

コラボレーション コントロールの制限事項を次に示します。

* Canvas アプリではコンポーネントを使用できません。
* コンポーネントでは、完全なタブ ビューのみがサポートされます。

     :::image type="content" source="../assets/images/collaboration-control/tasks-tab.png" alt-text="スクリーンショットはタスクを示しています。" border="true":::

* 選択したサブグリッド ビューは適用されません。 コラボレーション レコードのすべてのタスク、会議、またはメモが表示されます。

     :::image type="content" source="../assets/images/collaboration-control/subgrid-view.png" alt-text="スクリーンショットは、タスクのサブグリッド ビューを示しています。" border= "true":::

* タイムライン コントロールに追加されたアクティビティは、コンポーネントに作成されたコンポーネント、タスク、会議、メモには表示されません。タイムライン コントロールには含まれません。
* コンポーネントにアクセスする前に新しいレコードを保存する必要があります。それ以外の場合は空の画面が表示されます。
* コンポーネントは、追加するフォームまたはアプリからテーマを継承しません。
* ローカライズは、Microsoft Teams 内でアプリを実行する場合にのみ使用できます。
* Microsoft Edge strict モードはサポートされておらず、クロスサイト Cookie が必要です。

**管理 センターは、インストールまたはアップグレードが完了しても更新されません**

[コラボレーション コントロールのインストール](~/samples/install-collaboration-control.md)手順に従うと、Power Platform 管理センターにリダイレクトされます。 バナーはインストールの開始時に表示されますが、インストールが完了しても更新されません。 状態はインストール中に一覧表示され、完了すると一覧に表示されない可能性があります。 ソリューションの一覧 [https://make.powerapps.com/](https://make.preview.powerapps.com/) を表示して、インストールが完了したことを確認できます。

**インストール中の表示:** :::image type="content" source="../assets/images/collaboration-control/view-during-installation.png" alt-text="スクリーンショットは、インストール中のプロセスを示しています。" border="true":::

**インストール後の表示:** :::image type="content" source="../assets/images/collaboration-control/view-after-installation.png" alt-text="スクリーンショットは、インストールの完了を示しています。" border="true":::

コントロールを新しいバージョンにアップグレードすると、同じインストールが開始されたバナーが表示されますが、アップグレードが完了しても、コントロールの状態は引き続きインストールされます。 アップグレードが完了したことを確認するには、ソリューションの一覧 [https://make.powerapps.com/](https://make.preview.powerapps.com/)を確認します。所要時間は約 15 分です。

また、新しいバージョンがインストールされ、以前のバージョンが削除された特定のソリューションの履歴を確認することもできます。 :::image type="content" source="../assets/images/collaboration-control/history.png" alt-text="スクリーンショットは、インストールおよび削除されたバージョンの特定のソリューションの履歴を示しています。" border="true":::

## <a name="bookings-meetings"></a>Bookings Meetings

会議コントロールは、Bookings を使用して組織外のユーザーとやり取りするときに、1 つの会議で 1 つをサポートします。 現時点では、コラボレーション コントロールを使用して 1 対多の会議はサポートされていません。

**会議出席者の状態が正しくありません**

出席者の RSVPs が会議に参加している場合、参加者の応答の状態が、議事録ビューと会議の詳細の両方で正しく表示されない場合があります。 拒否ボタンを選択すると、画面にエラー メッセージが返されることがあります。

## <a name="tasks"></a>タスク

**タスク: フィルター "クリア" テキストが翻訳されない**

タスク フィルターに表示されている [クリア] ボタンのテキストは翻訳されません。

**タスク: グリッド コンテキスト メニューがトリミングされて表示される**

タスク グリッドに表示されるタスクの数が少ない場合、グリッド コンテキスト メニューはトリミングされて表示され、スクロール バーを使用する必要があります。

**タスク: キーワード検索フィルターは、"ゲスト" タスクに "BeginsWith" 演算子を使用します**

キーワード テキスト フィルターを使用してタスクを検索すると、"BeginsWith" 演算子を使用して "ゲスト" タスクが返されます。 "メンバー" タスクは、"Contains" 演算子を使用して返されます。

## <a name="files"></a>Files

ファイルのアーカイブ後にアーカイブ フォルダーに移動すると、アーカイブ フォルダーが重複する可能性があります。  アーカイブ フォルダーからファイル のメイン ビューに移動すると問題が解決され、アーカイブされたファイルは削除されません。

## <a name="controls"></a>コントロール

**コントロールの保存に失敗する**

コントロールがタスクまたは会議の保存に失敗した場合、グループ ID またはチャネル ID が正しく構成されていない可能性があります。  

解決策 1: ID が正しいことを確認し、設定が設定の演習に従って適用されていることを確認します。  

解決策 2: Power Apps 環境と Teams 環境が同じテナントにあることを確認します。  

**コントロールの読み込みまたはエラーの表示に失敗する**

コントロールの読み込みまたはエラーの表示に失敗した場合は、一時的な問題である可能性があります。

例:

:::image type="content" source="../assets/images/collaboration-control/sync-fail.png" alt-text="スクリーンショットは、コントロールの同期が失敗する方法を示しています。":::

これにより、コンソール ログに次のようにレンダリングされます。

:::image type="content" source="../assets/images/collaboration-control/control-fail.png" alt-text="スクリーンショットは、consol ログからの制御の失敗の例です。" border="true":::

解決策: ブラウザーを更新するか、Teams アプリでタブを再読み込みします。

Teams にアップロードした後でアプリ名、アイコン、または説明を変更する場合は、[アプリの外観をカスタマイズ](/MicrosoftTeams/customize-apps#customize-details-of-an-app)する方法に関するページを参照してください。

## <a name="error-logging"></a>エラー ログ

コントロールには、アプリケーションをデバッグするための次のメソッドが用意されています。

1. API が呼び出されたときのプラグイン イベントの **トレース ログ**。 この情報は、Dataverse 環境に格納されます。

    1. トレース ログを有効にするには、次の手順に従って [ログとトレースを行](/power-apps/developer/data-platform/logging-tracing?WT.mc_id=email)います。

1. UI コントロールの **ブラウザー ログ**。 これは標準のコンソール ログ記録です。

    1. ブラウザーを使用して Power Platform と Teams Web を介してCollaboration Manager アプリを実行する場合にサポートされます。
    1. コンソール タブで、Collaboration Manager エラー メッセージを使用するか、タスクなどのCollaboration Managerコントロール名を検索して、エラーを検索できます。

> [!TIP]
> Teams デスクトップ クライアントでエラーが発生した場合は、Teams Web でレプリケートしてエラー ログをキャプチャしてみてください。

## <a name="faq"></a>よく寄せられる質問

<br>

<details>

<summary><b>コラボレーション コントロール (プレビュー)とは何ですか?</b></summary>

コラボレーション コントロール (プレビュー) を使用すると、Power Apps の基幹業務カスタム アプリケーションに Microsoft 365 機能を追加して、Teams または Power Apps のビジネス プロセスで共同作業する際のユーザー ワークフローを簡略化できます。

<br>

</details>

<br>

<details>

<summary><b>メーカーのコラボレーション コントロール (プレビュー) の利点は何ですか?</b></summary>

これらの新しいコントロールを使用すると、作成者は Microsoft 365 コラボレーションをアプリに提供するコントロールをドラッグ アンド ドロップできます。

<br>

</details>

<br>

<details>

<summary><b>ユーザーのコラボレーション コントロール (プレビュー) の利点は何ですか?</b></summary>

ユーザーは、アプリのコンテキストを離れることなく、承認、ファイル、会議、メモ、タスクで共同作業することで、生産性の向上を体験し、フローを維持できます。

<br>

</details>

<br>

<details>

<summary><b>コラボレーション コントロール (プレビュー) にアクセス操作方法?</b></summary>

Power Platform 管理者に、AppSource から Power Apps 環境にコントロールをインストールするように要求します。

<br>

</details>

<br>

<details>

<summary><b>モデル 駆動型アプリにコントロールを追加操作方法?</b></summary>

フォーム デザイナーに移動し、コントロールを [コンポーネント] ウィンドウからフォームにドラッグします。

<br>

</details>
