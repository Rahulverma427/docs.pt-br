---
title: Como criar um pool de objetos usando um ConcurrentBag
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- object pool, in .NET Framework
ms.assetid: 0480e7ff-b6f9-480e-a889-2ed4264d8372
ms.openlocfilehash: 888521eb5c3c3169c4b39a26e82fef2e35c286d9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "75711266"
---
# <a name="how-to-create-an-object-pool-by-using-a-concurrentbag"></a>Como criar um pool de objetos usando um ConcurrentBag
Este exemplo mostra como usar um recipiente simultâneo para implementar um pool de objetos. Pools de objeto podem melhorar o desempenho do aplicativo em situações em que exigem várias instâncias de uma classe e nos quais criar ou destruir a classe é um processo caro. Quando um programa cliente solicita um novo objeto, o pool de objetos primeiro tenta fornecer um que já foi criado e retornado ao pool. Se nenhum estiver disponível, só então um novo objeto será criado.  
  
 <xref:System.Collections.Concurrent.ConcurrentBag%601> é usado para armazenar os objetos porque ele dá suporte à inserção e remoção rápidas, principalmente quando o mesmo thread está adicionando e removendo itens. Esse exemplo poderia ser aumentado ainda mais para ser criado em torno de um <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>, que a estrutura de dados do recipiente implementa, como <xref:System.Collections.Concurrent.ConcurrentQueue%601> e <xref:System.Collections.Concurrent.ConcurrentStack%601> fazem.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[CDS#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/objectpool.cs#04)]
 [!code-vb[CDS#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/objectpool04.vb#04)]  
  
## <a name="see-also"></a>Confira também

- [Coleções Thread-Safe](../../../../docs/standard/collections/thread-safe/index.md)
