---
title: "Encodeurs personnalisés"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fa0e1d7f-af36-4bf4-aac9-cd4eab95bc4f
caps.latest.revision: "15"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 2b1370adc510b26b14bff0dec45d83513a2f13b3
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2017
---
# <a name="custom-encoders"></a>Encodeurs personnalisés
Cette rubrique décrit comment créer des encodeurs personnalisés.  
  
 Dans [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], vous utilisez un *liaison* pour spécifier comment transférer des données sur un réseau entre les points de terminaison. Une liaison est composée d’une séquence de *éléments de liaison*. Une liaison inclut des éléments de liaison de protocole facultatifs tels que de la sécurité, un *encodeur de Message* élément de liaison et un élément de liaison de transport requis. Un encodeur de message est représenté par un élément de liaison d’encodage de message. Trois encodeurs de message sont inclus dans [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] : Binary, MTOM (Message Transmission Optimization Mechanism) et Text.  
  
 Un élément de liaison d'encodage de message sérialise un <xref:System.ServiceModel.Channels.Message> sortant et le passe au transport ou reçoit la forme sérialisée d'un message du transport et le transmet à la couche de protocole (si celle-ci est présente), ou à l'application (dans le cas contraire).  
  
 Les encodeurs de message transforment des instances <xref:System.ServiceModel.Channels.Message> vers une représentation sur le câble ou à partir de celle-ci. Même si les encodeurs sont décrits comme étant situés au-dessus de la couche de transport dans la pile des canaux, ils résident en fait à l'intérieur de cette couche. Les transports (par exemple HTTP) mettent en forme le message selon les spécifications de la norme de transport. Les encodeurs (par exemple Text Xml) se contentent d'encoder le message.  
  
 Lorsque vous vous connectez à un client ou à un serveur préexistant, vous n'aurez peut-être pas le choix de l'utilisation d'un encodage de message particulier. Toutefois, les services [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] peuvent être accessibles par l'intermédiaire de plusieurs points de terminaison, chacun ayant un encodeur de message différent. Lorsqu'un encodeur unique ne couvre pas toute l'audience de votre service, vous pouvez exposer votre service sur plusieurs points de terminaison. Les applications clientes peuvent utiliser ensuite le point de terminaison le mieux adapté. L'utilisation de plusieurs points de terminaison vous permet de combiner les avantages des encodeurs de message différents avec d'autres éléments de liaison.  
  
## <a name="system-provided-encoders"></a>Encodeurs fournis par le système  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fournit plusieurs liaisons fournies par le système et conçues pour couvrir les scénarios d'application les plus courants. Chacune de ces liaisons associe un transport, un encodeur de message et d'autres options (la sécurité, par exemple). Cette rubrique décrit comment étendre les encodeurs de message `Text`, `Binary` et `MTOM` inclus dans [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ou comment créer votre propre encodeur personnalisé. L'encodeur de message texte prend en charge un encodage XML ordinaire ainsi que des encodages SOAP. Le mode d'encodage XML brut de l'encodeur de message texte est appelé POX (Plain Old XML) afin de le distinguer de l'encodage SOAP basé sur le texte.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]les combinaisons d’éléments de liaison fournies par les liaisons fournies par le système, consultez la section correspondante de [choisir un Transport](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md).  
  
## <a name="how-to-work-with-system-provided-encoders"></a>Comment utiliser des encodeurs fournis par le système  
 Un encodage est ajouté à une liaison à l'aide d'une classe dérivée de <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fournit les types suivants d'éléments de liaison dérivés de la classe <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> qui peut fournir l'encodage Text, Binary et MTOM :  
  
-   <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> est l'encodeur le plus interopérable, mais le moins efficace pour les messages XML. Un service Web ou un client de service Web comprend généralement le langage XML textuel. Toutefois, transmettre de larges blocs de données binaires sous la forme de texte n'est pas efficace.  
  
