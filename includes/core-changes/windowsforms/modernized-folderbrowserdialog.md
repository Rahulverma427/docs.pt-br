---
ms.openlocfilehash: 24141f4b95cda2ae382a923da034e75c329b8555
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71217020"
---
### <a name="modernization-of-the-folderbrowserdialog"></a><span data-ttu-id="468cc-101">Modernização do FolderBrowserDialog</span><span class="sxs-lookup"><span data-stu-id="468cc-101">Modernization of the FolderBrowserDialog</span></span>

<span data-ttu-id="468cc-102">O <xref:System.Windows.Forms.FolderBrowserDialog> controle foi alterado em aplicativos Windows Forms para .NET Core.</span><span class="sxs-lookup"><span data-stu-id="468cc-102">The <xref:System.Windows.Forms.FolderBrowserDialog> control has changed in Windows Forms applications for .NET Core.</span></span>

#### <a name="change-description"></a><span data-ttu-id="468cc-103">Alterar descrição</span><span class="sxs-lookup"><span data-stu-id="468cc-103">Change description</span></span>

<span data-ttu-id="468cc-104">Na .NET Framework, o Windows Forms usa a caixa de diálogo a <xref:System.Windows.Forms.FolderBrowserDialog> seguir para o controle:</span><span class="sxs-lookup"><span data-stu-id="468cc-104">In the .NET Framework, Windows forms uses the following dialog for the <xref:System.Windows.Forms.FolderBrowserDialog> control:</span></span>

![O FolderBrowserDialogControl no .NET Framework](~/docs/images/core-changes/windowsforms/modernized-folderbrowserdialog/folderdlg-framework.png)

<span data-ttu-id="468cc-106">No .NET Core 3,0, Windows Forms usuários um controle baseado em COM mais recente que foi introduzido no Windows Vista:</span><span class="sxs-lookup"><span data-stu-id="468cc-106">In .NET Core 3.0, Windows Forms users a newer COM-based control that was introduced in Windows Vista:</span></span>

![O FolderBrowserDialogControl no .NET Core](~/docs/images/core-changes/windowsforms/modernized-folderbrowserdialog/folderdlg-core.png)

#### <a name="version-introduced"></a><span data-ttu-id="468cc-108">Versão introduzida</span><span class="sxs-lookup"><span data-stu-id="468cc-108">Version introduced</span></span>

<span data-ttu-id="468cc-109">3.0</span><span class="sxs-lookup"><span data-stu-id="468cc-109">3.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="468cc-110">Ação recomendada</span><span class="sxs-lookup"><span data-stu-id="468cc-110">Recommended action</span></span>

<span data-ttu-id="468cc-111">A caixa de diálogo será atualizada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="468cc-111">The dialog will be upgraded automatically.</span></span>

<span data-ttu-id="468cc-112">Se você quiser manter a caixa de diálogo original, defina <xref:System.Windows.Forms.FolderBrowserDialog.AutoUpgradeEnabled?displayProperty=nameWithType> a propriedade `false` como antes de mostrar a caixa de diálogo, conforme ilustrado pelo fragmento de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="468cc-112">If you desire to retain the original dialog, set the <xref:System.Windows.Forms.FolderBrowserDialog.AutoUpgradeEnabled?displayProperty=nameWithType> property to `false` before showing the dialog, as illustrated by the following code fragment:</span></span>

```csharp
var dialog = new FolderBrowserDialog();
dialog.AutoUpgradeEnabled = false;
dialog.ShowDialog();
```

#### <a name="category"></a><span data-ttu-id="468cc-113">Categoria</span><span class="sxs-lookup"><span data-stu-id="468cc-113">Category</span></span>

<span data-ttu-id="468cc-114">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="468cc-114">Windows Forms</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="468cc-115">APIs afetadas</span><span class="sxs-lookup"><span data-stu-id="468cc-115">Affected APIs</span></span>

- <xref:System.Windows.Forms.FolderBrowserDialog>

<!--

### Affected APIs

- `System.Windows.Forms.FolderBrowserDialog`

-->