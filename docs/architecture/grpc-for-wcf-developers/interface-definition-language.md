---
title: Linguagem de definição de interface-gRPC para desenvolvedores do WCF
description: Apresentando os buffers de protocolo IDL.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 71bdf8bf488e0a5bed177817343051bcd7847d25
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184424"
---
# <a name="interface-definition-language"></a><span data-ttu-id="f025c-103">Linguagem de definição de interface</span><span class="sxs-lookup"><span data-stu-id="f025c-103">Interface Definition Language</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="f025c-104">Com o WCF, os serviços podem expor metadados de descrição usando o WSDL (Web Service Definition Language), que é gerado dinamicamente usando a reflexão do .NET em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="f025c-104">With WCF, services can expose description metadata using the Web Service Definition Language (WSDL), which is generated dynamically using .NET Reflection at runtime.</span></span> <span data-ttu-id="f025c-105">Os desenvolvedores podem usar esses metadados para gerar clientes para esses serviços, potencialmente em outras linguagens se uma associação de plataforma neutra, como SOAP sobre HTTP, for usada.</span><span class="sxs-lookup"><span data-stu-id="f025c-105">Developers can use this metadata to generate clients for those services, potentially in other languages if a platform-neutral binding such as SOAP over HTTP is used.</span></span>

<span data-ttu-id="f025c-106">gRPC usa o IDL (Interface Definition Language) dos buffers de protocolo.</span><span class="sxs-lookup"><span data-stu-id="f025c-106">gRPC uses the Interface Definition Language (IDL) from Protocol Buffers.</span></span> <span data-ttu-id="f025c-107">Os buffers de protocolo IDL são uma linguagem personalizada de plataforma neutra com uma especificação aberta.</span><span class="sxs-lookup"><span data-stu-id="f025c-107">The Protocol Buffers IDL is a custom, platform-neutral language with an open specification.</span></span> <span data-ttu-id="f025c-108">Os desenvolvedores codificam `.proto` arquivos para descrever serviços junto com suas entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="f025c-108">Developers hand-code `.proto` files to describe services along with their inputs and outputs.</span></span> <span data-ttu-id="f025c-109">Esses `.proto` arquivos podem então ser usados para gerar stubs específicos de idioma ou de plataforma para clientes e servidores, permitindo que várias plataformas diferentes se comuniquem.</span><span class="sxs-lookup"><span data-stu-id="f025c-109">These `.proto` files can then be used to generate language- or platform-specific stubs for clients and servers, allowing multiple different platforms to communicate.</span></span> <span data-ttu-id="f025c-110">Ao compartilhar `.proto` arquivos, as equipes podem gerar código para usar os serviços de cada um sem precisar usar uma dependência de código.</span><span class="sxs-lookup"><span data-stu-id="f025c-110">By sharing `.proto` files, teams can generate code to use each others' services without needing to take a code dependency.</span></span>

<span data-ttu-id="f025c-111">Uma das vantagens da Protobuf IDL é que, como uma linguagem personalizada, ela permite que o gRPC seja completamente independente de linguagem e plataforma, não favorecendo nenhuma tecnologia sobre outra.</span><span class="sxs-lookup"><span data-stu-id="f025c-111">One of the advantages of the Protobuf IDL is that as a custom language it enables gRPC to be completely language and platform agnostic, not favoring any technology over another.</span></span>

<span data-ttu-id="f025c-112">O Protobuf IDL também é projetado para os seres humanos para leitura e gravação, enquanto o WSDL é destinado a um formato legível por máquina/gravável.</span><span class="sxs-lookup"><span data-stu-id="f025c-112">The Protobuf IDL is also designed for humans to both read and write, whereas WSDL is intended as a machine-readable/writable format.</span></span> <span data-ttu-id="f025c-113">A alteração do WSDL de um serviço WCF normalmente requer a realização das alterações no próprio código do serviço, na execução do serviço e na regeneração do arquivo WSDL a partir do servidor.</span><span class="sxs-lookup"><span data-stu-id="f025c-113">Changing the WSDL of a WCF service typically requires making the changes to the service code itself, running the service and regenerating the WSDL file from the server.</span></span> <span data-ttu-id="f025c-114">Por outro lado, com `.proto` um arquivo, as alterações são simples de se aplicar a um editor de texto e fluir automaticamente pelo código gerado.</span><span class="sxs-lookup"><span data-stu-id="f025c-114">By contrast, with a `.proto` file, changes are simple to apply with a text editor, and automatically flow through the generated code.</span></span> <span data-ttu-id="f025c-115">O Visual Studio 2019 `.proto` compila arquivos em segundo plano quando eles são salvos; ao usar outros editores, como vs Code as alterações serão aplicadas quando o projeto for compilado.</span><span class="sxs-lookup"><span data-stu-id="f025c-115">Visual Studio 2019 builds `.proto` files in the background when they are saved; when using other editors such as VS Code the changes will be applied when the project is built.</span></span>

<span data-ttu-id="f025c-116">Quando comparado com XML e particularmente SOAP, mensagens codificadas usando Protobuf têm muitas vantagens.</span><span class="sxs-lookup"><span data-stu-id="f025c-116">When compared with XML, and particularly SOAP, messages encoded using Protobuf have many advantages.</span></span> <span data-ttu-id="f025c-117">As mensagens Protobuf tendem a ser menores do que os mesmos dados serializados como XML SOAP, e codificar, decodificá-los e transmiti-los por meio de uma rede podem ser mais rápidos.</span><span class="sxs-lookup"><span data-stu-id="f025c-117">Protobuf messages tend to be smaller than the same data serialized as SOAP XML, and encoding, decoding and transmitting them over a network can be faster.</span></span>

<span data-ttu-id="f025c-118">A desvantagem potencial do Protobuf em comparação com o SOAP é que, como as mensagens não são legíveis, ferramentas adicionais são necessárias para depurar o conteúdo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="f025c-118">The potential disadvantage of Protobuf compared to SOAP is that, because the messages are not human readable, additional tooling is required to debug message content.</span></span>

> [!TIP]
> <span data-ttu-id="f025c-119">*o* gRPC oferece suporte à reflexão de servidor para acessar serviços dinamicamente sem stubs pré-compilados, embora ele seja mais destinado a ferramentas de finalidade geral do que clientes específicos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f025c-119">gRPC *does* support server reflection for dynamically accessing services without pre-compiled stubs, although it is intended more for general-purpose tools than application-specific clients.</span></span> <span data-ttu-id="f025c-120">Para obter mais informações sobre a reflexão do gRPC Server, consulte repositório [gRPC/gRPC](https://github.com/grpc/grpc/blob/master/doc/server-reflection.md) no github.</span><span class="sxs-lookup"><span data-stu-id="f025c-120">For more information about gRPC Server Reflection, see [grpc/grpc](https://github.com/grpc/grpc/blob/master/doc/server-reflection.md) repository on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="f025c-121">O formato binário do WCF, usado com a associação NetTCP, é muito mais próximo de Protobuf em termos de compactação e desempenho, mas NetTCP só é utilizável entre clientes e servidores .NET, enquanto o Protobuf é uma solução de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="f025c-121">WCF's binary format, used with the NetTCP binding, is much closer to Protobuf in terms of compactness and performance, but NetTCP is only usable between .NET clients and servers, whereas Protobuf is a cross-platform solution.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="f025c-122">[Anterior](approach.md)
>[Próximo](network-protocols.md)</span><span class="sxs-lookup"><span data-stu-id="f025c-122">[Previous](approach.md)
[Next](network-protocols.md)</span></span>