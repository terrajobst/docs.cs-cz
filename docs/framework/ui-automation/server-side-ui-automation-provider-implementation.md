---
title: Implementace zprostředkovatele automatizace uživatelského rozhraní na straně serveru
ms.date: 03/30/2017
helpviewer_keywords:
- server-side UI Automation provider implementation
- UI Automation, server-side provider implementation
- provider implementation, UI Automation
ms.assetid: 6acc6d08-bd67-4e2e-915c-9c1d34eb86fe
ms.openlocfilehash: 8a52d84f7152b9cb431ad0aa97c88b143463be2d
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76789615"
---
# <a name="server-side-ui-automation-provider-implementation"></a>Implementace zprostředkovatele automatizace uživatelského rozhraní na straně serveru

> [!NOTE]
> Tato dokumentace je určena pro .NET Framework vývojářů, kteří chtějí používat spravované [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] třídy definované v oboru názvů <xref:System.Windows.Automation>. Nejnovější informace o [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]najdete v tématu [rozhraní API pro Windows Automation: automatizace uživatelského rozhraní](/windows/win32/winauto/entry-uiauto-win32).

Tato část popisuje, jak implementovat zprostředkovatele automatizace uživatelského rozhraní na straně serveru pro vlastní ovládací prvek.

Implementace pro prvky Windows Presentation Foundation (WPF) a non-WPF elementy (například ty, které jsou navrženy pro model Windows Forms), jsou zásadním rozdílem. Prvky WPF poskytují podporu pro [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] prostřednictvím třídy odvozené z <xref:System.Windows.Automation.Peers.AutomationPeer>. Prvky jiného typu než WPF poskytují podporu prostřednictvím implementací rozhraní poskytovatele.

<a name="Security_Considerations"></a>

## <a name="security-considerations"></a>Důležité informace o zabezpečení

Poskytovatelé by měli být zapsáni tak, aby mohli pracovat v prostředí s částečným vztahem důvěryhodnosti. Vzhledem k tomu, že UIAutomationClient. dll není nakonfigurován tak, aby běžel v rámci částečné důvěryhodnosti, váš kód poskytovatele by neměl odkazovat na toto sestavení. Pokud ano, může kód běžet v prostředí s plnou důvěryhodností, ale pak selže v prostředí s částečnou důvěryhodností.

Konkrétně nepoužívejte pole z tříd v UIAutomationClient. dll, jako jsou ta v <xref:System.Windows.Automation.AutomationElement>. Místo toho použijte ekvivalentní pole z tříd v UIAutomationTypes. dll, například <xref:System.Windows.Automation.AutomationElementIdentifiers>.

<a name="Provider_Implementation_by_WPF_Elements"></a>

## <a name="provider-implementation-by-windows-presentation-foundation-elements"></a>Implementace poskytovatele pomocí Windows Presentation Foundationch prvků

Další informace o tomto tématu naleznete v tématu [automatizace uživatelského rozhraní vlastního ovládacího prvku WPF](../wpf/controls/ui-automation-of-a-wpf-custom-control.md).

<a name="Provider_Implementation_by_non_WPF_Elements"></a>

## <a name="provider-implementation-by-non-wpf-elements"></a>Implementace poskytovatele pomocí elementů, které nejsou WPF

Vlastní ovládací prvky, které nejsou součástí architektury WPF, ale které jsou napsány ve spravovaném kódu (nejčastěji se jedná o model Windows Forms ovládacích prvků), poskytují podporu pro [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] implementací rozhraní. Každý prvek musí implementovat alespoň jedno rozhraní uvedené v první tabulce v následující části. Kromě toho, pokud prvek podporuje jeden nebo více vzorů ovládacích prvků, musí implementovat příslušné rozhraní pro každý model ovládacího prvku.

Váš projekt poskytovatele [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] musí odkazovat na následující sestavení:

- UIAutomationProviders.dll

- UIAutomationTypes.dll

- WindowsBase.dll

<a name="Provider_Interfaces"></a>

### <a name="provider-interfaces"></a>Rozhraní poskytovatele

Každý poskytovatel [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] musí implementovat jedno z následujících rozhraní.

|Rozhraní|Popis|
|---------------|-----------------|
|<xref:System.Windows.Automation.Provider.IRawElementProviderSimple>|Poskytuje funkce pro jednoduchý ovládací prvek hostovaný v okně, včetně podpory vzorů a vlastností ovládacích prvků.|
|<xref:System.Windows.Automation.Provider.IRawElementProviderFragment>|Dědí z <xref:System.Windows.Automation.Provider.IRawElementProviderSimple>. Přidává funkce pro element ve složitém ovládacím prvku, včetně navigace v rámci fragmentu, nastavení fokusu a vrácení ohraničujícího obdélníku elementu.|
|<xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>|Dědí z <xref:System.Windows.Automation.Provider.IRawElementProviderFragment>. Přidává funkce pro kořenový prvek ve složitém ovládacím prvku, včetně vyhledání podřízeného prvku na zadaných souřadnicích a nastavení stavu fokusu pro celý ovládací prvek.|

