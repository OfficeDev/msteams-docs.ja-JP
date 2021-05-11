---
title: ボット メッセージの書式を設定する
author: clearab
description: ボット メッセージにリッチ書式を追加する
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 7dc082f4b17e123c9fa000552f02fc913c66dcf7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020906"
---
# <a name="format-your-bot-messages"></a>ボット メッセージの書式を設定する

メッセージの書式設定を使用すると、ボット メッセージを最適に表示できます。 ボタン、テキスト、画像、オーディオ、ビデオなどの対話型要素を含む添付ファイルであるリッチ カードをボット メッセージに書式設定できます。

## <a name="format-text-content"></a>テキスト コンテンツの書式設定

ボット メッセージを書式設定するには、省略可能なプロパティを設定して、ボット メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) を制御できます。

Microsoft Teamsは、次の書式設定オプションをサポートしています。

| `TextFormat` value | 説明 |
| --- | --- |
| プレーン | テキストは、書式が適用されずに生テキストとして扱われる必要があります。|
| markdown | テキストはマークダウンの書式設定として扱い、必要に応じてチャネルにレンダリングする必要があります。 |
| xml | テキストは単純な XML マークアップです。 |

Teamsマークダウンタグと XML 書式タグまたは HTML 書式タグのサブセットをサポートしています。

現在、書式設定には次の制限が適用されます。

* テキスト専用メッセージは、テーブルの書式設定をサポートしません。
* リッチ カードは、タイトルプロパティや字幕プロパティではなく、text プロパティの書式設定のみをサポートします。
* リッチ カードでは、マークダウンやテーブルの書式設定はサポートされていません。

テキスト コンテンツの書式を設定した後、ユーザーがサポートしているすべてのプラットフォームで書式設定が機能Microsoft Teams。

## <a name="cross-platform-support"></a>クロスプラットフォームのサポート

一部のスタイルは現在、すべてのプラットフォームでサポートされていません。 次の表に、テキスト専用メッセージとリッチ カードでサポートされているスタイルとスタイルの一覧を示します。

| Style                     | テキスト専用メッセージ | リッチ カード - XML のみ |
| ---                       | :---: | :---: |
| 太字                      | ✔ | ✖ |
| 斜体                    | ✔ | ✔ |
| ヘッダー (レベル 1 &ndash; 3) | ✖ | ✔ |
| 取り消し線             | ✖ | ✔ |
| 水平ルーラー           | ✖ | ✖ |
| 記号付きリスト            | ✖ | ✔ |
| 番号付きリスト              | ✖ | ✔ |
| 書式設定済みのテキスト         | ✔ | ✔ |
| Blockquote                | ✔ | ✔ |
| Hyperlink                 | ✔ | ✔ |
| 画像リンク                | ✔ | ✖ |

クロスプラットフォーム サポートを確認した後、個々のプラットフォームによるサポートも利用できます。

## <a name="support-by-individual-platform"></a>個々のプラットフォームによるサポート

テキストの書式設定のサポートは、メッセージとプラットフォームの種類によって異なります。

### <a name="text-only-messages"></a>テキスト専用メッセージ

次の表に、デスクトップ、iOS、Android でサポートされているスタイルとスタイルの一覧を示します。

| Style                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| 太字                      | ✔ | ✔ | ✔ |
| 斜体                    | ✔ | ✔ | ✔ |
| ヘッダー (レベル 1 &ndash; 3) | ✖ | ✖ | ✖ |
| 取り消し線             | ✔ | ✔ | ✖ |
| 水平ルーラー           | ✖ | ✖ | ✖ |
| 記号付きリスト            | ✔ | ✖ | ✖ |
| 番号付きリスト              | ✔ | ✖ | ✖ |
| 書式設定済みのテキスト         | ✔ | ✔ | ✔ |
| Blockquote                | ✔ | ✔ | ✔ |
| Hyperlink                 | ✔ | ✔ | ✔ |
| 画像リンク                | ✔ | ✔ | ✔ |

### <a name="cards"></a>カード

カードのサポートについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボット メッセージの更新および削除](~/bots/how-to/update-and-delete-bot-messages.md)
