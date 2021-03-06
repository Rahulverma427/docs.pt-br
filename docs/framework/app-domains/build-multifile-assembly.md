---
title: Como compilar um assembly de multiarquivos
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- entry point for assembly
- compiling assemblies
- Al.exe
- command-line compilers
- assembly manifest, multifile assemblies
- assemblies [.NET Framework], compiling
- Assembly Linker
- code modules
- multifile assemblies
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 261c5583-8a76-412d-bda7-9b8ee3b131e5
ms.openlocfilehash: 0f8c6d57425657e321d80f9edffa20f27bc28770
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74429562"
---
# <a name="how-to-build-a-multifile-assembly"></a>Como compilar um assembly de multiarquivos

Este artigo explica como criar um assembly de vários arquivos e fornece código que ilustra cada etapa no procedimento.

> [!NOTE]
> O IDE do Visual Studio para C# e Visual Basic pode ser usado apenas para criar assemblies de arquivo único. Se quiser criar assemblies de vários arquivos, você precisará usar os compiladores de linha de comando ou Visual Studio com o Visual C++. Os assemblies de multiarquivo têm suporte apenas pelo .NET Framework.

## <a name="create-a-multifile-assembly"></a>Criar um assembly de multiarquivos

1. Compile todos os arquivos que contêm namespaces referenciados por outros módulos no assembly nos módulos de código. A extensão padrão para módulos de código é *. netmodule*.

   Por exemplo, digamos que o arquivo `Stringer` tem um namespace chamado `myStringer`, que inclui uma classe chamada `Stringer`. A classe `Stringer` contém um método chamado `StringerMethod` que grava uma única linha no console.

   ```cpp
   // Assembly building example in the .NET Framework.
   using namespace System;

   namespace myStringer
   {
       public ref class Stringer
       {
       public:
           void StringerMethod()
           {
               System::Console::WriteLine("This is a line from StringerMethod.");
           }
       };
   }
   ```

   ```csharp
   // Assembly building example in the .NET Framework.
   using System;

   namespace myStringer
   {
       public class Stringer
       {
           public void StringerMethod()
           {
               System.Console.WriteLine("This is a line from StringerMethod.");
           }
       }
   }
   ```

   ```vb
   ' Assembly building example in the .NET Framework.
   Namespace myStringer
       Public Class Stringer
           Public Sub StringerMethod()
               System.Console.WriteLine("This is a line from StringerMethod.")
           End Sub
       End Class
   End Namespace
   ```

2. Use o comando a seguir para compilar esse código:

   ```cpp
   cl /clr:pure /LN Stringer.cpp
   ```

   ```csharp
   csc /t:module Stringer.cs
   ```

   ```vb
   vbc /t:module Stringer.vb
   ```

   Especificar o parâmetro *module* com a opção do compilador **/t:** indica que o arquivo deve ser compilado como um módulo em vez de como um assembly. O compilador produz um módulo chamado *Stringer. netmodule*, que pode ser adicionado a um assembly.

3. Compile todos os outros módulos, usando as opções do compilador necessárias para indicar os outros módulos que são referenciados no código. Esta etapa usa a opção do compilador **/addmodule**.

   No exemplo a seguir, um módulo de código chamado *cliente* tem um ponto de entrada `Main` método que faz referência a um método no módulo *Stringer. dll* criado na etapa 1.

   ```cpp
   #using "Stringer.netmodule"

   using namespace System;
   using namespace myStringer; //The namespace created in Stringer.netmodule.

   ref class MainClientApp
   {
       // Static method Main is the entry point method.
   public:
       static void Main()
       {
           Stringer^ myStringInstance = gcnew Stringer();
           Console::WriteLine("Client code executes");
           myStringInstance->StringerMethod();
       }
   };

   int main()
   {
       MainClientApp::Main();
   }
   ```

   ```csharp
   using System;
   using myStringer;

   class MainClientApp
   {
       // Static method Main is the entry point method.
       public static void Main()
       {
           Stringer myStringInstance = new Stringer();
           Console.WriteLine("Client code executes");
           myStringInstance.StringerMethod();
       }
   }
   ```

   ```vb
   Imports myStringer

   Class MainClientApp
       ' Static method Main is the entry point method.
       Public Shared Sub Main()
           Dim myStringInstance As New Stringer()
           Console.WriteLine("Client code executes")
           myStringInstance.StringerMethod()
       End Sub
   End Class
   ```

