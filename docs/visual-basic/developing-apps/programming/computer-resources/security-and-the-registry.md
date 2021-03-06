---
title: Zabezpečení a registr
ms.date: 07/20/2015
helpviewer_keywords:
- security [Visual Basic], registry
- registry [Visual Basic], security issues
ms.assetid: 9980aff7-2f69-492b-8f66-29a9a76d3df5
ms.openlocfilehash: 454180207d6432e80d87941d1f329f2a4ea7a801
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2020
ms.locfileid: "74345484"
---
# <a name="security-and-the-registry-visual-basic"></a>Zabezpečení a registr (Visual Basic)

Tato stránka popisuje bezpečnostní důsledky ukládání dat v registru.  
  
## <a name="permissions"></a>Oprávnění  

 Není bezpečné ukládat tajné klíče, například hesla, do registru jako prostý text, i v případě, že klíč registru je chráněn seznamy ACL (seznamy řízení přístupu).  
  
 Práce s registrem může ohrozit zabezpečení povolením nevhodného přístupu k systémovým prostředkům nebo chráněným informacím. Chcete-li použít tyto vlastnosti, musíte <xref:System.Security.Permissions.RegistryPermissionAccess> mít oprávnění ke čtení a zápisu z výčtu, který řídí přístup k proměnným registru. Jakýkoli kód spuštěný s úplným vztahem důvěryhodnosti (podle výchozích zásad zabezpečení se jedná o libovolný kód nainstalovaný na místním pevném disku uživatele) má potřebná oprávnění pro přístup k registru. Další informace naleznete <xref:System.Security.Permissions.RegistryPermission> v tématu class.  
  
 Proměnné registru by neměly být uloženy <xref:System.Security.Permissions.RegistryPermission> v umístění v paměti, kde kód bez přístupu k nim. Podobně při udělování oprávnění udělte minimální oprávnění potřebná k dokončení úlohy.  
  
 Hodnoty přístupu k oprávnění <xref:System.Security.Permissions.RegistryPermissionAccess> registru jsou definovány výčet. V následující tabulce jsou uvedeny její členy.  
  
|Hodnota|Přístup k proměnným registru|  
|-----------|----------------------------------|  
|`AllAccess`|Vytváření, čtení a zápis|  
|`Create`|Vytvořit|  
|`NoAccess`|Bez přístupu|  
|`Read`|Čtení|  
|`Write`|Zápis|  
  
## <a name="checking-values-in-registry-keys"></a>Kontrola hodnot v klíčích registru  

 Při vytváření hodnoty registru se musíte rozhodnout, co dělat, pokud tato hodnota již existuje. Jiný proces, možná škodlivý, může mít již vytvořilhodnotu a mají k ní přístup. Když vložíte data do hodnoty registru, data jsou k dispozici pro jiný proces. Chcete-li tomu `GetValue` zabránit, použijte metodu. Vrátí, `Nothing` pokud klíč ještě neexistuje.  
  
> [!IMPORTANT]
> Při čtení registru z webové aplikace závisí identita aktuálního uživatele na ověřování a zosobnění implementovaném ve webové aplikaci.  
  
## <a name="see-also"></a>Viz také

- <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>
- [Čtení z registru a zápis do něj](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)
