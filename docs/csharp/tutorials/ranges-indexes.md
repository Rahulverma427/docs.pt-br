---
title: Explore os intervalos de dados usando intervalos e índices
description: Este tutorial avançado ensina você a explorar dados usando intervalos e índices para examinar fatias de um conjunto de dados sequencial.
ms.date: 04/19/2019
ms.custom: mvc
ms.openlocfilehash: 64fae4581e265d4f70b8356d5c651b4fdaca3fe9
ms.sourcegitcommit: dd3b897feb5c4ac39732bb165848e37a344b0765
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2019
ms.locfileid: "64431497"
---
# <a name="indices-and-ranges"></a><span data-ttu-id="f3317-103">Índices e intervalos</span><span class="sxs-lookup"><span data-stu-id="f3317-103">Indices and ranges</span></span>

<span data-ttu-id="f3317-104">Intervalos e índices fornecem uma sintaxe sucinta para acessar elementos únicos ou intervalos em <xref:System.Array>, <xref:System.Span%601> ou <xref:System.ReadOnlySpan%601>.</span><span class="sxs-lookup"><span data-stu-id="f3317-104">Ranges and indices provide a succinct syntax for accessing single elements or ranges in an <xref:System.Array>, <xref:System.Span%601>, or <xref:System.ReadOnlySpan%601>.</span></span> <span data-ttu-id="f3317-105">Esses recursos permitem uma sintaxe mais concisa e clara para acessar elementos únicos ou intervalos de elementos em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="f3317-105">These features enable more concise, clear syntax to access single elements or ranges of elements in a sequence.</span></span>

<span data-ttu-id="f3317-106">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="f3317-106">In this tutorial, you'll learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3317-107">Use a sintaxe para intervalos em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="f3317-107">Use the syntax for ranges in a sequence.</span></span>
> * <span data-ttu-id="f3317-108">Compreenda as decisões de design para o início e o fim de cada sequência.</span><span class="sxs-lookup"><span data-stu-id="f3317-108">Understand the design decisions for the start and end of each sequence.</span></span>
> * <span data-ttu-id="f3317-109">Conheça cenários para os tipos <xref:System.Index> e <xref:System.Range>.</span><span class="sxs-lookup"><span data-stu-id="f3317-109">Learn scenarios for the <xref:System.Index> and <xref:System.Range> types.</span></span>

## <a name="language-support-for-indices-and-ranges"></a><span data-ttu-id="f3317-110">Suporte a idioma para intervalos e índices</span><span class="sxs-lookup"><span data-stu-id="f3317-110">Language support for indices and ranges</span></span>

<span data-ttu-id="f3317-111">Você pode especificar um índice **do final** usando o caractere `^` antes do índice.</span><span class="sxs-lookup"><span data-stu-id="f3317-111">You can specify an index **from the end** using the `^` character before the index.</span></span> <span data-ttu-id="f3317-112">A indexação do final começa da regra que `0..^0` especifica o intervalo inteiro.</span><span class="sxs-lookup"><span data-stu-id="f3317-112">Indexing from the end starts from the rule that `0..^0` specifies the entire range.</span></span> <span data-ttu-id="f3317-113">Para enumerar uma matriz inteira, você inicia *no primeiro elemento* e continua até você *passar do último elemento*.</span><span class="sxs-lookup"><span data-stu-id="f3317-113">To enumerate an entire array, you start *at the first element*, and continue until you are *past the last element*.</span></span> <span data-ttu-id="f3317-114">Pense no comportamento do método `MoveNext` em um enumerador: ele retorna falso quando a enumeração passa do último elemento.</span><span class="sxs-lookup"><span data-stu-id="f3317-114">Think of the behavior of the `MoveNext` method on an enumerator: it returns false when the enumeration passes the last element.</span></span> <span data-ttu-id="f3317-115">O índice `^0` significa "o fim", `array[array.Length]`, ou o índice que segue o último elemento.</span><span class="sxs-lookup"><span data-stu-id="f3317-115">The index `^0` means "the end", `array[array.Length]`, or the index that follows the last element.</span></span> <span data-ttu-id="f3317-116">Você está familiarizado com `array[2]` significando o elemento "2 desde o início".</span><span class="sxs-lookup"><span data-stu-id="f3317-116">You are familiar with `array[2]` meaning the element "2 from the start".</span></span> <span data-ttu-id="f3317-117">Agora, `array[^2]` significa o elemento "2 desde o final".</span><span class="sxs-lookup"><span data-stu-id="f3317-117">Now, `array[^2]` means the element "2 from the end".</span></span> 

