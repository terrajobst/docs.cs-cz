---
title: Migrace aplikace pro Windows Store do .NET Native
ms.date: 03/30/2017
ms.assetid: 4153aa18-6f56-4a0a-865b-d3da743a1d05
ms.openlocfilehash: 1942574e832ca7593d91c71370cc0af0c3051617
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2019
ms.locfileid: "73455608"
---
# <a name="migrate-your-windows-store-app-to-net-native"></a>Migrace aplikace pro Windows Store na .NET Native

.NET Native poskytuje statickou kompilaci aplikací ve Windows Storu nebo v počítači vývojáře. To se liší od dynamické kompilace provedené pro aplikace pro Windows Store pomocí kompilátoru JIT (just-in-time) nebo [generátoru nativních imagí (Ngen. exe)](../tools/ngen-exe-native-image-generator.md) na zařízení. Navzdory rozdílům se .NET Native snaží udržet kompatibilitu s [rozhraním .NET pro aplikace pro Windows Store](https://docs.microsoft.com/previous-versions/windows/apps/br230302%28v=vs.140%29). Ve většině případů fungují i v případě, že funkce pro .NET pro aplikace pro Windows Store funguje i .NET Native.  V některých případech ale může dojít ke změnám chování. Tento dokument popisuje tyto rozdíly mezi standardním rozhraním .NET pro aplikace pro Windows Store a .NET Native v následujících oblastech:

- [Obecné rozdíly v modulech runtime](#Runtime)

- [Rozdíly v dynamickém programování](#Dynamic)

- [Další rozdíly týkající se reflexe](#Reflection)

- [Nepodporované scénáře a rozhraní API](#Unsupported)

- [Rozdíly v aplikaci Visual Studio](#VS)

<a name="Runtime"></a>

## <a name="general-runtime-differences"></a>Obecné rozdíly v modulech runtime

- Výjimky, například <xref:System.TypeLoadException>, které jsou vyvolány kompilátorem JIT, když aplikace běží v modulu CLR (Common Language Runtime) obecně vede k chybám při kompilaci při zpracování pomocí .NET Native.

- Nevolejte metodu <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> z vlákna uživatelského rozhraní aplikace. To může vést k zablokování .NET Native.

- Nespoléhá se na řazení volání konstruktoru statické třídy. V .NET Native se pořadí vyvolání liší od pořadí na standardním modulu runtime. (I se standardním modulem runtime byste neměli spoléhat na pořadí spouštění statických konstruktorů tříd.)

- Nekonečná smyčka bez provedení volání (například `while(true);`) v jakémkoli vlákně může aplikaci přenést do zastavení. Podobně, velké nebo nekonečné čekací prodlevy můžou aplikaci zastavit.

- Některé obecné inicializační cykly nevyvolají výjimky v .NET Native. Například následující kód vyvolá výjimku <xref:System.TypeLoadException> pro standardní CLR. V .NET Native ne.

  [!code-csharp[ProjectN#8](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat1.cs#8)]

- V některých případech .NET Native poskytuje různé implementace knihoven .NET Framework třídy. Objekt vrácený z metody vždy implementuje členy vráceného typu. Vzhledem k tomu, že je jeho implementace jiného typu odlišná, možná ho nebude možné přetypovat na stejnou sadu typů, jakou jste mohli na jiných .NET Framework platformách. Například v některých případech nemusí být možné přetypování objektu <xref:System.Collections.Generic.IEnumerable%601> rozhraní vráceného metodami, jako je <xref:System.Reflection.TypeInfo.DeclaredMembers%2A?displayProperty=nameWithType> nebo <xref:System.Reflection.TypeInfo.DeclaredProperties%2A?displayProperty=nameWithType> na `T[]`.

- Mezipaměť WinInet není ve výchozím nastavení povolená v rozhraní .NET pro aplikace pro Windows Store, ale je na .NET Native. To zlepšuje výkon, ale má vliv na pracovní sadu. Není nutná žádná akce vývojáře.

<a name="Dynamic"></a>

## <a name="dynamic-programming-differences"></a>Rozdíly v dynamickém programování

.NET Native staticky propojuje v kódu z .NET Framework pro zajištění maximálního výkonu pro místní aplikaci kódu. Binární velikosti ale musí zůstat malé, takže celé .NET Framework nejde do. Kompilátor .NET Native vyřeší toto omezení pomocí zmenšení závislosti, který odebírá odkazy na nepoužitý kód. .NET Native však nemusí zachovat nebo vygenerovat některé informace o typu a kód, pokud tyto informace nelze odvodit staticky v době kompilace, ale místo toho se načte dynamicky za běhu.

.NET Native povolí reflexi a dynamické programování. Ne všechny typy však mohou být označeny pro reflexi, protože by byla velikost generovaného kódu příliš velká (obzvláště proto, že je podporována podpora veřejných rozhraní API v .NET Framework). Kompilátor .NET Native zpřístupňuje inteligentní volby, které typy by měly podporovat reflexi, a udržuje metadata a generuje kód pouze pro tyto typy.

Datová vazba například vyžaduje, aby aplikace mohla mapovat názvy vlastností na funkce. V rozhraní .NET pro aplikace pro Windows Store modul CLR (Common Language Runtime) automaticky používá reflexi k poskytnutí této možnosti pro spravované typy a veřejně dostupné nativní typy. V .NET Native kompilátor automaticky obsahuje metadata pro typy, na které svážete data.

Kompilátor .NET Native může také zpracovávat běžně používané obecné typy, například <xref:System.Collections.Generic.List%601> a <xref:System.Collections.Generic.Dictionary%602>, které fungují bez vyžadování jakýchkoli pomocných parametrů nebo direktiv. [Dynamické](../../csharp/language-reference/builtin-types/reference-types.md#the-dynamic-type) klíčové slovo je podporováno i v určitých omezeních.

> [!NOTE]
> Všechny cesty dynamického kódu by měly být důkladně testovány při přenosu vaší aplikace do .NET Native.

Výchozí konfigurace pro .NET Native je dostačující pro většinu vývojářů, ale vývojáři můžou chtít doladit své konfigurace pomocí souboru běhových direktiv (. Rd. XML). Navíc v některých případech kompilátor .NET Native nemůže určit, která metadata musí být k dispozici pro reflexi a spoléhá na pomocná doporučení, zejména v následujících případech:

- Některé konstrukce, jako je <xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType> a <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=nameWithType>, nelze určit staticky.

- Vzhledem k tomu, že kompilátor nemůže určit vytváření instancí, musí obecný typ, na kterém chcete reflektovat, být určen direktivami modulu runtime. To není pouhá, protože musí být zahrnut všechen kód, ale vzhledem k tomu, že reflexe na obecných typech může tvořit nekonečný cyklus (například při vyvolání obecné metody na obecném typu).

> [!NOTE]
> Direktivy modulu runtime jsou definovány v souboru direktiv modulu runtime (. Rd. XML). Obecné informace o používání tohoto souboru najdete v tématu [Začínáme](getting-started-with-net-native.md). Informace o direktivách modulu runtime naleznete v tématu [reference ke konfiguračnímu souboru direktiv modulu runtime (RD. XML)](runtime-directives-rd-xml-configuration-file-reference.md).

.NET Native také obsahuje nástroje pro profilaci, které vývojářům pomůžou určit, které typy mimo výchozí sadu mají podporovat reflexi.

<a name="Reflection"></a>

## <a name="other-reflection-related-differences"></a>Další rozdíly týkající se reflexe

Mezi rozhraním .NET pro aplikace pro Windows Store a .NET Native existuje řada dalších rozdílů týkajících se reflexe.

V .NET Native:

- Privátní odraz nad typy a členy v knihovně tříd .NET Framework není podporován. Můžete však reflektovat na vlastní privátní typy a členy a také typy a členy v knihovnách třetích stran.

- Vlastnost <xref:System.Reflection.ParameterInfo.HasDefaultValue%2A?displayProperty=nameWithType> správně vrací `false` pro objekt <xref:System.Reflection.ParameterInfo>, který představuje vrácenou hodnotu. V rozhraní .NET pro aplikace pro Windows Store vrátí `true`. Intermediate Language (IL) nepodporuje tento přímý odkaz a interpretace je ponechána na jazyku.

- Veřejné členy na <xref:System.RuntimeFieldHandle> a strukturách <xref:System.RuntimeMethodHandle> se nepodporují. Tyto typy jsou podporovány pouze pro LINQ, stromy výrazů a inicializaci statického pole.

- <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeProperties%2A?displayProperty=nameWithType> a <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeEvents%2A?displayProperty=nameWithType> zahrnují skryté členy v základních třídách, a proto mohou být přepsány bez explicitního přepsání. To platí také pro jiné metody [RuntimeReflectionExtensions. GetRuntime *](xref:System.Reflection.RuntimeReflectionExtensions) .

- <xref:System.Type.MakeArrayType%2A?displayProperty=nameWithType> a <xref:System.Type.MakeByRefType%2A?displayProperty=nameWithType> neselže při pokusu o vytvoření určitých kombinací (například pole s parametry ByRef).

- Nemůžete použít reflexi k vyvolání členů, kteří mají parametry ukazatele.

- Nemůžete použít reflexi k získání nebo nastavení pole ukazatele.

- Pokud je počet argumentů špatný a typ jednoho z argumentů je nesprávný, .NET Native vyvolá <xref:System.ArgumentException> namísto <xref:System.Reflection.TargetParameterCountException>.

- Binární serializace výjimek je obecně Nepodporovaná. V důsledku toho lze do <xref:System.Exception.Data%2A?displayProperty=nameWithType> slovníku přidat objekty, které nejsou serializovatelný.

<a name="Unsupported"></a>

## <a name="unsupported-scenarios-and-apis"></a>Nepodporované scénáře a rozhraní API

V následujících částech najdete seznam nepodporovaných scénářů a rozhraní API pro obecné vývoj, interoperabilitu a technologie, jako je HTTPClient a Windows Communication Foundation (WCF):

- [Obecný vývoj](#General)

- [HttpClient](#HttpClient)

- [Interop](#Interop)

- [Nepodporovaná rozhraní API](#APIs)

<a name="General"></a>

### <a name="general-development-differences"></a>Obecné rozdíly v vývoji

**Typy hodnot**

- Pokud přepíšete <xref:System.ValueType.Equals%2A?displayProperty=nameWithType> a <xref:System.ValueType.GetHashCode%2A?displayProperty=nameWithType> metody pro typ hodnoty, Nevolejte implementace základní třídy. V rozhraní .NET pro aplikace pro Windows Store se tyto metody spoléhají na reflexi. V době kompilace .NET Native generuje implementaci, která nespoléhá na reflexi modulu runtime. To znamená, že pokud tyto dvě metody nepřepíšete, budou fungovat podle očekávání, protože .NET Native generuje implementaci v době kompilace. Nicméně přepsání těchto metod, ale volání implementace základní třídy, způsobí výjimku.

- Typy hodnot větší než 1 MB nejsou podporovány.

- Typy hodnot nemohou mít konstruktor bez parametrů v .NET Native. (C# a Visual Basic zakázat konstruktory bez parametrů u typů hodnot. Ty však lze vytvořit v IL.)

**Pole**

- Pole s dolní mezí jinou než nula se nepodporují. Obvykle jsou tato pole vytvořena voláním <xref:System.Array.CreateInstance%28System.Type%2CSystem.Int32%5B%5D%2CSystem.Int32%5B%5D%29?displayProperty=nameWithType> přetížení.

- Dynamické vytváření multidimenzionálních polí se nepodporuje. Taková pole jsou obvykle vytvořena voláním přetížení metody <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType>, která obsahuje parametr `lengths` nebo voláním metody <xref:System.Type.MakeArrayType%28System.Int32%29?displayProperty=nameWithType>.

- Multidimenzionální pole se čtyřmi nebo více dimenzemi nejsou podporována. To znamená, že hodnota vlastnosti <xref:System.Array.Rank%2A?displayProperty=nameWithType> je čtyři nebo větší. Místo toho použijte [vícenásobná pole](../../csharp/programming-guide/arrays/jagged-arrays.md) (pole polí). Například `array[x,y,z]` je neplatný, ale `array[x][y][z]` není.

- Variance pro multidimenzionální pole není podporována a v době běhu způsobuje výjimku <xref:System.InvalidCastException>.

**Obecné typy**

- Nekonečné rozšíření obecného typu má za následek chybu kompilátoru. Například tento kód nemůže kompilovat:

  [!code-csharp[ProjectN#9](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat2.cs#9)]

**Ukazatele**

- Pole ukazatelů nejsou podporovaná.

- Nemůžete použít reflexi k získání nebo nastavení pole ukazatele.

**Serializace**

Atribut <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.String%29> není podporován. Místo toho použijte atribut <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.Type%29>.

**Prostředky**

Použití lokalizovaných prostředků s <xref:System.Diagnostics.Tracing.EventSource> třídou není podporováno. Vlastnost <xref:System.Diagnostics.Tracing.EventSourceAttribute.LocalizationResources%2A?displayProperty=nameWithType> nedefinuje lokalizované prostředky.

**Delegáty**

`Delegate.BeginInvoke` a `Delegate.EndInvoke` nejsou podporovány.

**Ostatní rozhraní API**

- Vlastnost [TypeInfo. GUID](xref:System.Type.GUID) vyvolá výjimku <xref:System.PlatformNotSupportedException>, pokud není pro typ použit atribut <xref:System.Runtime.InteropServices.GuidAttribute>. Identifikátor GUID se používá hlavně pro podporu modelu COM.

- Metoda <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> správně analyzuje řetězce, které obsahují krátká data v .NET Native. Neudržuje však kompatibilitu se změnami v části datum a čas analýzy popsané v článcích [KB2803771](https://support.microsoft.com/kb/2803771) a [KB2803755](https://support.microsoft.com/kb/2803755)znalostní báze Microsoft Knowledge Base.

- <xref:System.Numerics.BigInteger.ToString%2A?displayProperty=nameWithType> `("E")` se v .NET Native správně zaokrouhlují. V některých verzích modulu CLR je výsledný řetězec zkrácen namísto zaokrouhlení.

<a name="HttpClient"></a>

### <a name="httpclient-differences"></a>HttpClient rozdíly

V .NET Native třída <xref:System.Net.Http.HttpClientHandler> interně používá rozhraní WinINet (přes třídu <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter>) místo <xref:System.Net.WebRequest> a <xref:System.Net.WebResponse> třídy používané ve standardním rozhraní .NET pro aplikace pro Windows Store.  Rozhraní WinINet nepodporuje všechny možnosti konfigurace, které třída <xref:System.Net.Http.HttpClientHandler> podporuje.  Výsledek:

- Některé vlastnosti schopností <xref:System.Net.Http.HttpClientHandler> vrátí `false` na .NET Native, zatímco budou vracet `true` ve standardním rozhraní .NET pro aplikace pro Windows Store.

- Některé vlastnosti `get` přistupující objekty vždy vracejí pevnou hodnotu v .NET Native, která se liší od výchozí konfigurovatelné hodnoty v rozhraní .NET pro aplikace pro Windows Store.

V následujících pododdílech jsou uvedeny některé další rozdíly v chování.

**Soubory**

Třída <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> nepodporuje konfiguraci ani přepsání proxy serveru na základě jednotlivých požadavků.  To znamená, že všechny požadavky na .NET Native v závislosti na hodnotě <xref:System.Net.Http.HttpClientHandler.UseProxy%2A?displayProperty=nameWithType> vlastnosti používat systémovou proxy server nebo žádné proxy server.  V rozhraní .NET pro aplikace pro Windows Store je proxy server definováno vlastností <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType>.  Při .NET Native je nastavení <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType> na jinou hodnotu než `null` vyvolá výjimku <xref:System.PlatformNotSupportedException>.  Vlastnost <xref:System.Net.Http.HttpClientHandler.SupportsProxy%2A?displayProperty=nameWithType> vrací `false` na .NET Native, zatímco vrací `true` ve standardním .NET Framework pro aplikace pro Windows Store.

**Automatické přesměrování**

Třída <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> neumožňuje nakonfigurovat maximální počet automatických přesměrování.  Hodnota vlastnosti <xref:System.Net.Http.HttpClientHandler.MaxAutomaticRedirections%2A?displayProperty=nameWithType> je standardně 50 standardem .NET pro aplikace pro Windows Store a lze ji upravit. V .NET Native je hodnota této vlastnosti 10 a pokus o její úpravu vyvolá výjimku <xref:System.PlatformNotSupportedException>.  Vlastnost <xref:System.Net.Http.HttpClientHandler.SupportsRedirectConfiguration%2A?displayProperty=nameWithType> vrací `false` na .NET Native, zatímco vrací `true` v rozhraní .NET pro aplikace pro Windows Store.

**Automatická dekomprese**

Rozhraní .NET pro aplikace pro Windows Store umožňuje nastavit vlastnost <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A?displayProperty=nameWithType> na <xref:System.Net.DecompressionMethods.Deflate>, <xref:System.Net.DecompressionMethods.GZip>, <xref:System.Net.DecompressionMethods.Deflate> a <xref:System.Net.DecompressionMethods.GZip>nebo <xref:System.Net.DecompressionMethods.None>.  .NET Native podporuje pouze <xref:System.Net.DecompressionMethods.Deflate> společně s <xref:System.Net.DecompressionMethods.GZip>nebo <xref:System.Net.DecompressionMethods.None>.  Pokus o nastavení vlastnosti <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A> na hodnotu <xref:System.Net.DecompressionMethods.Deflate> nebo <xref:System.Net.DecompressionMethods.GZip> samostatně v tichém režimu nastaví na <xref:System.Net.DecompressionMethods.Deflate> i <xref:System.Net.DecompressionMethods.GZip>.

**Soubory cookie**

Zpracování souborů cookie se provádí současně <xref:System.Net.Http.HttpClient> a WinINet.  Soubory cookie z <xref:System.Net.CookieContainer> jsou kombinovány s soubory cookie v mezipaměti WinINet cookie.  Odebrání souboru cookie z <xref:System.Net.CookieContainer> zabrání v <xref:System.Net.Http.HttpClient> odeslání souboru cookie, ale pokud soubor cookie již viděla služba WinINet a soubory cookie nebyly odstraněny uživatelem, rozhraní WinINet ho pošle.  Nelze programově odebrat soubor cookie z WinINet pomocí <xref:System.Net.Http.HttpClient>, <xref:System.Net.Http.HttpClientHandler>nebo rozhraní API <xref:System.Net.CookieContainer>.  Nastavení vlastnosti <xref:System.Net.Http.HttpClientHandler.UseCookies%2A?displayProperty=nameWithType> na hodnotu `false` způsobí, že pouze <xref:System.Net.Http.HttpClient> zastaví posílání souborů cookie; Rozhraní WinINet může stále zahrnovat své soubory cookie v žádosti.

**Přihlašovací údaje**

V rozhraní .NET pro aplikace pro Windows Store pracují vlastnosti <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A?displayProperty=nameWithType> a <xref:System.Net.Http.HttpClientHandler.Credentials%2A?displayProperty=nameWithType> nezávisle.  Kromě toho vlastnost <xref:System.Net.Http.HttpClientHandler.Credentials%2A> přijímá libovolný objekt, který implementuje rozhraní <xref:System.Net.ICredentials>.  V .NET Native nastavení vlastnosti <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A> na `true` způsobí, že se vlastnost <xref:System.Net.Http.HttpClientHandler.Credentials%2A> stane `null`.  Kromě toho může být vlastnost <xref:System.Net.Http.HttpClientHandler.Credentials%2A> nastavena pouze na `null`, <xref:System.Net.CredentialCache.DefaultCredentials%2A>nebo objekt typu <xref:System.Net.NetworkCredential>.  Přiřazení jakýchkoli jiných objektů <xref:System.Net.ICredentials>, z nejoblíbenějších z nich je <xref:System.Net.CredentialCache>, na vlastnost <xref:System.Net.Http.HttpClientHandler.Credentials%2A> vyvolá <xref:System.PlatformNotSupportedException>.

**Jiné nepodporované nebo Nekonfigurovatelné funkce**

V .NET Native:

- Hodnota vlastnosti <xref:System.Net.Http.HttpClientHandler.ClientCertificateOptions%2A?displayProperty=nameWithType> je vždy <xref:System.Net.Http.ClientCertificateOption.Automatic>.  V rozhraní .NET pro aplikace pro Windows Store je výchozí hodnota <xref:System.Net.Http.ClientCertificateOption.Manual>.

- Vlastnost <xref:System.Net.Http.HttpClientHandler.MaxRequestContentBufferSize%2A?displayProperty=nameWithType> není konfigurovatelná.

- Vlastnost <xref:System.Net.Http.HttpClientHandler.PreAuthenticate%2A?displayProperty=nameWithType> je vždy `true`.  V rozhraní .NET pro aplikace pro Windows Store je výchozí hodnota `false`.

- Hlavička `SetCookie2` v odpovědích je ignorována jako zastaralá.

<a name="Interop"></a>
### <a name="interop-differences"></a>Rozdíly v interoperabilitách
 **Zastaralá rozhraní API**

 Počet zřídka používaných rozhraní API pro interoperabilitu se spravovaným kódem je zastaralý. Při použití s .NET Native mohou tato rozhraní API vyvolat výjimku <xref:System.NotImplementedException> nebo <xref:System.PlatformNotSupportedException> nebo způsobit chybu kompilátoru. V rozhraní .NET pro aplikace pro Windows Store jsou tato rozhraní API označena jako zastaralá, ale volání generují upozornění kompilátoru, nikoli chybu kompilátoru.

 Zastaralá rozhraní API pro zařazování `VARIANT` zahrnují:

- <xref:System.Runtime.InteropServices.BStrWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.CurrencyWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.DispatchWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.ErrorWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnknownWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.VariantWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.VarEnum?displayProperty=nameWithType>

 <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> je podporován, ale vyvolá výjimku v některých scénářích, například při použití s variantami [IDispatch](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) nebo ByRef.

 Zastaralá rozhraní API pro podporu rozhraní [IDispatch](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) zahrnují:

- <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDispatch?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=nameWithType>

Zastaralá rozhraní API pro události klasických objektů COM zahrnují:

- <xref:System.Runtime.InteropServices.ComEventsHelper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>

Zastaralá rozhraní API v rozhraní <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType>, která nejsou v .NET Native podporovaná, zahrnují:

- <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> (všichni členové)
- <xref:System.Runtime.InteropServices.CustomQueryInterfaceMode?displayProperty=nameWithType> (všichni členové)
- <xref:System.Runtime.InteropServices.CustomQueryInterfaceResult?displayProperty=nameWithType> (všichni členové)
- <xref:System.Runtime.InteropServices.Marshal.GetComInterfaceForObject%28System.Object%2CSystem.Type%2CSystem.Runtime.InteropServices.CustomQueryInterfaceMode%29?displayProperty=fullName>

Mezi další nepodporované funkce spolupráce patří:

- <xref:System.Runtime.InteropServices.ICustomAdapter?displayProperty=nameWithType> (všichni členové)
- <xref:System.Runtime.InteropServices.SafeBuffer?displayProperty=nameWithType> (všichni členové)
- <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.AnsiBStr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.AsAny?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.CustomMarshaler?displayProperty=fullName>

 Zřídka používaná zařazování rozhraní API:

- <xref:System.Runtime.InteropServices.Marshal.ReadByte%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt16%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt32%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt64%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadIntPtr%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteByte%28System.Object%2CSystem.Int32%2CSystem.Byte%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt16%28System.Object%2CSystem.Int32%2CSystem.Int16%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt32%28System.Object%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt64%28System.Object%2CSystem.Int32%2CSystem.Int64%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteIntPtr%28System.Object%2CSystem.Int32%2CSystem.IntPtr%29?displayProperty=fullName>

 **Volání platforem a kompatibilita zprostředkovatele komunikace s objekty COM**

 Většina volání platforem a scénářů spolupráce s objekty COM jsou pořád podporované v .NET Native. Konkrétně se podporuje veškerá interoperabilita s rozhraními API pro prostředí Windows Runtime (WinRT) a všechna zařazování požadovaná pro prostředí Windows Runtime. Patří sem podpora zařazování pro:

- Pole (včetně <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType>)

- `BStr`

- Delegáty

- Řetězce (Unicode, ANSI a HSTRING)

- Struktury (`byref` a `byval`)

- Sjednocení

- Popisovače Win32

- Všechny konstruktory WinRT

- Částečná podpora pro zařazování typů variant Podporovány jsou následující:

  - <xref:System.Boolean>

  - <xref:System.Byte>

  - <xref:System.Decimal>

  - <xref:System.Double>

  - <xref:System.Int16>

  - <xref:System.Int32>

  - <xref:System.Int64>

  - <xref:System.SByte>

  - <xref:System.Single>

  - <xref:System.UInt16>

  - <xref:System.UInt32>

  - <xref:System.UInt64>

  - `BStr`

  - [IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)

.NET Native ale nepodporuje následující:

- Používání klasických událostí COM

- Implementace rozhraní <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> pro spravovaný typ

- Implementace rozhraní [IDispatch](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) na spravovaném typu prostřednictvím atributu <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=nameWithType>. Všimněte si však, že nemůžete volat objekty COM prostřednictvím `IDispatch`a váš spravovaný objekt nemůže implementovat `IDispatch`.

Použití reflexe k vyvolání metody Invoke platformy není podporováno. Toto omezení můžete obejít tak, že zabalíte volání metody do jiné metody a pomocí reflexe namísto toho zavolejte obálku.

<a name="APIs"></a>

### <a name="other-differences-from-net-apis-for-windows-store-apps"></a>Další rozdíly od rozhraní API .NET pro aplikace pro Windows Store

Tato část obsahuje seznam zbývajících rozhraní API, která nejsou v .NET Native podporovaná. Největší sadou nepodporovaných rozhraní API jsou Windows Communication Foundation (WCF) API.

**Dataanotace (System. ComponentModel. DataAnnotations)**

Typy v oborech názvů <xref:System.ComponentModel.DataAnnotations> a <xref:System.ComponentModel.DataAnnotations.Schema> se v .NET Native nepodporují. Mezi ně patří následující typy, které jsou k dispozici v rozhraní .NET pro aplikace pro Windows Store pro Windows 8:

- <xref:System.ComponentModel.DataAnnotations.AssociationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ConcurrencyCheckAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.CustomValidationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DataType?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DataTypeAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayColumnAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayFormatAttribute>
- <xref:System.ComponentModel.DataAnnotations.EditableAttribute>
- <xref:System.ComponentModel.DataAnnotations.EnumDataTypeAttribute>
- <xref:System.ComponentModel.DataAnnotations.FilterUIHintAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.KeyAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RangeAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RegularExpressionAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RequiredAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.StringLengthAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.TimestampAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.UIHintAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationContext?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationResult?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Validator?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedOption?displayProperty=nameWithType>

 **Visual Basic**

Visual Basic se v .NET Native v tuto chvíli nepodporuje. Následující typy v oborech názvů <xref:Microsoft.VisualBasic> a <xref:Microsoft.VisualBasic.CompilerServices> nejsou k dispozici v .NET Native:

- <xref:Microsoft.VisualBasic.CallType?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Constants?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.HideModuleNameAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Strings?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Conversions?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.DesignerGeneratedAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.IncompleteInitialization?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.NewLateBinding?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl.ForLoopControl?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Operators?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.OptionCompareAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.OptionTextAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ProjectData?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.StandardModuleAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.StaticLocalInitFlag?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Utils?displayProperty=nameWithType>

**Kontext reflexe (obor názvů System. Reflection. Context)**

Třída <xref:System.Reflection.Context.CustomReflectionContext?displayProperty=nameWithType> není v .NET Native podporovaná.

**RTC (System .NET. http. RTC)**

Třída `System.Net.Http.RtcRequestFactory` není v .NET Native podporovaná.

**Windows Communication Foundation (WCF) (System. ServiceModel.\*)**

Typy v [oborech názvů System. ServiceModel. *](xref:System.ServiceModel) nejsou podporované v .NET Native. Mezi ně patří následující typy:

- <xref:System.ServiceModel.ActionNotSupportedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpMessageCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpSecurityMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.CallbackBehaviorAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.BeginOperationDelegate?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.ChannelBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.EndOperationDelegate?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.InvokeAsyncCompletedEventArgs?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationObjectAbortedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationObjectFaultedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationState?displayProperty=nameWithType>
- <xref:System.ServiceModel.DataContractFormatAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.DnsEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.DuplexChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.DuplexClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointAddress?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointAddressBuilder?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointNotFoundException?displayProperty=nameWithType>
- <xref:System.ServiceModel.EnvelopeVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.ExceptionDetail?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultCode?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultReason?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultReasonText?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpBindingBase?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpClientCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpTransportSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.ICommunicationObject?displayProperty=nameWithType>
- <xref:System.ServiceModel.IContextChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.IDefaultCommunicationTimeouts?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtensibleObject%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtension%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtensionCollection%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.InvalidMessageContractException?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageBodyMemberAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageContractMemberAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageHeader%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageHeaderException?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityOverTcp?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetHttpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetHttpMessageEncoding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetTcpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetTcpSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContextScope?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationFormatStyle?displayProperty=nameWithType>
- <xref:System.ServiceModel.ProtocolException?displayProperty=nameWithType>
- <xref:System.ServiceModel.QuotaExceededException?displayProperty=nameWithType>
- <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServerTooBusyException?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceActivationException?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceKnownTypeAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.SpnEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.TcpClientCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.TcpTransportSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.TransferMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.UnknownMessageReceivedEventArgs?displayProperty=nameWithType>
- <xref:System.ServiceModel.UpnEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.XmlSerializerFormatAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressHeader?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressHeaderCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressingVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ChannelManagerBase?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ChannelParameterCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CommunicationObject?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CompressionFormat?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.FaultConverter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpRequestMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpResponseMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannelFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IHttpCookieContainerManager?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IRequestSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ISession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.LocalClientSecuritySettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageBuffer?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncoder?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncoderFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageFault?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeader?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeaderInfo?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeaders?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageProperties?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageState?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.RequestContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SecurityHeaderLayout?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TcpConnectionPoolSettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TcpTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TransportSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WebSocketTransportSettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WebSocketTransportUsage?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ClientCredentials?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.FaultDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.FaultDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageBodyDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDirection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageHeaderDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageHeaderDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePartDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePartDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePropertyDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePropertyDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.OperationDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.OperationDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.ClientOperation?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.ClientRuntime?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.DispatchOperation?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.DispatchRuntime?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.EndpointDispatcher?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientOperationSelector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.BasicSecurityProfileVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.HttpDigestClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecureConversationVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityAccessDeniedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityPolicyVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.TrustVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.WindowsClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SupportingTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.UserNameSecurityTokenParameters?displayProperty=nameWithType>

### <a name="differences-in-serializers"></a>Rozdíly v serializátorech

Následující rozdíly se týkají serializace a deserializace s třídami <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>a <xref:System.Xml.Serialization.XmlSerializer>:

- V .NET Native <xref:System.Runtime.Serialization.DataContractSerializer> a <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> selhání serializaci nebo deserializovat odvozenou třídu, která má člena základní třídy, jehož typ není kořenovým typem serializace. Například v následujícím kódu, který se pokouší o serializaci nebo deserializaci `Y` výsledky v důsledku chyby:

  [!code-csharp[ProjectN#10](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat3.cs#10)]

  Typ `InnerType` není pro serializátor znám, protože členy základní třídy nejsou během serializace procházeny.

- <xref:System.Runtime.Serialization.DataContractSerializer> a <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> selhání serializaci třídy nebo struktury, která implementuje rozhraní <xref:System.Collections.Generic.IEnumerable%601>. Například následující typy selhaly při serializaci nebo deserializaci:

- <xref:System.Xml.Serialization.XmlSerializer> nedokáže serializovat následující hodnotu objektu, protože neví přesný typ objektu, který se má serializovat:

- <xref:System.Xml.Serialization.XmlSerializer> se nepovedlo serializovat nebo deserializovat, pokud je typ serializovaného objektu <xref:System.Xml.XmlQualifiedName>.

- Všechny serializátory (<xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>a <xref:System.Xml.Serialization.XmlSerializer>) negenerují kód serializace pro typ <xref:System.Xml.Linq.XElement?displayProperty=nameWithType> nebo pro typ, který obsahuje <xref:System.Xml.Linq.XElement>. Místo toho zobrazují chyby při sestavování.

- Následující konstruktory typů serializace nemají zaručeny fungovat podle očekávání:

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.DataContractSerializerSettings%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Xml.XmlDictionaryString%2CSystem.Xml.XmlDictionaryString%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.Json.DataContractJsonSerializerSettings%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.String%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlRootAttribute%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%2CSystem.Type%5B%5D%2CSystem.Xml.Serialization.XmlRootAttribute%2CSystem.String%29?displayProperty=nameWithType>

- <xref:System.Xml.Serialization.XmlSerializer> negeneruje kód pro typ, který obsahuje metody s atributem s některým z následujících atributů:

  - <xref:System.Runtime.Serialization.OnSerializingAttribute>

  - <xref:System.Runtime.Serialization.OnSerializedAttribute>

  - <xref:System.Runtime.Serialization.OnDeserializingAttribute>

  - <xref:System.Runtime.Serialization.OnDeserializedAttribute>

- <xref:System.Xml.Serialization.XmlSerializer> nedodržuje rozhraní <xref:System.Xml.Serialization.IXmlSerializable> vlastní serializace. Máte-li třídu, která implementuje toto rozhraní, <xref:System.Xml.Serialization.XmlSerializer> považuje typ za prostý starý objekt CLR (POCO) a serializace pouze jeho veřejné vlastnosti.

- Serializace jednoduchého objektu <xref:System.Exception> nefunguje dobře s <xref:System.Runtime.Serialization.DataContractSerializer> a <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>.

<a name="VS"></a>

## <a name="visual-studio-differences"></a>Rozdíly v aplikaci Visual Studio

**Výjimky a ladění**

Pokud spouštíte aplikace zkompilované pomocí .NET Native v ladicím programu, jsou pro následující typy výjimek povoleny výjimky s první pravděpodobností:

- <xref:System.MemberAccessException>

- <xref:System.TypeAccessException>

**Sestavování aplikací**

Použijte nástroje pro sestavení x86, které jsou ve výchozím nastavení používány v aplikaci Visual Studio. Nedoporučujeme používat nástroje AMD64 MSBuild, které se nacházejí v adresáři C:\Program Files (x86) \MSBuild\12.0\bin\amd64; Ty můžou vytvářet problémy s sestavením.

**Profilery**

- Profiler procesoru sady Visual Studio a Profiler paměti XAML nezobrazuje správně pouze můj kód.

- Profiler paměti XAML přesně nezobrazuje spravovaná data haldy.

- Profiler procesoru správně neidentifikuje moduly a zobrazuje názvy předpevných funkcí.

**Projekty knihovny testů jednotek**

Povolení .NET Native v knihovně testů jednotek pro projekt aplikací pro Windows Store není podporované a způsobí, že se projekt nepodaří sestavit.

## <a name="see-also"></a>Viz také:

- [Začínáme](getting-started-with-net-native.md)
- [Informace o konfiguračním souboru direktiv modulu runtime (rd.xml)](runtime-directives-rd-xml-configuration-file-reference.md)
- [Přehled aplikace .NET pro Windows Store](https://docs.microsoft.com/previous-versions/windows/apps/br230302%28v=vs.140%29)
- [Podpora pro aplikace pro web Windows Store a prostředí Windows Runtime v rozhraní .NET Framework](../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
