---
title: "방법: 경로를 따라 개체에 애니메이션 효과 주기(매트릭스 애니메이션) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "애니메이션, (매트릭스 애니메이션) 경로 따른 개체"
  - "매트릭스 애니메이션"
ms.assetid: 7000e697-1414-468c-b915-cf66062fc49e
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 방법: 경로를 따라 개체에 애니메이션 효과 주기(매트릭스 애니메이션)
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> 클래스에서 정의 된 경로 따라 개체에 애니메이션을 적용 하는 <xref:System.Windows.Media.PathGeometry>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 다음을 수행 하 여 경로 따라 개체에 애니메이션 효과 적용 합니다.  
  
-   적용 되는 <xref:System.Windows.Media.MatrixTransform> 이동할 수 있도록 개체에 있습니다.  
  
-   경로 사용 하 여 정의 된 <xref:System.Windows.Media.PathGeometry>합니다.  
  
-   만듭니다는 <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> 애니메이션 효과를 사용 하 여는 <xref:System.Windows.Media.Matrix> 의 속성은 <xref:System.Windows.Media.MatrixTransform>합니다. <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> 는 <xref:System.Windows.Media.PathGeometry> 사용 하 여 생성 및 <xref:System.Windows.Media.Matrix> 값입니다.  
  
 [!code-xml[PathAnimationGallery_snippet#MatrixAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathexample.xaml#matrixanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathExample.cs#matrixanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathExample.vb#matrixanimationusingpathwholepage)]  
  
 전체 샘플을 참조 하십시오. [경로 애니메이션 샘플](http://go.microsoft.com/fwlink/?LinkID=160028)합니다. 기하학적 경로 대 한 자세한 내용은 참조는 [Geometry 개요](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [애니메이션 개요](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [경로 애니메이션 샘플](http://go.microsoft.com/fwlink/?LinkID=160028)   
 [경로 애니메이션 방법 항목](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)