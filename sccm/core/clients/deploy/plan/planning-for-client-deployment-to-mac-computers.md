---
title: Pianificazione della distribuzione client per computer Mac
titleSuffix: Configuration Manager
description: Pianificazione della distribuzione del client in computer Mac in System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe9c5a22f1c3a17737ccfb452b3cd4dd418bf9a9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142460"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-system-center-configuration-manager"></a>Pianificazione della distribuzione del client in computer Mac in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile installare il client di Configuration Manager su computer Mac con sistema operativo Mac OS X e usare le funzionalità di gestione seguenti:  

- **Inventario hardware**  

   È possibile usare l'inventario hardware di Configuration Manager per raccogliere informazioni sull'hardware e sulle applicazioni installate sui computer Mac. Tali informazioni possono essere visualizzate in Esplora inventario risorse nella console di Configuration Manager e usate per creare raccolte, query e report. Per altre informazioni, vedere [Come usare Esplora inventario risorse per visualizzare l'inventario hardware in Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   Configuration Manager raccoglie le informazioni hardware seguenti dai computer Mac:  

  -   Processore  

  -   Sistema computer  

  -   Unità disco  

  -   Partizione disco  

  -   Scheda di rete  

  -   Sistema operativo  

  -   Service  

  -   Processo  

  -   Software installato  

  -   Prodotto di sistema  

  -   Controller USB  

  -   Dispositivo USB  

  -   Unità CD-ROM  

  -   Controller video  

  -   Monitor da tavolo  

  -   Batteria portatile  

  -   Memoria fisica  

  -   Stampante  

  > [!IMPORTANT]  
  >  Non è possibile estendere le informazioni hardware raccolte dai computer Mac durante l'inventario hardware.  

- **Impostazioni di conformità**  

   È possibile usare le impostazioni di conformità di Configuration Manager per visualizzarne la conformità e correggere le impostazioni di preferenza di Mac OS X (file con estensione plist). Ad esempio, si potrebbero applicare le impostazioni per la home page del browser Web Safari oppure assicurarsi che il firewall Apple sia abilitato. È inoltre possibile usare gli script della shell per monitorare e correggere le impostazioni in MAC OS X.  

- **Gestione delle applicazioni**  

   Configuration Manager può distribuire software nei computer Mac. È possibile distribuire i seguenti formati di software nei computer Mac:  

  -   Immagine disco Apple (.DMG)  

  -   File meta pacchetto (.MPKG)  

  -   Pacchetto di Mac OS X Installer (.PKG)  

  -   Applicazione di Mac OS X (.APP)  

  Quando si installa il client di Configuration Manager in computer Mac, non è possibile usare le funzionalità di gestione seguenti supportate dal client di Configuration Manager in computer Windows:  

- Installazione push client  

- Distribuzione del sistema operativo  

- Aggiornamenti software  

  > [!NOTE]  
  >  È possibile usare la gestione applicazioni di Configuration Manager per distribuire gli aggiornamenti software Mac OS X necessari ai computer Mac. Inoltre, è possibile usare le impostazioni di conformità per assicurarsi che i computer abbiano tutti gli aggiornamenti software necessari.  

- Finestre di manutenzione  

- Controllo remoto  

- Risparmio energia  

- Controllo e correzione client dello stato client  

  Per altre informazioni su come installare e configurare il client Mac di Configuration Manager, vedere [Come distribuire i client a computer Mac in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md).
