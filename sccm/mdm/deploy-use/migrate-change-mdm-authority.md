---
title: Impostare Intune come autorità MDM
titleSuffix: Configuration Manager
description: Informazioni su come cambiare l'autorità MDM da Configuration Manager (ibrido) a Intune autonomo.
author: aczechowski
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: b295dad503b801ff9d04767f75c1688107016d0b
ms.sourcegitcommit: 493cc42f05b9388ef872e466e5a75d569642b9fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2018
ms.locfileid: "34569681"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Cambiare l'autorità MDM in Intune autonomo

*Si applica a: System Center Configuration Manager (Current Branch)*    

È possibile modificare un tenant esistente di Microsoft Intune configurato dalla console di Configuration Manager (MDM ibrido) a Intune autonomo. L'impostazione di Intune come autorità MDM a livello di tenant è la fase finale del processo di [migrazione degli utenti e dei dispositivi MDM ibridi a Intune autonomo](migrate-hybridmdm-to-intunesa.md) nella configurazione solo cloud.    

> [!Important]    
> Per cambiare l'autorità MDM senza prima eseguire la migrazione degli utenti MDM ibridi a Intune, vedere [Cambiare l'autorità MDM](change-mdm-authority.md).

Questo articolo include informazioni su come modificare un tenant di Microsoft Intune esistente configurato dalla console di Configuration Manager (ibrido) a Intune autonomo e presuppone che siano già stati completati i passaggi seguenti:
- Uso dello [strumento di importazione dei dati di Intune](migrate-import-data.md) per importare gli oggetti di Configuration Manager in Intune. 
- [Preparazione di Intune per la migrazione degli utenti](migrate-prepare-intune.md) per assicurarsi che gli utenti e i relativi dispositivi continuino a essere gestiti dopo la migrazione.
- [Modifica dell'autorità MDM per utenti specifici (autorità MDM mista)](migrate-mixed-authority.md) per iniziare a gestire i dispositivi utente dal portale di Azure.


## <a name="users-and-devices-that-have-not-been-migrated"></a>Utenti e dispositivi di cui non è stata eseguita la migrazione
È già stata eseguita la migrazione di molti utenti e sono stati eseguiti test delle funzionalità di Intune per verificare che tutto funzioni come previsto. Di conseguenza, i criteri, i profili, le app e altri elementi sono stati configurati in Intune e sono stati testati accuratamente gli oggetti nei dispositivi. Non dovrebbero essere necessarie nuove configurazioni per i criteri a livello di tenant dopo la modifica nell'autorità MDM. Tuttavia, per gli utenti e i dispositivi di cui non è stata eseguita la migrazione in precedenza, vedere le seguenti informazioni su cosa aspettarsi dopo la modifica nell'autorità MDM:    
- È probabile che vi sia un tempo di transizione (fino a otto ore) prima dell'archiviazione del dispositivo e della sua sincronizzazione con il servizio.
- I dispositivi devono connettersi con il servizio dopo la modifica, in modo che le impostazioni dalla nuova autorità MDM (Intune autonomo) sostituiscano le impostazioni esistenti nel dispositivo.
- Alcune delle impostazioni di base (ad esempio i profili) dell'autorità MDM precedente (ibrido) rimarranno nel dispositivo per un massimo di sette giorni. 
- Per i dispositivi senza utenti associati (generalmente con il Device Enrollment Program per dispositivi iOS o scenari di registrazione in massa) non viene eseguita la migrazione alla nuova autorità MDM. Per tali dispositivi è necessario chiamare il supporto tecnico per chiedere assistenza nel passaggio alla nuova autorità MDM.

## <a name="prerequisites"></a>Prerequisiti
Esaminare le informazioni seguenti per preparare il passaggio alla nuova autorità MDM:
- Perché sia disponibile l'opzione per cambiare l'autorità MDM è necessario disporre di Configuration Manager 1610 o versioni successive.
- Assicurarsi che a tutti gli utenti attualmente gestiti da un'autorità MDM ibrida sia assegnata una licenza di Intune/EMS prima della modifica dell'autorità MDM. Questa licenza garantisce che l'utente e i suoi dispositivi siano gestiti da Intune autonomo dopo la modifica all'autorità MDM. Per altre informazioni, vedere [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Assegnare licenze di Intune agli account utente).
- Assicurarsi che all'account utente amministratore sia assegnata una licenza di Intune/EMS.

## <a name="change-the-mdm-authority-to-intune"></a>Cambiare l'autorità MDM in Intune
Usa la procedura seguente per modificare l'autorità MDM a livello di tenant in Intune.

1.  Nella console di Configuration Manager passare ad **Amministrazione** &gt; **Panoramica** &gt; **Servizi cloud** &gt; **Sottoscrizione a Microsoft Intune** ed eliminare la sottoscrizione a Intune esistente.
2.  Selezionare **Cambia l'autorità MDM in Microsoft Intune** e fare clic su **Avanti**.

    ![Finestra di dialogo Rimuovi la sottoscrizione di Microsoft Intune](media/mdm-change-delete-subscription.png)
3.  Accedere al tenant di Intune usato in origine quando è stata configurata l'autorità MDM in Configuration Manager.
4.  Fare clic su **Avanti** e completare la procedura guidata.
5.  L'autorità MDM è ora reimpostata. La sottoscrizione a Intune non è più visualizzata nel nodo Sottoscrizioni a Microsoft Intune della console di Configuration Manager.
6.  Accedere al [portale di Intune](https://aka.ms/IntunePortal).
7.  Nel pannello di Microsoft Intune fare clic su **Registrazione del dispositivo**.
8.  Nel pannello Panoramica di Registrazione del dispositivo vedere la proprietà **Autorità MDM**.

  > [!Important]    
  > Non usare la console di Intune classica. È necessario accedere a Intune nel portale di Azure.
7.  Verificare che l'autorità MDM sia stata modificata in **Microsoft Intune**. 

## <a name="next-steps"></a>Passaggi successivi
Una volta completata la modifica dell'autorità MDM, esaminare le informazioni seguenti:
- Durante il cambiamento nell'autorità MDM non vi sarà alcun impatto visibile sugli utenti finali. 
- Non è necessario riconfigurare i criteri a livello di tenant. 
- È possibile modificare i criteri a livello di tenant da Intune nel portale di Azure dopo la modifica nell'autorità MDM.
-  Dopo aver modificato l'autorità MDM, eseguire la procedura seguente per verificare che i nuovi dispositivi siano registrati correttamente con la nuova autorità:   
    - Registrare un nuovo dispositivo
    - Assicurarsi che il dispositivo appena registrato sia visualizzato in Intune.
    - Eseguire un'azione, ad esempio il blocco remoto, dalla console di amministrazione al dispositivo. Se l'azione ha esito positivo, il dispositivo è gestito dalla nuova autorità MDM.
- Nel caso di problemi con dispositivi specifici, è possibile annullare e ripetere la registrazione dei dispositivi in modo che siano connessi alla nuova autorità e gestiti il più rapidamente possibile.
- Per gli utenti e i dispositivi di cui non è stata eseguita la migrazione in precedenza:
    - Verificare che i dispositivi siano ora visualizzati nel pannello **Dispositivi** come dispositivi gestiti. Questi dispositivi devono collegarsi al servizio ed eseguire la sincronizzazione dopo la modifica nell'autorità MDM prima che vengano visualizzati. 
    - Quando il servizio Intune rileva che l'autorità MDM di un tenant è cambiata, invia un messaggio di notifica a tutti i dispositivi registrati per l'archiviazione e la sincronizzazione con il servizio (questo avviene al di fuori delle archiviazioni periodiche pianificate). Di conseguenza, dopo che l'autorità MDM per il tenant è stata cambiata da ibrida a Intune autonomo, tutti i dispositivi accesi e online si connettono al servizio, ricevono la nuova autorità MDM e da quel momento vengono gestiti da Intune autonomo. Non ci sono interruzioni per la gestione e protezione di questi dispositivi.
    - I dispositivi che sono spenti o non in linea durante (o immediatamente dopo) la modifica dell'autorità MDM si connettono e vengono sincronizzati con il servizio mediante la nuova autorità MDM quando sono nuovamente accesi e online.  
    - Gli utenti possono passare rapidamente alla nuova autorità MDM avviando manualmente un'archiviazione dal dispositivo al servizio. Gli utenti possono farlo facilmente usando l'app del Portale aziendale e avviando un controllo di conformità del dispositivo.
    - Quando un dispositivo è offline durante la modifica nell'autorità MDM e quando il dispositivo viene archiviato nel servizio si ha una situazione intermedia. Per garantire che il dispositivo rimanga protetto e funzionale durante questo periodo, i profili seguenti rimangono nel dispositivo per un massimo di sette giorni o fino a quando il dispositivo non si connette con la nuova autorità MDM e riceve le nuove impostazioni che sovrascrivono quelle esistenti:
        - Profilo di posta elettronica
        - Profilo VPN
        - Profilo certificato
        - Profilo Wi-Fi
        - Profili di configurazione
    - Contattare il supporto per modificare l'autorità MDM per i dispositivi non associati a un utente. 
