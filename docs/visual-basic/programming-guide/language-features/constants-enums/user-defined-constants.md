---
title: Constantes definidas pelo usuário
ms.date: 07/20/2015
helpviewer_keywords:
- constants [Visual Basic], circular references
- Const statement [Visual Basic], user-defined constants
- user-defined constants [Visual Basic]
- scope [Visual Basic], constants
- constants [Visual Basic], user-defined
- circular references between constants [Visual Basic]
ms.assetid: a1206d5c-c45e-4ac2-970a-4a0be6a05fdd
ms.openlocfilehash: 194a420b3749ca5c858a65c07b8c164287c1582a
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74354013"
---
# <a name="user-defined-constants-visual-basic"></a>Constantes definidas pelo usuário (Visual Basic)
Uma constante é um nome significativo que substitui um número ou uma cadeia de caracteres que não é alterada. Constantes armazenam valores que, como o nome implica, permanecem constantes durante a execução de um aplicativo. Você pode usar constantes que são definidas pelos controles ou componentes com os quais você trabalha, ou você pode criar suas próprias. As constantes que você cria são descritas como *definidas pelo usuário*.  
  
 Você declara uma constante com a instrução `Const`, usando as mesmas diretrizes para criar um nome de variável. Se `Option Strict` for `On`, você deverá declarar explicitamente o tipo de constante.  
  
## <a name="const-statement-usage"></a>Uso da instrução const  
 Uma instrução `Const` pode representar uma quantidade matemática ou de data/hora:  
  
 [!code-vb[VbEnumsTask#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#10)]  
  
 Ele também pode definir `String` constantes:  
  
 [!code-vb[VbEnumsTask#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#13)]  
  
 A expressão no lado direito do sinal de igual (`=`) geralmente é um número ou uma cadeia de caracteres literal, mas também pode ser uma expressão que resulte em um número ou cadeia de caracteres (embora essa expressão não possa conter chamadas para funções). Você pode até mesmo definir constantes em termos de constantes definidas anteriormente:  
  
 [!code-vb[VbEnumsTask#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#15)]  
  
## <a name="scope-of-user-defined-constants"></a>Escopo de constantes definidas pelo usuário  
 O escopo de uma instrução de `Const` é o mesmo de uma variável declarada no mesmo local. Você pode especificar o escopo de qualquer uma das seguintes maneiras:  
  
- Para criar uma constante que existe somente dentro de um procedimento, declare-a dentro desse procedimento.  
  
- Para criar uma constante disponível para todos os procedimentos em uma classe, mas não para qualquer código fora desse módulo, declare-o na seção declarações da classe.  
  
- Para criar uma constante que está disponível para todos os membros de um assembly, mas não para clientes externos do assembly, declare-o usando a palavra-chave `Friend` na seção declarações da classe.  
  
- Para criar uma constante disponível em todo o aplicativo, declare-a usando a palavra-chave `Public` na seção declarações a classe.  
  
 Para obter mais informações, consulte [como: declarar uma constante](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md).  
  
### <a name="avoiding-circular-references"></a>Evitando referências circulares  
 Como constantes podem ser definidas em termos de outras constantes, é possível criar inadvertidamente um *ciclo*, ou referência circular, entre duas ou mais constantes. Um ciclo ocorre quando você tem duas ou mais constantes públicas, cada uma delas definida em termos do outro, como no exemplo a seguir:  
  
 [!code-vb[VbEnumsTask#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#16)]  
[!code-vb[VbEnumsTask#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#17)]  
  
 Se ocorrer um ciclo, Visual Basic gerará um erro do compilador.  
  
## <a name="see-also"></a>Consulte também

- [Instrução Const](../../../../visual-basic/language-reference/statements/const-statement.md)
- [Tipos de Dados Constante e Literal](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)
- [Constantes e Enumerações](../../../../visual-basic/programming-guide/language-features/constants-enums/index.md)
- [Constantes e Enumerações](../../../../visual-basic/language-reference/constants-and-enumerations.md)
- [Visão geral de Enumerações](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)
- [Visão Geral de Constantes](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)
- [Como declarar uma enumeração](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)
- [Enumerações e Qualificação de Nome](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [Instrução Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
