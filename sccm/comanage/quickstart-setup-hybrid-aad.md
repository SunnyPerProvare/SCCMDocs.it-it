---
title: Configurare Azure AD ibrido
titleSuffix: Configuration Manager
description: Se nell'ambiente è attualmente i dispositivi Windows 10 aggiunti a un dominio, configurare identità ibrida di Azure AD prima di abilitare la co-gestione
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec02f740485d3f8b466cde0a644aaaa8885b91f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755212"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configurare ibrida di Azure AD per la co-gestione

Se si dispone di dispositivi Windows 10 aggiunti ad Active Directory in locale, prima di abilitare la co-gestione in Configuration Manager, aggiungere prima di tutto tali dispositivi ad Azure Active Directory (Azure AD). Questo processo è denominato aggiunta ad Azure AD ibrido. 

Nel video seguente, senior program manager Sandeep Deo e product marketing manager Adam Harbour discutere e demo di configurazione dei dispositivi in Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

Ibrida di Azure AD-processo di aggiunta automaticamente registri i dispositivi aggiunti a un dominio locale con Azure AD. Per altre informazioni su questo processo, vedere gli articoli seguenti:
- [Introduzione alla gestione dei dispositivi in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Come pianificare l'aggiunta ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

Aggiunta ad Azure AD ibrido è uno dei principali concetti fondamentali per la co-gestione. Questo processo può essere difficile per alcuni clienti, ad esempio:
- L'organizzazione Usa una soluzione di identità di terze parti 
- Le complessità della configurazione di Active Directory Federation Services (ADFS)

Risoluzione di questi problemi può richiedere alcune indicazioni. Questo articolo aiuta a ridurre i ritardi.


## <a name="how-to-do-it"></a>Come eseguire questa operazione

I dispositivi sono simili agli utenti quando si crea un'identità che si desidera proteggere. Per proteggere l'identità del dispositivo in qualsiasi momento e in qualsiasi posizione, è necessario portare l'identità del dispositivo in Azure AD.

In base al tipo di dominio in uso, esistono due modi principali per eseguire questa operazione. Configurare aggiunta ad Azure AD ibrido per uno dei seguenti tipi di dominio:  
- [Domini federati](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Domini gestiti](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

I due metodi precedenti forniscono un'esperienza ottimale. Per informazioni più dettagliate, tra cui il processo completamente manuale, vedere gli articoli seguenti:
- [Configurare manualmente i dispositivi aggiunti ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [Autenticazione pass-through di ad FS per Azure AD ibrida](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), che include l'individuazione di Azure AD  

Per risolvere il problema materiale sussidiario, vedere la [join di Windows 10 ad Azure AD ibrido Guida alla risoluzione dei](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Case study

Una società di software European grandi dimensioni con più di 100.000 utenti nella propria rete ha richiesto un approccio granulare e in più fasi per l'abilitazione di aggiunta ad Azure AD ibrido.

Durante la fase di pianificazione, poiché l'aggiunta ad Azure AD ibrido è un elemento fondamentale che supportano la co-gestione, gli amministratori di Configuration Manager ha lavorato con il team di identità. La società di software ha molte regole di ad FS e alcuni di essi sono stati complessi. Per risolvere questo problema, il team di identità ha esaminato le regole di ad FS esistente prima attivati aggiunta ad Azure AD ibrido. Il team IT ha anche scelto di aggiornare Azure AD Connect alla versione più recente. Azure AD Connect offre ora un flusso di processo automatizzato per l'abilitazione di aggiunta ad Azure AD ibrido.

Dopo il completamento della distribuzione e test nel proprio ambiente di pre-produzione, questo cliente abilitato aggiunta ad Azure AD ibrido per l'estate intero ambiente di produzione. All'interno di una settimana, che avevano tutti i dispositivi Windows 10 CO-gestiti.



## <a name="contact-fasttrack"></a>Contattare FastTrack

Se è necessario all'impostazione di Azure AD in qualsiasi punto del processo, andare al [Microsoft FastTrack](https://Microsoft.com/FastTrack/), accedi e richiedere assistenza. 

Per altre informazioni, vedere [assistenza dal FastTrack](/sccm/comanage/quickstart-fasttrack). 

