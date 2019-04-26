---
title: Impostare Intune come autorità MDM
titleSuffix: Configuration Manager
description: Informazioni su come cambiare l'autorità MDM da Configuration Manager (ibrido) a Intune autonomo.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d6a909be4b1817b9a251046d666839e2e351443
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62282168"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Cambiare l'autorità MDM in Intune autonomo

*Si applica a: System Center Configuration Manager (Current Branch)*    

È possibile modificare un tenant esistente di Microsoft Intune configurato dalla console di Configuration Manager (MDM ibrido) a Intune autonomo. L'impostazione di Intune come autorità MDM a livello di tenant è la fase finale del processo di [migrazione degli utenti e dei dispositivi MDM ibridi a Intune autonomo](migrate-hybridmdm-to-intunesa.md) nella configurazione solo cloud.    

> [!Important]    
> Per cambiare l'autorità MDM senza prima eseguire la migrazione degli utenti MDM ibridi a Intune, vedere [Cambiare l'autorità MDM](change-mdm-authority.md).

Questo articolo fornisce informazioni su come modificare un tenant di Microsoft Intune esistente configurato dalla console di Configuration Manager (ibrido) a Intune autonomo. Si presuppone di che aver già completato i passaggi seguenti:
- Uso dello [strumento di importazione dei dati di Intune](migrate-import-data.md) per importare gli oggetti di Configuration Manager in Intune. 
- [Preparazione di Intune per la migrazione degli utenti](migrate-prepare-intune.md) per assicurarsi che gli utenti e i relativi dispositivi continuino a essere gestiti dopo la migrazione.
- [Modifica dell'autorità MDM per utenti specifici (autorità MDM mista)](migrate-mixed-authority.md) per iniziare a gestire i dispositivi utente dal portale di Azure.


## <a name="users-and-devices-that-havent-been-migrated"></a>Utenti e dispositivi che non è stata eseguita la migrazione
Già eseguita la migrazione di molti utenti e testato la funzionalità di Intune per assicurarsi che tutto funzioni come previsto. Si è configurato i criteri, profili e le App in Intune e testata accuratamente gli oggetti nei dispositivi. Non dovrebbero essere necessarie nuove configurazioni per i criteri a livello di tenant dopo la modifica nell'autorità MDM. Tuttavia, per gli utenti e dispositivi che non hanno precedentemente migrati, esaminare le informazioni seguenti su cosa aspettarsi dopo la modifica nell'autorità MDM:    

- È probabile che un tempo di transizione fino a otto ore prima che il dispositivo e della sua sincronizzazione con il servizio.  

- I dispositivi devono connettersi con il servizio dopo la modifica, in modo che le impostazioni dalla nuova autorità MDM (Intune autonomo) sostituiscano le impostazioni esistenti nel dispositivo.  

- Alcune delle impostazioni di base (ad esempio i profili) dell'autorità MDM precedente (ibrido) rimarranno nel dispositivo per un massimo di sette giorni.  

- Per i dispositivi senza utenti associati non viene eseguita la migrazione alla nuova autorità MDM. Questi dispositivi sono in genere con gli scenari per iOS Device Enrollment Program o con registrazione in blocco. Per tali dispositivi è necessario chiamare il supporto tecnico per chiedere assistenza nel passaggio alla nuova autorità MDM.



## <a name="prerequisites"></a>Prerequisiti
Esaminare le informazioni seguenti per preparare il passaggio alla nuova autorità MDM:
- Perché sia disponibile l'opzione per cambiare l'autorità MDM è necessario disporre di Configuration Manager 1610 o versioni successive.
- Assicurarsi di assegnare una licenza Intune o EMS a tutti gli utenti attualmente gestiti da MDM ibrida. La licenza garantisce che l'utente e i suoi dispositivi siano gestiti da Intune autonomo dopo la modifica nell'autorità MDM. Per altre informazioni, vedere [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Assegnare licenze di Intune agli account utente).
- Assicurarsi che all'account utente amministratore sia assegnata una licenza di Intune/EMS.

## <a name="change-the-mdm-authority-to-intune"></a>Cambiare l'autorità MDM in Intune
Usa la procedura seguente per modificare l'autorità MDM a livello di tenant in Intune.

1. Nella console di Configuration Manager passare ad il **Administration** dell'area di lavoro, espandere **servizi Cloud**e selezionare il **sottoscrizione a Microsoft Intune** nodo. Eliminare la sottoscrizione di Intune esistente.  

2. Selezionare **cambia l'autorità MDM in Microsoft Intune**, quindi selezionare **successivo**.

    ![Finestra di dialogo Rimuovi la sottoscrizione di Microsoft Intune](media/mdm-change-delete-subscription.png)  

3. Accedere al tenant di Intune usato in origine quando è stata configurata l'autorità MDM in Configuration Manager. Selezionare **successivo** e completare la procedura guidata.

    L'autorità MDM è ora reimpostata. La sottoscrizione a Intune non è più visualizzata nel nodo Sottoscrizioni a Microsoft Intune della console di Configuration Manager.  

4. Accedi per il [portale di Intune](https://aka.ms/IntunePortal).

5. Selezionare **registrazione del dispositivo**.  

6. La registrazione di dispositivi panoramica, vedere la **autorità MDM** proprietà.

   > [!Important]    
   > Non usare la console classica di Intune. Accedere a Intune nel portale di Azure.  

7. Verificare che l'autorità MDM sia stata modificata in **Microsoft Intune**. 



## <a name="after-migration"></a>Dopo la migrazione

Una volta completata la modifica dell'autorità MDM, esaminare le informazioni seguenti:

- Durante il cambiamento nell'autorità MDM non vi sarà alcun impatto visibile sugli utenti finali.  

- Non è necessario riconfigurare i criteri a livello di tenant.  

- Se è necessario modificare i criteri a livello di tenant, eseguire questa azione da Intune nel portale di Azure.  

- In caso di problemi con dispositivi specifici, annullare e ripetere la registrazione dei dispositivi. Questa azione Ottiene siano connessi alla nuova autorità e gestiti nel minor tempo.


#### <a name="validate-new-device-enrollment"></a>Convalidare nuova registrazione del dispositivo
Dopo aver cambiato l'autorità MDM, è possibile usare la procedura seguente per convalidare che i nuovi dispositivi siano registrati correttamente con la nuova autorità:   
1. Registrare un nuovo dispositivo
2. Assicurarsi che il dispositivo appena registrato visualizzato in Intune
3. Avviare un'azione del dispositivo dal portale di Intune, ad esempio [blocco remoto](https://docs.microsoft.com/intune/device-remote-lock). Se ha esito positivo, il dispositivo è gestito correttamente dalla nuova autorità MDM.


#### <a name="for-users-and-devices-that-you-havent-previously-migrated"></a>Per gli utenti e dispositivi che non è stata precedentemente eseguita la migrazione

- Verificare che i dispositivi sono ora visualizzati nel **dispositivi** pagina come dispositivi gestiti. Prima di visualizzarlo, questi dispositivi devono archiviare ed eseguire la sincronizzazione con il servizio dopo la modifica nell'autorità MDM. 

- Quando il servizio Intune rileva che l'autorità MDM di un tenant è cambiata, invia un messaggio di notifica a tutti i dispositivi registrati. Indica ai dispositivi di archiviazione e la sincronizzazione con il servizio. Questa notifica viene eseguita all'esterno del controllo aggiuntivo regolarmente pianificato. Dopo aver cambiato l'autorità MDM per il tenant da ibrida a Intune autonomo, tutti i dispositivi online si connettono con il servizio. Si riceveranno la nuova autorità MDM e quindi vengono gestiti da Intune autonomo nel. Non vi è alcuna interruzione per la gestione e protezione di questi dispositivi.

- Per i dispositivi sono offline durante o immediatamente dopo la modifica nell'autorità MDM, collegati ed eseguire la sincronizzazione con il servizio mediante la nuova autorità MDM quando è possibile accendere e online.  

- È possibile passare rapidamente alla nuova autorità MDM avviando manualmente un'archiviazione dal dispositivo al servizio. Usare l'app portale aziendale per avviare un controllo di conformità.

- È una situazione intermedia quando un dispositivo è offline durante la modifica nell'autorità MDM e quando tale dispositivo viene archiviato nel servizio. Per assicurarsi che il dispositivo rimanga protetto e funzionale durante questo periodo, i profili seguenti rimarranno sul dispositivo fino a sette giorni. Possono anche rimanere fino a quando il dispositivo si connette con la nuova autorità MDM e riceve le nuove impostazioni che sovrascriveranno quelle esistenti:
    - Profilo di posta elettronica
    - Profilo VPN
    - Profilo certificato
    - Profilo Wi-Fi
    - Profili di configurazione

- Per i dispositivi che non sono associati a un utente, contattare il supporto per modificare l'autorità MDM. 

#### <a name="bkmk-ki-dep"></a> Record dei dispositivi DEP di Apple
<!--ICM 105091970-->
Dopo aver completato la migrazione da MDM ibrido, è possibile notare un dispositivo Apple DEP record rimangono nelle console di Configuration Manager. Dopo aver cambiato l'autorità MDM a Intune, è possibile rimuovere questi dispositivi da Configuration Manager. 

Esistono due soluzioni alternative:

- Se viene visualizzato questo comportamento prima di cambiare l'autorità MDM, quindi eliminare i record DEP da Configuration Manager.  

- Se già stata eseguita la migrazione e sta ancora usando Configuration Manager, usare il comando SQL seguente sul database del sito per rimuovere i record:  

    ```SQL
    Delete from MDMCorpOwnedDevices where DeviceType=8 and DiscoverySources=4
    ```



## <a name="next-steps"></a>Passaggi successivi

Ora che la migrazione è completata, gestire i dispositivi mobili con Intune. Per altre informazioni, vedere [quali sono le novità in Microsoft Intune](https://docs.microsoft.com/intune/whats-new).

