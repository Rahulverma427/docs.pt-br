---
title: REF CURSORs do Oracle
ms.date: 03/30/2017
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
ms.openlocfilehash: 7cd29a6a20015c7ce4475b0211cb07f7ee78b530
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794878"
---
# <a name="oracle-ref-cursors"></a>REF CURSORs do Oracle
O .NET Framework Provedor de Dados para Oracle dá suporte ao tipo de dados **cursor de referência** do Oracle. Ao usar o provedor de dados para trabalhar com REF CURSORs do Oracle, você deve considerar os seguintes comportamentos.  
  
> [!NOTE]
> Alguns comportamentos diferem dos do Provedor OLE DB para Oracle (MSDAORA).  
  
- Por motivos de desempenho, o Provedor de Dados para Oracle não associa automaticamente tipos de dados de **cursor de referência** , como MSDAORA, a menos que você os especifique explicitamente.  
  
- O provedor de dados não oferece suporte a nenhuma sequência de escape de ODBC, incluindo o escape {resultset} usado para especificar parâmetros de REF CURSOR.  
  
- Para executar um procedimento armazenado que retorna cursores de referência, você deve definir os parâmetros no <xref:System.Data.OracleClient.OracleParameterCollection> com um <xref:System.Data.OracleClient.OracleType> de **cursor** e uma <xref:System.Data.OracleClient.OracleParameter.Direction%2A> de **saída**. O provedor de dados oferece suporte a REF CURSORs de associação como parâmetros de saída somente. O provedor não oferece suporte a REF CURSORs como parâmetros de entrada.  
  
- A obtenção de <xref:System.Data.OracleClient.OracleDataReader> do valor do parâmetro não é suportada. Os valores são do tipo <xref:System.DBNull> após a execução do comando.  
  
- O único valor de enumeração **CommandBehavior** que funciona com cursores de referência (por exemplo, <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A>ao chamar) é **CloseConnection**; todos os outros são ignorados.  
  
- A ordem dos CURSOres de referência no **OracleDataReader** depende da ordem dos parâmetros no **OracleParameterCollection**. A propriedade <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A> é ignorada.  
  
- Não há suporte para o tipo de dados de **tabela** PL/SQL. No entanto, REF CURSORs são mais eficientes. Se você precisar usar um tipo de dados de **tabela** , use o OLE DB .NET provedor de dados com MSDAORA.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exemplos de REF CURSOR](ref-cursor-examples.md)  
 Contém três exemplos que demonstram como usar REF CURSORs.  
  
 [Parâmetros de REF CURSOR em um OracleDataReader](ref-cursor-parameters-in-an-oracledatareader.md)  
 Demonstra como executar um procedimento armazenado PL/SQL que retorna um parâmetro de CURSOR REF e lê o valor como um **OracleDataReader**.  
  
 [Recuperando dados de vários REF CURSORs usando um OracleDataReader](retrieving-data-from-multiple-ref-cursors.md)  
 Demonstra como executar um procedimento armazenado PL/SQL que retorna dois parâmetros de CURSOR de referência e lê os valores usando um **OracleDataReader**.  
  
 [Preenchendo um DataSet usando um ou mais REF CURSORs](filling-a-dataset-using-one-or-more-ref-cursors.md)  
 Demonstra como executar um procedimento armazenado PL/SQL, que retorna dois parâmetros de REF CURSOR e preenche um <xref:System.Data.DataSet> com as linhas retornadas.  
  
## <a name="see-also"></a>Consulte também

- [Oracle and ADO.NET](oracle-and-adonet.md) (Oracle e ADO.NET)
- [ADO.NET Overview](ado-net-overview.md) (Visão geral do ADO.NET)
