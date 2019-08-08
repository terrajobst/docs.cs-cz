---
title: Požadavky na architekturu bez serveru – aplikace bez serveru
description: Seznamte se s problémy při navrhování aplikací bez serveru, od správy stavů a trvalého úložiště pro škálování, protokolování, trasování a diagnostiku.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: ecbffbbd435b4926608e4def519fdaddddab688d
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/30/2019
ms.locfileid: "68676745"
---
# <a name="serverless-architecture-considerations"></a><span data-ttu-id="7897d-103">Důležité informace o bezserverové architektuře</span><span class="sxs-lookup"><span data-stu-id="7897d-103">Serverless architecture considerations</span></span>

<span data-ttu-id="7897d-104">Při přijetí architektury bez serveru se dokončí některé problémy.</span><span class="sxs-lookup"><span data-stu-id="7897d-104">Adopting a serverless architecture does come with certain challenges.</span></span> <span data-ttu-id="7897d-105">V této části se seznámíte s některými častými požadavky, které je třeba znát.</span><span class="sxs-lookup"><span data-stu-id="7897d-105">This section explores some of the more common considerations to be aware of.</span></span> <span data-ttu-id="7897d-106">Všechny tyto výzvy mají řešení.</span><span class="sxs-lookup"><span data-stu-id="7897d-106">All of these challenges have solutions.</span></span> <span data-ttu-id="7897d-107">Stejně jako u všech možností architektury by rozhodnutí o použití bez serveru mělo být provedeno až po pečlivém zvážení specialistů a nevýhody.</span><span class="sxs-lookup"><span data-stu-id="7897d-107">As with all architecture choices, the decision to go serverless should be made only after carefully considering the pros and cons.</span></span> <span data-ttu-id="7897d-108">V závislosti na potřebách vaší aplikace se můžete rozhodnout, že implementace bez serveru není správného řešení pro určité součásti.</span><span class="sxs-lookup"><span data-stu-id="7897d-108">Depending on the needs of your application, you may decide a serverless implementation isn't the right solution for certain components.</span></span>

## <a name="managing-state"></a><span data-ttu-id="7897d-109">Správa stavu</span><span class="sxs-lookup"><span data-stu-id="7897d-109">Managing state</span></span>

<span data-ttu-id="7897d-110">Funkce bez serveru, stejně jako u mikroslužeb obecně, jsou ve výchozím nastavení bezstavové.</span><span class="sxs-lookup"><span data-stu-id="7897d-110">Serverless functions, as with microservices in general, are stateless by default.</span></span> <span data-ttu-id="7897d-111">Zamezení stavu umožňuje neprovádět dočasné navýšení kapacity bez serveru, škálovat je a zajistit odolnost bez centrálního bodu selhání.</span><span class="sxs-lookup"><span data-stu-id="7897d-111">Avoiding state enables serverless to be ephemeral, to scale out, and to provide resiliency without a central point of failure.</span></span> <span data-ttu-id="7897d-112">V některých případech obchodní procesy vyžadují stav.</span><span class="sxs-lookup"><span data-stu-id="7897d-112">In some circumstances, business processes require state.</span></span> <span data-ttu-id="7897d-113">Pokud váš proces vyžaduje stav, máte dvě možnosti.</span><span class="sxs-lookup"><span data-stu-id="7897d-113">If your process requires state, you have two options.</span></span> <span data-ttu-id="7897d-114">Můžete použít jiný model než bez serveru nebo pracovat se samostatnou službou, která poskytuje stav.</span><span class="sxs-lookup"><span data-stu-id="7897d-114">You can adopt a model other than serverless, or interact with a separate service that provides state.</span></span> <span data-ttu-id="7897d-115">Přidáním stavu můžete řešení zkomplikovat a ztížit jeho škálování a potenciálně vytvořit jediný bod selhání.</span><span class="sxs-lookup"><span data-stu-id="7897d-115">Adding state can complicate the solution and make it harder to scale, and potentially create a single point of failure.</span></span> <span data-ttu-id="7897d-116">Pečlivě zvažte, jestli vaše funkce naprosto vyžaduje stav.</span><span class="sxs-lookup"><span data-stu-id="7897d-116">Carefully consider whether your function absolutely requires state.</span></span> <span data-ttu-id="7897d-117">Pokud je odpověď "Ano", určí, jestli je stále vhodná pro implementaci bez serveru.</span><span class="sxs-lookup"><span data-stu-id="7897d-117">If the answer is "yes," determine whether it still makes sense to implement it with serverless.</span></span>

