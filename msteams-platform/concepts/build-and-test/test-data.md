---
title: テストデータを Office 365 テストテナントに追加する
description: Microsoft Teams アプリを正常にテストするために Office 365 developer program サブスクリプションをセットアップする
keywords: アプリ開発者プログラムチームのテスト
ms.date: 11/01/2019
ms.openlocfilehash: 2d32b0bf4243d540eeb5e2cc89ea2518d737ae17
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674739"
---
# <a name="add-test-data-to-your-office-365-test-tenant"></a><span data-ttu-id="01ec5-104">テストデータを Office 365 テストテナントに追加する</span><span class="sxs-lookup"><span data-stu-id="01ec5-104">Add test data to your Office 365 test tenant</span></span>

<span data-ttu-id="01ec5-105">O365 開発者プログラムのサブスクリプション (またはその他のテストテナント) をセットアップして、作成したアプリを簡単にテストできるようにします。</span><span class="sxs-lookup"><span data-stu-id="01ec5-105">Set up your O365 developer program subscription (or other test tenant) to make it easy for you to test the apps that you've built.</span></span>  <span data-ttu-id="01ec5-106">これは次のような場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="01ec5-106">It will help you:</span></span>

- <span data-ttu-id="01ec5-107">組織に新しいチームとチャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="01ec5-107">Create new teams and channels in your organization</span></span>

- <span data-ttu-id="01ec5-108">ユーザーコンテンツパックを介して作成されたユーザーを、これらのチームに追加します。</span><span class="sxs-lookup"><span data-stu-id="01ec5-108">Add the users that are created via the User content pack to those teams.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="01ec5-109">始める前に</span><span class="sxs-lookup"><span data-stu-id="01ec5-109">Before you start</span></span>

<span data-ttu-id="01ec5-110">まだテストテナントがない場合は、Office 365 開発者プログラムに参加して、開発者向けサブスクリプションにサインアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="01ec5-110">If you don't already have a test tenant, you will need to join the Office 365 developer program and sign up for a developer subscription.</span></span> <span data-ttu-id="01ec5-111">必要な powershell モジュールをインストールする必要もあります。</span><span class="sxs-lookup"><span data-stu-id="01ec5-111">You'll also need to install the necessary powershell modules.</span></span> <span data-ttu-id="01ec5-112">使用しているテナントについては、スクリプトを実行するためのグローバル管理者のアクセス許可が必要になります。</span><span class="sxs-lookup"><span data-stu-id="01ec5-112">For whatever tenant you use you'll need to have global administrator permissions to run the scripts.</span></span>

1. [<span data-ttu-id="01ec5-113">Office 365 Developer Program に参加する</span><span class="sxs-lookup"><span data-stu-id="01ec5-113">Join the Office 365 Developer Program</span></span>](/office/developer-program/office-365-developer-program)
2. [<span data-ttu-id="01ec5-114">Microsoft 365 Developer サブスクリプションをセットアップする</span><span class="sxs-lookup"><span data-stu-id="01ec5-114">Set up a Microsoft 365 Developer Subscription</span></span>](/office/developer-program/office-365-developer-program-get-started)
3. [<span data-ttu-id="01ec5-115">Office 365 開発者向けサブスクリプションでサンプルのデータパックを使用して、ユーザーのコンテンツパックをインストールする</span><span class="sxs-lookup"><span data-stu-id="01ec5-115">Use sample data packs with your Office 365 developer subscription to install the Users content pack</span></span>](/office/developer-program/install-sample-packs)
4. [<span data-ttu-id="01ec5-116">Teams PowerShell モジュールをインストールする</span><span class="sxs-lookup"><span data-stu-id="01ec5-116">Install the Teams PowerShell module</span></span>](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)
5. [<span data-ttu-id="01ec5-117">Azure AD PowerShell モジュールをインストールする</span><span class="sxs-lookup"><span data-stu-id="01ec5-117">Install the Azure AD PowerShell module</span></span>](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module)

### <a name="optional-step-allow-upload-of-custom-apps"></a><span data-ttu-id="01ec5-118">オプションの手順: カスタムアプリのアップロードを許可する</span><span class="sxs-lookup"><span data-stu-id="01ec5-118">Optional step: allow upload of custom apps</span></span>

