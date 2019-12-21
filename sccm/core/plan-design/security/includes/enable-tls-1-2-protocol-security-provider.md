---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: b8d47aefee9ab47fa777dd648548ae45780e8f16
ms.sourcegitcommit: 3a0eaf3378632f312b46b2b8a524e286f9c4cd8e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75198905"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 è abilitato per impostazione predefinita, quindi non è necessario apportare modifiche a queste chiavi per abilitarlo. È possibile apportare modifiche in `Protocols` per disabilitare TLS 1.0 e TLS 1.1 dopo aver seguito il resto delle indicazioni fornite in questi articoli e aver verificato che l'ambiente funzioni quando è abilitato solo TLS 1.2.

Verificare l'impostazione della sottochiave del Registro di sistema `\SecurityProviders\SCHANNEL\Protocols`, come illustrato in [Procedure consigliate per Transport Layer Security (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