<span data-ttu-id="7897d-118">Existuje několik řešení, která je potřeba přijmout, aniž byste ohrozili výhody bez serveru.</span><span class="sxs-lookup"><span data-stu-id="7897d-118">There are several solutions to adopt state without compromising the benefits of serverless.</span></span> <span data-ttu-id="7897d-119">Mezi oblíbená řešení patří:</span><span class="sxs-lookup"><span data-stu-id="7897d-119">Some of the more popular solutions include:</span></span>

* <span data-ttu-id="7897d-120">Použít dočasné úložiště dat nebo distribuovanou mezipaměť, jako je Redis</span><span class="sxs-lookup"><span data-stu-id="7897d-120">Use a temporary data store or distributed cache, like Redis</span></span>
* <span data-ttu-id="7897d-121">Uložení stavu v databázi, jako je SQL nebo CosmosDB</span><span class="sxs-lookup"><span data-stu-id="7897d-121">Store state in a database, like SQL or CosmosDB</span></span>
* <span data-ttu-id="7897d-122">Stav zpracování prostřednictvím modulu pracovního postupu, jako jsou trvalé funkce</span><span class="sxs-lookup"><span data-stu-id="7897d-122">Handle state through a workflow engine like durable functions</span></span>

<span data-ttu-id="7897d-123">Dolním řádkem je, že byste měli znát potřebu jakékoli správy stavů v rámci procesů, které zvažujete k implementaci bez serveru.</span><span class="sxs-lookup"><span data-stu-id="7897d-123">The bottom line is that you should be aware of the need for any state management within processes you're considering to implement with serverless.</span></span>

## <a name="long-running-processes"></a><span data-ttu-id="7897d-124">Dlouhotrvající procesy</span><span class="sxs-lookup"><span data-stu-id="7897d-124">Long-running processes</span></span>

<span data-ttu-id="7897d-125">Mnohé výhody bez serveru se spoléhají na procesy, které jsou v dočasném případě.</span><span class="sxs-lookup"><span data-stu-id="7897d-125">Many benefits of serverless rely on the processes being ephemeral.</span></span> <span data-ttu-id="7897d-126">Krátkou dobu běhu usnadňuje poskytovateli bez serveru uvolnění prostředků jako funkcí end a sdílení funkcí napříč hostiteli.</span><span class="sxs-lookup"><span data-stu-id="7897d-126">Short run times make it easier for the serverless provider to free up resources as functions end and share functions across hosts.</span></span> <span data-ttu-id="7897d-127">Většina poskytovatelů cloudu omezuje celkovou dobu, po kterou může být funkce spuštěná přibližně na 10 minut.</span><span class="sxs-lookup"><span data-stu-id="7897d-127">Most cloud providers limit the total time your function can run to around 10 minutes.</span></span> <span data-ttu-id="7897d-128">Pokud váš proces může trvat delší dobu, můžete zvážit alternativní implementaci.</span><span class="sxs-lookup"><span data-stu-id="7897d-128">If your process may take longer, you might consider an alternative implementation.</span></span>

