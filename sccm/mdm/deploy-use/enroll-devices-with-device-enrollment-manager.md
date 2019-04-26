---
title: 'Registrare i dispositivi con il manager di registrazione dispositivi '
titleSuffix: Configuration Manager
description: Registrare i dispositivi di proprietà dell'azienda usando l'account del manager di registrazione dispositivi con System Center Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 15ccbb201b7db02f51ccec322e5a320e143d8da3
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62227208"
---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>Registrare i dispositivi usando il manager di registrazione dispositivi con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le organizzazioni possono usare Intune per gestire un numero elevato di dispositivi mobili con un singolo account utente. L'account del *manager di registrazione dispositivi* è un account utente speciale usato per registrare i dispositivi. Aggiungendo utenti esistenti all'account del manager di registrazione dispositivi si assegnano loro particolari funzionalità. Ogni dispositivo registrato usa una singola licenza. È consigliabile usare i dispositivi registrati tramite questo account come dispositivi condivisi senza affinità utente anziché come dispositivi personali dedicati.  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>Registrare i dispositivi di proprietà dell'azienda con il manager di registrazione dispositivi  
 È possibile assegnare a un gestore del negozio o a un supervisore, ad esempio, un account di manager di registrazione dispositivi per consentire l'esecuzione delle operazioni seguenti:  

-   Registrare un massimo di 1000 dispositivi per la gestione  
-   Usare l'app Portale aziendale per installare le app aziendali  
-   Configurare l'accesso ai dati aziendali  

Le limitazioni seguenti si applicano ai dispositivi gestiti usando un account del manager di registrazione dispositivi:

- Il gestore del negozio non può reimpostare il dispositivo dal portale aziendale.  
- I dispositivi non possono essere aggiunti all'area di lavoro o ad Azure Active Directory. I dispositivi non possono quindi usare l'accesso condizionale.
- Per distribuire le app aziendali ai dispositivi gestiti con il manager di registrazione dispositivi, distribuire l'app Portale aziendale come **Installazione richiesta** all'account utente del manager di registrazione dispositivi. Il manager di registrazione dispositivi può quindi avviare l'app Portale aziendale per installare altre app.
- Per migliorare le prestazioni, nell'app Portale aziendale viene visualizzato solo il dispositivo locale. La gestione remota di altri dispositivi DEM è possibile solo dalla console di Configuration Manager e se ne può occupare l'amministratore
- Il sito Web del portale aziendale non è disponibile per gli account del manager di registrazione dispositivi. Usare l'app Portale aziendale.
- Se si usa il manager di registrazione dispositivi per registrare i dispositivi iOS, non è possibile usare Apple Configurator o Apple Device Enrollment Program (DEP) per registrare i dispositivi. (solo iOS) 

  **Esempi di scenario con il manager di registrazione dispositivi:**   
  Un ristorante vuole adottare tablet POS per il personale di sala e monitor per gli ordini per il personale di cucina. I dipendenti non hanno quindi bisogno di accedere a dati aziendali o di effettuare l'accesso come utente. L'amministratore di Intune crea un account di manager di registrazione dispositivi e registra i dispositivi di proprietà dell'azienda con tale account. In alternativa, l'amministratore potrebbe concedere le credenziali di manager di registrazione dispositivi a un responsabile del ristorante, per consentirgli di registrare e gestire i dispositivi.  

  L'amministratore o il manager può quindi distribuire app specifiche del ruolo nei dispositivi del ristorante. Un amministratore può anche selezionare un dispositivo nella console e disattivarlo nella gestione dei dispositivi mobili.  

#### <a name="add-a-device-enrollment-manager"></a>Aggiungere un manager di registrazione dispositivi  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Servizi cloud**e fare clic su **Sottoscrizioni a Microsoft Intune**. Selezionare la sottoscrizione a Microsoft Intune a cui viene aggiunto un manager di registrazione dispositivi e fare clic su **Proprietà**.  

3.  Nella finestra di dialogo Microsoft Intune Subscription Properties (Proprietà sottoscrizione di Microsoft Intune) fare clic sulla scheda **Manager di registrazione dispositivi**.  

4.  Fare clic su **Aggiungi/Rimuovi**.  

5.  Nella finestra di dialogo **Manager di registrazione dispositivi** digitare il nome dell'utente che si vuole aggiungere come manager di registrazione dispositivi e fare clic su **Cerca**. Selezionare l'utente da aggiungere come Manager di registrazione dispositivi e fare clic su **Aggiungi**.  

6.  Verificare l'account utente che verrà aggiunto come manager di registrazione dispositivi e fare clic su **Aggiungi/Rimuovi**.  È necessaria una licenza di sottoscrizione per ogni utente che accede al servizio. Il *manager di registrazione dispositivi* non può essere un amministratore di Intune. Determinare se è necessario aggiungere altre licenze prima di usare questa funzionalità.  

7.  Il manager di registrazione dispositivi ora può registrare i dispositivi mobili usando la stessa procedura usata da un utente finale per uno scenario BYOD (Bring Your Own Device) nel portale aziendale.  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>Eliminare un manager di registrazione dispositivi da Intune  
L'eliminazione di un manager di registrazione dispositivi non influisce sui dispositivi registrati. Quando viene eliminato un manager di registrazione dispositivi:  
- Non viene annullata la registrazione dei dispositivi registrati  
- I dispositivi registrati continuano a essere completamente gestiti  
- Le credenziali dell'account del manager di registrazione dispositivi eliminato restano valide per collegarsi al portale aziendale per l'accesso alle app  
- Le credenziali dell'account del manager di registrazione dispositivi eliminato non possono ancora cancellare o disattivare i dispositivi  
- La relazione dell'account del manager di registrazione dispositivi per eliminato con i dispositivi registrati resta valida, ma non è possibile registrare ulteriori dispositivi

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  
2.  Nell'area di lavoro **Amministrazione** espandere **Servizi cloud**e fare clic su **Sottoscrizioni a Microsoft Intune**. Selezionare la sottoscrizione a Microsoft Intune a cui viene aggiunto un manager di registrazione dispositivi e fare clic su **Proprietà**.  
3.  Nella finestra di dialogo Microsoft Intune Subscription Properties (Proprietà sottoscrizione di Microsoft Intune) fare clic sulla scheda **Manager di registrazione dispositivi**.  
4.  **Cercare** il manager di registrazione dispositivi da eliminare, fare clic su **Rimuovi** e su **OK**.  
