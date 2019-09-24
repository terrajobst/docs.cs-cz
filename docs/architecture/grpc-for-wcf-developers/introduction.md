---
title: Úvod – gRPC pro vývojáře WCF
description: Úvod
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 2782f28e8a99fa7c0bde69f757d14e96e91f5cd4
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184419"
---
# <a name="introduction"></a><span data-ttu-id="10beb-103">Úvod</span><span class="sxs-lookup"><span data-stu-id="10beb-103">Introduction</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="10beb-104">Napomáháte počítačům navzájem komunikovat s jednou z primárních pracovních verzí digitálního stáří.</span><span class="sxs-lookup"><span data-stu-id="10beb-104">Helping machines communicate with each other has been one of the primary preoccupations of the digital age.</span></span> <span data-ttu-id="10beb-105">K určení optimálního vzdáleného komunikačního mechanismu, který bude vyhovovat požadavkům na interoperabilitu aktuální infrastruktury, je zejména průběžné úsilí.</span><span class="sxs-lookup"><span data-stu-id="10beb-105">In particular, there is an ongoing effort to determine the optimal remote communication mechanism that will suit the interoperability demands of the current infrastructure.</span></span> <span data-ttu-id="10beb-106">Jak můžete představovat, tento mechanismus se mění jak v rámci požadavků, tak ve vývojovém infrastruktuře.</span><span class="sxs-lookup"><span data-stu-id="10beb-106">As you can imagine, that mechanism changes as either the demands or the infrastructure evolves.</span></span>

<span data-ttu-id="10beb-107">Verze .NET Core 3,0 označuje Shift způsob, jakým společnost Microsoft dodává řešení pro vzdálenou komunikaci vývojářům, kteří chtějí poskytovat služby v rámci celé řady platforem.</span><span class="sxs-lookup"><span data-stu-id="10beb-107">The release of .NET Core 3.0 marks a shift in the way that Microsoft delivers remote communication solutions to developers who want to deliver services across a range of platforms.</span></span> <span data-ttu-id="10beb-108">.NET Core nenabízí Windows Communication Foundation (WCF), ale s vydáním verze ASP.NET Core 3,0 poskytuje vestavěnou funkci gRPC.</span><span class="sxs-lookup"><span data-stu-id="10beb-108">.NET Core doesn't offer Windows Communication Foundation (WCF) out of the box but, with the release of version ASP.NET Core 3.0, it does provide built-in gRPC functionality.</span></span>

<span data-ttu-id="10beb-109">gRPC je oblíbená architektura v širší komunitě pro software, kterou vývojáři využívají v různých programovacích jazycích pro moderní scénáře RPC.</span><span class="sxs-lookup"><span data-stu-id="10beb-109">gRPC is a popular framework in the wider software community, used by developers across many programming languages for modern RPC scenarios.</span></span> <span data-ttu-id="10beb-110">Komunita a ekosystém jsou zářivé a aktivní, s podporou protokolu gRPC přidávaného do součástí infrastruktury, jako je Kubernetes, sítě pro služby, nástroje pro vyrovnávání zatížení a další.</span><span class="sxs-lookup"><span data-stu-id="10beb-110">The community and the ecosystem are vibrant and active, with support for the gRPC protocol being added to infrastructure components like Kubernetes, service meshes, load balancers and more.</span></span> <span data-ttu-id="10beb-111">Tyto faktory, jakož i výkon, efektivitu a kompatibilitu mezi platformami, gRPC přirozené možnosti pro nové aplikace a aplikace WCF, které se přesunou do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="10beb-111">These factors, as well as its performance, efficiency and cross-platform compatibility, make gRPC a natural choice for new apps and WCF apps moving to .NET Core.</span></span>

## <a name="history"></a><span data-ttu-id="10beb-112">Historie</span><span class="sxs-lookup"><span data-stu-id="10beb-112">History</span></span>

