---
title: "CloneEnumWbemClassObject (fonction) (référence des API non managées)"
description: "La fonction CloneEnumWbemClassObject effectue une copie logique d’un énumérateur."
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: reference
api_name: CloneEnumWbemClassObject
api_location: WMINet_Utils.dll
api_type: DLLExport
f1_keywords: CloneEnumWbemClassObject
helpviewer_keywords: CloneEnumWbemClassObject function [.NET WMI and performance counters]
topic_type: Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 7a4103a0103a334a0e5eace32d8fcf1b365917b8
ms.sourcegitcommit: a53799f81351ad9afb3007cd68846ce6aeeb10cb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2017
---
# <a name="cloneenumwbemclassobject-function"></a><span data-ttu-id="a94e2-103">CloneEnumWbemClassObject (fonction)</span><span class="sxs-lookup"><span data-stu-id="a94e2-103">CloneEnumWbemClassObject function</span></span>
<span data-ttu-id="a94e2-104">Effectue une copie logique d’un énumérateur, en conservant sa position actuelle dans une énumération.</span><span class="sxs-lookup"><span data-stu-id="a94e2-104">Makes a logical copy of an enumerator, retaining its current position in an enumeration.</span></span>  
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a><span data-ttu-id="a94e2-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a94e2-105">Syntax</span></span>  
  
```  
HRESULT CloneEnumWbemClassObject (
   [out] IEnumWbemClassObject**  ppEnum, 
   [in] DWORD                    authLevel,
   [in] DWORD                    impLevel,
   [in] IEnumWbemClassObject*    pCurrentEnumWbemClassObject, 
   [in] BSTR                     strUser,
   [in] BSTR                     strPassword,
   [in BSTR]                     strAuthority 
); 
```  

## <a name="parameters"></a><span data-ttu-id="a94e2-106">Paramètres</span><span class="sxs-lookup"><span data-stu-id="a94e2-106">Parameters</span></span>

