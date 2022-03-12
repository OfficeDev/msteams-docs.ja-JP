---
title: アプリの既定のインストール オプションを構成する
description: 共有スコープのアプリの既定のインストール オプションと既定の機能を指定する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: a6857e549c688bd7078aeaceae4b9f5a885ae2c3
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453209"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a>アプリの既定のインストール オプションMicrosoft Teamsする

アプリは、アプリで複数のシナリオをサポートTeams一般的ですが、特定の範囲と機能を念頭に置いて設計した可能性があります。 たとえば、アプリが主にチームまたはチャネルを使用する場合、ストアにユーザーが表示する最初のインストール オプションが [チームに追加] である必要 **があります**。

:::row:::
   :::column span="2":::

![アプリのドロップダウンの例を追加する](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

アプリの主な機能がボットである場合は、ユーザーがアプリをチームにインストールするときにボットを既定の機能にすることもできます。

## <a name="configure-your-apps-default-install-scope"></a>アプリの既定のインストール スコープを構成する

アプリの既定のインストール スコープを構成します。 一度に設定できるスコープは 1 つのみです。

アプリ マニフェストで既定のインストール スコープを構成するには、次の手順を実行します。

1. アプリ マニフェストを開き、プロパティを追加 `defaultInstallScope` します。
2. 既定のインストール スコープの値を 、`personal``team``groupchat`のいずれかとして設定します`meetings`。

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> 詳細については、「アプリ マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。

## <a name="configure-the-default-capability-for-shared-scopes"></a>共有スコープの既定の機能を構成する

チーム、会議、またはグループチャット用にアプリがインストールされている場合は、既定の機能を構成します。

> [!NOTE]
> `defaultGroupCapability` は、チーム、グループチャット、または会議に追加される既定の機能を提供します。 アプリの既定の機能としてタブ、ボット、またはコネクタを選択しますが、アプリ定義で選択した機能が提供されている必要があります。

アプリ マニフェストで詳細を構成するには、次の手順を実行します。

1. アプリ マニフェストを開き、プロパティ `defaultGroupCapability` を追加します。
2. 、または の値`team`を設定します`meetings`。 `groupchat`
3. 選択したグループ機能の場合、使用可能なグループ機能`bot``tab`は、、またはです`connector`。

    > [!NOTE]
    > 既定の機能 、、または`bot``tab``connector`選択したグループ機能の 1 つのみ選択できます。

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> 詳細については、「アプリ マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリ パッケージを作成する](~/concepts/build-and-test/apps-package.md)
