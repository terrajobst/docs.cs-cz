---
title: ICLRTask::SwitchIn – metoda
ms.date: 03/30/2017
api_name:
- ICLRTask.SwitchIn
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask::SwitchIn
helpviewer_keywords:
- ICLRTask::SwitchIn method [.NET Framework hosting]
- SwitchIn method [.NET Framework hosting]
ms.assetid: 3d37ce20-aa65-4043-8f13-7c728b5d8a52
topic_type:
- apiref
ms.openlocfilehash: fbfd44c8e20bc75638d6356fe405f02790da8ac7
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2019
ms.locfileid: "73124609"
---
# <a name="iclrtaskswitchin-method"></a>ICLRTask::SwitchIn – metoda
Upozorní modul CLR (Common Language Runtime) na to, že úloha, kterou aktuální instance [ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) představuje, je teď v provozuschopném stavu.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT SwitchIn (  
    [in] HANDLE threadHandle  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `threadHandle`  
 pro Popisovač fyzického vlákna, na kterém je spuštěna úloha reprezentovaná aktuální instancí `ICLRTask`.  
  
## <a name="return-value"></a>Návratová hodnota  
  
|HRESULT|Popis|  
|-------------|-----------------|  
|S_OK|`SwitchIn` byla úspěšně vrácena.|  
|HOST_E_CLRNOTAVAILABLE|Modul CLR nebyl načten do procesu, nebo je modul CLR ve stavu, ve kterém nemůže spustit spravovaný kód nebo úspěšně zpracovat volání.|  
|HOST_E_TIMEOUT|Vypršel časový limit volání.|  
|HOST_E_NOT_OWNER|Volající nevlastní zámek.|  
|HOST_E_ABANDONED|Událost byla zrušena při čekání na blokované vlákno nebo vlákna.|  
|E_FAIL|Došlo k neznámé chybě závažnosti. Když metoda vrátí E_FAIL, CLR již není v rámci procesu použitelný. Následná volání metod hostování vrací HOST_E_CLRNOTAVAILABLE.|  
|HOST_E_INVALIDOPERATION|`SwitchIn` byla volána bez předchozího volání [metody Switch](../../../../docs/framework/unmanaged-api/hosting/iclrtask-switchout-method.md).|  
  
## <a name="remarks"></a>Poznámky  
 Parametr `threadHandle` představuje popisovač vlákna operačního systému, na kterém je naplánována úloha reprezentovaná aktuální instancí `ICLRTask`. Pokud došlo k zosobnění v tomto vláknu, musíte před přepnutím do úlohy zavolat [IHostSecurityManager:: RevertToSelf –](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-reverttoself-method.md) .  
  
> [!NOTE]
> Volání `SwitchIn` bez předchozího volání `SwitchOut` se nezdařila s hodnotou HRESULT HOST_E_INVALIDOPERATION.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** MSCorEE. h  
  
 **Knihovna:** Zahrnuto jako prostředek v knihovně MSCorEE. dll  
  
 **Verze .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [ICLRTask – rozhraní](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager – rozhraní](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask – rozhraní](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager – rozhraní](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