`ppEnum`  
<span data-ttu-id="a94e2-107">[out] Reçoit un pointeur vers un nouveau [IEnumWbemClassObject](https://msdn.microsoft.com/library/aa390857(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="a94e2-107">[out] Receives a pointer to a new [IEnumWbemClassObject](https://msdn.microsoft.com/library/aa390857(v=vs.85).aspx).</span></span>

`authLevel`  
<span data-ttu-id="a94e2-108">[in] Le niveau d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="a94e2-108">[in] The authorization level.</span></span>

<span data-ttu-id="a94e2-109">`impLevel`[in] Le niveau d’emprunt d’identité.</span><span class="sxs-lookup"><span data-stu-id="a94e2-109">`impLevel` [in] The impersonation level.</span></span>

`pCurrentEnumWbemClassObject`  
<span data-ttu-id="a94e2-110">[out] Un pointeur vers le [IEnumWbemClassObject](https://msdn.microsoft.com/library/aa390857(v=vs.85).aspx) instance à cloner.</span><span class="sxs-lookup"><span data-stu-id="a94e2-110">[out] A pointer to the [IEnumWbemClassObject](https://msdn.microsoft.com/library/aa390857(v=vs.85).aspx) instance to be cloned.</span></span>

`strUser`   
<span data-ttu-id="a94e2-111">[in] Le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a94e2-111">[in] The user name.</span></span> <span data-ttu-id="a94e2-112">Consultez le [ConnectServerWmi](connectserverwmi.md) (fonction) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a94e2-112">See the [ConnectServerWmi](connectserverwmi.md) function for more information.</span></span>

`strPassword`   
<span data-ttu-id="a94e2-113">[in] Le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a94e2-113">[in] The password.</span></span> <span data-ttu-id="a94e2-114">Consultez le [ConnectServerWmi](connectserverwmi.md) (fonction) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a94e2-114">See the [ConnectServerWmi](connectserverwmi.md) function for more information.</span></span>

`strAuthority`   
<span data-ttu-id="a94e2-115">[in] Le nom de domaine de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a94e2-115">[in] The domain name of the user.</span></span> <span data-ttu-id="a94e2-116">Consultez le [ConnectServerWmi](connectserverwmi.md) (fonction) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a94e2-116">See the [ConnectServerWmi](connectserverwmi.md) function for more information.</span></span>

## <a name="return-value"></a><span data-ttu-id="a94e2-117">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="a94e2-117">Return value</span></span>

<span data-ttu-id="a94e2-118">Les valeurs suivantes est retournées par cette fonction sont définies dans le *WbemCli.h* fichier d’en-tête, ou vous pouvez les définir en tant que constantes dans votre code :</span><span class="sxs-lookup"><span data-stu-id="a94e2-118">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="a94e2-119">Constante</span><span class="sxs-lookup"><span data-stu-id="a94e2-119">Constant</span></span>  |<span data-ttu-id="a94e2-120">Valeur</span><span class="sxs-lookup"><span data-stu-id="a94e2-120">Value</span></span>  |<span data-ttu-id="a94e2-121">Description</span><span class="sxs-lookup"><span data-stu-id="a94e2-121">Description</span></span>  |
|---------|---------|---------|
| `WBEM_E_FAILED` | <span data-ttu-id="a94e2-122">0 x 80041001</span><span class="sxs-lookup"><span data-stu-id="a94e2-122">0x80041001</span></span> | <span data-ttu-id="a94e2-123">Il a été un échec général.</span><span class="sxs-lookup"><span data-stu-id="a94e2-123">There has been a general failure.</span></span> |
| `WBEM_E_INVALID_PARAMETER` | <span data-ttu-id="a94e2-124">0 x 80041008</span><span class="sxs-lookup"><span data-stu-id="a94e2-124">0x80041008</span></span> | <span data-ttu-id="a94e2-125">Un paramètre n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="a94e2-125">A parameter is invalid.</span></span> |
| `WBEM_E_OUT_OF_MEMORY` | <span data-ttu-id="a94e2-126">0x80041006</span><span class="sxs-lookup"><span data-stu-id="a94e2-126">0x80041006</span></span> | <span data-ttu-id="a94e2-127">Pas assez de mémoire est disponible terminer l’opération.</span><span class="sxs-lookup"><span data-stu-id="a94e2-127">Not enough memory is available complete the operation.</span></span> |
| `WBEM_E_TRANSPORT_FAILURE` | <span data-ttu-id="a94e2-128">0x80041015</span><span class="sxs-lookup"><span data-stu-id="a94e2-128">0x80041015</span></span> | <span data-ttu-id="a94e2-129">Le lien de remote procedure call (RPC) entre les processus en cours et WMI a échoué.</span><span class="sxs-lookup"><span data-stu-id="a94e2-129">The remote procedure call (RPC) link between the current process and WMI has failed.</span></span> |
| `WBEM_S_NO_ERROR` | <span data-ttu-id="a94e2-130">0</span><span class="sxs-lookup"><span data-stu-id="a94e2-130">0</span></span> | <span data-ttu-id="a94e2-131">L’appel de fonction a réussi.</span><span class="sxs-lookup"><span data-stu-id="a94e2-131">The function call was successful.</span></span>  |
  
## <a name="remarks"></a><span data-ttu-id="a94e2-132">Remarques</span><span class="sxs-lookup"><span data-stu-id="a94e2-132">Remarks</span></span>

<span data-ttu-id="a94e2-133">Cette fonction encapsule un appel à la [IEnumWbemClassObject::Clone](https://msdn.microsoft.com/library/aa390859(v=vs.85).aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="a94e2-133">This function wraps a call to the [IEnumWbemClassObject::Clone](https://msdn.microsoft.com/library/aa390859(v=vs.85).aspx) method.</span></span>

<span data-ttu-id="a94e2-134">Cette méthode ne permet qu’une copie « meilleur effort ».</span><span class="sxs-lookup"><span data-stu-id="a94e2-134">This method makes only a "best effort" copy.</span></span> <span data-ttu-id="a94e2-135">En raison de la nature dynamique de nombreux objets CIM, il est possible que le nouvel énumérateur n’énumère pas le même jeu d’objets que l’énumérateur de la source.</span><span class="sxs-lookup"><span data-stu-id="a94e2-135">Due to the dynamic nature of many CIM objects, it is possible that the new enumerator does not enumerate the same set of objects as the source enumerator.</span></span>  

<span data-ttu-id="a94e2-136">Si l’appel de fonction échoue, vous pouvez obtenir des informations d’erreur supplémentaires en appelant le [GetErrorInfo](geterrorinfo.md) (fonction).</span><span class="sxs-lookup"><span data-stu-id="a94e2-136">If the function call fails, you can obtain additional error information by calling the [GetErrorInfo](geterrorinfo.md) function.</span></span>

## <a name="example"></a><span data-ttu-id="a94e2-137">Exemple</span><span class="sxs-lookup"><span data-stu-id="a94e2-137">Example</span></span>

<span data-ttu-id="a94e2-138">Pour obtenir un exemple, consultez la [IEnumWbemClassObject::Clone](https://msdn.microsoft.com/library/aa390859(v=vs.85).aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="a94e2-138">For an example, see the [IEnumWbemClassObject::Clone](https://msdn.microsoft.com/library/aa390859(v=vs.85).aspx) method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a94e2-139">Spécifications</span><span class="sxs-lookup"><span data-stu-id="a94e2-139">Requirements</span></span>  
 <span data-ttu-id="a94e2-140">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a94e2-140">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a94e2-141">**En-tête :** WMINet_Utils.idl</span><span class="sxs-lookup"><span data-stu-id="a94e2-141">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="a94e2-142">**Versions du .NET framework :**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="a94e2-142">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a94e2-143">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a94e2-143">See also</span></span>  
[<span data-ttu-id="a94e2-144">WMI et les compteurs de Performance (référence des API non managées)</span><span class="sxs-lookup"><span data-stu-id="a94e2-144">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)