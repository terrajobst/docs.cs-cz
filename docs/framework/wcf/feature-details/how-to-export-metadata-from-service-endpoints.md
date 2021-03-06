---
title: 'Postupy: Export metadat z koncových bodů služeb'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b6c4dfd0-f270-43ec-961a-e16eb6af2f2c
ms.openlocfilehash: 6bf2eb3d295f9cbf6a7e13a612d5846ceaa75ab4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "61778297"
---
# <a name="how-to-export-metadata-from-service-endpoints"></a>Postupy: Export metadat z koncových bodů služeb
Toto téma vysvětluje, jak pro export metadat z koncových bodů služby.  
  
### <a name="to-export-metadata-from-service-endpoints"></a>Pro export metadat z koncových bodů služby  
  
1. Vytvoření nového projektu aplikace konzoly Visual Studio. Přidejte kód je znázorněno v následujícím postupu v generovaném souboru Program.cs v rámci metody main().  
  
2. Vytvoření <xref:System.ServiceModel.Description.WsdlExporter>.  
  
     [!code-csharp[S_UEWsdlExporter#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#1)]
     [!code-vb[S_UEWsdlExporter#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#1)]  
  
3. Nastavte <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> vlastnost na jednu z hodnot <xref:System.ServiceModel.Description.PolicyVersion> výčtu. Tento příklad nastaví hodnotu <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A> který odpovídá 1.5 WS-Policy.  
  
     [!code-csharp[S_UEWsdlExporter#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#2)]
     [!code-vb[S_UEWsdlExporter#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#2)]  
  
4. Vytvoření pole <xref:System.ServiceModel.Description.ServiceEndpoint> objekty.  
  
     [!code-csharp[S_UEWsdlExporter#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#3)]
     [!code-vb[S_UEWsdlExporter#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#3)]  
  
5. Exportujte metadat pro každého koncového bodu služby.  
  
     [!code-csharp[S_UEWsdlExporter#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#4)]
     [!code-vb[S_UEWsdlExporter#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#4)]  
  
6. Zkontrolujte, ujistěte se, že nedošlo k žádným chybám během procesu exportu a načtení metadat.  
  
     [!code-csharp[S_UEWsdlExporter#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#5)]
     [!code-vb[S_UEWsdlExporter#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#5)]  
  
7. Teď můžete pomocí metadat, jako je zápis do souboru pomocí volání <xref:System.ServiceModel.Description.MetadataSet.WriteTo%28System.Xml.XmlWriter%29> metody.  
  
## <a name="example"></a>Příklad  
 Následuje úplný výpis v tomto příkladu kódu.  
  
 [!code-csharp[S_UEWsdlExporter#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#0)]
 [!code-vb[S_UEWsdlExporter#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#0)]  
  
## <a name="compiling-the-code"></a>Probíhá kompilace kódu  
 Při kompilaci souboru Program.cs odkaz System.ServiceModel.dll.  
  
## <a name="see-also"></a>Viz také:

- [Přehled architektury metadat](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)
- [Používání metadat](../../../../docs/framework/wcf/feature-details/using-metadata.md)
- [Koncové body: Adresy, vazby a kontrakty](../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
