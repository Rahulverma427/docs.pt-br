---
title: Ativar o recurso auto-completar com TAB
description: Este artigo ensina você a habilitar o preenchimento com TAB na CLI do .NET Core para o PowerShell, o Bash e o zsh.
author: thraka
ms.author: adegeo
ms.date: 11/03/2019
ms.openlocfilehash: 31328be14811760bc8d7fb527e0d55abfe6b1493
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/14/2020
ms.locfileid: "78156745"
---
# <a name="how-to-enable-tab-completion-for-the-net-core-cli"></a>Como habilitar o preenchimento com TAB na CLI do .NET Core

**Este artigo se aplica a:** ✔️ .NET Core 2.1 SDK e versões posteriores

Este artigo descreve como configurar o preenchimento com TAB para três shells: PowerShell, Bash e zsh. Para outros shells, consulte sua documentação sobre como configurar a conclusão da guia.

Uma vez configurado, a conclusão da guia para `dotnet` o .NET Core CLI é acionada digitando um comando no shell e, em seguida, pressionando a tecla TAB. A linha de comando atual é enviada para o comando `dotnet complete`, e os resultados são processados pelo shell. Teste os resultados sem habilitar o preenchimento com TAB enviando algo diretamente para o comando `dotnet complete`. Por exemplo: 

```console
> dotnet complete "dotnet a"
add
clean
--diagnostics
migrate
pack
```

Se esse comando não funcionar, verifique se esse SDK do .NET Core 2.0 ou superior está instalado. Se ele está instalado, mas esse comando ainda não funciona, verifique se o comando `dotnet` é resolvido para uma versão do SDK do .NET Core 2.0 e superior. Use o comando `dotnet --version` para ver para qual versão do `dotnet` o caminho atual está sendo resolvido. Para obter mais informações, confira [Selecionar a versão do .NET Core a ser usada](../versions/selection.md).

### <a name="examples"></a>Exemplos

Estes são alguns exemplos do que o preenchimento com TAB fornece:

Entrada                                | se torna                                                                     | porque
:------------------------------------|:----------------------------------------------------------------------------|:--------------------------------
`dotnet a⇥`                          | `dotnet add`                                                                 | `add` é o primeiro subcomando, em ordem alfabética.
`dotnet add p⇥`                      | `dotnet add --help`                                                          | O preenchimento com TAB faz a correspondência de subcadeias de caracteres e `--help` vem em primeiro lugar em ordem alfabética.
`dotnet add p⇥⇥`                    | `dotnet add package`                                                          | Na segunda vez que a tecla TAB é pressionada, a próxima sugestão é exibida.
`dotnet add package Microsoft⇥`      | `dotnet add package Microsoft.ApplicationInsights.Web`                      | Os resultados são retornados em ordem alfabética.
`dotnet remove reference ⇥`          | `dotnet remove reference ..\..\src\OmniSharp.DotNet\OmniSharp.DotNet.csproj` | O preenchimento com TAB reconhece o arquivo de projeto.

## <a name="powershell"></a>PowerShell

Para adicionar o preenchimento com TAB ao **PowerShell** na CLI do .NET Core, crie ou edite o perfil armazenado na variável `$PROFILE`. Para obter mais informações, confira [Como criar seu perfil](/powershell/module/microsoft.powershell.core/about/about_profiles#how-to-create-a-profile) e [Perfis e política de execução](/powershell/module/microsoft.powershell.core/about/about_profiles#profiles-and-execution-policy).

Adicione o seguinte código ao seu perfil:

```powershell
# PowerShell parameter completion shim for the dotnet CLI
Register-ArgumentCompleter -Native -CommandName dotnet -ScriptBlock {
     param($commandName, $wordToComplete, $cursorPosition)
         dotnet complete --position $cursorPosition "$wordToComplete" | ForEach-Object {
            [System.Management.Automation.CompletionResult]::new($_, $_, 'ParameterValue', $_)
         }
 }
```

## <a name="bash"></a>bash

Para adicionar o preenchimento com TAB ao shell do **Bash** na CLI do .NET Core, adicione o seguinte código ao arquivo `.bashrc`:

```bash
# bash parameter completion for the dotnet CLI

_dotnet_bash_complete()
{
  local word=${COMP_WORDS[COMP_CWORD]}

  local completions
  completions="$(dotnet complete --position "${COMP_POINT}" "${COMP_LINE}" 2>/dev/null)"
  if [ $? -ne 0 ]; then
    completions=""
  fi

  COMPREPLY=( $(compgen -W "$completions" -- "$word") )
}

complete -f -F _dotnet_bash_complete dotnet
```

## <a name="zsh"></a>zsh

Para adicionar o preenchimento com TAB ao shell do **zsh** na CLI do .NET Core, adicione o seguinte código ao arquivo `.zshrc`:

```zsh
# zsh parameter completion for the dotnet CLI

_dotnet_zsh_complete()
{
  local completions=("$(dotnet complete "$words")")

  reply=( "${(ps:\n:)completions}" )
}

compctl -K _dotnet_zsh_complete dotnet
```
