---
title: Bloky skriptu používající element msxsl:script
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: fde6f43f-c594-486f-abcb-2211197fae20
ms.openlocfilehash: a63452df16e452a90eff3977ac8726cc0a5ac439
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75710190"
---
# <a name="script-blocks-using-msxslscript"></a>Bloky skriptu používající element msxsl:script
Třída <xref:System.Xml.Xsl.XslCompiledTransform> podporuje vložené skripty pomocí elementu `msxsl:script`. Při načtení předlohy se styly jsou všechny definované funkce kompilovány do jazyka MSIL (Microsoft Intermediate Language) pomocí Code Document Object Model (CodeDOM) a jsou prováděny během doby běhu. Sestavení vygenerované z vloženého bloku skriptu je oddělené od sestavení generovaného pro šablonu stylů.  
  
## <a name="enable-xslt-script"></a>Povolit skript XSLT  
 Podpora pro vložené skripty je volitelné nastavení XSLT u <xref:System.Xml.Xsl.XslCompiledTransform> třídy. Podpora skriptů je ve výchozím nastavení zakázaná. Chcete-li povolit podporu skriptů, vytvořte objekt <xref:System.Xml.Xsl.XsltSettings> s vlastností <xref:System.Xml.Xsl.XsltSettings.EnableScript%2A> nastavenou na hodnotu `true` a předejte objekt metodě <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A>.  
  
> [!NOTE]
> Skriptování XSLT by mělo být povoleno pouze v případě, že potřebujete podporu skriptů a pracujete v plně důvěryhodném prostředí.  
  
## <a name="msxslscript-element-definition"></a>msxsl: definice elementu skriptu  
 `msxsl:script` element je rozšířením společnosti Microsoft k doporučení XSLT 1,0 a má následující definici:  
  
```xml  
<msxsl:script language = "language-name" implements-prefix = "prefix of user namespace"> </msxsl:script>  
```  
  
 Předpona `msxsl` je svázána s identifikátorem URI oboru názvů `urn:schemas-microsoft-com:xslt`. Šablona stylů musí zahrnovat `xmlns:msxsl=urn:schemas-microsoft-com:xslt` deklaraci oboru názvů.  
  
 Atribut `language` je nepovinný. Jeho hodnota je jazyk kódu vloženého bloku kódu. Jazyk je namapován na příslušný kompilátor CodeDOM pomocí metody <xref:System.CodeDom.Compiler.CodeDomProvider.CreateProvider%2A?displayProperty=nameWithType>. Třída <xref:System.Xml.Xsl.XslCompiledTransform> může podporovat libovolný jazyk platformy Microsoft .NET. za předpokladu, že příslušný zprostředkovatel je nainstalován v počítači a je zaregistrován v oddílu System. CodeDom souboru Machine. config. Pokud není zadán atribut `language`, výchozí jazyk je JScript. V názvu jazyka se nerozlišují velká a malá písmena, takže jazyky JavaScript a JavaScript jsou ekvivalentní.  
  
 Atribut `implements-prefix` je povinný. Tento atribut slouží k deklaraci oboru názvů a k jeho přidružení ke bloku skriptu. Hodnota tohoto atributu je předpona, která představuje obor názvů. Tuto předponu lze definovat někde v šabloně stylů.  
  
> [!NOTE]
> Při použití prvku `msxsl:script` důrazně doporučujeme, aby byl skript bez ohledu na jazyk umístěn uvnitř oddílu CDATA. Vzhledem k tomu, že skript může obsahovat operátory, identifikátory nebo oddělovače pro daný jazyk, pokud není obsažen v oddílu CDATA, má potenciál, který je špatně interpretován jako XML. Následující kód XML ukazuje šablonu oddílu CDATA, kde lze umístit kód.  
  
```xml  
<msxsl:script implements-prefix='your-prefix' language='CSharp'>  
<![CDATA[  
// Code block.  
]]>  
</msxsl:script>  
```  
  
## <a name="script-functions"></a>Funkce skriptu  
 Funkce mohou být deklarovány v rámci `msxsl:script` elementu. Je-li funkce deklarována, je obsažena v bloku skriptu. Šablony stylů mohou obsahovat více bloků skriptu, z nichž každý pracuje nezávisle na sobě. To znamená, že pokud provádíte uvnitř bloku skriptu, nemůžete volat funkci, která je definována v jiném bloku skriptu, pokud není deklarována tak, aby měla stejný obor názvů a stejný skriptovací jazyk. Vzhledem k tomu, že každý blok skriptu může být ve vlastním jazyce a blok je analyzován podle gramatických pravidel daného jazykového analyzátoru, doporučujeme použít správnou syntaxi používaného jazyka. Například pokud jste v bloku Microsoft C# Script Block, použijte syntaxi C# komentářů.  
  
 Zadané argumenty a návratové hodnoty funkce mohou být libovolného typu. Vzhledem k tomu, že typy XPath W3C jsou podmnožinou typů modulu CLR (Common Language Runtime), převod typu probíhá u typů, které nejsou považovány za typ XPath. V následující tabulce jsou uvedeny odpovídající typy W3C a ekvivalentní typ CLR.  
  
