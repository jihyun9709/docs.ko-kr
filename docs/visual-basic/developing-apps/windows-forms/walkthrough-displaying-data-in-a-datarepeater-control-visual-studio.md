---
title: "연습: DataRepeater 컨트롤 (Visual Studio)의 데이터 표시 | Microsoft 문서"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- DataRepeater, walkthrough
ms.assetid: 65dcdb95-6c3e-47cc-987d-190000f71653
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 09f15c94c3d5a3387935c8d3f4758c0ecfd7cfcd
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-displaying-data-in-a-datarepeater-control-visual-studio"></a>연습: DataRepeater 컨트롤의 데이터 표시(Visual Studio)
이 연습에서는의 바인딩된 데이터를 표시 하기 위한 기본 시작 후 완료 시나리오를 제공 된 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="prerequisite"></a>필수 조건  
 이 연습을 수행하려면 Northwind 샘플 데이터베이스가 있어야 합니다.  
  
 이 데이터베이스가 개발 컴퓨터에 없는 경우 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkID=98088)에서 다운로드할 수 있습니다. 자세한 내용은 [샘플 데이터베이스 다운로드](https://msdn.microsoft.com/library/bb399411)합니다.  
  
## <a name="overview"></a>개요  
 이 연습의 첫 번째 부분은 다음과 같은 네 가지 주요 작업으로 구성됩니다.  
  
-   솔루션 만들기  
  
-   추가 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
-   데이터 소스 추가  
  
-   데이터 바인딩된 컨트롤 추가  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-a-datarepeater-solution"></a>DataRepeater 솔루션 만들기  
 첫 번째 단계에서는 프로젝트 및 솔루션을 만듭니다.  
  
#### <a name="to-create-a-datarepeater-solution"></a>DataRepeater 솔루션을 만들려면  
  
1.  Visual Studio의 **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.  
  
2.  **새 프로젝트** 대화 상자의 **프로젝트 형식** 창에서 **Visual Basic**을 확장하고 **Windows**를 클릭합니다.  
  
3.  **템플릿** 창에서 **Windows Forms 응용 프로그램**을 클릭합니다.  
  
4.  **이름** 상자에 `DataRepeaterApp`을 입력합니다.  
  
5.  **확인**을 클릭합니다.  
  
     Windows Forms 디자이너가 열립니다.  
  
6.  Windows Forms 디자이너에서 폼을 선택합니다. **속성** 창에서 **Size** 속성을 `800, 700`으로 설정합니다.  
  
## <a name="adding-a-datarepeater-control"></a>DataRepeater 컨트롤 추가  
 이 단계에서는 추가 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>컨트롤을 폼.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-a-datarepeater-control"></a>DataRepeater 컨트롤을 추가하려면  
  
1.  **보기** 메뉴에서 **도구 상자**를 클릭합니다.  
  
     **도구 상자** 가 열립니다.  
  
2.  **Visual Basic PowerPacks** 탭을 선택합니다.  
  
3.  끌기는 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>컨트롤을 끌어와 **Form1**.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
4.  속성 창에서 **Location** 속성을 `0, 25`로 설정합니다.  
  
5.  **Size** 속성을 `460, 600`으로 설정합니다.  
  
## <a name="adding-a-data-source"></a>데이터 소스 추가  
 에 대 한 데이터 원본을 추가 하면이 단계는 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-a-data-source"></a>데이터 소스를 추가하려면  
  
1.  **데이터** 메뉴에서 **데이터 소스 표시**를 클릭합니다.  
  
2.  **데이터 소스** 창에서 **새 데이터 소스 추가**를 클릭합니다.  
  
3.  **데이터 소스 형식 선택** 페이지에서 **데이터베이스** 를 선택하고 **다음**을 클릭합니다.  
  
4.  **데이터 연결 선택** 페이지에서 다음 단계 중 하나를 수행합니다.  
  
    -   Northwind 샘플 데이터베이스에 대한 데이터 연결이 드롭다운 목록에 표시되면 해당 연결을 클릭합니다.  
  
         또는  
  
    -   **새 연결** 을 클릭하여 새 데이터 연결을 구성합니다. 자세한 내용은 참조 [하는 방법: SQL Server 데이터베이스에 대 한 연결 만들기](http://msdn.microsoft.com/en-us/360c340d-e5a6-4a7e-a569-e95d500be43d)합니다.  
  
5.  데이터베이스에 암호가 필요하면 중요한 데이터를 포함하는 옵션을 선택하고 **다음**을 클릭합니다.  
  
    > [!NOTE]
    >  대화 상자가 나타나는 경우 **예** 를 클릭하여 프로젝트에 파일을 저장합니다.  
  
6.  **응용 프로그램 구성 파일에 연결 문자열 저장** 페이지에서 **다음** 을 클릭합니다.  
  
7.  **데이터베이스 개체 선택** 페이지에서 **테이블** 노드를 확장합니다.  
  
8.  **Customers** 및 **Orders** 테이블 옆의 확인란을 선택한 다음 **마침**을 클릭합니다.  
  
     **NorthwindDataSet** 가 프로젝트에 추가되고 **Customers** 및 **Orders** 테이블이 **데이터 소스** 창에 나타납니다.  
  
## <a name="adding-data-bound-controls"></a>데이터 바인딩된 컨트롤 추가  
 이 단계에서는 데이터 바인딩된 컨트롤에 추가한 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-data-bound-controls"></a>데이터 바인딩된 컨트롤을 추가하려면  
  
1.  **데이터 소스** 창에서 **Customers** 테이블의 최상위 노드를 선택합니다.  
  
2.  테이블 노드의 드롭다운 목록에서 **자세히** 를 클릭하여 테이블의 놓기 형식을 **자세히** 로 변경합니다.  
  
3.  선택 된 **고객** 노드 테이블의 항목 템플릿 영역 (위쪽 영역)으로 끌어와 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
     A <xref:System.Windows.Forms.BindingNavigator>폼에 컨트롤이 추가 되 고 **NorthwindDataSet**, **CustomersBindingSource**, **CustomersTableAdapter**, **TableAdapterManager**, 및 **CustomersBindingNavigator** 구성 요소가 구성 요소 트레이에 추가 됩니다.</xref:System.Windows.Forms.BindingNavigator>  
  
4.  모든 필드와 해당 레이블을 선택하고 항목 템플릿 영역 왼쪽 가장자리 근처에 배치합니다.  
  
5.  마지막 다섯 개의 필드(**Region**, **Postal Code**, **Country**, **Phone**및 **Fax**)와 해당 레이블을 선택하고 첫 번째 여섯 개 필드의 오른쪽 위로 이동합니다.  
  
6.  항목 템플릿(컨트롤의 위쪽 영역)을 선택합니다.  
  
7.  속성 창에서 **Size** 속성을 `427, 170`으로 설정합니다.  
  
 이 시점에서 작동 중인 응용 프로그램에서는 고객의 반복 목록을 표시합니다. F5 키를 눌러 응용 프로그램을 실행하고, 데이터를 변경하고, 고객 레코드를 추가 또는 삭제할 수 있습니다.  
  
 다음 단계에서 사용자 지정 하는 방법을 배우게 됩니다는 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="next-steps-optional"></a>다음 단계(선택 사항)  
 이 연습 부분은 다음과 같은 네 가지 선택적인 작업으로 구성됩니다.  
  
-   모양을 변경 하는 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
-   사용자가 레코드를 추가하거나 삭제하지 못하도록 지정  
  
-   에 검색 기능 추가 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
-   마스터 / 세부 테이블을 추가 하는 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="changing-the-appearance-of-the-datarepeater-control"></a>DataRepeater 컨트롤의 모양 변경  
 이 선택적 단계에서 변경 된 `BackColor` 의 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>디자인 타임에 컨트롤.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 또한 행을 다른 색으로 표시하고 조건에 따라 레이블의 `ForeColor` 를 변경하는 코드를 추가합니다.  
  
#### <a name="to-change-the-appearance-of-the-control"></a>컨트롤의 모양을 변경하려면  
  
1.  Windows Forms 디자이너에서의 주 (아래쪽) 영역을 선택 된 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  속성 창에서 `BackColor` 속성을 흰색으로 설정합니다.  
  
3.  두 번 클릭 하 여 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>코드 편집기를 엽니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
4.  코드 편집기의 이벤트 드롭다운 목록에서 **DrawItem**을 클릭합니다.  
  
5.  에 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>이벤트 처리기에 다음 코드를 추가 `BackColor`:</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>  
  
     [!code-cs[#1 VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_1.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#1;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_1.vb)]  
  
6.  에 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>이벤트 처리기를 변경 하려면 다음 코드를 추가 `ForeColor` 조건에 따라 레이블:</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>  
  
     [!code-cs[#2 VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_2.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#2;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_2.vb)]  
  
7.  F5 키를 눌러 응용 프로그램을 실행하고 사용자 지정 항목을 확인합니다.  
  
## <a name="preventing-users-from-adding-or-deleting-records"></a>사용자가 레코드를 추가하거나 삭제하지 못하도록 지정  
 이 선택적 단계를 추가 하거나 레코드를 삭제 하지 못하도록 하는 코드 추가 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-prevent-users-from-adding-and-deleting-records"></a>사용자가 레코드를 추가하거나 삭제하지 못하도록 지정하려면  
  
1.  Windows Forms 디자이너에서 폼을 두 번 클릭하여 코드 편집기를 엽니다.  
  
2.  `Form_Load` 이벤트에 다음 코드를 추가합니다.  
  
     [!code-cs[#3 VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_3.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#3;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_3.vb)]  
  
3.  클래스 이름 드롭다운 목록에서 **BindingNavigatorDeleteItem**을 클릭합니다. 메서드 이름 드롭다운 목록에서 **EnabledChanged**를 클릭합니다.  
  
4.  다음 코드를 `BindingNavigatorDeleteItem_EnabledChanged` 이벤트 처리기에 추가합니다.  
  
     [!code-cs[#4 VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_4.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#4;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_4.vb)]  
  
    > [!NOTE]
    >  이 단계는 필요 하기 때문에 <xref:System.Windows.Forms.BindingSource>하면는 **DeleteItem** 현재 레코드가 변경 될 때마다 단추.</xref:System.Windows.Forms.BindingSource>  
  
5.  F5 키를 눌러 응용 프로그램을 실행합니다. **DeleteItem** 단추가 비활성화되므로 사용자가 Delete 키를 눌러 항목을 삭제할 수 없습니다.  
  
## <a name="adding-search-capability-to-the-datarepeater-control"></a>DataRepeater 컨트롤에 검색 기능 추가  
 이 선택적 단계에서 값을 검색 하는 기능을 구현는 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 검색 문자열이 발견되면 컨트롤에서 값을 포함하는 항목을 선택하고 항목을 뷰로 스크롤합니다.  
  
#### <a name="to-add-search-capability"></a>검색 기능을 추가하려면  
  
1.  끌기는 <xref:System.Windows.Forms.TextBox>에서 제어는 **도구 상자** 포함 된 양식에 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>컨트롤.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:System.Windows.Forms.TextBox>  
  
     아래에 배치 된 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  속성 창에서 **Name** 속성을 **SearchTextBox**로 변경합니다.  
  
3.  끌기는 <xref:System.Windows.Forms.Button>에서 제어는 **도구 상자** 포함 된 양식에 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>컨트롤.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:System.Windows.Forms.Button> 아래에 배치 된 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
4.  속성 창에서 **Name** 속성을 **SearchButton**으로 변경합니다. **Text** 속성을 **Search**로 변경합니다.  
  
5.  두 번 클릭은 <xref:System.Windows.Forms.Button>코드 편집기를 열려면 제어 하 고 다음 코드를 추가 하는 `SearchButton_Click` 이벤트 처리기입니다.</xref:System.Windows.Forms.Button>  
  
     [!code-cs[#5 VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_5.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough&#5;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_5.vb)]  
  
6.  F5 키를 눌러 응용 프로그램을 실행합니다. **SearchTextBox** 에 고객 ID를 입력하고 **Search** 단추를 클릭합니다.  
  
## <a name="adding-a-master-and-detail-table-to-the-datarepeater"></a>DataRepeater에 마스터 및 세부 테이블 추가  
 이 선택적 단계에서는 두 번째 추가 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>컨트롤을 각 고객에 대 한 관련된 주문을 표시 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-a-master-and-detail-table"></a>마스터 및 세부 테이블을 추가하려면  
  
1.  초를 끌어 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>에서 제어는 **Visual Basic PowerPacks** 탭에 **도구 상자** 양식에.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  속성 창에서 **Location** 속성을 `465, 25`로 설정합니다.  
  
3.  **Size** 속성을 `315, 600`으로 설정합니다.  
  
4.  **데이터 소스** 창에서 **Customers** 테이블 노드를 확장하고 **Orders** 테이블에 대한 상세 노드를 선택합니다.  
  
5.  테이블 노드의 드롭다운 목록에서 자세히를 클릭하여 이 **Orders** 테이블의 놓기 형식을 **자세히** 로 변경합니다.  
  
6.  이 끌어 **주문** 테이블 노드를 두 번째 항목 템플릿 영역 (위쪽 영역)로 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
     **OrdersBindingSource** 구성 요소 및 **OrdersTableAdapter** 구성 요소가 구성 요소 트레이에 추가됩니다.  
  
7.  F5 키를 눌러 응용 프로그램을 실행합니다. 첫 번째에서 각 고객을 선택 하면 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>컨트롤 주문이 두 번째에 표시 되는 해당 고객 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>제어 합니다.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="see-also"></a>참고 항목  
 [DataRepeater 컨트롤 소개](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [방법: DataRepeater 컨트롤의 바인딩된 데이터 표시](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [방법: 바인딩되지 않은 DataRepeater 컨트롤의 컨트롤 표시](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [방법: DataRepeater 컨트롤의 레이아웃 변경](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md)   
 [방법: DataRepeater 컨트롤의 항목 머리글 표시](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md)   
 [방법: DataRepeater 컨트롤의 데이터 검색](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md)   
 [방법: 두 DataRepeater 컨트롤 (Visual Studio)를 사용 하 여 마스터/세부 폼 만들기](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)   
 [방법: DataRepeater 컨트롤의 모양 변경](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [방법: DataRepeater 항목 추가 및 삭제 사용 안 함](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md)   
 [DataRepeater 컨트롤 문제 해결](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)