<span data-ttu-id="7897d-129">Existuje několik výjimek a řešení.</span><span class="sxs-lookup"><span data-stu-id="7897d-129">There are a few exceptions and solutions.</span></span> <span data-ttu-id="7897d-130">Jedním z řešení může být přerušit proces na menší součásti, které jsou jednotlivě časově spouštěny.</span><span class="sxs-lookup"><span data-stu-id="7897d-130">One solution may be to break your process into smaller components that individually take less time to run.</span></span> <span data-ttu-id="7897d-131">Pokud proces běží dlouho z důvodu závislostí, můžete také zvážit asynchronní pracovní postup pomocí řešení, jako jsou trvalé funkce.</span><span class="sxs-lookup"><span data-stu-id="7897d-131">If your process runs long because of dependencies, you can also consider an asynchronous workflow using a solution like durable functions.</span></span> <span data-ttu-id="7897d-132">Trvalé funkce se pozastaví a udržují stav procesu, zatímco čeká na dokončení externího procesu.</span><span class="sxs-lookup"><span data-stu-id="7897d-132">Durable functions pause and maintain the state of your process while it's waiting on an external process to finish.</span></span> <span data-ttu-id="7897d-133">Asynchronní zpracování zkracuje čas skutečného spuštění procesu.</span><span class="sxs-lookup"><span data-stu-id="7897d-133">Asynchronous handling reduces the time the actual process runs.</span></span>

## <a name="startup-time"></a><span data-ttu-id="7897d-134">Čas spuštění</span><span class="sxs-lookup"><span data-stu-id="7897d-134">Startup time</span></span>

<span data-ttu-id="7897d-135">Jedním z možných obav s implementacemi bez serveru je čas spuštění.</span><span class="sxs-lookup"><span data-stu-id="7897d-135">One potential concern with serverless implementations is startup time.</span></span> <span data-ttu-id="7897d-136">Pro zachování prostředků mnoho poskytovatelů bez serveru vytvoří infrastrukturu "na vyžádání".</span><span class="sxs-lookup"><span data-stu-id="7897d-136">To conserve resources, many serverless providers create infrastructure "on demand."</span></span> <span data-ttu-id="7897d-137">Pokud se po uplynutí určité doby aktivuje funkce bez serveru, může být potřeba vytvořit nebo restartovat prostředky pro hostování funkce.</span><span class="sxs-lookup"><span data-stu-id="7897d-137">When a serverless function is triggered after a period of time, the resources to host the function may need to be created or restarted.</span></span> <span data-ttu-id="7897d-138">V některých situacích může studené zahájení způsobit zpoždění v několika sekundách.</span><span class="sxs-lookup"><span data-stu-id="7897d-138">In some situations, cold starts may result in delays of several seconds.</span></span> <span data-ttu-id="7897d-139">Čas spuštění se liší mezi poskytovateli a úrovněmi služeb.</span><span class="sxs-lookup"><span data-stu-id="7897d-139">Startup time varies across providers and service levels.</span></span> <span data-ttu-id="7897d-140">K dispozici je několik přístupů, které řeší dobu spuštění, pokud je důležité minimalizovat úspěšnost aplikace.</span><span class="sxs-lookup"><span data-stu-id="7897d-140">There are a few approaches to address startup time if it's important to minimize for the success of the app.</span></span>

* <span data-ttu-id="7897d-141">Někteří poskytovatelé umožňují uživatelům platit za úrovně služeb, které zaručují infrastrukturu "Always On".</span><span class="sxs-lookup"><span data-stu-id="7897d-141">Some providers allow users to pay for service levels that guarantee infrastructure is "always on".</span></span>
* <span data-ttu-id="7897d-142">Implementujte mechanismus Keep-Alive (pomocí příkazu příkazového koncového bodu otestujte koncový bod a zachovejte ho).</span><span class="sxs-lookup"><span data-stu-id="7897d-142">Implement a keep-alive mechanism (ping the endpoint to keep it "awake").</span></span>
* <span data-ttu-id="7897d-143">Použijte orchestraci jako Kubernetes s přístupem k vydaným funkcím (hostitel už je spuštěný, takže rozchází nové instance je velmi rychlé).</span><span class="sxs-lookup"><span data-stu-id="7897d-143">Use orchestration like Kubernetes with a containerized function approach (the host is already running so spinning up new instances is extremely fast).</span></span>

## <a name="database-updates-and-migrations"></a><span data-ttu-id="7897d-144">Aktualizace a migrace databáze</span><span class="sxs-lookup"><span data-stu-id="7897d-144">Database updates and migrations</span></span>

