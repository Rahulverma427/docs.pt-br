---
ms.openlocfilehash: 19c613bf48479cb1e52531a4d6594db8ad89b8f3
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "67804678"
---
### <a name="workflowdesignerload-doesnt-remove-symbol-property"></a>WorkflowDesigner.Load não remove a propriedade de símbolo

|   |   |
|---|---|
|Detalhes|Ao destinar para o .NET Framework 4.5 no designer de fluxo de trabalho e carregar um fluxo de trabalho 3.5 hospedado novamente com o método <xref:System.Activities.Presentation.WorkflowDesigner.Load>, uma <xref:System.Xaml.XamlDuplicateMemberException?displayProperty=name> é gerada durante o salvamento do fluxo de trabalho.|
|Sugestão|Esse bug se manifesta somente no direcionamento do .NET Framework 4.5 no designer de fluxo de trabalho, de modo que a solução alternativa é definir o <code>WorkflowDesigner.Context.Services.GetService&lt;DesignerConfigurationService&gt;().TargetFrameworkName</code> para o .NET Framework 4.0. O problema também pode ser evitado usando o método <xref:System.Activities.Presentation.WorkflowDesigner.Load(System.String)> para carregar o fluxo de trabalho, em vez de <xref:System.Activities.Presentation.WorkflowDesigner.Load>.|
|Escopo|Principal|
|Versão|4.5|
|Type|Redirecionando|
|APIs afetadas|<ul><li><xref:System.Activities.Presentation.WorkflowDesigner.Load?displayProperty=nameWithType></li></ul>|
