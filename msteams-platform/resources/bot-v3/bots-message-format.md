---
title: ボットメッセージ形式
description: ボット メッセージの書式設定の詳細について説明します。
keywords: チーム シナリオ チャネル会話ボット メッセージ
ms.topic: reference
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: a9566331b259ba77f6770ff6394e8a788769af5d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566475"
---
# <a name="message-formatting-for-bots"></a>ボットのメッセージの書式設定

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

オプションの [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) プロパティを設定して、メッセージのテキスト コンテンツの表示方法を制御できます。

Microsoft Teamsは、次の書式設定オプションをサポートします。

| テキスト書式の値 | 説明 |
| --- | --- |
| 平地 | テキストは、書式設定がまったく適用されていない未加工のテキストとして扱う必要があります。 |
| markdown | テキストは Markdown フォーマットとして扱われ、必要に応じてチャネルにレンダリングされます。サポートされているスタイルの [テキストコンテンツの書式設定](#formatting-text-content) を参照してください。 |
| xml | テキストは単純な XML マークアップです。サポートされているスタイルの [テキストコンテンツの書式設定](#formatting-text-content) を参照してください。 |

## <a name="formatting-text-content"></a>テキストコンテンツの書式設定

Microsoft Teamsは、マークダウンおよび XML (HTML) 書式タグのサブセットをサポートします。

現在、以下の制限が適用されます。

* テキストのみのメッセージは、表の書式設定をサポートしていません。
* リッチ カードは、タイトルやサブタイトルのプロパティではなく、text プロパティの書式設定のみをサポートします。
* リッチ カードは、マークダウンまたはテーブルの書式設定をサポートしていません。

## <a name="cross-platform-support"></a>クロスプラットフォームサポート

Microsoft Teamsでサポートされているすべてのプラットフォームで書式設定が機能するように、一部のスタイルは現在、すべてのプラットフォームでサポートされていない点に注意してください。

| Style                     | テキストのみのメッセージ | リッチカード (XML のみ) |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| ヘッダー (レベル 1 &ndash; 3) | ✖ | ✔ |
| 取り消し線             | ✖ | ✔ |
| 水平ルール           | ✖ | ✖ |
| 順序なしリスト            | ✖ | ✔ |
| 順序付きリスト              | ✖ | ✔ |
| 書式設定済みのテキスト         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| hyperlink                 | ✔ | ✔ |
| 画像リンク                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>個々のプラットフォームによるサポート

テキストの書式設定のサポートは、メッセージの種類やプラットフォームによって異なります。

### <a name="text-only-messages"></a>テキストのみのメッセージ

| Style                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| ヘッダー (レベル 1 &ndash; 3) | ✖ | ✖ | ✖ |
| 取り消し線             | ✔ | ✔ | ✖ |
| 水平ルール           | ✖ | ✖ | ✖ |
| 順序なしリスト            | ✔ | ✖ | ✖ |
| 順序付きリスト              | ✔ | ✖ | ✖ |
| 書式設定済みのテキスト         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| hyperlink                 | ✔ | ✔ | ✔ |
| 画像リンク                | ✔ | ✔ | ✔ |

### <a name="cards"></a>カード

詳しくは、カードの [カードのフォーマット](~/task-modules-and-cards/cards/cards-format.md) を参照してください。
