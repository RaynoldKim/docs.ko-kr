---
title: "yield(C# 참조) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "yield"
  - "yield_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "yield 키워드[C#]"
ms.assetid: 1089194f-9e53-46a2-8642-53ccbe9d414d
caps.latest.revision: 46
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 46
---
# yield(C# 참조)
문에 `yield` 키워드를 사용하는 경우 해당 메서드, 연산자, 또는 이 키워드가 나타나는 `get` 접근자가 반복기임을 나타냅니다.  `yield`를 사용하여 반복기를 정의할 경우 사용자 지정 컬렉션 형식에 <xref:System.Collections.IEnumerable> 및 <xref:System.Collections.IEnumerator> 패턴을 구현하면 명시적 추가 클래스\(열거형의 상태를 보관하는 클래스, 예제는 <xref:System.Collections.Generic.IEnumerator%601> 참조\)를 사용하지 않아도 됩니다.  
  
 다음 예제에서는 두 가지 형태의 `yield` 문을 보여줍니다.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## 설명  
 `yield return` 문을 사용하여 각 요소를 따로따로 반환할 수 있습니다.  
  
 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 문 또는 LINQ 쿼리를 이용하여 반복기 메서드를 사용합니다.  각각의 `foreach` 루프의 반복이 반복기 메서드를 호출합니다.  `yield return` 문이 반복기 메서드에 도달하면 `expression` 이 반환되고 코드에서 현재 위치는 유지됩니다.  다음에 반복기 함수가 호출되면 해당 위치에서 실행이 다시 시작됩니다.  
  
 `yield break` 문을 사용하여 반복기를 종료할 수 있습니다.  
  
 반복기에 대한 자세한 내용은 [반복기](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)를 참조하십시오.  
  
## 반복기 메서드 및 Get 접근자  
 반복기 선언은 다음과 같은 요구 사항을 충족해야 합니다.  
  
-   반환 형식은 <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, 또는 <xref:System.Collections.Generic.IEnumerator%601>여야 합니다.  
  
-   선언에 [ref](../../../csharp/language-reference/keywords/ref.md) 또는 [out](../../../csharp/language-reference/keywords/out.md) 매개 변수가 허용되지 않습니다.  
  
 <xref:System.Collections.IEnumerable> 또는 <xref:System.Collections.IEnumerator>를 반환하는 반복기의 `yield` 형식은 `object`입니다.  반복기가 <xref:System.Collections.Generic.IEnumerable%601> 또는 <xref:System.Collections.Generic.IEnumerator%601>를 반환할 경우 `yield return` 문의 식 형식에서 제네릭 형식 매개 변수로 암시적 변환이 있어야 합니다.  
  
 `yield return` 또는 `yield break` 문은 다음과 같은 특징이 있는 메서드에 사용할 수 없습니다.  
  
-   무명 메서드  자세한 내용은 [무명 메서드](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)을 참조하십시오.  
  
-   안전하지 않은 블록을 포함하는 메서드  자세한 내용은 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)을 참조하십시오.  
  
## 예외 처리  
 `yield return` 문은 try\-catch 블록에서 찾을 수 없습니다.  `yield return` 문은 try\-finally 문의 try 블록에서 찾을 수 있습니다.  
  
 `yield break` 문은 try 블록이나 catch 블록에서 찾을 수 있지만 finally 블록에서는 찾을 수 없습니다.  
  
 `foreach` 본문\(반복기 메서드 외부\)에서 예외를 throw한 경우, 반복기 메서드의 `finally` 블록이 실행됩니다.  
  
## 기술 구현  
 다음 코드는 반복기 메서드에서 `IEnumerable<string>`을 반환하고 해당 요소를 반복합니다.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 `MyIteratorMethod` 호출은 메서드의 본문을 실행하지 않습니다.  대신에 `elements` 변수에 `IEnumerable<string>`을 반환합니다.  
  
 `foreach` 루프 반복에서 `elements`에 대한 <xref:System.Collections.IEnumerator.MoveNext%2A> 메서드가 호출됩니다.  이 호출은 다음 `yield return` 문에 도달할 때까지 `MyIteratorMethod` 본문을 실행합니다.  `yield return` 문에서 반환하는 식은 루프 본문에서 사용하는 `element` 변수 값뿐만 아니라 요소의 <xref:System.Collections.Generic.IEnumerator%601.Current%2A> 속성인 `IEnumerable<string>`도 결정합니다.  
  
 이후에 `foreach` 루프가 반복될 때마다 중지되었던 위치에서 반복기 본문 실행이 계속되고 `yield return` 문에 도달하면 다시 중지됩니다.  `foreach` 루프는 반복기 메서드가 종료되거나 `yield break` 문에 도달하면 완료됩니다.  
  
## 예제  
 다음 예제에는 `for` 루프 내에 `yield return` 문이 있습니다.  `Process`에서 `foreach` 문의 본문을 반복할 때마다 `Power` 반복기 함수에 대한 호출이 생성됩니다.  반복기 함수를 호출할 때마다 다음에 `for` 루프를 반복하는 도중에 `yield return` 문이 실행됩니다.  
  
 반복기 메서드의 반환 형식은 반복기 인터페이스 형식인 <xref:System.Collections.IEnumerable>입니다.  반복기 메서드가 호출되면 숫자의 거듭제곱이 들어 있는 열거형 개체를 반환합니다.  
  
 [!code-cs[csrefKeywordsContextual#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/yield_1.cs)]  
  
## 예제  
 다음 예제는 반복기인 `get` 접근자에 대해 설명합니다.  이 예제에서는 각 `yield return` 문이 사용자 정의 클래스의 인스턴스를 반환합니다.  
  
 [!code-cs[csrefKeywordsContextual#21](../../../csharp/language-reference/keywords/codesnippet/CSharp/yield_2.cs)]  
  
## C\# 언어 사양  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 참고 항목  
 [C\# 참조](../../../csharp/language-reference/index.md)   
 [C\# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [반복기](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)