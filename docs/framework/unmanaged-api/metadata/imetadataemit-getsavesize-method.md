---
title: IMetaDataEmit::GetSaveSize – metoda
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.GetSaveSize
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::GetSaveSize
helpviewer_keywords:
- IMetaDataEmit::GetSaveSize method [.NET Framework metadata]
- GetSaveSize method [.NET Framework metadata]
ms.assetid: 8aea2e2c-23a3-4cda-9a06-e19f97383830
topic_type:
- apiref
ms.openlocfilehash: 125a63638a41707b8eed918253cb1f93abb907eb
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/23/2019
ms.locfileid: "74434332"
---
# <a name="imetadataemitgetsavesize-method"></a>IMetaDataEmit::GetSaveSize – metoda
Získá odhadovanou binární velikost sestavení a jeho metadat v aktuálním oboru.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT GetSaveSize (  
    [in]  CorSaveSize fSave,  
    [out] DWORD       *pdwSaveSize  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `fSave`  
 pro Hodnota výčtu [CorSaveSize –](../../../../docs/framework/unmanaged-api/metadata/corsavesize-enumeration.md) , která určuje, zda má být získána přesná nebo Přibližná velikost. Platné jsou jenom tři hodnoty: cssAccurate, cssQuick a cssDiscardTransientCAs:  
  
- cssAccurate vrací přesný formát pro uložení, ale trvá déle, než se vypočítá.  
  
- cssQuick vrací velikost, doplněnou z důvodu bezpečnosti, ale pro výpočet trvá méně času.  
  
- cssDiscardTransientCAs informuje `GetSaveSize`, že může vyvolat nepřítomné vlastní atributy.  
  
 `pdwSaveSize`  
 mimo Ukazatel na velikost, která je nutná k uložení souboru.  
  
## <a name="remarks"></a>Poznámky  
 `GetSaveSize` vypočítá požadované místo v bajtech pro uložení sestavení a všech jeho metadat v aktuálním oboru. (Volání metody [IMetaDataEmit:: SaveToStream –](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-savetostream-method.md) vygenerovalo tento počet bajtů.)  
  
 Pokud volající implementuje rozhraní [IMapToken –](../../../../docs/framework/unmanaged-api/metadata/imaptoken-interface.md) (prostřednictvím [IMetaDataEmit:: SetHandler –](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-sethandler-method.md) nebo [IMetaDataEmit:: Merge](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-merge-method.md)), `GetSaveSize` provede dva průchody metadaty za účelem optimalizace a komprimace. V opačném případě se neprovede žádné optimalizace.  
  
 Pokud je provedena optimalizace, první průchod jednoduše seřadí struktury metadat a optimalizuje výkon při importu. Tento krok obvykle má za následek přesun záznamů s vedlejším účinkem, kdy jsou tokeny uchovávané nástrojem pro budoucí odkazy neověřené. Metadata neoznamují volajícím těchto změn tokenů do té doby, než je však druhý úspěch. Ve druhém průchodu se provede několik optimalizací, které mají omezit celkovou velikost metadat, jako je například optimalizace nepřítomnosti (předčasný vazba) `mdTypeRef` a `mdMemberRef` tokeny, pokud je odkaz na typ nebo člen deklarovaný v aktuálním oboru metadat. V tomto průchodu dojde k dalšímu zaokrouhlení mapování tokenů. Po tomto průchodu modul metadata Engine upozorní volajícího prostřednictvím jeho `IMapToken`ho rozhraní o jakékoli změněné hodnoty tokenu.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** Cor. h  
  
 **Knihovna:** Používá se jako prostředek v knihovně MSCorEE. dll.  
  
 **Verze .NET Framework:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [IMetaDataEmit – rozhraní](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 – rozhraní](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
