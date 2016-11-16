---
title: "Format de fichier d’assembly .NET"
description: "Format de fichier d’assembly .NET"
keywords: .NET, .NET Core
author: richlander
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 6520323e-ff28-4c8a-ba80-e64a413199e6
translationtype: Human Translation
ms.sourcegitcommit: 30175813af95911c8ab4f2f0e39c40bed49a23b3
ms.openlocfilehash: edd6975fe4acdba3e75084f10b4d71efebe42a4d

---

# <a name="net-assembly-file-format"></a>Format de fichier d’assembly .NET

La plateforme .NET définit un format de fichier binaire - « assembly » - qui permet de décrire entièrement et de contenir des programmes .NET. Les assemblys sont utilisés pour les programmes eux-mêmes comme n’importe quelle bibliothèque dépendante. Un programme .NET peut être exécuté comme tout autre assembly, sans que d’autres artefacts soient nécessaires, en dehors du runtime .NET approprié. Les dépendances natives, y compris les API du système d’exploitation, sont à part et ne sont pas contenues dans le format d’assembly .NET, même si elles sont parfois décrites avec ce format (par exemple, WinRT).

> Chaque composant CLI inclut les métadonnées des déclarations, implémentations et références spécifiques de ce composant. Par conséquent, les métadonnées spécifiques du composant sont désignées comme les métadonnées de composant, et le composant qui en résulte est autodescriptif (d’après ECMA 335 I.9.1, Components and assemblies).

Le format est entièrement spécifié et normalisé sous ECMA 335. Tous les compilateurs et les runtimes .NET utilisent ce format. La présence d’un format binaire documenté et rarement mis à jour a été un atout majeur (sans doute une exigence) pour l’interopérabilité. Le format a été modifié de manière substantielle en 2005 (.NET 2.0) pour prendre en charge les génériques et l’architecture de processeur.

Le format est indépendant du processeur et du système d’exploitation. Il a été utilisé dans le cadre des runtimes .NET qui ciblent plusieurs processeurs. Le format lui-même est hérité de Windows, il peut être implémenté sur n’importe quel système d’exploitation. La raison pour laquelle il est largement adopté pour l’interopérabilité du système d’exploitation est sans doute que la plupart des valeurs sont stockées dans un format Little Endian. Il n’a pas d’affinité particulière avec la taille du pointeur d’ordinateur (par exemple, 32 bits, 64 bits).

Le format d’assembly .NET est également très descriptif de la structure d’une bibliothèque ou d’un programme donné. Il décrit les composants internes d’un assembly, en particulier : les références et les types d’assembly définis, et leur structure interne. Les API ou les outils peuvent lire et traiter ces informations pour l’affichage ou pour prendre des décisions de programmation.

## <a name="format"></a>Format

Le format binaire .NET est basé sur le format de [fichier PE](http://en.wikipedia.org/wiki/Portable_Executable) de Windows. En fait, les bibliothèques de classes .NET sont des fichiers Windows PE conformes qui ressemblent à première vue à des bibliothèques de liens dynamiques (DLL) Windows ou à des fichiers exécutables d’application (EXE). Il s’agit d’une caractéristique très utile dans Windows, car ces fichiers peuvent se faire passer pour des fichiers binaires exécutables natifs et recevoir le même traitement (par exemple, charge de système d’exploitation, outils PE).

![En-têtes d’assembly](./media/assembly-format/assembly-headers.png)

En-têtes d’assembly d’après ECMA 335 II.25.1, Structure of the runtime file format.

## <a name="processing-the-assemblies"></a>Traitement des assemblys

Vous pouvez écrire des outils ou des API pour traiter les assemblys. Les informations d’assembly permettent de prendre des décisions de programmation au moment de l’exécution, de réécrire des assemblys, de fournir l’IntelliSense des API dans un éditeur et de générer de la documentation. [System.Reflection](https://msdn.microsoft.com/library/system.reflection.aspx) et [Mono.Cecil](http://www.mono-project.com/docs/tools+libraries/libraries/Mono.Cecil/) sont de bons exemples d’outils fréquemment utilisés à cet effet.



<!--HONumber=Nov16_HO1-->

