---
title: "기본적인 Windows Communication Foundation 개념 | Microsoft Docs"
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
helpviewer_keywords: 
  - "개념 [WCF]"
  - "기본 사항 [WCF]"
  - "WCF [WCF], 개념"
  - "Windows Communication Foundation [WCF], 개념"
ms.assetid: 3e7e0afd-7913-499d-bafb-eac7caacbc7a
caps.latest.revision: 39
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 39
---
# 기본적인 Windows Communication Foundation 개념
이 문서에서는 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 아키텍처에 대해 간략하게 설명합니다.또한 핵심 개념 및 이러한 개념이 서로 어떻게 연결되는지에 대해 설명합니다.가장 간단한 버전의 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 및 클라이언트를 만드는 방법에 대하 대한 자습서는 [초보자를 위한 자습서](../../../docs/framework/wcf/getting-started-tutorial.md)를 참조하십시오.[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 프로그래밍을 배우려면 [기본 WCF 프로그래밍](../../../docs/framework/wcf/basic-wcf-programming.md)을 참조하십시오.  
  
## WCF 기본 사항  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]는 서비스와 클라이언트 사이에서 메시지를 보내는 시스템을 만드는 런타임과 API 집합입니다.같은 컴퓨터 시스템에 있는 서로 다른 응용 프로그램 간의 통신이나 인터넷을 통해 액세스하는 다른 회사에 있는 시스템 간의 통신을 지원하는 응용 프로그램을 만들 때 동일한 인프라와 API가 사용됩니다.  
  
### 메시징 및 끝점  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]는 메시지 기반 통신과, 프로그래밍 모델에서 일관된 방식으로 표시할 수 있는 메시지\(예: HTTP 요청 또는 메시지 큐\(MSMQ라고도 함\) 메시지\)로 모델링할 수 있는 대상을 기반으로 합니다.따라서 서로 다른 여러 가지 전송 메커니즘 간에 통합된 API를 사용할 수 있습니다.  
  
 모델은 통신을 시작하는 응용 프로그램인 *클라이언트*와 클라이언트가 통신하기를 기다리다가 해당 통신에 응답하는 응용 프로그램인 *서비스*로 구분됩니다.단일 응용 프로그램이 클라이언트 및 서비스 모두로 작동할 수 있습니다.예제를 보려면 [이중 서비스](../../../docs/framework/wcf/feature-details/duplex-services.md) 및 [피어 투 피어 네트워킹](../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)을 참조하십시오.  
  
 메시지는 끝점 간에 전송됩니다.*끝점*은 메시지가 전송 및\/또는 수신되는 지점이며 메시지 교환에 필요한 모든 정보를 정의합니다.서비스는 하나 이상의 응용 프로그램 끝점\(및 0 이상의 인프라 끝점\)을 노출하고 클라이언트는 서비스 끝점 중 하나와 호환되는 끝점을 만듭니다.  
  
 *끝점*은 메시지가 전송되는 위치, 전송되는 방법 및 표시되는 메시지 모양을 표준 기반 방법으로 설명합니다.서비스는 해당 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 클라이언트 및 통신 *스택*을 만들기 위해 클라이언트가 처리할 수 있는 메타데이터로 이 정보를 노출할 수 있습니다.  
  
### 통신 프로토콜  
 통신 스택의 필수 요소 중 하나는 *전송 프로토콜*입니다.HTTP 및 TCP와 같은 일반적인 전송을 사용하여 인트라넷 및 인터넷을 통해 메시지를 전송할 수 있습니다.기타 전송으로는 피어 네트워킹 메시에서 메시지 큐 응용 프로그램과 노드의 통신을 지원하는 전송이 있습니다.추가 전송 메커니즘은 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]의 기본 제공 확장점을 사용하여 추가할 수 있습니다.  
  
 통신 스택에 필요한 다른 요소는 제공된 모든 메시지의 형식을 지정하는 방법을 지정하는 인코딩입니다.[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]는 다음 인코딩을 제공합니다.  
  
-   텍스트 인코딩, 상호 운용 가능한 인코딩.  
  
