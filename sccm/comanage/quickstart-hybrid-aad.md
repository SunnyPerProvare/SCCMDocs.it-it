---
title: Usare Azure AD per la co-gestione
titleSuffix: Configuration Manager
description: Con Azure AD si possono sfruttare i vantaggi di produttività migliorate per utenti e sicurezza per le risorse, per gli ambienti cloud e locali
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b773c0bfe8cd0f8253a67ac96f5a0113b7206c0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755410"
---
# <a name="use-azure-ad-for-co-management"></a>Usare Azure AD per la co-gestione

Nel cloud, l'identità è il nuovo piano di controllo. Azure Active Directory (Azure AD) consente il collegamento di utenti, dispositivi e applicazioni tra ambienti cloud e locali. Registrazione dei dispositivi ad Azure AD consente di migliorare la produttività per gli utenti e sicurezza per le risorse. La presenza di dispositivi in Azure AD è la base per la co-gestione e l'accesso condizionale basato su dispositivo. 

Per altre informazioni sull'accesso condizionale basato su dispositivo, vedere [How To: Richiedi che i dispositivi gestiti per accedere all'app cloud con l'accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

Nel video seguente, manager senior program Sandeep Deo e product marketing manager Adam Harbour discutere e demo di Azure AD per la co-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD fornisce due opzioni per i dispositivi aziendali in base alle esigenze dell'organizzazione:  

