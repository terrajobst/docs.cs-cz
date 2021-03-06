---
title: Mapování názvů algoritmů na třídy šifrování
ms.date: 03/30/2017
helpviewer_keywords:
- mapping algorithm names
- cryptography, mapping algorithm names
- cryptographic algorithms
- names [.NET Framework], algorithm mapping
ms.assetid: 01327c69-c5e1-4ef6-b73f-0a58351f0492
ms.openlocfilehash: 513000169504473aa6dd46feaca214f58502ffd0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912871"
---
# <a name="mapping-algorithm-names-to-cryptography-classes"></a>Mapování názvů algoritmů na třídy šifrování
Existují čtyři způsoby, jak může vývojář vytvořit objekt kryptografie pomocí Windows SDK:  
  
- Vytvořte objekt pomocí operátoru **New** .  
  
- Vytvořte objekt, který implementuje konkrétní kryptografický algoritmus, voláním metody **Create** pro abstraktní třídu pro daný algoritmus.  
  
- Vytvořte objekt, který implementuje určitý kryptografický algoritmus voláním <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=nameWithType> metody.  
  
- Vytvořte objekt, který implementuje třídu kryptografických algoritmů (například symetrického bloku Block), voláním metody **Create** pro abstraktní třídu pro daný typ algoritmu (například <xref:System.Security.Cryptography.SymmetricAlgorithm>).  
  
 Předpokládejme například, že vývojář chce vypočítat hodnotu hash SHA1 sady bajtů. <xref:System.Security.Cryptography> Obor názvů obsahuje dvě implementace algoritmu SHA1, jednu čistě spravovanou implementaci a jednu, která zabalí rozhraní CryptoAPI. Vývojář se může rozhodnout pro vytvoření instance konkrétní implementace SHA1 (například <xref:System.Security.Cryptography.SHA1Managed>) voláním operátoru **New** . Pokud se však nezáleží na tom, jakou třídu modul CLR (Common Language Runtime) načítá, pokud třída implementuje algoritmus hash SHA1, může vývojář vytvořit objekt voláním <xref:System.Security.Cryptography.SHA1.Create%2A?displayProperty=nameWithType> metody. Tato metoda volá **System. Security. Cryptography. objektu CryptoConfig. CreateFromName ("System. Security. Cryptography. SHA1")** , která musí vracet implementaci algoritmu hash SHA1.  
  
 Vývojář může také volat **System. Security. Cryptography. objektu CryptoConfig. CreateFromName ("SHA1")** , protože ve výchozím nastavení konfigurace kryptografie obsahuje krátké názvy pro algoritmy dodávané v .NET Framework.  
  
 Pokud nezáleží na tom, který algoritmus hash je použit, může vývojář zavolat <xref:System.Security.Cryptography.HashAlgorithm.Create%2A?displayProperty=nameWithType> metodu, která vrátí objekt, který implementuje transformaci hash.  
  
## <a name="mapping-algorithm-names-in-configuration-files"></a>Mapování názvů algoritmů v konfiguračních souborech  
 Ve výchozím nastavení vrátí <xref:System.Security.Cryptography.SHA1CryptoServiceProvider> modul runtime objekt pro všechny čtyři scénáře. Správce počítače však může změnit typ objektu, který metody v posledních dvou scénářích vrátí. K tomu je nutné namapovat popisný název algoritmu na třídu, kterou chcete použít v konfiguračním souboru počítače (Machine. config).  
  
 Následující příklad ukazuje, jak nakonfigurovat modul runtime tak, aby byl **System. Security. Cryptography. SHA1. Create**, **System. Security. objektu CryptoConfig. CREATEFROMNAME ("SHA1")** a **System. Security. Cryptography. HashAlgorithm. Create Vrátí objekt.** `MySHA1HashClass`  
  
```xml  
<configuration>  
   <!-- Other configuration settings. -->  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MySHA1Hash="MySHA1HashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="SHA1" class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.SHA1"  
                       class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.HashAlgorithm"  
                       class="MySHA1Hash"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 Můžete zadat název atributu v [elementu < cryptoClass\> ](./file-schema/cryptography/cryptoclass-element.md) (předchozí příklad název atributu `MySHA1Hash`). Hodnota atributu v  **\<prvku cryptoClass >** je řetězec, který modul CLR (Common Language Runtime) používá k nalezení třídy. Můžete použít libovolný řetězec, který splňuje požadavky zadané v části [určení plně kvalifikovaných názvů typů](../reflection-and-codedom/specifying-fully-qualified-type-names.md).  
  
 Mnoho názvů algoritmů může být mapováno na stejnou třídu. Element nameEntry > mapuje třídu na jeden popisný název algoritmu. [ \<](./file-schema/cryptography/nameentry-element.md) Atribut **Name** může být buď řetězec, který se používá při volání metody **System. Security. Cryptography. objektu CryptoConfig. CreateFromName** nebo názvu abstraktní <xref:System.Security.Cryptography> třídy kryptografie v oboru názvů. Hodnota atributu **Class** je název atributu v  **\<elementu cryptoClass >** .  
  
> [!NOTE]
> Algoritmus SHA1 lze získat voláním <xref:System.Security.Cryptography.SHA1.Create%2A?displayProperty=nameWithType> metody nebo metody **Security. objektu CryptoConfig. CreateFromName ("SHA1")** . Každá metoda zaručuje pouze to, že vrátí objekt, který implementuje algoritmus SHA1. V konfiguračním souboru není nutné namapovat každý popisný název algoritmu na stejnou třídu.  
  
 Seznam výchozích názvů a tříd, na které se mapují, najdete v tématu <xref:System.Security.Cryptography.CryptoConfig>.  
  
## <a name="see-also"></a>Viz také:

- [Kryptografické služby](../../standard/security/cryptographic-services.md)
- [Konfigurace šifrovacích tříd](configure-cryptography-classes.md)
