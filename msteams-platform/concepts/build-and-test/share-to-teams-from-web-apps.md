---
title: Web アプリから Teams に共有する
description: コード サンプルを使用して、Web サイトのプレビューを使用して、Web サイトの埋め込みボタンTeams共有を追加する方法について説明します
ms.topic: reference
ms.localizationpriority: medium
keywords: Teamsに共有Teams共有する
ms.openlocfilehash: b3efd268e2bded3955c2d9ab76d6dea755d06b5a
ms.sourcegitcommit: a3567e3e1a52b8e3cb2072b037f0e75bd0f12e58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2022
ms.locfileid: "65439301"
---
# <a name="share-to-teams-from-web-apps"></a>Web アプリから Teams に共有する

サード パーティの Web サイトでは、起動スクリプトを使用して、Web ページの Teams ボタンに Share を埋め込むことができます。 選択すると、ポップアップ ウィンドウで [Share to Teams エクスペリエンス] が起動します。 これにより、コンテキストを切り替えることなく、任意のユーザーまたはMicrosoft Teams チャネルへのリンクを直接共有できます。 このドキュメントでは、Web サイトの [Share to Teams] ボタンを作成して埋め込み、Web サイトプレビューを作成し、共有をMicrosoft Teams for Educationに拡張する方法について説明します。

> [!NOTE]
>
> * MicrosoftEdge&nbsp; と Google Chrome のデスクトップ バージョンのみがサポートされています。
> * Freemium またはゲスト アカウントの使用はサポートされていません。  

次の図は、Teamsに共有するポップアップ エクスペリエンスを示しています。

:::image type="content" source="../../assets/images/share-to-teams-popup.png" alt-text="ポップアップに共有Teams":::

## <a name="embed-a-share-to-teams-button"></a>[Teamsに共有を埋め込む] ボタン

1. Web ページに `launcher.js` スクリプトを追加します。

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. クラス属性と、その属性で共有するリンクを `teams-share-button` 含む HTML 要素を Web ページに `data-href` 追加します。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    これを完了すると、Microsoft Teams アイコンが Web サイトに追加されます。 次の図は、[Teamsに共有] アイコンを示しています。

    ![[Teamsに共有] アイコン](~/assets/icons/share-to-teams-icon.png)

1. または、[共有するTeams] ボタンに別のアイコン サイズが必要な場合は、属性を`data-icon-px-size`使用します。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```

1. 共有リンクにユーザー認証が必要で、リンクの URL プレビューが共有されるTeamsで適切にレンダリングされない場合は、属性セットを追加して URL プレビューを`data-preview``false`無効にすることができます。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. 選択したメッセージを作成ボックスに表示するには、属性で `data-msg-text` テキストを定義します。

     ```html
     <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-msg-text="<default-message-to-be-populated-in-compose-box>"
      data-preview="false">
      </div>
     ```

1. ページがコンテンツを動的にレンダリングする場合は、このメソッドを `shareToMicrosoftTeams.renderButtons()` 使用して **、** Share をパイプライン内の適切な場所に強制的にレンダリングすることができます。

## <a name="craft-your-website-preview"></a>Web サイトのプレビューを作成する

Web サイトがTeamsに共有されている場合、選択したチャネルに挿入されるカードには、Web サイトのプレビューが含まれます。 このプレビューの動作を制御するには、URL など、共有されている Web サイトに適切なメタデータを確実に `data-href` 追加します。  

プレビューを表示するには:

* **サムネイル イメージ**、または **タイトル** と **説明** の両方を含める必要があります。 最適な結果を得るには、3 つすべてを含めます。
* 共有 URL には認証は必要ありません。 認証が必要な場合は共有できますが、プレビューは作成されません。

次の表に、必要なタグの概要を示します。

|値|メタ タグ| Graphを開く|
|----|----|----|
|Title|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|説明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|サムネイル 画像| なし。 |`<meta property="og:image" content="http://example.com/image.jpg">`|

HTML の既定のバージョンまたは Open Graph バージョンのいずれかを使用できます。

## <a name="share-to-teams-for-education"></a>Microsoft Teams for Educationに共有する

[Teamsに共有] ボタンを使用する教師の場合は`Create an Assignment`、[. これにより、共有リンクに基づいて、選択したチームに割り当てを迅速に作成できます。 次の図は、教育用にTeamsに共有を表示します。

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="ポップアップ教育Teams共有する":::

## <a name="full-launcherjs-definition"></a>完全なlauncher.js定義

| プロパティ | HTML 属性 | 型 | 既定値 | 説明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | 該当なし | 共有するコンテンツの href。 |
| preview | `data-preview` | ブール値 (文字列として) | `true` | 共有するコンテンツのプレビューを表示するかどうかを指定します。 |
| iconPxSize | `data-icon-px-size` | number (文字列として) | `32` | レンダリングする [Teamsに共有] ボタンのサイズ (ピクセル単位)。 |
| msgText | `data-msg-text` | string | 該当なし | メッセージ作成ボックスのリンクの前に挿入される既定のテキスト。 最大文字数は 200 文字です。 |
| assignInstr | `data-assign-instr` | string | 該当なし | 割り当て "命令" フィールドに挿入される既定のテキスト。 最大文字数は 200 文字です。 |
| assignTitle | `data-assign-title` | string | 該当なし | 割り当て "タイトル" フィールドに挿入する既定のテキスト。 最大文字数は 50 文字です。 |

### <a name="methods"></a>メソッド

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (省略可能): `{ elements?: HTMLElement[] }`

現在、すべての共有ボタンがページにレンダリングされています。 省略可能 `options` なオブジェクトに要素の一覧が指定されている場合、それらの要素は共有ボタンにレンダリングされます。

### <a name="set-default-form-values"></a>既定のフォーム値を設定する

[Share to Teams] フォームの次のフィールドの既定値を設定できます。

* 次のことを言います。 `msgText`
* 割り当ての手順: `assignInstr`
* 課題のタイトル: `assignTitle`

#### <a name="example"></a>例

 次の例では、既定のフォーム値が指定されています。

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a>関連項目

* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
* [個人用アプリまたはタブから Teams に共有する](share-to-teams-from-personal-app-or-tab.md)
