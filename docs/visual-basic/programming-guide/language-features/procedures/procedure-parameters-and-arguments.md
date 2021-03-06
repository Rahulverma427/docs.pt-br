---
title: Parâmetros e argumentos de procedimento
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], argument lists
- values [Visual Basic], passing to procedures
- arguments [Visual Basic], passing
- procedures [Visual Basic], parameters
- Visual Basic code, argument lists
- Visual Basic code, procedures
- parameters [Visual Basic], Visual Basic procedures
- parameters [Visual Basic], lists
- arguments [Visual Basic], Visual Basic procedures
- arguments [Visual Basic], procedures
- parameter lists [Visual Basic]
- Visual Basic code, parameter lists
- argument lists [Visual Basic]
- procedures [Visual Basic], parameter lists
ms.assetid: ff275aff-aa13-40df-bd4c-63486db8c1e9
ms.openlocfilehash: 7dfbbcb39cf7bb05c8a62a7a252e425f287c9a09
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74352578"
---
# <a name="procedure-parameters-and-arguments-visual-basic"></a>Parâmetros e argumentos de procedimento (Visual Basic)
Na maioria dos casos, um procedimento precisa de algumas informações sobre as circunstâncias em que ele foi chamado. Um procedimento que executa tarefas repetidas ou compartilhadas usa informações diferentes para cada chamada. Essas informações consistem em variáveis, constantes e expressões que você passa para o procedimento ao chamá-lo.  
  
 Um *parâmetro* representa um valor que o procedimento espera que você forneça ao chamá-lo. A declaração do procedimento define seus parâmetros.  
  
 Você pode definir um procedimento sem parâmetros, um parâmetro ou mais de um. A parte da definição do procedimento que especifica os parâmetros é chamada de *lista de parâmetros*.  
  
 Um *argumento* representa o valor que você fornece a um parâmetro de procedimento ao chamar o procedimento. O código de chamada fornece os argumentos ao chamar o procedimento. A parte da chamada de procedimento que especifica os argumentos é chamada de *lista de argumentos*.  
  
 A ilustração a seguir mostra o código que chama o procedimento `safeSquareRoot` de dois locais diferentes. A primeira chamada passa o valor da variável `x` (4,0) para o parâmetro `number`e o valor de retorno em `root` (2,0) é atribuído à variável `y`. A segunda chamada passa o valor literal 9,0 para `number`e atribui o valor de retorno (3,0) à variável `z`.  
  
 ![Diagrama que mostra a passagem de um argumento para um parâmetro](./media/procedure-parameters-and-arguments/pass-argument-parameter.gif)  
  
 Para obter mais informações, consulte [diferenças entre parâmetros e argumentos](./differences-between-parameters-and-arguments.md).  
  
## <a name="parameter-data-type"></a>Tipo de dados de parâmetro  
 Você define um tipo de dados para um parâmetro usando a cláusula `As` em sua declaração. Por exemplo, a função a seguir aceita uma cadeia de caracteres e um inteiro.  
  
 [!code-vb[VbVbcnProcedures#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#32)]  
  
 Se a opção de verificação de tipo ([instrução Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) for `Off,` a cláusula `As` for opcional, exceto que, se qualquer parâmetro usar, todos os parâmetros deverão usá-lo. Se a verificação de tipo for `On`, a cláusula `As` será necessária para todos os parâmetros de procedimento.  
  
 Se o código de chamada espera fornecer um argumento com um tipo de dados diferente daquele de seu parâmetro correspondente, como `Byte` para um parâmetro `String`, ele deve executar um dos seguintes procedimentos:  
  
- Forneça somente argumentos com tipos de dados que ampliam para o tipo de dados de parâmetro;  
  
- Defina `Option Strict Off` para permitir conversões de estreitamento implícitas; or  
  
- Use uma palavra-chave de conversão para converter explicitamente o tipo de dados.  
  
### <a name="type-parameters"></a>Parâmetros de tipo  
 Um *procedimento genérico* também define um ou mais *parâmetros de tipo* , além de seus parâmetros normais. Um procedimento genérico permite que o código de chamada passe tipos de dados diferentes cada vez que chama o procedimento, para que possa personalizar os tipos de dados para os requisitos de cada chamada individual. Consulte [procedimentos genéricos em Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md).  
  
## <a name="see-also"></a>Consulte também

- [Procedimentos](./index.md)
- [Subprocedimentos](./sub-procedures.md)
- [Procedimentos de Função](./function-procedures.md)
- [Procedimentos de Propriedade](./property-procedures.md)
- [Procedimentos de Operador](./operator-procedures.md)
- [Como definir um parâmetro para um procedimento](./how-to-define-a-parameter-for-a-procedure.md)
- [Como passar argumentos para um procedimento](./how-to-pass-arguments-to-a-procedure.md)
- [Passando Argumentos por Valor e por Referência](./passing-arguments-by-value-and-by-reference.md)
- [Sobrecarga de Procedimento](./procedure-overloading.md)
- [Conversões de tipo no Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
