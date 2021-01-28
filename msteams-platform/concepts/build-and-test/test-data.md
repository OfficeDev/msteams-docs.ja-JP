---
title: Office 365 テスト テナントにテスト データを追加する
description: Microsoft Teams アプリOfficeテストを成功するには、Office 365 開発者プログラム サブスクリプションをセットアップします。
ms.topic: how-to
keywords: アプリ開発者プログラム チームのテスト
ms.date: 11/01/2019
ms.openlocfilehash: 97eeb9c35b22adf75ad7f630fb2a621f0330e060
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014440"
---
# <a name="add-test-data-to-your-office-365-test-tenant"></a>Office 365 テスト テナントにテスト データを追加する

作成したアプリを簡単にテストするために、O365 開発者プログラム サブスクリプション (または他のテスト テナント) をセットアップします。  これは、次の場合に役立ちます。

- 組織で新しいチームとチャネルを作成する

- ユーザー コンテンツ パックを介して作成されたユーザーをそれらのチームに追加します。

## <a name="before-you-start"></a>始める前に

テスト テナントをまだお持ちでない場合は、Office 365 開発者プログラムに参加して、開発者サブスクリプションにサインアップする必要があります。 必要な PowerShell モジュールもインストールする必要があります。 どのテナントを使用する場合でも、スクリプトを実行するにはグローバル管理者のアクセス許可が必要です。

1. [Office 365 Developer Program に参加する](/office/developer-program/office-365-developer-program)
2. [Microsoft 365 Developer サブスクリプションをセットアップする](/office/developer-program/office-365-developer-program-get-started)
3. [Office 365 開発者サブスクリプションでサンプル データ パックを使用して Users コンテンツ パックをインストールする](/office/developer-program/install-sample-packs)
4. [Teams PowerShell モジュールをインストールする](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)
5. [Azure AD PowerShell モジュールをインストールする](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module)

### <a name="optional-step-allow-upload-of-custom-apps"></a>オプションの手順: カスタム アプリのアップロードを許可する

既定では、テナント アプリ カタログにカスタム アプリをアップロードできるのは、グローバル管理者または Teams サービス管理者のみです。  また、すべてのユーザーが自分で使用するためにカスタム アプリをアップロードしたり、テスト用にチームにアップロードしたりすることもできます。

この設定を有効にするには、Teams 管理ポータルでグローバルなアプリセットアップ ポリシーを更新する必要があります。

<img width="430px" src="~/assets/images/microsoft-teams-admin-center-screenshot.png" title="アプリのセットアップ ポリシーのスクリーンショット" />

詳細については、次のトピックを参照してください。

 - [Microsoft Teams のアプリのセットアップ ポリシーを管理する](/microsoftteams/teams-app-setup-policies)

## <a name="create-teams-and-channels"></a>チームとチャネルを作成する

次のスニペットを XML (.xml) として保存し、保存した場所をメモします。  この XML は、作成されるチームとチャネルの構造とそのメンバーを定義します。

