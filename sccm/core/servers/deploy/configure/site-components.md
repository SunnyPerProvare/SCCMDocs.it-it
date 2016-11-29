---
title: Componenti del sito | System Center Configuration Manager
description: Informazioni su come configurare i componenti del sito per modificare il comportamento dei ruoli del sistema del sito e la creazione di report sullo stato del sito.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a0c2ff2ad2f76e7e769d49674ccf4d3efe6b4f3e


---
# <a name="site-components-for-system-center-configuration-manager"></a>Componenti del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In ogni sito di System Center Configuration Manager è possibile configurare i componenti del sito per modificare il comportamento dei ruoli del sistema del sito e la creazione di report sullo stato del sito. Le configurazioni dei componenti del sito si applicano a un sito e a ogni istanza di un ruolo del sistema del sito applicabile al sito.  

## <a name="about-site-components"></a>Informazioni sui componenti del sito  
 La maggior parte delle opzioni per i diversi componenti del sito risulta di facile comprensione quando viene visualizzata nella console di Configuration Manager. Tuttavia, le informazioni riportate di seguito possono spiegare meglio alcune configurazioni complesse o fornire dei collegamenti a risorse aggiuntive:  

**Distribuzione del software:**  

-   **Impostazioni per la distribuzione del contenuto:**  è possibile configurare le impostazioni per modificare la modalità di trasferimento del contenuto del server del sito nei relativi punti di distribuzione. Quando si aumentano i valori usati per le impostazioni di distribuzione simultanea, la distribuzione del contenuto potrebbe usare una maggiore larghezza della banda di rete.  

-   **Account di accesso alla rete:** per informazioni su come configurare e usare l'account di accesso alla rete, vedere [Network Access Account](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA) (Account di accesso alla rete)  

**Punto di aggiornamento software:**  

-   Per informazioni sulle opzioni di configurazione per il componente del punto di aggiornamento software, vedere [Install a software update point](../../../../sum/get-started/install-a-software-update-point.md) (Installare un punto di aggiornamento software).  

**Punto di gestione:**  

