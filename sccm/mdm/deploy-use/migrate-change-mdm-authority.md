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
ms.openlocfilehash: c7d39a8f9dfc6eee2e5600930208fd0202fb434b
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75520508"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Cambiare l'autorità MDM in Intune autonomo

*Si applica a: Configuration Manager (Current Branch)*    

È possibile modificare un tenant esistente di Microsoft Intune configurato dalla console di Configuration Manager (MDM ibrido) a Intune autonomo. L'impostazione di Intune come autorità MDM a livello di tenant è la fase finale del processo di [migrazione degli utenti e dei dispositivi MDM ibridi a Intune autonomo](migrate-hybridmdm-to-intunesa.md) nella configurazione solo cloud.    

> [!Important]    
> Per cambiare l'autorità MDM senza prima eseguire la migrazione degli utenti MDM ibridi a Intune, vedere [Cambiare l'autorità MDM](change-mdm-authority.md).

Questo articolo fornisce informazioni su come modificare un tenant di Microsoft Intune esistente configurato dalla console di Configuration Manager (ibrido) a Intune autonomo. Si presuppone che siano già stati completati i passaggi seguenti:
- Uso dello [strumento di importazione dei dati di Intune](migrate-import-data.md) per importare gli oggetti di Configuration Manager in Intune. 
- [Preparazione di Intune per la migrazione degli utenti](migrate-prepare-intune.md) per assicurarsi che gli utenti e i relativi dispositivi continuino a essere gestiti dopo la migrazione.
- [Modifica dell'autorità MDM per utenti specifici (autorità MDM mista)](migrate-mixed-authority.md) per iniziare a gestire i dispositivi utente dal portale di Azure.


## <a name="users-and-devices-that-havent-been-migrated"></a>Utenti e dispositivi di cui non è stata eseguita la migrazione
Sono già stati migrati molti utenti e sono state testate le funzionalità di Intune per assicurarsi che funzionino come previsto. Sono stati configurati criteri, profili e app in Intune ed è stato eseguito il test accurato degli oggetti nei dispositivi. Non dovrebbero essere necessarie nuove configurazioni per i criteri a livello di tenant dopo la modifica nell'autorità MDM. Tuttavia, per gli utenti e i dispositivi di cui non è stata eseguita la migrazione in precedenza, esaminare le informazioni seguenti su cosa aspettarsi dopo la modifica nell'autorità MDM:    

- È probabile che si verifichi un tempo di transizione di un massimo di otto ore prima che il dispositivo venga archiviato e sincronizzato con il servizio.  

- I dispositivi devono connettersi con il servizio dopo la modifica, in modo che le impostazioni dalla nuova autorità MDM (Intune autonomo) sostituiscano le impostazioni esistenti nel dispositivo.  

- Alcune delle impostazioni di base (ad esempio i profili) dell'autorità MDM precedente (ibrido) rimarranno nel dispositivo per un massimo di sette giorni.  

- Per i dispositivi senza utenti associati non viene eseguita la migrazione alla nuova autorità MDM. Questi dispositivi sono in genere con scenari per iOS Device Enrollment Program o per la registrazione in blocco. Per tali dispositivi è necessario chiamare il supporto tecnico per chiedere assistenza nel passaggio alla nuova autorità MDM.



## <a name="prerequisites"></a>Prerequisiti
Esaminare le informazioni seguenti per preparare il passaggio alla nuova autorità MDM:
- Perché sia disponibile l'opzione per cambiare l'autorità MDM è necessario disporre di Configuration Manager 1610 o versioni successive.
- Assicurarsi di assegnare una licenza di Intune/EMS a tutti gli utenti attualmente gestiti dalla soluzione MDM ibrida. La licenza garantisce che l'utente e i relativi dispositivi siano gestiti da Intune autonomo dopo la modifica nell'autorità MDM. Per altre informazioni, vedere [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Assegnare licenze di Intune agli account utente).
- Assicurarsi che all'account utente amministratore sia assegnata una licenza di Intune/EMS.

## <a name="change-the-mdm-authority-to-intune"></a>Cambiare l'autorità MDM in Intune
Usa la procedura seguente per modificare l'autorità MDM a livello di tenant in Intune.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** , espandere **servizi cloud**e selezionare il nodo **Microsoft Intune sottoscrizione** . Eliminare la sottoscrizione di Intune esistente.  

2. Selezionare **modifica autorità MDM in Microsoft Intune**, quindi selezionare **Avanti**.

    ![Finestra di dialogo Rimuovi la sottoscrizione di Microsoft Intune](media/mdm-change-delete-subscription.png)  

3. Accedere al tenant di Intune usato in origine quando è stata configurata l'autorità MDM in Configuration Manager. Selezionare **Avanti** e completare la procedura guidata.

    L'autorità MDM è ora reimpostata. La sottoscrizione a Intune non è più visualizzata nel nodo Sottoscrizioni a Microsoft Intune della console di Configuration Manager.  

4. Accedere al [portale di Intune](https://aka.ms/IntunePortal).

5. Selezionare **registrazione del dispositivo**.  

6. Nella panoramica della registrazione del dispositivo, vedere la proprietà dell' **autorità MDM** .

   > [!Important]    
   > Non usare la console classica di Intune. Accedere a Intune nella portale di Azure.  

7. Verificare che l'autorità MDM sia stata modificata in **Microsoft Intune**. 



## <a name="after-migration"></a>Dopo la migrazione

Una volta completata la modifica dell'autorità MDM, esaminare le informazioni seguenti:

- Durante il cambiamento nell'autorità MDM non vi sarà alcun impatto visibile sugli utenti finali.  

- Non è necessario riconfigurare i criteri a livello di tenant.  

- Se è necessario modificare i criteri a livello di tenant, eseguire questa azione da Intune nel portale di Azure.  

- In caso di problemi con dispositivi specifici, annullare e ripetere la registrazione dei dispositivi. Questa azione li ottiene connessi alla nuova autorità e viene gestita il più rapidamente possibile.


#### <a name="validate-new-device-enrollment"></a>Convalida nuova registrazione del dispositivo
Dopo aver modificato l'autorità MDM, attenersi alla procedura seguente per verificare che i nuovi dispositivi siano registrati correttamente per la nuova autorità:   
1. Registrare un nuovo dispositivo
2. Verificare che il dispositivo appena registrato sia visualizzato in Intune
3. Avviare un'azione del dispositivo dal portale di Intune, ad esempio [blocco remoto](https://docs.microsoft.com/intune/device-remote-lock). Se l'operazione ha esito positivo, il dispositivo viene gestito correttamente dalla nuova autorità MDM.


#### <a name="for-users-and-devices-that-you-havent-previously-migrated"></a>Per gli utenti e i dispositivi di cui non è stata eseguita la migrazione in precedenza

- Verificare che i dispositivi siano ora visualizzati nella pagina **dispositivi** come dispositivi gestiti. Prima di essere visualizzati, questi dispositivi devono archiviare e sincronizzare con il servizio dopo la modifica nell'autorità MDM. 

- Quando il servizio Intune rileva che l'autorità MDM di un tenant è cambiata, invia un messaggio di notifica a tutti i dispositivi registrati. Indica ai dispositivi di eseguire l'archiviazione e la sincronizzazione con il servizio. Questa notifica si verifica al di fuori dell'archiviazione periodicamente pianificata. Dopo aver cambiato l'autorità MDM per il tenant da ibrido a Intune autonomo, tutti i dispositivi online si connettono al servizio. Ricevono la nuova autorità MDM e quindi sono gestite da Intune standalone da ora in poi. Non ci sono interruzioni per la gestione e la protezione di questi dispositivi.

- Per i dispositivi offline durante o subito dopo la modifica nell'autorità MDM, si connettono e si sincronizzano con il servizio con la nuova autorità MDM quando sono accesi e online.  

- È possibile passare rapidamente alla nuova autorità MDM avviando manualmente un'archiviazione dal dispositivo al servizio. Usare l'app Portale aziendale per avviare un controllo di conformità del dispositivo.

- Quando un dispositivo è offline durante il cambiamento nell'autorità MDM e quando il dispositivo viene archiviato nel servizio, si verifica un periodo di tempo intermedio. Per assicurarsi che il dispositivo rimanga protetto e funzionale durante questo periodo, i profili seguenti rimangono nel dispositivo per un massimo di sette giorni. Possono anche rimanere fino a quando il dispositivo non si connette con la nuova autorità MDM e riceve nuove impostazioni che sovrascrivono quelle esistenti:
    - Profilo di posta elettronica
    - Profilo VPN
    - Profilo certificato
    - Profilo Wi-Fi
    - Profili di configurazione

- Per i dispositivi non associati a un utente, contattare il supporto tecnico per modificare l'autorità MDM. 

#### <a name="bkmk-ki-dep"></a>Record del dispositivo DEP Apple
<!--ICM 105091970-->
Dopo aver completato la migrazione dalla soluzione MDM ibrida, è possibile notare che i record dei dispositivi Apple DEP rimangono nella console di Configuration Manager. Dopo aver cambiato l'autorità MDM in Intune, non è possibile rimuovere questi dispositivi da Configuration Manager. 

Esistono due soluzioni alternative:

- Se viene visualizzato questo comportamento prima di cambiare l'autorità MDM, eliminare i record DEP dal Configuration Manager.  

- Se è già stata eseguita la migrazione e si usa ancora Configuration Manager, usare il comando SQL seguente nel database del sito per rimuovere i record:  

    ```SQL
    Delete from MDMCorpOwnedDevices where DeviceType=8 and DiscoverySources=4
    ```



## <a name="next-steps"></a>Passaggi successivi

Ora che la migrazione è stata completata, gestire i dispositivi mobili con Intune. Per ulteriori informazioni, vedere Novità [di Microsoft Intune](https://docs.microsoft.com/intune/whats-new).