<span data-ttu-id="7897d-145">Výhodou kódu bez serveru je, že můžete uvolnit nové funkce, aniž byste museli znovu nasazovat celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="7897d-145">An advantage of serverless code is that you can release new functions without having to redeploy the entire application.</span></span> <span data-ttu-id="7897d-146">Tato výhoda se může stát nevýhodou, když se účastní relační databáze.</span><span class="sxs-lookup"><span data-stu-id="7897d-146">This advantage can become a disadvantage when there's a relational database involved.</span></span> <span data-ttu-id="7897d-147">Změny v schématech databáze je obtížné synchronizovat s aktualizacemi bez serveru.</span><span class="sxs-lookup"><span data-stu-id="7897d-147">Changes to database schemas are difficult to synchronize with serverless updates.</span></span> <span data-ttu-id="7897d-148">K dalším problémům dochází, když se něco nepovede a změny se musí vrátit zpátky.</span><span class="sxs-lookup"><span data-stu-id="7897d-148">Additional challenges are posed when things go wrong and the changes must be rolled back.</span></span> <span data-ttu-id="7897d-149">Integrita dat je jedním z důvodů, že pro mikroslužby a funkce bez serveru je vhodné, aby si vlastní data.</span><span class="sxs-lookup"><span data-stu-id="7897d-149">Data integrity is one reason that a best practice for microservices and serverless functions is that they own their own data.</span></span> <span data-ttu-id="7897d-150">Změny je možné nasadit jako jednu jednotku výpočetních prostředků a dat.</span><span class="sxs-lookup"><span data-stu-id="7897d-150">It is possible to deploy changes as a single unit of compute and data.</span></span> <span data-ttu-id="7897d-151">Realitou je, že mnoho starších systémů funguje jako Velká databáze back-end, která musí být odsouhlasena s architekturou bez serveru.</span><span class="sxs-lookup"><span data-stu-id="7897d-151">The reality is that many legacy systems feature a large back-end database that must be reconciled with the serverless architecture.</span></span>

<span data-ttu-id="7897d-152">Oblíbeným přístupem k řešení správy verzí schématu je nikdy Neupravovat stávající vlastnosti a sloupce, ale místo toho přidat nové informace.</span><span class="sxs-lookup"><span data-stu-id="7897d-152">A popular approach to solve schema versioning is to never modify existing properties and columns, but instead add new information.</span></span> <span data-ttu-id="7897d-153">Zvažte například změnu pro přesun z logického příznaku "dokončeno" pro seznam TODO na "datum dokončení".</span><span class="sxs-lookup"><span data-stu-id="7897d-153">For example, consider a change to move from a Boolean "completed" flag for a todo list to a "completed date."</span></span> <span data-ttu-id="7897d-154">Místo odebrání starého pole bude tato změna databáze:</span><span class="sxs-lookup"><span data-stu-id="7897d-154">Instead of removing the old field, the database change will:</span></span>

1. <span data-ttu-id="7897d-155">Přidejte nové pole "datum dokončení".</span><span class="sxs-lookup"><span data-stu-id="7897d-155">Add a new "completed date" field.</span></span>
1. <span data-ttu-id="7897d-156">Transformujte pole "dokončeno" Boolean na vypočtenou funkci, která vyhodnotí, zda je datum dokončení po aktuálním datu.</span><span class="sxs-lookup"><span data-stu-id="7897d-156">Transform the "completed" Boolean field to a computed function that evaluates whether the completed date is after the current date.</span></span>
1. <span data-ttu-id="7897d-157">Přidejte Trigger, který nastaví datum dokončení na aktuální datum, kdy je dokončená logická hodnota nastavena na true (pravda).</span><span class="sxs-lookup"><span data-stu-id="7897d-157">Add a trigger to set the completed date to the current date when the completed Boolean is set to true.</span></span>

<span data-ttu-id="7897d-158">Sekvence změn zajišťuje, že starší verze kódu nadále běží "tak jak jsou", zatímco novější funkce bez serveru můžou využít nové pole.</span><span class="sxs-lookup"><span data-stu-id="7897d-158">The sequence of changes ensures that legacy code continues to run "as is" while newer serverless functions can take advantage of the new field.</span></span>