-   MTOM\(Message Transmission Optimization Mechanism\) 인코딩, 비구조적 이진 데이터를 서비스 간에 효율적으로 보내기 위한 상호 운용 가능한 방법입니다.  
  
-   효율적인 전송을 위한 이진 인코딩.  
  
 추가 인코딩 메커니즘\(예: 압축 인코딩\)은 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]의 기본 제공 확장점을 사용하여 추가할 수 있습니다.  
  
### 메시지 패턴  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]는 요청\-회신, 단방향 통신 및 이중 통신을 포함하여 여러 가지 메시징 패턴을 지원합니다.전송마다 서로 다른 메시징 패턴을 지원하기 때문에 지원하는 상호 작용 형식에 영향을 줍니다.또한 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] API 및 런타임은 메시지를 안전하고 안정적으로 보내는 데 도움을 줍니다.  
  
## WCF 용어  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 설명서에 사용되는 기타 개념 및 용어는 다음과 같습니다.  
  
 메시지  
 본문 및 헤더를 포함하여 여러 부분으로 구성될 수 있는 독립적인 데이터 단위입니다.  
  
 서비스  
 하나 이상의 끝점을 노출하는 구문이며 각 끝점은 하나 이상의 서비스 작업을 노출합니다.  
  
 끝점  
 메시지가 전송 및\/또는 수신되는 구문입니다.끝점은 메시지가 전송될 수 있는 장소를 정의하는 위치\(주소\), 메시지가 전송되는 방법을 설명하는 통신 메커니즘의 사양\(바인딩\) 및 전송될 수 있는 메시지를 설명하는 위치에서 전송 및\/또는 수신될 수 있는 메시지 집합의 정의\(서비스 계약\)로 구성됩니다.  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스는 끝점 컬렉션으로 전역에 노출됩니다.  
  
 응용 프로그램 끝점  
 응용 프로그램에 의해 노출된 끝점이며 응용 프로그램이 구현하는 서비스 계약에 해당합니다.  
  
 인프라 끝점  
 필요한 기능을 활용하기 위해 인프라에 의해 노출되거나 서비스 계약과 관련 없는 서비스에 의해 제공되는 끝점입니다.예를 들어, 서비스에는 메타데이터 정보를 제공하는 인프라 끝점이 포함될 수 있습니다.  
  
 주소  
 메시지가 수신될 위치를 지정하며,URI\(Uniform Resource Identifier\)로 지정됩니다.URI 스키마 부분은 HTTP 및 TCP와 같은 주소에 도달하는 데 사용할 전송 메커니즘 이름을 지정합니다.URI의 계층적 부분에는 전송 메커니즘에 따라 다른 고유한 위치 형식이 포함됩니다.  
  
 끝점 주소를 사용하면 서비스의 각 끝점마다 고유한 끝점 주소를 만들거나 특정한 조건으로 여러 끝점 간에 주소를 공유할 수 있습니다.다음 예제에서는 기본 이외의 포트를 가진 HTTPS 프로토콜을 사용하는 주소를 보여 줍니다.  
  
