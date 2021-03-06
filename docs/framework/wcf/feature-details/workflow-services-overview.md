---
title: Přehled služeb pracovních postupů
ms.date: 03/30/2017
ms.assetid: e536dda3-e286-441e-99a7-49ddc004b646
ms.openlocfilehash: cb013dd419d09af61eaff290709164427b1b655f
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75347865"
---
# <a name="workflow-services-overview"></a>Přehled služeb pracovních postupů

Služby pracovních postupů jsou služby založené na WCF, které jsou implementované pomocí pracovních postupů. Služby pracovních postupů jsou pracovní postupy, které používají aktivity zasílání zpráv k posílání a přijímání zpráv Windows Communication Foundation (WCF). .NET Framework 4,5 zavádí řadu aktivit zasílání zpráv, které umožňují odesílat a přijímat zprávy v rámci pracovního postupu. Další informace o aktivitách zasílání zpráv a o tom, jak je lze použít k implementaci různých vzorců výměny zpráv, najdete v tématu [aktivity zasílání zpráv](messaging-activities.md).

## <a name="benefits-of-using-workflow-services"></a>Výhody používání služeb pracovních postupů

Vzhledem k rostoucímu množství aplikací se jednotlivé služby stanou zodpovědností za volání dalších služeb, které přestanou práci na některých úlohách. Implementace těchto volání jako asynchronních operací zavádí určitou složitost kódu. Zpracování chyb přidává další složitost ve formě zpracování výjimek a poskytování podrobných informací o sledování. Některé služby jsou často dlouho spuštěné a při čekání na vstup můžou zabírat cenné systémové prostředky. Z důvodu těchto problémů jsou distribuované aplikace často velmi složité a obtížné je zapisovat a udržovat. Pracovní postupy představují přirozený způsob, jak vyjádřit koordinaci asynchronních prací, zejména volání na externí služby. Pracovní postupy jsou také efektivní v zastoupení dlouhodobě spuštěných obchodních procesů. Jsou to tyto kvality, díky kterým je pracovní postup skvělým prostředkem pro vytváření služeb v distribuovaném prostředí.

## <a name="implementing-a-workflow-service"></a>Implementace služby pracovního postupu

Při implementaci služby WCF definujete počet kontraktů, které popisují službu a data, která odesílá a přijímá. Data jsou reprezentována jako kontrakty dat a kontrakty zpráv. WCF i služba pracovních postupů používají jako součást popisů služeb kontrakt dat a definice kontraktů zpráv. Služba sama zveřejňuje metadata (ve formě WSDL) k popisu operací služby. V rámci WCF, kontrakty služeb a kontrakty operací definují službu a operace, které podporuje. Ve službě pracovních postupů se ale tyto smlouvy nacházejí v rámci samotného obchodního procesu. Jsou zpřístupněny v metadatech pomocí procesu nazývaného odvození kontraktu. Když je služba pracovního postupu hostovaná pomocí <xref:System.ServiceModel.Activities.WorkflowServiceHost>, prověří se definice pracovního postupu a vygeneruje se kontrakt na základě sady aktivit zasílání zpráv, které se v pracovním postupu nacházejí. K vygenerování kontraktu se používají zejména následující aktivity a vlastnosti:

Aktivita <xref:System.ServiceModel.Activities.Receive>

- <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>

- <xref:System.ServiceModel.Activities.Receive.OperationName%2A>

- <xref:System.ServiceModel.Activities.Receive.Action%2A>

Aktivita <xref:System.ServiceModel.Activities.SendReply>

- <xref:System.ServiceModel.Activities.SendReply.Action%2A>

Aktivita <xref:System.ServiceModel.Activities.TransactedReceiveScope>

Konečný výsledek odvození smlouvy je popis služby, která používá stejné datové struktury jako služby WCF a kontrakty operací. Tyto informace se pak použijí k vystavení WSDL pro službu pracovního postupu.

