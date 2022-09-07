---
title: さまざまな環境でアプリの動作をテストする
author: surbhigupta
description: このモジュールでは、さまざまな環境でアプリの動作をテストする方法について説明します
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 187219fec76830119e795d1dd60a36b2374c65ac
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617220"
---
# <a name="test-app-behavior-in-different-environment"></a>さまざまな環境でアプリの動作をテストする

Microsoft Teams と統合した後、Teams アプリをテストできます。 Teams アプリをテストするには、環境内に少なくとも 1 つのワークスペースを作成する必要があります。 Teams Toolkit を使用して Teams アプリをテストできます。

* **Teams でローカルでホストされている**: Teams Toolkit は、ローカル環境でテストするために Teams にサイドロードすることで、Teams アプリをローカルでホストします。

* **Teams でクラウドホスト: Teams** アプリをリモートでテストするには、Microsoft Azure Active Directory (Azure AD) でのプロビジョニングとデプロイを使用してクラウドホストする必要があります。 これには、ソリューションを Azure AD にアップロードし、Teams にアップロードする必要があります。

> [!NOTE]
> 運用環境規模のデバッグとテストでは、独自のプロセスを通じてテスト、ステージング、展開をサポートできるように、自分の会社のガイドラインに従うことをお勧めします。

## <a name="locally-hosted-environment"></a>ローカルでホストされる環境

Teams はクラウドベースの製品であり、アクセスするすべてのサービスを HTTPS エンドポイントを使用してパブリックに利用できるようにする必要があります。 ローカル ホスティングは、ローカル環境でテストするために Teams にサイドローディングすることです。

> [!NOTE]
> 任意のツールをテストに使用できますが、[ngrok](https://ngrok.com/download) を使用することをお勧めします

## <a name="cloud-hosted-environment"></a>クラウドホステッド環境

開発および運用コードとその HTTPS エンドポイントをホストするには、Azure AD でのプロビジョニングとデプロイを使用してチーム アプリをリモートでテストする必要があります。 ファイル内のオブジェクト`manifest.jason`に一覧表示されている Teams アプリからすべてのドメインに確実に[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)アクセスできるようにする必要があります

> [!NOTE]
> セキュリティで保護された環境を確保するには、参照する正確なドメインとサブドメインについて明示的に指定し、それらのドメインを制御する必要があります。たとえば、`*.azurewebsites.net` は推奨されませんが、`contoso.azurewebsites.net` をお勧めします。

## <a name="see-also"></a>関連項目

* [Microsoft Teams アプリをローカルでデバッグする](debug-local.md)
* [バックグランド プロセスのデバッグ](debug-background-process.md)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [クラウドにデプロイする](deploy.md)
* [Teams アプリ マニフェストのプレビューとカスタマイズ](TeamsFx-preview-and-customize-app-manifest.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