<span data-ttu-id="f3317-118">Você pode especificar um **intervalo** com o **operador de intervalo**: `..`.</span><span class="sxs-lookup"><span data-stu-id="f3317-118">You can specify a **range** with the **range operator**: `..`.</span></span> <span data-ttu-id="f3317-119">Por exemplo, `0..^0` especifica todo o intervalo da matriz: 0 desde o início até, mas não incluindo, 0 do final.</span><span class="sxs-lookup"><span data-stu-id="f3317-119">For example, `0..^0` specifies the entire range of the array: 0 from the start up to, but not including 0 from the end.</span></span> <span data-ttu-id="f3317-120">Qualquer operando pode usar "desde o início" ou "desde o final".</span><span class="sxs-lookup"><span data-stu-id="f3317-120">Either operand may use "from the start" or "from the end".</span></span> <span data-ttu-id="f3317-121">Além disso, qualquer operando pode ser omitido.</span><span class="sxs-lookup"><span data-stu-id="f3317-121">Furthermore, either operand may be omitted.</span></span> <span data-ttu-id="f3317-122">Os padrões são `0` para o índice de início, e `^0` para o índice final.</span><span class="sxs-lookup"><span data-stu-id="f3317-122">The defaults are `0` for the start index, and `^0` for the end index.</span></span>

```csharp-interactive
string[] words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};              // 9 (or words.Length) ^0
```

<span data-ttu-id="f3317-123">O índice de cada elemento reforça o conceito de "do início" e "do final", e que os intervalos excluem o fim do intervalo.</span><span class="sxs-lookup"><span data-stu-id="f3317-123">The index of each element reinforces the concept of "from the start", and "from the end", and that ranges are exclusive of the end of the range.</span></span> <span data-ttu-id="f3317-124">O "início" de toda a matriz é o primeiro elemento.</span><span class="sxs-lookup"><span data-stu-id="f3317-124">The "start" of the entire array is the first element.</span></span> <span data-ttu-id="f3317-125">O "final" de toda a matriz ocorre *após* o último elemento.</span><span class="sxs-lookup"><span data-stu-id="f3317-125">The "end" of the entire array is *past* the last element.</span></span>

<span data-ttu-id="f3317-126">Você pode recuperar a última palavra com o índice `^1`.</span><span class="sxs-lookup"><span data-stu-id="f3317-126">You can retrieve the last word with the `^1` index.</span></span> <span data-ttu-id="f3317-127">Adicione o código a seguir abaixo da inicialização:</span><span class="sxs-lookup"><span data-stu-id="f3317-127">Add the following code below the initialization:</span></span>

[!code-csharp[LastIndex](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastIndex)]

<span data-ttu-id="f3317-128">O código a seguir cria um subintervalo com as palavras "quick", "brown" e "fox".</span><span class="sxs-lookup"><span data-stu-id="f3317-128">The following code creates a subrange with the words "quick", "brown", and "fox".</span></span> <span data-ttu-id="f3317-129">Ele inclui `words[1]` até `words[3]`.</span><span class="sxs-lookup"><span data-stu-id="f3317-129">It includes `words[1]` through `words[3]`.</span></span> <span data-ttu-id="f3317-130">O elemento `words[4]` não está no intervalo.</span><span class="sxs-lookup"><span data-stu-id="f3317-130">The element `words[4]` isn't in the range.</span></span> <span data-ttu-id="f3317-131">Adicione o seguinte código ao mesmo método.</span><span class="sxs-lookup"><span data-stu-id="f3317-131">Add the following code to the same method.</span></span> <span data-ttu-id="f3317-132">Copie e cole-o na parte inferior da janela interativa.</span><span class="sxs-lookup"><span data-stu-id="f3317-132">Copy and paste it at the bottom of the interactive window.</span></span>

[!code-csharp[Range](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Range)]

<span data-ttu-id="f3317-133">O código a seguir cria um subintervalo com "lazy" e "dog".</span><span class="sxs-lookup"><span data-stu-id="f3317-133">The following code creates a subrange with "lazy" and "dog".</span></span> <span data-ttu-id="f3317-134">Ele inclui `words[^2]` e `words[^1]`.</span><span class="sxs-lookup"><span data-stu-id="f3317-134">It includes `words[^2]` and `words[^1]`.</span></span> <span data-ttu-id="f3317-135">O índice final `words[^0]` não está incluído.</span><span class="sxs-lookup"><span data-stu-id="f3317-135">The end index `words[^0]` isn't included.</span></span> <span data-ttu-id="f3317-136">Adicione o seguinte código também:</span><span class="sxs-lookup"><span data-stu-id="f3317-136">Add the following code as well:</span></span>

[!code-csharp[LastRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastRange)]

