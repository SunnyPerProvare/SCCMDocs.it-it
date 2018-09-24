---
title: Cambiare l'autorità MDM
titleSuffix: Configuration Manager
description: Informazioni su come cambiare l'autorità MDM da Configuration Manager (ibrido) a Intune autonomo
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: 692ffb04546da4f65b2198e582999582c996fdb2
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584610"
---
# <a name="change-your-mdm-authority"></a>Cambiare l'autorità MDM

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile cambiare l'autorità MDM senza dover contattare il supporto tecnico Microsoft e senza che sia necessario annullare la registrazione dei dispositivi gestiti esistenti e quindi eseguirla di nuovo. Questo articolo descrive i passaggi necessari per modificare un tenant esistente di Microsoft Intune configurato dalla console di Configuration Manager (ibrido) alla versione autonoma di Intune. Dopo aver completato i passaggi descritti in questo articolo, i dispositivi vengono gestiti da Microsoft Intune nel [portale di Azure](https://portal.azure.com). 

Questo articolo descrive la modifica dell'autorità MDM quando non è stata eseguita la migrazione di utenti in precedenza. Per cambiare l'autorità MDM dopo aver eseguito la [migrazione di un subset di utenti](migrate-hybridmdm-to-intunesa.md), vedere [Cambiare l'autorità MDM](migrate-change-mdm-authority.md).

> [!Important]  
> A partire dal 13 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="key-considerations"></a>Considerazioni principali

Dopo aver cambiato l'autorità MDM, prevedere un tempo di transizione fino a otto ore prima dell'archiviazione del dispositivo e della sua sincronizzazione con il servizio. Per garantire che i dispositivi registrati continuino a essere gestiti e protetti dopo la modifica, configurare le impostazioni direttamente in Intune. Tenere presenti le seguenti considerazioni:

- I dispositivi devono connettersi con il servizio dopo la modifica, in modo che le impostazioni dalla nuova autorità MDM (versione autonoma di Intune) sostituiscano le impostazioni esistenti nel dispositivo.  

- Dopo aver cambiato l'autorità MDM, alcune delle impostazioni di base (ad esempio i profili) dell'autorità MDM precedente (ibrido) rimarranno sul dispositivo per un massimo di sette giorni. È consigliabile configurare app e impostazioni (criteri, profili, app e così via) nella nuova autorità MDM non appena possibile. Inoltre, distribuire le impostazioni ai gruppi di utenti che contengono gli utenti con dispositivi registrati esistenti. Quando un dispositivo si connette al servizio dopo la modifica all'autorità MDM, riceve nuove impostazioni dalla nuova autorità MDM. Tutti i nuovi criteri di destinazione sostituiranno i criteri esistenti nel dispositivo.  

- Dopo il passaggio alla nuova autorità MDM, i dati di conformità nel [portale di Azure](https://portal.azure.com) possono richiedere fino a una settimana prima di fornire una segnalazione accurata. Tuttavia, gli stati di conformità in Azure Active Directory e nel dispositivo sono accurati e il dispositivo è comunque protetto.  

- Per i dispositivi senza utenti associati non viene eseguita la migrazione alla nuova autorità MDM. Questo comportamento si verifica generalmente con il Device Enrollment Program per dispositivi iOS o con scenari di registrazione in blocco. Per tali dispositivi, contattare il supporto tecnico per assistenza nel passaggio alla nuova autorità MDM.  



## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparare il cambiamento dell'autorità MDM in Intune autonomo

Esaminare le informazioni seguenti per preparare il passaggio alla nuova autorità MDM:

- Prima che un dispositivo si connetta al servizio dopo il passaggio alla nuova autorità MDM possono trascorrere fino a otto ore.  

- Assicurarsi che a tutti gli utenti attualmente gestiti in modo ibrido sia assegnata una licenza Intune o EMS prima del passaggio all'autorità MDM. Questa licenza garantisce che l'utente e i suoi dispositivi siano gestiti da Intune autonomo dopo il cambio dell'autorità MDM. Per altre informazioni, vedere [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Assegnare licenze di Intune agli account utente).  

- Assicurarsi che all'account utente amministratore sia assegnata una licenza di Intune/EMS. Verificare che l'account utente amministratore possa accedere a Intune prima di cambiare l'autorità MDM. Prima della modifica dell'autorità MDM, nel **portale di Azure** deve essere visualizzato [Imposta su Configuration Manager](https://portal.azure.com) (tenant ibrido) in Intune.  

- Durante il cambiamento nell'autorità MDM non vi sarà alcun impatto visibile sugli utenti finali. 



## <a name="change-the-mdm-authority-to-intune-standalone"></a>Cambiare l'autorità MDM in Intune autonomo

La procedura per cambiare l'autorità MDM in Intune autonomo include i passaggi generali seguenti:  

- Nella console di Configuration Manager usare l'opzione **Cambia l'autorità MDM in Microsoft Intune** per rimuovere la sottoscrizione a Microsoft Intune esistente.  

- Nel [portale di Azure](https://portal.azure.com) in Intune configurare e distribuire le nuove impostazioni e app dalla nuova autorità MDM (Intune).  

- I dispositivi, alla successiva connessione al servizio, saranno sincronizzati e riceveranno le nuove impostazioni dalla nuova autorità MDM.  

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Per cambiare l'autorità MDM in Intune autonomo
1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Servizi cloud** e selezionare il nodo **Sottoscrizione a Microsoft Intune**. Eliminare la sottoscrizione di Intune esistente.  

2. Selezionare **Cambia l'autorità MDM in Microsoft Intune** e fare clic su **Avanti**.  

   ![Rimozione guidata della sottoscrizione di Microsoft Intune, pagina Introduzione](./media/mdm-change-delete-subscription.png)

3. Accedere al tenant di Intune usato in origine quando è stata configurata l'autorità MDM in Configuration Manager.  

4. Fare clic su **Avanti** e completare la procedura guidata.  

5. L'autorità MDM è ora impostata su **Microsoft Intune**. La sottoscrizione a Intune non viene visualizzata nel nodo Sottoscrizioni a Microsoft Intune della console di Configuration Manager.  

6. Per verificare che l'autorità MDM sia impostata, procedere in questo modo:  

    1. Accedere al [portale di Azure](https://portal.azure.com) usando lo stesso tenant di Intune usato in precedenza.  

    2. Scegliere **Tutti i servizi** > **Intune** > **Registrazione del dispositivo**. L'autorità MDM viene visualizzata nella sezione in alto a destra del pannello **Panoramica**.  



## <a name="next-steps"></a>Passaggi successivi

Una volta completata la modifica dell'autorità MDM, esaminare i passaggi seguenti:  

- Quando il servizio Intune rileva che l'autorità MDM di un tenant è cambiata, invia un messaggio di notifica a tutti i dispositivi registrati per l'archiviazione e la sincronizzazione con il servizio. Questo comportamento si verifica al di fuori delle archiviazioni periodiche pianificate. Di conseguenza, dopo aver cambiato l'autorità MDM per il tenant da ibrida a Intune autonomo, tutti i dispositivi accesi e online si connettono al servizio, ricevono la nuova autorità MDM e vengono gestiti da Intune autonomo. Non ci sono interruzioni per la gestione e protezione di questi dispositivi.  

- I dispositivi che sono spenti o non in linea durante (o immediatamente dopo) la modifica dell'autorità MDM si connettono e vengono sincronizzati con il servizio mediante la nuova autorità MDM quando sono nuovamente accesi e online.   

- Gli utenti possono passare rapidamente alla nuova autorità MDM avviando manualmente un'archiviazione dal dispositivo al servizio. Gli utenti possono eseguire facilmente questa operazione usando l'app Portale aziendale e avviando un controllo di conformità del dispositivo.  

- Per verificare che tutto funzioni correttamente dopo che i dispositivi sono stati archiviati e sincronizzati con il servizio dopo la modifica dell'autorità MDM, cercare i dispositivi nel [portale di Azure](https://portal.azure.com). I dispositivi che in precedenza sono stati gestiti da Configuration Manager (ibrido) vengono ora visualizzati come dispositivi gestiti in Intune.    

- Quando un dispositivo è offline durante la modifica nell'autorità MDM e quando il dispositivo viene archiviato nel servizio si ha una situazione intermedia. Per garantire che il dispositivo rimanga protetto e funzionale durante questo periodo, i profili seguenti rimangono nel dispositivo per un massimo di sette giorni o fino a quando il dispositivo non si connette con la nuova autorità MDM e riceve le nuove impostazioni che sovrascrivono quelle esistenti:  
    - Profilo di posta elettronica
    - Profilo VPN
    - Profilo certificato
    - Profilo Wi-Fi
    - Profili di configurazione  

- Per sovrascrivere le impostazioni precedenti, verificare che le nuove impostazioni che devono sovrascrivere quelle esistenti abbiano lo stesso nome delle precedenti. In caso contrario, i dispositivi potrebbero finire con criteri e profili ridondanti.    

  > [!TIP]   
  > Creare tutte le impostazioni di gestione e le configurazioni, nonché le distribuzioni, subito dopo aver completato la modifica dell'autorità MDM. Questa azione consente di proteggere e gestire attivamente i dispositivi durante il periodo intermedio.   

-  Dopo aver modificato l'autorità MDM, eseguire la procedura seguente per verificare che i nuovi dispositivi siano registrati correttamente con la nuova autorità:   

    - Registrare un nuovo dispositivo  

    - Assicurarsi che il dispositivo appena registrato sia visualizzato nel [portale di Azure](https://portal.azure.com).  

    - Eseguire un'azione, ad esempio il blocco remoto, dal [portale di Azure](https://portal.azure.com) al dispositivo. Se l'azione ha esito positivo, il dispositivo è gestito dalla nuova autorità MDM.  
    
- In caso di problemi con dispositivi specifici, annullare e ripetere la registrazione dei dispositivi. Questa operazione consente la connessione alla nuova autorità e fa sì che i dispositivi siano gestiti il più rapidamente possibile.  

- Se si è abilitato [Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client) come tenant ibrido e quindi è stata eseguita la migrazione del tenant a Intune autonomo, l'impostazione di Android for Work nelle restrizioni di registrazione può risultare bloccata anziché consentita. Impostarla manualmente su **Consenti** per abilitare nuovamente la registrazione di Android for Work.<!--512117-->  

- Dopo aver cambiato l'autorità MDM, il token VPP Apple e le [app iOS acquistate con Volume Purchase Program](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps) associate non vengono rimosse automaticamente. Per eseguire la pulizia di queste informazioni, seguire la procedura descritta in [Eliminare un token VPP di Apple](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps#delete-an-apple-vpp-token). Al termine dell'operazione, il sito rimuove il token. Rimuove anche gli eventuali metadati dell'applicazione per tale token dal nodo delle applicazioni dello Store con licenza.<!--SCCMDocs issue 579-->  

    In rari casi, potrebbe essere visualizzato un errore che indica che il sito non è riuscito a eliminare l'oggetto di gestione.  

    - Se il token non è visibile, ignorare l'errore  

    - Se il token è ancora elencato, riprovare a eliminarlo  