```  
HTTPS://cohowinery:8005/ServiceModelSamples/CalculatorService  
```  
  
 바인딩  
 끝점이 전역에서 통신하는 방법을 정의합니다.통신 인프라를 만들기 위해 다른 요소의 맨 위에서 요소를 "스택"하는 바인딩 요소라는 구성 요소 집합으로 생성됩니다.최소한 바인딩은 사용할 전송\(예: HTTP 또는 TCP\) 및 인코딩\(예: 텍스트 또는 이진\)을 정의합니다.바인딩은 메시지 보안을 위해 사용되는 보안 메커니즘 또는 끝점에서 사용하는 메시지 패턴과 같은 세부 사항을 지정하는 바인딩 요소를 포함할 수 있습니다.자세한 내용은 [서비스 구성](../../../docs/framework/wcf/configuring-services.md)을 참조하십시오.  
  
 바인딩 요소  
 전송, 인코딩, 인프라 수준 프로토콜의 구현\(예: WS\-ReliableMessaging\) 또는 통신 스택의 기타 모든 구성 요소와 같이 바인딩의 특정 부분을 나타냅니다.  
  
 동작  
 서비스, 끝점, 특정 작업 또는 클라이언트의 다양한 런타임 측면을 제어하는 구성 요소입니다.동작은 범위에 따라 그룹화됩니다. 일반 동작은 모든 끝점에 전역적으로 영향을 주고 서비스 동작은 서비스 관련 측면에만 영향을 주며, 끝점 동작은 끝점 관련 속성에만 영향을 주고 작업 수준 동작은 특정 작업에 영향을 줍니다.예를 들어, 서비스 동작이 스로틀인 경우에는 메시지가 처리 가능한 양을 초과할 때 서비스에서 어떻게 대응할지를 지정합니다.반면에 끝점 동작은 보안 자격 증명을 찾는 방법 및 위치와 같이 끝점과 관련된 측면만 제어합니다.  
  
 시스템 제공 바인딩  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]에는 다양한 시스템 제공 바인딩이 포함되어 있습니다.이러한 바인딩은 특정 시나리오에 맞게 최적화된 바인딩 요소의 컬렉션입니다.예를 들어, <xref:System.ServiceModel.WSHttpBinding>은 다양한 WS\-\* 사양을 구현하는 서비스와 상호 운용하기 위해 디자인되었습니다.이렇게 미리 정의된 바인딩은 특정 시나리오에 제대로 적용될 수 있는 옵션만 제공하기 때문에 시간이 절약됩니다.미리 정의된 바인딩이 요구 사항을 충족하지 않을 경우 사용자 지정 바인딩을 만들 수 있습니다.  
  
 구성 및 코딩  
 코딩이나 구성을 사용하여, 또는 두 가지를 모두 사용하여 응용 프로그램을 제어할 수 있습니다.구성은 개발자 이외의 다른 담당자\(예: 네트워크 관리자\)가 코드를 기록한 후 다시 컴파일할 필요 없이 클라이언트 및 서비스 매개 변수를 설정할 수 있는 이점이 있습니다.구성을 사용하면 끝점 주소와 같은 값을 설정할 수 있을 뿐만 아니라 끝점, 바인딩 및 동작을 추가하여 보다 세부적인 제어를 수행할 수 있습니다.코딩은 개발자가 서비스 또는 클라이언트의 모든 구성 요소에 대해 엄격한 제어를 유지할 수 있도록 하며, 구성을 통해 수행된 모든 설정을 검사하고 필요한 경우 코드를 통해 재지정할 수 있습니다.  
  
 서비스 작업  
 작업의 기능을 구현하는 서비스 코드에서 정의된 프로시저입니다.이 작업은 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 클라이언트에서 메서드로 클라이언트에 노출됩니다.메서드는 값을 반환하고 선택적 인수 개수를 가져오거나, 인수를 가져오지 않고 응답을 반환하지 않을 수 있습니다.예를 들어, 간단한 "Hello"로 기능하는 작업을 클라이언트의 존재에 대한 알림으로 사용하고 일련의 작업을 시작할 수 있습니다.  
  
 서비스 계약  
 서로 연관된 여러 작업을 하나의 기능 단위로 묶습니다.계약은 서비스의 네임스페이스, 해당 콜백 계약 및 기타 설정과 같은 서비스 수준 설정을 정의할 수 있습니다.대부분의 경우 계약은 선택한 프로그래밍 언어로 인터페이스를 만들고 <xref:System.ServiceModel.ServiceContractAttribute> 특성을 인터페이스에 적용하여 정의합니다.실제 서비스 코드는 인터페이스를 구현한 결과입니다.  
  
 작업 계약  
 작업 계약은 매개 변수를 정의하고 작업 형식을 반환합니다.서비스 계약을 정의하는 인터페이스를 만드는 경우 <xref:System.ServiceModel.OperationContractAttribute> 특성을 계약의 일부인 각 메서드 정의에 적용하여 작업 계약을 나타냅니다.작업은 단일 메시지를 가져오고 단일 메시지를 반환하거나 형식 집합을 가져오고 형식을 반환하는 방법으로 모델링할 수 있습니다.후자의 경우 시스템에서 해당 작업에 대해 교환해야 하는 메시지 형식을 결정합니다.  
  
 메시지 계약  
 메시지 형식을 설명합니다.예를 들어, 메시지 요소가 헤더 또는 해당 본문에 삽입되어야 할지 여부, 메시지 요소에 적용되어야 하는 보안 수준 등을 선언합니다.  
  
 오류 계약  
 서비스 작업과 연결하여 호출자에게 반환될 수 있는 오류를 나타낼 수 있습니다.작업에는 작업과 관련된 오류가 0개 이상 포함될 수 있습니다.이러한 오류는 프로그래밍 모델에서 예외로 모델링된 SOAP 오류입니다.  
  
 데이터 계약  
 서비스가 사용하는 데이터 형식에 대한 설명으로, 메타데이터에 포함되어 있습니다.이 설명을 통해 해당 서비스를 다른 서비스와 상호 운용할 수 있습니다.데이터 형식은 매개 변수, 반환 형식 등으로 메시지의 모든 부분에서 사용될 수 있습니다.서비스가 간단한 형식만 사용하는 경우 명시적으로 데이터 계약을 사용할 필요가 없습니다.  
  
 호스팅  
 일부 프로세스의 경우 서비스를 호스팅해야 합니다.*호스트*는 서비스 수명을 제어하는 응용 프로그램입니다.서비스는 기존 호스팅 프로세스에 의해 자체 호스팅되거나 관리될 수 있습니다.  
  
 자체 호스팅 서비스  
 개발자가 만든 프로세스 응용 프로그램 내에서 실행되는 서비스입니다.개발자는 수명을 제어하고 서비스 속성을 설정하며 서비스를 열고\(수신 대기 모드로 설정된 경우\) 서비스를 닫습니다.  
  
 호스팅 프로세스  
 서비스를 호스팅하기 위해 디자인된 응용 프로그램입니다.여기에는 IIS\(인터넷 정보 서비스\), WAS\(Windows Activation Services\) 및 Windows Services가 있습니다.이러한 호스팅된 시나리오에서 호스트는 서비스 수명을 제어합니다.예를 들어, IIS를 사용하는 경우 서비스 어셈블리 및 구성 파일이 포함된 가상 디렉터리를 설정할 수 있습니다.메시지를 수신하면 IIS는 서비스를 시작하고 수명을 제어합니다.  
  
 인스턴스 만들기  
 서비스에는 인스턴스 만들기 모델이 포함되어 있습니다.인스턴스 만들기 모델에는 세 가지가 있습니다. 즉, 단일 CLR 개체가 모든 클라이언트에 서비스를 제공하는 "단일" 모델, 각 클라이언트 호출을 처리하기 위해 새로운 CLR 개체를 만드는 "호출별" 모델 및 각 개별 세션에 대해 CLR 개체 집합을 만드는 "세션별" 모델입니다.인스턴스 만들기 모델은 응용 프로그램 요구 사항 및 예상되는 서비스 사용 패턴에 따라 선택합니다.  
  
 클라이언트 응용 프로그램  
 메시지를 하나 이상의 끝점과 교환하는 프로그램입니다.클라이언트 응용 프로그램은 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 클라이언트의 인스턴스를 만들고 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 클라이언트의 메서드를 호출하여 시작합니다.하나의 응용 프로그램이 클라이언트 및 서비스 역할을 모두 수행할 수 있다는 점에 주의하십시오.  
  
 채널  
 바인딩 요소의 구체적인 구현입니다.바인딩은 구성을 나타내고 채널은 해당 구성과 관련된 구현입니다.따라서 각 바인딩 요소마다 관련된 채널이 있습니다.채널은 다른 채널 맨 위에 스택되어 바인딩의 구체적인 구현인 채널 스택을 만듭니다.  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 클라이언트  
 서비스 작업을 메서드로 노출하는 클라이언트 응용 프로그램 구문입니다\(Visual Basic 또는 Visual C\#와 같이 선택한 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 프로그래밍 언어로 표시\).모든 응용 프로그램은 서비스를 호스팅하는 응용 프로그램을 포함하여 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 클라이언트를 호스팅할 수 있습니다.따라서 다른 서비스의 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 클라이언트를 포함하는 서비스를 만들 수 있습니다.  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 클라이언트는 [ServiceModel Metadata 유틸리티 도구\(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)를 사용하고 메타데이터를 게시하는 실행 중인 서비스에서 선택하여 자동으로 만들 수 있습니다.  
  
 메타데이터  
 서비스에서 서비스와 통신하기 위해 외부 엔터티가 이해해야 하는 서비스 특성을 설명합니다.메타데이터는 [ServiceModel Metadata 유틸리티 도구\(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)에서 사용하여 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 클라이언트 및 서비스와 상호 작용하기 위해 클라이언트 응용 프로그램이 사용할 수 있는 함께 수반된 구성을 생성할 수 있습니다.  
  
 서비스에 의해 노출된 메타데이터에는 서비스의 데이터 계약을 정의한 XML 스키마 문서와 서비스의 메서드를 설명하는 WSDL 문서가 포함되어 있습니다.  
  
 사용할 경우 서비스와 끝점을 검사하여 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]에 의해 서비스 메타데이터가 자동으로 생성됩니다.서비스에서 메타데이터를 게시하려면 명시적으로 메타데이터 동작을 사용해야 합니다.  
  
 보안  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]에서는 기밀성\(도청을 방지하기 위해 메시지 암호화\), 무결성\(메시지 변조를 감지하기 위한 방법\), 인증\(서버 및 클라이언트의 유효성 검사를 위한 방법\) 및 권한 부여\(리소스 액세스 권한 제어\)가 포함됩니다.이러한 기능은 HTTP를 통한 TLS\(HTTPS라고도 함\)와 같이 기존 보안 메커니즘을 활용하거나 다양한 WS\-\* 보안 사양 중 하나 이상을 구현하여 제공합니다.  
  
 전송 보안 모드  
 전송 계층 메커니즘\(예: HTTPS\)에 의해 제공되는 기밀성, 무결성 및 인증을 지정합니다.HTTPS와 같은 전송을 사용하면 이 모드는 성능이 효율적이며 인터넷에서 널리 사용되기 때문에 이해하기 쉽습니다.단점은 이러한 종류의 보안이 통신 경로의 각 홉에서 개별적으로 적용되기 때문에 통신이 "메시지 가로채기\(man in the middle\)" 공격을 받기 쉽습니다.  
  
 메시지 보안 모드  
 [Web Services Security: SOAP Message Security](http://go.microsoft.com/fwlink/?LinkId=94684) 사양과 같은 하나 이상의 보안 사양을 구현하여 보안을 제공하도록 지정합니다.각 메시지에는 전송 중에 보안을 제공하고 수신자가 변조를 감지하거나 메시지를 해독하는 데 필요한 메커니즘이 포함되어 있습니다.따라서 보안은 모든 메시지 내에 캡슐화되어 여러 홉 전반에 걸쳐 종단 간 보안을 제공합니다.보안 정보가 메시지의 일부이기 때문에 여러 종류의 자격 증명을 메시지에 포함시킬 수도 있습니다. 이러한 자격 증명을 *클레임*이라고 합니다.또한 이러한 접근 방식은 원본 및 대상 간 여러 전송을 포함하여 메시지가 전송을 통해 안전하게 전달될 수 있는 이점이 있습니다.그러나 관련 암호화 메커니즘이 복잡하기 때문에 성능이 떨어질 수 있다는 단점이 있습니다.  
  
 메시지 자격 증명을 사용한 전송 보안 모드  
 전송 계층을 사용하여 메시지 기밀성, 인증 및 무결성을 제공하도록 지정합니다. 각 메시지에는 메시지 수신자에게 필요한 여러 자격 증명\(클레임\)이 포함될 수 있습니다.  
  
 WS\-\*  
 WS\-Security, WS\-ReliableMessaging 등과 같이 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]에서 구현되고 계속 업데이트되는 WS\(웹 서비스\) 사양 집합의 약어입니다.  
  
## 참고 항목  
 [Windows Communication Foundation 정의](../../../docs/framework/wcf/whats-wcf.md)   
 [Windows Communication Foundation 아키텍처](../../../docs/framework/wcf/architecture.md)   
 [Security Architecture](http://msdn.microsoft.com/ko-kr/16593476-d36a-408d-808c-ae6fd483e28f)