<span data-ttu-id="f3317-137">Os exemplos a seguir criam intervalos abertos para o início, fim ou ambos:</span><span class="sxs-lookup"><span data-stu-id="f3317-137">The following examples create ranges that are open ended for the start, end, or both:</span></span>

[!code-csharp[PartialRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_PartialRanges)]

<span data-ttu-id="f3317-138">Você também pode declarar intervalos ou índices como variáveis.</span><span class="sxs-lookup"><span data-stu-id="f3317-138">You can also declare ranges or indices as variables.</span></span> <span data-ttu-id="f3317-139">A variável então pode ser usada dentro dos caracteres `[` e `]`:</span><span class="sxs-lookup"><span data-stu-id="f3317-139">The variable can then be used inside the `[` and `]` characters:</span></span>

[!code-csharp[IndexRangeTypes](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_RangeIndexTypes)]

<span data-ttu-id="f3317-140">Os exemplos anteriores mostram duas decisões de design que exigem mais explicação:</span><span class="sxs-lookup"><span data-stu-id="f3317-140">The previous examples show two design decisions that require more explanation:</span></span>

- <span data-ttu-id="f3317-141">Os intervalos são *exclusivos*, o que significa que o elemento no último índice não está no intervalo.</span><span class="sxs-lookup"><span data-stu-id="f3317-141">Ranges are *exclusive*, meaning the element at the last index isn't in the range.</span></span>
- <span data-ttu-id="f3317-142">O índice `^0` é *o fim* da coleção, não *o último elemento* na coleção.</span><span class="sxs-lookup"><span data-stu-id="f3317-142">The index `^0` is *the end* of the collection, not *the last element* in the collection.</span></span>

<span data-ttu-id="f3317-143">O exemplo a seguir mostra muitos dos motivos para essas escolhas.</span><span class="sxs-lookup"><span data-stu-id="f3317-143">The following sample shows many of the reasons for those choices.</span></span> <span data-ttu-id="f3317-144">Modifique `x`, `y` e `z` para tentar combinações diferentes.</span><span class="sxs-lookup"><span data-stu-id="f3317-144">Modify `x`, `y`, and `z` to try different combinations.</span></span> <span data-ttu-id="f3317-145">Quando você testar, use valores em que `x` é menor que `y` e `y` é menor que `z` para as combinações válidas.</span><span class="sxs-lookup"><span data-stu-id="f3317-145">When you experiment, use values where `x` is less than `y`, and `y` is less than `z` for valid combinations.</span></span> <span data-ttu-id="f3317-146">Adicione o seguinte código a um novo método.</span><span class="sxs-lookup"><span data-stu-id="f3317-146">Add the following code in a new method.</span></span> <span data-ttu-id="f3317-147">Tente usar combinações diferentes:</span><span class="sxs-lookup"><span data-stu-id="f3317-147">Try different combinations:</span></span>

[!code-csharp[SemanticsExamples](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Semantics)]

## <a name="scenarios-for-indices-and-ranges"></a><span data-ttu-id="f3317-148">Cenários para Intervalos e Índices</span><span class="sxs-lookup"><span data-stu-id="f3317-148">Scenarios for Indices and Ranges</span></span>

<span data-ttu-id="f3317-149">Você muitas vezes usará intervalos e índices quando quiser executar uma análise no subintervalo de uma sequência inteira.</span><span class="sxs-lookup"><span data-stu-id="f3317-149">You'll often use ranges and indices when you want to perform some analysis on subrange of an entire sequence.</span></span> <span data-ttu-id="f3317-150">A nova sintaxe é mais clara para ler exatamente quais subintervalo está envolvido.</span><span class="sxs-lookup"><span data-stu-id="f3317-150">The new syntax is clearer in reading exactly what subrange is involved.</span></span> <span data-ttu-id="f3317-151">A função local `MovingAverage` usa um <xref:System.Range> como seu argumento.</span><span class="sxs-lookup"><span data-stu-id="f3317-151">The local function `MovingAverage` takes a <xref:System.Range> as its argument.</span></span> <span data-ttu-id="f3317-152">O método então enumera apenas esse intervalo ao calcular o mínimo, máximo e média.</span><span class="sxs-lookup"><span data-stu-id="f3317-152">The method then enumerates just that range when calculating the min, max, and average.</span></span> <span data-ttu-id="f3317-153">Experimente o seguinte código em seu projeto:</span><span class="sxs-lookup"><span data-stu-id="f3317-153">Try the following code in your project:</span></span>

[!code-csharp[MovingAverages](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_MovingAverage)]

<span data-ttu-id="f3317-154">Baixe o código concluído no repositório [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/RangesIndexes).</span><span class="sxs-lookup"><span data-stu-id="f3317-154">You can download the completed code from the [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/RangesIndexes) repository.</span></span>