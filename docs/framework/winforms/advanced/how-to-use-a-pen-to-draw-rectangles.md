---
title: 'Como: usar uma caneta para desenhar retângulos'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- rectangles [Windows Forms], drawing
- pens [Windows Forms], drawing rectangles
ms.assetid: 54a7fa14-3ad8-4d64-b424-2a12005b250c
ms.openlocfilehash: cd5d965f8b92d15cdeb3049330d9b3cc0de893b2
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590233"
---
# <a name="how-to-use-a-pen-to-draw-rectangles"></a>Como: usar uma caneta para desenhar retângulos
Para desenhar retângulos, é necessário um <xref:System.Drawing.Graphics> objeto e um <xref:System.Drawing.Pen> objeto. O <xref:System.Drawing.Graphics> objeto fornece os <xref:System.Drawing.Graphics.DrawRectangle%2A> método e o <xref:System.Drawing.Pen> objeto armazena recursos da linha, como cor e largura.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir desenha um retângulo com seu canto superior esquerdo em (10, 10). O retângulo tem uma largura de 100 e uma altura de 50. O segundo argumento passado para o <xref:System.Drawing.Pen.%23ctor%2A> construtor indica que a largura da caneta é 5 pixels.  
  
 Quando o retângulo é desenhado, a caneta é centralizada no limite do retângulo. Como a largura da caneta é 5, os lados do retângulo são desenhados com 5 pixels de largura, de forma que 1 pixel é desenhado no próprio limite, 2 pixels são desenhados no interior e 2 pixels são desenhados fora. Para obter mais detalhes sobre o alinhamento da caneta, consulte [como: Defina a largura da caneta e o alinhamento](how-to-set-pen-width-and-alignment.md).  
  
 A ilustração a seguir mostra o retângulo resultante. As linhas pontilhadas mostram onde o retângulo deveria ser desenhado se a largura da caneta tivesse um pixel. A exibição ampliada do canto superior esquerdo do retângulo mostra que as linhas pretas espessas são centralizadas nessas linhas pontilhadas.  
  
 ![Captura de tela mostrando o retângulo desenhado com preto e a linha pontilhada.](./media/how-to-use-a-pen-to-draw-rectangles/drawn-rectangle-black-lines-dotted-lines.gif)  
  
 [!code-csharp[System.Drawing.UsingAPen#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.UsingAPen#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#21)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 O exemplo anterior foi projetado para uso com o Windows Forms e requer <xref:System.Windows.Forms.PaintEventArgs> `e`, que é um parâmetro do <xref:System.Windows.Forms.Control.Paint> manipulador de eventos.  
  
## <a name="see-also"></a>Consulte também

- [Usando uma caneta para desenhar linhas e formas](using-a-pen-to-draw-lines-and-shapes.md)
