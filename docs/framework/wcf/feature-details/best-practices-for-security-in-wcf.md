---
title: "WCF 보안을 위한 최선의 방법 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "최선의 방법 [WCF], 보안"
ms.assetid: 3639de41-1fa7-4875-a1d7-f393e4c8bd69
caps.latest.revision: 19
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 19
---
# WCF 보안을 위한 최선의 방법
다음 단원에는 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]를 사용하여 보안 응용 프로그램을 만들 때 고려할 최선의 방법이 나열되어 있습니다.보안[!INCLUDE[crabout](../../../../includes/crabout-md.md)][보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md), [데이터에 대한 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md) 및 [메타데이터 관련 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-with-metadata.md)을 참조하십시오.  
  
## SPN을 사용하여 Windows 인증을 수행하는 서비스 식별  
 UPN\(User Principal Name\) 또는 SPN\(서비스 사용자 이름\)을 사용하여 서비스를 식별할 수 있습니다.네트워크 서비스와 같은 컴퓨터 계정으로 실행되는 서비스에는 실행 중인 컴퓨터에 해당하는 SPN ID가 있습니다.사용자 계정으로 실행되는 서비스에는 실행 중인 사용자에 해당하는 UPN ID가 있지만 `setspn` 도구를 사용하여 사용자 계정에 SPN을 할당할 수 있습니다.SPN을 통해 식별될 수 있도록 서비스를 구성하고 서비스에 연결하는 클라이언트가 SPN을 사용하도록 구성하면 특정 공격이 발생할 가능성이 줄어듭니다.이 지침은 Kerberos 또는 SSPI 협상을 사용하는 바인딩에 적용됩니다.클라이언트는 SSPI가 NTLM으로 대체되는 경우에 대비해 SPN을 계속 지정해야 합니다.  
  
## WSDL에서 서비스 ID 확인  
 WS\-SecurityPolicy를 사용하면 서비스가 자체 ID에 대한 정보를 메타데이터로 게시할 수 있습니다.`svcutil` 또는 <xref:System.ServiceModel.Description.WsdlImporter>와 같은 다른 메서드를 통해 가져오면 이러한 ID 정보는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스 끝점 주소의 ID 속성으로 변환됩니다.이러한 서비스 ID가 정확하며 유효한지 확인하지 않는 클라이언트는 사실상 서비스 인증을 건너뛰게 됩니다.이러한 클라이언트를 악의적인 서비스가 악용하여 WSDL의 클레임 ID를 변경하는 방법으로 자격 증명 전달 및 기타 "메시지 가로채기\(man\-in\-the\-middle\)" 공격을 실행할 수 있습니다.  
  
## NTLM 대신 X509 인증서 사용  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 피어 투 피어 인증을 위해 X509 인증서\(피어 채널에 사용됨\)와 Windows 인증\(SSPI 협상이 Kerberos에서 NTLM으로 다운그레이드됨\)이라는 두 가지 메커니즘을 제공합니다.다음과 같은 여러 가지 이유로 인해 NTLM 대신 1024비트 이상의 키를 사용하는 인증서 기반 인증을 사용하는 것이 좋습니다.  
  
-   상호 인증의 사용 가능성  
  
-   보다 강력한 암호화 알고리즘의 사용  
  