<span data-ttu-id="10beb-113">Základní princip počítačové sítě jako nevětšího počtu počítačů, který vyměňuje data mezi sebou, aby se zajistilo, že sada vzájemně souvisejících úloh se od svého zahájení nezměnila.</span><span class="sxs-lookup"><span data-stu-id="10beb-113">The fundamental principle of a computer network as nothing more than a group of computers exchanging data with each other to achieve a set of interrelated tasks hasn't changed since its inception.</span></span> <span data-ttu-id="10beb-114">Nicméně složitost, měřítko a očekávání se exponenciálně zvětšily.</span><span class="sxs-lookup"><span data-stu-id="10beb-114">However, the complexity, scale, and expectations have grown exponentially.</span></span>  

<span data-ttu-id="10beb-115">Během 1990s se důraz zaměřuje hlavně na vylepšení interních sítí pomocí stejného jazyka a platforem.</span><span class="sxs-lookup"><span data-stu-id="10beb-115">During the 1990s, the emphasis had been mainly focused on improving internal networks using the same language and platforms.</span></span> <span data-ttu-id="10beb-116">Pro tento typ komunikace se stala standardem Gold protokol TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="10beb-116">TCP/IP became the gold standard for this type of communication.</span></span>

<span data-ttu-id="10beb-117">Fokus se ale brzo přesune na to, jak nejlépe optimalizujete komunikaci napříč různými platformami, které podporují nezávisláý přístup k jazyku.</span><span class="sxs-lookup"><span data-stu-id="10beb-117">However, the focus soon shifted to how best to optimize communication across multiple platforms promoting a language agnostic approach.</span></span> <span data-ttu-id="10beb-118">Architektura zaměřená na služby (SOA) poskytuje strukturu pro volný spojování široké kolekce služeb, které by mohly být poskytnuty aplikaci.</span><span class="sxs-lookup"><span data-stu-id="10beb-118">Service-oriented architecture (SOA) provided a structure for loosely coupling a broad collection of services that could be provided to an application.</span></span>

<span data-ttu-id="10beb-119">K vývoji *webových služeb* došlo, když všechny hlavní platformy získají přístup k Internetu, ale stále se nemůžou vzájemně komunikovat.</span><span class="sxs-lookup"><span data-stu-id="10beb-119">The development of *Web Services* occurred once all major platforms could access the Internet, but they still couldn’t interact with each other.</span></span> <span data-ttu-id="10beb-120">Webové služby mají otevřené standardy a protokoly, mezi které patří:</span><span class="sxs-lookup"><span data-stu-id="10beb-120">Web services have open standards and protocols including:</span></span>

- <span data-ttu-id="10beb-121">XML pro označení a data kódu;</span><span class="sxs-lookup"><span data-stu-id="10beb-121">XML to tag and code data;</span></span>
- <span data-ttu-id="10beb-122">Protokol SOAP (Simple Object Access Protocol) pro přenos dat;</span><span class="sxs-lookup"><span data-stu-id="10beb-122">Simple Object Access Protocol (SOAP) to transfer data;</span></span>
- <span data-ttu-id="10beb-123">WSDL (Web Services Definition Language) – popisuje a připojuje webovou službu ke klientské aplikaci. *a*</span><span class="sxs-lookup"><span data-stu-id="10beb-123">Web Services Definition Language (WSDL) – describes and connects the web service to the client application; *and*</span></span>
- <span data-ttu-id="10beb-124">Služba UDDI (Universal Description Discovery Integration) – povoluje, aby webové služby byly zjistitelné jinými službami.</span><span class="sxs-lookup"><span data-stu-id="10beb-124">Universal Description Discovery Integration (UDDI)- enables Web Services to be discoverable by other Services</span></span>

