---
title: "방법: XmlSerializer를 사용하여 WCF 클라이언트 응용 프로그램의 시작 시간 개선 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21093451-0bc3-4b1a-9a9d-05f7f71fa7d0
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 방법: XmlSerializer를 사용하여 WCF 클라이언트 응용 프로그램의 시작 시간 개선
<xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize할 수 있는 데이터 형식을 사용하는 서비스 및 클라이언트 응용 프로그램은 런타임에 해당 데이터 형식에 대한 serialization 코드를 생성하고 컴파일합니다. 이로 인해 시작 시 성능이 저하될 수 있습니다.  
  
> [!NOTE]
>  미리 생성된 serialization 코드는 서비스가 아닌 클라이언트 응용 프로그램에서만 사용될 수 있습니다.  
  
 [ServiceModel Metadata 유틸리티 도구\(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)를 사용하면 응용 프로그램에 대해 컴파일된 어셈블리로부터 필요한 serialization 코드를 생성하여 이러한 응용 프로그램의 시작 성능을 향상시킬 수 있습니다.Svcutil.exe는 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize될 수 있는 컴파일된 응용 프로그램 어셈블리에서 서비스 계약에 사용하는 모든 데이터 형식에 대한 serialization 코드를 생성합니다.<xref:System.Xml.Serialization.XmlSerializer>를 사용하는 서비스 및 작업 계약은 <xref:System.ServiceModel.XmlSerializerFormatAttribute>와 함께 표시됩니다.  
  
### XmlSerializer serialization 코드를 생성하려면  
  
1.  서비스 또는 클라이언트 코드를 하나 이상의 어셈블리로 컴파일합니다.  
  
2.  SDK 명령 프롬프트를 엽니다.  
  
3.  명령 프롬프트에서 다음 형식을 사용하여 Svcutil.exe 도구를 실행합니다.  
  
    ```  
    svcutil.exe /t:xmlSerializer  <assemblyPath>*  
    ```  
  
     `assemblyPath` 인수는 서비스 계약 형식이 포함된 어셈블리의 경로를 지정합니다.Svcutil.exe는 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize될 수 있는 컴파일된 응용 프로그램 어셈블리에서 서비스 계약에 사용하는 모든 데이터 형식에 대한 serialization 코드를 생성합니다.  
  
     Svcutil.exe는 C\# serialization 코드만 생성할 수 있습니다.각 입력 어셈블리에 대해서 하나의 소스 코드 파일이 생성됩니다.생성된 코드의 언어를 **\/language** 스위치를 사용해서 변경할 수 없습니다.  
  
     종속 어셈블리의 경로를 지정하려면 **\/reference** 옵션을 사용합니다.  
  
4.  다음 옵션 중 하나를 사용하여 생성된 serialization 코드를 응용 프로그램에서 사용할 수 있도록 합니다.  
  
    1.  생성된 serialization 코드를 이름이 \[*original assembly*\].XmlSerializers.dll\(예: MyApp.XmlSerializers.dll\)인 별도의 어셈블리로 컴파일합니다.응용 프로그램에서 어셈블리를 로드할 수 있어야 하며, 해당 어셈블리는 원본 어셈블리와 동일한 키로 서명되어야 합니다.원본 어셈블리를 다시 컴파일하면 serialization 어셈블리도 다시 생성해야 합니다.  
  
    2.  생성된 serialization 코드를 별도의 어셈블리로 컴파일하고 <xref:System.ServiceModel.XmlSerializerFormatAttribute>를 사용하는 서비스 계약에 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute>를 사용합니다.컴파일된 serialization 어셈블리를 가리키기 위해 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> 또는 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A> 속성을 설정합니다.  
  
    3.  생성된 serialization 코드를 응용 프로그램 어셈블리로 컴파일하고 <xref:System.ServiceModel.XmlSerializerFormatAttribute>를 사용하는 서비스 계약에 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute>를 추가합니다.<xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> 또는 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A> 속성은 설정하지 마십시오.기본 serialization 어셈블리가 현재 어셈블리로 간주됩니다.  
  
## 예제  
 다음 명령은 어셈블리의 모든 서비스 계약이 사용하는 `XmlSerializer` 형식에 대해 serialization 형식을 생성합니다.  
  
```  
svcutil /t:xmlserializer myContractLibrary.exe  
```  
  
## 참고 항목  
 [ServiceModel Metadata 유틸리티 도구\(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)