---
title: Personalizando operações usando procedimentos armazenados exclusivamente
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 441e8ef3-998c-4d12-8825-ce66a178f90f
ms.openlocfilehash: a242ecdc774d67721aee640e75847317c1b815d6
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70247541"
---
# <a name="customizing-operations-by-using-stored-procedures-exclusively"></a>Personalizando operações usando procedimentos armazenados exclusivamente
Acesso a dados usando somente procedimentos armazenados é um cenário comum.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 Você pode modificar o exemplo fornecido em [Personalizando operações usando procedimentos armazenados](customizing-operations-by-using-stored-procedures.md) substituindo até mesmo a primeira consulta (o que causa a execução SQL dinâmica) com uma chamada de método que encapsula um procedimento armazenado.  
  
 Suponha `CustomersByCity` é o método, como no exemplo a seguir.  
  
### <a name="code"></a>Código  
 [!code-csharp[DLinqOverrideDefaultSproc#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefaultSproc/cs/northwind.cs#4)]
 [!code-vb[DLinqOverrideDefaultSproc#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefaultSproc/vb/northwind.vb#4)]  
  
 O código a seguir executa sem nenhum SQL dinâmicos.  
  
 [!code-csharp[DLinqOverrideDefaultSproc#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefaultSproc/cs/Program.cs#5)]
 [!code-vb[DLinqOverrideDefaultSproc#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefaultSproc/vb/Module1.vb#5)]  
  
## <a name="see-also"></a>Consulte também

- [Responsabilidades do desenvolvedor em substituir o comportamento padrão](responsibilities-of-the-developer-in-overriding-default-behavior.md)