```xml
<?xml version="1.0"?>
<Teams>
  <Team Name="Store Portal" ID="storeportal" Description="" Type="Private" Creator="admin">
    <Members>
      <Member UserName="AlexW" IsOwner="false"/>
      <Member UserName="PattiF" IsOwner="false"/>
      <Member UserName="PradeepG" IsOwner="false"/>
      <Member UserName="JoniS" IsOwner="false"/>
      <Member UserName="JohannaL" IsOwner="false"/>
      <Member UserName="NestorW" IsOwner="false"/>
      <Member UserName="IsaiahL" IsOwner="false"/>
      <Member UserName="AdeleV" IsOwner="false"/>
      <Member UserName="LeeG" IsOwner="false"/>
      <Member UserName="MeganB" IsOwner="true"/>
      <Member UserName="LynneR" IsOwner="false"/>
      <Member UserName="GradyA" IsOwner="false"/>
      <Member UserName="LidiaH" IsOwner="false"/>
      <Member UserName="DiegoS" IsOwner="false"/>
      <Member UserName="MiriamG" IsOwner="true"/>
    </Members>
    <Channels>
      <Channel Name="Sales" ID="sales" Description="" Creator="Admin" />
      <Channel Name="Inventory" ID="inventory" Description="" Creator="Admin" />
      <Channel Name="Los Angeles Store 239" ID="losangelesstore239" Description="" Creator="Admin" />
      <Channel Name="Seattle Store 121" ID="seattlestore121" Description="" Creator="Admin" />
      <Channel Name="Online" ID="online" Description="" Creator="Admin" />
      <Channel Name="Store Layout" ID="storelayout" Description="" Creator="Admin" />
      <Channel Name="Promotions" ID="promotions" Description="" Creator="Admin" />
    </Channels>
  </Team>
  <Team Name="Mark 8 Project Team" ID="Mark8ProjectTeam" Description="Welcome to the team that we've assembled to create the Mark 8." Type="Private" Creator="admin">
    <Members>
      <Member UserName="meganb" IsOwner="true" />
      <Member UserName="alexw" IsOwner="false" />
      <Member UserName="lynner" IsOwner="false" />
      <Member UserName="isaiahl" IsOwner="false" />
      <Member UserName="leeg" IsOwner="false" />
      <Member UserName="pradeepg" IsOwner="false" />
      <Member UserName="lidiah" IsOwner="false" />
      <Member UserName="diegos" IsOwner="false" />
      <Member UserName="johannal" IsOwner="false" />
      <Member UserName="miriamg" IsOwner="false" />
      <Member UserName="adelev" IsOwner="false" />
      <Member UserName="jonis" IsOwner="false" />
      <Member UserName="nestorw" IsOwner="false" />
      <Member UserName="gradya" IsOwner="false" />
      <Member UserName="pattif" IsOwner="false" />
    </Members>
    <Channels>
      <Channel Name="Research and Development" ID="researchanddevelopment" Description="Channel for Research and Development!" Creator="meganb" />
      <Channel Name="Design" ID="design" Description="Discuss design projects." Creator="meganb" />
      <Channel Name="Digital Assets Web" ID="digitalassetsweb" Description="Discuss digital assets." Creator="meganb" />
      <Channel Name="Go to Market Plan" ID="gotomarketplan" Description="Our go-to-market plan!" Creator="meganb" />
    </Channels>
  </Team>
  <Team Name="District 9 Road Safety Audit" ID="district9roadsafetyaudit" Description="" Type="Private" Creator="admin">
    <Members>
      <Member UserName="meganb" IsOwner="true" />
      <Member UserName="alexw" IsOwner="false" />
      <Member UserName="lynner" IsOwner="false" />
      <Member UserName="isaiahl" IsOwner="false" />
      <Member UserName="leeg" IsOwner="false" />
      <Member UserName="pradeepg" IsOwner="false" />
      <Member UserName="lidiah" IsOwner="false" />
      <Member UserName="diegos" IsOwner="false" />
      <Member UserName="johannal" IsOwner="false" />
      <Member UserName="miriamg" IsOwner="false" />
      <Member UserName="adelev" IsOwner="false" />
      <Member UserName="jonis" IsOwner="false" />
      <Member UserName="nestorw" IsOwner="false" />
      <Member UserName="gradya" IsOwner="false" />
      <Member UserName="pattif" IsOwner="false" />
    </Members>
    <Channels>
      <Channel Name="Audit Planning" ID="auditplanning" Description="" Creator="Admin" />
      <Channel Name="Delivery" ID="delivery" Description="" Creator="Admin" />
      <Channel Name="Findings" ID="findings" Description="" Creator="Admin" />
      <Channel Name="Recommended Actions" ID="recommendedactions" Description="" Creator="Admin" />
      <Channel Name="Survey" ID="survey" Description="" Creator="Admin" />
    </Channels>
  </Team>
  <Team Name="ACC-1000 Product Team" ID="acc1000productteam" Description="" Type="Private" Creator="admin" >
    <Members>
      <Member UserName="meganb" IsOwner="true" />
      <Member UserName="alexw" IsOwner="false" />
      <Member UserName="lynner" IsOwner="false" />
      <Member UserName="isaiahl" IsOwner="false" />
      <Member UserName="leeg" IsOwner="false" />
      <Member UserName="pradeepg" IsOwner="false" />
      <Member UserName="lidiah" IsOwner="false" />
      <Member UserName="diegos" IsOwner="false" />
      <Member UserName="johannal" IsOwner="false" />
      <Member UserName="miriamg" IsOwner="false" />
      <Member UserName="adelev" IsOwner="false" />
      <Member UserName="jonis" IsOwner="false" />
      <Member UserName="nestorw" IsOwner="false" />
      <Member UserName="gradya" IsOwner="false" />
      <Member UserName="pattif" IsOwner="false" />
    </Members>
    <Channels>
      <Channel Name="Corporate Communication" ID="corporatecommunication" Description="" Creator="Admin" />
      <Channel Name="Lean Process Improvement" ID="corporatecommunication" Description="" Creator="Admin" />
      <Channel Name="Training and Certification" ID="trainingandcertification" Description="" Creator="Admin" />
      <Channel Name="Production" ID="production" Description="" Creator="Admin" />
      <Channel Name="Research and Development" ID="researchanddevelopment" Description="" Creator="Admin" />
      <Channel Name="Supplier Collaboration" ID="suppliercollaboration" Description="" Creator="Admin" />
    </Channels>
  </Team>
</Teams>
```

