---
title: Zajištění integrity dat pomocí hodnot hash
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generating hash
- verifying hash codes
- cryptography [.NET Framework], hash
- data integrity
- checking hash codes
- encryption [.NET Framework], hash
- hash
ms.assetid: 33660f33-b70f-4dca-8c87-ab35cfc2961a
ms.openlocfilehash: 98bdce59ccbbb3b1d00ea5521169214c2bd7a10b
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75706198"
---
# <a name="ensuring-data-integrity-with-hash-codes"></a>Zajištění integrity dat pomocí hodnot hash
Hodnota hash je číselná hodnota s pevnou délkou, která jednoznačně identifikuje data. Hodnoty hash představují velké objemy dat s mnohem menšími číselnými hodnotami, takže se používají s digitálními podpisy. Hodnotu hash můžete efektivně podepsat, než je třeba podepsat větší hodnotu. Hodnoty hash jsou také užitečné pro ověření integrity dat odesílaných prostřednictvím nezabezpečených kanálů. Hodnota hash přijatých dat se dá porovnat s hodnotou hash dat, protože byla odeslána, aby se zjistilo, jestli se data změnila.  
  
 Toto téma popisuje, jak generovat a ověřit kódy hash pomocí tříd v oboru názvů <xref:System.Security.Cryptography?displayProperty=nameWithType>.  
  
## <a name="generating-a-hash"></a>Generování hodnoty hash  
 Spravované třídy hash mohou vytvořit hodnotu hash pole bajtů nebo objektu spravovaného datového proudu. Následující příklad používá algoritmus hash SHA1 k vytvoření hodnoty hash pro řetězec. V příkladu se používá třída <xref:System.Text.UnicodeEncoding> pro převod řetězce na pole bajtů, které jsou hashy pomocí <xref:System.Security.Cryptography.SHA1Managed> třídy. Hodnota hash se pak zobrazí v konzole nástroje.  

 Microsoft doporučuje SHA256 nebo lepší kvůli kolizi problémů se SHA1.
  
 [!code-csharp[GeneratingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/generatingahash/cs/program.cs#1)]
 [!code-vb[GeneratingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/generatingahash/vb/program.vb#1)]  
  
 Tento kód zobrazí následující řetězec pro konzolu:  
  
 `59 4 248 102 77 97 142 201 210 12 224 93 25 41 100 197 213 134 130 135`  
  
## <a name="verifying-a-hash"></a>Ověření hodnoty hash  
 Data je možné porovnat s hodnotou hash k určení její integrity. Data jsou obvykle Hashovaná v určitou dobu a hodnota hash je chráněna nějakým způsobem. Později můžete data znovu hash a porovnat s chráněnou hodnotou. Pokud se hodnoty hash shodují, data se nezmění. Pokud se hodnoty neshodují, data jsou poškozena. Aby tento systém fungoval, musí být chráněný algoritmus hash zašifrovaný nebo musí uchovávat tajné klíče ze všech nedůvěryhodných stran.  
  
 Následující příklad porovnává předchozí hodnotu hash řetězce s novou hodnotou hash. Tento příklad projde každým bajtem hodnot hash a provede porovnání.  
  
 [!code-csharp[VerifyingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/verifyingahash/cs/program.cs#1)]
 [!code-vb[VerifyingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/verifyingahash/vb/program.vb#1)]  
  
 Pokud se dvě hodnoty hash shodují, tento kód zobrazí následující kód konzole:  
  
```console  
The hash codes match.  
```  
  
 Pokud se neshodují, kód zobrazí následující:  
  
```console  
The hash codes do not match.  
```  
  
## <a name="see-also"></a>Viz také:

- [Kryptografické služby](../../../docs/standard/security/cryptographic-services.md)
