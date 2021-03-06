---
title: Hledání deklarací v sadě deklarací
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- claims [WCF], finding in a claimset
- claims [WCF]
ms.assetid: a76ce107-aeb3-47d0-bfa9-134c53664e20
ms.openlocfilehash: 42e6ee682220913f872da337eb41f6c290082988
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "61856421"
---
# <a name="finding-claims-in-a-claimset"></a>Hledání deklarací v sadě deklarací
Zkoumání obsahu <xref:System.IdentityModel.Claims.ClaimSet> pro konkrétní typy deklarací, které je běžné úlohy při použití ověřování na základě deklarací identity. K prozkoumání <xref:System.IdentityModel.Claims.ClaimSet> přítomnosti konkrétních deklarací identit, použijte <xref:System.IdentityModel.Claims.ClaimSet.FindClaims%2A> metody. Tato metoda poskytuje lepší výkon než iterace přímo přes <xref:System.IdentityModel.Claims.ClaimSet>. Následující příklad ukazuje použití těchto. Všimněte si, že `claimType` a `claimRight` může být parametry `null`. Parametry v takovém případě bude odpovídat všechny typy deklarací identity a deklarací identity práva.  
  
## <a name="example"></a>Příklad  
 [!code-csharp[c_FindClaimsPerf#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_findclaimsperf/cs/c_findclaimsperf.cs#2)]
 [!code-vb[c_FindClaimsPerf#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_findclaimsperf/vb/c_findclaimsperf.vb#2)]  
  
## <a name="see-also"></a>Viz také:

- [Správa deklarací identity a autorizace pomocí modelu identit](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)