<span data-ttu-id="7897d-159">Další informace o datech v architekturách bez serveru najdete v tématu [výzvy a řešení pro správu distribuovaných dat](../microservices/architect-microservice-container-applications/distributed-data-management.md).</span><span class="sxs-lookup"><span data-stu-id="7897d-159">For more information about data in serverless architectures, see [Challenges and solutions for distributed data management](../microservices/architect-microservice-container-applications/distributed-data-management.md).</span></span>

## <a name="scaling"></a><span data-ttu-id="7897d-160">Škálování</span><span class="sxs-lookup"><span data-stu-id="7897d-160">Scaling</span></span>

<span data-ttu-id="7897d-161">Jedná se o běžný nepojmový koncept, který znamená bez serveru.</span><span class="sxs-lookup"><span data-stu-id="7897d-161">It's a common misconception that serverless means "no server."</span></span> <span data-ttu-id="7897d-162">Je ve skutečnosti "méně serveru".</span><span class="sxs-lookup"><span data-stu-id="7897d-162">It's in fact "less server."</span></span> <span data-ttu-id="7897d-163">Je důležité, abyste pochopili, že při škálování dojde k tomu, že budete vědět, co je záložní infrastruktura.</span><span class="sxs-lookup"><span data-stu-id="7897d-163">The fact there is a backing infrastructure is important to understand when it comes to scaling.</span></span> <span data-ttu-id="7897d-164">Většina platforem bez serveru poskytuje sadu ovládacích prvků, které zpracovávají, jak by se měla infrastruktura škálovat při zvyšování hustoty událostí.</span><span class="sxs-lookup"><span data-stu-id="7897d-164">Most serverless platforms provide a set of controls to handle how the infrastructure should scale when event density increases.</span></span> <span data-ttu-id="7897d-165">Můžete si vybrat z nejrůznějších možností, ale vaše strategie se může lišit v závislosti na funkci.</span><span class="sxs-lookup"><span data-stu-id="7897d-165">You can choose from a variety of options, but your strategy may vary depending on the function.</span></span> <span data-ttu-id="7897d-166">Kromě toho jsou funkce obvykle spouštěny v rámci souvisejícího hostitele, takže funkce na stejném hostiteli mají stejné možnosti škálování.</span><span class="sxs-lookup"><span data-stu-id="7897d-166">Furthermore, functions are typically run under a related host, so that functions on the same host have the same scale options.</span></span> <span data-ttu-id="7897d-167">Proto je nutné organizovat a strategize, které funkce jsou hostovány společně na základě požadavků na škálování.</span><span class="sxs-lookup"><span data-stu-id="7897d-167">Therefore it is necessary to organize and strategize which functions are hosted together based on scale requirements.</span></span>

<span data-ttu-id="7897d-168">Pravidla často určují způsob horizontálního navýšení kapacity (zvýšení počtu prostředků hostitele) a horizontální navýšení kapacity (zvýšení počtu instancí hostitele) na základě různých parametrů.</span><span class="sxs-lookup"><span data-stu-id="7897d-168">Rules often specify how to scale-up (increase the host resources) and scale-out (increase the number of host instances) based on varying parameters.</span></span> <span data-ttu-id="7897d-169">Aktivační události pro škálování můžou zahrnovat plán, sazby požadavků, využití procesoru a využití paměti.</span><span class="sxs-lookup"><span data-stu-id="7897d-169">Triggers for scales may include schedule, request rates, CPU utilization, and memory usage.</span></span> <span data-ttu-id="7897d-170">Vyšší výkon často přináší větší náklady.</span><span class="sxs-lookup"><span data-stu-id="7897d-170">Higher performance often comes at a greater cost.</span></span> <span data-ttu-id="7897d-171">Levnější přístupy založené na spotřebě se nemusí škálovat tak rychle, když se míra požadavků náhle rozroste.</span><span class="sxs-lookup"><span data-stu-id="7897d-171">The less expensive, consumption-based approaches may not scale as quickly when the request rate suddenly increases.</span></span> <span data-ttu-id="7897d-172">Existuje kompromis mezi platbou předem před "náklady na pojištění" a riziky pomalejších reakcí z důvodu náhlého nárůstu zatížení.</span><span class="sxs-lookup"><span data-stu-id="7897d-172">There is a trade-off between paying up front "insurance cost" versus paying strictly "as you go" and risking slower responses due to sudden increases in demand.</span></span>

