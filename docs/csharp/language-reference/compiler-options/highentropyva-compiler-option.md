---
title: -highentropyva (Options du compilateur C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: /highentropyva
helpviewer_keywords:
- /highentropyva compiler option [C#]
- -highentropyva compiler option [C#]
- highentropyva compiler option [C#]
ms.assetid: eaf409b3-384e-49dd-9417-62453658f421
caps.latest.revision: "8"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 5746caed8c1bf61038c97a49987c4c168eef9f3f
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="highentropyva-c-compiler-options"></a>/highentropyva (Options du compilateur C#)
L’option du compilateur **/highentropyva** indique au noyau Windows si un fichier exécutable particulier prend en charge la randomisation du format d’espace d’adresse (ASLR) de forte entropie.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
/highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>Arguments  
 `+` &#124; `-`  
 Cette option spécifie qu’un exécutable 64 bits ou un exécutable marqué par l’option du compilateur [/platform:anycpu](../../../csharp/language-reference/compiler-options/platform-compiler-option.md) prend en charge un espace d’adressage virtuel d’entropie élevée. Cette option est désactivée par défaut. Utilisez **/highentropyva+** ou **/highentropyva** pour l’activer.  
  
## <a name="remarks"></a>Remarques  
 L’option **/highentropyva** permet à des versions compatibles du noyau Windows d’utiliser un degré d’entropie plus élevé lors de la randomisation du format de l’espace d’adresse d’un processus. En utilisant un degré d’entropie plus élevé, vous pouvez allouer un plus grand nombre d’adresses aux zones de mémoire, telles que les piles et les tas. Par conséquent, il est plus difficile de deviner l’emplacement d’une zone de mémoire.  
  
 Lorsque l’option du compilateur **/highentropyva** est spécifiée, l’exécutable cible et tous les modules dont il dépend doivent être capables de gérer les valeurs de pointeur supérieures à 4 Go lorsqu’ils sont exécutés comme un processus 64 bits.
