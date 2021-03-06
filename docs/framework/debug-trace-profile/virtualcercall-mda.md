---
title: virtualCERCall (MDA)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MDAs (managed debugging assistants), CER calls
- virtualCERCall MDA
- virtual CER calls
- constrained execution regions
- CER calls
- managed debugging assistants (MDAs), CER calls
ms.assetid: 1eb18c7a-f5e0-443f-80fb-67bfbb047da2
caps.latest.revision: "13"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: f3f0c06eef7524c18e252ade9122d8c9cb3c2f8c
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="virtualcercall-mda"></a>virtualCERCall (MDA)
L’Assistant Débogage managé `virtualCERCall` est activé comme un avertissement indiquant qu’un site d’appel dans un graphique des appels d’une région d’exécution limitée fait référence à une cible virtuelle, c’est-à-dire un appel virtuel à une méthode virtuelle non finale ou un appel à l’aide d’une interface. Le CLR (Common Language Runtime) ne peut pas prédire la méthode de destination de ces appels uniquement à partir du langage intermédiaire et de l’analyse des métadonnées. En conséquence, l’arborescence des appels ne peut pas être préparée dans le cadre du graphique d’une région d’exécution limitée et les interruptions de threads dans cette sous-arborescence ne peuvent pas être automatiquement bloquées. Cet Assistant Débogage managé vous avertit des cas où il peut s’avérer nécessaire d’étendre une région d’exécution limitée en utilisant des appels explicites à la méthode <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> dès que les informations supplémentaires requises pour calculer la cible de l’appel sont connues au moment de l’exécution.  
  
## <a name="symptoms"></a>Symptômes  
 Des régions d’exécution limitée ne s’exécutent pas lors de l’interruption d’un thread ou du déchargement d’un domaine d’application.  
  
## <a name="cause"></a>Cause  
 Une région d’exécution limitée contient un appel à une méthode virtuelle qui ne peut pas être préparée automatiquement.  
  
## <a name="resolution"></a>Résolution  
 Appelez <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> pour la méthode virtuelle.  
  
## <a name="effect-on-the-runtime"></a>Effet sur le runtime  
 Cet Assistant Débogage managé n'a aucun effet sur le CLR.  
  
## <a name="output"></a>Sortie  
  
```  
Method 'MethodWithCer', while executing within a constrained execution region, makes a call  
at IL offset 0x0024 to 'VirtualMethod', which is virtual and cannot be prepared automatically  
at compile time. The caller must ensure this method is prepared explicitly at  
runtime before entering the constrained execution region.  
method name="VirtualMethod"  
declaringType name="VirtualCERCall+MyClass"  
  declaringModule name="mda"  
    callsite name="MethodWithCer" offset="0x0024"  
```  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    < VirtualCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>Exemple  
  
```  
class MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    virtual void VirtualMethod()  
    {  
        ...  
    }  
}  
  
class MyDerivedClass : MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    override void VirtualMethod()  
    {  
        ...  
    }  
}  
  
void MethodWithCer(MyClass object)  
{  
    RuntimeHelpers.PrepareConstrainedRegions();  
    try  
    {  
        ...  
    }  
    finally  
    {  
        // Start of the CER.  
  
        // Cannot tell at analysis time whether object is a MyClass  
        // or a MyDerivedClass, so we do not know which version of   
        // VirtualMethod we are going to call.  
        object.VirtualMethod();  
    }  
}  
```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>  
 [Diagnostic d’erreurs avec les Assistants Débogage managé](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)  
 [Marshaling d'interopérabilité](../../../docs/framework/interop/interop-marshaling.md)