-   <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> représente l'élément de liaison qui spécifie l'encodage de caractères et le versioning de messages utilisés pour les messages XML binaires. Il s'agit de la plus efficace des options d'encodage, mais la moins interopérable, parce qu'elle est prise en charge uniquement par les points de terminaison [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   <<!--zz xref:System.ServiceModel.Channels.MTOMMessageEncodingBindingElement -->`System.ServiceModel.Channels.MTOMMessageEncodingBindingElement`> : représente l’élément de liaison qui spécifie l’encodage de caractères et le versioning de messages utilisés pour un message à l’aide d’un encodage de (Message Transmission Optimization Mechanism). MTOM est une technologie efficace pour la transmission de données binaires dans les messages [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. L'encodeur MTOM tente de parvenir à un équilibre entre rendement et interopérabilité. L'encodage MTOM transmet la plupart du XML sous forme textuelle, mais optimise les grands blocs de données binaires en les transmettant tels quels, sans conversion en texte.  
  
 L'élément de liaison crée un <xref:System.ServiceModel.Channels.MessageEncoderFactory> Binary, MTOM ou Text. La fabrique crée une instance <xref:System.ServiceModel.Channels.MessageEncoderFactory> Binary, MTOM ou Text. En général, il n'y a qu'une instance unique. Toutefois si des sessions sont utilisées, un encodeur différent peut être fourni à chaque session. L'encodeur Binary utilise celle-ci pour coordonner des dictionnaires dynamiques (consultez Infrastructure XML).  
  
 Les méthodes <xref:System.ServiceModel.Channels.MessageEncoder.ReadMessage%2A> et <xref:System.ServiceModel.Channels.MessageEncoder.WriteMessage%2A> sont les éléments principaux des encodeurs. Les méthodes permettent de lire un message d'un flux de données ou d'un tableau <xref:System.Byte>. Les tableaux d'octets sont utilisés lorsque le transport fonctionne en mode mémoire tampon. Les messages sont toujours écrits dans des flux de données. Si le transport doit mettre le message en mémoire tampon, il fournit un flux de données qui effectue la mise en mémoire tampon.  
  
 Le reste des membres utilisent le contenu de support, les types de média et <xref:System.ServiceModel.Channels.MessageEncoder.MessageVersion%2A>. Le transport appelle ces méthodes d'encodeur pour tester s'il peut décoder le message entrant ou pour déterminer si le message sortant est valide pour cet encodeur.  
  
 Chacune des trois implémentations d'encodeur ajoute des propriétés qui sont pertinentes aux encodages spécifiques et sont entièrement configurables. Les encodeurs exposent aussi des quotas de lecteur qui ont des valeurs sécurisées par défaut. Consultez Infrastructure XML pour une description des quotas.  
  
## <a name="features-of-system-provided-encoders"></a>Fonctionnalités des encodeurs fournis par le système  
 Les encodeurs fournis par le système offrent plusieurs fonctionnalités.  
  
### <a name="pooling"></a>Pooling  
 Chacune des implémentations d'encodeur essaient de regrouper autant que possible. La réduction d'allocations est un moyen clé pour améliorer les performances du code managé. Pour accomplir ce regroupement, les implémentations utilisent la classe `SynchronizedPool`. Le fichier C# contient une description des optimisations supplémentaires utilisées par cette classe.  
  
 Les instances `XmlDictionaryReader` et `XmlDictionaryWriter` sont regroupées et réinitialisées pour empêcher d'en allouer des nouvelles pour chaque message. Pour les lecteurs, un rappel `OnClose` récupère le lecteur lorsque `Close()` est appelé. L'encodeur recycle aussi certains objets de l'état du message utilisés pour construire des messages. Les tailles de ces regroupements sont configurables par les propriétés `MaxReadPoolSize` et `MaxWritePoolSize` sur chacune des trois classes dérivées de <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>.  
  
### <a name="binary-encoding"></a>Encodage Binaire  
 Lorsque l'encodage binaire utilise des sessions, la chaîne de dictionnaire dynamique doit être communiquée au récepteur du message. Cette opération s'effectue en préfixant le message avec les chaînes de dictionnaire dynamiques. Le récepteur supprime des chaînes, les ajoute à la session et traite le message. La transmission correcte des chaînes de dictionnaire nécessite la mise en mémoire tampon du transport.  
  
 Les chaînes sont ajoutées au message par une méthode `AddSessionInformationToMessage` interne. Elle ajoute les chaînes au format UTF-8 au début du message précédées de leur longueur. Puis l'en-tête entier de dictionnaire est préfixé avec la longueur de ses données. L'opération inverse est effectuée par une méthode interne `ExtractSessionInformationFromMessage`.  
  
 En plus de traiter des clés de dictionnaire dynamiques, les messages de session en mémoire tampon sont reçus d'une manière unique. Au lieu de créer un lecteur sur le document et de le traiter, l'encodeur binaire utilise la classe interne `MessagePatterns` pour déconstruire le flux binaire. L'idée est que la plupart des messages possède un certain jeu d'en-têtes qui apparaissent dans un certain ordre lorsqu'ils sont générés par [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Le système de modèle décompose le message en fonction de ce qu'il en attend. Si l'opération aboutie, il initialise un objet <xref:System.ServiceModel.Channels.MessageHeaders> sans analyser le XML. Dans le cas contraire, il revient à la méthode standard.  
  