## <a name="monitoring-tracing-and-logging"></a><span data-ttu-id="7897d-173">Monitorování, trasování a protokolování</span><span class="sxs-lookup"><span data-stu-id="7897d-173">Monitoring, tracing, and logging</span></span>

<span data-ttu-id="7897d-174">Často přehlédnutíný aspekt DevOps je monitorování aplikací po nasazení.</span><span class="sxs-lookup"><span data-stu-id="7897d-174">An often overlooked aspect of DevOps is monitoring applications once deployed.</span></span> <span data-ttu-id="7897d-175">Je důležité mít strategii pro monitorování funkcí bez serveru.</span><span class="sxs-lookup"><span data-stu-id="7897d-175">It's important to have a strategy for monitoring serverless functions.</span></span> <span data-ttu-id="7897d-176">Největší výzvou je často korelace nebo rozpoznávání, když uživatel volá více funkcí jako součást stejné interakce.</span><span class="sxs-lookup"><span data-stu-id="7897d-176">The biggest challenge is often correlation, or recognizing when a user calls multiple functions as part of the same interaction.</span></span> <span data-ttu-id="7897d-177">Většina platforem bez serveru umožňuje protokolování konzoly, které lze importovat do nástrojů třetích stran.</span><span class="sxs-lookup"><span data-stu-id="7897d-177">Most serverless platforms allow console logging that can be imported into third-party tools.</span></span> <span data-ttu-id="7897d-178">K dispozici jsou také možnosti pro automatizaci shromažďování telemetrie, generování a sledování ID korelace a sledování konkrétních akcí, které poskytují podrobné přehledy.</span><span class="sxs-lookup"><span data-stu-id="7897d-178">There are also options to automate collection of telemetry, generate and track correlation IDs, and monitor specific actions to provide detailed insights.</span></span> <span data-ttu-id="7897d-179">Azure poskytuje pokročilou [Application Insights platformu](https://docs.microsoft.com/azure/azure-functions/functions-monitoring) pro monitorování a analýzu.</span><span class="sxs-lookup"><span data-stu-id="7897d-179">Azure provides the advanced [Application Insights platform](https://docs.microsoft.com/azure/azure-functions/functions-monitoring) for monitoring and analytics.</span></span>

## <a name="inter-service-dependencies"></a><span data-ttu-id="7897d-180">Závislosti mezi službami</span><span class="sxs-lookup"><span data-stu-id="7897d-180">Inter-service dependencies</span></span>

<span data-ttu-id="7897d-181">Architektura bez serveru může zahrnovat funkce, které spoléhají na jiné funkce.</span><span class="sxs-lookup"><span data-stu-id="7897d-181">A serverless architecture may include functions that rely on other functions.</span></span> <span data-ttu-id="7897d-182">Ve skutečnosti se nejedná o architekturu bez serveru, aby mohla více služeb navzájem volat v rámci interakce nebo distribuované transakce.</span><span class="sxs-lookup"><span data-stu-id="7897d-182">In fact, it isn't uncommon in a serverless architecture to have multiple services call each other as part of an interaction or distributed transaction.</span></span> <span data-ttu-id="7897d-183">Aby se zabránilo silnému propojení, doporučujeme, aby se služby přímo neodkazovaly na sebe.</span><span class="sxs-lookup"><span data-stu-id="7897d-183">To avoid strong coupling, it's recommended that services don't reference each other directly.</span></span> <span data-ttu-id="7897d-184">Pokud je potřeba změnit koncový bod služby, může přímý odkaz vést k významnému refaktoringu.</span><span class="sxs-lookup"><span data-stu-id="7897d-184">When the endpoint for a service needs to change, direct references could result in major refactoring.</span></span> <span data-ttu-id="7897d-185">Navrhovaným řešením je poskytnout mechanismus zjišťování služby, jako je například registr, který poskytuje příslušný koncový bod pro typ požadavku.</span><span class="sxs-lookup"><span data-stu-id="7897d-185">A suggested solution is to provide a service discovery mechanism, such as a registry, that provides the appropriate end point for a request type.</span></span> <span data-ttu-id="7897d-186">Dalším řešením je využít služby zasílání zpráv, jako jsou fronty nebo témata pro komunikaci mezi službami.</span><span class="sxs-lookup"><span data-stu-id="7897d-186">Another solution is to leverage messaging services like queues or topics for communication between services.</span></span>

