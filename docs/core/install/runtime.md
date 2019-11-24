---
title: Install .NET Core runtime on Windows, Linux, and macOS - .NET Core
description: Learn how to install .NET Core on Windows, Linux, and macOS. Discover the dependencies required to run .NET Core apps.
author: thraka
ms.author: adegeo
ms.date: 11/06/2019
ms.custom: updateeachrelease
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: 395978a2e471260254caf3da8421adf2413c132c
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74450852"
---
# <a name="install-the-net-core-runtime"></a><span data-ttu-id="4db18-104">Install the .NET Core Runtime</span><span class="sxs-lookup"><span data-stu-id="4db18-104">Install the .NET Core Runtime</span></span>

<span data-ttu-id="4db18-105">In this article, you'll learn how to download and install the .NET Core runtime.</span><span class="sxs-lookup"><span data-stu-id="4db18-105">In this article, you'll learn how to download and install the .NET Core runtime.</span></span> <span data-ttu-id="4db18-106">The .NET Core runtime is used to run apps created with .NET Core.</span><span class="sxs-lookup"><span data-stu-id="4db18-106">The .NET Core runtime is used to run apps created with .NET Core.</span></span>

<span data-ttu-id="4db18-107">You can download and install .NET Core directly with one of the following links:</span><span class="sxs-lookup"><span data-stu-id="4db18-107">You can download and install .NET Core directly with one of the following links:</span></span>

