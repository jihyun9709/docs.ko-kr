---
title: "관리자를 위한 .NET Framework 배포 가이드 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "관리자 가이드, .NET Framework 배포"
  - "배포[.NET Framework], 관리자 가이드"
ms.assetid: bee14036-0436-44e8-89f5-4bc61317977a
caps.latest.revision: 40
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 38
---
# 관리자를 위한 .NET Framework 배포 가이드
이 단계별 문서에서는 시스템 관리자가 Microsoft System Center Configuration Manager를 사용하여 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 및 해당 시스템 종속성을 네트워크 전체에 배포할 수 있는 방법에 대해 설명합니다.  이 문서에서는 .NET Framework 4의 최소 요구 사항이 모든 대상 클라이언트 컴퓨터에서 충족되는 것으로 가정합니다.  [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 설치를 위한 소프트웨어와 하드웨어 요구 사항 목록은 [시스템 요구 사항](../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
> [!NOTE]
>  [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], System Center Configuration Manager 및 Active Directory를 비롯하여 이 문서에서 언급된 소프트웨어에는 각각 사용권 계약 내용이 적용됩니다.  이 지침에서는 적절한 소프트웨어 라이선스로 이러한 사용권 계약 내용을 검토하고 이에 동의했다고 가정합니다.  이 지침에서는 이러한 사용권 계약의 어떠한 내용도 배제하지 않습니다.  
>   
>  .NET Framework 지원에 대한 내용은 Microsoft 지원 웹 사이트의 [Microsoft .NET Framework 지원 기간 정책](http://go.microsoft.com/fwlink/?LinkId=196607)을 참조하세요.  
  
 이 항목에는 다음과 같은 단원이 포함되어 있습니다.  
  
 [배포 프로세스](#the_deployment_process)   
 [.NET Framework 배포](#deploying_in_a_test_environment)  
 [컬렉션 만들기](#creating_a_collection)  
 [패키지 및 프로그램 만들기](#creating_a_package)  
 [배포 지점 선택](#select_dist_point)  
 [패키지 배포](#deploying_package)  
 [리소스](#resources)  
 [문제 해결](#troubleshooting)  
  
<a name="the_deployment_process"></a>   
## 배포 프로세스  
 지원 인프라가 갖춰진 경우 System Center 2012 Configuration Manager를 사용하여 .NET Framework 재배포 가능 패키지를 네트워크 상의 컴퓨터에 배포합니다.  인프라 구축에는 컬렉션, 소프트웨어에 대한 패키지와 프로그램, 배포 지점, 배포의 5가지 주요 영역을 만들고 정의하는 작업이 포함됩니다.  
  
-   **컬렉션**은 .NET Framework가 배포되는 대상인 사용자, 사용자 그룹 또는 컴퓨터와 같은 Configuration Manager 리소스의 그룹입니다.  자세한 내용은 Configuration Manager 문서 라이브러리에서 [Configuration Manager의 컬렉션](http://technet.microsoft.com/library/gg682169.aspx)을 참조하세요.  
  
-   **패키지 및 프로그램**은 보통 클라이언트 컴퓨터에 설치할 소프트웨어 응용 프로그램을 나타내지만, 개별 파일, 업데이트 또는 개별 명령까지도 들어 있을 수 있습니다.  자세한 내용은 Configuration Manager 문서 라이브러리에서 [Configuration Manager의 패키지 및 프로그램](http://technet.microsoft.com/library/gg699369.aspx)을 참조하세요.  
  
-   **배포 지점**은 클라이언트 컴퓨터에서 실행할 소프트웨어에 필요한 파일을 저장하는 Configuration Manager 사이트 시스템 역할입니다.  Configuration Manager 클라이언트가 소프트웨어 배포를 수신하고 처리할 때, 이 클라이언트는 배포 지점에 연결하여 소프트웨어와 연결된 콘텐츠를 다운로드하고 설치 프로세스를 시작합니다.  자세한 내용은 Configuration Manager 문서 라이브러리에서 [Configuration Manager의 콘텐츠 관리 소개](http://technet.microsoft.com/library/gg682083.aspx)를 참조하세요.  
  
-   **배포**에서는 지정된 대상 컬렉션의 적절한 멤버에게 소프트웨어 패키지를 설치하라고 지시합니다.  자세한 내용은 Configuration Manager 문서 라이브러리에서 [Configuration Manager에 응용 프로그램을 배포하는 방법](http://technet.microsoft.com/library/gg682082.aspx)을 참조하세요.  
  
> [!IMPORTANT]
>  이 항목의 절차에는 패키지와 프로그램을 만들고 배포하기 위한 일반적인 설정이 포함되어 있고, 가능한 모든 설정이 다루어지지 않을 수도 있습니다.  다른 Configuration Manager 배포 옵션은 [Configuration Manager 문서 라이브러리](http://technet.microsoft.com/library/gg682041.aspx)를 참조하세요.  
  
<a name="deploying_in_a_test_environment"></a>   
## .NET Framework 배포  
 System Center 2012 Configuration Manager를 사용하여 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]의 자동 설치를 배포할 수 있고, 이 경우 사용자는 설치 프로세스와 상호 작용할 필요가 없습니다.  아래 단계를 수행합니다.  
  
1.  [컬렉션 만들기](#creating_a_collection)  
  
2.  [.NET Framework 재배포 가능 패키지와 프로그램을 만듭니다](#creating_a_package).  
  
3.  [배포 지점 선택](#select_dist_point)  
  
4.  [패키지를 배포합니다](#deploying_package).  
  
<a name="creating_a_collection"></a>   
### 컬렉션 만들기  
 이 단계에서는 패키지와 프로그램을 배포할 컴퓨터를 선택하고 이런 컴퓨터를 장치 컬렉션으로 그룹화합니다.  Configuration Manager에서 컬렉션을 만들려면 직접 멤버 자격 규칙\(컬렉션 멤버를 수동으로 지정함\) 또는 쿼리 규칙\(사용자가 지정하는 기준을 바탕으로 Configuration Manager가 컬렉션 멤버를 결정함\)을 사용할 수 있습니다.  쿼리와 직접 규칙을 포함한 멤버 자격 규칙에 대한 자세한 내용은 Configuration Manager 문서 라이브러리에서 [Configuration Manager의 컬렉션 소개](http://technet.microsoft.com/library/gg682177.aspx)를 참조하세요.  
  
 컬렉션을 만들려면  
  
1.  Configuration Manager 콘솔에서 **자산 및 준수**를 선택합니다.  
  
2.  **자산 및 준수** 작업 영역에서 **장치 컬렉션**을 선택합니다.  
  
3.  **만들기** 그룹의 **홈** 탭에서 **장치 컬렉션 만들기**를 선택합니다.  
  
4.  **장치 컬렉션 만들기 마법사**의 **일반** 페이지에서 컬렉션 이름을 입력합니다.  
  
5.  **찾아보기**를 선택하여 제한 컬렉션을 지정합니다.  
  
6.  **멤버 자격 규칙** 페이지에서 **규칙 추가**를 선택한 다음 **직접 규칙**을 선택하여 **직접 멤버 자격 규칙 만들기 마법사**를 엽니다.  **다음**을 선택합니다.  
  
7.  **리소스 검색** 페이지의 **리소스 클래스** 목록에서 **시스템 리소스**를 선택합니다.  **특성 이름** 목록에서 **이름**을 선택합니다.  **값** 필드에 `%`를 입력하고 **다음**을 선택합니다.  
  
8.  **리소스 선택** 페이지에서 .NET Framework를 배포할 각 컴퓨터에 대한 확인란을 선택합니다.  **다음**을 선택한 후 마법사를 완료합니다.  
  
9. **장치 컬렉션 만들기 마법사**의 **멤버 자격 규칙** 페이지에서 **다음**을 선택한 후 마법사를 완료합니다.  
  
 컬렉션에 대한 자세한 내용은 Configuration Manager 문서 라이브러리에서 [Configuration Manager의 컬렉션](http://technet.microsoft.com/library/bb693730.aspx)을 참조하세요.  
  
<a name="creating_a_package"></a>   
### .NET Framework 재배포 가능 패키지에 대한 프로그램과 패키지를 만듭니다.  
 다음 단계에서는 .NET Framework 재배포 가능 패키지를 수동으로 만듭니다.  이 패키지에는 .NET Framework를 설치하기 위해 지정된 매개 변수와 패키지가 대상 컴퓨터에 배포될 시작 위치가 포함되어 있습니다.  
  
 패키지를 만들려면  
  
1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 선택합니다.  
  
2.  **소프트웨어 라이브러리** 작업 영역에서 **응용 프로그램 관리**를 확장한 후 **패키지**를 선택합니다.  
  
3.  **만들기** 그룹의 **홈** 탭에서 **패키지 만들기**를 선택합니다.  
  
4.  **패키지 및 프로그램 만들기 마법사**의 **패키지** 페이지에서 다음 정보를 입력합니다.  
  
    -   이름: `.NET Framework 4.5`  
  
    -   Manufacturer: `Microsoft`  
  
    -   Language:  `English (US)`  
  
5.  **이 패키지에 소스 파일이 포함됨**을 선택한 후 **찾아보기**를 선택하여 .NET Framework 설치 파일이 들어 있는 로컬 또는 네트워크 폴더를 선택합니다.  폴더를 선택했을 때 **확인**을 선택한 후 **다음**을 선택합니다.  
  
6.  마법사의 **프로그램 형식** 페이지에서 **표준 프로그램**을 선택한 후 **다음**을 선택합니다.  
  
7.  **패키지 및 프로그램 만들기 마법사**의 **프로그램** 페이지에서 다음 정보를 입력합니다.  
  
    1.  **이름:** `.NET Framework 4.5`  
  
    2.  **명령줄:** `dotNetFx45_Full_x86_x64.exe /q /norestart /ChainingPackage ADMINDEPLOYMENT`\(명령줄 옵션은 이들 단계 뒤에 있는 표에 설명되어 있음\)  
  
    3.  **실행:** **숨김**을 선택합니다.  
  
    4.  **프로그램을 실행할 수 있음:** 사용자의 로그온 여부에 상관없이 프로그램을 실행할 수 있도록 지정하는 옵션을 선택합니다.  
  
8.  **요구 사항** 페이지에서 **다음**을 선택하여 기본값을 수락한 후 마법사를 완료합니다.  
  
 다음 표에는 7단계에서 지정한 명령줄 옵션이 설명되어 있습니다.  
  
|옵션|설명|  
|--------|--------|  
|**\/q**|자동 모드를 설정합니다.  사용자 입력이 필요하지 않으며 아무런 출력도 표시되지 않습니다.|  
|**\/norestart**|설치 프로그램이 자동으로 재부팅하지 않도록 합니다.  이 옵션을 사용하는 경우 Configuration Manager는 컴퓨터 다시 시작을 처리해야 합니다.|  
|**\/chainingpackage** *PackageName*|연결을 수행하는 패키지의 이름을 지정합니다.  이 정보는 [Microsoft CEIP\(사용자 환경 개선 프로그램\)](http://go.microsoft.com/fwlink/p/?LinkId=248244)에 등록한 사용자에게 다른 설치 세션 정보와 함께 보고됩니다.  패키지 이름에 공백이 포함되어 있으면 **\/chainingpackage "Chaining Product"**와 같이 큰따옴표를 구분자로 사용합니다.|  
  
 위 단계를 통해 .NET Framework 4.5라는 이름의 패키지가 만들어집니다.  이 프로그램은 .NET Framework 4.5 자동 설치 프로그램을 배포합니다.  자동 설치에서 사용자는 설치 프로세스와 상호 작용하지 않으며 연결 응용 프로그램은 반환 코드를 캡처하고 재부팅을 처리해야 합니다. MSDN 라이브러리의 [설치 패키지에서 프로세스 진행 정보 가져오기](http://go.microsoft.com/fwlink/?LinkId=179606)를 참조하세요.  
  
<a name="select_dist_point"></a>   
### 배포 지점 선택  
 서버에서 클라이언트 컴퓨터에 패키지와 프로그램을 배포하려면 먼저 사이트 시스템을 배포 지점으로 지정한 다음 배포 지점에 패키지를 배포해야 합니다.  
  
 다음 단계에 따라 이전 섹션에서 만든 .NET Framework 4.5 패키지에 대한 배포 지점을 선택합니다.  
  
1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 선택합니다.  
  
2.  **소프트웨어 라이브러리** 작업 영역에서 **응용 프로그램 관리**를 확장한 후 **패키지**를 선택합니다.  
  
3.  패키지 목록에서 이전 섹션에서 만든 **.NET Framework 4.5** 패키지를 선택합니다.  
  
4.  **배포** 그룹의 **홈** 탭에서 **콘텐츠 배포**를 선택합니다.  
  
5.  **콘텐츠 배포 마법사**의 **일반** 탭에서 **다음**을 선택합니다.  
  
6.  마법사의 **콘텐츠 대상** 페이지에서 **추가**를 선택한 후 **배포 지점**을 선택합니다.  
  
7.  **배포 지점 추가** 대화 상자에서 패키지와 프로그램을 호스트하는 배포 지점을 선택한 후 **확인**을 선택합니다.  
  
8.  마법사에서 필요한 작업을 완료합니다.  
  
 이제 패키지에는 .NET Framework 4.5를 자동으로 배포하는 데 필요한 모든 정보가 포함됩니다.  패키지와 프로그램을 배포하기 전에 배포 지점에 .NET Framework 4.5가 설치되어 있는지 확인합니다. Configuration Manager 문서 라이브러리에서 [Configuration Manager의 콘텐츠 관리 작업 및 유지 관리](http://technet.microsoft.com/library/gg712694.aspx#BKMK_MonitorContent)의 "콘텐츠 모니터링" 섹션을 참조하세요.  
  
<a name="deploying_package"></a>   
### 패키지 배포  
 .NET Framework 4.5 패키지와 프로그램을 배포하려면  
  
1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 선택합니다.  
  
2.  **소프트웨어 라이브러리** 작업 영역에서 **응용 프로그램 관리**를 확장한 후 **패키지**를 선택합니다.  
  
3.  패키지 목록에서 **.NET Framework 4.5**로 명명하여 만든 패키지를 선택합니다.  
  
4.  **배포** 그룹의 **홈** 탭에서 **배포**를 선택합니다.  
  
5.  **소프트웨어 배포 마법사**의 **일반** 페이지에서 **찾아보기**를 선택한 후 앞서 만든 컬렉션을 선택합니다.  **다음**을 선택합니다.  
  
6.  마법사의 **콘텐츠** 페이지에서 소프트웨어를 배포하려는 시작 지점이 표시되는지 확인하고 **다음**을 선택합니다.  
  
7.  마법사의 **배포 설정** 페이지에서 **작업**이 **설치**로, **용도**가 **필수**로 설정되어 있는지 확인합니다.  이렇게 하면 소프트웨어 패키지가 대상으로 지정된 컴퓨터에 필수적으로 설치됩니다.  **다음**을 선택합니다.  
  
8.  마법사의 **일정** 페이지에서 .NET Framework를 설치하려는 시점을 지정합니다.  **새로 만들기**를 선택하여 설치 시간을 지정하거나, 사용자가 로그온하거나 로그오프할 때, 또는 최대한 빨리 소프트웨어를 설치하도록 지시할 수 있습니다.  **다음**을 선택합니다.  
  
9. 마법사의 **사용자 경험** 페이지에서 기본값을 사용하고 **다음**을 선택합니다.  
  
    > [!WARNING]
    >  프로덕션 환경에는 배포 일정에 대해 다른 선택 항목을 요구하는 정책이 있을 수도 있습니다.  이러한 옵션에 대한 자세한 내용은 TechNet 라이브러리의 [광고 이름 속성: 일정 탭](http://technet.microsoft.com/library/bb694016.aspx)을 참조하세요.  
  
10. 마법사의 **배포 지점** 페이지에서 기본값을 사용하고 **다음**을 선택합니다.  
  
11. 마법사에서 필요한 작업을 완료합니다.  **모니터링** 작업 영역의 **배포** 노드에서 배포의 진행 상태를 모니터링할 수 있습니다.  
  
 이제 패키지는 대상 컬렉션으로 배포되고 .NET Framework 4.5의 자동 설치가 시작됩니다.  .NET Framework 4.5 설치 오류 코드에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [반환 코드](#return_codes) 섹션을 참조하십시오.  
  
<a name="resources"></a>   
## 리소스  
 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 재배포 가능 패키지의 배포 테스트를 위한 인프라에 대한 자세한 내용은 다음 자료를 참조하십시오.  
  
 **Active Directory, DNS, DHCP**  
  
-   [Windows Server 2008용 Active Directory 도메인 서비스](http://technet.microsoft.com/library/dd378891.aspx)  
  
-   [소규모 네트워크의 DNS에 대한 Windows Server 2008 단계별 가이드](http://www.microsoft.com/download/details.aspx?id=17157)  
  
-   [DNS 서버](http://technet.microsoft.com/library/cc732997.aspx)  
  
-   [DHCP 서버](http://technet.microsoft.com/library/cc896553.aspx)  
  
 **SQL Server 2008**  
  
-   [SQL Server 2008 설치\(SQL Server 비디오\)](http://technet.microsoft.com/library/dd299415.aspx)  
  
-   [데이터베이스 관리자용 SQL Server 2008 보안 개요](http://download.microsoft.com/download/a/c/d/acd8e043-d69b-4f09-bc9e-4168b65aaa71/SQL2008SecurityOverviewforAdmins.docx)  
  
 **System Center 2012 Configuration Manager\(관리 지점, 배포 지점\):**  
  
-   [System Center 2012 Configuration Manager의 사이트 관리](http://technet.microsoft.com/library/gg681983.aspx)  
  
-   [Configuration Manager 단일 사이트 계획 및 배포](http://technet.microsoft.com/library/bb680961.aspx)  
  
 **Windows 컴퓨터용 System Center 2012 Configuration Manager 클라이언트:**  
  
-   [System Center 2012 Configuration Manager에서의 클라이언트 배포](http://technet.microsoft.com/library/gg699391.aspx)  
  
<a name="troubleshooting"></a>   
## 문제 해결  
  
### 로그 파일 위치  
 다음 로그 파일은 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 설치 중에 생성됩니다.  
  
 %temp%\\Microsoft .NET Framework 4.5\*.txt                                 
 %temp%\\Microsoft .NET Framework 4.5\*.html  
  
 [로그 수집 도구](http://www.microsoft.com/download/details.aspx?id=12493)를 사용하여 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 로그 파일을 수집하고 파일 크기를 줄여주는 압축된 캐비닛 파일\(.cab\)을 만들 수 있습니다.  
  
<a name="return_codes"></a>   
### 반환 코드  
 다음 표에서는 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 재배포 가능 설치 프로그램의 가장 일반적인 반환 코드를 보여 줍니다.  반환 코드는 설치 관리자 버전에 관계없이 모두 동일합니다.  
  
 자세한 정보에 대한 링크는 다음 섹션 [다운로드 오류 코드](#additional_error_codes)를 참조하십시오.  
  
|반환 코드|설명|  
|-----------|--------|  
|0|설치되었습니다.|  
|1602|사용자가 설치를 취소했습니다.|  
|1603|설치하는 동안 심각한 오류가 발생했습니다.|  
|1641|설치를 완료하려면 컴퓨터를 다시 시작해야 합니다.  이 메시지는 설치가 성공적으로 수행되었음을 의미합니다.|  
|3010|설치를 완료하려면 컴퓨터를 다시 시작해야 합니다.  이 메시지는 설치가 성공적으로 수행되었음을 의미합니다.|  
|5100|사용자 컴퓨터가 시스템 요구 사항을 충족하지 못합니다.|  
  
<a name="additional_error_codes"></a>   
### 다운로드 오류 코드  
  
-   [BITS\(Background Intelligent Transfer Service\) 오류 코드](http://msdn.microsoft.com/library/aa362823.aspx)  
  
-   [URL 모니커 오류 코드](http://msdn.microsoft.com/library/ms775145.aspx)  
  
-   [WinHttp 오류 코드](http://msdn.microsoft.com/library/aa383770.aspx)  
  
 기타 오류 코드  
  
-   [Windows Installer 오류 코드](http://msdn.microsoft.com/library/aa368542.aspx)  
  
-   [Windows 업데이트 에이전트 결과 코드](http://technet.microsoft.com/library/cc720442.aspx)  
  
## 참고 항목  
 [개발자를 위한 배포 가이드](../../../docs/framework/deployment/deployment-guide-for-developers.md)   
 [시스템 요구 사항](../../../docs/framework/get-started/system-requirements.md)