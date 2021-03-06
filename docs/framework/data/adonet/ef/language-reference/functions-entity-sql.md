---
title: "함수(Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 52b3d776-5acc-4f69-b614-5a43ce56ef9f
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 함수(Entity SQL)
Entity SQL에서는 사용자 정의 함수, 정식 함수 및 공급자 특정 함수를 지원합니다.  사용자 정의 함수는 개념적 모델에 지정되거나 쿼리에 인라인으로 지정됩니다.  자세한 내용은 [사용자 정의 함수](../../../../../../docs/framework/data/adonet/ef/language-reference/user-defined-functions-entity-sql.md)을 참조하세요.  
  
 정식 함수는 Entity Framework에 미리 정의되어 있으며 데이터 공급자의 지원이 필요합니다.  공급자가 지원하지 않는 함수를 사용자가 호출하는 경우 Entity SQL 명령은 실패합니다.  따라서, 일반적으로 정식 함수는 공급자 특정 네임스페이스에 들어 있는 저장소 특정 함수의 경우에 권장됩니다.  자세한 내용은 [정식 함수](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)을 참조하세요.  
  
 Microsoft SQL 클라이언트 관리 공급자에서는 공급자 특정 함수 집합이 제공됩니다.  자세한 내용은 [Entity Framework 함수용 SqlClient](../../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)을 참조하세요.  
  
## 단원 내용  
 [사용자 정의 함수](../../../../../../docs/framework/data/adonet/ef/language-reference/user-defined-functions-entity-sql.md)  
  
 [함수 오버로드 확인](../../../../../../docs/framework/data/adonet/ef/language-reference/function-overload-resolution-entity-sql.md)  
  
 [집계 함수](../../../../../../docs/framework/data/adonet/ef/aggregate-functions-sqlclient-for-entity-framework.md)  
  
## 참고 항목  
 [Entity SQL 개요](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)