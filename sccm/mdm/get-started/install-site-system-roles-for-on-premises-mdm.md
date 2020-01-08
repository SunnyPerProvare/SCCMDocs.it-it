---
title: 'Installare ruoli per la gestione di dispositivi mobili locale '
titleSuffix: Configuration Manager
description: Installare i ruoli del sistema del sito per la gestione dei dispositivi mobili locale in Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49a3d8722d3ad238b7f8fa417bd0eb47e1cda056
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75519573"
---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-configuration-manager"></a>Installare i ruoli del sistema del sito per la gestione dei dispositivi mobili locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager nella gestione dei dispositivi mobili\-locale richiede i seguenti ruoli del sistema del sito nell'infrastruttura del sito di Configuration Manager:  

- Punto di registrazione  

- Punto proxy di registrazione  

- Punto di distribuzione  

- Punto di gestione dei dispositivi  

- Punto di connessione del servizio  

  Se si sta aggiungendo la gestione di dispositivi mobili locale a un'organizzazione in cui la maggior parte dei PC e dei dispositivi è gestita tramite il software client di Configuration Manager, la maggior parte dei ruoli del sistema del sito potrebbe essere già installata nell'ambito dell'infrastruttura esistente. In caso contrario, vedere [aggiungere ruoli del sistema del sito per Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md) per informazioni complete su come aggiungerli al sito.  

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
   >  I punti di distribuzione configurati per le connessioni Intranet richiedono che i limiti del sito siano configurati per loro. Current Branch di Configuration Manager supporta i limiti degli intervalli IPv4 solo per la gestione di dispositivi mobili locale. Per ulteriori informazioni sulla configurazione dei limiti del sito, vedere [definire i limiti del sito e i gruppi di limiti per Configuration Manager](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

4. Fare clic sulla casella di controllo accanto a **Consenti ai dispositivi mobili di connettersi a questo punto di distribuzione** e quindi fare clic su **OK**.  

5. Aprire le proprietà per il ruolo del sistema del sito del punto di gestione. Nella scheda Generale verificare che sia selezionato **HTTPS** e selezionare **Consenti solo connessioni intranet**.  

    Se con il client di Configuration Manager si gestiscono separatamente anche computer Mac, usare **Consenti connessioni intranet e Internet**.  

6. Fare clic sulla casella di controllo accanto a **Consenti ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione**. Fare clic su **OK**.  

    Questo consente di trasformare il punto di gestione in un punto di gestione dei dispositivi.  

   Una volta aggiunti e configurati i ruoli del sistema del sito per la gestione dei dispositivi moderni, è necessario configurare i server che ospitano i ruoli come endpoint di tipo trusted per la registrazione e la comunicazione con i dispositivi gestiti. Per altre informazioni, vedere [configurare i certificati per le comunicazioni attendibili per la gestione dei dispositivi mobili locale](../../mdm/get-started/set-up-certificates-on-premises-mdm.md) .  
