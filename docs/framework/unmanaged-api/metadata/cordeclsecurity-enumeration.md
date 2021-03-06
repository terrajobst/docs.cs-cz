---
title: CorDeclSecurity – výčet
ms.date: 03/30/2017
api_name:
- CorDeclSecurity
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorDeclSecurity
helpviewer_keywords:
- CorDeclSecurity enumeration [.NET Framework metadata]
ms.assetid: 864f1267-d267-4696-8df7-1f83f8444d6f
topic_type:
- apiref
ms.openlocfilehash: 98183ed02f8821b7c40852de2d040775d30f2518
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/23/2019
ms.locfileid: "74443742"
---
# <a name="cordeclsecurity-enumeration"></a>CorDeclSecurity – výčet
Určuje bezpečnostní akce, které lze provést pomocí deklarativního zabezpečení.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
typedef enum CorDeclSecurity {  
  
    dclActionMask               =   0x001f,  
    dclActionNil                =   0x0000,  
    dclRequest                  =   0x0001,  
    dclDemand                   =   0x0002,  
    dclAssert                   =   0x0003,  
    dclDeny                     =   0x0004,  
    dclPermitOnly               =   0x0005,  
    dclLinktimeCheck            =   0x0006,  
    dclInheritanceCheck         =   0x0007,  
    dclRequestMinimum           =   0x0008,  
    dclRequestOptional          =   0x0009,  
    dclRequestRefuse            =   0x000a,  
    dclPrejitGrant              =   0x000b,  
    dclPrejitDenied             =   0x000c,  
    dclNonCasDemand             =   0x000d,  
    dclNonCasLinkDemand         =   0x000e,  
    dclNonCasInheritance        =   0x000f,  
    dclLinkDemandChoice         =   0x0010,  
    dclInheritanceDemandChoice  =   0x0011,  
    dclDemandChoice             =   0x0012,  
    dclMaximumValue             =   0x0012  
  
} CorDeclSecurity;  
```  
  
## <a name="members"></a>Members  
  
|Člen|Popis|  
|------------|-----------------|  
|`dclActionMask`|Rezervovaný.|  
|`dclActionNil`|Rezervovaný.|  
|`dclRequest`|Rezervovaný.|  
|`dclDemand`|Všem volajícím vyšším v zásobníku volání je nutné udělit oprávnění určené aktuálním objektem oprávnění.|  
|`dclAssert`|Volající kód může přistupovat k prostředku identifikovanému aktuálním objektem oprávnění, a to i v případě, že by volajícím vyšším v zásobníku nebylo uděleno oprávnění pro přístup k prostředku.|  
|`dclDeny`|Možnost přístupu k prostředku určenému aktuálním objektem oprávnění je odepřena volajícím, i když jim byla udělena oprávnění k přístupu.|  
|`dclPermitOnly`|Přístup k prostředkům, které jsou určené tímto objektem oprávnění, lze získat i v případě, že byl kódu uděleno oprávnění k přístupu k jiným prostředkům.|  
|`dclLinktimeCheck`|Okamžitému volajícímu se musí udělit zadané oprávnění pro dané časové období.|  
|`dclInheritanceCheck`|Odvozená třída, která dědí jinou třídu nebo k přepsání metody, je vyžadována pro udělení zadaného oprávnění.|  
|`dclRequestMinimum`|Volající může požadovat minimální oprávnění, která jsou požadována ke spuštění kódu. Tuto akci lze použít pouze v rámci oboru sestavení.|  
|`dclRequestOptional`|Volající může požádat o další oprávnění, která jsou volitelná (nevyžadují se ke spuštění). Tento požadavek implicitně odmítne všechna ostatní oprávnění, která nejsou výslovně požadována. Tuto akci lze použít pouze v rámci oboru sestavení.|  
|`dclRequestRefuse`|Žádost volajícího o oprávnění, která by mohla být nepoužitá, nebude udělena. Tuto akci lze použít pouze v rámci oboru sestavení.|  
|`dclPrejitGrant`|Rezervovaný.|  
|`dclPrejitDenied`|Rezervovaný.|  
|`dclNonCasDemand`|Rezervovaný.|  
|`dclNonCasLinkDemand`|K tomuto okamžitému volajícímu se musí udělit zadané oprávnění.|  
|`dclNonCasInheritance`|Rezervovaný.|  
|`dclLinkDemandChoice`|Rezervovaný.|  
|`dclInheritanceDemandChoice`|Rezervovaný.|  
|`dclDemandChoice`|Rezervovaný.|  
|`dclMaximumValue`|Rezervovaný.|  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** CorHdr. h  
  
 **Verze .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [Výčty pro metadata](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