## <a name="managing-failure-and-providing-resiliency"></a><span data-ttu-id="7897d-187">Správa selhání a zajištění odolnosti</span><span class="sxs-lookup"><span data-stu-id="7897d-187">Managing failure and providing resiliency</span></span>

<span data-ttu-id="7897d-188">Je také důležité vzít v úvahu *vzor okruhu a přerušení*: Pokud z nějakého důvodu se služba stále nedaří, není vhodné tuto službu volat opakovaně.</span><span class="sxs-lookup"><span data-stu-id="7897d-188">It's also important to consider the *circuit-breaker pattern*: If, for some reason, a service continues to fail, it isn't advisable to call that service repeatedly.</span></span> <span data-ttu-id="7897d-189">Místo toho se zavolá alternativní služba nebo se vrátí zpráva, dokud není znovu vytvořen stav závislé služby.</span><span class="sxs-lookup"><span data-stu-id="7897d-189">Instead, an alternative service is called or a message returned until the health of the dependent service is re-established.</span></span> <span data-ttu-id="7897d-190">Architektura bez serveru musí vzít v úvahu strategii pro řešení a správu závislostí mezi službami.</span><span class="sxs-lookup"><span data-stu-id="7897d-190">The serverless architecture needs to take into account the strategy for resolving and managing inter-service dependencies.</span></span>

<span data-ttu-id="7897d-191">Aby bylo možné pokračovat ve vzorku okruhu, je nutné, aby služba byla odolná proti chybám a odolná.</span><span class="sxs-lookup"><span data-stu-id="7897d-191">To continue the circuit-breaker pattern, services need to be fault tolerant and resilient.</span></span> <span data-ttu-id="7897d-192">Odolnost proti chybám znamená schopnost vaší aplikace pokračovat v běhu i po neočekávaných výjimkách nebo při zjištění neplatných stavů.</span><span class="sxs-lookup"><span data-stu-id="7897d-192">Fault tolerance refers to the ability of your application to continue running even after unexpected exceptions or invalid states are encountered.</span></span> <span data-ttu-id="7897d-193">Odolnost proti chybám je obvykle funkcí samotného kódu a způsobu jejich zápisu pro zpracování výjimek.</span><span class="sxs-lookup"><span data-stu-id="7897d-193">Fault tolerance is typically a function of the code itself and how it's written to handle exceptions.</span></span> <span data-ttu-id="7897d-194">Odolnost proti chybám označuje, jak může aplikace při obnovování selhat.</span><span class="sxs-lookup"><span data-stu-id="7897d-194">Resiliency refers to how capable the app is at recovering from failures.</span></span> <span data-ttu-id="7897d-195">Odolnost proti chybám je často spravovaná platformou bez serveru.</span><span class="sxs-lookup"><span data-stu-id="7897d-195">Resiliency is often managed by the serverless platform.</span></span> <span data-ttu-id="7897d-196">Platforma by měla být schopná aktivovat novou instanci funkce bez serveru, když se stávající instance nezdařila.</span><span class="sxs-lookup"><span data-stu-id="7897d-196">The platform should be able to spin up a new serverless function instance when the existing one fails.</span></span> <span data-ttu-id="7897d-197">Platforma by měla být také inteligentní, aby zastavila nové instance, když dojde k chybě každé nové instance.</span><span class="sxs-lookup"><span data-stu-id="7897d-197">The platform should also be intelligent enough to stop spinning up new instances when every new instance fails.</span></span>

