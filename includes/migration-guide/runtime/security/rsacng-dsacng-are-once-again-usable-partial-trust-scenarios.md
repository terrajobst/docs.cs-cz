---
ms.openlocfilehash: 8b41e3234c00059ecb5088bbf2597611d7f139b8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2020
ms.locfileid: "67857246"
---
### <a name="rsacng-and-dsacng-are-once-again-usable-in-partial-trust-scenarios"></a>RSACng a DSACng jsou opět použitelné ve scénářích částečné důvěryhodnosti

|   |   |
|---|---|
|Podrobnosti|CngLightup (používá se v několika kryptografických apis vyšší úrovně, například <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=nameWithType>) a <xref:System.Security.Cryptography.RSACng?displayProperty=nameWithType> v některých případech se spoléhá na plnou důvěryhodnost. Patří mezi ně P/Invokes bez uplatnění <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode?displayProperty=nameWithType> oprávnění <xref:System.Security.Cryptography.CngKey?displayProperty=nameWithType> a cesty <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode?displayProperty=nameWithType>kódu, kde má požadavky na oprávnění pro . Počínaje rozhraním .NET Framework 4.6.2 byl CngLightup použit k přepnutí, kdykoli <xref:System.Security.Cryptography.RSACng?displayProperty=nameWithType> je to možné. V důsledku toho částečné důvěryhodnosti <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=nameWithType> aplikace, které <xref:System.Security.SecurityException> úspěšně používané začaly selhat a vyvolat výjimky. Tato změna přidá požadované nepodmíněných výrazů tak, aby všechny funkce používající CngLightup mít požadovaná oprávnění.|
|Návrh|Pokud tato změna v rozhraní .NET Framework 4.6.2 negativně ovlivnila vaše aplikace pro částečnou důvěryhodnost, upgradujte na rozhraní .NET Framework 4.7.1.|
|Rozsah|Edge|
|Version|4.6.2|
|Typ|Modul runtime|
|Ovlivněná rozhraní API|<ul><li><xref:System.Security.Cryptography.DSACng.%23ctor(System.Security.Cryptography.CngKey)?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.DSACng.Key?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.DSACng.LegalKeySizes?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.DSACng.CreateSignature(System.Byte[])?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.DSACng.VerifySignature(System.Byte[],System.Byte[])?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RSACng.%23ctor(System.Security.Cryptography.CngKey)?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RSACng.Key?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RSACng.Decrypt(System.Byte[],System.Security.Cryptography.RSAEncryptionPadding)?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RSACng.SignHash(System.Byte[],System.Security.Cryptography.HashAlgorithmName,System.Security.Cryptography.RSASignaturePadding)?displayProperty=nameWithType></li></ul>|
