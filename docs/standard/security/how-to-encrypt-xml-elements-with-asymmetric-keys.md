---
title: "How to: Encrypt XML Elements with Asymmetric Keys | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "cryptography [.NET Framework], asymmetric keys"
  - "AES algorithm"
  - "System.Security.Cryptography.RSACryptoServiceProvider class"
  - "asymmetric keys [.NET Framework]"
  - "System.Security.Cryptography.EncryptedXml class"
  - "XML encryption"
  - "key containers"
  - "Advanced Encryption Standard algorithm"
  - "Rijndael"
  - "encryption [.NET Framework], asymmetric keys"
ms.assetid: a164ba4f-e596-4bbe-a9ca-f214fe89ed48
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Encrypt XML Elements with Asymmetric Keys
Puede usar las clases en el espacio de nombres <xref:System.Security.Cryptography.Xml> para cifrar un elemento dentro de un documento XML.  El cifrado XML es un método estándar para intercambiar o almacenar datos XML cifrados sin preocuparse de que los datos puedan leerse con facilidad.  Para obtener más información sobre el estándar de cifrado XML, consulte la especificación de World Wide Web Consortium \(W3C\) del cifrado XML en http:\/\/www.w3.org\/TR\/xmldsig\-core\/.  
  
 Puede usar el cifrado de XML para reemplazar cualquier elemento o documento XML con un elemento \<`EncryptedData`\> que contenga los datos XML cifrados.  El elemento \<`EncryptedData`\> también puede contener subelementos con información sobre las claves y los procesos usados durante el cifrado.  El cifrado XML permite que un documento contenga varios elementos cifrados y permite cifrar varias veces un elemento.  En el ejemplo de código de este procedimiento se muestra cómo crear un elemento \<`EncryptedData`\> junto con otros subelementos que se pueden usar durante el posterior descifrado.  
  
 En este ejemplo se cifra un elemento XML mediante dos claves.  Genera un par de claves públicas\/privadas RSA y lo guarda en un contenedor de claves seguras.  Después, el ejemplo crea una clave de sesión independiente mediante el algoritmo AES \(Estándar de cifrado avanzado\), también llamado algoritmo de Rijndael.  El ejemplo usa la clave de sesión AES para cifrar el documento XML y usa la clave pública RSA para cifrar la clave de sesión AES.  Por último, el ejemplo guarda la clave de sesión AES cifrada y los datos XML cifrados en el documento XML dentro de un nuevo elemento \<`EncryptedData`\>.  
  
 Para descifrar el elemento XML, recupere la clave privada RSA del contenedor de claves, úsela para descifrar la clave de sesión y, posteriormente, descifrar el documento.  Para obtener más información sobre la manera de descifrar un elemento XML cifrado mediante este procedimiento, consulte [How to: Decrypt XML Elements with Asymmetric Keys](../../../docs/standard/security/how-to-decrypt-xml-elements-with-asymmetric-keys.md).  
  
 Este ejemplo resulta adecuado en aquellas situaciones en las que varias aplicaciones tienen que compartir datos cifrados o en las que una aplicación tiene que guardar datos cifrados entre los intervalos en los que se ejecuta.  
  
### Para cifrar un elemento XML con una clave asimétrica  
  
1.  Cree un objeto <xref:System.Security.Cryptography.CspParameters> y especifique el nombre del contenedor de claves.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#2)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#2)]  
  
2.  Genere una clave simétrica mediante la clase <xref:System.Security.Cryptography.RSACryptoServiceProvider>.  La clave se guarda automáticamente en el contenedor de claves al pasar el objeto <xref:System.Security.Cryptography.CspParameters> al constructor de la clase <xref:System.Security.Cryptography.RSACryptoServiceProvider>.  Esta clave se usará para cifrar la clave de sesión AES y se puede recuperar más adelante para descifrarla.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#3)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#3)]  
  
3.  Cree un objeto <xref:System.Xml.XmlDocument> cargando un archivo XML del disco.  El objeto <xref:System.Xml.XmlDocument> contiene el elemento XML que se va a cifrar.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#4)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#4)]  
  
4.  Busque el elemento especificado en el objeto <xref:System.Xml.XmlDocument> y cree un objeto <xref:System.Xml.XmlElement> nuevo para representar el elemento que desea cifrar.  En este ejemplo, el elemento `"creditcard"` está cifrado.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#5)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#5)]  
  
5.  Cree una nueva sesión de clave mediante la clase <xref:System.Security.Cryptography.RijndaelManaged>.  Esta clave cifrará el elemento XML, se cifrará ella misma y se colocará en el documento XML.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#6)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#6)]  
  
