---
title: Como alterar o alinhamento horizontal de uma coluna em um ListView
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], horizontal alignment [WPF]
ms.assetid: b9573e44-9dad-4d14-939c-7859ca372758
ms.openlocfilehash: 5447f1a73b008b2ed4f345eba00f4d631e11e257
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2019
ms.locfileid: "73458596"
---
# <a name="how-to-change-the-horizontal-alignment-of-a-column-in-a-listview"></a>Como alterar o alinhamento horizontal de uma coluna em um ListView
Por padrão, o conteúdo de cada coluna em uma <xref:System.Windows.Controls.ListViewItem> é alinhado à esquerda. Você pode alterar o alinhamento de cada coluna fornecendo um <xref:System.Windows.DataTemplate> e definindo a propriedade <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> no elemento dentro do <xref:System.Windows.DataTemplate>. Este tópico mostra como um <xref:System.Windows.Controls.ListView> alinha seu conteúdo por padrão e como alterar o alinhamento de uma coluna em uma <xref:System.Windows.Controls.ListView>.  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, os dados nas colunas `Title` e `ISBN` são alinhados à esquerda.  
  
 [!code-xaml[ListViewHowTos#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#1)]  
[!code-xaml[ListViewHowTos#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#2)]  
  
 Para alterar o alinhamento da coluna `ISBN`, é necessário especificar que a propriedade <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> de cada <xref:System.Windows.Controls.ListViewItem> seja <xref:System.Windows.HorizontalAlignment.Stretch>, de modo que os elementos em cada <xref:System.Windows.Controls.ListViewItem> possam se estender ou ser posicionados ao longo de toda a largura de cada coluna. Como o <xref:System.Windows.Controls.ListView> está associado a uma fonte de dados, você precisa criar um estilo que defina o <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>. Em seguida, você precisa usar uma <xref:System.Windows.DataTemplate> para exibir o conteúdo em vez de usar a propriedade <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>. Para exibir o `ISBN` de cada modelo, o <xref:System.Windows.DataTemplate> pode conter apenas um <xref:System.Windows.Controls.TextBlock> que tenha sua propriedade <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> definida como <xref:System.Windows.HorizontalAlignment.Right>.  
  
 O exemplo a seguir define o estilo e <xref:System.Windows.DataTemplate> necessário para tornar a coluna de `ISBN` alinhada à direita e altera a <xref:System.Windows.Controls.GridViewColumn> para fazer referência à <xref:System.Windows.DataTemplate>.  
  
 [!code-xaml[ListViewHowTos#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#3)]  
[!code-xaml[ListViewHowTos#4](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#4)]  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da vinculação de dados](../../../desktop-wpf/data/data-binding-overview.md)
- [Visão geral de modelagem dos dados](../data/data-templating-overview.md)
- [Associar dados XML usando um XMLDataProvider e consultas XPath](../data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)
- [Visão geral de ListView](listview-overview.md)
