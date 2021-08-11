---
title: Developer Preview
description: パブリック サーバーの機能について説明Developer Preview Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: teams プレビュー開発者向け機能
ms.openlocfilehash: ddf935279d5298caa032df7f109369bdc4b798ef51206f5cc688846061fd6720
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57703962"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>開発者向けパブリック プレビュー Microsoft Teams

>[!NOTE]
>プレビューに含まれる機能は完全ではない可能性があります。また、パブリック リリースで利用可能になる前に変更が加わる可能性があります。 これらは、テストおよび探索の目的でのみ提供されます。 これらは、実稼働アプリケーションでは使用できません。

Developer Previewは、開発者向けの公開プログラムで、開発者は、開発中の未発表の機能に早期にアクセスMicrosoft Teams。 これにより、今後の機能を確認してテストし、アプリに潜在的に組み込Microsoft Teamsできます。 開発者プレビューの [機能](~/feedback.md) に関するフィードバックも歓迎します。 開発者プレビューはクライアントMicrosoft Teams有効になっているので、組織全体に影響を与える心配はありません。

## <a name="developer-preview-app-manifest"></a>開発者プレビュー アプリ マニフェスト

開発者プレビューで有効になっている多くの機能では、アプリ マニフェスト JSON ファイルを変更する必要があります。 これを行うには、開発者プレビュー マニフェスト スキーマ[](~/resources/schema/manifest-schema-dev-preview.md)を使用する必要があります このスキーマを使用する場合は[、App Studio](~/concepts/build-and-test/app-studio-overview.md)を使用してこれらの変更を加え、テスト用にアプリをアップロードすることはできません。 アプリをアップロードするには、アプリ バーのアイコンをクリックし、 を `More apps` 選択する必要があります `Upload a custom app link` 。 このメソッドを使用すると、圧縮されたバージョンのアプリ パッケージのみをアップロードできます。

App Studio を使用してアプリ パッケージの開発者以外のプレビュー部分を作成し、そのパッケージをエクスポートし、ファイルを手動で編集して、使用する開発者プレビュー機能を追加すると便利です `manifest.json` 。 開発者プレビュー機能をファイルに追加すると、パッケージを App Studio に再 `manifest.json` インポートできない。

## <a name="enable-developer-preview"></a>開発者プレビューを有効にする

開発者プレビューはクライアント単位で有効になっていますが、開発者プレビューを有効にするオプションは組織レベルで制御されます。 個人の開発者プレビューを有効にするオプションを有効にするには、ユーザーがカスタム アプリをアップロードできる機能を持っている必要があります。 詳細については [、「テナントのセットアップ](~/concepts/build-and-test/prepare-your-o365-tenant.md) 」を参照してください。

開発者プレビュー機能を含むアプリを使用すると、開発者プレビューを有効にしていないクライアントが予期せず動作する可能性があります。 開発者プレビューのエントリが表示されない場合、最も可能性の高い理由は、組織がアプリのアップロード用に構成されていないことです。

### <a name="on-a-desktop-or-web-client"></a>デスクトップまたは Web クライアント上

デスクトップまたは Web クライアントでパブリック開発者プレビューを有効にするには、次の操作を行う必要があります。

1. ここで説明するように、テナントの管理コンソールでアプリのアップロードを有効 [にします](~/concepts/build-and-test/prepare-your-o365-tenant.md)。
1. プロファイル (インターフェイスの右上または左下) をクリックしてTeamsメニュー Teamsします。
1. [開発者プレビュー→について] を選択します。
1. [開発者 **プレビューに切り替える] を選択します**。

### <a name="on-a-mobile-client"></a>モバイル クライアント上

モバイル クライアントでパブリック開発者プレビューを有効にするには、次の操作を行う必要があります。

1. ここで説明するように、テナントの管理コンソールでアプリのアップロードを有効 [にします](~/concepts/build-and-test/prepare-your-o365-tenant.md)。
1. 左上のハンバーガー メニューを開き、[次へ]**を設定。**
1. [概要 **] を選択します**。
1. [開発者プレビュー] トグルをクリックします。

## <a name="disable-developer-preview"></a>開発者プレビューを無効にする

[開発者向けプレビューについて] で同→を使用し、それをクリックしてオフにします。

## <a name="features-available-in-developer-preview"></a>開発者プレビューで使用可能な機能

開発者プレビューで現在有効になっている機能の完全な一覧については、「パブリック開発者プレビューの [機能」を参照してください](../../resources/dev-preview/developer-preview-features.md)。
