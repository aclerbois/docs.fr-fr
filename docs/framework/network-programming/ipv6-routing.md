---
title: Routage IPv6
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c98731b4-b542-46a2-9947-1cea63c186b2
caps.latest.revision: "4"
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: 21edbfee91a759b0b48f9dd6c0c9e900cdff93f5
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="ipv6-routing"></a>Routage IPv6
Le protocole IPv6 comprend un mécanisme de routage souple. En raison de la façon dont les ID réseau IPv4 sont alloués, les tables de routage volumineuses doivent être gérées par les routeurs Internet principaux. Ces routeurs doivent connaître tous les itinéraires afin de transmettre les paquets qui sont susceptibles d’être dirigés vers des nœuds Internet. Grâce à sa capacité de regrouper des adresses, IPv6 permet un adressage souple et réduit considérablement la taille des tables de routage. Dans cette nouvelle architecture d’adressage, les routeurs intermédiaires doivent uniquement effectuer le suivi de la partie locale de leur réseau afin de transmettre les messages de manière appropriée.  
  
## <a name="neighbor-discovery"></a>Découverte de voisin  
 Voici certaines des fonctionnalités fournies par la découverte de voisin :  
  
-   La découverte de routeurs. Elle permet aux hôtes d’identifier les routeurs locaux.  
  
-   La résolution d’adresse. Elle permet aux nœuds de résoudre une adresse link-layer pour l’adresse correspondante du tronçon suivant (en remplacement du protocole ARP).  
  
-   La configuration automatique des adresses. Elle permet aux hôtes de configurer automatiquement les adresses locales et globales.  
  
 La découverte de voisin utilise le protocole IPv6 (ICMPv6) pour les types de messages suivants :  
  
-   Annonces de routeur. Envoyées par un routeur à intervalles réguliers ou en réponse à une sollicitation de routeur. Les routeurs IPv6 utilisent des annonces de routeur pour annoncer leur disponibilité, leurs préfixes d’adresse et autres paramètres.  
  
-   Sollicitations de routeur. Envoyées par un hôte pour demander que les routeurs présents sur la liaison envoient immédiatement une annonce de routeur.  
  
-   Sollicitations de voisin. Envoyées par les nœuds pour la résolution d’adresse, la détection d’adresses en double et la vérification de disponibilité d’un voisin.  
  
-   Annonces de voisin. Envoyées par les nœuds pour répondre à une sollicitation de voisin ou pour avertir les voisins d’un changement d’adresse link-layer.  
  
-   Redirections. Envoyées par les routeurs pour indiquer une meilleure adresse de tronçon suivant à une destination particulière pour un nœud expéditeur.  
  
## <a name="see-also"></a>Voir aussi  
 [Protocole IPv6](../../../docs/framework/network-programming/internet-protocol-version-6.md)  
 [Sockets](../../../docs/framework/network-programming/sockets.md)