-   **Punti di gestione:** è possibile configurare il sito per pubblicare informazioni sui punti di gestione in Active Directory Domain Services.  

     I client di Configuration Manager usano i punti di gestione per la posizione del servizio al fine di trovare informazioni sul sito, come ad esempio le opzioni di selezione dell'appartenenza al gruppo di limiti e del certificato PKI e per trovare altri punti di gestione nel sito e punti di distribuzione da cui scaricare il software. I client utilizzano anche punti di gestione per completare l'assegnazione del sito, scaricare criteri client e caricare le informazioni client.  

     Poiché per il client il metodo più sicuro per trovare punti di gestione è la loro pubblicazione nei Servizi di dominio Active Directory, in genere si selezioneranno sempre tutti i punti di gestione funzionanti per la pubblicazioni nei Servizi di dominio Active Directory. Tuttavia, questo metodo di individuazione della posizione del servizio richiede che lo schema venga esteso per Configuration Manager, che ci sia un contenitore di **System Management** con autorizzazioni di sicurezza appropriate affinché il server del sito pubblichi in tale contenitore, che il sito di Configuration Manager sia configurato per pubblicare in Active Directory Domain Services e che i client appartengano alla stessa foresta Active Directory del server del sito.  

     Quando i client nella Intranet non possono usare Active Directory Domain Services per individuare i punti di gestione, usare la pubblicazione [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

     Per informazioni generali sulla posizione del servizio, vedere [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager).  

-   **Pubblica punti di gestione intranet selezionati in DNS**: specificare questa opzione quando i client nella Intranet non riescono a trovare i punti di gestione in Active Directory Domain Services, ma possono usare un record di risorse della posizione del servizio DNS (SRV RR) per trovare un punto di gestione nel sito assegnato.  

    Affinché Configuration Manager pubblichi i punti di gestione Intranet in DNS, è necessario che vengano soddisfatte tutte le condizioni seguenti:  

    -   La versione di BIND dei server DNS è 8.1.2 o successiva.  

    -   I server DNS sono configurati per gli aggiornamenti automatici e supportano i record di risorse di individuazione del servizio.  

    -   I FQDN specificati per i punti di gestione in Configuration Manager hanno voci host (record A o AAA) in DNS.  

    > [!WARNING]  
    >  Affinché i client trovino i punti di gestione pubblicati in DNS, è necessario assegnare i client a un sito specifico (invece di usare l'assegnazione automatica del sito) e configurare tali client in modo che usino il codice del sito con il suffisso del dominio del relativo punto di gestione. Per altre informazioni, vedere [Locating Management Points](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_LocatingMPs) (Individuazione dei punti di gestione) in [How to assign clients to a site in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md)(Come assegnare i client a un sito in System Center Configuration Manager).  

     Se i client di Configuration Manager non possono usare Active Directory Domain Services o DNS per individuare i punti di gestione nella Intranet, eseguono il fallback usando [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). Il primo punto di gestione installato per il sito viene automaticamente pubblicato in WINS quando viene configurato in modo da accettare le connessioni client HTTP nell'Intranet.  

**Creazione rapporti di stato:**  

-   Queste impostazioni configurano direttamente il livello di dettaglio incluso nei report di stato dei siti e dei clienti.  

**Notifica posta elettronica:**  

-   Specificare i dettagli dell'account e del server di posta elettronica per abilitare Configuration Manager per l'invio di notifiche via posta elettronica per gli avvisi.  

**Valutazione dell'appartenenza alla raccolta:**  

-   Usare questa attività per impostare la frequenza con cui l'appartenenza alla raccolta viene valutata in modo incrementale. La valutazione incrementale aggiorna l'appartenenza alla raccolta solo con risorse nuove o modificate.  

#### <a name="to-edit-the-site-components-at-a-site"></a>Per modificare i componenti del sito in un sito  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Siti**, quindi selezionare il sito che include i componenti da configurare.  

2.  Nella scheda **Home** del gruppo **Impostazioni** , fare clic su **Configura componenti sito** , quindi selezionare il componente del sito che si desidera configurare.  

##  <a name="a-namebkmkservicemgra-use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Usare Configuration Manager Service Manager per gestire i componenti del sito  
È possibile usare Configuration Manager Service Manager per controllare i servizi di Configuration Manager e per visualizzare lo stato di qualsiasi servizio o thread di lavoro di Configuration Manager (definiti collettivamente come componenti di Configuration Manager):  

-   I componenti di Configuration Manager possono essere eseguiti su qualsiasi sistema del sito.  

-   I componenti sono gestiti come i servizi in Windows: è possibile avviare, arrestare, mettere in pausa, ripristinare o eseguire una query sui componenti di Configuration Manager.  

Un servizio di Configuration Manager viene eseguito quando deve svolgere un compito, in genere quando un file di configurazione viene scritto nella inbox di un componente. Per identificare il componente coinvolto in un'operazione, è possibile usare **Configuration Manager Service Manager** per modificare diversi servizi e thread di Configuration Manager e quindi osservare la variazione conseguente nel comportamento di Configuration Manager. Ad esempio, è possibile interrompere uno alla volta i servizi di Configuration Manager finché viene eliminata una particolare risposta. In questo modo è possibile determinare il servizio all'origine del comportamento.  

> [!TIP]  
>  La procedura seguente consente di modificare il funzionamento dei componenti di Configuration Manager.  

#### <a name="to-use-the-configuration-manager-service-manager"></a>Per utilizzare Configuration Manager Service Manager  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio** >  **Stato del sistema**e quindi fare clic su **Stato componente**.  

2.  Nella scheda **Home** del gruppo **Componente** , fare clic su **Avvia**, quindi selezionare **Configuration Manager Service Manager**.  

3.  All'apertura di Configuration Manager Service Manager, connettersi al sito che si desidera gestire.  

     Se non si visualizza il sito che si desidera gestire, fare clic su **Sito**, quindi su **Connetti**e infine immettere il nome del server del sito corretto.  

4.  Espandere il sito e passare a **Componenti** o **Server** in base alla posizione dei componenti che si desidera gestire.  

5.  Nel riquadro a destra selezionare uno o più componenti, quindi nel menu **Componente** , fare clic su **Query** per aggiornare lo stato della selezione.  

6.  Dopo aver aggiornato lo stato del componente, utilizzare una delle quattro opzioni basate su azioni nel menu **Componente** per modificare il funzionamento dei componenti. Dopo aver richiesto un'azione, è necessario eseguire una query sul componente per visualizzare il nuovo stato del componente.  

7.  Chiudere Configuration Manager Service Manager al termine della modifica dello stato operativo dei componenti.  



<!--HONumber=Nov16_HO1-->


