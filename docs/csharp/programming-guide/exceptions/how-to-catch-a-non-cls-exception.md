---
title: "방법: CLS 규격이 아닌 예외 catch | Microsoft 문서"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exceptions [C#], non-CLS
ms.assetid: db4630b3-5240-471a-b3a7-c7ff6ab31e8d
caps.latest.revision: 8
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3515ecab379a0e910cdd5ba82a4a39b085cc816f
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-catch-a-non-cls-exception"></a>방법: CLS 규격이 아닌 예외 catch
C++/CLI를 포함한 일부 .NET 언어를 사용하면 개체가 <xref:System.Exception>에서 파생되지 않은 예외를 throw할 수 있습니다. 이러한 예외를 *CLS 규격이 아닌 예외* 또는 *예외가 아닌 항목*이라고 합니다. [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)]에서는 CLS 규격이 아닌 예외를 throw할 수 없지만 다음 두 가지 방법으로 해당 예외를 catch할 수 있습니다.  
  
-   `catch (Exception e)` 블록 내에서 <xref:System.Runtime.CompilerServices.RuntimeWrappedException>으로.  
  
     기본적으로 [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 어셈블리는 CLS 규격이 아닌 예외를 래핑된 예외로 catch합니다. <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A> 속성을 통해 액세스할 수 있는 원래 예외에 액세스해야 할 경우 이 메서드를 사용합니다. 이 항목의 뒤에 나오는 절차에서는 이 방식으로 예외를 catch하는 방법을 설명합니다.  
  
-   일반 catch 블록(예외 형식이 지정되지 않은 catch 블록) 내에서 예외는 `catch (Exception)` 또는 `catch (Exception e)` 블록 뒤에 배치됩니다.  
  
     CLS 규격이 아닌 예외에 대한 응답으로 일부 작업(예: 로그 파일에 쓰기)을 수행하고자 하고 예외 정보에 액세스할 필요가 없는 경우 이 방법을 사용합니다. 기본적으로 공용 언어 런타임은 모든 예외를 래핑합니다. 이 동작을 사용하지 않으려면 일반적으로 AssemblyInfo.cs 파일에 있는 어셈블리 수준 특성 `[assembly: RuntimeCompatibilityAttribute(WrapNonExceptionThrows = false)]`를 코드에 추가합니다.  
  
### <a name="to-catch-a-non-cls-exception"></a>CLS 규격이 아닌 예외를 catch하려면  
  
1.  `catch(Exception e) block` 내에서 `as` 키워드를 사용하여 `e`가 <xref:System.Runtime.CompilerServices.RuntimeWrappedException>으로 캐스트될 수 있는지 테스트합니다.  
  
2.  <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A> 속성을 통해 원래 예외에 액세스합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 C++/CLR로 작성된 클래스 라이브러리에서 throw된 CLS 규격이 아닌 예외를 catch하는 방법을 보여 줍니다. 이 예제에서 [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 클라이언트 코드는 throw되는 예외 형식이 <xref:System.String?displayProperty=fullName>이라는 것을 사전에 알고 있습니다. 코드에서 해당 형식에 액세스할 수 있으면 <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A> 속성을 다시 원래 형식으로 캐스트할 수 있습니다.  
  
```  
// Class library written in C++/CLR.  
   ThrowNonCLS.Class1 myClass = new ThrowNonCLS.Class1();  
  
   try  
   {  
    // throws gcnew System::String(  
    // "I do not derive from System.Exception!");  
    myClass.TestThrow();   
   }  
  
   catch (Exception e)  
   {  
    RuntimeWrappedException rwe = e as RuntimeWrappedException;  
    if (rwe != null)      
    {  
      String s = rwe.WrappedException as String;  
      if (s != null)  
      {  
        Console.WriteLine(s);  
      }  
    }  
    else  
    {  
       // Handle other System.Exception types.  
    }  
   }             
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Runtime.CompilerServices.RuntimeWrappedException>   
 [예외 및 예외 처리](../../../csharp/programming-guide/exceptions/index.md)
