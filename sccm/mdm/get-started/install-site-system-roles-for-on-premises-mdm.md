---
title: 'Installare ruoli per la gestione di dispositivi mobili locale '
titleSuffix: Configuration Manager
description: Installare i ruoli del sistema del sito per la gestione di dispositivi mobili locale in System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5d81d385c48d9653e1596e6a5d9d1163e84f314
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62216256"
---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Installare i ruoli del sistema del sito per la gestione dei dispositivi mobili (MDM) locale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La gestione di dispositivi mobili locale di System Center Configuration Manager richiede i ruoli del sistema del sito seguenti all'interno dell'infrastruttura del sito di Configuration Manager:  

- Punto di registrazione  

- Punto proxy di registrazione  

- Punto di distribuzione  

- Punto di gestione dei dispositivi  

- punto di connessione del servizio  

  Se si sta aggiungendo la gestione di dispositivi mobili locale a un'organizzazione in cui la maggior parte dei PC e dei dispositivi è gestita tramite il software client di Configuration Manager, la maggior parte dei ruoli del sistema del sito potrebbe essere già installata nell'ambito dell'infrastruttura esistente. In caso contrario, vedere [Add site system roles for System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md) (Aggiungere ruoli del sistema del sito per System Center Configuration Manager) per informazioni complete su come aggiungere i ruoli al sito.  

> [!NOTE]  
>  Se si usano le repliche di database con il ruolo di sistema del sito punto gestione periferiche, i nuovi dispositivi registrati non riusciranno inizialmente a connettersi al punto gestione periferiche, fino al completamento della sincronizzazione della replica di database. Questo errore di connessione si verifica perché la replica di database non include le informazioni sul nuovo dispositivo registrato necessarie per attivare correttamente la connessione. Le repliche vengono sincronizzate ogni 5 minuti, quindi i dispositivi non riusciranno a connettersi per i primi 5 minuti dopo la registrazione (in genere 2 tentativi di connessione). Trascorso questo tempo, la connessione verrà attivata correttamente.  

 Che si stiano usando ruoli del sistema del sito esistenti o aggiungendone di nuovi, è necessario configurarli perché possano essere usati per gestire i dispositivi moderni. Attenersi alla procedura seguente per configurare il punto di distribuzione e il punto di gestione dei dispositivi per il corretto funzionamento della gestione di dispositivi mobili locale:  

> [!NOTE]  
>  Il ramo corrente di Configuration Manager supporta solo le connessioni Intranet dai dispositivi ai punti di distribuzione e di gestione dei dispositivi per la gestione dei dispositivi mobili locale. Se tuttavia si gestiscono anche computer Mac OS X, questi client richiedono connessioni Internet a tali ruoli del sistema del sito. In tal caso, quando si configurano le proprietà del punto di distribuzione e del punto di gestione dei dispositivi, è necessario usare l'impostazione **Consenti connessioni intranet e Internet**.  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>Per configurare i ruoli del sistema del sito per la gestione dei dispositivi moderni:  

1. Nella console di Configuration Manager fare clic su **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito**.  

2. Selezionare il server del sistema del sito con il punto di distribuzione o il punto di gestione dei dispositivi che si vuole configurare, aprire le proprietà per **Sistema del sito** e verificare che sia specificato un nome FQDN. Fare clic su **OK**.  

3. Aprire le proprietà per il ruolo del sistema del sito del punto di distribuzione. Nella scheda Generale verificare che sia selezionato **HTTPS** e selezionare **Consenti solo connessioni intranet**.  

    Se con il client di Configuration Manager si gestiscono separatamente anche computer Mac, usare **Consenti connessioni intranet e Internet**.  

   > [!NOTE]  
   >  I punti di distribuzione configurati per le connessioni Intranet richiedono che i limiti del sito siano configurati per loro. Current Branch di Configuration Manager supporta i limiti degli intervalli IPv4 solo per la gestione di dispositivi mobili locale. Per altre informazioni sulla configurazione di limiti del sito, vedere [Define site boundaries and boundary groups for System Center Configuration Manager](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md) (Definire i limiti del sito e i gruppi di limiti per System Center Configuration Manager).  

4. Fare clic sulla casella di controllo accanto a **Consenti ai dispositivi mobili di connettersi a questo punto di distribuzione** e quindi fare clic su **OK**.  

5. Aprire le proprietà per il ruolo del sistema del sito del punto di gestione. Nella scheda Generale verificare che sia selezionato **HTTPS** e selezionare **Consenti solo connessioni intranet**.  

    Se con il client di Configuration Manager si gestiscono separatamente anche computer Mac, usare **Consenti connessioni intranet e Internet**.  

6. Fare clic sulla casella di controllo accanto a **Consenti ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione**. Fare clic su **OK**.  

    Questo consente di trasformare il punto di gestione in un punto di gestione dei dispositivi.  

   Una volta aggiunti e configurati i ruoli del sistema del sito per la gestione dei dispositivi moderni, è necessario configurare i server che ospitano i ruoli come endpoint di tipo trusted per la registrazione e la comunicazione con i dispositivi gestiti. Per altre informazioni, vedere [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md) (Configurazione di certificati per comunicazioni attendibili per la gestione di dispositivi mobili locale in System Center Configuration Manager).  
