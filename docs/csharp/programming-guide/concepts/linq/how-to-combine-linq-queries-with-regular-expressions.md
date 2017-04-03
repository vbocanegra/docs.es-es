---
title: "Cómo: Combinar consultas LINQ con expresiones regulares (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 6b003b65-20a4-4ca2-929e-2ee3f215aecc
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 51cce0d7ffd4806365600ee93d57806af96f08a8
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-combine-linq-queries-with-regular-expressions-c"></a>Cómo: Combinar consultas LINQ con expresiones regulares (C#)
En este ejemplo se muestra cómo usar la clase <xref:System.Text.RegularExpressions.Regex> para crear una expresión regular para coincidencias más complejas en cadenas de texto. Con la consulta LINQ, resulta fácil filtrar por los archivos exactos que se quieren buscar con la expresión regular y dar forma a los resultados.  
  
## <a name="example"></a>Ejemplo  
  
```csharp  
class QueryWithRegEx  
{  
    public static void Main()  
    {  
        // Modify this path as necessary so that it accesses your version of Visual Studio.  
        string startFolder = @"c:\program files\Microsoft Visual Studio 9.0\";  
        // One of the following paths may be more appropriate on your computer.  
        //string startFolder = @"c:\program files (x86)\Microsoft Visual Studio 9.0\";  
        //string startFolder = @"c:\program files\Microsoft Visual Studio 10.0\";  
        //string startFolder = @"c:\program files (x86)\Microsoft Visual Studio 10.0\";  
  
        // Take a snapshot of the file system.  
        IEnumerable<System.IO.FileInfo> fileList = GetFiles(startFolder);  
  
        // Create the regular expression to find all things "Visual".  
        System.Text.RegularExpressions.Regex searchTerm =  
            new System.Text.RegularExpressions.Regex(@"Visual (Basic|C#|C\+\+|J#|SourceSafe|Studio)");  
  
        // Search the contents of each .htm file.  
        // Remove the where clause to find even more matchedValues!  
        // This query produces a list of files where a match  
        // was found, and a list of the matchedValues in that file.  
        // Note: Explicit typing of "Match" in select clause.  
        // This is required because MatchCollection is not a   
        // generic IEnumerable collection.  
        var queryMatchingFiles =  
            from file in fileList  
            where file.Extension == ".htm"  
            let fileText = System.IO.File.ReadAllText(file.FullName)  
            let matches = searchTerm.Matches(fileText)  
            where matches.Count > 0  
            select new  
            {  
                name = file.FullName,  
                matchedValues = from System.Text.RegularExpressions.Match match in matches  
                                select match.Value  
            };  
  
        // Execute the query.  
        Console.WriteLine("The term \"{0}\" was found in:", searchTerm.ToString());  
  
        foreach (var v in queryMatchingFiles)  
        {  
            // Trim the path a bit, then write   
            // the file name in which a match was found.  
            string s = v.name.Substring(startFolder.Length - 1);  
            Console.WriteLine(s);  
  
            // For this file, write out all the matching strings  
            foreach (var v2 in v.matchedValues)  
            {  
                Console.WriteLine("  " + v2);  
            }  
        }  
  
        // Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
  
    // This method assumes that the application has discovery   
    // permissions for all folders under the specified path.  
    static IEnumerable<System.IO.FileInfo> GetFiles(string path)  
    {  
        if (!System.IO.Directory.Exists(path))  
            throw new System.IO.DirectoryNotFoundException();  
  
        string[] fileNames = null;  
        List<System.IO.FileInfo> files = new List<System.IO.FileInfo>();  
  
        fileNames = System.IO.Directory.GetFiles(path, "*.*", System.IO.SearchOption.AllDirectories);  
        foreach (string name in fileNames)  
        {  
            files.Add(new System.IO.FileInfo(name));  
        }  
        return files;  
    }  
}  
```  
  
 Tenga en cuenta que también se puede consultar el objeto <xref:System.Text.RegularExpressions.MatchCollection> devuelto por una búsqueda de `RegEx`. En este ejemplo se genera solo el valor de cada coincidencia en los resultados. Pero también es posible usar LINQ para realizar todo tipo de filtrado, ordenación y agrupación en esa colección. Dado que <xref:System.Text.RegularExpressions.MatchCollection> es una colección <xref:System.Collections.IEnumerable> no genérica, tiene que indicar explícitamente el tipo de la variable de rango en la consulta.  
  
## <a name="compiling-the-code"></a>Compilar el código  
 Cree un proyecto destinado a .NET Framework versión 3.5 o posterior, con una referencia a System.Core.dll y directivas `using` para los espacios de nombres System.Linq y System.IO.  
  
## <a name="see-also"></a>Vea también  
 [LINQ y cadenas (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)   
 [LINQ y directorios de archivos (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-file-directories.md)