-   전달된 X509 자격 증명을 활용하는 작업의 어려움  
  
 NTLM 전달 공격에 대한 개요를 보려면 [http:\/\/msdn.microsoft.com\/msdnmag\/issues\/06\/09\/SecureByDesign\/default.aspx](http://go.microsoft.com/fwlink/?LinkId=109571)로 이동하십시오.  
  
## 가장 후 항상 되돌리기  
 클라이언트의 가장을 사용하도록 설정한 API를 사용하는 경우, 원래 ID로 되돌려야 합니다.예를 들어 <xref:System.Security.Principal.WindowsIdentity> 및 <xref:System.Security.Principal.WindowsImpersonationContext>를 사용하는 경우에는 다음 코드에서처럼 C\# `using` 문 또는 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]`Using` 문을 사용합니다.<xref:System.Security.Principal.WindowsImpersonationContext> 클래스는 <xref:System.IDisposable> 인터페이스를 구현하므로 코드가 `using` 블록을 벗어나면 CLR\(공용 언어 런타임\)은 원래 ID로 자동으로 되돌아갑니다.  
  
 [!code-csharp[c_SecurityBestPractices#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securitybestpractices/cs/source.cs#1)]
 [!code-vb[c_SecurityBestPractices#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securitybestpractices/vb/source.vb#1)]  
  
## 필요할 때만 가장  
 <xref:System.Security.Principal.WindowsIdentity> 클래스의 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A> 메서드를 사용하면 매우 제어된 범위에서 가장을 사용할 수 있습니다.이는 전체 작업의 범위에 대해 가장을 허용하는 <xref:System.ServiceModel.OperationBehaviorAttribute>의 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> 속성을 사용하는 것과 대조됩니다.가능하면 보다 정확한 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A> 메서드를 사용하여 가장 범위를 제어합니다.  
  
## 신뢰할 수 있는 소스에서 메타데이터 가져오기  
 메타데이터의 원본을 신뢰할 수 있는지, 다른 사람이 메타데이터를 훼손하지는 않았는지 확인합니다.HTTP 프로토콜을 사용하여 검색한 메타데이터는 일반 텍스트로 전송되며 변경할 수 있습니다.서비스가 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> 및 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A> 속성을 사용하는 경우 서비스 작성자가 제공하는 URL을 통해 HTTPS 프로토콜을 사용하여 데이터를 다운로드합니다.  
  
## 보안을 사용하여 메타데이터 게시  
 서비스의 게시된 메타데이터가 훼손되지 않게 하려면 전송 또는 메시지 수준 보안을 사용하여 메타데이터 교환 끝점의 보안을 설정합니다.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][메타데이터 끝점 게시](../../../../docs/framework/wcf/publishing-metadata-endpoints.md) 및 [방법: 코드를 사용하여 서비스에 대한 메타데이터 게시](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md).  
  
## 로컬 발급자 사용  
 지정된 바인딩에 발급자 주소와 바인딩을 지정하면 해당 바인딩을 사용하는 끝점에는 로컬 발급자가 사용되지 않습니다.로컬 발급자를 항상 사용해야 하는 클라이언트는 이러한 바인딩을 사용하지 않도록 하거나 발급자 주소가 null이 되도록 바인딩을 수정해야 합니다.  
  
## SAML 토큰 크기 할당량  
 SAML\(Security Assertions Markup Language\) 토큰이 메시지에 serialize될 때 STS\(보안 토큰 서비스\)에서 해당 토큰을 발급하거나 클라이언트에서 인증의 일부로 해당 토큰을 서비스에 제공하는 경우, 최대 메시지 크기 할당량은 SAML 토큰 및 다른 메시지 부분을 수용할 수 있도록 충분히 커야 합니다.일반적으로 기본 메시지 크기 할당량이면 충분합니다.그러나 SAML 토큰에 수백 개의 클레임이 포함되어 있어 SAML 토큰이 큰 경우에는 serialize된 토큰을 수용할 수 있도록 할당량을 늘려야 합니다.할당량에 대한 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]는 [데이터에 대한 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)을 참조하십시오.  
  
## 사용자 지정 바인딩에서 SecurityBindingElement.IncludeTimestamp를 True로 설정  
 사용자 지정 바인딩을 만들 때는 <xref:System.ServiceModel.Channels.SecurityBindingElement.IncludeTimestamp%2A>를 `true`로 설정해야 합니다.그렇지 않을 경우 <xref:System.ServiceModel.Channels.SecurityBindingElement.IncludeTimestamp%2A>가 `false`로 설정되어 있고 클라이언트가 X509 인증서와 같은 비동기 키 기반 토큰을 사용하는 경우 메시지가 서명되지 않습니다.  
  
## 참고 항목  
 [보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [데이터에 대한 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)   
 [메타데이터 관련 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-with-metadata.md)