<span data-ttu-id="10beb-125">SOAP definuje pravidla, podle kterých mohou distribuované prvky aplikace vzájemně komunikovat, a to i v případě, že jsou na různých platformách.</span><span class="sxs-lookup"><span data-stu-id="10beb-125">SOAP defines the rules by which distributed elements of an application can communicate with each other even if they are on different platforms.</span></span> <span data-ttu-id="10beb-126">Protokol SOAP je založen na XML, takže je čitelný pro člověka.</span><span class="sxs-lookup"><span data-stu-id="10beb-126">SOAP is based on XML, so it's human-readable.</span></span> <span data-ttu-id="10beb-127">Usmrcení pro snazší porozumění protokolu SOAP má velikost; Zprávy SOAP jsou větší než zprávy v srovnatelných protokolech.</span><span class="sxs-lookup"><span data-stu-id="10beb-127">The sacrifice for making SOAP easily understood is size; SOAP messages are larger than messages in comparable protocols.</span></span> <span data-ttu-id="10beb-128">Protokol SOAP byl navržen pro rozdělení monolitické aplikací do formuláře s více komponentami, aniž by došlo ke ztrátě zabezpečení nebo řízení.</span><span class="sxs-lookup"><span data-stu-id="10beb-128">SOAP was designed to break down monolithic applications into multi-component form without losing security or control.</span></span> <span data-ttu-id="10beb-129">Proto služba WCF byla navržena pro práci s tímto druhem systému, na rozdíl od gRPC, která začala jako distribuovaný systém.</span><span class="sxs-lookup"><span data-stu-id="10beb-129">Therefore, WCF was designed to work with that kind of system, unlike gRPC, which began as a distributed system.</span></span> <span data-ttu-id="10beb-130">Služba WCF vyřešila některá z těchto omezení tím, že vyvíjí a zdokumentuje proprietární protokoly rozšíření pro zásobník protokolu SOAP, ale za cenu nedostatku podpory od jiných platforem.</span><span class="sxs-lookup"><span data-stu-id="10beb-130">WCF addressed some of these limitations by developing and documenting proprietary extension protocols for the SOAP stack, but at the cost of lack of support from other platforms.</span></span>

<span data-ttu-id="10beb-131">Windows Communication Foundation je rozhraní pro vytváření služeb.</span><span class="sxs-lookup"><span data-stu-id="10beb-131">Windows Communication Foundation is a framework for building services.</span></span> <span data-ttu-id="10beb-132">Byla navržena v 2000s, aby usnadnila vývojářům použití prvotního SOA ke správě složitosti práce s protokolem SOAP.</span><span class="sxs-lookup"><span data-stu-id="10beb-132">It was designed in the early 2000s to help developers using early SOA to manage the complexities of working with SOAP.</span></span> <span data-ttu-id="10beb-133">I když odebere požadavek, aby vývojář mohl zapisovat svoje vlastní protokoly SOAP, WCF dál používá protokol SOAP, aby bylo možné vzájemnou spolupráci s jinými systémy.</span><span class="sxs-lookup"><span data-stu-id="10beb-133">Although it removes the requirement for the developer to write their own SOAP protocols, WCF still uses SOAP to enable interoperability with other systems.</span></span> <span data-ttu-id="10beb-134">Služba WCF byla také navržena tak, aby poskytovala řešení pro různé protokoly (HTTP/1.1, NetTCP a tak dále).</span><span class="sxs-lookup"><span data-stu-id="10beb-134">WCF was also designed to deliver solutions across multiple protocols (HTTP/1.1, NetTCP, and so on).</span></span>

## <a name="microservices"></a><span data-ttu-id="10beb-135">Mikroslužby</span><span class="sxs-lookup"><span data-stu-id="10beb-135">Microservices</span></span>

<span data-ttu-id="10beb-136">V architektuře mikroslužeb jsou velké aplikace sestavené jako kolekce menších modulárních služeb.</span><span class="sxs-lookup"><span data-stu-id="10beb-136">In microservice architectures, large applications are built as a collection of smaller modular services.</span></span> <span data-ttu-id="10beb-137">Každá součást provede konkrétní úlohu nebo proces a komponenty jsou navrženy tak, aby fungovaly, ale mohou být izolované podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="10beb-137">Each component does a specific task or process, and components are designed to work interoperably but can be isolated as necessary.</span></span>

<span data-ttu-id="10beb-138">Mezi výhody pro mikroslužby patří:</span><span class="sxs-lookup"><span data-stu-id="10beb-138">Advantages to microservices include:</span></span>