<span data-ttu-id="01ec5-119">既定では、グローバル管理者または teams サービス管理者のみが、カスタムアプリをテナントのアプリカタログにアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="01ec5-119">By default, only global admins or teams service admins can upload custom apps into the tenant app catalog.</span></span>  <span data-ttu-id="01ec5-120">また、すべてのユーザーが自分で使用するカスタムアプリ、またはテストのために teams をアップロードできるようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="01ec5-120">You can also enable all users to upload custom apps for their own use or to teams for testing.</span></span>

<span data-ttu-id="01ec5-121">この設定を有効にするには、Teams 管理ポータルでグローバルアプリセットアップポリシーを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="01ec5-121">To enable this setting, you'll need to update the global App Setup Policy in your Teams Admin Portal.</span></span>

<img width="430px" src="~/assets/images/microsoft-teams-admin-center-screenshot.png" title="アプリのセットアップポリシーのスクリーンショット" />

<span data-ttu-id="01ec5-123">詳細については、次のトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="01ec5-123">For more information see:</span></span>

 - [<span data-ttu-id="01ec5-124">Microsoft Teams でアプリのセットアップポリシーを管理する</span><span class="sxs-lookup"><span data-stu-id="01ec5-124">Manage app setup policies in Microsoft Teams</span></span>](/microsoftteams/teams-app-setup-policies)

## <a name="create-teams-and-channels"></a><span data-ttu-id="01ec5-125">チームとチャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="01ec5-125">Create teams and channels</span></span>

<span data-ttu-id="01ec5-126">次のスニペットを XML (.xml) として保存し、保存した場所をメモします。</span><span class="sxs-lookup"><span data-stu-id="01ec5-126">Save the following snippet as an XML (.xml) and note where you've saved it.</span></span>  <span data-ttu-id="01ec5-127">この XML は、作成する teams およびチャネルの構造と、そのメンバーによって定義されます。</span><span class="sxs-lookup"><span data-stu-id="01ec5-127">This XML defines the structure of the teams and channels that will be created - along with its members.</span></span>

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

<span data-ttu-id="01ec5-128">次のスニペットを PowerShell スクリプト (. ps1) として保存し、保存した場所をメモします。</span><span class="sxs-lookup"><span data-stu-id="01ec5-128">Save the following snippet as a PowerShell script (.ps1) and note where you've saved it.</span></span>  <span data-ttu-id="01ec5-129">このスクリプトは、チームとチャネルを作成し、それらにメンバーを追加するための手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="01ec5-129">This script executes the steps to create the teams and channels and add members to them.</span></span>

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

<span data-ttu-id="01ec5-130">Windows PowerShell セッションを管理者モードで開きます。</span><span class="sxs-lookup"><span data-stu-id="01ec5-130">Open a Windows PowerShell session in Administrator mode.</span></span>  <span data-ttu-id="01ec5-131">保存したばかりのスクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="01ec5-131">Run the script that you just saved.</span></span>  <span data-ttu-id="01ec5-132">資格情報を入力するように求めるメッセージが表示されます。開発者サブスクリプションに最初にサインアップしたときに受信したグローバル管理者の資格情報を使用します。</span><span class="sxs-lookup"><span data-stu-id="01ec5-132">You'll be prompted to provide the credentials - use the Global Administrator credentials you received when you first signed up for your developer subscription.</span></span>

> [!Note]
> <span data-ttu-id="01ec5-133">このスクリプトは、実行に数分かかる場合があります。 PowerShell セッションを閉じないでください。</span><span class="sxs-lookup"><span data-stu-id="01ec5-133">The script will take several minutes to execute - do not close your PowerShell session.</span></span>  <span data-ttu-id="01ec5-134">サブスクリプション内のユーザーのうち、既定のコンテンツパックで作成されたものを変更した場合、一部のユーザーが teams に追加されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="01ec5-134">If you've modified the users in your subscription from what is created in the default content pack, some users may not be added to teams.</span></span>  <span data-ttu-id="01ec5-135">スクリプトを実行すると、成功または失敗したアクションが出力されます。</span><span class="sxs-lookup"><span data-stu-id="01ec5-135">As the script executes it will output successful or failed actions.</span></span>

<span data-ttu-id="01ec5-136">スクリプトの実行が完了すると、ユーザーアカウントのいずれかを使用して Teams クライアントにログインし、新しく作成された teams を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="01ec5-136">Once the script has finished execution, you can login to the Teams client with one of the user accounts and view the newly created teams.</span></span>