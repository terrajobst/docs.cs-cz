---
title: 'Postupy: Vytvoření jednosměrného kontraktu'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 85084cd9-31cc-4e95-b667-42ef01336622
ms.openlocfilehash: cc777da65ce1c0d425404b1cc8d47e8189684a7f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62039400"
---
# <a name="how-to-create-a-one-way-contract"></a>Postupy: Vytvoření jednosměrného kontraktu
Toto téma popisuje základní kroky k vytvoření metody, které používají jednosměrného kontraktu. Tyto metody vyvolání operací ve službě Windows Communication Foundation (WCF) od klienta ale Nečekejte odpověď. Tento typ smlouvy lze použít například k publikování oznámení pro mnoho předplatitele. Jednosměrné kontrakty můžete použít také při vytvoření duplexního kontraktu (obousměrné), která umožňuje klientům a serverům komunikovat mezi sebou nezávisle tak, aby buď inicializaci volání do jiné. Můžete to umožní zejména, server pro jednosměrnou volání klienta, který klient může považovat za události. Podrobné informace o zadávání jednosměrné metody, naleznete v tématu <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> vlastnost a <xref:System.ServiceModel.OperationContractAttribute> třídy.  
  
 Další informace o vytváření klientské aplikace pro duplexní kontrakt, naleznete v tématu [jak: Přístup ke službám pomocí jednosměrných kontraktů a kontraktů požadavek odpověď](../../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md). Pracovní ukázku najdete v tématu [jednosměrné](../../../../docs/framework/wcf/samples/one-way.md) vzorku.  
  
### <a name="to-create-a-one-way-contract"></a>K vytvoření jednosměrného kontraktu  
  
1. Vytvoření kontraktu služby s použitím <xref:System.ServiceModel.ServiceContractAttribute> třídy rozhraní, které definuje služba je pro implementaci metody.  
  
2. Označuje, které metody v rozhraní klienta může vyvolávat použití <xref:System.ServiceModel.OperationContractAttribute> třídy k nim.  
  
3. Určení operací, které musí mít žádný výstup (žádnou návratovou hodnotu a žádné na víc systémů nebo parametry předávané odkazem) jako jednosměrná tak, že nastavíte <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> vlastnost `true`. Všimněte si, že operace, která provádění <xref:System.ServiceModel.OperationContractAttribute> třída splňovat kontraktu požadavku a odpovědi ve výchozím nastavení, protože <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> vlastnost `false` ve výchozím nastavení. Proto je nutné explicitně zadat hodnotu atributu vlastnost, která má být `true` Pokud chcete, aby jednosměrného kontraktu metody.  
  
## <a name="example"></a>Příklad  
 Následující příklad kódu definuje kontrakt služby, který zahrnuje několik jednosměrné metody. Všechny metody mají jednosměrné kontrakty s výjimkou `Equals`, která výchozí hodnota je požadavek odpověď a vrátí výsledek.  
  
 [!code-csharp[S_Service_Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
## <a name="see-also"></a>Viz také:

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [Navrhování a implementace služeb](../../../../docs/framework/wcf/designing-and-implementing-services.md)
- [Postupy: Definování kontraktu služby](../../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)
- [Relace](../../../../docs/framework/wcf/samples/session.md)
- [Postupy: Vytvoření duplexního kontraktu](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)
