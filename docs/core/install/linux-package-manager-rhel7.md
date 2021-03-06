---
title: Instalace .NET Core na Linux RHEL 7 správce balíčků - .NET Core
description: Pomocí správce balíčků nainstalujte sadu .NET Core SDK a runtime na RHEL 7.
author: thraka
ms.author: adegeo
ms.date: 03/17/2020
ms.openlocfilehash: d1f1372b32c7b2471a96492d48aab5533dadb64a
ms.sourcegitcommit: 07123a475af89b6da5bb6cc51ea40ab1e8a488f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80134204"
---
# <a name="rhel-7-package-manager---install-net-core"></a>Správce balíčků RHEL 7 – instalace jádra rozhraní .NET

[!INCLUDE [package-manager-switcher](includes/package-manager-switcher.md)]

Tento článek popisuje, jak pomocí správce balíčků nainstalovat .NET Core na RHEL 7.

[!INCLUDE [package-manager-intro-sdk-vs-runtime](includes/package-manager-intro-sdk-vs-runtime.md)]

## <a name="register-your-red-hat-subscription"></a>Registrace předplatného Red Hatu

Chcete-li nainstalovat .NET Core z Red Hat na RHEL, musíte se nejprve zaregistrovat pomocí Správce předplatného Red Hat. Pokud se tak v systému nestalo nebo si nejste jisti, přečtěte si [dokumentaci k produktu Red Hat pro .NET Core](https://access.redhat.com/documentation/net_core/).

## <a name="install-the-net-core-sdk"></a>Nainstalujte sadu .NET Core SDK.

Po registraci ve Správci předplatného jste připraveni k instalaci a povolení sady .NET Core SDK. V terminálu spusťte následující příkazy, abyste povolili dotnetový kanál RHEL 7 a nainstalovali.

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31 -y
scl enable rh-dotnet31 bash
```

## <a name="install-the-aspnet-core-runtime"></a>Instalace ASP.NET Core Runtime

Po registraci u Správce předplatného jste připraveni nainstalovat a povolit ASP.NET Core Runtime. V terminálu spusťte následující příkazy.

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-aspnetcore-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

## <a name="install-the-net-core-runtime"></a>Instalace rozhraní .NET Core Runtime

Po registraci ve Správci předplatného jste připraveni k instalaci a povolení rozhraní .NET Core Runtime. V terminálu spusťte následující příkazy.

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-dotnet-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

## <a name="see-also"></a>Viz také

- [Použití rozhraní .NET Core 3.1 na Red Hat Enterprise Linux 7](https://access.redhat.com/documentation/en-us/net_core/3.1/html/getting_started_guide/gs_install_dotnet)
