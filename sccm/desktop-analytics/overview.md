---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: Panoramica sul servizio desktop Analytics integrato con Configuration Manager.
ms.date: 07/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ee4075926f5c6f01dddcf41a2c329e88a4ee591
ms.sourcegitcommit: 160bcdaf783f3946ad5c7869b2566cbfc4da545c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401499"
---
# <a name="what-is-desktop-analytics"></a>Che cos'è Desktop Analytics?

> [!Note]  
> Queste informazioni si riferiscono a un servizio di anteprima che può essere modificato in modo sostanziale prima del rilascio commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Desktop Analytics è un servizio basato sul cloud che si integra con Configuration Manager. Il servizio fornisce informazioni e informazioni dettagliate per prendere decisioni più informate sulla preparazione degli aggiornamenti dei client Windows. Combina i dati dell'organizzazione con i dati aggregati da milioni di dispositivi connessi ai servizi cloud Microsoft.

USA desktop Analytics con Configuration Manager per:  

- Creare un inventario delle app in esecuzione nell'organizzazione  

- Valutazione della compatibilità delle app con gli ultimi aggiornamenti delle funzionalità di Windows 10  

- Identificare i problemi di compatibilità e ricevere suggerimenti sulla mitigazione in base alle informazioni dettagliate sui dati abilitati per il cloud  

- Creazione di gruppi pilota che rappresentano l'intera applicazione e l'intera proprietà del driver in un set minimo di dispositivi  

- Distribuire Windows 10 in dispositivi pilota e gestiti in produzione  

![Screenshot del home page di analisi del desktop nel portale di Azure](media/portal-home.png)

> [!Note]  
> Desktop Analytics è un successore di Windows Analytics. Il servizio *Windows Analytics* include Preparazione aggiornamenti, Conformità aggiornamenti e integrità dispositivi.
>
> Tutte queste funzionalità vengono combinate nel servizio *Desktop Analytics* . Desktop Analytics è inoltre più strettamente integrato con Configuration Manager.



## <a name="benefits"></a>Vantaggi

Molti clienti hanno problemi a ricevere e rimanere aggiornati con Windows 10. Il problema principale è quello di testare le applicazioni. Questo processo è in genere manuale. Per gli amministratori IT e i proprietari delle applicazioni è necessario richiedere molto tempo per analizzare continuamente le applicazioni esistenti. Correggere quindi gli eventuali problemi che si verificano.

Desktop Analytics offre i vantaggi seguenti:

- **Inventario di dispositivi e software**: Inventario dei fattori chiave come le app e le versioni di Windows.  

- **Identificazione pilota**: Identificazione del set più piccolo di dispositivi che forniscono la più ampia copertura di fattori. Questo argomento è incentrato sui fattori che sono più importanti per un progetto pilota di aggiornamenti e aggiornamenti di Windows. Assicurandosi che il progetto pilota abbia una maggiore riuscita consente di procedere in modo più rapido e sicuro alle distribuzioni più ampie nell'ambiente di produzione.  

- **Identificazione del problema**: Usando i dati di mercato aggregati insieme ai dati dell'ambiente, il servizio prevede potenziali problemi per ottenere e rimanere aggiornati con Windows. Suggerisce quindi potenziali mitigazioni.  

- **Integrazione Configuration Manager**: Il servizio cloud consente di abilitare l'infrastruttura locale esistente. Usare questi dati e analisi per distribuire e gestire Windows sui dispositivi.  



## <a name="prerequisites"></a>Prerequisiti

Per usare desktop Analytics, verificare che l'ambiente soddisfi i prerequisiti seguenti.


### <a name="technical"></a>Tecnico

- Una sottoscrizione di Azure attiva, con autorizzazioni di [amministratore globale](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) . Gli [account Microsoft](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) non sono supportati.  

    > [!Important]  
    > Desktop Analytics richiede attualmente la distribuzione di un servizio Office 365 nel tenant del Azure AD. Questo non è un requisito in futuro.

    - **Proprietario dell'area di lavoro** o autorizzazioni di **collaboratore** per **configurare l'area di lavoro**e i ruoli seguenti:  

      - Ruolo di [**amministratore di desktop Analytics**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) .

      - [**Log Analytics collaboratore**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) e [**amministratore accesso utenti**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) nel gruppo di risorse per usare un'area di lavoro esistente o creare una nuova area di lavoro in un gruppo di risorse esistente.

      - Autorizzazioni di [**proprietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)o [**collaboratore**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) e [**amministratore accesso utenti**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) per la sottoscrizione per creare un'area di lavoro in un nuovo gruppo di risorse.  

