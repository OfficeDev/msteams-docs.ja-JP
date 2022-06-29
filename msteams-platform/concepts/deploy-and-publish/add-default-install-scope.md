---
title: アプリの既定のインストール オプションを構成する
description: Teams アプリの既定のインストール オプションと共有スコープの既定の機能を指定する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 75ea4dbae2379e6d6e7e2cc707314207cd7186ca
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503453"
---
# <a name="configure-default-install-options-for-teams-app"></a>Teams アプリの既定のインストール オプションを構成する

アプリは Teams で複数のシナリオをサポートするのが一般的ですが、特定のスコープと機能を念頭に置いて設計した可能性があります。 たとえば、アプリが主にチームまたはチャネルで使用される場合は、ストアにユーザーが最初に表示するインストール オプションが **チームに追加** されていることを確認できます。

:::row:::
   :::column span="2":::

![アプリドロップダウンの例を追加する](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

アプリの主な機能がボットの場合は、ユーザーがアプリをチームにインストールするときに、ボットを既定の機能にすることもできます。

## <a name="configure-your-apps-default-install-scope"></a>アプリの既定のインストール スコープを構成する

アプリの既定のインストール スコープを構成します。 一度に設定できるスコープは 1 つだけです。

アプリ マニフェストで既定のインストール スコープを構成するには:

1. アプリ マニフェストを開き、プロパティを追加します `defaultInstallScope` 。
2. 既定のインストール スコープの値を 、、、`personal``team``groupchat`または .`meetings`

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> 詳細については、 [アプリ マニフェスト スキーマ](~/resources/schema/manifest-schema.md)を参照してください。

## <a name="configure-the-default-capability-for-shared-scopes"></a>共有スコープの既定の機能を構成する

チーム、会議、またはグループチャット用にアプリをインストールするときに、既定の機能を構成します。

> [!NOTE]
> `defaultGroupCapability` は、チーム、groupchat、または会議に追加される既定の機能を提供します。 アプリの既定の機能としてタブ、ボット、またはコネクタを選択しますが、アプリ定義で選択した機能が提供されていることを確認する必要があります。

アプリ マニフェストで詳細を構成するには:

1. アプリ マニフェストを開き、そのマニフェストに `defaultGroupCapability` プロパティを追加します。
2. の値`team``groupchat`を設定します`meetings`。
3. 選択したグループ機能の場合、使用可能なグループ機能は 、、 `bot`、 `tab`、または `connector`.

    > [!NOTE]
    > 選択できる既定の機能は、1 つのみ、`bot``tab`または`connector`選択したグループ機能に対して選択できます。

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> 詳細については、 [アプリ マニフェスト スキーマ](~/resources/schema/manifest-schema.md)を参照してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アプリ パッケージを作成する](~/concepts/build-and-test/apps-package.md)