|Typ W3C|Typ CLR|  
|--------------|--------------|  
|`String`|<xref:System.String>|  
|`Boolean`|<xref:System.Boolean>|  
|`Number`|<xref:System.Double>|  
|`Result Tree Fragment`|<xref:System.Xml.XPath.XPathNavigator>|  
|`Node Set`|<xref:System.Xml.XPath.XPathNodeIterator>|  
  
 Číselné typy CLR jsou převedeny na <xref:System.Double>. Typ <xref:System.DateTime> je převeden na <xref:System.String>. <xref:System.Xml.XPath.IXPathNavigable> typy jsou převedeny na <xref:System.Xml.XPath.XPathNavigator>. **Prvek XPathNavigator []** je převeden na <xref:System.Xml.XPath.XPathNodeIterator>.  
  
 Všechny ostatní typy vyvolávají chybu.  
  
### <a name="importing-namespaces-and-assemblies"></a>Import oborů názvů a sestavení  
 Třída <xref:System.Xml.Xsl.XslCompiledTransform> předdefinuje sadu sestavení a oborů názvů, které jsou ve výchozím nastavení podporovány prvkem `msxsl:script`. Můžete však použít třídy a členy patřící do oboru názvů, který není v předdefinovaném seznamu, importováním sestavení a oboru názvů do bloku `msxsl:script`.  
  
#### <a name="assemblies"></a>Sestavení  
 Ve výchozím nastavení je odkazováno na následující dvě sestavení:  
  
- System.dll  
  
- System.Xml.dll  
  
- Microsoft. VisualBasic. dll (Pokud je jazyk skriptu VB)  
  
 Další sestavení lze importovat pomocí elementu `msxsl:assembly`. To zahrnuje sestavení při kompilování předlohy se styly. Element `msxsl:assembly` má následující definici:  
  
```xml  
<msxsl:script>  
  <msxsl:assembly name="system.assemblyName" />  
  <msxsl:assembly href="path-name" />  
    <![CDATA[  
    // User code  
    ]]>  
</msxsl:script>  
```  
  
 Atribut `name` obsahuje název sestavení a atribut `href` obsahuje cestu k sestavení. Název sestavení může být úplný název, například "System. data, Version = 2.0.3600.0, Culture = neutral, PublicKeyToken = b77a5c561934e089" nebo krátký název, například "System. Web".  
  
#### <a name="namespaces"></a>Jmenné prostory  
 Ve výchozím nastavení jsou zahrnuty následující obory názvů:  
  
- Systém  
  
- System.Collection  
  
- System.Text  
  
- System.Text.RegularExpressions  
  
- System.Xml  
  
- System.Xml.Xsl  
  
- System.Xml.XPath  
  
- Microsoft. VisualBasic (Pokud je skriptovací jazyk VB)  
  
 Podporu pro další obory názvů můžete přidat pomocí atributu `namespace`. Hodnota atributu je název oboru názvů.  
  
```xml  
<msxsl:script>  
  <msxsl:using namespace="system.namespaceName" />  
    <![CDATA[  
    // User code  
    ]]>  
</msxsl:script>  
```  
  
## <a name="example"></a>Příklad  
 V následujícím příkladu je použit vložený skript k výpočtu obvodu kružnice s daným poloměrem.  
  
 [!code-csharp[XSLT_Script#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_Script/CS/xslt_script.cs#1)]
 [!code-vb[XSLT_Script#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_Script/VB/xslt_script.vb#1)]  
  
#### <a name="numberxml"></a>Number. XML  
 [!code-xml[XSLT_Script#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Script/XML/number.xml#2)]  
  
#### <a name="calcxsl"></a>calc.xsl  
 [!code-xml[XSLT_Script#3](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Script/XML/calc.xsl#3)]  
  
### <a name="output"></a>Výstup  
  
```xml  
<circles xmlns:msxsl="urn:schemas-microsoft-com:xslt" xmlns:user="urn:my-scripts">  
  <circle>  
    <radius>12</radius>  
    <circumference>75.36</circumference>  
  </circle>  
  <circle>  
    <radius>37.5</radius>  
    <circumference>235.5</circumference>  
  </circle>  
</circles>  
```  
  
## <a name="see-also"></a>Viz také:

- [Transformace XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)
- [Dynamické vytváření a kompilování zdrojového kódu](../../../../docs/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation.md)
