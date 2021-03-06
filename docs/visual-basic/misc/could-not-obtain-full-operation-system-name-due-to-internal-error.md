---
title: "Impossible d’obtenir le nom complet du système d’exploitation en raison d’une erreur interne"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords: vbrDiagnosticInfo_FullOSName
ms.assetid: f69da02b-eb9a-4284-bb9e-3025517ae6c1
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 65796c41d2a9fbd03517e7b15bc6b566ba4364fb
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="could-not-obtain-full-operation-system-name-due-to-internal-error"></a>Impossible d’obtenir le nom complet du système d’exploitation en raison d’une erreur interne
Impossible d’obtenir le nom complet du système d’exploitation en raison d’une erreur interne. Ceci peut être dû au fait que WMI est absent de l’ordinateur actuel.  
  
 Un appel à la propriété `My.Computer.Info.OSFullName` a échoué. WMI (Windows Management Instrumentation) n’est peut-être pas installé sur l’ordinateur actuel.  
  
## <a name="to-correct-this-error"></a>Pour corriger cette erreur  
  
1.  Ajoutez un bloc `Try...Catch` autour de l’appel à la propriété `My.Computer.Info.OSFullName` .  
  
2.  Pour plus d’informations sur WMI et comment l’installer, accédez à et recherchez « Windows Management Instrumentation Core ».  
  
## <a name="see-also"></a>Voir aussi  
 [My.Computer.Info.OSFullName, propriété](http://msdn.microsoft.com/en-us/b3b0fbd1-4dc5-428a-ad04-0d9fc9c2a9be)  
 [Exceptions et gestion des erreurs dans Visual Basic](http://msdn.microsoft.com/en-us/3e351e73-cf23-40ab-8b60-05794160529e)  
 [Try...Catch...Finally (instruction)](../../visual-basic/language-reference/statements/try-catch-finally-statement.md)