- <span data-ttu-id="10beb-139">Změny a upgrady je možné zpracovat nezávisle.</span><span class="sxs-lookup"><span data-stu-id="10beb-139">Changes and upgrades can be handled independently.</span></span>
- <span data-ttu-id="10beb-140">Zpracování chyb je efektivnější, protože problémy lze trasovat na konkrétní služby, které jsou následně izolované, znovu sestaveny, testovány a znovu nasazeny nezávisle na ostatních službách.</span><span class="sxs-lookup"><span data-stu-id="10beb-140">Error handling becomes more efficient as problems can be traced to specific services that are then isolated, rebuilt, tested, and redeployed independent of the other services.</span></span>
- <span data-ttu-id="10beb-141">Škálovatelnost může být omezen na konkrétní instance nebo služby, nikoli na celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="10beb-141">Scalability can be confined to the specific instances or services rather than the whole application.</span></span>
- <span data-ttu-id="10beb-142">Vývoj může nastat napříč několika týmy, s menším třením, než nastane, když spousta týmů pracuje na jednom základu kódu.</span><span class="sxs-lookup"><span data-stu-id="10beb-142">Development can happen across multiple teams, with less friction than occurs when many teams work on a single codebase.</span></span>

<span data-ttu-id="10beb-143">Přechod ke zvýšení virtualizace, cloud computingu, kontejnerům a Internet věcí přispěl k průběžnému nárůstu mikroslužeb.</span><span class="sxs-lookup"><span data-stu-id="10beb-143">The move towards increasing virtualization, cloud computing, containers and the Internet of Things have contributed to the ongoing rise of microservices.</span></span> <span data-ttu-id="10beb-144">Mikroslužby ale nemají žádné výzvy.</span><span class="sxs-lookup"><span data-stu-id="10beb-144">However, microservices aren't without their challenges.</span></span> <span data-ttu-id="10beb-145">Fragmentovaná nebo decentralizovaná infrastruktura se podrobněji zakládá na potřebě jednoduchosti a rychlosti při komunikaci mezi službami.</span><span class="sxs-lookup"><span data-stu-id="10beb-145">The fragmented/decentralized infrastructure placed more emphasis on the need for simplicity and speed when communicating between services.</span></span> <span data-ttu-id="10beb-146">Tím se zaznamenala pozornost na určitou pracné a neobčanskoprávní povahu protokolu SOAP.</span><span class="sxs-lookup"><span data-stu-id="10beb-146">This in turn drew attention to the sometimes laborious and contorted nature of SOAP.</span></span>

<span data-ttu-id="10beb-147">Bylo v tomto prostředí, které gRPC bylo spuštěno, 10 let po prvním vydání služby WCF od společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="10beb-147">It was into this environment that gRPC was launched, 10 years after Microsoft first released WCF.</span></span> <span data-ttu-id="10beb-148">GRPC se vyvinula přímo z interní infrastruktury vzdáleného volání procedur (Stubby) Google na základě stejných standardů a protokolů, které informovaly o parametrech řady předchozích vzdálených volání procedur (RPC).</span><span class="sxs-lookup"><span data-stu-id="10beb-148">Evolved directly from Google’s internal infrastructure RPC (Stubby), gRPC was never based on the same standards and protocols that had informed the parameters of many earlier RPCs.</span></span> <span data-ttu-id="10beb-149">Kromě toho gRPCa na základě HTTP/2 a to je důvod, proč by se mohl nakreslit na nové funkce, které poskytují rozšířený transportní protokol.</span><span class="sxs-lookup"><span data-stu-id="10beb-149">Additionally, gRPC was only ever based on HTTP/2 and that's why it could draw on the new capabilities that advanced transport protocol provided.</span></span> <span data-ttu-id="10beb-150">Konkrétně obousměrné streamování, binární zasílání zpráv a multiplexing.</span><span class="sxs-lookup"><span data-stu-id="10beb-150">In particular, bidirectional streaming, binary messaging, and multiplexing.</span></span>

## <a name="about-this-guide"></a><span data-ttu-id="10beb-151">O této příručce</span><span class="sxs-lookup"><span data-stu-id="10beb-151">About this guide</span></span>

