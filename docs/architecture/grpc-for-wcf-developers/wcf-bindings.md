---
title: Vazby a přenosy WCF – gRPC pro vývojáře WCF
description: Přečtěte si, jak se liší vazby WCF a přenosy na gRPC.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 50bac73ee68d7156fc5fed55dfffb3ba7f2de924
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184055"
---
# <a name="wcf-bindings-and-transports"></a><span data-ttu-id="b1fa0-103">Vazby a přenosy WCF</span><span class="sxs-lookup"><span data-stu-id="b1fa0-103">WCF bindings and transports</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="b1fa0-104">WCF má spoustu různých předdefinovaných *vazeb* , které určují různé síťové protokoly, formáty drátů a další podrobnosti implementace.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-104">WCF has lots of different built-in *bindings* that specify different network protocols, wire formats, and other implementation details.</span></span> <span data-ttu-id="b1fa0-105">gRPC má efektivně jenom jeden síťový protokol a jeden telegrafický formát (technicky *může* být přizpůsobený síťový formát, ale je nad rámec této knihy).</span><span class="sxs-lookup"><span data-stu-id="b1fa0-105">gRPC effectively has just one network protocol and one wire format (technically the wire format *may* be customized, but that is beyond the scope of this book).</span></span> <span data-ttu-id="b1fa0-106">Pravděpodobně zjistíte, že gRPC nabízí nejlepší řešení ve většině případů.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-106">You are likely to discover that gRPC offers the best solution in most cases.</span></span> <span data-ttu-id="b1fa0-107">Níže je Stručná diskuze o nejdůležitějších vazbách WCF a jejich porovnání s jejich ekvivalentem v gRPC.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-107">What follows is a short discussion about the most relevant WCF bindings and how they compare to their equivalent in gRPC.</span></span>

## <a name="nettcp"></a><span data-ttu-id="b1fa0-108">NetTCP</span><span class="sxs-lookup"><span data-stu-id="b1fa0-108">NetTCP</span></span>

<span data-ttu-id="b1fa0-109">NetTCP vazba WCF umožňuje trvalá připojení, malé zprávy a obousměrné zasílání zpráv, ale funguje jenom mezi klienty a servery .NET.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-109">WCF's NetTCP binding allows for persistent connections, small messages, and two-way messaging but only works between .NET clients and servers.</span></span> <span data-ttu-id="b1fa0-110">gRPC umožňuje stejné funkce, ale podporuje se v různých programovacích jazycích a platformách.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-110">gRPC allows the same functionality but is supported across multiple programming languages and platforms.</span></span> <span data-ttu-id="b1fa0-111">gRPC má mnoho funkcí vazby WCF NetTCP, i když není vždy implementováno stejným způsobem.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-111">gRPC has many of the features of WCF NetTCP binding, although not always implemented in the same way.</span></span> <span data-ttu-id="b1fa0-112">Například v technologii WCF je šifrování řízeno prostřednictvím konfigurace a zpracovává se v rámci rozhraní.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-112">For example, in WCF, encryption is controlled through configuration and handled in the framework.</span></span> <span data-ttu-id="b1fa0-113">V gRPC se šifrování dosahuje na úrovni připojení pomocí protokolu HTTP/2 přes TLS.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-113">In gRPC, encryption is achieved at the connection level using HTTP/2 over TLS.</span></span>

## <a name="http"></a><span data-ttu-id="b1fa0-114">HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fa0-114">HTTP</span></span>

<span data-ttu-id="b1fa0-115">BasicHttpBinding WCF je všeobecně založené na textu, používá protokol SOAP jako formát drátu a je velmi pomalé standardy moderních síťových aplikací.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-115">WCF's BasicHttpBinding is generally text based, using SOAP as the wire format, and is very slow by the standards of modern networked applications.</span></span> <span data-ttu-id="b1fa0-116">Používá se jenom k zajištění interoperability mezi platformami nebo připojení přes internetovou infrastrukturu.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-116">It's only really used to provide cross-platform interoperability, or connection over internet infrastructure.</span></span> <span data-ttu-id="b1fa0-117">Ekvivalent v gRPC – protože používá protokol HTTP/2 jako podkladovou transportní vrstvu s binárním formátem Protobuf pro zprávy, může nabízet NetTCP výkon na úrovni služby, ale s plnou interoperabilitou mezi platformami a všemi moderními programovacími jazyky. rozhraní.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-117">The equivalent in gRPC—because it uses HTTP/2 as the underlying transport layer with the binary Protobuf wire format for messages—can offer NetTCP service level performance but with full cross-platform interoperability with all modern programming languages and frameworks.</span></span>

## <a name="named-pipes"></a><span data-ttu-id="b1fa0-118">Pojmenované kanály</span><span class="sxs-lookup"><span data-stu-id="b1fa0-118">Named Pipes</span></span>

<span data-ttu-id="b1fa0-119">Technologie WCF poskytovala vazbu pojmenovaných kanálů pro komunikaci mezi procesy na stejném fyzickém počítači.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-119">WCF provided a Named Pipes binding for communication between processes on the same physical machine.</span></span> <span data-ttu-id="b1fa0-120">Pojmenované kanály nejsou v první verzi ASP.NET Core gRPC podporovány.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-120">Named Pipes are not supported by the first release of ASP.NET Core gRPC.</span></span>

