---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: Panoramica del servizio Desktop Analytics integrato con Configuration Manager.
ms.date: 10/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 76fa92c93a290c49c286be3bb1368dfdf8347ef3
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72384977"
---
# <a name="what-is-desktop-analytics"></a>Che cos'è Desktop Analytics?

Desktop Analytics è un servizio basato sul cloud che si integra con Configuration Manager. Il servizio offre dati analitici e intelligenza per consentire agli utenti di prendere decisioni più informate sull'idoneità degli aggiornamenti dei client Windows. Combina i dati dell'organizzazione con i dati aggregati di milioni di dispositivi connessi a servizi cloud Microsoft.

Usare Desktop Analytics con Configuration Manager per eseguire le operazioni seguenti:  

- Creare un inventario delle app in esecuzione nell'organizzazione  

- Valutare la compatibilità delle app con gli ultimi aggiornamenti delle funzionalità di Windows 10  

- Identificare i problemi di compatibilità e ricevere suggerimenti sulla mitigazione in base alle informazioni dettagliate sui dati abilitati per il cloud  

- Creare gruppi pilota che rappresentino l'intera applicazione e le proprietà del driver in un insieme minimo di dispositivi  

- Distribuire Windows 10 a dispositivi pilota e gestiti dalla produzione  

![Screenshot della home page di Desktop Analytics nel portale di Azure](media/portal-home.png)

> [!Note]  
> Desktop Analytics è l'evoluzione di Windows Analytics. Il servizio *Windows Analytics* include Preparazione aggiornamenti, Conformità aggiornamenti e Integrità dispositivi.
>
> Tutte queste funzionalità vengono combinate nel servizio *Desktop Analytics*. Desktop Analytics è ancora più strettamente integrato con Configuration Manager.



## <a name="benefits"></a>Vantaggi

Molti clienti hanno problemi a ottenere Windows 10 e a mantenerlo aggiornato. Il problema principale è quello di testare le applicazioni. Questo processo è in generalmente manuale. Per gli amministratori IT e i proprietari delle applicazioni analizzare continuamente le applicazioni esistenti e quindi correggere eventuali problemi è molto dispendioso in termini di tempo.

Desktop Analytics offre i vantaggi seguenti:

- **Inventario di dispositivi e software**: Inventario dei fattori chiave, ad esempio le app e le versioni di Windows.  

- **Identificazione del progetto pilota**: Identificazione dell'insieme minimo di dispositivi che consentono la più ampia copertura di fattori. Vengono identificati i fattori ritenuti più importanti per un progetto pilota di aggiornamenti Windows. Assicurarsi che il progetto pilota sia ottimale per poter procedere in modo più rapido e sicuro a distribuzioni di grani dimensioni in ambiente di produzione.  

- **Identificazione dei problemi**: Usando congiuntamente i dati di mercato aggregati e i dati dell'ambiente, il servizio esegue una previsione dei potenziali problemi per ottenere Windows e rimanere aggiornati. Suggerisce quindi eventuali mitigazioni.  

- **Integrazione di Configuration Manager**: Il servizio cloud consente di abilitare l'infrastruttura locale esistente. Usare questi dati e queste analisi per distribuire e gestire Windows nei dispositivi.  



## <a name="prerequisites"></a>Prerequisiti

Per usare Desktop Analytics, verificare che l'ambiente soddisfi i prerequisiti seguenti.


### <a name="technical"></a>Prerequisiti tecnici

- Una sottoscrizione di Azure attiva con autorizzazioni di [Amministratore globale](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions). Gli [account Microsoft](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) non sono supportati.  

    > [!Important]  
    > Desktop Analytics richiede attualmente la distribuzione di un servizio di Office 365 nel tenant di Azure AD. Non sarà un requisito in futuro.

    - Autorizzazioni di **Proprietario dell'area di lavoro** o di **Collaboratore** per **configurare l'area di lavoro** e i ruoli seguenti:  

      - Ruolo [**Amministratore di Desktop Analytics**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).

      - [**Collaboratore di Log Analytics**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) e [**Amministratore Accesso utenti**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) nel gruppo di risorse per usare un'area di lavoro esistente o crearne una nuova in un gruppo di risorse esistente.

      - Autorizzazioni di [**Proprietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) o [**Collaboratore**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) e [**Amministratore Accesso utenti**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) nella sottoscrizione per creare un'area di lavoro in un nuovo gruppo di risorse.  