<span data-ttu-id="10beb-152">Tato příručka se věnuje klíčovým funkcím gRPC.</span><span class="sxs-lookup"><span data-stu-id="10beb-152">This guide covers the key features of gRPC.</span></span> <span data-ttu-id="10beb-153">Úvodní kapitoly přebírají nejvyšší úroveň v hlavních funkcích WCF a porovnávají je s gRPC.</span><span class="sxs-lookup"><span data-stu-id="10beb-153">The early chapters take a high-level look at the main features of WCF and compare them to gRPC.</span></span> <span data-ttu-id="10beb-154">Identifikuje, kde jsou přímé korelace mezi WCF a gRPC a také tam, kde gRPC nabízí výhodu.</span><span class="sxs-lookup"><span data-stu-id="10beb-154">It identifies where the are direct correlations between WCF and gRPC and also where gRPC offers an advantage.</span></span> <span data-ttu-id="10beb-155">V případě, že není žádná korelace mezi WCF a gRPC nebo kde gRPC není schopná nabídnout stejné řešení jako WCF, bude tato příručka navrhovat alternativní řešení nebo místa, kde se dozvíte, kde můžete získat další informace.</span><span class="sxs-lookup"><span data-stu-id="10beb-155">Where there's no correlation between WCF and gRPC or where gRPC isn't able to offer an equivalent solution to WCF, this guide will suggest workarounds or places to go for further information.</span></span>

<span data-ttu-id="10beb-156">Pomocí sady ukázkových aplikací WCF je kapitola 5 obsáhlá podrobněá, která se přechází na převod hlavních typů služby WCF (jednoduchá požadavek-odpověď, jednosměrná a streamovaná) na jejich ekvivalenty v gRPC.</span><span class="sxs-lookup"><span data-stu-id="10beb-156">Using a set of sample WCF applications, Chapter 5 is a deep dive look at a converting the main types of WCF service (simple request-reply, one-way, and streaming) to their equivalents in gRPC.</span></span>

<span data-ttu-id="10beb-157">V poslední části této knihy se dozvíte, jak získat nejlepší z gRPC v praxi, včetně použití dalších nástrojů, jako jsou kontejnery Docker nebo Kubernetes, k využití efektivity gRPC a podrobného zobrazení sledování pomocí protokolování, metrik a distribuovaných probíhá.</span><span class="sxs-lookup"><span data-stu-id="10beb-157">The final section of the book looks at how to get the best from gRPC in practice, including using additional tools like Docker containers or Kubernetes to leverage to the efficiency of gRPC, and a detailed look at the monitoring with logging, metrics, and distributed tracing.</span></span>

## <a name="whom-this-guide-is-for"></a><span data-ttu-id="10beb-158">Pro kterou je tato příručka určena</span><span class="sxs-lookup"><span data-stu-id="10beb-158">Whom this guide is for</span></span>

<span data-ttu-id="10beb-159">Tato příručka je určená pro vývojáře, kteří pracují v .NET Framework nebo .NET Core, kteří dříve používali WCF a kteří chtějí migrovat své aplikace do moderního prostředí RPC pro .NET Core 3,0 a novější verze.</span><span class="sxs-lookup"><span data-stu-id="10beb-159">This guide was written for developers working in .NET Framework or .NET Core who have previously used WCF and who are seeking to migrate their applications to a modern RPC environment for .NET Core 3.0 and later versions.</span></span> <span data-ttu-id="10beb-160">Průvodce může být také obecně používán pro vývojáře, kteří upgradují nebo berou v úvahách o upgradu na rozhraní .NET Core 3,0, kteří chtějí používat integrované nástroje gRPC.</span><span class="sxs-lookup"><span data-stu-id="10beb-160">The guide may also be of use more generally for developers upgrading or considering upgrading to .NET Core 3.0 who want to use the built-in gRPC tools.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="10beb-161">[Předchozí](index.md)
>[Další](grpc-overview.md)</span><span class="sxs-lookup"><span data-stu-id="10beb-161">[Previous](index.md)
[Next](grpc-overview.md)</span></span>