---
title: 'Como: Habilitar verificação ortográfica em um controle de edição de texto'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- spellchecking [WPF]
- real-time spellchecking
- TextBox control [WPF], real-time spellchecking
- spelling checker [WPF]
- checking spelling [WPF]
ms.assetid: 6f953d2b-67e8-4012-84ce-53c0e958da47
ms.openlocfilehash: 7381bafc349506d89058581e9ed62a4348a72865
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62031936"
---
# <a name="how-to-enable-spell-checking-in-a-text-editing-control"></a>Como: Habilitar verificação ortográfica em um controle de edição de texto
O exemplo a seguir mostra como habilitar verificação ortográfica em tempo real um <xref:System.Windows.Controls.TextBox> usando o <xref:System.Windows.Controls.SpellCheck.IsEnabled%2A> propriedade do <xref:System.Windows.Controls.SpellCheck> classe.  
  
## <a name="example"></a>Exemplo  
 [!code-xaml[TextBoxMiscSnippets_snip#SpellCheckExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/spellcheckexample.xaml#spellcheckexamplewholepage)]  
  
 [!code-csharp[TextBoxMiscSnippets_procedural_snip#SpellCheckCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_procedural_snip/CSharp/SpellCheckExample.cs#spellcheckcodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_procedural_snip#SpellCheckCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_procedural_snip/visualbasic/spellcheckexample.vb#spellcheckcodeexamplewholepage)]  
  
## <a name="see-also"></a>Consulte também

- [Usar verificação ortográfica com um menu de contexto](how-to-use-spell-checking-with-a-context-menu.md)
- [Visão geral de TextBox](textbox-overview.md)
- [Visão geral de RichTextBox](richtextbox-overview.md)