次のスニペットを PowerShell スクリプト (.ps1) として保存し、保存した場所をメモします。  このスクリプトは、チームとチャネルを作成し、メンバーを追加する手順を実行します。

```powershell
Param(
    [Parameter(Mandatory = $true)]
    
    # This specifies the location of your configuration XML.
    
    [string] $teamsFilePath 
)
    
[xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

if ($XmlDocument.Teams.Team.Count -gt 0) {

    try {
        
        # 1. Login with the global administrator account for your O365 Developer Program tenant.  This script will then use these credentials to connect to the powershell modules for Azure Active Directory and Microsoft Teams
        
        $creds = Get-Credential

        # Connecting to AAD PowerShell
        Connect-AzureAD -Credential $creds | Out-Null

        # Connect to Microsoft Teams PowerShell
        Connect-MicrosoftTeams -Credential $creds | Out-Null

        Write-Host "Connected to Microsoft 365 and configuring your organization with test teams and channels"

        # 2. Create the teams as specified in the XML.
        
        foreach ($team in $XmlDocument.Teams.Team ) {
            try {
                $group = New-Team -DisplayName $team.Name -Description $teams.description -visibility public 
                Write-Host "Successfully created team: " $group.DisplayName
            }
            catch {
                Write-Host "Unable to create team: $_"
            }
                
            # 3. Add users to the newly created teams.
            foreach ($user in $team.Members.Member) {
                try {
                    $newUserPrincipalName = (Get-AzureADUser -SearchString $user.UserName).UserPrincipalName

                    if($user.IsOwner -eq $true){
                        Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName -Role Owner | Out-Null
                    }else{
                        Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName | Out-Null
                    }

                    Write-Host "Successfully added user : " $user.UserName
                }
                catch {
                    Write-Host "Unable to add team user: $_"
                }

            }

            # 4. Add a set of channels to each newly created team
            foreach ($channel in $team.Channels.Channel) {
                try {
                    # Adding each team channel
                    New-TeamChannel -GroupId $group.GroupId -DisplayName $channel.Name -Description $channel.Description | Out-Null
                    Write-Host "Successfully created channel: " $channel.Name
                }
                catch {
                    Write-Host "Unable to add new Team Channel: $_"
                }   
            }

            Clear-Variable -Name group
        }

        Clear-Variable -Name creds
        
        # 5. Disconnect from all PowerShell sessions
        
        Write-Host "Completed execution and disconnecting from Microsoft 365 PowerShell sessions."
        Disconnect-MicrosoftTeams
        Disconnect-AzureAD
    }
    catch {
        Write-Host "Unable to complete the operation: $_"
    }
}
else {
    Write-Host "Content file has invalid data."
}
```

管理者モードWindows PowerShellセッションを開きます。  保存したスクリプトを実行します。  資格情報の入力を求めるメッセージが表示されます。開発者サブスクリプションに最初にサインアップするときに受け取ったグローバル管理者の資格情報を使用します。

> [!Note]
> スクリプトの実行には数分かかりますが、PowerShell セッションは閉じできません。  サブスクリプションのユーザーを既定のコンテンツ パックで作成された内容から変更した場合、一部のユーザーがチームに追加されない可能性があります。  スクリプトを実行すると、成功または失敗したアクションが出力されます。

スクリプトの実行が完了したら、ユーザー アカウントのいずれかを使用して Teams クライアントにログインし、新しく作成したチームを表示できます。