4. Use o comando a seguir para compilar esse código:

   ```cpp
   cl /clr:pure /FUStringer.netmodule /LN Client.cpp
   ```

   ```csharp
   csc /addmodule:Stringer.netmodule /t:module Client.cs
   ```

   ```vb
   vbc /addmodule:Stringer.netmodule /t:module Client.vb
   ```

   Especifique a opção **/t:module** porque este módulo será adicionado a um assembly em uma etapa futura. Especifique a opção **/addmodule** porque o código no *cliente* faz referência a um namespace criado pelo código em *Stringer. netmodule*. O compilador produz um módulo chamado *Client. netmodule* que contém uma referência a outro módulo, *Stringer. netmodule*.

   > [!NOTE]
   > Os compiladores C# e Visual Basic dão suporte à criação de assemblies de vários arquivos diretamente usando as duas sintaxes diferentes a seguir.
   >
   > Duas compilações criam um assembly de dois arquivos:
   >
   >   ```cpp
   >   cl /clr:pure /LN Stringer.cpp
   >   cl /clr:pure Client.cpp /link /ASSEMBLYMODULE:Stringer.netmodule
   >   ```
   >
   >   ```csharp
   >   csc /t:module Stringer.cs
   >   csc Client.cs /addmodule:Stringer.netmodule
   >   ```
   >
   >   ```vb
   >   vbc /t:module Stringer.vb
   >   vbc Client.vb /addmodule:Stringer.netmodule
   >   ```
   >
   > Uma compilação cria um assembly de dois arquivos:
   >
   >   ```cpp
   >   cl /clr:pure /LN Stringer.cpp
   >   cl /clr:pure Client.cpp /link /ASSEMBLYMODULE:Stringer.netmodule
   >   ```
   >
   >   ```csharp
   >   csc /out:Client.exe Client.cs /out:Stringer.netmodule Stringer.cs
   >   ```
   >
   >   ```vb
   >   vbc /out:Client.exe Client.vb /out:Stringer.netmodule Stringer.vb
   >   ```

5. Use o [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md) para criar o arquivo de saída que contém o manifesto do assembly. Esse arquivo contém informações de referência para todos os módulos ou recursos que fazem parte do assembly.

    No prompt de comando, digite o seguinte comando:

    **al** \<*nome do módulo*> \<*nome do módulo*> … **/main:** \<*nome do método*>  **/out:** \<*nome de arquivo*>  **/target:** \<*tipo de arquivo do assembly*>

    Neste comando, os argumentos *nome do módulo* especificam o nome de cada módulo a ser incluído no assembly. A opção **/main:** especifica o nome do método que é o ponto de entrada do assembly. A opção **/out:** especifica o nome do arquivo de saída, que contém metadados do assembly. A opção **/target:** especifica que o assembly é um arquivo executável do aplicativo de console ( *. exe*), um arquivo executável do Windows ( *. Win*) ou um arquivo de biblioteca ( *. lib*).

    No exemplo a seguir, *al. exe* cria um assembly que é um executável de aplicativo de console chamado *myAssembly. exe*. O aplicativo consiste em dois módulos chamados *Client. netmodule* e *Stringer. netmodule*, e o arquivo executável chamado *myAssembly. exe*, que contém apenas metadados do assembly. O ponto de entrada do assembly é o método `Main` na classe `MainClientApp`, que está localizada em *Client. dll*.

    ```cmd
    al Client.netmodule Stringer.netmodule /main:MainClientApp.Main /out:myAssembly.exe /target:exe
    ```

    Você pode usar o [MSIL Disassembler (Ildasm.exe)](../tools/ildasm-exe-il-disassembler.md) para examinar o conteúdo de um assembly ou determinar se um arquivo é um assembly ou um módulo.

## <a name="see-also"></a>Consulte também

- [Criar assemblies](../../standard/assembly/create.md)
- [Como exibir o conteúdo do assembly](../../standard/assembly/view-contents.md)
- [Como o runtime localiza assemblies](../deployment/how-the-runtime-locates-assemblies.md)
- [Assemblies de multiarquivo](multifile-assemblies.md)