### <a name="mtom-encoding"></a>MTOM Encoding  
 Le <<!--zz xref:System.ServiceModel.Channels.MTOMMessageEncodingBindingElement --> `System.ServiceModel.Channels.MTOMMessageEncodingBindingElement`> classe a une propriété de configuration supplémentaire appelée <<!--zz xref:System.ServiceModel.Channels.MTOMMessageEncodingBindingElement --> `System.ServiceModel.Channels.MTOMMessageEncodingBindingElement`. MaxBufferSize % 2 >. Celle-ci place une limite supérieure sur la quantité de données qu'il est possible de mettre en mémoire tampon pendant la lecture d'un message. Le jeu d'informations XML (Infoset), ou d'autres parties MIME, peuvent nécessiter leur mise en mémoire tampon pour réassembler toutes les parties MIME dans un message unique.  
  
 Pour fonctionner correctement avec HTTP, la classe d'encodeur de message MTOM interne fournit des API internes pour `GetContentType` (qui est aussi interne) et `WriteMessage` qui est public et peut être substitué. Il doit s'effectuer plus de communication pour que les valeurs dans les en-têtes HTTP soient conformes aux valeurs dans les en-têtes MIME.  
  
 En interne, l'encodeur de message MTOM utilise les lecteurs de texte de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], il est semblable à l'encodeur Text. La différence principale est qu'il optimise des segments importants de binaire, ou BLOB (Binary Large Objects) en ne les convertissant pas en encodage de base 64 avant d'être incorporé dans les octets de message. À la place, ces BLOB restent extraits et référencés comme des pièces jointes MIME.  
  
## <a name="writing-your-own-encoder"></a>Écriture de votre propre encodeur  
 Pour implémenter votre propre encodeur de message personnalisé, vous devez fournir des implémentations personnalisées des classes de base abstraites suivantes :  
  
-   <xref:System.ServiceModel.Channels.MessageEncoder>  
  
-   <xref:System.ServiceModel.Channels.MessageEncoderFactory>  
  
-   <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>  
  
 La conversion de la représentation en mémoire d'un message en une représentation qui peut être écrite dans un flux de données est encapsulée dans la classe <xref:System.ServiceModel.Channels.MessageEncoder> qui agit en tant que fabrique pour les lecteurs XML et writers XML qui prennent en charge des types spécifiques d'encodages XML.  
  
-   Les méthodes clés de cette classe que vous devez substituer sont :  
  
-   <xref:System.ServiceModel.Channels.MessageEncoder.WriteMessage%2A> qui accepte un objet <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> et l'écrit dans un objet <xref:System.IO.Stream>.  
  
-   <xref:System.ServiceModel.Channels.MessageEncoder.ReadMessage%2A> qui accepte un objet <xref:System.IO.Stream> et une taille d'en-tête maximale et retourne un objet <xref:System.ServiceModel.Channels.Message>.  
  
 C'est le code que vous écrivez dans ces méthodes qui gèrent la conversion entre le protocole de transport standard et votre encodage personnalisé.  
  
 Ensuite, vous devez coder une classe de fabrique qui crée votre encodeur personnalisé. Substituez <xref:System.ServiceModel.Channels.MessageEncoderFactory.Encoder%2A> pour retourner une instance de votre <xref:System.ServiceModel.Channels.MessageEncoder> personnalisé.  
  
 Puis connectez votre <xref:System.ServiceModel.Channels.MessageEncoderFactory> personnalisé à la pile d'élément de liaison utilisée pour configurer le service ou le client en substituant la méthode <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A> pour retourner une instance de cette fabrique.  
  
 Il existe deux exemples fournis avec [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] qui illustrent ce processus avec le code d’exemple : [encodeur de Message personnalisé : encodeur de texte personnalisé](../../../../docs/framework/wcf/samples/custom-message-encoder-custom-text-encoder.md) et [encodeur de Message personnalisé : encodeur de Compression](../../../../docs/framework/wcf/samples/custom-message-encoder-compression-encoder.md).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>  
 <xref:System.ServiceModel.Channels.MessageEncoderFactory>  
 <xref:System.ServiceModel.Channels.MessageEncoder>  
 [Présentation de l’architecture de transfert de données](../../../../docs/framework/wcf/feature-details/data-transfer-architectural-overview.md)  
 [Choix d’un encodeur de Message](../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)  
 [Choix d’un Transport](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)
