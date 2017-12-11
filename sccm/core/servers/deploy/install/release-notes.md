---
title: 'Note sulla versione '
titleSuffix: Configuration Manager
description: Leggere queste note su problemi urgenti non ancora risolti nel prodotto o illustrati in un articolo di Microsoft Knowledge Base.
ms.custom: na
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 8030ce7f98ebb34d9581ad036513b9b1c879c0ad
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2017
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Note sulla versione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con System Center Configuration Manager, le note sulla versione del prodotto sono limitate ai problemi urgenti non ancora risolti (disponibili con un aggiornamento nella console) o descritti in dettaglio in un articolo di Microsoft Knowledge Base.  

Le informazioni sui problemi noti che interessano gli scenari di base vengono comunicate nella documentazione online del prodotto nella libreria della documentazione di System Center Configuration Manager.  

> [!TIP]  
>  Questo argomento contiene le note sulla versione di System Center Configuration Manager (Current Branch). Per una versione Technical Preview di System Center Configuration Manager, vedere [Technical Preview per System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

Per informazioni sulle nuove funzionalità introdotte con diverse versioni, vedere gli argomenti seguenti:
- [Novità della versione 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Novità della versione 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)
- [Novità della versione 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)



## <a name="setup-and-upgrade"></a>Configurazione e aggiornamento  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Quando si installa un sito di Long-Term Servicing Branch con la versione 1606, viene installato un sito Current Branch
<!-- Consider move to core content  -->
Quando si usa il supporto di base della versione 1606 della versione di ottobre 2016 per installare un sito Long-Term Servicing Branch (LTSB), il programma di installazione installa invece un sito Current Branch. Ciò si verifica perché l'opzione per installare un punto di connessione del servizio con l'installazione del sito non è selezionata.

 - Anche se non è richiesto, un punto di connessione del servizio deve essere selezionato per l'installazione di un sito LTSB.

Al termine dell'installazione, il punto di connessione del servizio può essere disinstallato.  Tuttavia, è necessario avere un punto di connessione del servizio in modalità offline o online per inviare i dati di telemetria e ottenere gli aggiornamenti della protezione sia per i siti Current Branch che per i siti LTSB.

Se il sito è stato installato come Current Branch ma originariamente si voleva installare un sito LTSB, è possibile disinstallare il sito e quindi reinstallarlo. In alternativa è possibile chiamare il [Supporto tecnico Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) per assistenza.  

Per confermare quale tipologia installare, nella console passare a **Amministrazione** > **Configurazione del sito** > **Siti** e aprire **Impostazioni gerarchia**. L'opzione per convertire il sito in un sito Current Branch è disponibile solo quando il sito esegue LTSB.  

**Soluzione alternativa:**  nessuna.   


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Un aggiornamento è bloccato con stato Download nel nodo Aggiornamenti e manutenzione della console di Configuration Manager  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Durante il download automatico degli aggiornamenti tramite un punto di connessione del servizio online, un aggiornamento può bloccarsi con stato Download. Quando il download di un aggiornamento è bloccato, le voci simili a quelle seguenti sono incluse nei file di log indicati:  

Log DMPdownloader:  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Soluzione alternativa**: sul server del sito modificare la chiave del Registro di sistema seguente in modo che corrisponda a quanto indicato di seguito e quindi riavviare il servizio SMS_Executive o attendere fino a 24 ore il successivo ciclo di download automatico.  

-   **Chiave da modificare**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valore per lo stato**: impostare sul valore decimale **146944** o sul valore esadecimale **0x00023e00**  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>L'installazione non riesce quando si usano file redist dalla cartella CD.Latest con un errore di verifica del manifesto
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Quando si esegue il programma di installazione dalla cartella CD.Latest creata per la versione 1606 e si usano i file redist inclusi nella cartella CD.Latest, il programma di installazione non riesce e restituisce gli errori seguenti nel registro di installazione di Configuration Manager:

  - ERRORE: Controllo di hash file non riuscito per defaultcategories.dll
  - ERRORE: Verifica del manifesto non riuscita. Versione errata del manifesto?

**Soluzione alternativa:** eseguire una delle operazioni seguenti:
 - Durante l'installazione, scegliere di scaricare i file redist più aggiornati da Microsoft e non usare quelli inclusi nella cartella CD.Latest.
 - Eliminare manualmente la cartella *cd.latest\redist\languagepack\zhh* ed eseguire di nuovo l'installazione.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Distribuzione e aggiornamento del client  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>L'installazione del client non riesce e viene restituito il codice di errore 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*Quanto descritto di seguito si applica a tutte le versioni attive di Configuration Manager.*   
Quando si distribuisce il client in computer Windows e tutte le versioni sono attive, l'installazione ha esito negativo. Il file ccmsetup.log contiene la voce "File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation" seguita da "InstallFromManifest failed 0x8007064c".

**Soluzione alternativa** Il problema è causato da una versione danneggiata di Silverlight installata in precedenza. Per risolvere il problema, provare a eseguire lo strumento seguente sul computer interessato: [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>I piani di manutenzione creano molte distribuzioni e molti gruppi di aggiornamento software duplicati per impostazione predefinita  
Per impostazione predefinita, la procedura guidata Crea piano di manutenzione viene attualmente eseguita dopo ogni sincronizzazione degli aggiornamenti software. A ogni esecuzione, la procedura guidata crea un nuovo gruppo di aggiornamento software e una nuova distribuzione. Se una sincronizzazione degli aggiornamenti software viene eseguita molte volte al giorno, ad esempio, la procedura guidata Crea piano di manutenzione crea più distribuzioni e gruppi di aggiornamento software, probabilmente identici, ogni giorno.  

**Soluzione alternativa**:    
dopo aver creato un piano di manutenzione, aprire le proprietà del piano, passare alla scheda **Pianificazione valutazione**, selezionare **Esegui la regola in base a una pianificazione**, fare clic su **Personalizza** e quindi creare una pianificazione personalizzata. Ad esempio, è possibile impostare l'esecuzione del piano di manutenzione ogni 60 giorni.  



## <a name="software-updates"></a>Aggiornamenti software

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>L'importazione delle impostazioni client di Office 365 da un file di configurazione non ha esito positivo quando contiene lingue non supportate
<!-- 489258  Fixed in 1706  -->
*Quanto descritto di seguito si applica alle versioni 1702 e precedenti.*   
Si verificherà un errore quando si importano le impostazioni del client di Office 365 da un file di configurazione XML esistente e il file contiene lingue non supportate dal client di Office 365 ProPlus. Per i dettagli vedere [Distribuire le app di Office 365 ai client dal dashboard di gestione client di Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Soluzione alternativa**:    
Usare solo [lingue supportate dal client di Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) nel file di configurazione XML.  



## <a name="mobile-device-management"></a>Gestione dispositivi mobili  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>A partire dalla versione 1710 non è più possibile distribuire i profili VPN di Windows Phone 8.1 in Windows 10   <!-- 503274  Should be fixed by 1802, if not sooner -->
Nella versione 1710 non è più possibile creare un profilo VPN tramite il flusso di lavoro di Windows Phone 8.1 che sia applicabile anche ai dispositivi Windows 10. Per questi profili, la pagina Piattaforme supportate non è più visualizzata nella creazione guidata e viene selezionato automaticamente Windows Phone 8.1 nel back-end; nelle pagine delle proprietà è disponibile la pagina Piattaforme supportate ma le opzioni di Windows 10 non sono visualizzate.

**Soluzione alternativa**: usare il flusso di lavoro del profilo VPN di Windows 10 per i dispositivi Windows 10. Se questo non è possibile per l'ambiente, contattare il supporto tecnico. Se necessario, il supporto tecnico indicherà come aggiungere la destinazione Windows 10.


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>La cancellazione completa disattiva i dispositivi Windows 10 con meno di 4 GB di RAM
L'esecuzione della cancellazione completa nei dispositivi Windows 10 RTM (versioni precedenti alla versione 1511) con meno di 4 GB di RAM può rendere i dispositivi inutilizzabili. Dopo aver tentato la cancellazione completa, il dispositivo non può essere avviato e non risponde.

**Soluzione alternativa**: verificare che i PC Windows 10 RTM abbiano almeno 4 GB di RAM disponibile prima di eseguire una cancellazione completa del dispositivo. Per visualizzare il numero di versione dei dispositivi Windows 10, immettere "winver" al prompt dei comandi. Se il dispositivo è già stato cancellato e non risponde, usare un'unità di avvio USB con Windows 10 per avviare e ripristinare l'accesso al dispositivo.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando un utente appartiene a due o più raccolte di utenti in cui sono distribuiti criteri di termini e condizioni, l'utente visualizza più insiemi degli stessi termini  
<!-- 454394    -->
Quando un amministratore distribuisce un insieme di termini in più raccolte utente e un utente è membro di più di una di queste raccolte, tale utente visualizzerà più copie di termini identici all'apertura del portale aziendale.  Se, ad esempio, un utente denominato "UtenteEsempio" è un membro di due diverse raccolte di utenti, denominate "DipendentiAzienda1" e "DipendentiAzienda2" e i termini e le condizioni denominati "CondizioniAziendali" vengono distribuiti sia a DipendentiAzienda1 sia a DipendentiAzienda2, UtenteEsempio vedrà due set identici di CondizioniAziendali nella pagina di accettazione delle condizioni. Considerato che gli utenti possono solo accettare o rifiutare tutte le condizioni, non vi è alcun rischio di trovarsi in uno stato di accettazione ambiguo in cui l'utente ha sia accettato che rifiutato le condizioni. Il report di accettazione di termini e condizioni includerà una sola riga per ogni set di condizioni per ogni utente, quindi nel report non possono esserci errori. L'unico effetto riscontrato dall'utente è la visualizzazione di due insiemi di condizioni nella pagina di accettazione.  

**Soluzione alternativa**: assicurarsi che ogni utente sia incluso solo in solo una raccolta in cui vengono distribuite le condizioni.  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>I profili di posta elettronica Android for Work che usano l'autenticazione del certificato non vengono applicati ai dispositivi
<!--  487657      -->
Quando si crea un profilo di posta elettronica Android for Work, per l'autenticazione sono disponibili due opzioni. La prima consiste nell'uso del nome utente e della password, l'altra nell'uso di certificati. A questo punto, l'opzione "certificati" non funziona. Se il profilo viene creato con il metodo di autenticazione impostato su **certificati**, tale profilo non viene applicato al dispositivo e all'utente verrà chiesto di immettere manualmente i dettagli dell'account di posta elettronica.

**SOLUZIONE ALTERNATIVA**: nessuna. Gli amministratori devono usare l'opzione **nome utente e password** o attendere fino alla risoluzione del problema.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
