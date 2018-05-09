---
title: Componenti del sito
titleSuffix: Configuration Manager
description: Informazioni su come configurare i componenti del sito per modificare il comportamento dei ruoli del sistema del sito e la creazione di report sullo stato del sito.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: da7537ff9cda198f938eafdfc5db198e79a2cb5b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="site-components-for-system-center-configuration-manager"></a>Componenti del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In ogni sito di System Center Configuration Manager è possibile impostare i componenti del sito per modificare il comportamento dei ruoli del sistema del sito e la creazione di report sullo stato del sito. Le configurazioni dei componenti del sito si applicano a un sito e a ogni istanza di un ruolo del sistema del sito applicabile nel sito.  

## <a name="about-site-components"></a>Informazioni sui componenti del sito  
 La maggior parte delle opzioni per i diversi componenti del sito risulta di facile comprensione quando viene visualizzata nella console di Configuration Manager. Le informazioni riportate di seguito possono illustrare meglio alcune configurazioni complesse oppure indirizzano a contenuti aggiuntivi.  

### <a name="software-distribution"></a>Distribuzione del software  

-   **Impostazioni per la distribuzione del contenuto:**  è possibile specificare le impostazioni per modificare la modalità di trasferimento del contenuto del server del sito ai relativi punti di distribuzione. Quando si aumentano i valori usati per le impostazioni di distribuzione simultanea, la distribuzione del contenuto potrebbe usare una maggiore larghezza della banda di rete.  

-   **Account di accesso alla rete:** per informazioni su come impostare e usare l'account di accesso alla rete, vedere [Account di accesso alla rete](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

### <a name="software-update-point"></a>Punto di aggiornamento software  

-   Per informazioni sulle opzioni di configurazione per il componente del punto di aggiornamento software, vedere [Installare un punto di aggiornamento software](../../../../sum/get-started/install-a-software-update-point.md).  

### <a name="management-point"></a>Punto di gestione  

