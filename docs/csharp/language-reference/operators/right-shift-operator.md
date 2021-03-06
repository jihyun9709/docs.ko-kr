---
title: "&gt;&gt; 연산자(C# 참조)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '>>_CSharpKeyword'
dev_langs:
- CSharp
helpviewer_keywords:
- '>> operator [C#]'
- right shift operator (>>) [C#]
ms.assetid: a07f8679-d318-4ef8-b38b-65903efb8056
caps.latest.revision: 15
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: dd3f077e9bb491cefce7db7c015bde201f6f8207
ms.contentlocale: ko-kr
ms.lasthandoff: 07/28/2017

---
# <a name="gtgt-operator-c-reference"></a>&gt;&gt; 연산자(C# 참조)
오른쪽 시프트 연산자(`>>`)는 첫 번째 피연산자를 두 번째 피연산자로 지정된 비트 수만큼 오른쪽으로 이동합니다.  
  
## <a name="remarks"></a>설명  
 첫 번째 피연산자가 [int](../../../csharp/language-reference/keywords/int.md) 또는 [uint](../../../csharp/language-reference/keywords/uint.md)(32비트 수량)이면 두 번째 피연산자의 하위 5비트(두 번째 피연산자 & 0x1f)로 시프트 수가 지정됩니다.  
  
 첫 번째 피연산자가 [long](../../../csharp/language-reference/keywords/long.md) 또는 [ulong](../../../csharp/language-reference/keywords/ulong.md)(64비트 수량)이면 두 번째 피연산자의 하위 6비트(두 번째 피연산자 & 0x3f)로 시프트 수가 지정됩니다.  
  
 첫 번째 피연산자가 [int](../../../csharp/language-reference/keywords/int.md) 또는 [long](../../../csharp/language-reference/keywords/long.md)이면 오른쪽 시프트는 산술 시프트입니다(비어 있는 상위 비트가 부호 비트로 설정됨). 첫 번째 피연산자가 [uint](../../../csharp/language-reference/keywords/uint.md) 또는 [ulong](../../../csharp/language-reference/keywords/ulong.md) 형식이면 오른쪽 시프트는 논리적 시프트입니다(상위 비트가 0으로 채워짐).  
  
 사용자 정의 형식은 `>>` 연산자를 오버로드할 수 있습니다. 첫 번째 피연산자의 형식은 사용자 정의 형식이어야 하고 두 번째 피연산자의 형식은 [int](../../../csharp/language-reference/keywords/int.md)여야 합니다. 자세한 내용은 [operator](../../../csharp/language-reference/keywords/operator.md)를 참조하세요. 이항 연산자가 오버로드되면 해당 대입 연산자도 암시적으로 오버로드됩니다.  
  
## <a name="example"></a>예제  
 [!code-cs[csRefOperators#26](../../../csharp/language-reference/operators/codesnippet/CSharp/right-shift-operator_1.cs)]  
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)   
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)   
 [C# 연산자](../../../csharp/language-reference/operators/index.md)

