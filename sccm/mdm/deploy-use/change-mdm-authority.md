---
title: "Modificare l'autorità MDM"
titleSuffix: Configuration Manager
description: "Informazioni su come modificare l'autorità MDM da Configuration Manager (ibrido) a Intune autonomo"
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/17/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: c61a44cce443a7ff210a626d114068691541aaae
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="change-your-mdm-authority"></a>Modificare l'autorità MDM
A partire dalla versione 1610 di Configuration Manager, è possibile cambiare l'autorità MDM senza bisogno di contattare il supporto tecnico Microsoft e senza dover annullare e ripetere la registrazione dei dispositivi gestiti esistenti. Questo articolo descrive i passaggi necessari per modificare un tenant esistente di Microsoft Intune configurato dalla console di Configuration Manager (ibrido) alla versione autonoma di Intune. Dopo aver completato i passaggi descritti in questo articolo, i dispositivi verranno gestiti da Microsoft Intune nel [portale di Azure](https://portal.azure.com). 

> [!Note]    
> Se si vuole modificare un tenant di Microsoft Intune esistente, con l'autorità MDM impostata su Intune, a Configuration Manager (ibrido), vedere [Cambiare l'autorità MDM](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority).

> [!Important]    
> Questo articolo descrive la modifica dell'autorità MDM quando non è stata eseguita la migrazione di utenti in precedenza. Per cambiare l'autorità MDM dopo aver eseguito la [migrazione di un subset di utenti](migrate-hybridmdm-to-intunesa.md), vedere [Cambiare l'autorità MDM](migrate-change-mdm-authority.md).

## <a name="key-considerations"></a>Considerazioni principali
Dopo il passaggio alla nuova autorità MDM, è probabile che ci sia un tempo di transizione (fino a otto ore) prima dell'archiviazione del dispositivo e della sua sincronizzazione con il servizio. È necessario configurare le impostazioni nella nuova autorità MDM (Intune autonomo) per garantire che i dispositivi registrati continuino a essere gestiti e protetti dopo la modifica. Tenere presenti le seguenti considerazioni:
- I dispositivi devono connettersi con il servizio dopo la modifica, in modo che le impostazioni dalla nuova autorità MDM (versione autonoma di Intune) sostituiscano le impostazioni esistenti nel dispositivo.
- Dopo aver cambiato l'autorità MDM, alcune delle impostazioni di base (ad esempio i profili) dell'autorità MDM precedente (ibrido) rimarranno sul dispositivo per un massimo di sette giorni. È consigliabile configurare app e impostazioni (criteri, profili, app e così via) nella nuova autorità MDM non appena possibile. Inoltre, distribuire le impostazioni ai gruppi di utenti che contengono gli utenti con dispositivi registrati esistenti. Quando un dispositivo si connette al servizio dopo la modifica all'autorità MDM, riceve nuove impostazioni dalla nuova autorità MDM. Tutti i nuovi criteri di destinazione sostituiranno i criteri esistenti nel dispositivo.
- Dopo il passaggio alla nuova autorità MDM, i dati di conformità nel [portale di Azure](https://portal.azure.com) possono richiedere fino a una settimana prima di fornire una segnalazione accurata. Tuttavia, gli stati di conformità in Azure Active Directory e nel dispositivo saranno accurati e il dispositivo sarà comunque protetto.
- Per i dispositivi senza utenti associati (generalmente con il Device Enrollment Program per dispositivi iOS o scenari di registrazione in massa) non viene eseguita la migrazione alla nuova autorità MDM. Per tali dispositivi è necessario chiamare il supporto tecnico per chiedere assistenza nel passaggio alla nuova autorità MDM.

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparare il cambiamento dell'autorità MDM in Intune autonomo
Esaminare le informazioni seguenti per preparare il passaggio alla nuova autorità MDM:
- Perché sia disponibile l'opzione per cambiare l'autorità MDM è necessario disporre di Configuration Manager 1610 o versioni successive.
- Prima che un dispositivo si connetta al servizio dopo il passaggio alla nuova autorità MDM possono trascorrere fino a otto ore.
- Assicurarsi che a tutti gli utenti attualmente gestiti in modo ibrido sia assegnata una licenza Intune o EMS prima del passaggio all'autorità MDM. Questa licenza garantisce che l'utente e i suoi dispositivi siano gestiti da Intune autonomo dopo la modifica all'autorità MDM. Per altre informazioni, vedere [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Assegnare licenze di Intune agli account utente).
- Assicurarsi che all'account utente amministratore sia assegnata una licenza Intune o EMS e verificare che l'account utente amministratore possa accedere a Intune prima di cambiare l'autorità MDM. Prima della modifica dell'autorità MDM, nel **portale di Azure** deve essere visualizzato [Imposta su Configuration Manager](https://portal.azure.com) (tenant ibrido) in Intune.
- Durante il cambiamento nell'autorità MDM non vi sarà alcun impatto visibile sugli utenti finali. 

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Cambiare l'autorità MDM in Intune autonomo
La procedura per cambiare l'autorità MDM in Intune autonomo include i passaggi generali seguenti:  
- Nella console di Configuration Manager usare l'opzione **Cambia l'autorità MDM in Microsoft Intune** per rimuovere la sottoscrizione a Microsoft Intune esistente.
- Nel [portale di Azure](https://portal.azure.com) in Intune configurare e distribuire le nuove impostazioni e app dalla nuova autorità MDM (Intune).
- I dispositivi, alla successiva connessione al servizio, saranno sincronizzati e riceveranno le nuove impostazioni dalla nuova autorità MDM.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Per cambiare l'autorità MDM in Intune autonomo
1. Nella console di Configuration Manager passare ad **Amministrazione** &gt; **Panoramica** &gt; **Servizi cloud** &gt; **Sottoscrizione a Microsoft Intune** ed eliminare la sottoscrizione a Intune esistente.
2. Selezionare **Cambia l'autorità MDM in Microsoft Intune** e fare clic su **Avanti**.
   ![Scaricare la richiesta di certificato APNs](./media/mdm-change-delete-subscription.png)
3. Accedere al tenant di Intune usato in origine quando è stata configurata l'autorità MDM in Configuration Manager.
4. Fare clic su **Avanti** e completare la procedura guidata.
5. L'autorità MDM è ora impostata su **Microsoft Intune**. La sottoscrizione a Intune non dovrebbe più essere visualizzata nel nodo Sottoscrizioni a Microsoft Intune della console di Configuration Manager. 
6. Per verificare che l'autorità MDM sia impostata, procedere in questo modo: a. Accedere al [portale di Azure](https://portal.azure.com) usando lo stesso tenant di Intune usato in precedenza. 
    b. Scegliere **Altri servizi** > **Monitoraggio e gestione** > **Intune** > **Registrazione del dispositivo**. L'autorità MDM viene visualizzata nella sezione in alto a destra del pannello **Panoramica**. 

## <a name="next-steps"></a>Passaggi successivi
Una volta completata la modifica dell'autorità MDM, esaminare i passaggi seguenti:
- Quando il servizio Intune rileva che l'autorità MDM di un tenant è stata modificata, invia un messaggio di notifica a tutti i dispositivi registrati per l'archiviazione e la sincronizzazione con il servizio (questo avviene al di fuori delle archiviazioni regolarmente pianificate). Di conseguenza, dopo che l'autorità MDM per il tenant è stata cambiata da ibrida ad Intune autonomo, tutti i dispositivi accesi e in linea si connetteranno con il servizio, riceveranno la nuova autorità MDM e da quel momento saranno gestiti da Intune autonomo. Non ci saranno interruzioni alla gestione e protezione di questi dispositivi.
- I dispositivi che sono spenti o non in linea durante (o immediatamente dopo) la modifica dell'autorità MDM si connettono e vengono sincronizzati con il servizio mediante la nuova autorità MDM quando sono nuovamente accesi e online.  
- Gli utenti possono passare rapidamente alla nuova autorità MDM avviando manualmente un'archiviazione dal dispositivo al servizio. Gli utenti possono farlo facilmente usando l'app del portale aziendale e avviando un controllo di conformità del dispositivo.
- Per verificare che tutto funzioni correttamente dopo che i dispositivi sono stati archiviati e sincronizzati con il servizio dopo la modifica dell'autorità MDM, cercare i dispositivi nel [portale di Azure](https://portal.azure.com). I dispositivi che in precedenza sono stati gestiti da Configuration Manager (ibrido) verranno ora visualizzati come dispositivi gestiti in Intune.    
- Quando un dispositivo è offline durante la modifica nell'autorità MDM e quando il dispositivo viene archiviato nel servizio si ha una situazione intermedia. Per garantire che il dispositivo resti protetto e funzionale durante questo periodo, i profili seguenti rimarranno nel dispositivo per un massimo di sette giorni (o fino a quando il dispositivo non si connette con la nuova autorità MDM e riceve le nuove impostazioni che sovrascriveranno quelle esistenti):
    - Profilo di posta elettronica
    - Profilo VPN
    - Profilo certificato
    - Profilo Wi-Fi
    - Profili di configurazione
- Verificare che le nuove impostazioni che devono sovrascrivere quelle esistenti abbiano lo stesso nome delle precedenti per garantire che le impostazioni precedenti vengano sovrascritte. In caso contrario, i dispositivi potrebbero finire con criteri e profili ridondanti.    

  > [!TIP]   
  > Come procedura consigliata è necessario creare tutte le impostazioni di gestione e le configurazioni, nonché le distribuzioni, subito dopo aver completato la modifica dell'autorità MDM. In questo modo, si garantirà che i dispositivi siano protetti e gestiti attivamente durante il periodo intermedio.   
-  Dopo aver modificato l'autorità MDM, eseguire la procedura seguente per verificare che i nuovi dispositivi siano registrati correttamente con la nuova autorità:   
    - Registrare un nuovo dispositivo
    - Assicurarsi che il dispositivo appena registrato sia visualizzato nel [portale di Azure](https://portal.azure.com).
    - Eseguire un'azione, ad esempio il blocco remoto, dal [portale di Azure](https://portal.azure.com) al dispositivo. Se l'azione ha esito positivo, il dispositivo è gestito dalla nuova autorità MDM.
- Nel caso di problemi con dispositivi specifici, è possibile annullare e ripetere la registrazione dei dispositivi in modo che siano connessi alla nuova autorità e gestiti il più rapidamente possibile.