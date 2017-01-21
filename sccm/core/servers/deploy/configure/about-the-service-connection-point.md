---
title: Punto di connessione del servizio | Documentazione Microsoft
description: Informazioni sul ruolo di sistema del sito di Configuration Manager e pianificazione della gamma di usi.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4a8d98addcd463eb82d8b7100b44254a10d21992
ms.openlocfilehash: b5f7ad01f7a32d69d0c75b3c80a053f3c020c036


---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>Informazioni sul punto di connessione del servizio in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il punto di connessione del servizio di System Center Configuration Manager è un ruolo di sistema del sito che svolge diverse funzioni importanti per la gerarchia. Prima di configurare il punto di connessione del servizio, esaminare e pianificare i diversi usi che potrebbero influire sul modo in cui si configura il ruolo del sistema del sito:  

-   **Gestire i dispositivi mobili con Microsoft Intune**: questo ruolo sostituisce il connettore di Microsoft Intune usato dalle versioni precedenti di Configuration Manager e può essere configurato con i dettagli della sottoscrizione di Intune. Vedere [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../../mdm/understand/hybrid-mobile-device-management.md) (Gestione di dispositivi mobili ibridi (MDM) con System Center Configuration Manager e Microsoft Intune)  

-   **Gestire i dispositivi mobili con MDM locale**: questo ruolo offre supporto per i dispositivi locali gestiti che non si connettono a Internet. Vedere [Gestire i dispositivi mobili con l'infrastruttura locale in System Center Configuration Manager](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)  

-   **Caricare i dati di utilizzo dall'infrastruttura di Configuration Manager**: è possibile controllare il livello o la quantità di dettaglio da caricare. I dati caricati consentono di:  

    -   Identificare e risolvere i problemi in modo proattivo  

    -   Migliorare i prodotti e il servizio  

    -   Identificare gli aggiornamenti per Configuration Manager applicabili alla versione in uso  

  Per informazioni sui dati raccolti da ogni livello e su come modificare il livello di raccolta dopo aver installato il ruolo, vedere [Dati di diagnostica e di utilizzo ](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data) e selezionare il collegamento corrispondente alla versione di Configuration Manager in uso.  

    Per altre informazioni, vedere [Impostazioni e livelli per i dati di utilizzo](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Scaricare gli aggiornamenti applicabili all'infrastruttura di Configuration Manager**: vengono resi disponibili solo gli aggiornamenti rilevanti per l'infrastruttura, in base ai dati di utilizzo da scaricare.  

 **Ogni gerarchia supporta una sola istanza di questo ruolo:**  

-   Il ruolo del sistema del sito può essere installato solo nel sito di livello superiore nella gerarchia, ovvero un sito di amministrazione centrale o il sito primario autonomo.  

-   Se si espande il sito primario autonomo in una gerarchia più ampia, è necessario disinstallare questo ruolo dal sito primario per poterlo quindi installare nel sito di amministrazione centrale.  

##  <a name="a-namebkmkmodesa-modes-of-operation"></a><a name="bkmk_modes"></a> Modalità di funzionamento  
 Il punto di connessione del servizio supporta due modalità di funzionamento:  

-   In **modalità online**il punto di connessione del servizio controlla automaticamente ogni 24 ore se sono presenti aggiornamenti e quindi scarica i nuovi aggiornamenti disponibili per la versione corrente del prodotto e dell'infrastruttura, rendendoli disponibili nella console di Configuration Manager  

-   In **modalità offline** il punto di connessione del servizio non si connette al servizio cloud di Microsoft ed è necessario [Usare lo strumento di connessione del servizio](../../../../core/servers/manage/use-the-service-connection-tool.md) per importare gli aggiornamenti disponibili  

Quando si passa dalla modalità online a offline o viceversa dopo aver installato il punto di connessione del servizio, è necessario riavviare il thread SMS_DMP_DOWNLOADER del servizio SMS_Executive di Configuration Manager per rendere effettiva la modifica.  A tale scopo, usare Configuration Manager Service Manager per riavviare solo il thread SMS_DMP_DOWNLOADER del servizio SMS_Executive.  È anche possibile riavviare il servizio SMS_Executive per Configuration Manager (che riavvia la maggior parte dei componenti del sito) oppure attendere l'esecuzione di un'attività pianificata, ad esempio un backup del sito che arresta e riavvia successivamente il servizio SMS_Executive.  

Per usare Configuration Manager Service Manager, nella console passare a **Monitoraggio** > **Stato sistema** > **Stato componente**, fare clic su **Avvia** e selezionare **Configuration Manager Service Manager**.  In Service Manager:  

-   Nel riquadro di spostamento espandere il sito e **Componenti**, quindi selezionare il componente da riavviare.  

-   Nel riquadro dei dettagli fare clic con il pulsante destro del mouse sul componente e scegliere **Query**.  

-   Dopo aver verificato lo stato del componente, fare di nuovo clic con il pulsante destro del mouse sul componente e selezionare **Arresta**.  

-   Ripetere la **query** nel componente per verificare che sia arrestato, quindi fare di nuovo clic con il pulsante destro del mouse sul componente e selezionare **Avvia**.  

> [!IMPORTANT]  
>  Quando si aggiunge una sottoscrizione di Microsoft Intune al punto di connessione del servizio, il ruolo di sistema del sito viene impostato automaticamente sulla modalità online. Il punto di connessione del servizio non supporta la modalità offline se è configurato con una sottoscrizione di Intune.  

**Quando il ruolo viene installato in un computer remoto rispetto al server del sito:**  

-   L'account computer del server del sito deve essere un amministratore locale sul computer che ospita una connessione al servizio remoto

-   È necessario configurare il server di sistema del sito che ospita il ruolo con un account di installazione del sistema del sito  

-   L'account di installazione del sistema del sito viene usato dal responsabile della distribuzione nel server del sito per trasferire gli aggiornamenti dal punto di connessione del servizio

##  <a name="a-namebkmkurlsa-internet-access-requirements"></a><a name="bkmk_urls"></a> Requisiti per l'accesso a Internet  
Per abilitare l'operazione, il computer che ospita il punto di connessione del servizio ed eventuali firewall tra il computer e Internet deve passare le comunicazioni tramite la **porta TCP 443** ai seguenti percorsi Internet. Il punto di connessione del servizio supporta anche l'uso di un proxy Web con o senza autenticazione per accedere a questi percorsi.  

**Aggiornamenti e manutenzione**  

-   *.akamaiedge.net  

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Manutenzione di Windows 10**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>Installare il punto di connessione del servizio
Quando si esegue il **programma di installazione** per installare il sito di livello superiore di una gerarchia, viene offerta la possibilità di installare il punto di connessione del servizio.

Dopo l'esecuzione del programma di installazione, o se si reinstalla il ruolo del sistema del sito, usare la procedura guidata **Aggiungi ruoli del sistema del sito** o **Crea server di sistema sito** per installare il sistema del sito in un server del sito di livello superiore della gerarchia, ovvero un sito di amministrazione centrale o un sito primario autonomo.  Entrambe le procedure guidate sono disponibili nella scheda **Home** della console, in **Amministrazione** > **Configurazione del sito** > **Server e ruoli del sistema del sito**.



<!--HONumber=Dec16_HO5-->