<span data-ttu-id="b1fa0-121">Mimo Windows jsou funkce poskytované pojmenovanými kanály místo toho obecně poskytovány pomocí soketů domény systému UNIX.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-121">Outside Windows, the functionality provided by Named Pipes is instead generally provided by Unix Domain Sockets.</span></span> <span data-ttu-id="b1fa0-122">Tyto sokety jsou běžné TCP jako sokety, které představují adresy souborového systému, `/var/run/docker.sock`například, které gRPC můžou pracovat s klientem i serverem.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-122">These sockets are regular TCP-like sockets represented with file-system addresses, such as `/var/run/docker.sock`, which gRPC can work with as both client and server.</span></span> <span data-ttu-id="b1fa0-123">Pokud ve Windows potřebujete použít funkci s pojmenovanými kanály, další aktualizace Windows 10 a Windows serveru ve 2019.4. čtvrtletí přidá doménové sokety jako plně podporovanou nativní funkci v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-123">If you need to use Named Pipes style functionality on Windows, the next update to Windows 10 and Windows Server, in 2019 Q4, adds Domain Sockets as a fully supported native feature within Windows.</span></span> <span data-ttu-id="b1fa0-124">Proto můžou služby gRPC běžící na těchto a novějších verzích Windows (nebo na Linux) používat k používání doménových soketů místo pojmenovaných kanálů.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-124">So, gRPC services running on these and later versions of Windows (or on Linux) can use Domain Sockets instead of Named Pipes.</span></span> <span data-ttu-id="b1fa0-125">Pokud ale tým není schopen aktualizovat na nejnovější verzi systému Windows, bude nutné použít hostitele TCP Sockets.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-125">However, if your team is unable to update to the latest version of Windows, then you'll need to use localhost TCP sockets.</span></span> <span data-ttu-id="b1fa0-126">Bezpečnostní informace týkající se používání místních soketů TCP lze řešit pomocí ověřování certifikátů mezi klientem a serverem.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-126">Security concerns about using local TCP sockets can be addressed with the use of certificate authentication between client and server.</span></span>

## <a name="msmq"></a><span data-ttu-id="b1fa0-127">MSMQ</span><span class="sxs-lookup"><span data-stu-id="b1fa0-127">MSMQ</span></span>

<span data-ttu-id="b1fa0-128">MSMQ je proprietární fronta zpráv Windows.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-128">MSMQ is a proprietary Windows message queue.</span></span> <span data-ttu-id="b1fa0-129">Vazba WCF na službu MSMQ umožňuje "požární a zapomenuté" žádosti od klientů, které mohou být zpracovány kdykoli později.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-129">WCF's binding to MSMQ enables "fire and forget" requests from clients that may be processed at any time in the future.</span></span> <span data-ttu-id="b1fa0-130">gRPC nativně neposkytuje žádné funkce fronty zpráv.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-130">gRPC doesn't natively provide any message queue functionality.</span></span> <span data-ttu-id="b1fa0-131">Nejlepší alternativou je přímé použití systému zasílání zpráv, jako je Azure Service Bus, RabbitMQ nebo Kafka.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-131">The best alternative would be to directly use a messaging system like Azure Service Bus, RabbitMQ, or Kafka.</span></span> <span data-ttu-id="b1fa0-132">To může být implementováno pomocí klienta, který umísťuje zprávy přímo do fronty, nebo služby streamování klienta gRPC, která zprávy zařadí do fronty.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-132">This could be implemented with the client placing messages directly onto the queue, or a gRPC client streaming service that enqueues the messages.</span></span>

## <a name="webhttpbinding"></a><span data-ttu-id="b1fa0-133">WebHttpBinding</span><span class="sxs-lookup"><span data-stu-id="b1fa0-133">WebHttpBinding</span></span>

<span data-ttu-id="b1fa0-134">WebHttpBinding (označované také jako WCF ReST) s `WebGet` atributy a `WebInvoke` umožňují vyvíjet ReSTful rozhraní API, která by mohla mluvit JSON v čase, kdy to bylo méně běžné než nyní.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-134">The WebHttpBinding (also known as WCF ReST), with the `WebGet` and `WebInvoke` attributes, enabled you to develop ReSTful APIs that could speak JSON at a time when this was less common than now.</span></span> <span data-ttu-id="b1fa0-135">Proto pokud máte rozhraní API RESTful vytvořené pomocí WCF REST, zvažte jeho migraci do běžné ASP.NET Core aplikace webového rozhraní API MVC, která by poskytovala ekvivalentní funkce namísto převodu na gRPC.</span><span class="sxs-lookup"><span data-stu-id="b1fa0-135">Therefore, if you have a RESTful API built with WCF REST, consider migrating it to a regular ASP.NET Core MVC Web API application, which would provide equivalent functionality, rather than converting to gRPC.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="b1fa0-136">[Předchozí](wcf-endpoints-grpc-methods.md)
>[Další](rpc-types.md)</span><span class="sxs-lookup"><span data-stu-id="b1fa0-136">[Previous](wcf-endpoints-grpc-methods.md)
[Next](rpc-types.md)</span></span>