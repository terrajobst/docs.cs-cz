---
title: 'Postupy: Konzistentní odkazy na certifikáty X.509'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- certificates [WCF], referencing X.509 certificates
ms.assetid: a6de1c63-e450-4640-ad08-ad7302dbfbfc
ms.openlocfilehash: 2214517784d311cbd0fe487fd6db2cbf48189955
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662791"
---
# <a name="how-to-consistently-reference-x509-certificates"></a>Postupy: Konzistentní odkazy na certifikáty X.509
Můžete určit certifikát v několika ohledech: hodnota hash certifikátu, vystavitele a sériovým číslem nebo identifikátor klíče subjektu (identifikátor klíče subjektu). Identifikátor klíče subjektu poskytuje jedinečnou identifikaci veřejného klíče subjektu certifikátu a často se používá při práci s XML – digitální podpis. Identifikátor klíče subjektu hodnota je obvykle součástí certifikátu X.509 jako *rozšíření certifikátu X.509*. Windows Communication Foundation (WCF) má výchozí *odkazující na styl* , která používá vystavitele a sériovým číslem, pokud chybí rozšíření identifikátor klíče subjektu z certifikátu. Pokud certifikát obsahuje vlastnost extension identifikátor klíče subjektu, používá výchozí odkazující na styl identifikátor klíče subjektu tak, aby odkazoval na certifikát. Pokud uprostřed způsob prostřednictvím vývoji aplikace přepnou od používání certifikátů, které nepoužívají identifikátor klíče subjektu rozšíření na certifikátech, které používají rozšíření identifikátor klíče subjektu, odkazující styl použitý v zprávy WCF vygenerované také změní.  
  
 Pokud v jednotném stylu odkazující se vyžaduje bez ohledu na přítomnost identifikátor klíče subjektu rozšíření, je možné nakonfigurovat požadované odkazující styl, jak je znázorněno v následujícím kódu.  
  
## <a name="example"></a>Příklad  
 Následující příklad vytvoří vlastní bezpečnostní element vazby, který používá jediný konzistentní odkazující styl, název vystavitele a sériové číslo.  
  
 [!code-csharp[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_referencingcertificatesconsistently/cs/source.cs#1)]
 [!code-vb[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_referencingcertificatesconsistently/vb/source.vb#1)]  
  
## <a name="compiling-the-code"></a>Probíhá kompilace kódu  
 Pro zkompilování kódu se vyžaduje následující obory názvů:  
  
- <xref:System>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.ServiceModel.Channels>  
  
- <xref:System.ServiceModel.Security.Tokens>  
  
## <a name="see-also"></a>Viz také:

- [Práce s certifikáty](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
