---
title: "nullable 형식(C# 프로그래밍 가이드)"
ms.date: 2017-05-15
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- nullable types [C#]
- C# language, nullable types
- types [C#], nullable
ms.assetid: e473cb01-28ca-42be-9cea-f717055d72c6
caps.latest.revision: 44
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
ms.openlocfilehash: 909c90da69d85512399eacd16e1ba6db7aad2291
ms.contentlocale: ko-kr
ms.lasthandoff: 07/28/2017

---
# <a name="nullable-types-c-programming-guide"></a>nullable 형식(C# 프로그래밍 가이드)
Nullable 형식은 <xref:System.Nullable%601?displayProperty=fullName> 구조체의 인스턴스입니다. Null 허용 형식은 해당 내부 형식의 올바른 값 범위와 추가 `null` 값을 나타낼 수 있습니다. 예를 들어 "Nullable of Int32"로도 나타내는 `Nullable<Int32>`에는 -2147483648에서 2147483647까지 값이 할당되거나 `null` 값이 할당될 수 있습니다. `Nullable<bool>`에는 [true](../../../csharp/language-reference/keywords/true.md), [false](../../../csharp/language-reference/keywords/false.md) 또는 [null](../../../csharp/language-reference/keywords/null.md) 값이 할당될 수 있습니다. 숫자 및 부울 형식에 `null`을 할당하는 기능은 값을 할당할 수 없는 요소를 포함하는 데이터베이스 및 기타 데이터 형식을 처리할 때 특히 유용합니다. 예를 들어 데이터베이스의 부울 필드는 값 `true` 또는 `false`를 저장하거나 정의되지 않을 수 있습니다. 
  
[!code-cs[nullable-형식](../../../../samples/snippets/csharp/programming-guide/nullable-types/nullable-ex1.cs)]  
  
추가 예제를 보려면 [Null 허용 형식 사용](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)을 참조하세요.  
  
## <a name="nullable-types-overview"></a>null 허용 형식 개요  
 null 허용 형식은 다음 특성을 갖습니다.  
  
-   null 허용 형식은 `null` 값이 할당될 수 있는 값-형식 변수를 나타냅니다. 참조 형식에 따라 null 허용 형식을 만들 수 없습니다. (참조 형식은 `null` 값을 이미 지원합니다.)  
  
-   구문 `T?`는 <xref:System.Nullable%601>의 축약형입니다. 여기서 `T`는 값 형식입니다. 두 가지 형태는 동일하게 사용할 수 있습니다.  
  
-   일반 값 형식의 경우처럼 null 허용 형식에 값을 할당합니다(예: `int? x = 10;` 또는 `double? d = 4.108`). null 허용 형식에 값 `null`을 할당할 수도 있습니다. `int? x = null.`  
  
-   <xref:System.Nullable%601.GetValueOrDefault%2A?displayProperty=fullName> 메서드를 사용하여 할당된 값 또는 내부 형식의 기본값(값이 `null`인 경우)을 반환합니다(예: `int j = x.GetValueOrDefault();`).  
  
-   다음 예제와 같이 <xref:System.Nullable%601.HasValue%2A> 및 <xref:System.Nullable%601.Value%2A> 읽기 전용 속성을 사용하여 null인지 테스트하고 값을 검색합니다. `if(x.HasValue) j = x.Value;`  
  
    -   `HasValue` 속성은 변수에 이 있으면 `true`를, `null`이면 `false`를 반환합니다.  
  
    -   `Value` 속성은 할당된 값이 있으면 해당 값을 반환합니다. 그렇지 않으면 <xref:System.InvalidOperationException?displayProperty=fullName>이 throw됩니다.  
  
    -   `HasValue`의 기본값은 `false`입니다. `Value` 속성에는 기본값이 없습니다.  
  
    -   다음 예제와 같이 null 허용 형식에 `==` 및 `!=` 연산자를 사용할 수도 있습니다. `if (x != null) y = x;`  
  
-   `??` 연산자를 사용하여 현재 값이 `null`인 null 허용 형식이 null을 허용하지 않는 형식에 할당되면 적용될 기본값을 할당합니다(예: `int? x = null; int y = x ?? -1;`).  
  
-   중첩된 null 허용 형식은 허용되지 않습니다. 다음 줄은 컴파일되지 않습니다. `Nullable<Nullable<int>> n;`  
  
## <a name="related-sections"></a>관련 단원  
 추가 정보  
  
-   [Nullable 형식 사용](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)  
  
-   [Nullable 형식 boxing](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)  
  
-   [?? 연산자](../../../csharp/language-reference/operators/null-conditional-operator.md)  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Nullable>   
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)   
 [C#](../../../csharp/csharp.md)   
 [C# 참조](../../../csharp/language-reference/index.md)   
 ['리프트'란 정확히 어떤 의미입니까?](http://go.microsoft.com/fwlink/?LinkId=112382)

