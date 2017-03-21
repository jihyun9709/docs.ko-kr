---
title: "개념 및 용어 (함수 변환) (Visual Basic) | Microsoft 문서"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 24fd244d-ebae-4721-8858-89bb544aea0b
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9c4716765199798e50c4318b290f8a2d76ef5841
ms.lasthandoff: 03/13/2017


---
# <a name="concepts-and-terminology-functional-transformation-visual-basic"></a>개념 및 용어 (함수 변환) (Visual Basic)
이 항목에서는 순수 함수 변형의 개념과 용어에 대해 소개합니다. 데이터 변환에 대한 함수 변환 방법은 전통적인 명령형 프로그래밍보다 신속하게 프로그래밍할 수 있고 표현이 다양하며 디버깅과 유지 관리가 쉬운 코드를 생성합니다.  
  
 이 단원의 항목에서는 함수형 프로그래밍에 대해 전체적으로 설명하지 않고 XML의 모양을 쉽게 변환하는 데 사용할 수 있는 몇 가지 함수형 프로그래밍 기능만 살펴봅니다.  
  
## <a name="what-is-pure-functional-transformation"></a>순수 함수 변형이란?  
 *순수 함수 변환*, 호출 된 함수 집합 *순수 함수*을 원래 형태에서 구조화 된 데이터 집합을 다른 형식으로 변환 하는 방법을 정의 합니다. "순수" 라는 단어는 함수는 나타냅니다 *구성 가능한*, 이들이 필요:  
  
-   *자체 포함 된*는 자유롭게 정렬 하 고 프로그램의 나머지 부분과 상호 종속 되거나 얽 없이 다시 정렬할 수 있습니다. 순수 변형은 환경에 대한 지식이 없고 환경에 영향을 미치지 않습니다. 즉, 변환에 사용 되는 함수가 없는 *부작용*합니다.  
  
-   *상태 비저장*항상 같은 결과가 발생 합니다 동일한 입력에 대해 동일한 함수나 특정 함수 집합을 실행 되도록 합니다. 순수 변형은 이전 사용에 대한 기록을 갖고 있지 않습니다.  
  
> [!IMPORTANT]
>  이 자습서의 나머지 부분에서 "순수 함수"라는 용어는 특정 언어 기능이 아니라 프로그래밍 방법을 나타내기 위해 일반적인 의미에서 사용되었습니다.  
>   
>  참고 Visual Basic에서는 함수로로 순수 함수를 구현 되어야 합니다.  
>   
>  또한 순수 함수와 C++의 순수 가상 메서드를 혼동하면 안 됩니다. 순수 가상 메서드의 경우 포함하는 클래스가 추상 클래스이고 메서드 본문이 제공되지 않습니다.  
  
### <a name="functional-programming"></a>함수형 프로그래밍  
 *함수형 프로그래밍* 은 순수 함수 변환을 직접 지 원하는 프로그래밍 방법입니다.  
  
 지금까지 기계 학습, Scheme, Haskell 및 F #와 같은 범용 함수형 프로그래밍 언어는 주로 학계 관심의 되었습니다. 항상 Visual Basic의 순수 함수 변환을 작성할 수 있었지만의 어려움 때문 하므로 없는 것에 대부분의 프로그래머가 쉽게 선택할 수 없었습니다. 그러나 이후 버전의 Visual Basic, 새로운 언어와 같은 구문이 람다 식 및 형식 유추를 사용 하면 함수형 프로그래밍 훨씬 쉽고 생산적입니다.  
  
 함수형 프로그래밍에 대 한 자세한 내용은 참조 [vs 함수형 프로그래밍 합니다. 명령형 프로그래밍 비교 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md)합니다.  
  
#### <a name="domain-specific-fp-languages"></a>영역별 FP 언어  
 범용 프로그래밍 언어가 널리 채택되지는 않았지만 특정 영역별 함수형 프로그래밍 언어는 보다 성공적이었습니다. 예를 들어, CSS 스타일시트는 많은 웹 페이지의 모양과 느낌을 결정하는 데 사용되고 XSLT(Extensible Stylesheet Language Transformation) 스타일시트는 XML 데이터 조작에서 광범위하게 사용됩니다. XSLT에 대 한 자세한 내용은 참조 [XSLT 변환을](http://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03)합니다.  
  
## <a name="terminology"></a>용어  
 다음 표에는 함수 변환과 관련된 몇 가지 용어가 정의되어 있습니다.  
  
 고차(1급) 함수  
 프로그램 개체로 취급할 수 있는 함수입니다. 예를 들어, 고차 함수는 다른 함수로 전달되거나 다른 함수에서 반환될 수 있습니다. Visual Basic의 경우 대리자와 람다 식은 지 더 높은 순서 기능을 지 원하는 언어 기능. 고차 함수를 작성하려면 하나 이상의 인수를 선언하여 대리자를 사용하며, 고차 함수를 호출할 때는 흔히 람다 식을 사용합니다. 대부분의 표준 쿼리 연산자가 고차 함수입니다.  
  
 자세한 내용은 참조 [표준 쿼리 연산자 개요 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)합니다.  
  
 람다 식  
 대리자 형식이 예상되는 곳에서 항상 사용할 수 있는 인라인 익명 함수입니다. 이는 람다 식에 대한 간략한 정의이지만 이 자습서의 목적에 적합합니다.  
  
 에 대 한 자세한 내용은 참조 [람다 식](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)합니다.  
  
 컬렉션  
 대개 동일한 형식을 갖고 있는 구조화된 데이터 집합입니다. LINQ와 호환 되도록 컬렉션을 구현 해야는 <xref:System.Collections.IEnumerable>인터페이스 또는 <xref:System.Linq.IQueryable>인터페이스 (또는 해당 제네릭 요소 중 하나 <xref:System.Collections.Generic.IEnumerator%601>또는 <xref:System.Linq.IQueryable%601>).</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerator%601> </xref:System.Linq.IQueryable> </xref:System.Collections.IEnumerable>  
  
 튜플(익명 형식)  
 수학적 개념인 튜플은 각각 특정한 형식을 가진 개체의 유한 시퀀스입니다. 튜플을 정렬된 목록이라고 하기도 합니다. 익명 형식은 이 개념을 언어에 구현한 것입니다. 익명 형식을 사용하여 명명되지 않은 클래스 형식을 선언하고 해당 형식의 개체를 동시에 인스턴스화할 수 있습니다.  
  
 자세한 내용은 참조 [익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)합니다.  
  
 형식 유추(암시적 형식 지정)  
 명시적 형식 선언이 없는 경우 컴파일러에서 변수의 형식을 결정하도록 하는 기능입니다.  
  
 자세한 내용은 참조 [로컬 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)합니다.  
  
 지연된 실행 및 지연 계산  
 확인된 값이 실제로 필요할 때까지 식의 계산을 지연하는 것입니다. 지연된 실행은 컬렉션에서 지원됩니다.  
  
 자세한 내용은 참조 [기본 쿼리 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md) 및 [지연 된 실행과 지연 계산은 LINQ to XML (Visual Basic)에서](../../../../visual-basic/programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)합니다.  
  
 이러한 언어 기능은 이 단원 전반의 코드 샘플에서 사용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [순수 함수 변환 (Visual Basic) 소개](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [함수형 프로그래밍과 명령형 프로그래밍 비교 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md)