-   **Punti di gestione:** è possibile impostare il sito per pubblicare informazioni sui punti di gestione in Active Directory Domain Services.  

     I client di Configuration Manager usano punti di gestione per individuare i servizi e per trovare informazioni sul sito, ad esempio l'appartenenza al gruppo di limiti e le opzioni di selezione del certificato PKI. I client usano anche punti di gestione per trovare altri punti di gestione nel sito, nonché i punti di distribuzione da cui scaricare il software. I punti di gestione consentono ai client di completare l'assegnazione del sito e scaricare informazioni sul client.  

     Poiché per il client il metodo più sicuro per trovare punti di gestione è la loro pubblicazione nei Servizi di dominio Active Directory, in genere si selezioneranno sempre tutti i punti di gestione funzionanti per la pubblicazioni nei Servizi di dominio Active Directory. Questo metodo di individuazione del servizio tuttavia richiede i seguenti elementi:

     - Questo schema è esteso per Configuration Manager.
     - È disponibile un contenitore di **Gestione sistema** con autorizzazioni di sicurezza appropriate per il server del sito per pubblicare in tale contenitore.
     - Il sito di Configuration Manager è impostato per pubblicare in Active Directory Domain Services.
     - I client appartengano alla stessa foresta di Active Directory del server del sito.  

     Se i client nella Intranet non possono usare Active Directory Domain Services per trovare i punti di gestione, usare invece la pubblicazione [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

 Per informazioni generali sulla posizione del servizio, vedere [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager).  

-   **Pubblica punti di gestione intranet selezionati in DNS:** specificare questa opzione quando i client dell'intranet non possono trovare i punti di gestione da Active Directory Domain Services. Possono invece usare un record di risorse del percorso del servizio DNS (SRV RR) per trovare un punto di gestione nel sito assegnato.  

    Affinché Configuration Manager pubblichi i punti di gestione Intranet in DNS, è necessario che vengano soddisfatte tutte le condizioni seguenti:  

    -   La versione di BIND dei server DNS è 8.1.2 o successiva.  

    -   I server DNS sono impostati per eseguire aggiornamenti automatici e supportano i record di risorse del percorso del servizio.  

    -   I nomi di domini completamente qualificati (FQDN) specificati per i punti di gestione in Configuration Manager hanno voci host (record A o AAA) in DNS.  

    > [!WARNING]  
    >  Affinché i client trovino punti di gestione pubblicati in DNS, è necessario assegnare i client a un sito specifico invece di usare l'assegnazione sito automatica. Impostare questi client per usare il codice del sito con il suffisso del dominio del relativo punto di gestione. Per altre informazioni, vedere [Individuazione dei punti di gestione](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points) in [Come assegnare i client a un sito in System Center Configuration Manager](/sccm/core/clients/deploy/assign-clients-to-a-site).  

     Se i client di Configuration Manager non possono usare Active Directory Domain Services o DNS per trovare i punti di gestione nella Intranet, useranno [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). Il primo punto di gestione installato per il sito viene automaticamente pubblicato in WINS quando viene impostato per accettare le connessioni client HTTP nell'Intranet.  

### <a name="status-reporting"></a>Creazione di report sullo stato  

-   Queste opzioni impostano direttamente il livello di dettaglio incluso nei report sullo stato dei siti e dei clienti.  

### <a name="email-notification"></a>Notifica con posta elettronica  

-   Specificare i dettagli dell'account e del server di posta elettronica per abilitare Configuration Manager per l'invio di notifiche via posta elettronica per gli avvisi.  

### <a name="collection-membership-evaluation"></a>Valutazione dell'appartenenza alla raccolta  

-   Usare questa attività per impostare la frequenza con cui l'appartenenza alla raccolta viene valutata in modo incrementale. La valutazione incrementale aggiorna l'appartenenza alla raccolta solo con risorse nuove o modificate.  

### <a name="edit-the-site-components-at-a-site"></a>Modificare i componenti del sito nel sito  

Seguire la procedura seguente per modificare i componenti del sito:

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Siti** e quindi selezionare il sito che ha i componenti da configurare.  

2.  Nel gruppo **Impostazioni** della scheda **Home** fare clic su **Configura componenti sito**. Selezionare quindi il componente del sito da configurare.  

##  <a name="BKMK_ServiceMgr"></a> Usare Configuration Manager Service Manager per gestire i componenti del sito  
È possibile usare Configuration Manager Service Manager per controllare i servizi di Configuration Manager e per visualizzare lo stato di qualsiasi servizio o thread di lavoro di Configuration Manager (definiti collettivamente come componenti di Configuration Manager). Informazioni sui componenti di Configuration Manager:  

-   I componenti possono essere eseguiti su ogni sistema del sito.  

-   I componenti vengono gestiti allo stesso modo dei servizi in Windows. È possibile avviare, arrestare, sospendere, riprendere o eseguire query nei componenti di Configuration Manager.  

Un servizio di Configuration Manager viene eseguito quando deve svolgere un compito, in genere quando un file di configurazione viene scritto nella inbox di un componente. Per identificare il componente coinvolto in un'operazione, è possibile usare Configuration Manager Service Manager per modificare vari servizi e thread. È quindi possibile notare la conseguente modifica nel comportamento di Configuration Manager. Ad esempio, è possibile interrompere i servizi di Configuration Manager uno alla volta fino a quando viene eliminata una particolare risposta. In questo modo è possibile determinare il servizio all'origine del comportamento.  

> [!TIP]  
>  La procedura seguente consente di modificare il funzionamento dei componenti di Configuration Manager.  

### <a name="use-the-configuration-manager-service-manager"></a>Usare Configuration Manager Service Manager  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio** >  **Stato del sistema**e quindi fare clic su **Stato componente**.  

2.  Nel gruppo **Componente** della scheda **Home** fare clic su **Avvio**. Selezionare quindi **Configuration Manager Service Manager**.  

3.  All'apertura di Configuration Manager Service Manager, connettersi al sito che si desidera gestire.  

     Se non si visualizza il sito che si desidera gestire, fare clic su **Sito**, quindi su **Connetti**e infine immettere il nome del server del sito corretto.  

4.  Espandere il sito e passare a **Componenti** o **Server**in base alla posizione dei componenti che si desidera gestire.  

5.  Nel riquadro a destra selezionare uno o più componenti. Nel menu **Componente** fare clic su **Query** per aggiornare lo stato della selezione.  

6.  Dopo aver aggiornato lo stato del componente, usare una delle quattro opzioni basate su azioni nel menu **Componente** per modificare il funzionamento dei componenti. Dopo aver richiesto un'azione, è necessario eseguire una query sul componente per visualizzare il nuovo stato del componente.  

7.  Chiudere Configuration Manager Service Manager al termine della modifica dello stato operativo dei componenti.  