- [<span data-ttu-id="4db18-108">.NET Core 3.1 Preview 3 downloads</span><span class="sxs-lookup"><span data-stu-id="4db18-108">.NET Core 3.1 Preview 3 downloads</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [<span data-ttu-id="4db18-109">.NET Core 3.0 downloads</span><span class="sxs-lookup"><span data-stu-id="4db18-109">.NET Core 3.0 downloads</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0)
- [<span data-ttu-id="4db18-110">.NET Core 2.2 downloads</span><span class="sxs-lookup"><span data-stu-id="4db18-110">.NET Core 2.2 downloads</span></span>](https://dotnet.microsoft.com/download/dotnet-core/2.2)
- [<span data-ttu-id="4db18-111">.NET Core 2.1 downloads</span><span class="sxs-lookup"><span data-stu-id="4db18-111">.NET Core 2.1 downloads</span></span>](https://dotnet.microsoft.com/download/dotnet-core/2.1)

## <a name="install-with-an-installer"></a><span data-ttu-id="4db18-112">Install with an installer</span><span class="sxs-lookup"><span data-stu-id="4db18-112">Install with an installer</span></span>

<span data-ttu-id="4db18-113">Both Windows and macOS have standalone installers that can be used to install the .NET Core 3.0 runtime.</span><span class="sxs-lookup"><span data-stu-id="4db18-113">Both Windows and macOS have standalone installers that can be used to install the .NET Core 3.0 runtime.</span></span>

- <span data-ttu-id="4db18-114">Windows [x64 CPUs](https://dotnet.microsoft.com/download/thank-you/dotnet-runtime-3.0.0-windows-x64-installer) | [x32 CPUs](https://dotnet.microsoft.com/download/thank-you/dotnet-runtime-3.0.0-windows-x86-installer)</span><span class="sxs-lookup"><span data-stu-id="4db18-114">Windows [x64 CPUs](https://dotnet.microsoft.com/download/thank-you/dotnet-runtime-3.0.0-windows-x64-installer) | [x32 CPUs](https://dotnet.microsoft.com/download/thank-you/dotnet-runtime-3.0.0-windows-x86-installer)</span></span>
- <span data-ttu-id="4db18-115">macOS [x64 CPUs](https://dotnet.microsoft.com/download/thank-you/dotnet-runtime-3.0.0-macos-x64-installer)</span><span class="sxs-lookup"><span data-stu-id="4db18-115">macOS [x64 CPUs](https://dotnet.microsoft.com/download/thank-you/dotnet-runtime-3.0.0-macos-x64-installer)</span></span>

::: zone pivot="os-linux"

## <a name="install-with-a-package-manager"></a><span data-ttu-id="4db18-116">Install with a package manager</span><span class="sxs-lookup"><span data-stu-id="4db18-116">Install with a package manager</span></span>

<span data-ttu-id="4db18-117">You can install the .NET Core Runtime with many of the common Linux package managers.</span><span class="sxs-lookup"><span data-stu-id="4db18-117">You can install the .NET Core Runtime with many of the common Linux package managers.</span></span> <span data-ttu-id="4db18-118">For more information, see [Linux Package Manager - Install .NET Core](linux-package-manager-rhel7.md).</span><span class="sxs-lookup"><span data-stu-id="4db18-118">For more information, see [Linux Package Manager - Install .NET Core](linux-package-manager-rhel7.md).</span></span>

::: zone-end

::: zone pivot="os-windows"

## <a name="install-with-powershell-automation"></a><span data-ttu-id="4db18-119">Install with PowerShell automation</span><span class="sxs-lookup"><span data-stu-id="4db18-119">Install with PowerShell automation</span></span>

<span data-ttu-id="4db18-120">The [dotnet-install scripts](../tools/dotnet-install-script.md) are used for automation and non-admin installs of the runtime.</span><span class="sxs-lookup"><span data-stu-id="4db18-120">The [dotnet-install scripts](../tools/dotnet-install-script.md) are used for automation and non-admin installs of the runtime.</span></span> <span data-ttu-id="4db18-121">You can download the script from the [dotnet-install script reference page](../tools/dotnet-install-script.md).</span><span class="sxs-lookup"><span data-stu-id="4db18-121">You can download the script from the [dotnet-install script reference page](../tools/dotnet-install-script.md).</span></span>

<span data-ttu-id="4db18-122">The script defaults to installing the latest [long term support (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) version, which is .NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="4db18-122">The script defaults to installing the latest [long term support (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) version, which is .NET Core 2.1.</span></span> <span data-ttu-id="4db18-123">To install the current release of .NET Core (3.0), run the script with the following switch:</span><span class="sxs-lookup"><span data-stu-id="4db18-123">To install the current release of .NET Core (3.0), run the script with the following switch:</span></span>

```powershell
dotnet-install.ps1 -Channel 3.0
```

::: zone-end

::: zone pivot="os-linux,os-macos"

## <a name="install-with-bash-automation"></a><span data-ttu-id="4db18-124">Install with bash automation</span><span class="sxs-lookup"><span data-stu-id="4db18-124">Install with bash automation</span></span>

<span data-ttu-id="4db18-125">The [dotnet-install scripts](../tools/dotnet-install-script.md) are used for automation and non-admin installs of the runtime.</span><span class="sxs-lookup"><span data-stu-id="4db18-125">The [dotnet-install scripts](../tools/dotnet-install-script.md) are used for automation and non-admin installs of the runtime.</span></span> <span data-ttu-id="4db18-126">You can download the script from the [dotnet-install script reference page](../tools/dotnet-install-script.md).</span><span class="sxs-lookup"><span data-stu-id="4db18-126">You can download the script from the [dotnet-install script reference page](../tools/dotnet-install-script.md).</span></span>

<span data-ttu-id="4db18-127">The script defaults to installing the latest [long term support (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) version, which is .NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="4db18-127">The script defaults to installing the latest [long term support (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) version, which is .NET Core 2.1.</span></span> <span data-ttu-id="4db18-128">To install the current release of .NET Core (3.0), run the script with the following switch:</span><span class="sxs-lookup"><span data-stu-id="4db18-128">To install the current release of .NET Core (3.0), run the script with the following switch:</span></span>

```bash
./dotnet-install.sh -c Current
```

::: zone-end

## <a name="docker"></a><span data-ttu-id="4db18-129">Docker</span><span class="sxs-lookup"><span data-stu-id="4db18-129">Docker</span></span>

<span data-ttu-id="4db18-130">Containers provide a lightweight way to isolate your application from the rest of the host system.</span><span class="sxs-lookup"><span data-stu-id="4db18-130">Containers provide a lightweight way to isolate your application from the rest of the host system.</span></span> <span data-ttu-id="4db18-131">Containers on the same machine share just the kernel and use resources given to your application.</span><span class="sxs-lookup"><span data-stu-id="4db18-131">Containers on the same machine share just the kernel and use resources given to your application.</span></span>

<span data-ttu-id="4db18-132">.NET Core can run in a Docker container.</span><span class="sxs-lookup"><span data-stu-id="4db18-132">.NET Core can run in a Docker container.</span></span> <span data-ttu-id="4db18-133">As imagens oficiais do Docker do .NET Core são publicadas no MCR (Registro de Contêiner da Microsoft) e podem ser encontradas no [repositório do Hub do Docker do .NET Core da Microsoft](https://hub.docker.com/_/microsoft-dotnet-core/).</span><span class="sxs-lookup"><span data-stu-id="4db18-133">Official .NET Core Docker images are published to the Microsoft Container Registry (MCR) and are discoverable at the [Microsoft .NET Core Docker Hub repository](https://hub.docker.com/_/microsoft-dotnet-core/).</span></span> <span data-ttu-id="4db18-134">Cada repositório contém imagens para diferentes combinações do .NET (SDK ou Runtime) e do sistema operacional que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="4db18-134">Each repository contains images for different combinations of the .NET (SDK or Runtime) and OS that you can use.</span></span>

<span data-ttu-id="4db18-135">A Microsoft fornece imagens personalizadas para cenários específicos.</span><span class="sxs-lookup"><span data-stu-id="4db18-135">Microsoft provides images that are tailored for specific scenarios.</span></span> <span data-ttu-id="4db18-136">Por exemplo, o [repositório do ASP.NET Core](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) fornece imagens que são criadas para a execução de aplicativos ASP.NET Core na produção.</span><span class="sxs-lookup"><span data-stu-id="4db18-136">For example, the [ASP.NET Core repository](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) provides images that are built for running ASP.NET Core apps in production.</span></span>

<span data-ttu-id="4db18-137">For more information about using .NET Core in a Docker container, see [Introduction to .NET and Docker](../docker/introduction.md) and [Samples](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md).</span><span class="sxs-lookup"><span data-stu-id="4db18-137">For more information about using .NET Core in a Docker container, see [Introduction to .NET and Docker](../docker/introduction.md) and [Samples](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4db18-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4db18-138">Next steps</span></span>

- <span data-ttu-id="4db18-139">[How to check if .NET Core is already installed](how-to-detect-installed-versions.md).</span><span class="sxs-lookup"><span data-stu-id="4db18-139">[How to check if .NET Core is already installed](how-to-detect-installed-versions.md).</span></span>