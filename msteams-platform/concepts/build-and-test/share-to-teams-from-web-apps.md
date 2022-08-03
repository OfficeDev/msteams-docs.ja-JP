---
title: Web アプリから Teams に共有する
description: コード サンプルを使用して、Web サイトのプレビューを使用して、Web サイトの [Teams に共有] 埋め込みボタンを追加する方法について説明します
ms.topic: reference
ms.localizationpriority: medium
ms.openlocfilehash: 1d7b9b6ae80b224e67f24a589fae5e6af7e7f839
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232338"
---
# <a name="share-to-teams-from-web-apps"></a>Web アプリから Teams に共有する

サードパーティの Web サイトは、ランチャー スクリプトを使用して、Web ページに [Teams に共有​​] ボタンを埋め込むことができます。 [Teams に共有] ボタンを選択すると、ポップアップ ウィンドウで Teams への共有エクスペリエンスが起動します。 これにより、コンテキストを切り替えることなく、任意のユーザーまたはMicrosoft Teams チャネルへのリンクを直接共有できます。

次の図は、Teams への共有プレビュー エクスペリエンスのポップアップ ウィンドウを表示します。

:::image type="content" source="~/assets/images/share-to-teams-popup.png" alt-text="Share-to-Teams ポップアップ":::

> [!NOTE]
>
> * Microsoft&nbsp;Edge と Google Chrome のデスクトップ バージョンのみがサポートされています。
> * Freemium またはゲスト アカウントの使用はサポートされていません。

また、Web アプリ、個人用アプリ、またはタブでホストされている [Teams に共有] ボタンを使用して共有されているリンクのリンクを展開解除することもできます。詳細については、 [リンク解除に関するページを](~/messaging-extensions/how-to/link-unfurling.md)参照してください。

次の図は、[Teams に共有] ボタンを使用したリンク解除エクスペリエンスを示しています。

:::image type="content" source="~/assets/images/share-to-teams-link-unfurling.png" alt-text="Share-to-Teams のリンク展開":::

この記事では、Web サイトの [Teams に共有] ボタンを作成して埋め込み、Web サイトプレビューを作成し、共有をMicrosoft Teams for Educationに拡張する方法について説明します。

Teams に共有ボタンを埋め込む方法については、次のビデオを参照してください。
<br>
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4vhWH]
<br>

## <a name="embed-a-share-to-teams-button"></a>Teams への共有の埋め込みボタン

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

    これを完了すると、Teams アイコンが Web サイトに追加されます。 次の図は、[Teams に共有] アイコンを示しています。

    :::image type="content" source="~/assets/icons/share-to-teams-icon.png" alt-text="Teams に共有アイコン":::

1. または、[Teams に共有] ボタンに別のアイコン サイズが必要な場合は、属性を `data-icon-px-size` 使用します。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```

1. 共有リンクにユーザー認証が必要で、リンクの URL プレビューが Teams では適切にレンダリングされない場合は、属性セット`false`を追加して URL プレビューを`data-preview`無効にすることができます。

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

Web サイトが Teams と共有されている場合、選択したチャネルに挿入されるカードには、Web サイトのプレビューが含まれます。 このプレビューの動作を制御するには、URL など、共有されている Web サイトに適切なメタデータを確実に `data-href` 追加します。  

プレビューを表示するには:

* **サムネイル イメージ**、または **タイトル** と **説明** の両方を含める必要があります。 最適な結果を得るには、3 つすべてを含めます。
* 共有 URL には認証は必要ありません。 認証が必要な場合は共有できますが、プレビューは作成されません。

次の表に、必要なタグの概要を示します。

|Value|メタ タグ| グラフを開く|
|----|----|----|
|Title|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|説明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|サムネイル 画像| 何一つ。 |`<meta property="og:image" content="http://example.com/image.jpg">`|

HTML の既定のバージョンまたは Open Graph バージョンのいずれかを使用できます。

## <a name="share-to-teams-for-education"></a>Microsoft Teams for Educationに共有する

[チームに共有] ボタンを使用する教師には、共有リンクに `Create an Assignment` 基づいて選択したチームに割り当てを迅速に作成できる追加オプションがあります。 次の図は、教育機関向けの Teams への共有を示しています。

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="Teams に共有するポップアップ教育":::

## <a name="full-launcherjs-definition"></a>完全なlauncher.js定義

| プロパティ | HTML 属性 | Type | 既定値 | 説明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | 文字列 | 該当なし | 共有するコンテンツの href。 |
| preview | `data-preview` | ブール値 (文字列として) | `true` | 共有するコンテンツのプレビューを表示するかどうかを指定します。 |
| iconPxSize | `data-icon-px-size` | number (文字列として) | `32` | レンダリングする [Teams に共有] ボタンのサイズ (ピクセル単位)。 |
| msgText | `data-msg-text` | 文字列 | 該当なし | メッセージ作成ボックスのリンクの前に挿入される既定のテキスト。 最大文字数は 200 文字です。 |
| assignInstr | `data-assign-instr` | string | 該当なし | 割り当て "命令" フィールドに挿入される既定のテキスト。 最大文字数は 200 文字です。 |
| assignTitle | `data-assign-title` | string | 該当なし | 割り当て "タイトル" フィールドに挿入する既定のテキスト。 最大文字数は 50 文字です。 |

### <a name="methods"></a>メソッド

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (省略可能): `{ elements?: HTMLElement[] }`

現在、すべての共有ボタンがページにレンダリングされています。 省略可能 `options` なオブジェクトに要素の一覧が指定されている場合、それらの要素は共有ボタンにレンダリングされます。

### <a name="set-default-form-values"></a>既定のフォーム値を設定する

[Teams への共有] フォームで、次のフィールドの既定値を設定することを選択できます。

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