Následující rozhraní poskytují přidané funkce, ale není nutné je implementovat.

|Rozhraní|Popis|
|---------------|-----------------|
|<xref:System.Windows.Automation.Provider.IRawElementProviderAdviseEvents>|Umožňuje poskytovateli sledovat požadavky na události.|
|<xref:System.Windows.Automation.Provider.IRawElementProviderHwndOverride>|Umožňuje přemístit prvky založené na oknech v rámci [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stromu fragmentu.|

Všechna ostatní rozhraní v oboru názvů <xref:System.Windows.Automation.Provider> jsou pro podporu vzorů ovládacích prvků.

<a name="Requirements_for_Non_WPF_Providers"></a>

### <a name="requirements-for-non-wpf-providers"></a>Požadavky na zprostředkovatele jiných výrobců než WPF

Aby bylo možné komunikovat s [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], musí váš ovládací prvek implementovat následující hlavní oblasti funkčnosti:

|Funkce|Implementace|
|-------------------|--------------------|
|Vystavení poskytovatele pro [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|V reakci na WM_GETOBJECT zprávu odeslanou oknu ovládacího prvku vrátí objekt, který implementuje <xref:System.Windows.Automation.Provider.IRawElementProviderSimple> (nebo odvozené rozhraní). U fragmentů musí být to zprostředkovatel pro kořen fragmentu.|
|Zadejte hodnoty vlastností.|Implementujte <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPropertyValue%2A> k poskytnutí nebo přepsání hodnot.|
|Povolení interakce klienta s ovládacím prvkem|Implementujte rozhraní, která podporují vzory ovládacích prvků, jako je <xref:System.Windows.Automation.Provider.IInvokeProvider>. Vrátí tyto poskytovatele vzorů v implementaci <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPatternProvider%2A>.|
|Vyvolat události|Zavolejte jednu ze statických metod <xref:System.Windows.Automation.Provider.AutomationInteropProvider> k vyvolání události, na kterou může klient naslouchat.|
|Povolit navigaci a zaostření v rámci fragmentu|Implementujte <xref:System.Windows.Automation.Provider.IRawElementProviderFragment> pro každý prvek v rámci fragmentu. (Není nutné pro prvky, které nejsou součástí fragmentu.)|
|Povolit zaostření a umístění podřízeného prvku v fragmentu|Implementujte <xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>. (Není nutné pro prvky, které nefragmentují kořeny.)|

<a name="Property_Values_in_Non_WPF_Providers"></a>

### <a name="property-values-in-non-wpf-providers"></a>Hodnoty vlastností v jiných zprostředkovatelích než WPF

poskytovatelé [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] pro vlastní ovládací prvky musí podporovat některé vlastnosti, které může použít systém automatizace a také klientské aplikace. Pro prvky, které jsou hostovány ve Windows (HWND), může [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] načíst některé vlastnosti z výchozího poskytovatele Windows, ale musí si od vlastního poskytovatele získat jiné.

Zprostředkovatelé pro ovládací prvky na bázi HWND nemusejí obvykle zadávat následující vlastnosti (identifikované hodnotami polí):

- <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.ProcessIdProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.ClassNameProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.HasKeyboardFocusProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.IsPasswordProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.RuntimeIdProperty>

> [!NOTE]
> Z okna se získá <xref:System.Windows.Automation.AutomationElementIdentifiers.RuntimeIdProperty> jednoduchého prvku nebo kořen fragmentu, který je hostovaný v okně. prvky fragmentů pod kořenem (například položky seznamu v poli seznam) však musí poskytovat své vlastní identifikátory. Další informace najdete v tématu <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.GetRuntimeId%2A>.
>
> <xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty> by měl být vrácen pro poskytovatele hostované v ovládacím prvku model Windows Forms. V takovém případě nemůže být ve výchozím zprostředkovateli Windows načtena správná hodnota.
>
> <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> obvykle dodává poskytovatel hostitele. Například pokud je vlastní ovládací prvek odvozen od <xref:System.Windows.Forms.Control>, název je odvozen z vlastnosti `Text` ovládacího prvku.

Příklad kódu naleznete v tématu [návratové vlastnosti ze zprostředkovatele automatizace uživatelského rozhraní](return-properties-from-a-ui-automation-provider.md).

<a name="Events_in_Non_WPF_Providers"></a>

### <a name="events-in-non-wpf-providers"></a>Události v jiných zprostředkovatelích než WPF

poskytovatelé [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] by měli vyvolat události, které upozorňují klientské aplikace na změny ve stavu uživatelského rozhraní. Následující metody slouží k vyvolání událostí.

|Metoda|Popis|
|------------|-----------------|
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.RaiseAutomationEvent%2A>|Vyvolává různé události, včetně událostí aktivovaných vzorci ovládacích prvků.|
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.RaiseAutomationPropertyChangedEvent%2A>|Vyvolá událost, když se změní vlastnost [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.RaiseStructureChangedEvent%2A>|Vyvolá událost při změně struktury stromu [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. například odebráním nebo přidáním prvku.|

Účelem události je upozornit klienta na něco, co se [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)], a to bez ohledu na to, jestli je aktivita aktivovaná [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]m systémem. Například událost identifikovaná <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent> by měla být vyvolána při každém vyvolání ovládacího prvku, buď prostřednictvím přímého vstupu uživatele, nebo klientské aplikace, která volá <xref:System.Windows.Automation.InvokePattern.Invoke%2A>.

Pro optimalizaci výkonu může poskytovatel selektivně vyvolat události nebo vyvolat žádné události, pokud není pro jejich příjem registrována žádná klientská aplikace. Pro optimalizaci se používají následující metody.

|Metoda|Popis|
|------------|-----------------|
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.ClientsAreListening%2A>|Tato statická vlastnost určuje, jestli se některé klientské aplikace přihlásily k odběru [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]ch událostí.|
|<xref:System.Windows.Automation.Provider.IRawElementProviderAdviseEvents>|Implementace poskytovatele tohoto rozhraní v kořenovém adresáři fragmentů umožňuje, aby bylo doporučeno, aby klienti zaregistrovali a zrušili registraci obslužných rutin událostí pro události v fragmentu.|

<a name="Non_WPF_Provider_Navigation"></a>

### <a name="non-wpf-provider-navigation"></a>Navigace od jiného poskytovatele než WPF

Poskytovatelé jednoduchých ovládacích prvků, jako je vlastní tlačítko hostovaná v okně (HWND), nepotřebují podporovat navigaci v rámci [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stromu. Navigace do a z prvku je zpracována výchozím poskytovatelem pro hostitelské okno, které je určeno v implementaci <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A>. Při implementaci poskytovatele pro komplexní vlastní ovládací prvek je však nutné podporovat navigaci mezi kořenovým uzlem fragmentu a jeho následníky a mezi uzly na stejné úrovni.

> [!NOTE]
> Prvky jiné fragmenty než kořenového adresáře musí vracet `null` odkaz z <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A>, protože nejsou přímo hostovány v okně a žádný výchozí zprostředkovatel nemůže podporovat navigaci na a z nich.

Struktura fragmentu je určena vaší implementací <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.Navigate%2A>. Pro každý možný směr z každého fragmentu vrátí tato metoda objekt Provider pro element v tomto směru. Pokud v tomto směru není žádný element, metoda vrátí odkaz `null`.

Kořen fragmentu podporuje navigaci pouze na podřízené elementy. Například seznam pole vrátí první položku v seznamu, když je směr <xref:System.Windows.Automation.Provider.NavigateDirection.FirstChild>, a poslední položku, když je směr <xref:System.Windows.Automation.Provider.NavigateDirection.LastChild>. Kořen fragmentu nepodporuje navigaci na nadřazený objekt nebo na stejné úrovni. to zpracovává poskytovatel hostitelského okna.

Prvky fragmentu, které nejsou kořenem, musí podporovat navigaci na nadřazený objekt a na všechny členy na stejné úrovni a podřízené objekty.

<a name="Non_WPF_Provider_Reparenting"></a>

### <a name="non-wpf-provider-reparenting"></a>Opětovné řazení poskytovatele WPF Provider

Automaticky otevíraná okna jsou ve skutečnosti okna nejvyšší úrovně, takže ve výchozím nastavení se ve stromové struktuře [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] jako podřízené položky plochy. V mnoha případech jsou však automaticky otevíraná okna logicky podřízeny nějakému jinému ovládacímu prvku. Například rozevírací seznam pole se seznamem je logicky podřízenou položkou pole se seznamem. Podobně automaticky otevírané okno nabídky je logicky podřízenou položkou nabídky. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] poskytuje podporu pro nadřízená překryvná okna tak, aby se zobrazila jako podřízená položka přidruženého ovládacího prvku.

Postup pro opětovné vytvoření nadřazeného okna:

1. Vytvořte poskytovatele pro místní okno. To vyžaduje, aby byla třída místního okna známa předem.

2. Implementujte všechny vlastnosti a vzory obvyklým způsobem pro automaticky otevírané okno, jako by šlo o ovládací prvek sám o sobě.

3. Implementujte vlastnost <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A> tak, aby vracela hodnotu získanou z <xref:System.Windows.Automation.Provider.AutomationInteropProvider.HostProviderFromHandle%2A>, kde parametr je obslužná rutina okna v místním okně.

4. Implementujte <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.Navigate%2A> pro automaticky otevírané okno a jeho nadřazený ovládací prvek tak, aby se navigace správně zpracovala z logického nadřazeného objektu na logické podřízené objekty a mezi podřízenými položkami na stejné úrovni.

Když [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] narazí na překryvné okno, rozpozná, že navigace je přepsána z výchozí hodnoty, a přeskočí na překryvném okně, když se zjistí jako podřízený počítač. Místo toho bude uzel dosažitelný pouze prostřednictvím fragmentu.

Opětovné vytvoření nadřazeného objektu není vhodné pro případy, kdy ovládací prvek může hostovat okno libovolné třídy. Například matrice může hostovat libovolný typ HWND ve svých pásmech. Pro zpracování těchto případů [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] podporuje alternativní forma přemístění HWND, jak je popsáno v následující části.

<a name="Non_WPF_Provider_Repositioning"></a>

### <a name="non-wpf-provider-repositioning"></a>Přemístění poskytovatele rozhraní non-WPF

fragmenty [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] mohou obsahovat dva nebo více prvků, které jsou obsaženy v okně (HWND). Vzhledem k tomu, že každý HWND má svého vlastního výchozího poskytovatele, který považuje HWND za podřízenou položku obsahující HWND, strom [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ve výchozím nastavení zobrazí HWND v fragmentu jako podřízené objekty nadřazeného okna. Ve většině případů to je žádoucí chování, ale někdy může vést k záměně, protože se neshoduje s logickou strukturou [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)].

Dobrým příkladem toho je ovládací prvek matrice. Matrice obsahuje pruhy, z nichž každý může zase obsahovat ovládací prvek založený na HWND, jako je například panel nástrojů, textové pole nebo pole se seznamem. Výchozí zprostředkovatel oken pro matrice HWND uvidí ovládací prvky pruhy HWND jako podřízené a poskytovatel matrice uvidí pásma jako podřízené objekty. Vzhledem k tomu, že zprostředkovatel HWND a poskytovatel matrice pracují v kombinaci a kombinování jejich podřízených prvků, jsou pruhy i ovládací prvky založené na HWND zobrazeny jako podřízené objekty matrice. Logicky by však měly být pouze pruhy zobrazeny jako podřízené položky matrice a každý poskytovatel pásma by měl být spojen s výchozím zprostředkovatelem HWND pro ovládací prvek, který obsahuje.

K tomu je potřeba, aby poskytovatel kořene fragmentu pro matrice vystavil sadu podřízených prvků reprezentujících pásma. Každý panel má jednoho poskytovatele, který může vystavit vlastnosti a vzory. Ve své implementaci <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A>vrátí poskytovatel pásma výchozího zprostředkovatele okna pro HWND ovládacího prvku, který získá voláním <xref:System.Windows.Automation.Provider.AutomationInteropProvider.HostProviderFromHandle%2A>a předáním v popisovači okna ovládacího prvku. Nakonec poskytovatel kořenového prvku fragmentu pro matrice implementuje rozhraní <xref:System.Windows.Automation.Provider.IRawElementProviderHwndOverride> a v jeho implementaci <xref:System.Windows.Automation.Provider.IRawElementProviderHwndOverride.GetOverrideProviderForHwnd%2A> vrátí příslušného poskytovatele pásma pro ovládací prvek obsažený v zadaném HWND.

## <a name="see-also"></a>Viz také:

- [Přehled zprostředkovatelů automatizace uživatelského rozhraní](ui-automation-providers-overview.md)
- [Vystavení zprostředkovatele automatizace uživatelského rozhraní na straně serveru](expose-a-server-side-ui-automation-provider.md)
- [Vrácení vlastností ze zprostředkovatele automatizace uživatelského rozhraní](return-properties-from-a-ui-automation-provider.md)
- [Vyvolávání událostí ze zprostředkovatele automatizace uživatelského rozhraní](raise-events-from-a-ui-automation-provider.md)
- [Povolení navigace u zprostředkovatele fragmentu automatizace uživatelského rozhraní na straně klienta](enable-navigation-in-a-ui-automation-fragment-provider.md)
- [Podpora vzorů ovládacích prvků u zprostředkovatele automatizace uživatelského rozhraní](support-control-patterns-in-a-ui-automation-provider.md)