6.  Cree una nueva instancia de la clase <xref:System.Security.Cryptography.Xml.EncryptedXml> y úsela para cifrar el elemento especificado mediante la clave de sesión.  El método <xref:System.Security.Cryptography.Xml.EncryptedXml.EncryptData%2A> devuelve el elemento cifrado como una matriz de bytes cifrados.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#7)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#7)]  
  
7.  Construya un objeto <xref:System.Security.Cryptography.Xml.EncryptedData> y rellénelo con el identificador de dirección URL del elemento XML cifrado.  Este identificador de dirección URL permite que una entidad descifradora sepa que el código XML contiene un elemento cifrado.  Puede usar el campo <xref:System.Security.Cryptography.Xml.EncryptedXml.XmlEncElementUrl> para especificar el identificador de dirección URL.  El elemento XML de texto simple se reemplazará por un elemento \<`EncryptedData`\> encapsulado por este objeto <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#8)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#8)]  
  
8.  Cree un objeto <xref:System.Security.Cryptography.Xml.EncryptionMethod> inicializado en el identificador de dirección URL del algoritmo criptográfico usado para generar la clave de sesión.  Pase el objeto <xref:System.Security.Cryptography.Xml.EncryptionMethod> a la propiedad <xref:System.Security.Cryptography.Xml.EncryptedType.EncryptionMethod%2A>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#9)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#9)]  
  
9. Cree un objeto <xref:System.Security.Cryptography.Xml.EncryptedKey> para incluir la clave de sesión cifrada.  Cifre la clave de sesión, agréguela al objeto <xref:System.Security.Cryptography.Xml.EncryptedKey> y escriba un nombre de clave de sesión y una dirección URL de identificador de clave.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#10)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#10)]  
  
10. Cree un nuevo objeto <xref:System.Security.Cryptography.Xml.DataReference> que asigne los datos cifrados a una clave de sesión determinada.  Este paso opcional le permite especificar fácilmente que una clave única cifró varias partes de un documento XML.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#11)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#11)]  
  
11. Agregue la clave cifrada al objeto <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#12)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#12)]  
  
12. Cree un nuevo objeto <xref:System.Security.Cryptography.Xml.KeyInfo> para especificar el nombre de la clave RSA.  Agréguelo al objeto <xref:System.Security.Cryptography.Xml.EncryptedData>.  Así, la entidad descifradora podrá identificar la clave asimétrica que debe usar al descifrar la clave de sesión.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#13)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#13)]  
  
13. Agregue los datos de elementos cifrados al objeto <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#14)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#14)]  
  
14. Reemplace el elemento del objeto <xref:System.Xml.XmlDocument> original por el elemento <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#15)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#15)]  
  
15. Guarde el objeto <xref:System.Xml.XmlDocument>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#16)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#16)]  
  
## Ejemplo  
 En este ejemplo se supone que un archivo llamado `"test.xml"` se encuentra en el mismo directorio que el programa compilado.  También se supone que `"test.xml"` contiene un elemento `"creditcard"`.  Puede colocar el siguiente código XML en un archivo llamado `test.xml` y usarlo con este ejemplo.  
  
```  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
  
```  
  
 [!code-csharp[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#1)]
 [!code-vb[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#1)]  
  
## Compilar el código  
  
-   Para compilar este ejemplo, debe incluir una referencia a `System.Security.dll`.  
  
-   Incluya los siguientes espacios de nombres: <xref:System.Xml>, <xref:System.Security.Cryptography> y <xref:System.Security.Cryptography.Xml>.  
  
## Seguridad de .NET Framework  
 No almacene nunca una clave criptográfica simétrica en texto sin formato ni transfiera una clave simétrica entre equipos en texto sin formato.  Tampoco debe almacenar ni transferir nunca la clave privada de un par de claves asimétricas en texto sin formato.  Para obtener más información acerca de las claves criptográficas simétricas y asimétricas, consulte [Generating Keys for Encryption and Decryption](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md).  
  
 No inserte nunca una clave directamente en el código fuente.  Las claves insertadas se pueden leer fácilmente desde un ensamblado con el [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) o abriendo el ensamblado en un editor de texto, como el Bloc de notas.  
  
 Cuando termine de usar una clave criptográfica, bórrela de la memoria estableciendo cada byte en cero o llamando al método <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> de la clase criptográfica administrada.  A veces, las claves criptográficas se pueden leer desde la memoria con un depurador o desde un disco duro si la ubicación de memoria se pagina en el disco.  
  
## Vea también  
 <xref:System.Security.Cryptography.Xml>   
 [How to: Decrypt XML Elements with Asymmetric Keys](../../../docs/standard/security/how-to-decrypt-xml-elements-with-asymmetric-keys.md)