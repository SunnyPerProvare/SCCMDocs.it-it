---
title: Windows Autopilot con CO-gestione
titleSuffix: Configuration Manager
description: Usare Windows Autopilot con CO-gestione in Configuration Manager per semplificare il set di backup di nuovi dispositivi Windows 10.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28710b925444d681a161eff184b845a1cdd430b1
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838753"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot con CO-gestione

Ricezione di un nuovo dispositivo Windows 10 è interessante. Tuttavia, può richiedere più tempo per configurare tutte le impostazioni e le App in modo da poter essere produttivi. CO-gestione consente di risolvere questo problema con Windows Autopilot di provisioning dei dispositivi.

AutoPilot offre un'esperienza semplificata per sia per gli utenti nelle situazioni seguenti:
- Configurare e preconfigurare nuovi dispositivi Windows 10  
- Reimpostare, riciclare e ripristinare i dispositivi esistenti  

AutoPilot consente di ridurre il tempo, risorse e la complessità associata alla distribuzione, gestione e disattivazione dei dispositivi. Allo stesso tempo, l'esperienza per gli utenti è semplice e facile dal primo avvio.

Windows Autopilot supporta diversi scenari, ognuno dei quali vengono ingrandite con CO-gestione:

- Gli utenti possono eseguire le proprie le distribuzioni di nuovi dispositivi in Active Directory con aggiunta ad Azure AD ibrido o Azure Active Directory (Azure AD)  

- È possibile impostare la modalità self-distribuzione di nuove distribuzioni di dispositivo in Azure AD per i chioschi multimediali e i dispositivi condivisi  

- Con Windows Autopilot per i dispositivi esistenti, usare Configuration Manager per eseguire la migrazione di un dispositivo esistente di Windows 7 e Active Directory per Windows 10 e Azure AD  

Nel video seguente, senior program manager Danny Guillory e principal program manager per Andrew McMurray discutere e demo di Windows Autopilot con CO-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Vantaggi

Quando si usano insieme CO-gestione e Autopilot, di assicurare che i nuovi dispositivi l'accesso alla rete nello stesso stato di gestione. In questa configurazione, i dispositivi registrati in Intune e hanno un client di Configuration Manager.  Consente di usare il nuovo modello di provisioning di Windows 10 e consente di eliminare la necessità di creare, gestire e aggiornare le immagini del sistema operativo personalizzate. 

In tutti questi scenari, è possibile eseguire automaticamente [abilitare la co-gestione](/sccm/comanage/how-to-prepare-win10) da Intune. Questa automazione è utile con il processo di provisioning e per la gestione continuativa del dispositivo.

Con Autopilot, non è necessario preoccuparsi di driver e immagini. Concentrarsi su il provisioning dei dispositivi per questo processo automatizzato con Intune e Configuration Manager tramite la co-gestione.


Ecco come utilizzo combinato di CO-gestione e Autopilot consente ora:

#### <a name="reduce-time-costs-and-complexity"></a>Ridurre tempi, costi e complessità
Windows Autopilot Usa la versione ottimizzata per OEM di Windows 10 che è già preinstallata nel dispositivo. Questa configurazione consente di salvare le organizzazioni la fatica di dover gestire le immagini personalizzate e i driver per ogni modello di dispositivo in uso. Invece di ricreazione dell'immagine del dispositivo, trasformare l'installazione esistente di Windows 10 in uno stato "aziendali". Applica le impostazioni e i criteri, consente di installare le App e modifica l'edizione di Windows 10. Ad esempio, l'aggiornamento da Windows 10 Pro a Windows 10 Enterprise in modo che sia possibile supportare funzionalità avanzate.

#### <a name="improve-the-user-experience"></a>Migliorare l'esperienza utente
La migliore esperienza utente provoca l'interruzione minima del e consente di tornare a concentrarsi sul proprio lavoro. Windows Autopilot offre un approccio semplice per consentire agli utenti di configurare rapidamente con pochi semplici clic e le credenziali di Azure AD. Per molte organizzazioni con un campo grande di dipendenti remoti, usare Windows Autopilot per fornire i nuovi dispositivi direttamente dal produttore.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Usare Autopilot e Configuration Manager per eseguire la migrazione di dispositivi Windows 7 esistenti a Windows 10
Con Windows Autopilot per i dispositivi esistenti, creare un file di configurazione e distribuirla con una sequenza di attività di Configuration Manager. Questo processo consente di migrare facilmente dispositivi esistenti da Windows 7 a Windows 10. Usare un'immagine di firma di Windows 10 in Configuration Manager e quindi applicarlo nel dispositivo Windows 7 esistente con la configurazione di Autopilot. Quando l'utente avvia il dispositivo, utilizzano il processo di onboarding guidata dall'utente di Autopilot.

Ecco i passaggi per Autopilot per i dispositivi esistenti:

![Panoramica del processo per Windows Autopilot per i dispositivi esistenti](media/autopilot-for-existing-devices.png)

1. Distribuire criteri di gruppo per il reindirizzamento delle cartelle note in OneDrive
2. Generare file di configurazione di Autopilot
3. Distribuire la sequenza di attività per eseguire l'aggiornamento a Windows 10
4. Computer Windows 10 passa attraverso Autopilot al primo avvio

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernizzare il provisioning dei dispositivi per tutti i tipi di ruoli di lavoro
Con Autopilot, è ora possibile fornire una distribuzione del sistema operativo invisibile all'utente a dispositivi automatizzati o i dispositivi condivisi usando la modalità di distribuzione automatica. Questa configurazione soddisfa le esigenze di tutti i diversi tipi di ruoli di lavoro. Inoltre, la funzione di Windows Autopilot reimpostare garantisce che un nuovo provisioning di un dispositivo a un nuovo utente è molto semplice. Questo processo semplifica ciò che è sempre stata un'attività difficile quando si hanno stagionali o i ruoli di lavoro del contratto. 



## <a name="case-study"></a>Case study

La società di spedizione slitte delle guide e logistica tedesco Shenker DB Usa Autopilot per aumentare la produttività dei dipendenti e liberare ai team IT di lavorare su operazioni quotidiane di supporto. Shenker ha allontanato dal tradizionale imaging e sostituito con il provisioning tramite il cloud. Ora viene usato Azure-aggiunta ad AD e Intune per ottenere rapidamente i nuovi dispositivi. 

Anziché avere tempo bonifica dei rifiuti lavoratori in viaggio in una posizione con servizi IT, Shenker ora utilizza Windows Autopilot. Sono inclusi i relativi componenti hardware di ruoli di lavoro direttamente dal produttore per ufficio campo locale. Il ruolo di lavoro al nuovo dispositivo si connette a internet e accedono con le proprie credenziali di Azure AD. Il dispositivo, quindi si connette alle applicazioni e servizi tale Schenker assegna reparto IT per il profilo dell'utente singolo.

Per altre informazioni, vedere [consente di centralizzare la società di logistica globale IT, unisce i dipendenti con area di lavoro digitale moderna](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Proposta di valore

Creare soddisfazione in merito all'interno dell'organizzazione tramite la creazione di un'esperienza utente migliore per gli utenti. Usare Windows Autopilot per ridurre i costi. Guadagnare tempo per concentrarsi su altri progetti di ricavare valore e impatto per l'organizzazione.



## <a name="configure"></a>Configurare

Per altre informazioni, vedere gli articoli seguenti:

[Usare Intune per creare i profili Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)

[Windows Autopilot per i dispositivi esistenti](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices) sequenza di attività

