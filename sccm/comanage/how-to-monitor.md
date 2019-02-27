---
title: Monitorare la co-gestione
titleSuffix: Configuration Manager
description: Usare il dashboard di co-gestione per esaminare le informazioni sui dispositivi con co-gestione.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c731692bc2277cc5ce97e079387b392ca09ff3e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755394"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Come monitorare la co-gestione in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Dopo aver abilitato la co-gestione, monitorare i dispositivi di co-gestione usando i metodi seguenti:

- [Dashboard di co-gestione](#co-management-dashboard)  

- [Criteri di distribuzione](#deployment-policies)

- [Dati del dispositivo WMI](#wmi-device-data)



## <a name="co-management-dashboard"></a>Dashboard di co-gestione

A partire dalla versione 1802, è possibile visualizzare un dashboard con informazioni sulla co-gestione. Il dashboard consente di esaminare i computer co-gestiti presenti nell'ambiente. I grafici consentono di identificare i dispositivi che potrebbero richiedere attenzione.<!--1356648-->

Nella console di Configuration Manager andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Co-gestione**.

A partire dalla versione 1810, il dashboard di co-gestione è stata migliorato con l'aggiunta di informazioni più dettagliate. <!--1358980-->

![Schermata del dashboard di CO-gestione](media/co-management-dashboard.png)


### <a name="co-managed-devices"></a>Dispositivi con co-gestione

*Si applica alla versione 1802 e 1806*

Specifica la percentuale di dispositivi co-gestiti presenti in tutto l'ambiente.

![Riquadro dispositivi CO-gestiti](media/co-management-dashboard/Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>Distribuzione del sistema operativo client

*Si applica a tutte le versioni* 

Specifica il numero di dispositivi client per ogni versione di sistema operativo. Gli elementi sono raggruppati nei modi seguenti:  
- Windows 7 e 8.x  
- Windows 10, versioni precedenti alla 1709  
- Windows 10, versione 1709 e successive  

    > [!Tip]  
    > Windows 10, versione 1709 e successive, è un prerequisito per la co-gestione.  

Passare il mouse su una sezione del grafico per visualizzare la percentuale dei dispositivi nello specifico gruppo di sistemi operativi.

![Riquadro di distribuzione del sistema operativo client](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>Stato della co-gestione (anello)

*Si applica alla versione 1802 e 1806*

Specifica la suddivisione dei dispositivi con esito positivo e negativo nelle categorie seguenti:
- Esito positivo, aggiunto ad Azure AD ibrido  
- Esito positivo, aggiunto ad Azure AD  
- Errore: registrazione automatica non riuscita  

Passare il mouse su una sezione del grafico per visualizzare la percentuale dei dispositivi nella categoria. 

![Nel riquadro stato (grafico ad anello) CO-gestione](media/co-management-dashboard/Co-management-status-graph.PNG)

Selezionare una sezione del grafico per visualizzare l'elenco dei dispositivi presenti in tale categoria.

![Elenco di dispositivi con errore di registrazione](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>Stato della co-gestione (imbuto)

*Si applica alla versione 1810 e successive*

Un grafico a imbuto che mostra il numero di dispositivi che presentano i seguenti stati del processo di registrazione:  
- Dispositivi idonei  
- Scheduled  
- La registrazione è stata avviata  
- Registrazione eseguita  

![Riquadro Stato della co-gestione (imbuto)](media/co-management-dashboard/1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>Stato di registrazione della co-gestione

*Si applica alla versione 1810 e successive*

Specifica la suddivisione degli stati dei dispositivi nelle categorie seguenti:
- Esito positivo, aggiunto ad Azure AD ibrido  
- Esito positivo, aggiunto ad Azure AD  
- Registrazione, aggiunta ad Azure AD ibrido  
- Operazione non riuscita, aggiunta ad Azure AD ibrido  
- Operazione non riuscita, aggiunta ad Azure AD  
- Accesso utente in sospeso  

Selezionare uno stato nel riquadro per visualizzare un elenco dei dispositivi con tale stato.  

![Riquadro Stato di registrazione della co-gestione](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>Transizione del carico di lavoro

*Si applica a tutte le versioni*

Grafico a barre con il numero di dispositivi passati a Microsoft Intune per i carichi di lavoro disponibili. 

L'elenco dei carichi di lavoro varia in base alla versione di Configuration Manager. Per altre informazioni, vedere [Carichi di lavoro che è possibile passare a Intune](/sccm/comanage/workloads).

Passare il mouse su una sezione del grafico per visualizzare il numero di dispositivi di cui è stata eseguita la transizione per il carico di lavoro. 

![Grafico a barre di transizione del carico di lavoro](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>Errori di registrazione

*Si applica alla versione 1810 e successive*

Questa tabella è un elenco di errori di registrazione dei dispositivi. Questi errori possono provenire dal componente di MDM in Windows, il nucleo del sistema operativo Windows o il client di Configuration Manager. 

Sono disponibili centinaia di possibili errori. La tabella seguente elenca gli errori più comuni.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Errore | Descrizione |
|---------|---------|
| 2147549183 (0x8000FFFF) | La registrazione MDM non è stata configurata ancora in Azure AD, o la registrazione URL non è previsto.<br><br>[Abilitare la registrazione automatica di Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | Licenza dell'utente è nella registrazione blocco di uno stato non valido<br><br>[Assegnare licenze agli utenti](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Quando si tenta automaticamente di registrazione in Intune, ma la configurazione di Azure AD non viene applicata completamente. Questo problema dovrebbe essere temporaneo, come i tentativi di dispositivo dopo un breve periodo di tempo. |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | L'utente ha annullato l'operazione<br><br>Se la registrazione MDM richiede l'autenticazione a più fattori e l'utente non ha eseguito l'accesso con un secondo fattore supportato, Windows visualizza una notifica di tipo avviso popup a registrare. Se l'utente non risponde per la notifica di tipo avviso popup, si verifica questo errore. Questo problema dovrebbe essere temporaneo, come verrà Riprova e richiedere all'utente di Configuration Manager. Gli utenti devono utilizzare l'autenticazione a più fattori quando accedono a Windows. Anche formare gli utenti a prevedono questo comportamento e se richiesto, intraprendere l'azione. | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Gestione dei dispositivi mobili in genere non è supportata | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Server non è stato possibile autenticare l'utente<br><br> Non vi è alcun token di Azure AD per l'utente. Assicurarsi che l'utente possa autenticarsi con Azure AD. |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | Iscrizione automatica MDM è supportato solo in Windows RS3 e versioni successive.<br><br>Verificare che il dispositivo soddisfi i [i requisiti minimi](/sccm/comanage/overview#windows-10) per la co-gestione. |
| 3400073293 | Risposta dell'account dell'area di autenticazione ADAL utente sconosciuto<br><br>Controllare la configurazione di Azure AD e assicurarsi che gli utenti possono eseguire l'autenticazione. | 
| 3399548929 | Necessario accesso dell'utente<br><br>Questo problema dovrebbe essere temporaneo. Si verifica quando l'utente rapidamente effettua la disconnessione prima che si verifichi l'attività di registrazione. | 
| 3400073236 | Richiesta di token di sicurezza ADAL non è riuscita.<br><br>Controllare la configurazione di Azure AD e assicurarsi che gli utenti possono eseguire l'autenticazione. |
| 2149122477 | Problema HTTP generico |
| 3400073247 | L'autenticazione Windows integrata di ADAL è supportata solo nel flusso federato<br><br>[Pianificare l'implementazione di join di Azure Active Directory ibrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | Il server o il proxy non è stato trovato.<br><br>Questo problema dovrebbe essere temporaneo, quando il client non può comunicare con il cloud. Se persiste, assicurarsi che il client disponga della connettività coerente in Azure. | 
| 2149056532 | Piattaforma specifica o la versione non è supportato<br><br>Verificare che il dispositivo soddisfi i [i requisiti minimi](/sccm/comanage/overview#windows-10) per la co-gestione. |
| 2147943568 | Elemento non trovato<br><br>Questo problema dovrebbe essere temporaneo. Se persiste, contattare il supporto tecnico Microsoft. |
| 2192179208 | Non sono sufficienti risorse di memoria sono disponibili per elaborare il comando.<br><br>Questo problema dovrebbe essere temporaneo, dovrebbe risolversi da solo quando il client Riprova. |
| 3399614467 | ADAL concessione di autorizzazione non è riuscita per questa asserzione<br><br>Controllare la configurazione di Azure AD e assicurarsi che gli utenti possono eseguire l'autenticazione. |
| 2149056517 | Errore generico dal server di gestione, ad esempio errore di accesso al database<br><br>Questo problema dovrebbe essere temporaneo. Se persiste, contattare il supporto tecnico Microsoft. |
| 2149134055 | Nome di WinHTTP non risolto<br><br>Il client non è possibile risolvere il nome del servizio. Controllare la configurazione DNS. | 
| 2149134050 | timeout Internet<br><br>Questo problema dovrebbe essere temporaneo, quando il client non può comunicare con il cloud. Se persiste, assicurarsi che il client disponga della connettività coerente in Azure. | 


Per altre informazioni, vedere [i valori di errore di registrazione MDM](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants).



## <a name="deployment-policies"></a>Criteri di distribuzione

vengono creati due criteri nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Un criterio è per il gruppo pilota e uno per la produzione. Questi criteri segnalano solo il numero di dispositivi in cui Configuration Manager ha applicato il criterio. Non tengono conto del numero di dispositivi registrati in Intune, che è un requisito necessario prima che i dispositivi possano essere co-gestiti.  



## <a name="wmi-device-data"></a>Dati del dispositivo WMI

Query di **SMS_Client_ComanagementState** classe WMI. È possibile creare raccolte personalizzate in Configuration Manager, che consentono di determinare lo stato della distribuzione di CO-gestione. Per altre informazioni sulla creazione di raccolte personalizzate, vedere [come creare raccolte](/sccm/core/clients/manage/collections/create-collections). 

I campi seguenti sono disponibili nella classe WMI:  

- **MachineId**: Un ID univoco del dispositivo per il client di Configuration Manager  

- **MDMEnrolled**: specifica se il dispositivo è registrato nella soluzione MDM  

- **Authority**: L'autorità per il quale il dispositivo è registrato  

- **ComgmtPolicyPresent**: specifica se nel client sono presenti criteri di co-gestione di Configuration Manager. Se il valore di **MDMEnrolled** è **0**, il dispositivo non è co-gestito, indipendentemente dalla presenza o meno di criteri di co-gestione nel client.  

Un dispositivo è co-gestito quando i campi **MDMEnrolled** e **ComgmtPolicyPresent** sono entrambi impostati su **1**.  