- Configuration Manager versione 1902 con aggiornamento cumulativo (4500571) o versione successiva. Per altre informazioni, vedere [Aggiornare Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - Ruolo [**Amministratore completo**](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_Planroles) in Configuration Manager  

    > [!Note]  
    > Desktop Analytics supporta un ID commerciale per ogni tenant di Azure Active Directory (Azure AD) e gerarchia di Configuration Manager. Se nell'ambiente sono presenti più gerarchie, usare ID commerciali e tenant di Azure AD diversi.<!-- 4958160 -->

- Dispositivi che eseguono Windows 7, Windows 8.1 o Windows 10  

    - Installare gli aggiornamenti più recenti. Per altre informazioni, vedere [Aggiornare i dispositivi](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - I dispositivi devono anche avere il client di Configuration Manager versione 1902 con aggiornamento cumulativo (4500571) o versione successiva. Per altre informazioni, vedere [Aggiornare Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    > [!Note]  
    > Desktop Analytics non supporta gli aggiornamenti a Windows 10 Long-Term Servicing Channel (LTSC). Per altre informazioni, vedere [Panoramica di Windows as a Service](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Desktop Analytics è progettato per supportare al meglio lo scenario di aggiornamento sul posto. Se è necessario apportare modifiche principali, ad esempio passare da un'architettura a 32 bit a un'architettura a 64 bit, usare uno scenario di creazione dell'immagine. Le informazioni dettagliate di Desktop Analytics risultano comunque utili in questi classici scenari di distribuzione del sistema operativo, ma è possibile ignorare le indicazioni specifiche dell'aggiornamento sul posto. Per altre informazioni, vedere [Scenari per distribuire sistemi operativi aziendali con Configuration Manager](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems).

- Dati di diagnostica di Windows. Per altre informazioni, vedere gli articoli seguenti:  

    - [Livelli dei dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Privacy di Desktop Analytics](/sccm/desktop-analytics/privacy)  

- Connettività di rete dai dispositivi al cloud pubblico Microsoft. Per altre informazioni, vedere [Come abilitare la condivisione dei dati](/sccm/desktop-analytics/enable-data-sharing).  

> [!Important]   
> Microsoft è impegnata a offrire strumenti e risorse che consentono di controllare la privacy. Microsoft non raccoglie quindi i dati seguenti dai dispositivi che si trovano in paesi europei (SEE e Svizzera):
>
> - Dati di diagnostica di Windows da dispositivi Windows 8.1
> - Dati di uso delle app per Windows 7

### <a name="licensing-and-costs"></a>Licenze e costi

I dispositivi registrati in Desktop Analytics possono essere usati solo dagli utenti che hanno una licenza per i prodotti seguenti:

- Windows 10 Enterprise E3 o E5 (incluso in Microsoft 365 F1, E3 o E5)

- Windows 10 Education A3 o A5 (incluso in Microsoft 365 A3 o A5)

- Accesso a Desktop virtuale Windows E3 o E5  

Oltre al costo delle sottoscrizioni delle licenze, non sono previsti costi aggiuntivi per l'uso di Desktop Analytics. In Log Analytics di Azure Desktop Analytics è un servizio con tariffa zero. Ciò significa che è escluso da limiti di dati e costi, indipendentemente dal piano tariffario scelto in Log Analytics di Azure. Per altre informazioni sui piani tariffari di Log Analytics di Azure, vedere [Prezzi - Log Analytics](https://azure.microsoft.com/pricing/details/monitor/).

- Se si usa il livello gratuito che prevede un limite sulla quantità di dati raccolti ogni giorno, i dati di Desktop Analytics non vengono conteggiati per questo limite. È possibile raccogliere tutti i dati di Desktop Analytics dai dispositivi e avere ancora l'intero limite a disposizione per raccogliere dati aggiuntivi da altre origini.

- Se si usa un livello a pagamento che addebita i costi a seconda dei GB di dati raccolti, non vengono addebitati i costi per i dati di Desktop Analytics. È possibile raccogliere tutti i dati di Desktop Analytics dai dispositivi senza sostenere alcun costo.

> [!Note]  
> I vari piani di Log Analytics di Azure hanno periodi di conservazione dei dati diversi. Desktop Analytics eredita i criteri di conservazione dei dati dell'area di lavoro. Se l'area di lavoro rientra nel piano gratuito, Desktop Analytics conserva gli ultimi 30 giorni di "snapshot giornalieri" raccolti nell'area di lavoro.


## <a name="next-steps"></a>Passaggi successivi

L'esercitazione seguente offre una guida dettagliata per iniziare a usare Desktop Analytics e Configuration Manager:  

- [Distribuire Windows 10 a un gruppo pilota](/sccm/desktop-analytics/tutorial-windows10)  
