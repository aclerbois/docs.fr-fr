---
title: "Assistant Débogage managé jitCompilationStart"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JIT compilation
- MDAs (managed debugging assistants), JIT compilation
- JitCompilationStart MDA
- managed debugging assistants (MDAs), JIT compilation
ms.assetid: 5ffd2857-d0ba-4342-9824-9ffe04ec135d
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 67c80fce223d8f212fa485a8105862bcf24e161b
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="jitcompilationstart-mda"></a>Assistant Débogage managé jitCompilationStart
L’Assistant Débogage managé `jitCompilationStart` est activé pour signaler le moment où le compilateur juste-à-temps (JIT, Just-In-Time) commence à compiler une fonction.  
  
## <a name="symptoms"></a>Symptômes  
 La taille du jeu de travail augmente pour un programme qui est déjà au format d’image natif, car mscorjit.dll est chargé dans le processus.  
  
## <a name="cause"></a>Cause  
 Les assemblys dont dépend le programme n’ont pas tous été générés au format natif, ou ceux qui l’ont été ne sont pas correctement inscrits.  
  
## <a name="resolution"></a>Résolution  
 L’activation de cet Assistant Débogage managé vous permet de déterminer la fonction qui est compilée juste-à-temps. Déterminez si l’assembly qui contient la fonction est généré au format natif et s’il est correctement inscrit.  
  
## <a name="effect-on-the-runtime"></a>Effet sur le runtime  
 Cet Assistant Débogage managé enregistre un message juste avant qu’une méthode ne soit compilée juste-à-temps, de sorte que son activation a un impact significatif sur les performances. Notez que, si une méthode est inline, cet Assistant Débogage managé ne générera pas de message séparé.  
  
## <a name="output"></a>Sortie  
 L’exemple de code suivant illustre une sortie. Dans ce cas, la sortie montre que, dans l’assembly Test, la méthode m sur la classe ns2.CO a été compilée juste-à-temps.  
  
```  
method name="Test!ns2.C0::m"  
```  
  
## <a name="configuration"></a>Configuration  
 Le fichier de configuration suivant présente divers filtres qui peuvent être utilisés pour filtrer les méthodes signalées quand elles sont d’abord compilées juste-à-temps. Vous pouvez spécifier que toutes les méthodes doivent être signalées en affectant * à la valeur de l’attribut name.  
  
```xml  
<mdaConfig>  
  <assistants>  
    <jitCompilationStart>  
      <methods>  
        <match name="C0::m" />  
        <match name="MyMethod" />  
        <match name="C2::*" />  
        <match name="ns0::*" />  
        <match name="ns1.C0::*" />  
        <match name="ns2.C0::m" />  
        <match name="ns2.C0+N0::m" />  
      </methods>  
    </jitCompilationStart >  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>Exemple  
 L’exemple de code suivant doit normalement être utilisé avec le fichier de configuration précédent.  
  
```  
using System;  
using System.Reflection;  
using System.Runtime.CompilerServices;  
using System.Runtime.InteropServices;  
  
public class Entry  
{  
    public static void Main(string[] args)  
    {  
        C0.m();  
        C1.MyMethod();  
        C2.m();  
  
        ns0.C0.m();  
        ns0.C0.N0.m();  
        ns0.C1.m();  
  
        ns1.C0.m();  
        ns1.C0.N0.m();  
  
        ns2.C0.m();  
        ns2.C0.N0.m();  
    }  
}  
  
public class C0  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
public class C1  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void MyMethod() { }  
}  
  
public class C2  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
namespace ns0  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
  
    public class C1  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
    }  
}  
  
namespace ns1  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
  
namespace ns2  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>  
 [Diagnostic d’erreurs avec les Assistants Débogage managé](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)  
 [Marshaling d'interopérabilité](../../../docs/framework/interop/interop-marshaling.md)
