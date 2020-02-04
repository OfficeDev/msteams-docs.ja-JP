---
title: メッセージング拡張機能検索コマンドを定義する
author: clearab
description: Microsoft Teams アプリのメッセージング拡張機能検索コマンドを定義します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b6837fb8a131d8ce3e2bbd0c51c2861dbffda2bc
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674934"
---
# <a name="define-messaging-extension-search-commands"></a>メッセージング拡張機能検索コマンドを定義する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

メッセージング拡張検索コマンドを使用すると、ユーザーは外部システムを検索し、その検索結果をカードの形式でメッセージに挿入することができます。

## <a name="choose-messaging-extension-invoke-locations"></a>メッセージング拡張機能の呼び出し場所を選択する

最初に決定する必要があるのは、検索コマンドをトリガー (または、より具体的に*呼び出す*) できる場所です。 検索コマンドは、次の場所のいずれかまたは両方から呼び出すことができます。

* [メッセージの作成] 領域の下部にあるボタン
* コマンドボックスで @mentioning

[メッセージの作成] 領域から呼び出した場合、ユーザーは会話に結果を送信することができます。 コマンドボックスから呼び出した場合、ユーザーは結果として得られたカードを操作したり、別の場所で使用するためにコピーしたりすることができます。

## <a name="add-the-command-to-your-app-manifest"></a>アプリケーションマニフェストにコマンドを追加する

ユーザーが検索コマンドをどのように操作するかが決定したので、それをアプリのマニフェストに追加します。 これを行うには、アプリマニフェスト`composeExtension` JSON の最上位レベルに新しいオブジェクトを追加します。 そのためには、アプリ Studio のヘルプを使用するか、手動で行うことができます。

### <a name="create-a-command-using-app-studio"></a>アプリ Studio を使用してコマンドを作成する

次の手順では、[メッセージング拡張機能が](~/messaging-extensions/how-to/create-messaging-extension.md)既に作成済みであることを前提としています。

1. Microsoft Teams クライアントから、 **App Studio**を開き、[**マニフェストエディター** ] タブを選択します。
2. アプリパッケージが既にアプリ Studio で作成されている場合は、一覧から選択します。 それ以外の場合は、既存のアプリパッケージをインポートできます。
3. [コマンド] セクションの [**追加**] ボタンをクリックします。
4. [ユーザーがサービスを照会して情報を受信できるようにする] を選択し、**それをメッセージに挿入**します。
5. **コマンド Id**と**タイトル**を追加します。
6. 検索コマンドを開始する場所を選択します。 現在、**メッセージ**を選択しても、検索コマンドの動作は変更されません。
7. 検索パラメーターを追加します。
8. [保存] をクリックします。

### <a name="manually-create-a-command"></a>コマンドを手動で作成する

メッセージング拡張機能検索コマンドをアプリマニフェストに手動で追加するには、オブジェクトの`composeExtension.commands`配列に follow パラメーターを追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このコマンドに割り当てる一意の ID です。 ユーザー要求には、この ID が含まれます。 | はい | 1.0 |
| `title` | コマンド名を指定します。 この値は UI に表示されます。 | はい | 1.0 |
| `description` | このコマンドの機能を示すヘルプテキスト。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | にする必要があります。 | いいえ | 1.4 |
|`initialRun` | **True**に設定すると、ユーザーが UI でこのコマンドを選択するとすぐにこのコマンドが実行されることを示します。 | いいえ | 1.0 |
| `context` | 検索アクションを使用できるコンテキストを定義する値のオプションの配列です。 可能な値`message`は`compose`、、 `commandBox`、です。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

また、検索パラメーターの詳細を追加して、Teams クライアントでユーザーに表示されるテキストを定義する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `parameters` | コマンドのパラメーターの静的リスト。 | いいえ | 1.0 |
| `parameter.name` | パラメーターの名前です。 これは、ユーザーの要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このパラメーターの目的または提供する必要がある値の例について説明します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | 簡単なユーザーフレンドリパラメーターのタイトルまたはラベル。 | はい | 1.0 |
| `parameter.inputType` | 必要な入力の種類を設定します。 可能な値`text`は`textarea`、 `number` `date` `time`、、、 `toggle`、です。 既定値はに設定されています`text` | いいえ | 1.4 |

#### <a name="app-manifest-example"></a>アプリマニフェストの例

以下に、検索コマンドを定義`composeExtensions`するオブジェクトの例を示します。 完全なマニフェストの例として、完全なアプリマニフェストスキーマについては、「 [app manifest スキーマ](~/resources/schema/manifest-schema.md)」を参照してください。

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```

## <a name="next-steps"></a>次のステップ

検索コマンドが追加されたので、[検索要求を処理](~/messaging-extensions/how-to/search-commands/respond-to-search.md)する必要があります。

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]