- Configuration Manager versione 1902 con aggiornamento cumulativo (4500571) o versione successiva. Per ulteriori informazioni, vedere [Update Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - Ruolo [**amministratore completo**](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_Planroles) in Configuration Manager  

    > [!Note]  
    > Desktop Analytics supporta un ID commerciale per ogni tenant Azure Active Directory (Azure AD) e Configuration Manager gerarchia. Se nell'ambiente sono presenti più gerarchie, utilizzare ID commerciali diversi e tenant Azure AD.<!-- 4958160 -->

- Dispositivi che eseguono Windows 7, Windows 8.1 o Windows 10  

    - Installare gli aggiornamenti più recenti. Per altre informazioni, vedere [aggiornare i dispositivi](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - I dispositivi devono anche avere il client di Configuration Manager, versione 1902 con aggiornamento cumulativo (4500571) o versione successiva. Per ulteriori informazioni, vedere [Update Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    > [!Note]  
    > Desktop Analytics non supporta gli aggiornamenti per il canale di manutenzione a lungo termine di Windows 10 (LTSC). Per altre informazioni, vedere [Panoramica di Windows come servizio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Desktop Analytics è progettato per supportare al meglio lo scenario di aggiornamento sul posto. Se è necessario apportare modifiche sostanziali, ad esempio dall'architettura a 32 bit a 64 bit, usare uno scenario di imaging. Le informazioni dettagliate di desktop Analytics sono ancora utili in questi scenari di distribuzione di sistemi operativi classici, ma è possibile ignorare le indicazioni specifiche sull'aggiornamento sul posto. Per ulteriori informazioni, vedere [scenari per la distribuzione di sistemi operativi aziendali con Configuration Manager](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems).

- Dati di diagnostica di Windows. Per altre informazioni, vedere gli articoli seguenti:  

    - [Livelli di dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Privacy di analisi desktop](/sccm/desktop-analytics/privacy)  

- Connettività di rete dai dispositivi al cloud pubblico Microsoft. Per ulteriori informazioni, vedere [come abilitare la condivisione dei dati](/sccm/desktop-analytics/enable-data-sharing)  

> [!Important]   
> Microsoft è impegnata a fornire gli strumenti e le risorse che consentono di controllare la privacy. Di conseguenza, Microsoft non raccoglie i dati seguenti dai dispositivi che si trovano in paesi europei (See e Switzerland):
>
> - Dati di diagnostica di Windows da dispositivi Windows 8.1
> - Dati di utilizzo delle app per Windows 7

### <a name="licensing-and-costs"></a>Licenze e costi

Desktop Analytics richiede una delle seguenti sottoscrizioni di licenza:

- Windows 10 Enterprise E3 o E5; o Microsoft 365 F1, E3 o E5  

- Windows 10 Education a3 o a5; o Microsoft 365 a3 o a5  

- Windows VDA E3 o E5  

Oltre al costo degli abbonamenti delle licenze, non sono previsti costi aggiuntivi per l'uso di analisi del desktop. All'interno di Azure Log Analytics, desktop Analytics è "con classificazione zero". Questa valutazione significa che è esclusa dai limiti e dai costi dei dati, indipendentemente dal piano tariffario Log Analytics di Azure scelto. Per altre informazioni sui piani tariffari di Azure Log Analytics, vedere [prezzi-log Analytics](https://azure.microsoft.com/pricing/details/monitor/).

- Se si usa il livello gratuito, che prevede un limite per la quantità di dati raccolti al giorno, i dati di analisi desktop non vengono conteggiati per questo limite. È possibile raccogliere tutti i dati di analisi desktop dai dispositivi e disporre ancora del limite completo per la raccolta di dati aggiuntivi da altre origini.

- Se si usa un livello a pagamento che addebita i costi per GB di dati raccolti, non vengono addebitati i costi per i dati di analisi del desktop. Puoi raccogliere tutti i dati di analisi del desktop dai tuoi dispositivi senza sostenere costi.

> [!Note]  
> Diversi piani di Log Analytics di Azure hanno periodi di conservazione dei dati diversi. Desktop Analytics eredita i criteri di conservazione dei dati dell'area di lavoro. Se l'area di lavoro si trova nel piano gratuito, desktop Analytics mantiene gli ultimi 30 giorni di "snapshot giornalieri" raccolti nell'area di lavoro.


## <a name="next-steps"></a>Passaggi successivi

L'esercitazione seguente fornisce una guida dettagliata per iniziare a usare analisi di desktop e Configuration Manager:  

- [Distribuire Windows 10 in progetto pilota](/sccm/desktop-analytics/tutorial-windows10)  