> [!NOTE]
> [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] neumožňuje psát služby pracovních postupů pomocí existující definice smlouvy bez nutnosti další podpory nástrojů. Kontrakty služby pracovního postupu se vytvářejí procesem odvození kontraktu, který je popsaný výše. Kontrakty zpráv a kontrakty dat se ale plně podporují.

## <a name="workflow-services-and-msmq-based-bindings"></a>Služby pracovních postupů a vazby založené na službě MSMQ

WCF definuje dvě vazby založené na službě MSMQ <xref:System.ServiceModel.NetMsmqBinding> a <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>.  Vazby založené na službě MSMQ se často používají se službami pracovních postupů kvůli dlouhodobé povaze takových služeb. Vazby založené na službě MSMQ mají vlastnost `ValidityDuration`, která určuje, jak dlouho mohou být zprávy služby MSMQ považovány za platné. Z důvodu dlouhodobého chodu služeb pracovních postupů je možné, že doba platnosti zprávy služby MSMQ může uplynout před tím, než ji služba pracovního postupu zpracuje. Je proto velmi důležité nastavit dobu platnosti vazby služby MSMQ na odpovídající hodnotu. Tato hodnota musí být zvolena na základě pracovního postupu a způsobu, jakým zpracovává zprávy. Pokud máte například pracovní postup s aktivitou <xref:System.ServiceModel.Activities.Receive> následovaný vlastní aktivitou, která trvá 10 minut, a za ní následuje jiná aktivita <xref:System.ServiceModel.Activities.Receive>, správná hodnota `ValidityDuration` by byla větší než 10 minut.

## <a name="hosting-a-workflow-service"></a>Hostování služby pracovního postupu

Podobně jako služby WCF musí být služby pracovních postupů hostované. Služby WCF používají třídu <xref:System.ServiceModel.ServiceHost> k hostování služeb a služeb pracovních postupů, které používají <xref:System.ServiceModel.Activities.WorkflowServiceHost> k hostování služeb. Podobně jako služby WCF je možné služby pracovních postupů hostovat různými způsoby, například:

- Ve spravované aplikaci .NET Framework.

- V Internetová informační služba (IIS).

- V aktivační službě procesů systému Windows (WAS).

- Ve spravované službě systému Windows.

Služby pracovních postupů hostované ve spravované aplikaci .NET Framework nebo spravované službě systému Windows vytvoří instanci třídy <xref:System.ServiceModel.Activities.WorkflowServiceHost> a předejte jí instanci <xref:System.ServiceModel.Activities.WorkflowService>, která obsahuje definici pracovního postupu v rámci vlastnosti <xref:System.ServiceModel.Activities.WorkflowService.Body%2A>. Definice pracovního postupu, která obsahuje aktivity zasílání zpráv, se zveřejňuje jako služba pracovního postupu.

Chcete-li hostovat službu pracovního postupu ve službě IIS nebo WAS, umístěte soubor. xamlx, který obsahuje definici služby pracovního postupu, do virtuálního adresáře. Výchozí koncový bod (pomocí <xref:System.ServiceModel.BasicHttpBinding>) se vytvoří automaticky a další informace najdete v tématu [zjednodušená konfigurace](../../../../docs/framework/wcf/simplified-configuration.md). Můžete také umístit soubor Web. config do virtuálního adresáře a zadat tak vlastní koncové body. Pokud je vaše definice pracovního postupu v sestavení, můžete umístit soubor. svc do virtuálního adresáře a sestavení pracovního postupu v adresáři App_Code. Soubor. svc musí určovat objekt pro vytváření hostitele služby a třídu, která implementuje službu pracovního postupu. Následující příklad ukazuje, jak zadat objekt pro vytváření hostitele služby a zadat třídu, která implementuje službu pracovního postupu.

```
<%@ServiceHost Factory=" System.ServiceModel.Activities.Activation.WorkflowServiceHostFactory
Service="EchoService"%>
```
