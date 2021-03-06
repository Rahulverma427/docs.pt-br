---
title: 'Tutorial: ML.NET modelo de classificação de imagem do TensorFlow'
description: Aprenda a transferir o conhecimento de um modelo TensorFlow existente para um novo modelo de classificação de imagem ML.NET. O modelo TensorFlow foi treinado para classificar as imagens em mil categorias. O modelo ML.NET faz uso do aprendizado de transferência para classificar imagens em categorias menos amplas.
ms.date: 01/30/2020
ms.topic: tutorial
ms.custom: mvc, title-hack-0612
ms.openlocfilehash: 1e5478f53c82f36ddafe19e3659e2234ff9687b4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "78241020"
---
# <a name="tutorial-generate-an-mlnet-image-classification-model-from-a-pre-trained-tensorflow-model"></a>Tutorial: Gere um modelo de classificação de imagem ML.NET a partir de um modelo TensorFlow pré-treinado

Aprenda a transferir o conhecimento de um modelo TensorFlow existente para um novo modelo de classificação de imagem ML.NET.

O modelo TensorFlow foi treinado para classificar as imagens em mil categorias. O modelo ML.NET faz uso de parte do modelo TensorFlow em seu pipeline para treinar um modelo para classificar imagens em 3 categorias.

Treinar um modelo de [Classificação de Imagens](https://en.wikipedia.org/wiki/Outline_of_object_recognition) do zero requer a configuração de milhões de parâmetros, uma tonelada de dados de treinamento rotulados e uma grande quantidade de recursos de computação (centenas de horas de GPU). Embora não seja tão eficaz quanto treinar um modelo personalizado do zero, o aprendizado de transferência permite que você ative esse processo trabalhando com milhares de imagens em comparação com milhões de imagens rotuladas e crie um modelo personalizado rapidamente (em uma hora em uma máquina sem GPU). Este tutorial dimensiona esse processo ainda mais, usando apenas uma dúzia de imagens de treinamento.

Neste tutorial, você aprenderá como:
> [!div class="checklist"]
>
> * Compreender o problema
> * Incorpore o modelo TensorFlow pré-treinado no pipeline ML.NET
> * Treine e avalie o modelo ML.NET
> * Classificar uma imagem de teste

Você pode encontrar o código-fonte para este tutorial no repositório [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF). Observe que, por padrão, a configuração de projeto do .NET para este tutorial se destina ao .NET Core 2.2.

## <a name="what-is-transfer-learning"></a>O que é o aprendizado por transferência?

Transferir aprendizagem é o processo de usar o conhecimento adquirido ao resolver um problema e aplicá-lo a um problema diferente, mas relacionado.

Para este tutorial, você usa parte de um modelo TensorFlow - treinado para classificar imagens em mil categorias - em um modelo ML.NET que classifica imagens em 3 categorias.

## <a name="prerequisites"></a>Pré-requisitos

* [Visual Studio 2017 versão 15.6 ou posterior](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) com a carga de trabalho ".NET Core cross-platform development" instalada.
* [O arquivo .ZIP do diretório de recursos do tutorial](https://github.com/dotnet/samples/blob/master/machine-learning/tutorials/TransferLearningTF/image-classifier-assets.zip)
* [O modelo de machine learning do InceptionV1](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip)

## <a name="select-the-right-machine-learning-task"></a>Selecione a tarefa de aprendizado de máquina certa

### <a name="deep-learning"></a>Aprendizado

[Aprendizado profundo](https://en.wikipedia.org/wiki/Deep_learning) é um subconjunto do aprendizado de máquina, que está revolucionando áreas como Pesquisa Visual Computacional e Reconhecimento de Fala.

Os modelos de aprendizado profundo são treinados usando grandes conjuntos de [dados rotulados](https://en.wikipedia.org/wiki/Labeled_data) e [redes neurais](https://en.wikipedia.org/wiki/Artificial_neural_network) que contêm várias camadas de aprendizado. Aprendizado profundo:

* Funciona melhor em algumas tarefas como a Pesquisa Visual Computacional.
* Requer enormes quantidades de dados de treinamento.

Classificação de imagens é uma tarefa comum de Aprendizado de Máquina que nos permite classificar automaticamente as imagens em categorias como:

* Detectar uma face humana em uma imagem ou não.
* Detectando gatos vs. cães.

 Ou como nas imagens a seguir, determinando se uma imagem é um(n) alimento, brinquedo ou aparelho:

![imagem de pizza](./media/image-classification/220px-Pepperoni_pizza.jpg)
![imagem de ursinho de pelúcia](./media/image-classification/119px-Nalle_-_a_small_brown_teddy_bear.jpg)
![imagem de torradeira](./media/image-classification/193px-Broodrooster.jpg)

>[!Note]
> As imagens anteriores pertencem ao Wikimedia Commons e são atribuídas da seguinte forma:
>
> * "220px-Pepperoni_pizza.jpg" Public Domain, https://commons.wikimedia.org/w/index.php?curid=79505,
> * "119px-Nalle_-_a_small_brown_teddy_bear.jpg" By [Jonik](https://commons.wikimedia.org/wiki/User:Jonik) - Self-photographed, CC BY-SA 2.0, https://commons.wikimedia.org/w/index.php?curid=48166.
> * "193px-Broodrooster.jpg" By [M.Minderhoud](https://nl.wikipedia.org/wiki/Gebruiker:Michiel1972) - Own work, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=27403

O `Inception model` é treinado para classificar imagens em mil categorias, mas para este tutorial, você precisa classificar imagens em um conjunto de categorias menores, e apenas essas categorias. Digite a parte `transfer` de `transfer learning`. Você pode transferir a capacidade de `Inception model` de reconhecer e classificar imagens para as novas categorias limitadas do seu classificador de imagens personalizadas.

* Alimentos
* Brinquedos
* Dispositivos

Este tutorial usa o modelo TensorFlow [Inception](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip) de deep learning, um modelo popular de reconhecimento de imagem treinado no `ImageNet` conjunto de dados. O modelo TensorFlow classifica imagens inteiras em mil classes, como "Umbrella", "Jersey" e "Dishwasher".

Como `Inception model` o já foi pré-treinado em milhares de imagens diferentes, internamente contém os [recursos de imagem necessários](https://en.wikipedia.org/wiki/Feature_(computer_vision)) para identificação de imagens. Podemos fazer uso desses recursos de imagem interna no modelo para treinar um novo modelo com muito menos classes.

Conforme mostrado no diagrama a seguir, você adiciona uma referência aos pacotes ML.NET NuGet em seus aplicativos .NET Core ou .NET Framework. as capas, ML.NET inclui `TensorFlow` e faz referência à biblioteca nativa que `TensorFlow` permite escrever um código que carrega um arquivo de modelo treinado existente.

![Diagrama de arco da transformação do TensorFlow do ML.NET](./media/image-classification/tensorflow-mlnet.png)

### <a name="multiclass-classification"></a>Classificação multiclasse

Depois de usar o modelo de criação do TensorFlow para extrair recursos adequados como entrada para um algoritmo clássico de aprendizado de máquina, adicionamos um ML.NET [multiclasse .](../resources/tasks.md#multiclass-classification)

O treinador específico utilizado neste caso é o [algoritmo de regressão logística multinomial](https://en.wikipedia.org/wiki/Multinomial_logistic_regression).

O algoritmo implementado por este treinador funciona bem em problemas com um grande número de recursos, o que é o caso de um modelo de aprendizagem profunda operando em dados de imagem.

### <a name="data"></a>Dados

Há duas fontes de dados: o arquivo `.tsv` e os arquivos de imagem.  O arquivo `tags.tsv` contém duas colunas: a primeira é definida como `ImagePath` e a segunda é a `Label` correspondente à imagem. O arquivo de exemplo a seguir não possui uma linha de cabeçalho e tem a seguinte aparência:

<!-- markdownlint-disable MD010 -->
```tsv
broccoli.jpg    food
pizza.jpg   food
pizza2.jpg  food
teddy2.jpg  toy
teddy3.jpg  toy
teddy4.jpg  toy
toaster.jpg appliance
toaster2.png    appliance
```
<!-- markdownlint-enable MD010 -->

As imagens de treinamento e teste estão localizadas nas pastas de recursos que você baixará em um arquivo zip. Essas imagens pertencem ao Wikimedia Commons.
> *[Wikimedia Commons](https://commons.wikimedia.org/w/index.php?title=Main_Page&oldid=313158208), o repositório de mídia gratuito.* Recuperado 10:48, 17 de outubro de https://commons.wikimedia.org/wiki/Pizza https://commons.wikimedia.org/wiki/Toaster 2018 de:https://commons.wikimedia.org/wiki/Teddy_bear

## <a name="setup"></a>Instalação

### <a name="create-a-project"></a>Criar um projeto

1. Criar um **Aplicativo de Console .NET Core** chamado "TransferLearningTF".

1. Instalar o **Pacote NuGet Microsoft.ML**:

    * No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e selecione **Gerenciar Pacotes NuGet**.
    * Escolha "nuget.org" como a fonte do pacote, selecione a guia Browse, procure por **Microsoft.ML**.
    * Clique na **versão** para da dada, selecione o pacote **1.4.0** na lista e selecione o botão **Instalar.**
    * Selecione o botão **OK** na **caixa de diálogo Visualização Alterações.**
    * Selecione o botão **Eu Aceito** na caixa de diálogo **Aceitação de Licença** se você concordar com os termos de licença dos pacotes listados.
    * Repita estas etapas para **Microsoft.ML.ImageAnalytics v1.4.0**, **SciSharp.TensorFlow.Redist v1.15.0** e **Microsoft.ML.TensorFlow v1.4.0**.

### <a name="download-assets"></a>Baixar ativos

1. Baixe [O arquivo zip do diretório de ativos do projeto](https://github.com/dotnet/samples/blob/master/machine-learning/tutorials/TransferLearningTF/image-classifier-assets.zip)e descompacte.

1. Copie o diretório`assets` no diretório do projeto *TransferLearningTF*. Este diretório e seus subdiretórios contêm os arquivos de dados e de suporte (exceto o modelo Concepção, que você irá baixar e adicionar na próxima etapa) necessários para este tutorial.

1. Baixe o [modelo Concepção](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip) e descompacte-o.

1. Copie o conteúdo do diretório `inception5h` apenas descompactado em seu diretório de projeto *TransferLearningTF*`assets/inception`. Este diretório contém o modelo e os arquivos de suporte adicionais necessários para este tutorial, conforme mostrado na imagem a seguir:

   ![Conteúdo do diretório de concepção](./media/image-classification/inception-files.png)

1. No Gerenciador de Soluções, clique com o botão direito do mouse em cada um dos arquivos no diretório e nos subdiretórios do ativo e selecione**Propriedades**. Em **Avançado,** altere o valor de **Copiar para Diretório de Saída** para Copiar se mais **novo**.

### <a name="create-classes-and-define-paths"></a>Criar classes e definir demarcadores

1. Adicione as seguintes instruções `using` adicionais ao início do arquivo *Program.cs*: 

    [!code-csharp[AddUsings](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#AddUsings)]

1. Adicione o seguinte código à `Main` linha logo acima do método para especificar os caminhos do ativo:

    [!code-csharp[DeclareGlobalVariables](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#DeclareGlobalVariables)]

1. Crie classes para seus dados de entrada e previsões.

    [!code-csharp[DeclareImageData](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#DeclareImageData)]

    `ImageData` é a classe de conjunto de dados de entrada e tem os seguintes campos <xref:System.String>:

    * `ImagePath` contém o nome do arquivo de imagem.
    * `Label` contém um valor para o rótulo da imagem.

1. Adicione uma nova classe ao seu projeto para `ImagePrediction`:

    [!code-csharp[DeclareImagePrediction](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#DeclareImagePrediction)]

    `ImagePrediction` é a classe de previsão de imagem e possui os seguintes campos:

    * `Score` contém a porcentagem de confiança para uma determinada classificação de imagem.
    * `PredictedLabelValue` contém um valor para o rótulo de classificação de imagem previsto.

    `ImagePrediction` é a classe usada para previsão depois que o modelo foi treinado. Tem um `string` (`ImagePath`) para o demarcador da imagem. O `Label` é usado para reutilizar e treinar o modelo. O `PredictedLabelValue` é usado durante a previsão e avaliação. Para avaliação, uma entrada com dados de treinamento, os valores previstos e o modelo são usados.

### <a name="initialize-variables-in-main"></a>Inicializar variáveis em Main

1. Inicialize a variável `mlContext` com uma nova instância de `MLContext`.  Substitua a linha `Console.WriteLine("Hello World!")` pelo seguinte código no método `Main`:

    [!code-csharp[CreateMLContext](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#CreateMLContext)]

    A [classe MLContext](xref:Microsoft.ML.MLContext) é um ponto de partida para todas as operações do ML.NET e a inicialização do `mlContext` cria um ambiente do ML.NET que pode ser compartilhado entre os objetos de fluxo de trabalho da criação de modelo. Ele é semelhante, conceitualmente, a `DBContext` no Entity Framework.

### <a name="create-a-struct-for-inception-model-parameters"></a>Criar uma estrutura para parâmetros do modelo Inception

1. O modelo Inception tem vários parâmetros que você precisa passar. Criar uma estrutura para mapear os valores dos parâmetros para `Main()` nomes amigáveis com o seguinte código, logo após o método:

    [!code-csharp[InceptionSettings](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#InceptionSettings)]

### <a name="create-a-display-utility-method"></a>Criar um método de utilitário de exibição

Uma vez que você exibirá os dados de imagem e as previsões relacionadas mais de uma vez, crie um método de utilitário de exibição para lidar com a exibição dos resultados de imagem e previsão.

1. Crie o método `DisplayResults()`, logo após o struct `InceptionSettings`, usando o seguinte código:

    ```csharp
    private static void DisplayResults(IEnumerable<ImagePrediction> imagePredictionData)
    {

    }
    ```

1. Preencha o corpo `DisplayResults` do método:

    [!code-csharp[DisplayPredictions](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#DisplayPredictions)]

### <a name="create-a-tsv-file-utility-method"></a>Criar um método de utilitário de arquivo .tsv

1. Crie o método `ReadFromTsv()`, logo após o método `DisplayResults()`, usando o seguinte código:

    ```csharp
    public static IEnumerable<ImageData> ReadFromTsv(string file, string folder)
    {

    }
    ```

1. Preencha o corpo `ReadFromTsv` do método:

    [!code-csharp[ReadFromTsv](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#ReadFromTsv)]

    O código analisa através `tags.tsv` do arquivo para adicionar o caminho `ImagePath` do arquivo ao `Label` nome `ImageData` do arquivo de imagem para a propriedade e carregá-lo e em um objeto.

### <a name="create-a-method-to-make-a-prediction"></a>Crie um método para fazer uma previsão

1. Crie o método `ClassifySingleImage()`, logo antes do método `DisplayResults()`, usando o seguinte código:

    ```csharp
    public static void ClassifySingleImage(MLContext mlContext, ITransformer model)
    {

    }
    ```

1. Crie `ImageData` um objeto que contenha o caminho e `ImagePath`o nome do arquivo de imagem totalmente qualificados para o single . Adicione o seguinte código como as próximas linhas no método `ClassifySingleImage()`:

    [!code-csharp[LoadImageData](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#LoadImageData)]

1. Faça uma única previsão, adicionando o seguinte `ClassifySingleImage` código como a próxima linha no método:

    [!code-csharp[PredictSingle](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#PredictSingle)]

    Para obter a previsão, use o método [Predict().](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) O [PredictionEngine](xref:Microsoft.ML.PredictionEngine%602) é uma API de conveniência, que permite realizar uma previsão em uma única instância de dados. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)não é seguro para rosca. É aceitável usar em ambientes de um único fio ou protótipo. Para melhorar o desempenho e a segurança `PredictionEnginePool` dos fios nos [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) ambientes de produção, use o serviço, que cria um objeto para uso em toda a sua aplicação. Consulte este guia sobre como [usar `PredictionEnginePool` em uma API web ASP.NET.](../how-to-guides/serve-model-web-api-ml-net.md#register-predictionenginepool-for-use-in-the-application)

    > [!NOTE]
    > A extensão de serviço `PredictionEnginePool` está atualmente em versão prévia.

1. Exiba o resultado da previsão como a próxima linha de código no método `ClassifySingleImage()`:

   [!code-csharp[DisplayPrediction](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#DisplayPrediction)]

## <a name="construct-the-mlnet-model-pipeline"></a>Construa o gasoduto modelo ML.NET

Um ML.NET modelo de gasoduto é uma cadeia de estimadores. Note que nenhuma execução acontece durante a construção do gasoduto. Os objetos estimadores são criados, mas não executados.

1. Adicionar um método para gerar o modelo

    Este método é o coração do tutorial. Ele cria um gasoduto para o modelo, e treina o gasoduto para produzir o modelo ML.NET. Ele também avalia o modelo em relação a alguns dados de teste inéditos.

    Crie o método `GenerateModel()` logo após o struct `InceptionSettings` e antes do método `DisplayResults()`, usando o seguinte código:

    ```csharp
    public static ITransformer GenerateModel(MLContext mlContext)
    {

    }
    ```

1. Adicione os estimadores para carregar, redimensionar e extrair os pixels dos dados da imagem:

    [!code-csharp[ImageTransforms](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#ImageTransforms)]

    Os dados de imagem precisam ser processados no formato que o modelo TensorFlow espera. Neste caso, as imagens são carregadas na memória, redimensionadas para um tamanho consistente, e os pixels são extraídos em um vetor numérico.

1. Adicione o estimador para carregar o modelo TensorFlow e marque-o:

    [!code-csharp[ScoreTensorFlowModel](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#ScoreTensorFlowModel)]

    Esta etapa no pipeline carrega o modelo TensorFlow na memória e processa o vetor de valores de pixel através da rede do modelo TensorFlow. Aplicar entradas a um modelo de aprendizagem profunda e gerar uma saída usando o modelo é chamado **de Pontuação**. Ao usar o modelo em sua totalidade, a pontuação faz uma inferência, ou previsão.

    Neste caso, você usa todo o modelo TensorFlow, exceto a última camada, que é a camada que faz a inferência. A saída da penúltima camada `softmax_2_preactivation`é rotulada . A saída desta camada é efetivamente um vetor de recursos que caracterizam as imagens de entrada originais.

    Este vetor de recurso gerado pelo modelo TensorFlow será usado como entrada para um algoritmo de treinamento ML.NET.

1. Adicione o estimador para mapear os rótulos de seqüência nos dados de treinamento para inteiros valores-chave:

    [!code-csharp[MapValueToKey](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#MapValueToKey)]

    O ML.NET treinador que é anexado em `key` seguida requer que seus rótulos estejam em formato e não em cordas arbitrárias. Uma chave é um número que tem um mapeamento de um para um para um valor de seqüência.

1. Adicione o algoritmo de treinamento ML.NET:

    [!code-csharp[AddTrainer](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#AddTrainer)]

1. Adicione o estimador para mapear o valor-chave previsto de volta em uma seqüência:

    [!code-csharp[MapKeyToValue](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#MapKeyToValue)]

## <a name="train-the-model"></a>Treinar o modelo

1. Carregue os dados de treinamento usando o invólucro [LoadFromTextFile.](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile(Microsoft.ML.DataOperationsCatalog,System.String,Microsoft.ML.Data.TextLoader.Options)) Adicione o seguinte código ao método `GenerateModel()` como a linha seguinte:

    [!code-csharp[LoadData](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#LoadData "Load the data")]

    Os dados do ML.NET são representados como uma [classe IDataView](xref:Microsoft.ML.IDataView). `IDataView` é uma maneira flexível e eficiente de descrever dados tabulares (numéricos e texto). Os dados podem ser carregados de um arquivo de texto ou em tempo real (por exemplo, banco de dados SQL ou arquivos de log) para um objeto `IDataView`.

1. Treine o modelo com os dados carregados acima:

    [!code-csharp[TrainModel](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#TrainModel)]

    O `Fit()` método treina seu modelo aplicando o conjunto de dados de treinamento ao pipeline.

## <a name="evaluate-the-accuracy-of-the-model"></a>Avalie a precisão do modelo

1. Carregar e transformar os dados do teste, adicionando `GenerateModel` o seguinte código à próxima linha do método:

    [!code-csharp[LoadAndTransformTestData](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#LoadAndTransformTestData "Load and transform test data")]

    Existem algumas imagens de exemplo que você pode usar para avaliar o modelo. Como os dados de treinamento, estes `IDataView`precisam ser carregados em um , para que possam ser transformados pelo modelo.

1. Adicione o seguinte `GenerateModel()` código ao método para avaliar o modelo:

    [!code-csharp[Evaluate](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#Evaluate)]

    Depois de determinar a previsão, o método [Evaluate ()](xref:Microsoft.ML.RecommendationCatalog.Evaluate%2A):

    * Avalia o modelo (compara os valores previstos com o conjunto `labels`de dados do teste ).
    * Retorna as métricas de desempenho do modelo.

1. Exibir as métricas de precisão do modelo

    Use o código a seguir para exibir as métricas, compartilhar os resultados e, em seguida, agir com relação a eles:

    [!code-csharp[DisplayMetrics](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#DisplayMetrics)]

    As seguintes métricas são avaliadas para classificação de imagem:

    * `Log-loss` - confira [Perda de log](../resources/glossary.md#log-loss). Convém que a Perda de log seja tão próxima de zero quanto possível.
    * `Per class Log-loss`. Convém que a Perda de log por classe seja tão próxima de zero quanto possível.

1. Adicione o seguinte código para retornar o modelo treinado como a próxima linha:

    [!code-csharp[SaveModel](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#ReturnModel)]

## <a name="run-the-application"></a>Execute o aplicativo!

1. Adicionar a `GenerateModel` chamada `Main` no método após a criação da classe MLContext:

    [!code-csharp[CallGenerateModel](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#CallGenerateModel)]

1. Adicione a chamada `ClassifySingleImage()` ao método como a `Main` próxima linha de código no método:

    [!code-csharp[CallClassifySingleImage](../../../samples/snippets/machine-learning/TransferLearningTF/csharp/Program.cs#CallClassifySingleImage)]

1. Execute seu aplicativo de console (Ctrl + F5). O resultado deverá ser semelhante à seguinte saída.  Você poderá ver avisos ou mensagens de processamento, mas essas mensagens foram removidas dos resultados a seguir para maior clareza.

    ```console
    =============== Training classification model ===============
    Image: broccoli2.jpg predicted as: food with score: 0.8955513
    Image: pizza3.jpg predicted as: food with score: 0.9667718
    Image: teddy6.jpg predicted as: toy with score: 0.9797683
    =============== Classification metrics ===============
    LogLoss is: 0.0653774699265059
    PerClassLogLoss is: 0.110315812569315 , 0.0204391272836966 , 0
    =============== Making single image classification ===============
    Image: toaster3.jpg predicted as: appliance with score: 0.9646884
    ```

Parabéns! Agora você construiu com sucesso um modelo de aprendizado de `TensorFlow` máquina para classificação de imagem aplicando o aprendizado de transferência para um modelo em ML.NET.

Você pode encontrar o código-fonte para este tutorial no repositório [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF).

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
>
> * Compreender o problema
> * Incorpore o modelo TensorFlow pré-treinado no pipeline ML.NET
> * Treine e avalie o modelo ML.NET
> * Classificar uma imagem de teste

Conferir o repositório GitHub de Amostras de Aprendizado de Máquina para explorar uma amostra de classificação de imagem expandida.
> [!div class="nextstepaction"]
> [dotnet/machinelearning-samples GitHub repository](https://github.com/dotnet/machinelearning-samples/)