<span data-ttu-id="7897d-198">Další informace najdete v tématu [implementace vzoru pro přerušení okruhů](../microservices/implement-resilient-applications/implement-circuit-breaker-pattern.md).</span><span class="sxs-lookup"><span data-stu-id="7897d-198">For more information, see [Implementing the Circuit Breaker pattern](../microservices/implement-resilient-applications/implement-circuit-breaker-pattern.md).</span></span>

## <a name="versioning-and-greenblue-deployments"></a><span data-ttu-id="7897d-199">Nasazování verzí a zelených a modrých nasazení</span><span class="sxs-lookup"><span data-stu-id="7897d-199">Versioning and green/blue deployments</span></span>

<span data-ttu-id="7897d-200">Hlavní výhodou bez serveru je možnost upgradovat konkrétní funkci, aniž by bylo nutné znovu nasazovat celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="7897d-200">A major benefit of serverless is the ability to upgrade a specific function without having to redeploy the entire application.</span></span> <span data-ttu-id="7897d-201">Aby bylo možné upgrady provést, musí být funkce zavedeny se správou verzí, aby je služba volající je směrovala na správnou verzi kódu.</span><span class="sxs-lookup"><span data-stu-id="7897d-201">For upgrades to be successful, functions must be versioned so that services calling them are routed to the correct version of code.</span></span> <span data-ttu-id="7897d-202">Strategie pro nasazení nových verzí je taky důležitá.</span><span class="sxs-lookup"><span data-stu-id="7897d-202">A strategy for deploying new versions is also important.</span></span> <span data-ttu-id="7897d-203">Běžným přístupem je použití zelených a modrých nasazení.</span><span class="sxs-lookup"><span data-stu-id="7897d-203">A common approach is to use "green/blue deployments."</span></span> <span data-ttu-id="7897d-204">Zeleným nasazením je aktuální funkce.</span><span class="sxs-lookup"><span data-stu-id="7897d-204">The green deployment is the current function.</span></span> <span data-ttu-id="7897d-205">Nová "modrá" verze se nasadí do produkčního a testovaného.</span><span class="sxs-lookup"><span data-stu-id="7897d-205">A new "blue" version is deployed to production and tested.</span></span> <span data-ttu-id="7897d-206">Při testování projde zelená a modrá verze, takže nová verze bude živá.</span><span class="sxs-lookup"><span data-stu-id="7897d-206">When testing passes, the green and blue versions are swapped so the new version comes live.</span></span> <span data-ttu-id="7897d-207">Pokud se vyskytnou nějaké problémy, můžou se znovu zaměnit.</span><span class="sxs-lookup"><span data-stu-id="7897d-207">If any issues are encountered, they can be swapped back.</span></span> <span data-ttu-id="7897d-208">Podpora správy verzí a zelených a modrých nasazení vyžaduje kombinaci vytváření funkcí pro přizpůsobení změn verzí a práci s platformou bez serveru pro zpracování nasazení.</span><span class="sxs-lookup"><span data-stu-id="7897d-208">Supporting versioning and green/blue deployments requires a combination of authoring the functions to accommodate version changes and working with the serverless platform to handle deployments.</span></span> <span data-ttu-id="7897d-209">Jedním z možných způsobů je použití proxy serverů, které jsou popsané v kapitole [platforma bez serveru Azure](azure-functions.md#proxies) .</span><span class="sxs-lookup"><span data-stu-id="7897d-209">One possible approach is to use proxies, which are described in the [Azure serverless platform](azure-functions.md#proxies) chapter.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="7897d-210">[Předchozí](serverless-architecture.md)Další
>[](serverless-design-examples.md)</span><span class="sxs-lookup"><span data-stu-id="7897d-210">[Previous](serverless-architecture.md)
[Next](serverless-design-examples.md)</span></span>