---
title: "XSLT 매개 변수 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: fe60aaa0-ae43-4b1c-9be1-426af66ba757
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# XSLT 매개 변수
<xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 메서드를 사용하여 <xref:System.Xml.Xsl.XsltArgumentList>에 XSLT 매개 변수를 추가합니다.  이 때 정규화된 이름 및 네임스페이스 URI가 매개 변수 개체와 연결됩니다.  
  
### XSLT 매개 변수를 사용하려면  
  
1.  <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 메서드를 사용하여 <xref:System.Xml.Xsl.XsltArgumentList> 개체를 만들고 매개 변수를 추가합니다.  
  
2.  스타일시트에서 매개 변수를 호출합니다.  
  
3.  <xref:System.Xml.Xsl.XsltArgumentList> 개체를 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드에 전달합니다.  
  
## 매개 변수 형식  
 매개 변수 개체는 W3C 형식과 일치해야 합니다.  다음 표에서는 해당 W3C 형식, 해당 Microsoft .NET 클래스\(형식\) 및 W3C 형식이 XPath 형식인지 또는 XSLT 형식인지를 보여 줍니다.  
  
|W3C 형식|해당 .NET 클래스\(형식\)|XPath 또는 XSLT 형식|  
|------------|-----------------------|----------------------|  
|`String`|<xref:System.String?displayProperty=fullName>|XPath|  
|`Boolean`|<xref:System.Boolean?displayProperty=fullName>|XPath|  
|`Number`|<xref:System.Double?displayProperty=fullName>|XPath|  
|`Result Tree Fragment`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|XSLT|  
|`Node*`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|XPath|  
|`Node Set`|<xref:System.Xml.XPath.XPathNodeIterator><br /><br /> **XPathNavigator\[\]**|XPath|  
  
 \*단일 노드가 포함된 노드 집합과 같습니다.  
  
 매개 변수 개체가 위 클래스에 해당하지 않으면 다음 규칙에 따라 변환됩니다.  CLR\(공용 언어 런타임\) 숫자 형식은 <xref:System.Double>로 변환됩니다.  <xref:System.DateTime> 형식은 <xref:System.String>으로 변환되고,  <xref:System.Xml.XPath.IXPathNavigable> 형식은 <xref:System.Xml.XPath.XPathNavigator>로 변환됩니다.  **XPathNavigator\[\]**는 <xref:System.Xml.XPath.XPathNodeIterator>로 변환됩니다.  
  
 다른 모든 형식은 오류를 throw합니다.  
  
## 예제  
 다음 예제에서는 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 메서드를 사용하여 계산된 할인 기간을 유지하는 매개 변수를 만듭니다.  할인 기간은 주문 날짜로부터 20일 동안으로 계산됩니다.  
  
 [!code-csharp[XSLT_Param#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_Param/CS/xsltparam.cs#1)]
 [!code-vb[XSLT_Param#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_Param/VB/xsltparam.vb#1)]  
  
### 입력  
  
##### order.xml  
 [!code-xml[XSLT_Param#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/order.xml#2)]  
  
##### discount.xsl  
 [!code-xml[XSLT_Param#3](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/discount.xsl#3)]  
  
### 출력  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<order>  
  <total>36.9</total>  
     15% discount if paid by: 2/4/2004 12:00:00 AM  
</order>  
```  
  
## 참고 항목  
 [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)