- **Dispositivi aggiunti ad AD Azure**: Aggiungere i dispositivi Windows 10 ad Azure AD senza la necessità per unirle in join ad Active Directory locale  

    - Supporta Windows 10

    - Configurare senza richiedere alcuna configurazione aggiuntiva per gli ambienti locali  

    - Abilitando alcune impostazioni di Azure AD, è possibile abilitare gli utenti ad aggiungere dispositivi ad Azure AD tramite l'esperienza di installazione di Windows (OOBE)  

    - Per altre informazioni, vedere [Procedura: Pianificare l'implementazione di join Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Ibrida dispositivi aggiunti ad AD Azure**: Aggiungere i dispositivi aggiunti a un dominio esistenti ad Azure AD  

    - Supporta Windows 10, Windows 8.1 e Windows 7

    - Configurare con le attestazioni di AD FS o Azure AD Connect  

    - Per Windows 10 il join venga eseguito nel contesto del computer, in modo che gli utenti non dovranno eseguire passaggi aggiuntivi  

    - Per altre informazioni, vedere [come pianificare l'implementazione di join di Azure Active Directory ibrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

Entrambe le opzioni offrono funzionalità simili per gli utenti. È flessibile che consente di scegliere uno in base alle esigenze. Ad esempio, è possibile [accedere alle risorse locali](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) dalle macchine aggiunti ad AD Azure anche se essi non sono aggiunti ad Active Directory. 

È possibile aggiungere dispositivi ad Azure AD in diversi ambienti, non importa il [metodo di autenticazione](https://docs.microsoft.com/azure/security/azure-ad-choose-authn). Ad esempio, l'autenticazione federata o l'autenticazione cloud. 

Se si dispone già di un server di Active Directory in locale, impostazione di una delle due opzioni è semplice. 



## <a name="benefits"></a>Vantaggi

Aggiunta dei dispositivi ad Azure AD offre i vantaggi seguenti per l'organizzazione:

#### <a name="single-sign-on-to-cloud-resources"></a>Single sign-on alle risorse cloud
Nei dispositivi aggiunti ad Azure AD, otterrai un'esperienza integrata l'accesso alle risorse cloud o in locale. Dopo l'accesso a un computer Windows che viene aggiunto ad Azure AD, otterrai single sign-on a tutte le applicazioni senza alcuna richiesta di accesso aggiuntivi.  

#### <a name="windows-hello-for-business"></a>Windows Hello for Business
Windows Hello for Business offre autenticazione avanzata senza password per Windows 10. Unendo in join i dispositivi ad Azure AD, è possibile abilitare Windows Hello for Business in base per le risorse sia cloud sia in locale di utenti. Windows Hello for Business consente di eliminare il problema di ricordare le password complesse o esporli inavvertitamente. Il processo di accesso è semplice e sicuro. 

Per altre informazioni, vedere [Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

#### <a name="device-based-conditional-access"></a>Accesso condizionale basato su dispositivo
Abilitare l'accesso condizionale basato sullo stato del dispositivo per proteggere meglio i dati dell'organizzazione. Accesso condizionale basato su dispositivo richiede un dispositivo gestito. Questo dispositivo deve essere un dispositivo conforme o una combinazione di dispositivi aggiunti ad AD Azure. Per i dispositivi aggiunti ad AD di Azure, è necessario per contrassegnare il dispositivo come compatibile con Intune. Ma per la gestione ibrida Azure dispositivi aggiunti ad AD, lo stato del dispositivo stesso viene utilizzato per valutare l'accesso condizionale. CO-gestione offre l'ulteriore vantaggio della valutazione della conformità tramite Intune per ibrida di Azure per i dispositivi aggiunti ad AD. Questa funzionalità garantisce che la configurazione del dispositivo sia intatta. 

Per altre informazioni sull'accesso condizionale basato su dispositivo, vedere [How To: Richiedi che i dispositivi gestiti per accedere all'app cloud con l'accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

#### <a name="automatic-device-licensing"></a>Gestione delle licenze automatica dei dispositivi
Tutti i dispositivi Windows 10 aggiunti ad Azure AD passano attraverso controlli di licenza. Questi controlli consentono di aggiornare automaticamente tali da Pro a Enterprise tramite il cloud Microsoft. Quando si rimuove la sottoscrizione da usare da parte dell'utente, dispositivo riduce automaticamente la licenza. Questa funzionalità fornisce un unico riquadro di controllo per la gestione delle licenze di Windows, senza eventuali processi complessi o sistemi locali.

#### <a name="self-service-functionality"></a>Funzionalità self-service
Funzionalità self-service include la reimpostazione della password self-service e chiave di ripristino di BitLocker. Azure AD offre più dirette opzioni per reimpostare la password o accedere alle chiavi di ripristino di BitLocker. È possibile usare Azure AD per reimpostare la password direttamente dalla schermata di blocco di Windows, anziché da un web browser. Queste funzionalità ridurre gli attriti per gli utenti e consentono di ridurre i costi del supporto tecnico per l'organizzazione.  

Per altre informazioni, vedere [Guida introduttiva: Reimpostazione della password self-service](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr).

#### <a name="enterprise-state-roaming"></a>Stato Enterprise roaming
Tutti i dispositivi aggiunti ad Azure AD possono sincronizzare le impostazioni per il cloud. Qualsiasi dispositivo in cui un utente accede sincronizzazioni tutte le impostazioni per un'esperienza più produttiva.  



## <a name="value-proposition"></a>Proposta di valore

Aggiunta dei dispositivi ad Azure AD tramite uno dei due metodi accelera la trasformazione digitale. In questo modo di altre funzionalità fornite da Microsoft 365. È possibile garantire una maggiore sicurezza per i tuoi dati e si avrà un'esperienza ottimale. 

Azure AD fornisce diverse opzioni per semplificare il lavoro caricano, ad esempio:

- Gestire tutte le identità dei dispositivi dell'organizzazione da un'unica posizione  

- Riduci i costi dell'help desk, consentendo la reimpostazione della password self-service. Quindi si gli utenti possa reimpostare la password dalla schermata di blocco di Windows 10 nel dispositivo in qualsiasi momento.  



## <a name="configure"></a>Configurare

Se si dispone già di un ambiente Active Directory in locale e si desidera aggiungere i dispositivi aggiunti a un dominio ad Azure AD, ibrida di Azure di configurare dispositivi aggiunti ad AD. Per altre informazioni, [come pianificare l'implementazione di join di Azure Active Directory ibrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 

Configuration Manager ha un'impostazione client per [automaticamente registrare nuovi dispositivi Windows 10 aggiunti a un dominio con Azure AD](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Per altre informazioni sulla configurazione delle impostazioni client, vedere [come configurare le impostazioni client](/sccm/core/clients/deploy/configure-client-settings).

Se si vuole configurare Azure Active Directory-join per i dispositivi senza essere stati anche aggiunti al dominio locale, rivedere le considerazioni per Azure AD join nell'ambiente in uso. Una volta che si è deciso di passare con aggiunta ad Azure AD, sono disponibili molte opzioni per la distribuzione in base alle esigenze dell'organizzazione. Per altre informazioni, vedere gli articoli seguenti:
- [Come si fa: Pianificare l'implementazione di join Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Comprendere le opzioni di provisioning](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  

